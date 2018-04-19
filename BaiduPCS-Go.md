[TOC]

> [github](https://github.com/iikira/BaiduPCS-Go)

> 快速下载百度云盘上的东西

## 下载/安装
[下载地址](https://github.com/iikira/BaiduPCS-Go/releases)

## 登录
`BaiduPCS-Go login`

## 下载
```
BaiduPCS-Go d [网盘的路径]
BaiduPCS-Go d /我的资源
```

## 上传
```
# 注意全部使用 "/"的斜线

# 将本地的 C:\Users\Administrator\Desktop\1.mp4 上传到网盘 /视频 目录
BaiduPCS-Go upload C:/Users/Administrator/Desktop/1.mp4 /视频

# 将本地的 C:\Users\Administrator\Desktop\1.mp4 和 C:\Users\Administrator\Desktop\2.mp4 上传到网盘 /视频 目录
BaiduPCS-Go upload C:/Users/Administrator/Desktop/1.mp4 C:/Users/Administrator/Desktop/2.mp4 /视频

# 将本地的 C:\Users\Administrator\Desktop 整个目录上传到网盘 /视频 目录
BaiduPCS-Go upload C:/Users/Administrator/Desktop /视频
```
## 设置下载最大并发数

```
#查看 配置帮助
config set -h

//设置配置
config set -max_parallel 250
```
