[TOC]

## 开机启动软件
window 10 
在该地址中放入快捷快捷方式即可
`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`

## 激活window
1. 管理员模式打开`cmd`,一次输入
```
slmgr.vbs /upk
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms zh.us.to
slmgr /ato
```
## chrome 浏览器的 复制bash 功能
![](images/Snipaste_2018-12-06_12-56-50.png)

如果复制的是`Copy as Curl(baash)`,且电脑安装git bash
则可在git bash 中执行