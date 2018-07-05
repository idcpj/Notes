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



## 常用命令
> 提示: 可能所有消息都需要sudo权限

|命令| 用途|
|---|---|
|  `docker rm `  |  删除 container  |
|  `docker  rmi ` |  删除mage  |
|  `docker cp `    |  在hos和 container之间拷贝文件  |
|  `docker commit `  |  保存改动为新的mage  |
