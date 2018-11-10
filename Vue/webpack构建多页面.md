[TOC]


> [在github 参考源码](https://github.com/idcpj/vue-mall/tree/master/webpack_demo)

## 目录结构
```
src
├── cart.html
├── index.html
└── js
    ├── cart.js
    ├── common.js
    └── index.js
```
## 运行
```
npm init
npm install webpack --save-dev
```    
## 安装常用插件
### 编译 html
[html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin)
```
new HtmlWebpackPlugin({
    filename:"cart.html",
    template:"./src/cart.html",
    chunks:['cart'],
    minify:{   //压缩 html 代码
        removeComments:true,
        collapseWhitespace:true
    }
}),
```
### 编译前先删除文件
[clean-webpack-plugin](https://github.com/johnagan/clean-webpack-plugin)
```
new CleanWebpackPlugin(['./dist'],{
    root:path.join(__dirname,''),
    verbose:true,
    dry:false,
}),
```
###  css-loader,style-loader
```
npm install --save-dev css-loader style-loader extract-text-webpack-plugin

//需要在页面的 js 中引入 css ,如  index.js
import "../css/index.css";

//webpack.config.js
module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
```
### es6
```
npm install -D babel-loader @babel/core @babel/preset-env

//webpack.config.js
rules: [
    {
      test: /\.m?js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    }
  ]
```
### 使用 jquery
[npm 官网](https://www.npmjs.com/package/jquery)
```
npm i jquery

//index.js
define(["jquery"], function($) {
    //code
});
```
### uglifyjs-webpack-plugin js 压缩
[npm 官网](https://www.npmjs.com/package/webpack-parallel-uglify-plugin)
```
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
 
module.exports = {
  //...
  optimization: {
    minimizer: [new UglifyJsPlugin()]
  }
};
```

## 技巧
###  js 最好以模块形式引入
如
```
//common.js
define("common",function () {
    return {
        initIndex:function () {
            console.log("common init index");
        },
        initCart:function () {
            console.log("common init cart");
        }
    }
});

//index.js
require(['./common.js'],function (common) {
    common.initIndex();
});
```
### webpack.config.js 设置
```
entry: {
    index:"./src/js/index.js", //设置多入口
    cart:'./src/js/cart.js',
},
devtool:"#source-map" //用于调试
```