[TOC]
 
## 生成 模型
`bee generate model User -fields="user_id:string,user_login:string,user_name:string"`

## 优化生成的模型

### 如果主键不是int 可手动设置
`UserId      string `orm:"pk"`` 

并修改模型中对应的字段与类型
###  对单个添加索引
`UserLogin   string `orm:"index"``
### 对GetAllxxx 函数进行优化
把`query`的参数更改设置`query map[string]interface{}`
