[TOC]

## 常用命令
执行文件的命令
```
#demo.sh文件
cd /tmp

$ source demo.sh  
```
## demo

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


