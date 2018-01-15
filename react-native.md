## [TOC]

---

 1. 官方文档
[开发文档](http://reactnative.cn/docs/0.50/getting-started.html#content)
2. 推荐可视化 react-natice 工具 [DECO](https://www.decoide.org/)
## 安装

参考文档 [搭建开发环境](http://reactnative.cn/docs/0.50/getting-started.html#content)

如果自动下载`gradle-2.14.1-all.zip`[下载](http://services.gradle.org/distributions/gradle-2.14.1-all.zip)失败,请手动
文件安装位置
`C:\Users\cc\.gradle\wrapper\dists\gradle-2.14.1-all\8bnwg5hd3w55iofp58khbp6yv`
mac 安装位置
`/Users/idcpj/.gradle/wrapper/dists/gradle-2.14.1-all/8bnwg5hd3w55iofp58khbp6yv/`

## MAC 准备工作

启动Xcode，并在Xcode | Preferences | Locations菜单中检查一下是否装有某个版本的Command Line Tools

Mac 的ios虚拟机 使用`commamd + d` 打开调试界面
1. 运行方式一
	直接输入 `react-native run-ios`
2. 运行方式二
	用xcode 打开项目中的`.xcodeproj`文件,点击运行

## android 准备工作

在命令行中启动虚拟机
`emulator -avd a7`  -a7 为虚拟机名
1. 运行方式一
	直接输入 `react-native android-ios`
2. 运行方式二
	用android Studio 打开项目的`android`文件,运行


## 测试技巧

安装phpstorm 插件  搜索 **react**  
虚拟机双击`r`可刷新状态

## 技巧
1. 摇一摇手机,打开`enable Live Reload`
