[TOC]

> [官网手册](https://webpack.docschina.org/concepts/)

## 安装
```
npm install -g webpack
npm install -g webpack-cli
```

## 初始化
```bash
> npm init
> npm install -D webpack    #-D 等价于 --save-dev
> npm install -D webpack-cli
> mkdir src && cd src
> touch index.js
> webpack --mode development
```
### 需要处理 css 的 引入
安装 `css-loader`
`> npm install -D css-loader`

## webpack.config.js 设置
> [更多配置查看官网](https://webpack.js.org/concepts/#entry)
```js
const path= require('path');
const true_path = path.resolve(__dirname, './');

module.exports={
    entry:'./src/script/main.js', //需要打包的 js 入口文件 ,注意多入口的输出 可使用 [name]-[hash].js
    output:{
        path: true_path+ '/dist', //1. 必须为绝对路径, 2. 通过 path 对象中的函数,实现把相对路径变为绝对路径
        filename:"js/[name]-[hash].js",
        publicPath:"http://demo.com"  //引入 js 等资源前加入域名
    }
}
```
### 引入 `html-webpack-plugin`  插件
> [插件手册(github)](https://github.com/jantimon/html-webpack-plugin#)
```
const HtmlWebpackPlugin = require('html-webpack-plugin'); 

module.exports = {
    plugins:[
        new HtmlWebpackPlugin({
            template: './src/index.html',
            minify:{
                removeComments:true,// 删除注释
                collapseWhitespace:true,// 删除空格
            }
        }),
    ]
}
```




### 通过 `<%= %>` 传值
1. 传递插件中的值
```js
new HtmlWebpackPlugin({
    template: './src/index.html',
    title:"this is a title"
}),
```
```html
<title><%= htmlWebpackPlugin.options.title %></title>
```
2. 设置 js 引入的位置
需要 配置`HtmlWebpackPlugin` 中 `inject:false`,默认为生成在 body 尾部
```js
//webpack.config.js
entry: {
    main:'./src/script/main.js',
    a:'./src/script/a.js',
},
```
```js
//设置 main.js 的位置 如在 title 中
<script type="text/javascript" src="<%= htmlWebpackPlugin.files.chunks.main.entry %>"></script>

//在 body 中
<script type="text/javascript" src="<%= htmlWebpackPlugin.files.chunks.a.entry %>"></script>
```




## pack.json 配置
```
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start-dev":"webpack --mode development  --proress "
  },
```
`  > npm run start-dev  即可运行`
