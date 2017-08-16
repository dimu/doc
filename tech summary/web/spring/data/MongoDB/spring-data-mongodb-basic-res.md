#spring data MongoDB基础研究#

##mongodb环境安装##
* 下载windows64位的msi文件
* 点击安装，如果想修改安装路径，请点击custom按钮，选择路径配置
* 安装完成后必须进行data路径的初始化操作，并且data文件夹必须位于盘符的根目录下，然后在mongo的bin路径下执行初始化指令**"mongod --dbpath d:\mongodbdata"**
* mongo的bin路径下mongod.exe是服务管理程序，mongo.exe是shell交互程序,可以将mongo注册成为windows服务，开机自动运行，否则需要手动启动mongod.exe，将mongo注册成为windows服务的命令为: mongod.exe --bind_ip yourIPadress --logpath "d:\mongodbdata\dbConf\mongodb.log" --logappend --dbpath "d:\mongodbdata" --port yourPortNumber --serviceName "YourServiceName" --serviceDisplayName "YourServiceName" --install


##mongodb基本shell操作##
mongodb，hadoop等分布式数据库一样，都分为cluster和standalone两种方式，下面是standalone配置方式。

**standalone**

1. 启动mongodb服务（mongod.exe）  例：mongod -dbpath d:\mongodb\data\mat或者mongod -f d:\mongod.conf
2. 启动客户端shell脚本 （mongo.exe） 语法 mongo host:port 
3. shell脚本常见操作
    
    
    * 创建数据库 use databaseName ，例：use mat，如果创建了数据库但是不创建集合，在退出服务的时候，系统是不会默认保存数据库的。如果需要退出时候能够保存你创建的数据库，需要在数据库中创建集合
    * 创建集合 db.createCollection(collectionName), 例： db.createCollection("device")。 集合有点类似于关系数据库中的表。另外一种方式db.device.insert({})插入对象的过程中会自动创建集合device。
    * 新增数据，db.collectionName.insert(object),例：db.device.insert({'matid':'11111', 'device_name':'hello'})
    * 查找数据 db.collectionName.find()或者匹配查询条件db.collectionName.find(paramObject)
    * 其他帮助指令 可以通过db.help()查看db所支持的脚本函数，使用db.colleciontName.help()查看集合所支持的帮助函数。show dbs：查看数据库状态，show collections等
        

###insert###