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
## 技巧
### res.end() 用法
如果是在回调函数内部,则`res.end()`也必须写在回调函数中

### 一级路由 在 `app.js ` 中的位置
```
app.use(cookieParser());

//配置路由
app.use('/', indexRouter);
const indexRouter = require('./routes/index');

// catch 404 and forward to error handler
app.use(function(req, res, next) {
    next(createError(404));
});

```




