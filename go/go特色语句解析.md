
[TOC]

##  创建不分类型的数组和 map
```
//interface 可创任意类型的数组
a :=[]interface{}{"a",1,"b"}
fmt.Print(a[0])//a

//interface 可创任意类型的map
b :=map[interface{}]interface{}{"asd":132,123:"asasd"}
fmt.Print(b[123]) //asasd
```


## 用 switch 判断类型
```
var a  interface{}
a=3
switch a.(type) {
case int:
    fmt.Print("int ")
    break
case string:
    fmt.Print("string")
    break
default:
    fmt.Print("not kome")
}
```

## 结构体与指针用法
```
type Books struct {
    title string
    author string
    subject string
    book_id int
}

var book Books

/* book 1 描述 */
book.title = "Go 语言"
book.author = "www.runoob.com"
book.subject = "Go 语言教程"
book.book_id = 6495407
```

## select 用法
```
ch4 := make(chan int, 1)
for i := 0; i < 4; i++ {
    select {
    case e, ok := <-ch4:
        if !ok {
            fmt.Println("End.")
            return
        }
        fmt.Println(e)
        close(ch4)    //关闭 channel

    default:
        fmt.Println("No Data!")
        ch4<-1
    }
}

/*输出
No Data!
1
End.
*/
```



## var 与 new 区别
```go
p := new(person)
err := xml.Unmarshal(str, p)
```
同
```go
var p person
err := xml.Unmarshal(str, &p)
```
> 对于new 相当于分配引用类型的内存地址,并且赋值,而 var 只分配内存,没有赋值

```
var c *int
*c = 10
fmt.Println(*c)  //会报错

/*====*/

b := new(int)
*b = 10
fmt.Println(*b)  //10 
```
## new 与 make 的区别
`make` 只创建 `chan`、`map`以及切片的内存创建
