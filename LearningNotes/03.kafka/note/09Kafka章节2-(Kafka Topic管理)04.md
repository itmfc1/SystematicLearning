09Kafka章节2-(Kafka Topic管理)04



笔记，步骤，思路记录，无实操。



启动三台主机的kafka服务

```shell
# 进入kafka目录
cd /usr/kafka_2.11-2.2.0

# 启动kafak
./bin/kafka-server-start.sh -daemon config/server.properties

# 查看java应用程序
jps
```



![image-20201228201843468](../image/image-20201228201843468.png)

topic管理

* 创建
* 查看
* 详情

![image-20201228201540677](../image/image-20201228201540677.png)

创建topic

```shell
# 创建topic
./bin/kafka-topics.sh --bootstrap-server CentOSA:9092,CentOSB:9092,CentOSB:9092 --create --topic topic topic01 --partitions 3 --replication-factor 2

```

![image-20201228201939760](../image/image-20201228201939760.png)

查看topic

```shell
# 查看topic
./bin/kafka-topics.sh --bootstrap-server CentOSA:9092,CentOSB:9092,CentOSB:9092 --list
```



![image-20201228202159096](../image/image-20201228202159096.png)

查看三台主机A、B、C的kafka日志,体会分区和副本因子的概念

```shell
# 查看kafka日志
ls /usr/kafka-logs/

```



![image-20201228202446318](../image/image-20201228202446318.png)



查看topic详情

```shell
# 查看详情
./bin/kafka-topics.sh --bootstrap-server CentOSA:9092,CentOSB:9092,CentOSB:9092 --describe --topic topic01

```



![image-20201228202840796](../image/image-20201228202840796.png)



![image-20201228203138469](../image/image-20201228203138469.png)

topic管理

* 修改
* 删除

![image-20201228203008303](../image/image-20201228203008303.png)

![image-20201228203222344](../image/image-20201228203222344.png)

修改分区，kafka的分区只能增，不能减。



![image-20201228203329387](../image/image-20201228203329387.png)

![image-20201228203410214](../image/image-20201228203410214.png)

![image-20201228203447233](../image/image-20201228203447233.png)

删除topic



![image-20201228203538791](../image/image-20201228203538791.png)

topic管理

* 订阅
* 生产



![image-20201228203642471](../image/image-20201228203642471.png)

先创建topic

![image-20201228203825936](../image/image-20201228203825936.png)

在A上创建消费者



![image-20201228204011267](../image/image-20201228204011267.png)

在B上创建生产者，生产消息



![image-20201228204055765](../image/image-20201228204055765.png)

观察消息



![image-20201228204136886](../image/image-20201228204136886.png)

topic管理

* 消费组



![image-20201228204330716](../image/image-20201228204330716.png)

查看现在的组信息

![image-20201228204456801](../image/image-20201228204456801.png)

查看g1组的详细信息



![image-20201228204734136](../image/image-20201228204734136.png)



小结

* kafka单机和集群的搭建
* topic管理