# 安装java jdk
    下载地址: http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
    cd /usr/local
    wget http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz

    tar zxvf jdk-8u181-linux-x64.tar.gz
    mv jdk-8u181-linux-x64 java
    添加环境变量
    #java
    export JAVA_HOME=/usr/local/java
    export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

    export PAHT=$PATH:$JAVA_HOME/bin:/usr/local/kafka

    建立软连接
    ln -s /usr/local/java/bin/java /usr/bin/java
# 安装zookeeper
    下载地址: http://mirrors.hust.edu.cn/apache/zookeeper/zookeeper-3.4.13/zookeeper-3.4.13.tar.gz
    cd /usr/local
    wget http://mirrors.hust.edu.cn/apache/zookeeper/zookeeper-3.4.13/zookeeper-3.4.13.tar.gz
    tar zxvf zookeeper-3.4.13.tar.gz
    ln -s zookeeper-3.4.13 zookeeper
    mkdir /var/lib/zookeeper
    cd zookeeper
    配置zookeeper
    cp conf/zoo_sample.cfg conf/zoo.cfg
    cd conf
    vim zoo.cfg
    # The number of milliseconds of each tick
    tickTime=2000
    # The number of ticks that the initial 
    # synchronization phase can take
    initLimit=10
    # The number of ticks that can pass between 
    # sending a request and getting an acknowledgement
    syncLimit=5
    # the directory where the snapshot is stored.
    # do not use /tmp for storage, /tmp here is just 
    # example sakes.
    dataDir=/var/lib/zookeeper
    # the port at which the clients will connect
    clientPort=2181

# 启动zookeeper
    /usr/local/zookeeper/bin/zkServer.sh start
    查看2181端口
    yum install telnet
    # telnet localhost 2181
    测试2181
    srvr

# 安装kafka
    下载地址: http://mirrors.hust.edu.cn/apache/kafka/1.1.1/kafka_2.11-1.1.1.tgz
    安装
    cd /usr/local
    wget http://mirrors.hust.edu.cn/apache/kafka/1.1.1/kafka_2.11-1.1.1.tgz
    tar zxvf kafka_2.11-1.1.1.tgz
    ln -s kafka_2.11-1.1.1 kafka

# kafka操作日志
    cd /usr/local/kafka
    vim config/server.properties
    log.dirs=/web/data/kafka/kafka-logs

    mkdir -p /web/data/kafka/kafka-logs
    chmod -R 777 /web/data/kafka

# 启动kafka
    /usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/server.properties 

# 创建topic mytest
    [root@daheige config]# /usr/local/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic mytest
    Created topic "mytest".
# 往测试主题上发送消息
    /usr/local/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mytest
    >daheige
# 读取测试主题上的消息
    /usr/local/kafka/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic mytest --from-beginning
    daheige








