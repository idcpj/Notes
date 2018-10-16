
[TOC]


> [官方文档](https://beego.me/docs/quickstart/)
> [github]()

## 常用命令
```
go get github.com/beego/bee    //获取beego
bee [new/api ] apiproject      //新建web 项目或api 项目
bee run                        //运行项目
bee pack                //打包项目
bee generate model [modelname] [-fields="name:type"]
bee generate controller [controllerfile]
```

## init 函数
beego 在运行时候会先加载,涉及到的所有 所有 `.go`文件中的init
可用于初始化 mysql,redis 等操作



## 对接口进行 `gzip` 压缩
 创建基础控制器  并处理 gzip逻辑
 ```
 package controllers

import (
	"bytes"
	"compress/gzip"

	"github.com/astaxie/beego"
)

/**
基础控制器
*/
type BaseController struct {
	beego.Controller
}

/*
对数据进行压缩
*/
func (this *BaseController) HandleGzip(json string) {
	var b bytes.Buffer
	w := gzip.NewWriter(&b)
    //设置压缩级别
    //w, e := gzip.NewWriterLevel(&b, 1)
    
	defer w.Close()
	w.Write([]byte(json))
	w.Flush()

	this.Ctx.Output.Header("Content-Type", "text/html; charset=utf8")
	this.Ctx.Output.Header("Content-Encoding", "gzip")
	this.Ctx.WriteString(b.String())
}
```
## linux 后台启动并不输出内容
`nohup ./beepkg  > /dev/null 2>&1 &`

## 前置后置操作

```
var FilterUser = func(ctx *context.Context) {
	beego.Debug("BeforeRouter")
}
/**
BeforeStatic
BeforeRouter
BeforeExec
AfterExec
FinishRouter
*/
beego.InsertFilter("/*", beego.BeforeRouter, FilterUser)
```











