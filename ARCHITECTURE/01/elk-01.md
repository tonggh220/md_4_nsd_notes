# ELK日志分析平台

## ELK架构图例

```mermaid
graph LR
subgraph webserver1
  H1[apache] --> F1(filebeat)
end
subgraph webserver2
  H2[apache] --> F2(filebeat)
end
F1 --> A1
F2 --> A1
subgraph Logstash
  A1(input) --> A2(filter) --> A3(output)
end
subgraph ES Cluster
  ES1(Elasticsearch)  
  ES2(Elasticsearch)
  ES3(Elasticsearch)
  ES4(Elasticsearch)
  ES5(Elasticsearch)
end
A3 --> ES1
A3 --> ES2
A3 --> ES3
A3 --> ES4
A3 --> ES5
ES1 --> K(kibana)
ES2 --> K
ES3 --> K
ES4 --> K
ES5 --> K
```



## Elasticsearch 安装

###### 在跳板机上配置 yum 仓库

拷贝云盘 rpm-package/elk 目录到跳板机

```shell
[root@ecs-proxy ~]# cp -a elk /var/ftp/localrepo/elk
[root@ecs-proxy elk]# cd /var/ftp/localrepo/
[root@ecs-proxy localrepo]# createrepo --update .
```

###### 购买 5 台云主机 

1核1G即可 (es-0001 ... es-0005)
192.168.1.41  ... 192.168.1.45

###### 单机安装

```shell
[root@es-0001 ~]# vim /etc/hosts
192.168.1.41	es-0001
[root@es-0001 ~]# yum install -y java-1.8.0-openjdk elasticsearch
[root@es-0001 ~]# vim /etc/elasticsearch/elasticsearch.yml
54：  network.host: 0.0.0.0
[root@es-0001 ~]# systemctl enable --now elasticsearch
[root@es-0001 ~]# curl http://192.168.1.41:9200/
{
  "name" : "War Eagle",
  "cluster_name" : "elasticsearch",
  "version" : {
    "number" : "2.3.4",
    "build_hash" : "e455fd0c13dceca8dbbdbb1665d068ae55dabe3f",
    "build_timestamp" : "2016-06-30T11:24:31Z",
    "build_snapshot" : false,
    "lucene_version" : "5.5.0"
  },
  "tagline" : "You Know, for Search"
}
```

