
<!-- toc -->

## 命令提示符
> 根据不同的颜色显示命令提示符

一、编辑配置文件
```
vim /etc/profile
export PS1='[\[\e[32;1m\]\u@\[\e[33;1m\]\h\[\e[34;1m\] \W\[\e[0m\]]\$ '
```
二、加载配置文件
```
source /etc/profile
```
三、常见的颜色
```
export PS1='\[\e[30;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 黑色提示符
export PS1='\[\e[31;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 红色提示符
export PS1='\[\e[32;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 绿色提示符
export PS1='\[\e[33;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 黄色提示符
export PS1='\[\e[34;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 蓝色提示符
export PS1='\[\e[35;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 粉色提示符
export PS1='\[\e[36;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 浅蓝提示符
export PS1='\[\e[37;1m\][\u@\h \W]\\$ \[\e[0m\]'  -- 白色提示符
```
四、命令提示如的表达式说明

| 序号 | 参数 | 含义                                                   |
| :--: | :--: | :----------------------------------------------------- |
|  1   |  \d  | 代表日期，格式为weekday month date                     |
|  2   |  \H  | 完整的主机名称                                         |
|  3   |  \h  | 仅主机的第一个名字（默认）                             |
|  4   |  \t  | 显示时间为24小时格式，如HH:MM:SS                       |
|  5   |  \T  | 显示时间12小时格式                                     |
|  6   |  \A  | 显示时间24小时格式                                     |
|  7   |  \u  | 当前用户的账户名称（默认）                             |
|  8   |  \v  | BASH的版本信息                                         |
|  9   |  \w  | 完整的工作目录名称。家目录会以~显示（默认）            |
|  10  |  \W  | 利用basename取得工作目录名称，所以只会列出最后一个目录 |
|  11  | \\#  | 下达的第几个命令                                       |
|  12  | \  | 提示字符，如果是root时，提示符为 # , 普通用户则为 $    |

## 优化yum源

一、常见yum源
阿里源
```
1. 备份
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
2. 下载
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
或者
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

```
清华源
```
1. 备份
sudo cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
2. 替换  /etc/yum.repos.d/CentOS-Base.repo   # 小技巧 vim d + G 删除全部
```
网易源
```
1. 备份
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
2. 下载对应版本repo文件, 放入/etc/yum.repos.d/(操作前请做好相应备份) 
http://mirrors.163.com/.help/CentOS7-Base-163.repo
```
二、Epel源
```
1. 备份
mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
2. 下载新repo 到/etc/yum.repos.d/
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
3. 检查epel扩展源
yum repolist
```
三、常见的工具软件安装
```
yum clean all
yum makecache
yum install -y vim tree wget net-tools nmap bash-completion（补全centos7的部分命令参数）
```

## 防火墙

### CentOS6
查看状态
```
/etc/init.d/iptables status
```
永久关闭
```
chkconfig iptables off
```
临时关闭
```
/etc/init.d/iptables stop
/etc/init.d/iptables status
```
### CentOS7
查看状态
```
systemctl status firewalld
```
永久关闭
```
systemctl disable firewalld
```
临时关闭
```
systemctl stop firewalld
systemctl status firewalld  -- 操作完确认
```
简单方法
```
systemctl is-active firewalld   --- 检查服务是否正常运行
systemctl is-enabled firewalld  --- 检查确认服务是否开机运行
```
## 关闭selinux服务
> selinux服务对root用户权限设置

一、查看转态
```
getenforce    --- 确认selinux服务是否开启或是关闭的
```
二、临时关闭
```
setenforce 
usage:  setenforce [ Enforcing | Permissive | 1 | 0 ]
Enforcing   1  --- 临时开启selinux
Permissive  0  --- 临时关闭selinux
```
```
setenforce 0   --- 临时关闭selinux服务
```
三、永久关闭
```
enforcing 	- SELinux security policy is enforced.  
			  selinux服务处于正常开启状态
permissive 	- SELinux prints warnings instead of enforcing.
			  selinux服务被临时关闭了
disabled 	- No SELinux policy is loaded.
			  selinux服务彻底关闭
```
```
vi /etc/selinux/config
SELINUX=disabled
PS: 如果想让selinux配置文件生效,重启系统
```

- [ ] 使用 sed 完成关闭 selinux

```


```
## 字符编码设置

### CentOS6
查看字符集
```
echo $LANG   --- LANG用于设置字符编码信息
en_US.UTF-8
```
临时修改
```
echo $LANG
en_US.UTF-8
LANG=XXX
```
永久修改

```
方法一
tail -5 /etc/profile
export LANG='en_US.UTF-8'

方法二
vi /etc/sysconfig/i18n
LANG='en_US.UTF-8
source /etc/sysconfig/i18n
```
### CentOS7
查看字符集
```
echo $LANG
en_US.UTF-8
```
临时修改
```
echo $LANG
en_US.UTF-8
LANG=XXX
```
永久修改
```
方法一
tail -5 /etc/profile
export LANG='en_US.UTF-8'
方法二
cat /etc/locale.conf 
LANG="zh_CN.UTF-8"
```
一条命令即临时设置，又永久设置
```
localectl set-locale LANG=zh_CN.GBK
```