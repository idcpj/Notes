[TOC]

## 安装 express 生成器
`npm i -g express-generator`

## 初始化项目
```
express server
cd server
npm i
```

## 前端引擎
默认为 jade
切换为 html
```
npm i ejs --save

//在app.js 中

var ejs = require("ejs");
app.set('view engine', 'html');  
app.engine('.html',ejs.__express)
```
