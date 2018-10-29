[TOC]

> [参考已有项目] (https://www.jianshu.com/p/bff94aa90836)

## 安装 java
`choco install choco install jdk8`

## 安装 Android Development Tools Bundle
> [参考官网](https://developer.oculus.com/documentation/mobilesdk/0.6/concepts/mobile-dev-setup-android-win/)

[32-bit .zip download](https://dl.google.com/android/adt/adt-bundle-windows-x86-20140702.zip)
[64-bit .zip download](https://dl.google.com/android/adt/adt-bundle-windows-x86_64-20140702.zip)

设置环境变量
```
设置 %ANDROID_HOME %
ANDROID_HOME C:\Dev\Android\adt-bundle-windows-x86-20140702\sdk

设置 path
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\tools
```

## 安装 cordova
`npm install -g cordova`
## 创建项目
```
cordova create MyApp
cordova platform add browser  [ios,android,]
cordova run [ios,android]
```


## 错误解决
### `cordova run android` 出错
#### 缺少安装证书
 Before building your project, you need to accept the license agreements ...
```
mkdir "%ANDROID_HOME%\licenses"
echo |set /p="8933bad161af4178b1185d1a37fbf41ea5269c55" > "%ANDROID_HOME%\licenses\android-sdk-license"
```

### `cordova run window `出错
#### MSBuild v4.0 is not supported, aborting
添加环境变量：
```
VSINSTALLDIR = C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\
```