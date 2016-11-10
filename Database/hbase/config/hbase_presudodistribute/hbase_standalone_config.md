#hbase data export & import
文件导出 命令 表名 地址
file:///表示本地路径
/相对于hdfs的路径，优先考虑使用hdfs导出
./hbase org.apache.hadoop.hbase.mapreduce.Export userinfo /tmp/stark_summer/userinfo
如果使用hdfs进行导出,然后继续使用以下命令
hadoop fs -ls tablename  查看文件

#文件导入基本操作
1. hadoop fs -get  /xx/xxxx/tablename 获取到本地路径 hdfs://localhost:9000/hbase/** （从hdfs文件系统中下载到本地）
2. hadoop fs -mkdir -p(文件夹) hdfs://localhost:9000/hbase/xx/xxx/xxxx/filename
3. hadoop fs -put /xx/xxxxx/tablename(本地路径) hdfs://localhost:9000/hbase/*******（文件系统）
4. hdfs dfs -copyFromLocal /xx/xxx/hbase/lib/* hdfs://test-centos:9000/xx/xxx/hbase/lib/
5. ./hbase org.apache.hadoop.hbase.mapreduce.Driver import vip_unnormal_bigtable hdfs://localhost:9000/hbase/vip_unnormal_bigtable

#reinstall clean directory
/home/dwx/tmp
hdfs://dwx-centos:9000/hbase
/home/dwx/tmp/zookeeper



#hadoop & hbase web port
namenode节点：http://dwx-centos:50070/
http://dwx-centos:16030/

#table structure
 'vip_unnormal_bigtable', {NAME => 'd', DATA_BLOCK_ENCODING => 'NONE', BLOOMFILTER => 'ROW', REPLICATION_SCOPE => '0', COMPRESSION => 'NONE', VERSIONS =>'1', MIN_VERSIONS => '0', KEEP_DELETED_CELLS => 'false', IN_MEMORY => 'false', BLOCKCACHE => 'true'}

 'vip_unnormal_location_bigtable', {NAME => 'd', DATA_BLOCK_ENCODING => 'NONE', BLOOMFILTER => 'ROW', REPLICATION_SCOPE => '0', VERSIONS => '1', COMPRESSION => 'NONE', MIN_VERSIONS => '0', KEEP_DELETED_CELLS => 'false', IN_MEMORY => 'false', BLOCKCACHE => 'true'}

 'vip_unnormal_person_bigtable', {NAME => 'd', DATA_BLOCK_ENCODING => 'NONE', BLOOMFILTER => 'ROW', REPLICATION_SCOPE => '0', COMPRESSION => 'NONE', VERSIONS => '1', MIN_VERSIONS => '0', KEEP_DELETED_CELLS => 'false', IN_MEMORY => 'false', BLOCKCACHE => 'true'}

 'vip_unnormal_person_daily_bigtable', {NAME => 'topalertday', DATA_BLOCK_ENCODING => 'NONE', BLOOMFILTER => 'ROW', REPLICATION_SCOPE => '0', VERSIONS => '1', COMPRESSION => 'NONE', MIN_VERSIONS => '0',  KEEP_DELETED_CELLS => 'false', BLOC                         IN_MEMORY => 'false', BLOCKCACHE                             
 => 'true'}

#查询分析表
cdr_info_bigtable


#hadoop & hbase 伪分布式安装方式
1. 下载hadoop & hbase tar.gz格式的文件包
2.
3. 格式化namenode -》  ./hadoop namenode -format
4. 启动hadoop ->   start-dfs.sh  -> start-yarn.sh
5. 运行jps查看进程情况
6. 创建hadoop fs文件夹
7. 配置hbase文件
8. 运行./start-hbase.sh
9. 运行./hbase shell
