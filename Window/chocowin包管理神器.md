[TOC]

> [查看如何提交包](https://xuanwo.org/2016/02/15/chocolatey-intro/)
## 安装
[官网](https://chocolatey.org/install)

以管理员权限

安装choco：
`@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

安装库
1. php7
2. tim	
4. vagrant	
5. googlechrome	
6. nodejs
7. virtualbox
8. notepadplusplus  
10. clover  
11. adobe-creative-cloud
12. boostnote   
14. filezilla  
15. licecap   
16. teamviewer
17. firefox
18. openssh  
19. postman
20. git
21. ConEmu 

```
choco install -y php composer tim  vagrant virtualbox googlechrome nodejs notepadplusplus  clover adobe-creative-cloud boostnote  filezilla licecap teamviewer firefox openssh postman git ConEmu 
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