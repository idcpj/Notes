[TOC]

> [查看如何提交包](https://xuanwo.org/2016/02/15/chocolatey-intro/)
## 安装
[官网](https://chocolatey.org/install)

以管理员权限

安装choco：
`@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

安装库
```
1.php7
2.qq-tim	
4.vagrant	
5.googlechrome	谷歌浏览器
6.nodejs
7.virtualbox
8.notepadplusplus  notepad++
9.wechat 
10.clover  四叶草
11.adobe-creative-cloud
12.boostnote   笔记
13.wox  window的 Alfred
14.filezilla  开源ftp
15. licecap   gif录制屏
16. teamviewer
17. firefox
18. openssh  可以使用ssh 连接服务器
choco install -y php composer tim  tim vagrant virtualbox googlechrome nodejs notepadplusplus wechat clover adobe-creative-cloud boostnote wox filezilla licecap teamviewer firefox openssh

```

### 安装指定版本
```
choco install phpstorm --version 2017.2.4
```

## 升级
### 升级到最高
`choco upgrade phpstorm `

### 升级到指定版本
`choco upgrade phpstorm --version 2017.3.6`

## 疑问
>去检查报错中提供的信息、

1. 如出现验证失败
`choco install -y --ignore-checksums  wechat`