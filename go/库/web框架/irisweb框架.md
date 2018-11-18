[TOC]

## 安装
` go get -u github.com/kataras/iris`

## 快速入门
```
func main() {
	app :=iris.New()
	app.Get("/", func(c iris.Context) {
		c.WriteString("hello word")
	})
        //模板输出
        app.RegisterView(iris.HTML("./",".html"))
	app.Get("/hello", func(c iris.Context) {
		c.ViewData("title","this is a iris")
		c.ViewData("content","this is a content")
		c.View("hello.html")
	})
	app.Run(iris.Addr(":8080"))
}
```