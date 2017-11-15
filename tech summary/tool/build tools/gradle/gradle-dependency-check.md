##gradle如何查看包依赖

* 当由于依赖引入，加载了不需要的jar文件，如何查询
   
``` gradle :saas-admin-webapp:dependencyInsight --dependency support
```

运行结果中可以显示看出包含support的jar包是被那个包引入的，如下图
[](./images/dependencyinsight.png)

* 当