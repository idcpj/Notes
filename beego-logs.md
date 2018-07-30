
[TOC]

### demo
```
package main

import (
	"fmt"
	"time"

	"github.com/astaxie/beego/logs"
)

func main() {
	//配置
	log := logs.NewLogger(10000)
	year := time.Now().Year()
	month := time.Now().Month()
	day := time.Now().Day()
	logConfig := fmt.Sprintf(`{"filename":"log/%d/%d/%d/%d-%d-%d.log"}`, year, month, day, year, month, day)
    
    //测试
	log.SetLogger("file", logConfig)
	log.Trace("trace")
	log.Info("info")
	log.Warn("warning")
	log.Debug("debug")
	log.Critical("critical")
    
    //效果
    /**
        2018/07/30 10:59:09.455 [D]  trace
        2018/07/30 10:59:09.456 [I]  info
        2018/07/30 10:59:09.456 [W]  warning
        2018/07/30 10:59:09.456 [D]  debug
        2018/07/30 10:59:09.456 [C]  critical
	 */
}

```
## 配置文件
1. 输出到控制台
```
//file
log.SetLogger("console", "")
```
2. 输出到文件
```
log.SetLogger("file", `{"filename":"test.log"}`)
```
3. 发送到邮箱
```
log.SetLogger("smtp", `{"username":"beegotest@gmail.com","password":"xxxxxxxx","host":"smtp.gmail.com:587","sendTos":["xiemengjun@gmail.com"]}`)

```
4. 多类型进行分类
```
log.SetLogger("multifile", `{"filename":"test.log","separate":["emergency", "alert", "critical", "error", "warning", "notice", "info", "debug"]}`)
```
>生成的文件为`2018-7-30.error.log`,`2018-7-30.info.log`