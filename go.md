[TOC]

> [git快速入门指南](https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/01.0.md)

##  安装配置
### 类linux 配置 go
有4个环境变量需要设置: GOROOT、 GOPATH、 GOBIN,以及PATH
需要设置到某一个 profile文件中(`~/bash_ profile`或`/etc/ profile`)
```
export GOROOT=/usr/local/go
export GOBIN=$GOROOT/bin
export PATH=$PATH:$GOBIN
export GOPATH=/var/opt/wwwroot/goblin
```
添加到对应的`profile` 配置文件中
eg:
`source .zshrc` 或`source .bashrc`
### mac
1. 安装
`brew install go`
2. 如果 goland 编辑器 无法调试
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
## 工作目录最好是在src 中创建项目
这样自定义包可以编辑器可以识别并导入

## package 包说明
1. 在同一个目录只能由一个` main `包,即开头为`package main`,不然编译会报错
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

func init() {
	fmt.Print("my name is show2")
}

func Show2(){} 
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


## 常用命令
1. `go build` : 用于编译源码文件、代码包、依赖包
2. `go run` : 可以编译并运行Go源码文件
```
a :  强制编译相关代码,不论它们的编译结果是否已是最新的
n :  打印编译过程中所需运行的命令,但不真正执行它们
p n: 并行编译,其中n为并行的数量,为cpu 核数
```
4. `go get -v` : 命令主要是用来动态获取远程代码包的
eg: `go get -v http://xxxxx/test.go`
注意: `go get` 下载的文件是放在 `GOPATH`中
可通过 `go env | grep GOPATH ` 查看
可在`goLand`中设置全局和项目的的 `GOPATH`
```
-d : 只执行下载动作,而不执行安装动作
-fix : 在下载代码包后先执行修正动作,而后再进行编译和安装
-u : 利用网络来更新已有的代码包及其依赖包
```
5. `go install ./模块名`
可编译出一个存在 src同级的 bin 目录下的执行命令
## 初始化模块的函数 `init`

如某个目录下有 多个`*.go` 文件,
在引入`xxx/model` 时
每个文件的 `func init()` 都会执行

## go get 如何下载太慢
1. 先通过 `go get github.com/go-sql-driver/mysql` 生成目录即可
2. 在目录下 使用`git clone https://github.com/go-sql-driver/mysql` 下载代码,注意,此时,目录为需上移动
2.5 如果有些需要执行命令 如`goimports`,则`go install golang.org/x/tools/cmd/goimports
`
3. 在自己项目中 直接`import` 路径即可

## 程序从后台运行，不出现dos窗口
`go build -ldflags "-H windowsgui`
文件为当前目录对应的文件

## 在不同平台编译指定文件
Mac 下编译 Linux 和 Windows 64位可执行程序
```
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```
Linux 下编译 Mac 和 Windows 64位可执行程序
```
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

Windows 下编译 Mac 和 Linux 64位可执行程序
```
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go

SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```

```
GOOS：目标平台的操作系统（darwin、freebsd、linux、windows） 
GOARCH：目标平台的体系架构（386、amd64、arm） 
```
## 自动编译linux 和window 的多个文件
```
SET GOOS=linux
go build antbiz.go
cd proxy
go build antzoo.go
cd ../

SET GOOS=windows
go build antbiz.go
cd proxy
go build antzoo.go
cd ../
```

## 要有全局概念
即在启动程序中只启动一次 ,在使用框架时候尤其如何.某些全局的配置,可以在main 函数中进行设置
以beego为例
```
import (
	_ "antbiz/routers"

	_ "antbiz/lib" //  main函数中 初始化

	"github.com/astaxie/beego"
	"github.com/astaxie/beego/orm"
)

func main() {
	//是否开启debug
	orm.Debug = false

	beego.Run()

}
```

在 `lib/cache`
```
var Bm cache.Cache

func init() {
	var err error
	Bm, err = cache.NewCache("memory", `{"interval":60}`)
	if err != nil {
		beego.Debug("缓存加载失败")
	}
}
```
这样 在全局中就可以使用 Bm这个函数了
