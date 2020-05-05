
<!-- toc -->

## 常用命令

### 一、快捷方式
#### 中断命令执行操作过程
```
ctrl+c 
```
#### 清屏操作
```
ctrl+l 
```
#### 注销功能
```
ctrl+d  
```
#### 快速将光标移动到行首
```
ctrl+a 
```
#### 快速将光标移动到行尾
```
ctrl+e
```
#### 按照一个英文单词进行移动光标
```
ctrl+左右方向键
```
#### 将上一个命令最后一个信息进行调取
```
esc+. 
```
#### 光标所在位置到行首内容进行删除（剪切）
```
ctrl+u 
```
#### 光标所在位置到行尾内容进行删除（剪切）
```
ctrl+k
```
#### 粘贴剪切的内容
```
ctrl+y 
```
#### xshell进入到了锁定状态
```
ctrl+s 
```
#### 解除锁定状态
```
ctrl+q
```
#### 快速搜索历史命令
```
ctrl+r   
```

### 二、常用命令
#### tar
```
必要参数有如下：
-A 新增压缩文件到已存在的压缩
-B 设置区块大小
-c 建立新的压缩文件
-d 记录文件的差别
-r 添加文件到已经压缩的文件
-u 添加改变了和现有的文件到已经存在的压缩文件
-x 从压缩的文件中提取文件
-t 显示压缩文件的内容
-z 支持gzip解压文件
-j 支持bzip2解压文件
-Z 支持compress解压文件
-v 显示操作过程
-l 文件系统边界设置
-k 保留原有文件不覆盖
-m 保留文件不被覆盖
-W 确认压缩文件的正确性

可选参数如下：
-b 设置区块数目
-C 切换到指定目录
-f 指定压缩文件
–help 显示帮助信息
–version 显示版本信息
```
##### tar
```
解包：tar xvf FileName.tar
打包：tar cvf FileName.tar DirName
（注：tar是打包，不是压缩！）
```
##### .tar.gz 和 .tgz
解压
```
tar zxvf FileName.tar.gz
```
压缩
```
tar zcvf FileName.tar.gz DirName
```

---

```
gz

	解压1：gunzip FileName.gz
	解压2：gzip -d FileName.gz
	压缩：gzip FileName

.bz2

	解压1：bzip2 -d FileName.bz2
	解压2：bunzip2 FileName.bz2
	压缩： bzip2 -z FileName

.tar.bz2

	解压：tar jxvf FileName.tar.bz2
	压缩：tar jcvf FileName.tar.bz2 DirName
.bz

	解压1：bzip2 -d FileName.bz
	解压2：bunzip2 FileName.bz
	压缩：未知

.tar.bz

	解压：tar jxvf FileName.tar.bz
	压缩：未知

.Z

	解压：uncompress FileName.Z
	压缩：compress FileName

 .tar.Z

	解压：tar Zxvf FileName.tar.Z
	压缩：tar Zcvf FileName.tar.Z DirName

.zip

	解压：unzip FileName.zip
	压缩：zip FileName.zip DirName

.rar

	解压：rar x FileName.rar
	压缩：rar a FileName.rar DirName
```

#### rpm

##### 查看软件是否安装

```
rpm -qa sl
  -q:表示查询 query
  -a:表示所有 all
```

##### 查看软件包中有哪些信息

```
rpm -ql ansible
  -l:表示列表显示
```

##### 查询软件中有哪些配置文件

```
rpm -qc anlible
  -c:查询程序的配置文件
```

##### 查看文件信息属于哪个软件

```
which ssh
/usr/bin/ssh
rpm -qf /usr/bin/ssh
# 组合使用
rpm -qf `which ssh`
openssh-clients-7.4p1-16.el7.x86_64
```

#### ln

> ln -s 原始文件的目录 快捷方式的目录以及名字

##### 创建软连接

```
ln -s /opt/redis_cluster/redis-3.2.9/ /opt/redis_cluster/redis
```

##### 软连接的删除

```
正确的删除方式（删除软链接，但不删除实际数据）
rm -rf ./djdemo
注意：
rm -rf ./djdemo/  (此时也会将软连接对应的数据删除)
```

#### netstat

> yum install net-tools -y 

##### netstat命令用于显示各种网络相关信息

```
netstat -antlp | grep redis
-a:(all)显示所有选项，netstat默认不显示LISTEN相关
-t:(tcp)仅显示tcp相关选项
-u:(udp)仅显示udp相关选项
-n:拒绝显示别名，能显示数字的全部转化成数字
-l：仅列出所有在 Listen (监听) 的服务状态
```

##### 查看网卡列表

```
netstat –i
```

##### 查看一个端口是否被打开

```
netstat -an | grep 23
```

##### 显示监听的端口

```
netstat -l
```

##### 查看指定程序的端口

```
netstat -apn | grep ssh
```

##### 显示PID和进程名称

```
netstat -pt
```

##### 显示监听的端口

```
netstat -l
```

#### rz/sz

> yum install lrzsz -y

##### 上传文件

```
rz 
```

##### 下载文件

```
sz file
```

#### lsof

> yum install lsof -y

查看端口占用

```
lsof -i:9200  # 查看端口占用
```









