

## 安装

Elasticsearch是基于Java开发所以第一步安装Java

```linux
yum install -y java-1.8.0-openjdk.x86_64 
```

下载并安装

```linux
mkdir  -p /data/es_soft/
cd /data/es_soft/
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.6.0.rpm

rpm -ivh elasticsearch-6.6.0.rpm
```

启动服务

```linux
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
systemctl status elasticsearch.service

curl 127.0.0.1:9200
{
  "name" : "o-nKKSr",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "ige0b_ybQuC6YdKBTN2sQw",
  "version" : {
    "number" : "6.6.0",
    "build_flavor" : "default",
    "build_type" : "rpm",
    "build_hash" : "a9861f4",
    "build_date" : "2019-01-24T11:27:09.439740Z",
    "build_snapshot" : false,
    "lucene_version" : "7.6.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

```

Elasticsearch默认端口9200

```linx
ps -ef|grep elastic
lsof -i:9200
```

**注意事项：**

1. 锁定内存要修改配置
2. JVM虚拟机最大最小内存设置为一样
3. 最大内存不要超过30G
4. 更改数据目录需要授权用户给elasticsearch
5. es启动比较慢