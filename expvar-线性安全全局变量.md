[TOC]
## 说明
用来存放简单的全局变量,并且是线性安全
```
expvar.NewInt()
expvar.NewFloat()
expvar.NewString()
expvar.NewMap()
```
通过访问`/debug/vars` 接口可以打印所有的值

### 用法
```
var visits = expvar.NewInt("visits")
var ex_string = expvar.NewString("ex_string")

func handler(w http.ResponseWriter, r *http.Request) {
	//添加值
	visits.Add(1)
	log.Println(visits.Value())	//获取值

	ex_string.Set("dmeo3")
	log.Println(ex_string.Value()) //demo3

	log.Println("bists")
	fmt.Fprintf(w, "Hi there, I love %s!", r.URL.Path[1:])
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}
```