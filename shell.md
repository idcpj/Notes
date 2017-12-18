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

#如果赋予执行权限可直接使用
chmod a+x hello.sh; 
./hello.sh
```
>第一行#!/bin/bash在宣告这个script使用的shell名称：
>主要环境变数的宣告：将一些重要的环境变数设定好,如PATH与LAN,直接使用外部指令

## source, sh script, ./script
`sh script` 与 `./script` 只是是否文件是执行文件的区别,如果,则可直接使用`./script`
`source` 与`sh script`  `source`在父程序中执行,即执行的变量会保留在父程序中
```
[dmtsai@study bin]$ source showname.sh 
Please input your first name: VBird 
Please input your last name:   Tsai

Your full name is: VBird Tsai 
[dmtsai@study bin]$ echo ${firstname} ${lastname} 
VBird Tsai   <==嘿嘿！有资料产生喔！
```


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

read -p "Please input your first name: " firstname       #提示使用者输入 把值赋值给firstname
read -p "Please input your last name: " lastname        #提示使用者输入 
echo -e "\nYour full name is: ${firstname} ${ lastname}" #结果由萤幕输出
```
## 各种符号的运用

### 判断符号 `[ ]`
判断为空
`[ -z "${HOME}" ] ; echo $?`
不为空 输出`1` 为空 `0`

判断相等
```
read -p "Please input (Y/N): " yn
[ "${yn}" == "Y" -o "${yn}" == "y" ] && echo "OK, continue" && exit 0
[ "${yn}" == "N" -o "${yn}" == "n" ] && echo "Oh, interrupt!" && exit 0
echo "I don't know what your choice is" && exit 0
```
>`-o` 或运算符  可用`||` 替换
>`[□"$HOME"□==□"$MAIL"□]`  比较运算时,`□` 必须为不能为空,且必是空格
>在中括号[] 内的每个元件都需要有空白键来分隔；
在中括号内的变数，最好都以双引号括号起来；
在中括号内的常数，最好都以单或双引号括号起来。

### 命令行中传参数
```
echo "The script name is ==> ${0}"
echo "Total parameter number is ==> $#"
[ "$#" -lt 2 ] && echo "The number of parameter is less than 2. Stop here." && exit 0
echo "Your whole parameter is ==> '$@'"
echo "The 1st parameter ==> ${1}"
echo "The 2nd parameter ==> ${2}"
```

执行结果
```
[dmtsai@study bin]$ sh how_paras.sh theone haha quot 
The script name is ==> how_paras.sh        <==档名 
Total parameter number is ==> 3                   <==果然有三个参数 
Your whole parameter is == > 'theone haha quot' <==参数的内容全部 
The 1st parameter ==> theone              <==第一个参数 
The 2nd parameter ==> haha                <==第二个参数
```
>$# ：代表后接的参数『个数』，以上表为例这里显示为『 4 』；
"$@" ：代表『 "$1" "$2" "$3" "$4" 』之意，每个变数是独立的(用双引号括起来)；
"$*" ：代表『 "$1 c $2 c $3 c $4" 』，其中c为分隔字元，预设为空白键，所以本例中代表『 "$1 $2 $3 $4" 』之意。

## 条件判断式

### if .... then

```
if [条件判断式]; then
	当条件判断式成立时，可以进行的指令工作内容；
fi    <==将if反过来写，就成为fi啦！结束if之意！
```
单提条件判断
```
read -p "Please input (Y/N): " yn

if [ "${yn}" == "Y" ] || [ "${yn}" == "y" ]; then
	echo "OK, continue"
	exit 0
fi
if [ "${yn}" == "N" ] || [ "${yn}" == "n" ]; then
	echo "Oh, interrupt!"
	exit 0
fi
echo "I don't know what your choice is" && exit 0
```

多条件判断
```
read -p "Please input (Y/N): " yn

if [ "${yn}" == "Y" ] || [ "${yn}" == "y" ]; then
	echo "OK, continue"
elif [ "${yn}" == "N" ] || [ "${yn}" == "n" ]; then
	echo "Oh, interrupt!"
else
	echo "I don't know what your choice is"
fi
```
