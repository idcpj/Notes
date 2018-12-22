
[TOC]

   
## 软件下载

先通过`brew search xxx `  进行查找  然后通过 `brew cask install xxx`  或 `brew install xxx ` 安装
    
## 解除对sudo对限制
`El Capitan` 加入了`Rootless`机制
重启按住 Command+R，进入恢复模式，打开Terminal。

`csrutil disable`   关闭
`csrutil enable`    开启

## MAC软件
**Homebrew**
[官网](https://brew.sh/index_zh-cn.html)

```
brew install  mycli       //   mycli -uroot -proot  为MySQL命令行客户端，提供语法高亮和提示功能的工具
brew cask install qlstephen   //可以让您查看没有文件扩展名的纯文本文件
brew cask install qlcolorcode    //在预览源代码文件，高亮代码
brew cask install qlmarkdown		//Markdown文件转换成静态页面预览
brew cask install quicklook-json  		//格式化预览JSON文件
brew cask install quicklook-csv       //预览.CSV文件
brew cask install qlimagesize		//显示图像大小和分辨率
brew cask install quicklook-pat		//预览Adobe Photoshop图案文件
brew cask install betterzipQL      //预览压缩文件
brew cask install qlimagesize   //标题栏中显示图片分辨率及文件大小
brew cask install launchrocket      //在系统偏好设置即可启动apache,mysql等
```


**cakebrew**  界面版homebrew	[官网](https://www.cakebrew.com/)

**ndm**    查看本地`npm`安装的包客户端软件 [官网](https://720kb.github.io/ndm/)

**Klib**   全新的 Kindle、iBooks 标注管理工具。  [官网](http://klib.me/cn/)

**AppCleaner**  彻底卸载不需要的应用程序 [官网](http://freemacsoft.net/appcleaner/)

**Alfred**   效率神器

**让电脑识别 NTFS**  [简书地址](https://www.jianshu.com/p/6abf7946f56b) 推荐第三个

**Aria2GUI** 下载快速  可以突破百度云限制
在添加任务时候选择最大连接数为30 左右

## 其他配置

### 永久配置别名
`vim ~/.bashrc`
输入内容`alias ll='ls -l'`
执行生效`source .bashrc`
如果不行
```
~/.bash_profile
#在里面加入一行：
source ~/.bashrc
```
>`.bash_profile`文件是用户登陆终端的时候会自动执行的文件

## 多线程下载
`brew install axel`

下载 - 高速下载百度云
`axel -n 30 http://www.demo.com`


## mac 命令
4. 下载大文件时不希望电脑自动休眠，但需要关闭屏幕？
用 `pmset displaysleep` ；
6. 让通知快点消失：
`defaults write com.apple.notificationcenterui bannerTime 3；`
7. 使不活动的图标进入半透明状态：
`defaults write com.apple.dock showhidden -bool TRUE; killall Dock`
7. 让 Dock 瞬间出现/消失：
`defaults write com.apple.dock autohide-time-modifier -int 0;killall Dock`
8. 在 Launchpad 里放下更多图标（注意，这条命令会重新排列 Launchpad 图标顺序）：
`defaults write com.apple.dock springboard-columns -int 8; defaults write com.apple.dock springboard-rows -int 7; defaults write com.apple.dock ResetLaunchPad -bool TRUE; killall Dock`

## 其他命令
```
php index.php &   		#在命令后加 & 让进程在后台运行
jobs –l 				#查看后台运行的进程
fg %n 					#让后台运行的进程 n 到前台来
bg %n 					#让进程 n 到后台去;
```
## 查看端口占用
`lsof -i:80`
 查看所有端口
 `netstat -nat |grep LISTEN`
## 复制文件路径
1.方法一
`option + command + C`
2.方法二
文件右键,在按住option