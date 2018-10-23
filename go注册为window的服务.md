
[TOC]


##  使用go 注册
```
package main

import (
	"fmt"
	"log"
	"net/http"

	"os"

	"github.com/kardianos/service"
)

var serviceConfig = &service.Config{
	Name:        "go_serviceName1",
	DisplayName: "go_service Display Name",
	Description: "go_service description",
}

func main() {

	// 构建服务对象
	prog := &Program{}
	s, err := service.New(prog, serviceConfig)
	if err != nil {
		log.Fatal(err)
	}

	// 用于记录系统日志
	logger, err := s.Logger(nil)
	if err != nil {
		log.Fatal(err)
	}

	if len(os.Args) < 2 {
		err = s.Run()
		if err != nil {
			logger.Error(err)
		}
		return
	}

	//方法 一.
	//cmd := os.Args[1]
	//if cmd == "install" {
	//	err = s.Install()
	//	if err != nil {
	//		log.Fatal(err)
	//	}
	//	fmt.Println("安装成功")
	//}
	//if cmd == "uninstall" {
	//	err = s.Uninstall()
	//	if err != nil {
	//		log.Fatal(err)
	//	}
	//	fmt.Println("卸载成功")
	//}

	////方法 一. install, uninstall, start, stop
	cmd := os.Args[1]
	if cmd == "help" {
		fmt.Println("可以使用的命令有 [install | uninstall | start | stop]")
		return
	}

	err = service.Control(s, cmd)
	if err != nil {
		log.Fatal(err)
	} else {
		fmt.Println(cmd, " 成功")
	}
}

type Program struct{}

func (p *Program) Start(s service.Service) error {
	log.Println("开始服务")
	go p.run() //调用run 方法
	return nil
}

func (p *Program) Stop(s service.Service) error {
	log.Println("停止服务")
	return nil
}

func (p *Program) run() {
	// 此处编写具体的服务代码
	startHttp()
}

//============为测试功能代码 创建一个9090的web服务 start=======  
func sayhelloName(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello astaxie!") //这个写入到w的是输出到客户端的
}

func startHttp() {
	http.HandleFunc("/", sayhelloName)       //设置访问的路由
	err := http.ListenAndServe(":9090", nil) //设置监听的端口
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}
//============为测试功能代码 end=======

```
运行
```
> go build main.go
> main.exe install    //[install | uninstall | stop | start]

```

## 使用命令注册
### 添加服务
```
描述:
        在注册表和服务数据库中创建服务项。
用法:
        sc <server> create [service name] [binPath= ] <option1> <option2>...

选项:
注意: 选项名称包括等号。
      等号和值之间需要一个空格。
 type= <own|share|interact|kernel|filesys|rec|userown|usershare>
       (默认 = own)
 start= <boot|system|auto|demand|disabled|delayed-auto>
       (默认 = demand)
 error= <normal|severe|critical|ignore>
       (默认 = normal)
 binPath= <.exe 文件的 BinaryPathName>
 group= <LoadOrderGroup>
 tag= <yes|no>
 depend= <依存关系(以 / (斜杠)分隔)>
 obj= <AccountName|ObjectName>
       (默认= LocalSystem)
 DisplayName= <显示名称>
 password= <密码>
 ```
 eg:
```
sc create go_server binPath= "D:\go\api\src\demo\demo.exe” type= share start= auto
```
### 删除服务
 第三参数为服务名,
 通过`服务->属性->服务名称`  并非显示名称
`sc delete godemo.exe` 

### widow 编译为不显示 dos 界面
`go build -ldflags "-H windowsgui"`

### nssm 安装go 编译的 exe
[下载](https://nssm.cc/download)
`nssm install`