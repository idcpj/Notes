[TOC]

## 常用命令
执行文件的命令
```
#demo.sh文件
cd /tmp

$ source demo.sh  
```
## 案例
### 基础案例
```bash
# vim hello.sh 
===
#!/bin/bash
# 第一个demo
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
echo -e "Hello World! \a \n"
exit 0
===
# sh hello.sh
>>> hello word
```
>`export PATH `设置命令所在路径
>`echo -e` 特殊输出
>`exit 0`  `0`为数字零

|字符|说明|
|---|---|
|	|	|
|`\a`| 发出警告声；|
|`\b`| 删除前一个字符；|
|`\c`| 最后不加上换行符号；|
|`\f`| 换行但光标仍旧停留在原来的位置；|
|`\n`| 换行且光标移至行首；|
|`\r`| 光标移至行首，但不换行；|
|`\t`| 插入tab；|
|`\v`| 与\f相同；|
|`\\ `|插入\字符；|
|`\nnn`| 插入nnn（八进制）所代表的ASCII字符；|

### 对谈式脚本
```bash
#!/bin/bash
# Program:
# User inputs his first name and last name. Program shows his full name.
# History:
# 2015/07/16 VBird First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

read -p "Please input your first name: " firstname       #提示使用者输入  把内容肚子到firstname
read -p "Please input your last name: " lastname        #提示使用者输入 
echo -e "\nYour full name is: ${firstname} ${ lastname}" #结果由萤幕输出
```
## 生成日期文件
```bash
#!/bin/bash
# Program:
# Program creates three files, which named by user's input and date command.
# History:
# 2015/07/16 VBird First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

# 1.让使用者输入档案名称，并取得fileuser这个变数； 
echo -e "I will use 'touch' command to create 3 files." #纯粹显示资讯 
read -p "Please input your filename: " fileuser          #提示使用者输入

# 2.为了避免使用者随意按Enter ，利用变数功能分析档名是否有设定？
filename=${fileuser:-"filename"}            #开始判断有否设定档名

# 3.开始利用date指令来取得所需要的档名了； 
date1=$(date --date='2 days ago' +%Y%m%d)   #前两天的日期 
date2=$(date --date='1 days ago' +%Y%m%d)   #前一天的日期 
date3=$(date +%Y%m%d)                       #今天的日期 
file1=${filename}${date1}                   #底下三行在设定档名
file2=${filename}${date2}
file3=${filename}${date3}

# 4.将档名建立吧！
touch "${file1}"                            #底下三行在建立档案
touch "${file2}"
touch "${file3}"
```
>`filename=${fileuser:-"filename"}`  判断是否有`fileuser` 没有使用预设的`filename`,加上`:` 如果变量为空也使用预设的值


## 变量
```bash
#赋值
$ name="cpj"

#输出
$ echo $name 或${name}
>> cpj

#取消
$ unset name

```
|数设定方式 |	str 没有设定 |	str 为空字串 |	str 已设定非为空字串|
|---|---|---|---|
|var=${str-expr} |	var=expr|		var= | var=$str|
|var=${str:-expr} |	var=expr|		var=expr | var=$str|
|var=${str+expr} |	var=	|		var=expr | var=expr|
|var=${str:+expr}} |	var=|		var= | var=expr|
|var=${str=expr} |	str=expr,var=expr|		str 不变,var= | str 不变,var=$str|
|var=${str:=expr} |		str=expr,var=expr|		str=expr,var=expr | str 不变,var=$str|
|var=${str?expr} |		exp 输出至 stderr|		var= | var=$str|
|var=${str:?expr} |		exp 输出至 stderr|		expr 輸出至 stderr | var=$str|


