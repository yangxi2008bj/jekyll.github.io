---
layout: 		post
title: 			"安装Zookeeper"
date:			2018-01-20 
author:			Xi Yang
tags: 
    - zookeeper
    - centos
    - windows
---   

##### CentOS安装Zookeeper

- 下载获取zookeeper并解压
	```bash
	wget http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.4.11/zookeeper-3.4.11.tar.gz
	tar -zxvf zookeeper-3.4.11.tar.gz
	```

- 在zookeeper-3.4.11中的conf文件夹中创建zoo.cfg，内容如下：
	```bash
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
	  dataDir=/tmp/zookeeper
	  # the port at which the clients will connect
	  clientPort=2181
	  # the maximum number of client connections.
	  # increase this if you need to handle more clients
	  #maxClientCnxns=60
	  #
	  # Be sure to read the maintenance section of the
	  # administrator guide before turning on autopurge.
	  #
	  # http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
	  #
	  # The number of snapshots to retain in dataDir
	  #autopurge.snapRetainCount=3
	  # Purge task interval in hours
	  # Set to "0" to disable auto purge feature
	  #autopurge.purgeInterval=1
	```

- 在zookeeper-3.4.11中的bin文件下执行命令开启zookeeper服务：
	```bash
	./zkServer.sh start
	```

##### Windows安装Zookeeper

- 下载文件：
	http://mirrors.cnnic.cn/apache/zookeeper/zookeeper-3.4.11/zookeeper-3.4.11.tar.gz 

- 把下载的zookeeper的文件解压到指定目录。如： D:\machine\zookeeper-3.4.11

- 在conf下增加zoo.cfg文件，内容如下：
	 ```bash
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
	 dataDir=D:\\data\\zookeeper
	 # the port at which the clients will connect
	 clientPort=2181
	 # the maximum number of client connections.
	 # increase this if you need to handle more clients
	 #maxClientCnxns=60
	 #
	 # Be sure to read the maintenance section of the
	 # administrator guide before turning on autopurge.
	 #
	 # http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
	 #
	 # The number of snapshots to retain in dataDir
	 #autopurge.snapRetainCount=3
	 # Purge task interval in hours
	 # Set to "0" to disable auto purge feature
	 #autopurge.purgeInterval=1
 	 ```

- 进入到bin目录，并且启动zkServer.cmd
