[TOC]

## 安装
`npm install cookie-parser`

## 引用
```
var express      = require('express')
var cookieParser = require('cookie-parser')
 
var app = express()
app.use(cookieParser())
```
## 获取 cookie 
```
app.get('/', function(req, res) {
  console.log('Cookies: ', req.cookies)
})
```
## 设置 cookie 与 session
```
//保存 cookie
res.cookie("userId",doc.userId,{
    path:"/",
    maxAge:1000*60*60//一小时
});
//保存 session
req.session.user=doc.user;
 
```
