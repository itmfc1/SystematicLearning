07Kafka章节2-(Kafka单机配置)02



```shell
[root@node0924 ~]# ls
a                                  install.log.syslog                          soft
aa                                 jdk-8u271-linux-x64.rpm                     springboot
anaconda-ks.cfg                    kafka_2.11-2.2.0.tgz                        test
apache-zookeeper-3.6.2-bin.tar.gz  mysql-community-release-el6-5.noarch.rpm    zfg
data                               mysql-community-release-el6-5.noarch.rpm.1  zkdata
install.log                        shadow-utils-4.1.4.2-13.el6.x86_64.rpm      zsh-4.3.10-7.el6.x86_64.rpm
[root@node0924 ~]# tar -zxf kafka_2.11-2.2.0.tgz -C /usr/
[root@node0924 ~]# cd /usr/
[root@node0924 usr]# ls
apache-zookeeper-3.6.2-bin  etc    include           lib    libexec  mfc   share  tmp
bin                         games  kafka_2.11-2.2.0  lib64  local    sbin  src
[root@node0924 usr]# cd kafka_2.11-2.2.0
[root@node0924 kafka_2.11-2.2.0]# ls
bin  config  libs  LICENSE  NOTICE  site-docs
[root@node0924 kafka_2.11-2.2.0]# ls bin/
connect-distributed.sh        kafka-dump-log.sh                    kafka-topics.sh
connect-standalone.sh         kafka-log-dirs.sh                    kafka-verifiable-consumer.sh
kafka-acls.sh                 kafka-mirror-maker.sh                kafka-verifiable-producer.sh
kafka-broker-api-versions.sh  kafka-preferred-replica-election.sh  trogdor.sh
kafka-configs.sh              kafka-producer-perf-test.sh          windows
kafka-console-consumer.sh     kafka-reassign-partitions.sh         zookeeper-security-migration.sh
kafka-console-producer.sh     kafka-replica-verification.sh        zookeeper-server-start.sh
kafka-consumer-groups.sh      kafka-run-class.sh                   zookeeper-server-stop.sh
kafka-consumer-perf-test.sh   kafka-server-start.sh                zookeeper-shell.sh
kafka-delegation-tokens.sh    kafka-server-stop.sh
kafka-delete-records.sh       kafka-streams-application-reset.sh
[root@node0924 kafka_2.11-2.2.0]# 

```

解压kafka到指定目录

`tar -zxf kafka_2.11-2.2.0.tgz -C /usr/`





```shell
[root@node0924 kafka_2.11-2.2.0]# ls config/
connect-console-sink.properties    connect-log4j.properties       server.properties
connect-console-source.properties  connect-standalone.properties  tools-log4j.properties
connect-distributed.properties     consumer.properties            trogdor.conf
connect-file-sink.properties       log4j.properties               zookeeper.properties
connect-file-source.properties     producer.properties
[root@node0924 kafka_2.11-2.2.0]# vi config/server.properties

```



vi config/server.properties



```
# The id of the broker. This must be set to a unique integer for each broker.
broker.id=0



# The address the socket server listens on. It will get the value returned from
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
#     listeners = listener_name://host_name:port
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
listeners=PLAINTEXT://node0924:9092



# A comma separated list of directories under which to store log files
log.dirs=/usr/kafka-logs

# root directory for all kafka znodes.
zookeeper.connect=node0924:2181

```

kafka配置完成，下面演示kafak启动



```shell
[root@node0924 kafka_2.11-2.2.0]# jps
3048 Jps
2041 QuorumPeerMain
[root@node0924 kafka_2.11-2.2.0]# ./bin/kafka-server-start.sh -daemon config/server.properties
[root@node0924 kafka_2.11-2.2.0]# jps
3332 Kafka
2041 QuorumPeerMain
3354 Jps
[root@node0924 kafka_2.11-2.2.0]# 

```

启动前要先有zookeeper，后台启动
./bin/kafka-server-start.sh -daemon config/server.properties

或者

bin/kafka-server-start.sh config/server.properties &



```shell
# ./bin/kafka-server-stop.sh关闭kafka
[root@node0924 kafka_2.11-2.2.0]# ./bin/kafka-server-stop.sh
[root@node0924 kafka_2.11-2.2.0]# jps
3332 Kafka
2041 QuorumPeerMain
3422 Jps
[root@node0924 kafka_2.11-2.2.0]# jps
3432 Jps
2041 QuorumPeerMain
[root@node0924 kafka_2.11-2.2.0]# 

```

关闭后，需要等一会，这是一个优雅关闭的过程





```
./bin/kafka-topics.sh --help
```

查看topics帮助



```shell
[root@node0924 kafka_2.11-2.2.0]# ./bin/kafka-topics.sh --bootstrap-server node0924:9092 --create --topic topic01 --partitions 2 --replication-factor 3
[2020-12-20 17:03:57,850] INFO [Admin Manager on Broker 0]: Error processing create topic request for topic topic01 with arguments (numPartitions=2, replicationFactor=3, replicasAssignments={}, configs={}) (kafka.server.AdminManager)
org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 3 larger than available brokers: 1.
Error while executing topic command : org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 3 larger than available brokers: 1.
[2020-12-20 17:03:57,867] ERROR java.util.concurrent.ExecutionException: org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 3 larger than available brokers: 1.
	at org.apache.kafka.common.internals.KafkaFutureImpl.wrapAndThrow(KafkaFutureImpl.java:45)
	at org.apache.kafka.common.internals.KafkaFutureImpl.access$000(KafkaFutureImpl.java:32)
	at org.apache.kafka.common.internals.KafkaFutureImpl$SingleWaiter.await(KafkaFutureImpl.java:89)
	at org.apache.kafka.common.internals.KafkaFutureImpl.get(KafkaFutureImpl.java:260)
	at kafka.admin.TopicCommand$AdminClientTopicService.createTopic(TopicCommand.scala:175)
	at kafka.admin.TopicCommand$TopicService$class.createTopic(TopicCommand.scala:134)
	at kafka.admin.TopicCommand$AdminClientTopicService.createTopic(TopicCommand.scala:157)
	at kafka.admin.TopicCommand$.main(TopicCommand.scala:60)
	at kafka.admin.TopicCommand.main(TopicCommand.scala)
Caused by: org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 3 larger than available brokers: 1.
 (kafka.admin.TopicCommand$)
[root@node0924 kafka_2.11-2.2.0]# 

```

./bin/kafka-topics.sh --bootstrap-server node0924:9092 --create --topic topic01 --partitions 2 --replication-factor 3



创建topic,创建副本因子为3，大于可用的1。



```shell
[root@node0924 kafka_2.11-2.2.0]# ./bin/kafka-topics.sh --bootstrap-server node0924:9092 --create --topic topic001 --partitions 3 --replication-factor 1
[root@node0924 kafka_2.11-2.2.0]# 

```

定义好topic。后面要消费它



```
./bin/kafka-console-consumer.sh --bootstrap-server node0924:9092 --topic topic001 --group group001
```

定义消费组，消费者，1-3个，测试



```
./bin/kafka-console-producer.sh --broker-list node0924:9092 --topic topic001
```

发送消息，生产者





```
./bin/kafka-console-consumer.sh --bootstrap-server node0924:9092 --topic topic001 --group group002
```

测试广播，不用的消费组



```
./bin/kafka-server-stop.sh
```

关闭kakfa



```shell
[root@node0924 kafka_2.11-2.2.0]# jps
2041 QuorumPeerMain
6477 Jps
[root@node0924 kafka_2.11-2.2.0]# cd ..
[root@node0924 usr]# ls
apache-zookeeper-3.6.2-bin  etc    include           kafka-logs  lib64    local  sbin   src
bin                         games  kafka_2.11-2.2.0  lib         libexec  mfc    share  tmp
[root@node0924 usr]# cd apache-zookeeper-3.6.2-bin
[root@node0924 apache-zookeeper-3.6.2-bin]# ./bin/zkServer.sh stop zoo.cfg
ZooKeeper JMX enabled by default
Using config: /usr/apache-zookeeper-3.6.2-bin/bin/../conf/zoo.cfg
Stopping zookeeper ... STOPPED
[root@node0924 apache-zookeeper-3.6.2-bin]# jps
6509 Jps
[root@node0924 apache-zookeeper-3.6.2-bin]# 

```



`./bin/zkServer.sh stop zoo.cfg` 关闭zookeeper。



```
shutdown -h now
```

关闭linux系统。相当于关机



![image-20201220172601638](../image/image-20201220172601638.png)

单机kafak-总结

