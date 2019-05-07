一、镜像

> 建议注册docker仓库账号，后面要使用。[仓库地址](https://hub.docker.com/)

__nginx__

```
docker search nginx

docker pull nginx
```

# 尝试启动第一个docker容器，依次运行如下命令

`docker images` 确定不存在docker镜像

`docker pull nginx` 或`docker pull nginx:1.14`(下载特定版本)

`docker run -d -p 8000:80 --name test-nginx nginx` 或 `docker run -d -p 8000:80 --name test-nginx nginx:1.14` 

docker run

启动一个容器（即从镜像创建一个实例）。

-d 后台运行，如果不加-d, 想要docker运行，需要保持输入命令行的面板开启，会实时输出docker运行的信息。

-p 8000:80 将容器的80端口映射到主机的8000端口，这个很重要，对于需要对外提供服务的docker来说，如果不写映射，docker容器将无法对外使用

--name test-nginx 给创建的容器命名，方便管理

nginx 启动容器依赖的镜像名称或id

打开浏览器：http://hostip:8000 

刷新两次浏览器，执行docker logs test-nginx  查看docker日志

```

docker logs -f -t --since="2018-09-09" --tail=10  test-nginx

-f : 查看实时日志

-t : 查看日志产生的日期

-tail=10 : 查看最后的10条日志。

test-nginx : 容器名称

```


这里访问的文件在哪里呢？

（1）docker镜像介绍已经告诉我们了
（2）进入docker一探究竟

```
进入容器

docker exec -it 容器id bash

退出容器

exit
```

进入容器后，执行 cd /usr/share/nginx/html/ cat index.html文件，发现这个就是我们在浏览器访问的文件。

执行 cd /etc/nginx/conf.d cat default.conf, 发现这个文件文件就是docker中nginx的配置。

我们更改下这个文件，看下效果。

那么我们怎么将宿主机的项目通过docker访问到呢？

这里我们介绍两种方法

1. 通过执行命令 -v 来映射目录
2. 通过dockerfile 执行命令COPY或ADD


__想要成功启动容器必须注意一下几点__

- 端口被占用 `netstat -ntlp`查看端口占用情况，然后关闭对应端口`kill -9 PID`(对应的进程号)，重新启动 kill
- 同名的docker容器已经在运行了
- 主机防火墙没有开放使用的端口，到后台设置
- 将端口映射，主机端口：docker端口，搞反了

`docker ps -a`

查看所有的容器

`docker ps`

查看所有运行中的容器



# 尝试启动第二个docker容器

在/data 目录下新建 /test/index.html

index.html

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta name="renderer" content="webkit">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <title>入口文件</title>
</head>
<body>
<div id="app">
这个是index.html入口文件
</div>
<!-- built files will be auto injected -->
</body>

</html>

```

`docker run -d -p 9000:80 -v /data/test/:/usr/share/nginx/html --name test-nginx1 nginx`

-v /data/test/:/usr/share/nginx/html 映射目录，将宿主机的/data/test/目录下的文件映射到docker容器/usr/share/nginx/html文件目录下。

打开浏览器访问：http://hostip:9000



