# docker step by step —— volumes

volume主要是解决如何管理容器中程序运行的数据问题，例如数据库数据，日志文件，静态文件，语音视频文件。面对应用的数据库迁移，共享，日志文件系统收集等等，都无法直接将文件管理在容器内部。

## docker数据卷常见操作

1. **创建数据卷**

`docker volume create volume_name`