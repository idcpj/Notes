[TOC]

> [快速入门](https://weex.apache.org/cn/guide/)
> [手册](https://weex.apache.org/cn/references/)
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

//开启 debug
weex debug

```

## 注意事项

### 适配和缩略
1. Weex对于长度值目前只支持像素值,不支持相对单位(em、rem);适配以750pX标准。
2. 设定边框, border目前不支持类似这样 border:1 px solid #f10000的组合写法。
3. 设定背景色, background目前不支持类似这样 background:red 的写法,需要修改为具体的 background- color:red。
### 定位
1. wex支持 position定位 relative| absolute| fixed sticky,默认值 为 relative。
2. weex目前不支持 z-index设置元素层级关系,但靠后的元素层级更高,因此,对于层级高的元素,可将其排列在后面。
3. 如果定位元素超过容器边界,在 Android下,超出部分将不可见,原因在于 Android端元素 overflow默认值为 hidden
### 其余需要注意的地方
1. wex支持线性渐变 linear- gradient不支持 radial- gradient径向渐变。
2. weex中box- shadow仅仅支持ios。
3. 目前< image>组件无法定义一个或几个角的 border-radius,只对ios有效,对 Android无效
4. weex中, flexbox是默认并且唯一的布局模型,每个元素都默认拥有了 `display:fex`属性。

