[TOC]

## 安装
### mac

#### 安装
**配置文件默认在 /usr/local/etc 下的 mongod.conf**
```
sudo brew install mongodb
```
#### 启动
```
//启动 mongod 服务
mongod --config=/usr/local/etc/mongod.conf
--数据库位置  /usr/local/var/mongodb
--日志位置 /usr/local/var/log/mongodb/mongo.log

//启动 shell
mongo
```

## mongoDB用户认证
[简书参考](https://www.jianshu.com/p/3b1134e7b12b)

## 数据库操作
### 创建数据库
`use test`
### 创建集合
```
use test
db.goods
```
### 删除数据库
```
use test
db.dropDatabase()
```
### 删除集合
```
use test
db.集合名.drop()
```
## 查询

###  复杂查询
```
let params = {
    salePrice: {
        $gt: priceGt,  //gt 大于
        $lte: priceLte,  //lte 小于等于
    }
};
goodsModel = goods.find(params);
goodsModel.sort({salePrice:param.sort}).skip(0).limit(10);
goodsModel.exec((err,doc)=>{
    //todo
});
```