[TOC]
[mongoose 官网](https://mongoosejs.com/docs/validation.html)
[简书参考](https://www.jianshu.com/p/9b20c1e2f373)
## 安装
`npm i -S mongoose`

## demo使用
在`model/base.js `中
连接数据库
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

在`model/goods.js`中
创建 映射关系
```
const mongoose = require("mongoose");
let Schema = mongoose.Schema;

//定义一个shcema
var productSchema = new Schema({
    'productId':String,   // 或者 'productId':{type:String}
    'productName':String,
    'salePrice':Number,
    'productImage':String,
});

// 输出(导出)
module.exports = mongoose.model('good',productSchema,"goods");//第三参数对应表名 
```

在 `routers/goods.js` 中
```
const goods = require("../models/goods");

//复杂条件查询
params.salePrice={
    $gt: priceGt,
    $lte: priceLte,
}
goodsModel = goods.find(params);
goodsModel.sort({salePrice:param.sort}).skip(skip).limit(param.pageSize);
goodsModel.exec((err,doc)=>{}

//单条查询
User.findOne({userName:userName},(err1,userDoc)=>{
    //保存
    userDoc.userName="ccc";
    userDoc.save((err4,doc3)=>{})
}
//删除用户下购物车中的某个物品
 userModel.update({userId: userId}, 
                {$pull: {cartList: 
                            {productId: productId}
                        }
                }, (err, doc) => {})

//更新 购物车下的某个物品数量
userModel.update({
userId:userId,"cartList.productId":productId},
{"cartList.$.productNum":productNum},(err,doc)=>{});
```
## 