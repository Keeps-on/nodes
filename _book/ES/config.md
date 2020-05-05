

## 配置

```
rpm -ql elasticsearch		#查看elasticsearch软件安装了哪些目录
rpm -qc elasticsearch		#查看elasticsearch的所有配置文件

/etc/elasticsearch/elasticsearch.yml           #配置文件
/etc/elasticsearch/jvm.options.                #jvm虚拟机配置文件
/etc/init.d/elasticsearch  		               #init启动文件
/etc/sysconfig/elasticsearch		           #环境变量配置文件
/usr/lib/sysctl.d/elasticsearch.conf	       #sysctl变量文件，修改最大描述符
/usr/lib/systemd/system/elasticsearch.service  #systemd启动文件
/var/lib/elasticsearch		                   #数据目录
/var/log/elasticsearch		                   #日志目录
/var/run/elasticsearch		                   #pid目录
```


### 配置文件

#### 默认配置文件

```
grep "^[a-Z]" /etc/elasticsearch/elasticsearch.yml
node.name: node-1                     # 节点名称
network.host: 192.168.8.16,127.0.0.1
http.port: 9200
bootstrap.memory_lock: true           # 内存锁定
path.data: /var/lib/elasticsearch     # 默认存储数据的目录
path.logs: /var/log/elasticsearch     # 日志
```
#### 数据目录的修改
```
# 查看elasticsearch所有的用户
cat /etc/passwd
elasticsearch:x:997:995:elasticsearch user:/nonexistent:/sbin/nologin
# 修改数据目录权限
chown -R elasticsearch:elasticsearch /data/elasticsearch/
```

#### 内存限制
```
vim /etc/elasticsearch/jvm.options # 内存相关的配置
-Xms1g  # 最小占用内存
-Xmx1g  # 最大占用内存
说明：当elasticsearch启动的时候会最大最小占用的内存；
官方建议
1. 不要超过32G，当你的内存超过32G不仅性能不会提升，反而会下降
2. 最大最小内存设置为一样
3. 配置文件设置锁定内存 bootstrap.memory_lock: true 
4. 至少给你服务器本身空余50%的内存
```

#### 启动报错

> 查看日志如果内存锁定失败
>
> https://www.elastic.co/guide/en/elasticsearch/reference/6.6/setup-configuration-memory.html
> https://www.elastic.co/guide/en/elasticsearch/reference/6.6/setting-system-settings.html#sysconfig

```
### 修改启动配置文件或创建新配置文件
方法1: systemctl edit elasticsearch
方法2: vim /usr/lib/systemd/system/elasticsearch.service 
### 增加如下参数
[Service]
LimitMEMLOCK=infinity

### 重新启动
systemctl daemon-reload
systemctl restart elasticsearch
```
