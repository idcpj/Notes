[TOC]

1. 安装python
`docker pull python:3.5`

2. `~/python/demo.py` 写入
```
print("Hello, World!");
```
3.`~/python/`  目录下
`docker run  -v $PWD:/usr/src/myapp  -w /usr/src/myapp python:3.5 python demo.py`

> -v $PWD:/usr/src/myapp :将主机中当前目录下的myapp挂载到容器的/usr/src/myapp
-w /usr/src/myapp :指定容器的/usr/src/myapp目录为工作目录
python demo.py :使用容器的python命令来执行工作目录中的demo.py文件