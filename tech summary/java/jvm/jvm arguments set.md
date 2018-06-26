#jvm 参数

[jvm堆内存模型](./images/jvm heap model.jpg)

* -Xmx1G //jvm允许分配的最大堆内存，按需分派
* -Xms512 //jvm初始分配的堆内存
* -Xmn256m //年轻代内存大小，整个jvm内存=年轻代（young Gen）+年老代(old memory）+持久代（perm）
* -XX:PermSize=128m //持久代内存大小
* -XX:MetaSpaceSize=128m //jvm8中移除了PermGem设置，取而代之的是Metaspace
