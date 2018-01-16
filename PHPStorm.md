# PHPStorm
[TOC]

## 激活地址
http://idea.liyang.io

## 汉化和配置
汉化替换lib下文件
文件在oneDrive

## 连接Mysql
>view->工具窗口->database
>若无法下载驱动,在XML文件中mysql的地址:[下载](http://download.jetbrains.com/idea/jdbc-drivers/mysql-connector-java-5.1.35-bin.jar)

## 开启phpstorm调试模式

1. 开启phpdebug

		xdebug.profiler_output_dir="D:\phpStudy\tmp\xdebug"
		xdebug.trace_output_dir="D:\phpStudy\tmp\xdebug"
		zend_extension="D:\phpStudy\php\php-5.4.45\ext\php_xdebug.dll"   写自己的文件路径
		xdebug.remote_enable = On
		xdebug.remote_handler = dbgp
		xdebug.remote_host= localhost
		xdebug.remote_port = 9000
		xdebug.idekey = PHPSTORM
>查看phpinfo  是否存在debug
    
2. 下载chrome插件
		[点击跳转](https://chrome.google.com/webstore/detail/jetbrains-ide-support/hmhgeddbohgjknpmjagkdomcpobmllji)
        
3. [详细教程](https://segmentfault.com/a/1190000004175313)
设置->语言框架->php->debug->9000端口
		
4. 新建一个测试

    点击工具栏中的调试->编辑配置
    添加 php web Application
    右侧server中,添加本地域名,端口号
    start url 填写框架的入口文件或需要调试的文件
    
## compser

1. 安装compser
2. 设置phpstorm
安装路径大致为`C:\ProgramData\ComposerSetup\bin\composer.phar`
设置 `composer.json`路径

3. 验证
`composer -V`
4. 安装证书
[教程](http://www.ituring.com.cn/article/261281)
```
1) 删除extension_dir = "./"和extension_dir = "ext"前面的分号,消注释这两行代码，配置PHP插件目录为./ext。
2) 删除extension=php_openssl.dll前面的分号，取消注释，从而启用OpenSSL插件。
3) 下载证书
4) ;openssl.cafile= (若没有则创建) 
    openssl.cafile='D:\phpStudy\php\php-5.5.38\verify\cacert.pem'
```
5. 重启软件

 ## 其他技巧
### 生成随机字母
`lorem100 生成百个单词`


## 快捷键
|   `Shift+Ctrl+Alt+N` |  全局搜索类  |
| --- | --- |
| ` Alt+J`  |   选中相同代码 |
|  `Shift+Ctrl+Alt+J` |   一次全部选中 |
|  `Ctrl+Alt+T`   |   环绕生成 |
| ` F2`  |   导航错误位置 |
|  `Shift+F1`  |   查找外部文档 |
|  `'hello word'.log`  |  按 table 变为  console.log('helloword'); |
|  `CTRL+T ` |   翻译英文 |
|  `Alt+Shift+D` |   与剪切板对比 |
|  `Ctrl + Alt + ->` |   与剪切板对比 |
|`ctrl+shift+n`| 搜索文件位置|
| `ctrl+n`|    更多功能,如给属性添加Getters and Setters |
|`ctrl+shift+alt+n`| 快速打开指定的方法|

