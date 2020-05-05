
## 配置
```
vim /opt/redis_cluster/redis_6379/conf/redis_6379.conf
```
---
```
### 以守护进行模式启动
daemonize yes
### 绑定主机ip地址
bind 192.168.8.105
### 监听端口
port 6379
### pid文件存放位置
pidfile /opt/redis_cluster/redis_6379/pid/redis_6379.pid
### log文件存放位置
logfile /opt/redis_cluster/redis_6379/logs/redis_6379.log
### 设置数据库的数量
databases 16
### 指定本地持久化文件的文件名,默认为dump.rdb
dbfilename redis_6379.rdb
# 启动服务
ps -ef | grep redis
root     107878  00:00:00 /usr/local/bin/redis-server 127.0.0.1:6379
root     111025   00:00:00 redis-server 192.168.8.104:6379
# 启动redis
redis-cli -h 192.168.8.104
# 查看redis的安装目录
1. 查看redis的进程号 xxxx
ps -ef | grep redis
2. 执行以下指令
ls -l /proc/xxxx/cwd
```