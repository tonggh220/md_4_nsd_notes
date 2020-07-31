# Hadoop -- 01

## Hadoop分布式集群

#### 单机安装部署

###### 购买云主机 

| 主机    | IP地址       | 配置          |
| ------- | ------------ | ------------- |
| hadoop1 | 192.168.1.50 | 最低配置2核2G |

###### hadoop安装

```shell
[root@hadoop1 ~]# yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
[root@hadoop1 ~]# tar -zxf hadoop-2.7.7.tar.gz
[root@hadoop1 ~]# mv hadoop-2.7.7 /usr/local/hadoop
[root@hadoop1 ~]# chown -R 0.0 /usr/local/hadoop
[root@hadoop1 ~]# vim /etc/hosts
192.168.1.50	hadoop1
```

###### JAVA运行环境

```shell
[root@hadoop1 ~]# vim /usr/local/hadoop/etc/hadoop/hadoop-env.sh
25:  export JAVA_HOME="java-1.8.0-openjdk安装路径"
33:  export HADOOP_CONF_DIR="/usr/local/hadoop/etc/hadoop"
[root@hadoop1 ~]# /usr/local/hadoop/bin/hadoop version
```

###### 热点词汇分析

```shell
[root@hadoop1 ~]# cd /usr/local/hadoop
[root@hadoop1 hadoop]# mkdir input
[root@hadoop1 hadoop]# cp *.txt input/
[root@hadoop1 hadoop]# ./bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.7.jar wordcount ./input ./output
[root@hadoop1 hadoop]# cat ./output/*
```





