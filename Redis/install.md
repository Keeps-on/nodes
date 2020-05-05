## 安装

### 下载软件
```
mkdir /data/soft -p
wget -O /data/soft/redis-3.2.9.tar.gz http://download.redis.io/releases/redis-3.2.9.tar.gz
```
### 目录结构
```
mkdir /opt/redis_cluster/redis_6379/{conf,logs,pid} -p
redis_cluster/
└── redis_6379
    ├── conf -- 配置文件
    ├── logs -- 日志
    └── pid  -- 进程
```
### 解压
```
tar zxvf redis-3.2.9.tar.gz -C /opt/redis_cluster/
```
### 创建软连接
```
ln -s /opt/redis_cluster/redis-3.2.9/ /opt/redis_cluster/redis
```
### 安装
```
cd /opt/redis_cluster/redis
make && make install
```
---
```
ll /usr/local/bin/
total 15052
-rwxr-xr-x. 1 root root 2432016 Apr 24 20:29 redis-benchmark
-rwxr-xr-x. 1 root root   25088 Apr 24 20:29 redis-check-aof
-rwxr-xr-x. 1 root root 5180928 Apr 24 20:29 redis-check-rdb
-rwxr-xr-x. 1 root root 2584968 Apr 24 20:29 redis-cli
lrwxrwxrwx. 1 root root      12 Apr 24 20:29 redis-sentinel -> redis-server
-rwxr-xr-x. 1 root root 5180928 Apr 24 20:29 redis-server
```
