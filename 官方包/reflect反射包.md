[TOC]

## 获取结构体的类型
```
type Admin struct {
   username string
   title    string
}

func main() {
   var u Admin
   t := reflect.TypeOf(u)
   field := t.Field(1)
   println(field.Name)        //title
   println(field.Type.Name()) //string

   f1, ok := t.FieldByName("username")
   println(ok)
   println(f1.Name)        //username
   println(f1.Type.Name()) //string
}
```
## 字段标签
```
type Admin struct {
   username string `demo:"user" type:"name"`
   title    string
}

func main() {
   var user Admin
   u := reflect.TypeOf(user)
   f, _ := u.FieldByName("username")
   demo := f.Tag.Get("demo")
   println(demo) //user
}
```