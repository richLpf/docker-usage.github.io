## mongo

我们安装环境经常会出现很多环境问题，这里我们尝试用docker部署下mongo,感受下docker的方便和速度

直接运行

`docker run -d -v /data/mongodb:/etc/mongo -p 27017:27017 --name test-mongo mongo`

docker将拉取dockerhub 中mongo的最新镜像，并将mongo的数据存放在宿主机的/data/mongodb中，端口号为27017

## mongo版本

mongo的版本，我们在docker tags 中可以看到各种各样的版本

执行docker pull mongo:3.6 将拉取3.6版本

## 什么是mongodb?

mongodb 是一个免费，开源，跨平台运行的文档数据库。作为一个非关系型数据库，mongodb使用json的数据模式。mongodb 的开发着是mongodb inc.

## 如何使用镜像

** 开始一个mongo服务器实例

`docker run --name some-mongo -d mongo:tag`

some-mongo 是你想为容器起的名字，tag是你使用的mongodb的版本号，可以查看相关的版本号。

## 从另一个容器连接mongodb数据库

mongo服务在镜像中默认的端口号是27017，因此通过docker网络连接远程也是一样的。下面的例子开始启动另一个mongodb容器实例,像上面一样用命令行运行原始容器一样。允许你执行mongo实例


`docker run -it --network some-network --rm mongo mongo --host some-mongo test`


some-mongo 是最开始的mongo容器的名字




## mongo的基本操作

### 数据库

### 集合

### 文档




## mongo的高级功能


## mongo在nodejs中的使用


## mgo在go中的使用






```


#日志文件位置
logpath=/data/db/journal/mongodb.log　　（这些都是可以自定义修改的）

# 以追加方式写入日志
logappend=true

# 是否以守护进程方式运行
fork = true

# 默认27017
#port = 27017

# 数据库文件位置
dbpath=/data/db

# 启用定期记录CPU利用率和 I/O 等待
#cpu = true

# 是否以安全认证方式运行，默认是不认证的非安全方式
#noauth = true
#auth = true

# 详细记录输出
#verbose = true

# Inspect all client data for validity on receipt (useful for
# developing drivers)用于开发驱动程序时验证客户端请求
#objcheck = true

# Enable db quota management
# 启用数据库配额管理
#quota = true
# 设置oplog记录等级
# Set oplogging level where n is
#   0=off (default)
#   1=W
#   2=R
#   3=both
#   7=W+some reads
#diaglog=0

# Diagnostic/debugging option 动态调试项
#nocursors = true

# Ignore query hints 忽略查询提示
#nohints = true
# 禁用http界面，默认为localhost：28017
#nohttpinterface = true

# 关闭服务器端脚本，这将极大的限制功能
# Turns off server-side scripting.  This will result in greatly limited
# functionality
#noscripting = true
# 关闭扫描表，任何查询将会是扫描失败
# Turns off table scans.  Any query that would do a table scan fails.
#notablescan = true
# 关闭数据文件预分配
# Disable data file preallocation.
#noprealloc = true
# 为新数据库指定.ns文件的大小，单位:MB
# Specify .ns file size for new databases.
# nssize =

# Replication Options 复制选项
# in replicated mongo databases, specify the replica set name here
#replSet=setname
# maximum size in megabytes for replication operation log
#oplogSize=1024
# path to a key file storing authentication info for connections
# between replica set members
#指定存储身份验证信息的密钥文件的路径
#keyFile=/path/to/keyfile


```


一、linux 源码安装
1、下载对应版本的mongnodb
```
1、到官网下载
https://www.mongodb.com/download-center#community

2、在linux下载
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.12.tgz    # 下载
```
2、解压，移动到 /usr/local/mongodb
```

tar -zxvf mongodb-linux-x86_64-3.0.6.tgz                                   # 解压

mv  mongodb-linux-x86_64-3.0.6/ /usr/local/mongodb                         # 将解压包拷贝到指定目录
```
3、用软连接的方式配置mongo全局命令

```
ln -s /usr/local/mongodb/bin/mongo /usr/bin/mongo

ln -s /usr/local/mongodb/bin/mongod /usr/bin/mongod
```

4、启动mongo服务

```
mkdir -p /data/mongodb

mongo -dbpath /data/mongodb -logpath /data/mongo/mongo.log -logappend -fork -port 27017 

```

二：mongo  docker 安装

