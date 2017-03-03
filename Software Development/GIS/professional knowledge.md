#GIS专业术语#

1. zoom： 伸缩放大
2. projection： 投影标准，决定地图坐标系
3. Feature：要素，是空间数据最基本、不可分割的单位，有点、线、面等，可根据应用需要，用点状符号、线型、面状填充图案加边界线表达。每一个Feature都有自己的属性，存放在属性表中，和表中的一行相对应。
4. Feature Class：要素类（相同类型的要素类型聚集在一起），一个要素类一般和一个属性表相对应。
5. Layer：图层，每一个图层都由同一类型的Feature组成，如点状图层数据来自点状要素类，线状图层来自线状要素类，面状图层来自多边形要素类。
6. Table：属性表，由若干列与若干行组成，每列代表一种属性（字段），属性有自己的名称，每一行代表一条记录，在行与列的交叉处是属性单元。
7. Data Frame：数据框架，将多个图层、属性表汇集在一起。在ArcMap窗口中，左侧是数据框架的目录表，显示了每个图层的名称、图例、说明、又是还有独立的属性表。
8. Data Source：数据源，不经转换的属性，空间数据，各种要素，属性表等。
9. Map： 
10. stroke


# OpenLayers 案例研究 #
     var route = /** @type {ol.geom.LineString} */ (new ol.format.Polyline({
        factor: 1e6
      }).readGeometry(polyline, {
        dataProjection: 'EPSG:4326',
        featureProjection: 'EPSG:3857'
      }));

	  /*获取线型要素所有的坐标对*/
      var routeCoords = route.getCoordinates();
      /*获取线型坐标的长度*/
      var routeLength = routeCoords.length;
	  
      /*添加路径要素*/
      var routeFeature = new ol.Feature({
        type: 'route',
        /*线型要素*/
        geometry: route
      });

      /*添加点要素*/
      var geoMarker = new ol.Feature({
        type: 'geoMarker',
        geometry: new ol.geom.Point(routeCoords[0])
      });

      /*添加图标要素*/
      var startMarker = new ol.Feature({
        type: 'icon',
        /*在指定的线的起始坐标上标记图标，图标的样式由icon指定*/
        geometry: new ol.geom.Point(routeCoords[0])
      });

	  /*添加图标要素*/
      var endMarker = new ol.Feature({
        type: 'icon',
		/*在线型的终点坐标上标记图标，图标样式*/
        geometry: new ol.geom.Point(routeCoords[routeLength - 1])
      });

      var styles = {
        'route': new ol.style.Style({
          /*定义为stroke类型*/
          stroke: new ol.style.Stroke({
            /*绘制宽度与颜色*/
            width: 6, color: [237, 212, 0, 0.8]
          })
        }),
        'icon': new ol.style.Style({
          /**/
          image: new ol.style.Icon({
            anchor: [0.5, 1],
            src: 'https://openlayers.org/en/v4.0.1/examples/data/icon.png'
          })
        }),
        'geoMarker': new ol.style.Style({
          /*绘制圆形，中间为黑色，外边为2个像素的边线*/
          image: new ol.style.Circle({
            radius: 7,
            snapToPixel: false,
            fill: new ol.style.Fill({color: 'black'}),
            stroke: new ol.style.Stroke({
              color: 'white', width: 2
            })
          })
        })
      };

      var animating = false;
      var speed, now;
      var speedInput = document.getElementById('speed');
      var startButton = document.getElementById('start-animation');

      var vectorLayer = new ol.layer.Vector({
        source: new ol.source.Vector({
		  /*要素组：路径要素组，起始，终止节点，圆形点*/
          features: [routeFeature, geoMarker, startMarker, endMarker]
        }),

		/*根据不同的要素选择不同的样式*/
        style: function(feature) {
          // hide geoMarker if animation is active
          if (animating && feature.get('type') === 'geoMarker') {
            return null;
          }
          return styles[feature.get('type')];
        }
      });

      var center = [-5639523.95, -3501274.52];

      var map = new ol.Map({
        target: document.getElementById('map'),
        loadTilesWhileAnimating: true,
        view: new ol.View({
          center: center,
          zoom: 10,
          minZoom: 2,
          maxZoom: 19
        }),
        layers: [
			/*由tile以及vector两个图层构成*/
          new ol.layer.Tile({
            source: new ol.source.BingMaps({
              imagerySet: 'AerialWithLabels',
              key: 'Your Bing Maps Key from http://www.bingmapsportal.com/ here'
            })
          }),
          vectorLayer
        ]
      });

      var moveFeature = function(event) {
        var vectorContext = event.vectorContext;
        var frameState = event.frameState;

        if (animating) {
          var elapsedTime = frameState.time - now;
          // here the trick to increase speed is to jump some indexes
          // on lineString coordinates
          var index = Math.round(speed * elapsedTime / 1000);

          if (index >= routeLength) {
            stopAnimation(true);
            return;
          }
		  //在路径上生成图标
          var currentPoint = new ol.geom.Point(routeCoords[index]);
          var feature = new ol.Feature(currentPoint);
          vectorContext.drawFeature(feature, styles.geoMarker);
        }
        // tell OpenLayers to continue the postcompose animation
        map.render();
      };

      function startAnimation() {
        if (animating) {
          stopAnimation(false);
        } else {
          animating = true;
          now = new Date().getTime();
          speed = speedInput.value;
          startButton.textContent = 'Cancel Animation';
          // hide geoMarker
          geoMarker.setStyle(null);
          // just in case you pan somewhere else
          map.getView().setCenter(center);
          map.on('postcompose', moveFeature);
          map.render();
        }
      }


      /**
       * @param {boolean} ended end of animation.
       */
      function stopAnimation(ended) {
        animating = false;
        startButton.textContent = 'Start Animation';

        // if animation cancelled set the marker at the beginning
        var coord = ended ? routeCoords[routeLength - 1] : routeCoords[0];
        /** @type {ol.geom.Point} */ (geoMarker.getGeometry())
          .setCoordinates(coord);
        //remove listener
        map.un('postcompose', moveFeature);
      }

      startButton.addEventListener('click', startAnimation, false);