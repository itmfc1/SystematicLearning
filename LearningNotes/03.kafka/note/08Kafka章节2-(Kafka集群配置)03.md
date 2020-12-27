08Kafka章节2-(Kafka集群配置)03



笔记，步骤，思路记录，无实操。



![image-20201227210854208](../image/image-20201227210854208.png)

kafka环境搭建-集群



准备三台linux虚拟机，kafka-A、kafka-B、kafka-C，启动，登录。使用`ifconfig`命令，查看ip

准备好文件`jdk-8u271-linux-x64.rpm`、`apache-zookeeper-3.6.2-bin.tar.gz`、`kafka_2.11-2.2.0.tgz`

查看系统有没有安装jdk，`rpm -qa | grep jdk`

没有安装jdk，则进行jdk的安装，`rpm -ivh jdk-8u271-linux-x64.rpm`



三台主机的ssh免密码认证，先删除。`rm -rf .ssh`

配置三台主机名和映射关系，`vi /etc/hosts`

kafka-A

```
192.168.52.130 CentOSA
192.168.52.131 CentOSB
192.168.52.132 CentOSC
```

kafka-B

```
192.168.52.130 CentOSA
192.168.52.131 CentOSB
192.168.52.132 CentOSC
```

kafka-C

```
192.168.52.130 CentOSA
192.168.52.131 CentOSB
192.168.52.132 CentOSC
```



测试一下网络，`ping CentOSA`、`ping CentOSB`、`ping CentOSC`



将文件拷贝覆盖到其他主机上，

`scp /etc/hosts CentOSB:/etc`，选择`yes`，输入密码。

`scp /etc/hosts CentOSC:/etc`，选择`yes`，输入密码。



查看配置的hosts文件内容，`cat /etc/hosts`



在home目录，配置环境变量，`vi .bashrc`

```
JAVA_HOME=/usr/mfc/jdk1.8.0_271-amd64
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=.
export JAVA_HOME
export PATH
export CLASSPATH
```

启用配置的环境变量，`source .bashrc`

查看配置的环境变量，`echo $JAVA_HOME`、`echo $PATH`



将文件拷贝覆盖到其他主机上，

`scp .bashrc CentOSB:~/`，选择`yes`，输入密码。

`scp .bashrc CentOSC:~/`，选择`yes`，输入密码。

B、C两台机器重新加载一下环境变量，`source .bashrc`



查看防火墙，关闭防火墙

```shell
# 查看防火墙状态
serivice iptables status
# 关闭防火墙
serivice iptables stop
# 关闭开机自启
chkconfig iptables off
# 查看
chkconfig --list | grep iptables
```



同步三台机器的日期

```shell
# 使用ntpd
ntpd
# 没有ntpd命令，下载一个
yum install ntp -y
# 时钟同步
ntpd ntp1.aliyun.com
# 当前系统时间写入到CMOS中
clock -w
```



以A为模板，安装配置zookeeper

```shell
# 解压zookeeper文件到/usr/目录
tar -zxf apache-zookeeper-3.6.2-bin.tar.gz -C /usr/
# 进入zookeeper
cd apache-zookeeper-3.6.2-bin
# 拷贝文件，并改名
cp conf/zoo_sample.cfg conf/zoo.cfg
# 编辑zoo.cfg
vi conf/zoo.cfg
```

zoo.cfg的修改内容

```
dataDir=/root/zkdata

#autopurge.prugeinteval=1
server.1=CentOSA:2888:3888
server.2=CentOSB:2888:3888
server.3=CentOSC:2888:3888
```

创建root下的目录，`mkdir /root/zkdata`



将A的zookeeper文件和配置，拷贝到B、C

```shell
# 拷贝文件夹
scp -r /usr/apache-zookeeper-3.6.2-bin CentOSB:/usr/
scp -r /usr/apache-zookeeper-3.6.2-bin CentOSC:/usr/
```

B、C创建root下的目录，`mkdir /root/zkdata`



进入home，创建zkdata下的标识

```shell
# A
echo 1 > /root/zhdata/myid
# B
echo 2 > /root/zhdata/myid
# C
echo 3 > /root/zhdata/myid
```



配置成功后，三台主机进行启动zookeeper

```shell
# A
/usr/apache-zookeeper-3.6.2-bin/bin/zkServer.sh start zoo.cfg
# B
/usr/apache-zookeeper-3.6.2-bin/bin/zkServer.sh start zoo.cfg
# C
/usr/apache-zookeeper-3.6.2-bin/bin/zkServer.sh start zoo.cfg
```

启用不成功，检查myid文件和防火墙



配置kafka

```shell
# 解压
tar -zxf kafka_2.11-2.2.0.tgz -C /usr/
# 进入kafka
cd kafka_2.11-2.2.0
# 编辑
vi config/server.properties
```

以A为模板，config/server.properties编辑的内容

```
listeners=PLAINTEXT://CentOSA:9092

log.dirs=/usr/kafka-logs

zookeeper.connect=CentOSA:2181,CentOSB:2181,CentOSC:2181
```

将A的kafka文件和配置，拷贝到B、C

```shell
# 拷贝文件夹
scp -r /usr/kafka_2.11-2.2.0 CentOSB:/usr/
scp -r /usr/kafka_2.11-2.2.0 CentOSC:/usr/
```



修改B的server.properties

```shell
vi /usr/kafka_2.11-2.2.0/config/server.properties
```

修改的内容

```
broker.id=1

listeners=PLAINTEXT://CentOSB:9092
```



修改C的server.properties

```shell
vi /usr/kafka_2.11-2.2.0/config/server.properties
```

修改的内容

```
broker.id=2

listeners=PLAINTEXT://CentOSC:9092
```



启动三台主机的kafka服务

```shell
# 进入kafka目录
cd /usr/kafka_2.11-2.2.0

# 启动kafak
./bin/kafka-server-start.sh -daemon config/server.properties

# 查看java应用程序
jps
```

