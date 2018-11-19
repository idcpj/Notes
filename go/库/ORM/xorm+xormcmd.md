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