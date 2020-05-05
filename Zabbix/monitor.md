## 自定义监控项

### 获取TCP连接状态的值

```
netstat -ant|awk 'NR>2{print $6}'|grep "TIME_WAIT"|wc -l
```

### 设置自定义监控项的格式

```
cd /etc/zabbix/zabbix_agentd.d/
# 官方示例
UserParameter=mysql.ping,HOME=/var/lib/zabbix mysqladmin ping | grep -c alive
mysql.ping # 监控项键名称
mysqladmin ping | grep -c alive # 取值的命令
```

---
在指定目录下创建监控项
```
vim /etc/zabbix/zabbix_agentd.d/tcp_status.conf
UserParameter=TIME_WAIT,netstat -ant|awk 'NR>2{print $6}'|grep "TIME_WAIT"|wc -l
UserParameter=LISTEN,netstat -ant|awk 'NR>2{print $6}'|grep "LISTEN"|wc -l
UserParameter=ESTABLISHED,netstat -ant|awk 'NR>2{print $6}'|grep "ESTABLISHED"|wc -l
```

---

测试

```
zabbix_get -s 192.168.8.11 -k TIME_WAIT
28
```

### 配置监控项

![](.\img\12.png)

---

![](.\img\13.png)

---

![](.\img\14.png)

---

#### 监控项克隆

![](.\img\15.png)

---


![](.\img\16.png)

---

### 设置触发器

![](.\img\17.png)

---

![](.\img\18.png)

---

![](.\img\19.png)













[TOC]

