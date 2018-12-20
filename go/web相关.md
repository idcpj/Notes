
[TOC]

> [gitbook 参考](https://astaxie.gitbooks.io/build-web-application-with-golang/zh/)

## demo
```
package main

import (
	"fmt"
	"html/template"
	"log"
	"net/http"
)

func sayhelloName(w http.ResponseWriter, r *http.Request) {
	log.Println("打印到控制台")            //2018/07/23 10:05:55  打印到控制台
	fmt.Fprintf(w, "Hello astaxie!") //这个写入到w的是输出到客户端的
}

func login(w http.ResponseWriter, r *http.Request) {
	r.ParseForm() //需要加这一步,才能解析 post 表单
	fmt.Println("method:", r.Method)
	if r.Method == "GET" {
		t, e := template.ParseFiles("login.gtpl") //加载模板文件
		if e != nil {
			log.Println(e)
		}
		log.Println(t.Execute(w, nil))
	} else {
		fmt.Println("username:", r.Form["username"])
		fmt.Println("password:", r.Form["password"])
	}
}

func main() {
	http.HandleFunc("/", sayhelloName)       //设置访问的路由
	http.HandleFunc("/login", login)         //设置访问的路由
	err := http.ListenAndServe(":9090", nil) //设置监听的端口
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}
```
## 原生获取get post 参数
### 获取get 参数
```
//获取多个参数
values := r.URL.Query()
log.Println(values) //map[age:[1] ip:[127.0.0.1]]

//获取单个
age := values.Get("age") //1
log.Println(age)
```
### 获取post 参数
```
//获取单个
name := r.PostFormValue("name")
log.Println(name)

//获取多个
r.ParseForm()
values := r.PostForm
log.Println(values)
// 方式一.获取单个
log.Println(values["name"])
//方式二.获取单个
name = values.Get("name")
log.Println(name)
```

## request.Form 参数格式
```
v := url.Values{}
    v.Set("name", "Ava")
    v.Add("friend", "Jess")
    v.Add("friend", "Sarah")
    v.Add("friend", "Zoe")
    // v.Encode() == "name=Ava&friend=Jess&friend=Sarah&friend=Zoe"
    fmt.Println(v.Get("name"))
    //fmt.Println(v.Get("friend")) //Jess
    fmt.Println(v["friend"]) //[Jess Sarah Zoe]
```
## 表单上传验证
### 判断是否是整数
```
etint, err := strconv.Atoi(r.Form.Get("age"))
if err != nil {
    //数字转化出错了，那么可能就不是数字
}
fmt.Println(etint)
```
### 验证是否中文
```
if m, _ := regexp.MatchString("^\\p{Han}+$", r.Form.Get("realname")); !m {
    return false
}
```
### 英文
```
if m, _ := regexp.MatchString("^[a-zA-Z]+$", r.Form.Get("engname")); !m {
    return false
}
```
### 电子邮件地址
```

if m, _ := regexp.MatchString(`^([\w\.\_]{2,10})@(\w{1,}).([a-z]{2,4})$`, r.Form.Get("email")); !m {
    fmt.Println("no")
}else{
    fmt.Println("yes")
}
```
### 手机号码
```
if m, _ := regexp.MatchString(`^(1[3|4|5|8][0-9]\d{4,8})$`, r.Form.Get("mobile")); !m {
    return false
}
```
### 下拉菜单
```
slice:=[]string{"apple","pear","banane"}

v := r.Form.Get("fruit")
for _, item := range slice {
    if item == v {
        return true
    }
}

return false
```
### 单选按钮
```
slice:=[]int{1,2}

for _, v := range slice {
    if v == r.Form.Get("gender") {
        return true
    }
}
return false
```
### 复选框
```

slice:=[]string{"football","basketball","tennis"}
a:=Slice_diff(r.Form["interest"],slice)
if a == nil{
    return true
}

return false
```
> [Slice_diff 函数在github](https://github.com/astaxie/beeku) 


###  日期和时间
```
t := time.Date(2009, time.November, 10, 23, 0, 0, 0, time.UTC)
fmt.Printf("Go launched at %s\n", t.Local())
```
### 身份证号码
```
//验证15位身份证，15位的是全部数字
if m, _ := regexp.MatchString(`^(\d{15})$`, r.Form.Get("usercard")); !m {
    return false
}

//验证18位身份证，18位前17位为数字，最后一位是校验位，可能为数字或字符X。
if m, _ := regexp.MatchString(`^(\d{17})([0-9]|X)$`, r.Form.Get("usercard")); !m {
    return false
}
```
## 预防跨站脚本
```
fmt.Println("username:", template.HTMLEscapeString(r.Form.Get("username"))) //输出到后台 <cpj>  -> &lt;cpj&gt;
template.HTMLEscape(w, []byte(r.Form.Get("username")))                      // 输出到 客户端   <cpj> -> &lt;cpj&gt;
```
