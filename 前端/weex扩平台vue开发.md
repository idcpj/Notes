[TOC]

> [官方文档](https://weex.apache.org/cn/guide/)

## 调试工具
`weexplayground` 在需要调试的平台上安装

## 安装
`npm install -g weex-toolkit`

## 初始化项目
```
weex init projectName
npm install

//同时开启 
npm run dev 与 npm run serve
```

## 注意事项

### 适配和缩略
1. Weex对于长度值目前只支持像素值,不支持相对单位(em、rem);适配以750pX标准。
2. 设定边框, border目前不支持类似这样 border:1 px solid #f10000的组合写法。
3. 设定背景色, background目前不支持类似这样 background:red 的写法,需要修改为具体的 background- color:red。