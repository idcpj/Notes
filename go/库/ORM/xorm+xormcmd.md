[TOC]

> [github](https://github.com/go-xorm/xorm/)
> [github 中文教程](https://github.com/go-xorm/manual-zh-CN)

##  安装 xorm
```
//xorm
go get -u github.com/go-xorm/xorm
```
## 常用配置
```
engine.ShowSQL(true)   //在控制台打印日志 
engine.SetMaxIdleConns() //设置连接池的空闲数大小
engine.SetMaxOpenConns() //设置最大打开连接数
```
## 创建 Engine Group 引擎 实现读写分离
> [跳转到教程](https://github.com/go-xorm/manual-zh-CN/blob/master/chapter-01/2.engine_group.md)
```
conns := []string{
		"postgres://postgres:root@localhost:5432/test?sslmode=disable;", // 第一个默认是master
		"postgres://postgres:root@localhost:5432/test1?sslmode=disable;", // 第二个开始都是slave
		"postgres://postgres:root@localhost:5432/test2?sslmode=disable",
}

var err error eg, err = xorm.NewEngineGroup("postgres", conns)
```

##  tag 映射规则
|tag|规则|
|---|---|
|name	|当前field对应的字段的名称，可选，如不写，则自动根据field名字和转换规则命名，如与其它关键字冲突，请使用单引号括起来。|
|pk	|是否是Primary Key，如果在一个struct中有多个字段都使用了此标记，则这多个字段构成了复合主键，单主键当前支持int32,int,int64,uint32,uint,uint64,string这7种Go的数据类型，复合主键支持这7种Go的数据类型的组合。|
|当前支持30多种字段类型|，详情参见本文最后一个表格	字段类型|
|autoincr	|是否是自增|
|[not ]null 或 notnull	|是否可以为空|
|unique或unique|(uniquename)	是否是唯一，如不加括号则该字段不允许重复；如加上括号，则括号中为联合唯一索引的名字，此时如果有另外一个或多个字段和本unique的uniquename相同，则这些uniquename相同的字段组成联合唯一索引|
|index或index|(indexname)	是否是索引，如不加括号则该字段自身为索引，如加上括号，则括号中为联合索引的名字，此时如果有另外一个或多个字段和本index的indexname相同，则这些indexname相同的字段组成联合索引|
|extends	|应用于一个匿名成员结构体或者非匿名成员结构体之上，表示此结构体的所有成员也映射到数据库中，extends可加载无限级|
|-	|这个Field将不进行字段映射|
|->	|这个Field将只写入到数据库而不从数据库读取|
|<-	|这个Field将只从数据库读取，而不写入到数据库|
|created	|这个Field将在Insert时自动赋值为当前时间|
|updated	|这个Field将在Insert或Update时自动赋值为当前时间|
|deleted	|这个Field将在Delete时设置为当前时间，并且当前记录不删除|
|version	|这个Field将会在insert时默认为1，每次更新自动加1|
|default |0或default(0)	设置默认值，紧跟的内容如果是Varchar等需要加上单引号|
|json	|表示内容将先转成Json格式，然后存储到数据库中，数据库中的字段类型可以为Text或者二进制|

## 表操作
```
IsTableEmpty() //判断表是否为空，参数和CreateTables相同
IsTableExist()  //判断表是否存在
DropTables()  //删除表
```
## 前缀映射
```
tbMapper := core.NewPrefixMapper(core.SnakeMapper{}, "prefix_")
engine.SetTableMapper(tbMapper)
```