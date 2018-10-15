[TOC]
[mongoose 官网](https://mongoosejs.com/docs/validation.html)
## 安装
`npm i -S mongoose`

## demo使用
在`model/goods.js`中
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

// 输出(导出)w
module.exports = mongoose.model('good',productSchema); ```
```
`routers/goods.js`
```
const express = require("express");
const router = express.Router();
const mongoose = require("mongoose");
const goods = require("../models/goods");

const connStr= "mongodb://127.0.0.1:27017/imoocsell";

// 若是带账号密码的：'mongodb://root:123456@127.0.0.1:27017/dumall'
mongoose.connect(connStr);

mongoose.connection.on("connected",()=>{
    console.log("MongoDB connected success.")
});

mongoose.connection.on("error",()=>{
    console.log("MongoDB connected fail.")
});

mongoose.connection.on("disconnected",()=>{
    console.log("MongoDB connected disconnected.")
});

router.get("/list",(req,res,err)=>{
    goods.find({},(err,doc)=>{
        if(err){
            res.json({
                status:1,
                msg:err.message
            })
        }else{
            res.json({
                status:0,
                msg:"",
                result:doc
            })
        }

        res.end();
    })

});

module.exports=router;
```
## 