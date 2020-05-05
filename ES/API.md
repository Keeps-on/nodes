
## Elasticsearch-API

增删改查:

1. 插入数据不需要提前创建好数据库
2. index -- 库
   type -- 表
   filter -- 字段
3. 默认随机生成_ID -- 唯一键ID

#### 增

##### 创建索引

```
curl -XPUT 'localhost:9200/vipinfo?pretty'

{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : ”vipinfo"
}
```

##### 插入文本

```
curl -XPUT 'localhost:9200/vipinfo/user/1?pretty' -H 'Content-Type: application/json' -d'
{
    "first_name" : "John",
    "last_name": "Smith",
    "age" : 25,
    "about" : "I love to go rock climbing", "interests": [ "sports", "music" ]
}'

curl -XPUT  'localhost:9200/vipinfo/user/2?pretty' -H 'Content-Type: application/json' -d' {
"first_name": "Jane",
"last_name" : "Smith",
"age" : 32,
"about" : "I like to collect rock albums", "interests": [ "music" ]
}'

curl –XPUT  'localhost:9200/vipinfo/user/3?pretty' -H 'Content-Type: application/json' -d' {
"first_name": "Douglas", "last_name" : "Fir",
"age" : 35,
"about": "I like to build cabinets", "interests": [ "forestry" ]
}'
```

#### 删

```
curl -XDELETE 'localhost:9200/vipinfo/user/1?pretty'

{
  "_index" : "vipinfo",
  "_type" : "user",
  "_id" : "1",
  "_version" : 2,
  "result" : "deleted",
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 1,
  "_primary_term" : 2
}

# 删除索引
curl -XDELETE 'localhost:9200/vipinfo?pretty'
{
  "acknowledged" : true
}

```

#### 改

```
curl -XPUT 'localhost:9200/vipinfo/user/1?pretty' -H 'Content-Type: application/json' -d'
{
    "first_name" : "John",
    "last_name": "Smith",
    "age" : 27,
    "about" : "I love to go rock climbing", "interests": [ "sports", "music" ]
}

{
  "_index" : "vipinfo",
  "_type" : "user",
  "_id" : "1",
  "_version" : 2,
  "result" : "updated",
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 1,
  "_primary_term" : 1
}

# 注意该种方法会将全部的内容全部删除掉
curl -XPOST 'localhost:9200/vipinfo/user/1?pretty' -H 'Content-Type: application/json' -d'
{
    "age" : 29
}'
```

#### 查

##### 查询全部

```
curl -XGET localhost:9200/vipinfo/user/_search?pretty
```

##### 查询指定文档

```linux
curl -XGET 'localhost:9200/vipinfo/user/1?pretty'

查询不到返回 false
curl -XGET 'localhost:9200/vipinfo/user/32?pretty'
{
  "_index" : "vipinfo",
  "_type" : "user",
  "_id" : "32",
  "found" : false
}
```

##### 条件查询

```linux
curl -XGET 'localhost:9200/vipinfo/user/_search?q=last_name:Smith&pretty'

curl -XGET 'localhost:9200/vipinfo/user/_search?pretty' -H 'Content-Type: application/json' -d'           
{
  "query" : { 
    "match" : {
        "last_name" : "Smith"
     }
  } 
}'

curl -XGET 'localhost:9200/vipinfo/user/_search?pretty' -H 'Content-Type: application/json' -d'{ 
  "query" : { 
    "bool": { 
      "must": { 
        "match" : { 
          "last_name" : "smith" 
          } 
     }, 
     "filter": { 
        "range" : {"age" : { "gt" : 30 }  
          } 
        } 
      } 
    } 
 }'
```