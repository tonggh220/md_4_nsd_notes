# Hadoop -- 01

## Hadoop分布式集群

#### 单机安装部署

###### 购买云主机 

| 主机    | IP地址       | 配置          |
| ------- | ------------ | ------------- |
| hadoop1 | 192.168.1.50 | 最低配置2核2G |

###### hadoop安装

拷贝云盘 public/hadoop/hadoop-2.7.7.tar.gz 到 hadoop1 上

```shell
[root@hadoop1 ~]# yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
[root@hadoop1 ~]# tar -zxf hadoop-2.7.7.tar.gz
[root@hadoop1 ~]# mv hadoop-2.7.7 /usr/local/hadoop
[root@hadoop1 ~]# chown -R 0.0 /usr/local/hadoop
```

###### 配置JAVA运行环境

```shell
[root@hadoop1 ~]# vim /etc/hosts
192.168.1.50	hadoop1
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

#### 集群安装部署

###### 购买云主机 

| 主机      | IP地址       | 配置          |
| --------- | ------------ | ------------- |
| hadoop1   | 192.168.1.50 | 最低配置2核2G |
| node-0001 | 192.168.1.51 | 最低配置2核2G |
| node-0002 | 192.168.1.52 | 最低配置2核2G |
| node-0003 | 192.168.1.53 | 最低配置2核2G |

###### HDFS部署

以下操作所有机器都要执行

```shell
[root@hadoop1 ~]# yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
[root@hadoop1 ~]# vim /etc/hosts
192.168.1.50	hadoop1
192.168.1.51	node-0001
192.168.1.52	node-0002
192.168.1.53	node-0003
```

以下操作仅在 hadoop1 上执行

```shell
[root@hadoop1 ~]# vim /etc/ssh/ssh_config
# 60行新添加
	StrictHostKeyChecking no
[root@hadoop1 ~]# ssh-keygen -t rsa -b 2048 -N '' -f /root/.ssh/id_rsa
[root@hadoop1 ~]# for i in hadoop1 node-{0001..0003};do
                      ssh-copy-id -i /root/.ssh/id_rsa.pub ${i}
                  done
```



