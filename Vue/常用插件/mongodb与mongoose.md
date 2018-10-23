[TOC]

## 安装
```
 npm install mongodb --save  
 npm install mongoose --save  
```
## 使用
在`models/base.js` 中
```
const mongoose = require("mongoose");
// 若是带账号密码的：'mongodb://root:123456@127.0.0.1:27017/dumall'
const connStr= "mongodb://127.0.0.1:27017/imoocsell";
mongoose.connect(connStr,{ useNewUrlParser: true });
mongoose.connection.on("connected",()=>{
    console.log("MongoDB connected success.")
});
mongoose.connection.on("error",()=>{
    console.log("MongoDB connected fail.")
});
mongoose.connection.on("disconnected",()=>{
    console.log("MongoDB connected disconnected.")
});
```
在 `models/goods.js` 中
```
require("./base")
const mongoose = require("mongoose");
let Schema = mongoose.Schema;


//定义一个shcema
const productSchema = new Schema({
    'productId':String,   // 或者 'productId':{type:String}
    'productName':String,
    'salePrice':Number,
    'productImage':String,

    // 在列表页点击“加入购物车时”，会获取对应goods商品数据，然后给该商品添加checked和productNum属性，再将该商品添加到购物车列表中，Schema中不定义属性的话是添加不了的。
    "checked":String,
    "productNum":Number
});


// 输出(导出)w
module.exports = mongoose.model('good',productSchema,); // 定义一个good商品模型，可以根据这个商品模型调用其API方法。

// 这个模型定义的是数据库dumall的goods集合数据，所以这个model取名good是对应这个集合，连接数据库之后，这个模型会根据名字的复数形式"goods"来查找数据集合。
// module.exports = mongoose.model('goods',productSchema,'goods'); //也可以后面注明链接的是数据库的goods集合
```
在 `router/goods.js` 中
```
const goods = require("../models/goods");

goodsModel = goods.find(params);
goodsModel.sort({salePrice:param.sort}).skip(skip).limit(param.pageSize);
goodsModel.exec((err,doc)=>{});
```

