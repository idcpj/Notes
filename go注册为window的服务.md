
[TOC]


##  使用go 注册
```
package main

import (
	_ "antbiz/routers"
	"log"

	_ "antbiz/lib" 

	"os"

	"github.com/astaxie/beego"
	"github.com/astaxie/beego/orm"
	"github.com/kardianos/service"
)

type program struct{}

func (p *program) Start(s service.Service) error {
	log.Println("开始服务")
	go p.run()
	return nil
}
func (p *program) Stop(s service.Service) error {
	log.Println("停止服务")
	return nil
}
func (p *program) run() {
	// 这里放置程序要执行的代码……

	//是否开启debug
	orm.Debug = false

	beego.Run()
}

func main() {
	//服务的配置信息
	cfg := &service.Config{
		Name:        "UpAntBiz",
		DisplayName: "UpAntBiz",
		Description: "UpAntBiz",
	}
	// Interface 接口
	prg := &program{}
	// 构建服务对象
	s, err := service.New(prg, cfg)
	if err != nil {
		log.Fatal(err)
	}
	// logger 用于记录系统日志
	logger, err := s.Logger(nil)
	if err != nil {
		log.Fatal(err)
	}
	if len(os.Args) == 2 { //如果有命令则执行
		err = service.Control(s, os.Args[1])
		if err != nil {
			log.Fatal(err)
		}
	} else { //否则说明是方法启动了
		err = s.Run()
		if err != nil {
			logger.Error(err)
		}
	}
	if err != nil {
		logger.Error(err)
	}
}

```
运行
```
> go build main.go
> main.exe [install| stop | start] 

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