
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


**iterm2**    更好的命令行窗口	[官网](http://www.iterm2.com/)

**Oh my zsh**    拥有大量的有用的功能，助手，插件，主题，等特性的命令行工具插件	 [官网](http://ohmyz.sh/) 


**ndm**    查看本地`npm`安装的包客户端软件 [官网](https://720kb.github.io/ndm/)

**Sparkle**    可视化网页设计工具。	 [官网](https://sparkleapp.com/)  

**Klib**   全新的 Kindle、iBooks 标注管理工具。  [官网](http://klib.me/cn/)

**AppCleaner**  彻底卸载不需要的应用程序 [官网](http://freemacsoft.net/appcleaner/)

**FinderGo Finder** 中快速打开终端，定位到目录
**Cleaner for Xcode**  Xcode 的清理工具，清理几十G应该不是问题

**BetterZip 3**     压缩解压缩工具支持格式 ZIP、TAR、TGZ、TBZ、TXZ (new)、7-ZIP、RAR。

**Alfred**   效率神器

**Charles Mac**   用于HTTP信息抓包工具

**CodeRunner**   无需安装环境直接运行各种语言代码

**让电脑识别 NTFS**  [简书地址](https://www.jianshu.com/p/6abf7946f56b) 推荐第三个

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
