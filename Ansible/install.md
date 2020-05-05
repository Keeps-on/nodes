
<!-- toc -->
## 安装与配置

### 安装
```
yum install -y ansible     --- 需要依赖epel的yum源
```
### 配置
#### 配置文件说明
```
/etc/ansible/ansible.cfg   --- ansible服务配置文件
/etc/ansible/hosts         --- 主机清单文件   定义可以管理的主机信息
/etc/ansible/roles         --- 角色目录
```
#### 配置主机清单
> 文件位置：/etc/ansible/hosts

```
jkj 
```

#### 密钥对验证
主控端生成密钥对
```
ssh-keygen -t 秘钥的类型(dsa|rsa)
```
管理端接收公钥
```
ssh-copy-id -i /root/.ssh/id_dsa.pub root@192.168.8.105 
```
注意：指定用户root如果不指定以当前用户

### 批量分发公钥
下载安装sshpass
```
yum install -y sshpass
```

执行免交互方式分发公钥命令
```
sshpass -p123456 ssh-copy-id -i /root/.ssh/id_dsa.pub root@172.16.1.41
```
不要输入连接yes或no的确认信息
```
ssh-copy-id -i /root/.ssh/id_dsa.pub root@172.16.1.41 "-o StrictHostKeyChecking=no"
```
服务端口号发生变化
```
sshpass -p123456 ssh-copy-id -i /root/.ssh/id_dsa.pub root@172.16.1.41 -p 52113 "-o StrictHostKeyChecking=no"
```
脚本

```
#!/bin/bash

for ip in {1..100}
do
	sshpass -p123456 ssh-copy-id -i /root/.ssh/id_dsa.pub root@172.16.1.$ip "-o StrictHostKeyChecking=no" &>/dev/null
done
```

分发公钥检查脚本(批量管理脚本)  --- 串型批量管理
```
#!/bin/bash
CMD=$1
for ip in {7,31,41}
do
	ssh 172.16.1.$ip $CMD 
done 

```