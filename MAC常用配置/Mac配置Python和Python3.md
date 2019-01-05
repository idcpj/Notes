[TOC]

首先安装 brew

## 安装python3
`brew install python3`
用 `python3 xx.py` 即可
且自带pip3  用 `pip3 install xx` 即可

## 安装 python2.x
`brew install python`
安装后自带pip

>可能通过`python2 xx.py` 执行
>可能通过`pip2  install 执行` 执行
通过查看 ` vim /usr/local/bin/` 查看`python`和`pip2` 对应的但执行方式
>可以在`/usr/local/bin/` 把2去掉

## 手动创建软连接到 /usr/local/bin
demo 
```
ln -s ../Cellar/python@2/2.7.14_1/bin/python2 python2    
ln -s ../Cellar/python@2/2.7.14_1/bin/pip2 pip2
```

## 修改执行命令的路径
`vim /etc/path`
```
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```
把`/usr/local/bin`放在`/usr/bin/`之前，即可有限运行brew 安装的python



