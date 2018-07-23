
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
func main() {
    ch4 := make(chan int, 1)
	for i := 0; i < 4; i++ {
		select {
		case e, ok := <-ch4:
			if !ok {
				fmt.Println("End.")
				return
			}
			fmt.Println(e)
			close(ch4)    

		default:
			fmt.Println("No Data!")
			ch4<-1
		}
	}
}

/*输出
No Data!
1
End.
*/
```



## range 用法
```
nums := []int{2, 3, 4}
for k, v:= range nums {
    //code k=0,1,2,v=2,3,4
}
```