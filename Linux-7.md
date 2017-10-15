#Linux/7
---
 
[TOC]

## 常用快捷键
```
cd -    进入上次目录(在目录中切换)
crtl+r  **在历史命令中搜索**
crtl+u  从光标所在位置删除到行首
ps      查看进程
man ls  查看帮助手册
Ctrl+z/fg   切换后台/切换到前台
cat /etc/group | grep -E "shiyanlou"	搜索并打印某个文件
```
## 设置命令别名
- 设置临时别名
```
alias www='cd /var/www' 
```
-  永久别名
```
cd ~
ll -a
vim .bashrc
    alias rm='rm -i'
    alias cp='cp -i'
    alias mv='mv -i'
    alias lsl='ll -a'  #新增

```
## 杀掉进程
```
[root@localhost www]# ps
  PID TTY          TIME CMD
 2928 pts/0    00:00:00 sudo
 2929 pts/0    00:00:00 su
 2930 pts/0    00:00:00 bash
 3848 pts/0    00:00:00 ps
[root@localhost www]# kill 2929
```
## 文件处理
```
mkdir -p    递归创建目录
cp -a       复制  
                    -r   复制目录
                    -p  连带文件属性复制
                    -d   若源文件是链接文件.则复制链接属性
                    -a  相当于  -pdr(前三个相加)
ln -s       创建链接
                    -s 创建软链接   相当于windows的快捷方式
```
## 搜索内容
```
/hello	    向下搜索
?hello      向上搜索  
n, N	    在/或?搜索时 按n 继续搜索 按N反向搜索
```
## 开关机操作
```
    shutdown 
            -k ： 不要真的关机，只是发送警告讯息出去！
            -r ： 在将系统的服务停掉之后就重新开机(常用)
            -h ： 将系统的服务停掉后，立即关机。(常用)
            -c ： 取消已经在进行的shutdown 指令内容。
shutdown -h now
shutdown -h 20:25
shutdown -h +10
shutdown -r now
reboot 关机
```
## 文件/文件夹权限
### chgrp 改变组
```
-rw-rw-r--. 1 vagrant vagrant 15 Aug 17 08:34 test
[root@localhost vagrant]# chgrp root test.php 
-rw-rw-r--. 1 vagrant root    15 Aug 17 08:34 test
```
### chown 改变档案拥有者和组
```
-rw-rw-r--. 1 vagrant vagrant    15 Aug 17 08:34 test
[root@localhost vagrant]#  chown root:sftp test
-rw-rw-r--. 1 root    sftp    15 Aug 17 08:34 test
```
### chmod  改变权限
`r`可读    `w`可写  `w`可执行( 对目录而言是**能否进入该目录**)

    r:4 
    w:2 
    x:1
    owner = rwx = 4+2+1 = 7 
    group = rwx = 4+2+1 = 7 
    others= --- = 0+0+0 = 0
```
-rw-r--r--. 1 root    root    26 Aug 16 06:10 test.php
[root@localhost vagrant]# chmod 755 test.php 
-rwxr-xr-x. 1 root    root    26 Aug 16 06:10 test.php
```
    chmod u=rwx,g=rx,o=r test.php       
    chmod a+w test.php
            -a all 所有分组
            所有组加上可写权限

## 目录
### 根目录
|目录|说明|
|---|---|
|/bin|可执行文件|
|/boot|放置开机会使用到的档案|
|/dev|周边设备,以文件形式放置在此目录|
|/etc|系统设置文件,其他权限可看,root可写|
|/lib|/lib放置的则是在开机时会用到的函式库|
|/media|放置的就是可移除的装置啦|
|/mnt|暂时挂载某些额外的装置|
|/opt|给第三方软体放置的目录|
|/run|规定系统开机后所产生的各项信息|
|/sbin|为开机过程中所需要的,开机、修复、还原系统所需要的指令|
|/srv|『service』的缩写,如WWW, FTP|
|/tmp|程序暂时放置档案的地方|
|/usr|看下表|
|/home|用户目录|
|/lib|用来存放与/lib 不同的格式的二进位函式库|
|/root|系统管理员(root)的家目录|

### /usr  (Unix Software Resource的缩写)

|目录|说明|
|---|---|
|/usr/bin/|/bin为此快捷目录|
|/usr/lib/|/lib为此快捷目录|
|/usr/local/|自行安装的软件|
|/usr/sbin/|/sbin为此快捷目录|
|/usr/games/|与游戏相关的文档|
|/usr/include/|c/c++等程式语言的档头(header)与包含档(include)放置处|
|/usr/libexec/|不被一般使用者惯用的执行档或脚本(script)|
|/usr/lib<qual>/|与/lib<qual>/功能相同，因此目前/lib<qual> 就是连结到此目录中|
|/usr/src/|一般原始码建议放置到这里|

### /var  
|目录|说明|
|---|---|
|/usr/cache/|程序运行时产生的一些暂存档|
|/usr/lib/|程式本身执行的过程中，需要使用到的资料档案放置的目录,如MySQL资料库放置在/var/lib/mysql/|
|/usr/lock/|些装置或者是档案资源一次只能被一个应用程式所使用,如刻录机|
|/usr/mail/|放置个人电子邮件信箱的目录|
|/usr/run/|/run 为此快捷键|
|/usr/spool/|排队等待其他程式使用的资料，如系统收到新邮件|
|/usr/log/|软件或系统的日志|
|/usr/log/|软件或系统的日志|
|/usr/log/|软件或系统的日志|

![LInux目录树图](https://dn-anything-about-doc.qbox.me/linux_base/4-1.png)

---

## 目录
```
cd [空] 进入当前登录者的home
pwd     显示当前的目录 (Print Working Directory)
mkdir   新建目录
        mkdir -p test1/test2/test3/test4  递归建立目录
        mkdir -m 711 test2   建立权限为711的存档
rmdir   删除空目录
        rmdir -p test1/test2/test3/test4 递归删除目录
```

## 路径
```
[root@localhost tmp]# PATH="${PATH}:/root" 添加路径 /root 路径
[root@localhost tmp]# echo $PATH 
/sbin:/bin:/usr/sbin:/usr/bin:/root
```

## 复制、删除与移动:cp,rm,mv
### 复制
```
cp [option] source1 source2 
    -a 档案的属性,权限,时间一起复制(常用于备份)
    -i 若目标已经存在,则进行询问
    -r 可以复制目录(可能会改变文件属性,可用-a 代替)
    -u 目标文档与源文档有差异复制(常用于备份)
```
### 删除
```
mv  [-fir]档案或目录
    -f 忽略不存在的档案，不会出现警告讯息
    -i 在删除前会询问 (y/n)
    -r 递归删除 
```
### 移动(重命名)
```
 mv [options] source1 source2 source3 .... directory 
    -f 如果目标档案已经存在，不会询问而直接覆盖
    -i 如果目标已经存在,就会询问是否覆盖 (y/n)
    -u  若目标档案已经存在，且source 比较新，才会更新
```

## 档案内容查阅
```
cat     由第一行开始显示档案内容
tac     从最后一行开始显示，可以看出tac 是cat 的倒着写！
nl      显示的时候，顺道输出行号！
more    一页一页的显示档案内容
less    与more 类似，但是比more 更好的是，他可以往前翻页！
head    只看头几行
tail    只看尾巴几行
od      以二进位的方式读取档案内容！
```

## 修改档案时间或建置新档
- modification time (mtime):    文档内容变更时变化
- status time (ctime):          文档权限与属性改变时变化
- access time (atime):          读取该文档时,变化

```
touch [-acdmt]档案
    -a 仅修订access time
    -c 仅修改档案的时间，若该档案不存在则不建立新档案；
    -d 后面可以接欲修订的日期而不用目前的日期
    -m 仅修改mtime ；
    -t 后面可以接欲修订的时间而不用目前的时间，格式为[YYYYMMDDhhmm]
```
```
touch -d "2 days ago" test.php  变更ctime 
```
## 档案预设权限：umask
** 查看当前属性**
```
[root@study ~]# umask
0022 
[root@study ~]# umask -S
u=rwx,g=rx,o=rx
```
*注1:0222 先只需要考虑后三位022 , 删掉什么权限就写什么数,如需要删掉写的权限(r=4,w=2,x=1) 则删除2*

*注2:若使用者建立为『档案』则预设『没有可执行( x )权限』，亦即只有rw这两个项目，也就是最大为666*

**预设**
之后新创建的文件和目录会按照新设置的权限
```
//设置权限
[root@study ~]# umask 002 
//新创建的文件为 -rw-rw-r--
//新创建的目录为 drwxrwxr-x
```
## 设定隐藏属性
```
chattr [+-=][ASacdistu]档案或目录名称

    + ：增加某一个特殊参数，其他原本存在参数则不动。
    - ：移除某一个特殊参数，其他原本存在参数则不动。
    = ：设定一定，且仅有后面接的参数
```
|参数|说明|
|---|---|
|A|当设定了A 这个属性时，若你有存取此档案(或目录)时，他的存取时间atime 将不会被修改，可避免I/O 较慢的机器过度的存取磁碟。(目前建议使用档案系统挂载参数处理这个项目)|
|S|一般档案是非同步写入磁碟的(原理请参考前一章sync的说明)，如果加上S这个属性时， 当你进行任何档案的修改，该更动会『同步』写入磁碟中。|
|a|当设定a 之后，这个档案将只能增加资料，而不能删除也不能修改资料，只有root 才能设定这属性|
|c|这个属性设定之后，将会自动的将此档案『压缩』，在读取的时候将会自动解压缩，     但是在储存的时候，将会先进行压缩后再储存(看来对于大档案似乎蛮有用的！)|
|d|当dump 程序被执行的时候，设定d 属性将可使该档案(或目录)不会被dump 备份|
|i|这个i 可就很厉害了！他可以让一个档案『不能被删除、改名、设定连结也无法写入或新增资料！』 对于系统安全性有相当大的助益！只有root 能设定此属性|
|s|当档案设定了s 属性时，如果这个档案被删除，他将会被完全的移除出这个硬碟空间，所以如果误删了，完全无法救回来了喔！|
|u|与s 相反的，当使用u 来设定档案时，如果该档案被删除了，则资料内容其实还存在磁碟中，可以使用来救援该档案喔！|

*注1:属性设定常见的是**a** 与 **i** 的设定值，而且很多设定值必须要身为root 才能设定*
例子:
```
[root@study tmp]# touch attrtest
[root@study tmp]# chattr +i attrtest 
[root@study tmp] # rm attrtest         
rm: remove regular empty file `attrtest'? y
rm: cannot remove `attrtest': Operation not permitted
//即使root用户也无法删除
//取消i属性
[root@study tmp]# chattr -i attrtest
```
### 显示隐藏属性
```
 lsattr [-adR]档案或目录
    -a ：将隐藏档的属性也秀出来；
    -d ：如果接的是目录，仅列出目录本身的属性而非目录内的档名；
    -R ：连同子目录的资料也一并列出来！ 
```
```
[root@study tmp]# lsattr passwd
----ia---------- passwd
```
## SUID/SGID/SBIT 权限设定
```
4 为SUID
2 为SGID
1 为SBIT
[root@study tmp]# chmod 6755 test;  //赋值
```
## file 观察档案类型
```
file /usr/bin/passwd
```
## 指令档名的搜寻
### which
```
[vagrant@localhost ~]$ which ifconfig       搜索命令
/usr/sbin/ifconfig
```
### whereis
```
root@study ~]# whereis ifconfig
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
```
### find
#### 时间相关搜索
```
find [PATH] [option] [action] 
    -mtime n ：n 为数字，意义为在n 天之前的『一天之内』被更动过内容的档案；
    -mtime +n ：列出在n 天之前(不含n 天本身)被更动过内容的档案档名；
    -mtime -n ：列出在n 天之内(含n 天本身)被更动过内容的档案档名。
    -newer file ：file 为一个存在的档案，列出比file 还要新的档案档名
    
例子
find / -mtime 0                 将过去系统上面24小时内有更动过内容(mtime)的档案列出
find /etc -newer /etc/passwd    寻找/etc底下的档案，如果档案日期比/etc/passwd新就列出 
```
![find 相关的时间参数意义](http://linux.vbird.org/linux_basic/0220filemanager/find_time.gif)

#### 使用者或群组名称有关的参数
```
-uid n      ：n为数字，这个数字是使用者的帐号ID，亦即UID ，这个UID 是记录在
-gid n      ：n 为数字，这个数字是群组名称的ID，亦即GID，这个GID 记录在
-user name  ：name 为使用者帐号名称喔！例如dmtsai
-group name ：name 为群组名称喔，例如users ；
-nouser     ：寻找档案的拥有者不存在/etc/passwd 的人！
-nogroup    ：寻找档案的拥有群组不存在于/etc/group 的档案！
              当你自行安装软体时，很可能该软体的属性当中并没有档案拥有者，
              这是可能的！在这个时候，就可以使用-nouser 与-nogroup 搜寻。
例子:
[root@study ~]# find /home -user dmtsai     搜寻/home底下属于dmtsai的档案
```
#### 与档案权限及名称有关的参数

```
-name filename：搜寻档案名称为filename 的档案；
   -size [+-]SIZE：搜寻比SIZE 还要大(+)或小(-)的档案。这个SIZE 的规格有：
                   c: 代表byte， k: 代表1024bytes。所以，要找比50KB
                   还要大的档案，就是『 -size +50k 』
   -type    TYPE ：搜寻档案的类型为TYPE 的，类型主要有：一般正规档案(f), 装置档案(b, c),
                   目录(d), 连结档(l), socket (s), 及FIFO (p) 等属性。
 例子:
 [root@study ~]# find /etc -name passwd        找出passwd文档
 [root@study ~]# find / -name "*passwd*"    找出档名包含了passwd这个关键字的档案(记得加引号)
 [root@study ~]# find / -size +1M           找出大于1M的
```
#### 額外可進行的動作
```
-exec command ：command 为其他指令，-exec 后面可再接额外的指令来处理搜寻到的结果。
-print ：将结果列印到萤幕上，这个动作是预设动作！

例子;
[root@localhost home]# find / -name passwd -exec ls -l {} \;
total 0
-r--r--r--. 1 root root 0 Aug 29 02:22 index
dr-xr-xr-x. 2 root root 0 Aug 29 02:22 perms
-rw-r--r--. 1 root root 1398 Aug  3 09:04 /etc/passwd
-rw-r--r--. 1 root root 188 Jun 10  2014 /etc/pam.d/passwd

注释:{}代表的是由find找到的内容
      -exec 一直到\; 中间就是需要插入的命令
       `;` 在bash 环境下是有特殊意义的，因此利用反斜线来跳脱。

```
## 列出系统上的所有磁碟列表
```
[root@study ~]# lsblk [-dfimpt] [device] 
    选项与参数：
    -d ：仅列出磁碟本身，并不会列出该磁碟的分割资料
    -f ：同时列出该磁碟内的档案系统名称
    -i ：使用ASCII 的线段输出，不要使用复杂的编码(再某些环境下很有用)
    -m ：同时输出该装置在/dev 底下的权限资料(rwx 的资料)
    -p ：列出该装置的完整档名！而不是仅列出最后的名字而已。
    -t ：列出该磁碟装置的详细资料，包括磁碟伫列机制、预读写的资料量大小等
    
[root@localhost vagrant]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk 
├─sda1                    8:1    0    1M  0 part 
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part 
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]


注释：
    NAME：就是装置的档名啰！会省略/dev 等前导目录！
    MAJ:MIN：其实核心认识的装置都是透过这两个代码来熟悉的！分别是主要：次要装置代码！
    RM：是否为可卸载装置(removable device)，如光碟、USB 磁碟等等
    SIZE：当然就是容量啰！
    RO：是否为唯读装置的意思
    TYPE：是磁碟(disk)、分割槽(partition) 还是唯读记忆体(rom) 等输出
    MOUTPOINT：就是前一章谈到的挂载点！
```
## 列出磁碟的分割表类型与分割资讯
```
[root@study ~]# parted device_name print

例子:
[root@localhost vagrant]# parted /dev/sda print
Model: ATA VBOX HARDDISK (scsi)     #磁碟的模组名称(厂商) 
Disk /dev/sda: 42.9GB               #磁碟的总容量
Sector size (logical/physical): 512B/512B   #磁碟的每个逻辑/物理磁区容量
Partition Table: msdos                      #分割表的格式(MSDOS(MBR)/GPT)
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  2097kB  1049kB  primary
 2      2097kB  1076MB  1074MB  primary  xfs          boot
 3      1076MB  42.9GB  41.9GB  primary               lvm

```
## 磁碟分割
MBR分割表请使用fdisk分割， GPT分割表请使用gdisk分割！
## gdisk
```
[root@localhost dev]# fdisk /dev/sda
Command (m for help): p

Disk /dev/sda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000a5130

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1            2048        4095        1024   83  Linux
/dev/sda2   *        4096     2101247     1048576   83  Linux
/dev/sda3         2101248    83886079    40892416   8e  Linux LVM
Command (m for help): q  #离开  不保存操作
```
## 用fdisk 新增分割槽
```

```