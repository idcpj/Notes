[TOC]


##  安装配置
### 类linux 配置 go
有4个环境变量需要设置: GOROOT、 GOPATH、 GOBIN,以及PATH
需要设置到某一个 profile文件中(~/bash_ profile或/etc/ profile)
```
export GOROOT=/usr/local/go  //该环境变量的值应该为Go语言的当前安装目录
export GOPATH=-/golib: /goproject  //该环境变量的值应该为Go语言的工作区的集合
export GOBIN=-/gobin  //它的值应该是你想存放Go程序的可执行文件的目录
export PATH=$PATH: SGOROOT/bin: SGOBIN  //为了方便使用Go语言命令和Go程序的可执行文件,需要追加其值
```
添加到对应的`profile` 配置文件中
eg:
`source .zshrc` 或`source .bashrc`
## mac
1. 安装
`brew install go`
2. 如何 goland 无法调试
`https://developer.apple.com/download/more/` 
下载 `Command Line tools(macoS 10.13) for Xcode 9.1`

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
###  `_`(下划线) 用法,初始化 `init` 函数
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

### 变量可见性规则
1. 大写字母开头的变量是可导出的,也就是其它包可以读取的,是公用变量
2. 小写字母开头的就是不可导出的,是私有变量。


## 类型别名
类型别名不能进行计算
```
type a int16  //定义 a 为 int16 
func main() {
	 var abc a  //定义 abc 为 a 类型
	 fmt.Print(unsafe.Sizeof(abc)) //2 
}
```
## 打印结构类型或自动打印类型
使用** `%v`**
```
a := [][]int{
    {1,2,3},
    {1,2,3},
}
fmt.Printf("%v",a) //[[1 2 3] [1 2 3]]

//识别 字符串和整形
b :=1
c :="a"
fmt.Printf("%v",b) 
fmt.Printf("%v",c)
```


## 常用命令
1. `go build` : 用于编译源码文件、代码包、依赖包
2. `go run` : 可以编译并运行Go源码文件
```
a :  强制编译相关代码,不论它们的编译结果是否已是最新的
n :  打印编译过程中所需运行的命令,但不真正执行它们
p n: 并行编译,其中n为并行的数量,为cpu 核数
```
4. `go get` : 命令主要是用来动态获取远程代码包的
eg: `go get http://xxxxx/test.go`
注意: `go get` 下载的文件是放在 `GOPATH`中
可通过 `go env | grep GOPATH ` 查看
可在`goLand`中设置全局和项目的的 `GOPATH`
```
-d : 只执行下载动作,而不执行安装动作
-fix : 在下载代码包后先执行修正动作,而后再进行编译和安装
-u : 利用网络来更新已有的代码包及其依赖包
```


## go get 如何下载太慢
1. 先通过 `go get github.com/go-sql-driver/mysql` 生成目录即可
2. 在目录下 使用`git clone https://github.com/go-sql-driver/mysql` 下载代码,注意,此时,目录为需上移动
3. 在自己项目中 直接`import` 路径即可