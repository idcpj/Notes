
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


var DbConfig = map[string]interface{}{
	"Default": "mysql_dev",
	"SetMaxOpenConns": 300,
	"SetMaxIdleConns": 10,

	"Connections": map[string]map[string]string{
		"mysql_dev": {
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

	db := connection.GetInstance()
}
```



## 查
```
//对table 进行复制
user := db.Table("users")
```
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
### 其他查询
```
res, err := db.Table("users").Count()
min, err := db.Table("users").Min("age")
avg, err := db.Table("users").Avg("age")
sum, err := db.Table("users").Sum("age")

```
## 插入
### 插入一条
```
//方法一,初始化并赋值
data := map[string]interface{}{
    "name":"abc",
    "create_at":"1235454",
}
//方法二 初始化 后赋值
 //var data []map[string]interface{}
//data["name"]="ceswasd"
//data["create_at"]="1235454"


res, err := db.Table("user").Data(data).Insert()
if err != nil {
    panic(err)
}
//判断是否插入成功
if res > 0 {
    fmt.Printf("RowsAffected: %v \n", res)  //受影响行数
}

fmt.Printf("LastInsertId: %d", db.LastInsertId)  //返回受影响的id
fmt.Printf("SqlLogs: %v", db.SqlLogs)  //日志记录
```
## 更新
```
data := map[string]interface{}{
    "name":"update",
    "created_at":1324563,
}
where :=map[string]interface{}{
    "id":53,
}

res,err :=db.Table("user").Data(data).Where(where).Update()
if err !=nil{
    panic(err)
}

fmt.Println(res)
```
## 删除
```
where := map[string]interface{}{
    "id": 17,
}
res, err := db.Table("user").Where(where).Delete()
if err != nil {
    panic(err)
}
fmt.Println(res)//1

```

## 其他
### 多条件语句
```
where := [][]interface{}{
    {"id", ">", 1},
    {"name", "=", "salamander"},
}
res, err := db.Table("user").Where(where).Get()
if err != nil {
    panic(err)
}

fmt.Println(res)
```

### 处理事务
```
db.Transaction(func(){
    db.Table("user").Data(map[string]interface{}{"name":"fizz"}).Insert()
    db.Table("user").Data(map[string]interface{}{"name":"fizz2"}).Where("id",1).Update()
})
```
或
```
trans,err := db.Transaction(func() error {

    res2, err2 := db.Table("users").Data(data2).Insert()
    if err2 != nil {
        return err2
    }
    if res2 == 0 {
        return errors.New("Insert failed")
    }
    fmt.Println(res2)

    res1, err := db.Table("users").Data(data2).Where(where).Update()
    if err != nil {
        return err
    }
    if res1 == 0 {
        return errors.New("update failed")
    }
    fmt.Println(res1)

    return nil
    })

    fmt.Println(trans, err)
}
```