[TOC]

## 安装
```
//xorm 工具
go get github.com/go-xorm/cmd/xorm
```
## 使用
### Reverse
把数据表转为go 结构体
```
cd $GOPATH/src/github.com/go-xorm/cmd/xorm

sqlite: xorm reverse sqite3 test.db templates/goxorm

mysql: xorm reverse mysql root:12345678@[ip:port]/xorm_test?charset=utf8 templates/goxorm

mymysql: xorm reverse mymysql xorm_test2/root/ templates/goxorm

postgres: xorm reverse postgres "dbname=xorm_test sslmode=disable" templates/goxorm

mssql: xorm reverse mssql "server=test;user id=testid;password=testpwd;database=testdb" templates/goxorm
```