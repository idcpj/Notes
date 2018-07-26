
[TOC]


> [官方文档](https://beego.me/docs/quickstart/)
> [github]()


## init 函数
beego 在运行时候会先加载,涉及到的所有 所有 `.go`文件中的init
可用于初始化 mysql,redis 等操作

## model 操作
```
type HsDept struct {
	DEPT_ROOT_ID   string `orm:"pk"`
}

orm.RegisterDriver("mysql", orm.DRMySQL)

orm.RegisterDataBase("default", "mysql", "root:www.upsoft01.com@tcp(192.168.0.71:3306)/antdbms_test2?charset=utf8", 60)

//需要添加这一步才能查找对应的数据表,不然会报错,找不到改表
orm.RegisterModel(new(HsDept))

```