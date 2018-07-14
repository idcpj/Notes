[TOC]
##  import 用法
### 设置别名
```
import (
	abc "fmt"
)
```
### 直接调用(不推荐)
```
import (
	. "fmt"  //添加点
)
func main() {
	Print("hello word")
}
```
###  `_` 用法,初始化 `init` 函数
```
import (
	_ "./show2"  //只调用 show2包的 init() 函数 包中的其他方法不可调用
)
```

## package 包说明
1. 在同一个目录只能由一个` main `包,即开头为`package main`
2. `package` 的包名 最好与目录名相同 eg: test 目录下则包名为`package test`
### 如何导入自定义包
```
├── learn1
│   └── learn1.go
├── show2
│   └── show2.go
└── main.go
```
`show2.go` 中内容
```
package show2

import "fmt"

func init() {//调用包时,会进行初始化
	fmt.Print("my name is show2")
}

func Show2(){} ///要与目录名保持一直,且首字母大写
```
导入 包
```
import (
	"./show2"  //可使用相对路径
)

//main(函数
func main() {
	show2.Show2()
}
```

## 类型别名
类型别名不能进行计算
```
type a int16  //定义 a 为 int16 
func main() {
	 var abc a  //定义 abc 为 a 类型
	 fmt.Print(unsafe.Sizeof(abc)) //2 
}

```

## 常用命令
1. `go build` : 用于编译源码文件、代码包、依赖包
2. `go run` : 可以编译并运行Go源码文件
3. `go get` : 命令主要是用来动态获取远程代码包的
eg: `go get http://xxxxx/test.go`
注意: `go get` 下载的文件是放在 `GOPATH`中
可通过 `go env | grep GOPATH ` 查看
可在`goLand`中设置全局和项目的的 `GOPATH`
