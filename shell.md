[TOC]

## Shell Script

简单demo
```
[dmtsai@study bin]$ vim hello.sh
#!/bin/bash
# Program:
#       This program shows "Hello World!" in your screen.
# History:
# 2015/07/16	VBird	First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
echo -e "Hello World! \a \n"
exit 0
---
```

```
#执行
sh hello.sh
#输出  Hello World !
```
>第一行#!/bin/bash在宣告这个script使用的shell名称：
>主要环境变数的宣告：将一些重要的环境变数设定好,如PATH与LAN,直接使用外部指令

## 对谈式脚本

```
[dmtsai@study bin]$ vim showname.sh 
#!/bin/bash
# Program:
# User inputs his first name and last name. Program shows his full name.
# History:
# 2015/07/16 VBird First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

read -p "Please input your first name: " firstname       #提示使用者输入 
read -p "Please input your last name: " lastname        #提示使用者输入 
echo -e "\nYour full name is: ${firstname} ${ lastname}" #结果由萤幕输出
```
>
