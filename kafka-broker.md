# broker
    cd /usr/local/kafka
    vim config/server.properties

    #kafka操作日志
    log.dirs=/web/data/kafka/kafka-logs

    新创建的主题包含多少个分区
    num.partitions=1

    zookeeper配置
    # root directory for all kafka znodes.
    zookeeper.connect=localhost:2181
    # Timeout in ms for connecting to zookeeper
    zookeeper.connection.timeout.ms=6000 #zookeeper连接超时限制

    num.recovery.threads.per.data.dir=1 #使用可配置的线程池个数来处理日志片段
    一般是服务器重启,启动,崩溃重启(检查或截短每个分区的日志片段)
    服务器关闭,用于关闭日志片段

    auto.create.topics.enable #自动创建主题
    (默认在写入消息),读取消息,当任意客户端发送元数据请求时
    如果需要显示地创建主题,请设置为false

    # The number of threads that the server uses for receiving requests from the network and sending responses to the network
    num.network.threads=3 #网络最大线程

    # The number of threads that the server uses for processing requests, which may include disk I/O
    num.io.threads=8 #io最大线程数

    # The send buffer (SO_SNDBUF) used by the socket server
    socket.send.buffer.bytes=102400 #最大发送数据字节

    # The receive buffer (SO_RCVBUF) used by the socket server
    socket.receive.buffer.bytes=102400 #接收字节

    # The maximum size of a request that the socket server will accept (protection against OOM)
    socket.request.max.bytes=104857600 #最大请求字节


# 配置zookeeper
    vim zookeeper.properties 
    dataDir=/var/lib/zookeeper #自定义目录
    # the port at which the clients will connect
    clientPort=2181
    # disable the per-ip limit on the number of connections since this is a non-production config
    maxClientCnxns=0



