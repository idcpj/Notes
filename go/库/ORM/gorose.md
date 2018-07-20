
[TOC]

> [github地址](https://github.com/gohouse/gorose/blob/master/examples/mysql.go)


## 起始配置
```
package main

//导入的包
import (
	"fmt"
	"github.com/gohouse/gorose"
	_ "github.com/go-sql-driver/mysql"

)

//配置
var DbConfig = map[string]interface{}{
	// Default database configuration
	"Default": "mysql_dev",
	// (Connection pool) Max open connections, default value 0 means unlimit.
	"SetMaxOpenConns": 300,
	// (Connection pool) Max idle connections, default value is 1.
	"SetMaxIdleConns": 10,

	// Define the database configuration character "mysql_dev".
	"Connections":map[string]map[string]string{
		"mysql_dev": map[string]string{
			"host":     "192.168.0.70",
			"username": "root",
			"password": "www.upsoft01.com",
			"port":     "3306",
			"database": "demo",
			"charset":  "utf8",
			"protocol": "tcp",
			"prefix":   "",      // Table prefix
			"driver":   "mysql", // Database driver(mysql,sqlite,postgres,oracle,mssql)
		},
	},
}

func main() {
	//连接
	connection, err := gorose.Open(DbConfig)
	if err != nil {
		fmt.Println(err)
		return
	}
	// 关闭 DB
	defer connection.Close()

```



## 查
### 原生语句查询
```
//直接查询
userInfo,err := db.Query("select * from user")
if err != nil{
    panic(err)
}

for _,v :=range userInfo{
    fmt.Println(v) //map[id:19 name:salamander created_at:1531993413]
}
```

### 快速查第一条
```
res ,err :=db.Table("user").Where("id = 50").First() //First  返回的是一维数组
if err!=nil {
    panic(err)
}

fmt.Println(res) //[map[id:50 name:salamander1 created_at:1531993414]]
```
###  get 函数返回多维数组
```
res ,err :=db.Table("user").Where("id = 50").Get() //get  返回的是多维数组
if err!=nil {
    panic(err)
}

fmt.Println(res) //map[id:50 name:salamander1 created_at:1531993414]
```
### 返回json值
```
result,err := db.Table("user").Get()
if err !=nil {
    panic(err)
}
fmt.Print(db.JsonEncode(result)) //返回多维数组的json
```

### 大量数据 分块处理
```
db.Table("user").Fields("name ").Where("id > 49").Chunk(100, func(data []map[string]interface{}) {
    for _,item :=range data{
        fmt.Println(item["name"])
    }
})
```


## 处理事务
```
db.Transaction(func(){
    db.Table("user").Data(map[string]interface{}{"name":"fizz"}).Insert()
    db.Table("user").Data(map[string]interface{}{"name":"fizz2"}).Where("id",1).Update()
})
```