# redis config #

**官网教程**

    * $ wget http://download.redis.io/releases/redis-4.0.1.tar.gz
    * $ tar xzf redis-4.0.1.tar.gz
    * $ cd redis-4.0.1 
    * $ make：如果没有安装gcc，需要安装gcc，联网条件使用yum install gcc与yum install gcc-c++,安装完后运行make的时候需要带make MALLOC=libc，malloc环境使用libc，因为redis默认使用的是jemalloc，而本地没有jemalloc环境
   
**运行redis服务**

    * ./src/redis-server

**运行redis shell**

    * ./src/redis-cli