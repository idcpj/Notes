[TOC]
> [官方镜像列表](https://hub.docker.com/explore/)

## 安装
1. mac
`brew cask install docker`
[下载dmg格式](https://download.docker.com/mac/stable/Docker.dmg)

    镜像加速
    在 `Preferences`->`Daemon`->`Registry mirrors`->`Apply Restart`

2.Linux
```
yum -y install docker-io
```


## 镜像加速器
> [点击跳转](https://bingohuang.gitbooks.io/docker_practice/content/install/mirror.html)



## 镜像

查找镜像
`sudo docker search httpd`

列出镜像
`sudo docker images `

获取新镜像
格式:`sudo docker pull [选项] [Docker Registry地址]<仓库名>:<标签>`
如:`sudo docker pull training/webap`

使用镜像
`sudo docker run httpd`
docker run -d -P training/webapp python app.py

## 启动 docker
```bash
$ service docker start
$ ps aux | grep docker  #检查是否开启
$ sudo docker info  #查看docke 消息
```

## 使用镜像来创建一个容器
运行后就会进入ubuntu 的容器
```
runoob@runoob:~$ docker run -t -i ubuntu:15.10 /bin/bash
root@e218edb10161:/# 
```

## 常用命令
> 提示: 可能所有消息都需要sudo权限
```
docker ps 		//查看系统中运行的docker容器
docker kill [container] 	//删除docker容器
docker stop [container] 	//停止正在运行的docker容器
docker attach/exec [container] 		//进入容器
docker run 		//运行镜像，生成容器
docker images 		//查看系统中存在的docker镜像
docker rmi [image] 	//删除镜像
docker build 	//生成镜像
docker pull 	//拉取镜像
docker push 	//上传镜像 
docker search 	//搜索镜像
```