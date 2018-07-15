
[TOC]

##  创建不非类型的数组和 map
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
//创建结构体
type MyInt struct {
    n int
}
//添加方法
func (myInt *MyInt) Increase() {
	myInt.n++
}

func (myInt *MyInt) Decrease() {
	myInt.n--
}

func main() {
	mi := MyInt{}
	mi.Increase()
	mi.Increase()
	mi.Decrease()
	mi.Decrease()
	mi.Increase()
	fmt.Print(mi.n) //1
}
```

# select 用法
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

## 异常处理
```
parentPath, err := os.Getwd()
if err != nil {
    return nil, err
}
//todo
```
