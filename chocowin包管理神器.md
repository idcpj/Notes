[TOC]

## 安装
[官网](https://chocolatey.org/install)
[参考教程]
以管理员权限

安装choco：
`@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

安装库
```
1.php7
2.qq-tim	
3.jdk8-java 环境
4.vagrant	
5.googlechrome	谷歌浏览器
6.nodejs
7.virtualbox
8.notepadplusplus
9.wechat 
10.clover  四叶草
11.adobe-creative-cloud
12.boostnote   笔记
13.wox  window的 Alfred


choco install -y php composer tim jdk8 tim vagrant virtualbox googlechrome nodejs notepadplusplus wechat clover adobe-creative-cloud boostnote wox

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