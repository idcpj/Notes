[TOC]

## 安装
1. mac
`brew cask install docker`
[下载dmg格式](https://download.docker.com/mac/stable/Docker.dmg)

    镜像加速
    在 `Preferences`->`Daemon`->`Registry mirrors`->`Apply Restart`

2.Linux
```
sudo wget -g0- https://getdocker.com/ | sh
sudo usermod -aG docker xxx      #xxx为 whoami的结果
```
## 镜像
列出镜像
`docker images `
获取新镜像
`docker pull php`
查找镜像
`docker search httpd`
使用镜像
`docker run httpd`



## 常用命令

|命令| 用途|
|---|---|
|  `docker pull`	|   获取 Image |
|  `docker build`   |创建mage   |
|  `docker images` | 列出mage |
|  `docker run` | 运行 container |
|  `docker ps ` |  列出 container |

|命令| 用途|
|---|---|
|  `docker rm `  |  删除 container  |
|  `docker  rmi ` |  删除mage  |
|  `docker cp `    |  在hos和 container之间拷贝文件  |
|  `docker commit `  |  保存改动为新的mage  |