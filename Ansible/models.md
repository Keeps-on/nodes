<!-- toc -->
## 常用模块


### command
基本使用
```
ansible docker -m command -a "mkdir  -p /data/es_soft/"
```
**注意**：有些符号信息无法识别:  <", ">", "|", ";" and "&"

#### chdir
> 在执行命令之前对目录进行切换

```
ansible docker -m command -a "chdir=/data/es_soft rpm -ivh elasticsearch-6.6.0.rpm"
```
#### creates
> 如果文件存在了,不执行命令操作

```
ansible docker -m command -a "creates=/tmp/hosts touch test.txt" 
```
#### removes
> 如果文件存在了,这个步骤将执行

```
ansible docker -m command -a "removes=/tmp/hosts chdir=/tmp touch test.txt"
```
#### free_form
> 使用command模块的时候,-a参数后面必须写上一个合法linux命令信息

```
The command module takes a free form command to run. 
There is no parameter actually named 'free form'. See the examples!
使用command模块的时候,-a参数后面必须写上一个合法linux命令信息
```
### shell

### scripts

### copy
> 将数据信息进行批量分发

```
ansible docker -m copy -a "src=/data/elasticsearch-6.6.0.rpm dest=/data/elasticsearch-6.6.0.rpm"
```
### file

### yum




