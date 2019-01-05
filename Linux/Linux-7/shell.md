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

```bash
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
```bash
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
```bash
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
`$0`->文件名
`$1` -> 第一个参数
`$2` -> 第二个参数

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
```bash
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
```bash
read -p "Please input (Y/N): " yn

if [ "${yn}" == "Y" ] || [ "${yn}" == "y" ]; then
	echo "OK, continue"
elif [ "${yn}" == "N" ] || [ "${yn}" == "n" ]; then
	echo "Oh, interrupt!"
else
	echo "I don't know what your choice is"
fi
```

### case ..... esac
```bash
case $变数名称in    <==关键字为case ，还有变数前有钱字号 
  "第一个变数内容" )    <==每个变数内容建议用双引号括起来，关键字则为小括号)
	程式段
	;;             <==每个类别结尾使用两个连续的分号来处理！
  "第二个变数内容" )
	程式段
	;; 
  * )                   <==最后一个变数内容都会用*来代表所有其他值
	不包含第一个变数内容与第二个变数内容的其他程式执行段
	exit 1
	;; 
esac                   <==最终的case结尾！『反过来写』思考一下！
```


demo
```
case ${1} in
  "hello")
	echo "Hello, how are you ?"
	;;
  "")
	echo "You MUST input parameters, ex> {${0} someword}"
	;;
  *)    #其实就相当于万用字元，0~无穷多个任意字元之意！
	echo "Usage ${0} {hello}"
	;;
esac
```

### for...do...done 的固定循环

```

for var in con1 con2 con3 ...
do
	程式段
done
```

demo
```
for animal in dog cat elephant
do
	echo "There are ${animal}s.... "
done
```
一次输出`dog `,`cat`,`elephant`

### for...do...done 的数值处理

```
for ((初始值;限制值;执行步阶))
do
	程式段
done
```
demo
```
read -p "Please input a number, I will count for 1+2+...+your_input: " nu

s=0
for (( i=1; i<=${nu}; i=i+1 ))
do
	s=$((${s}+${i}))
done
echo "The result of '1+2+3+...+${nu}' is ==> ${s}"
```

### shell script 的追踪与debug
```

[dmtsai@study ~]$ sh [-nvx] scripts.sh 
选项与参数：
-n ：不要执行script，仅查询语法的问题；
-v ：再执行sccript 前，先将scripts 的内容输出到萤幕上；
-x ：将使用到的script 内容显示到萤幕上，这是很有用的参数！
```
demo 
```
按步执行
sh -x demo1.sh 

```
