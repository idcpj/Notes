
[TOC]

## struct 转json 需要注意
1. struct的结构属性必须为大写字母开头,表示外部可读
2. 在最后添加第三个参数,表示转换为json 时候命名为什么
```
type DeptNode struct {
	DeptId       interface{} `json:"dept_id"`
	DeptParentId interface{} `json:"dept_parent_id"`
	Name         interface{} `json:"name"`
	OrderId      interface{} `json:"order_id"`
	Users        interface{} `json:"users"`
	//SubDepts []*DeptNode `json:"sub_dept"`
}

//转换为json
b, err := json.Marshal(tree)
fmt.Println("json:", string(b))  //需要在此处 添加string才能转为字符串
```

## 处理位置的json
```
//如何处理一个位置的json
a := `{"Servers":[{"serverName":"Shanghai_VPN","serverIP":"127.0.0.1"},{"serverName":"Beijing_VPN","serverIP":"127.0.0.2"}]}`

var s interface{}
err := json.Unmarshal([]byte(a), &s)
if err != nil {
    panic(err)
}

m := s.(map[string]interface{})

for k, v := range m {
    switch vv := v.(type) {
    case string:
        fmt.Println(k, "is string", vv)
    case int:
        fmt.Println(k, "is int", vv)
    case float64:
        fmt.Println(k, "is float64", vv)
    case []interface{}:  //核心代码
        fmt.Println(k, "is an array:")
        for i, u := range vv {
            fmt.Println(i, u)
        }
    default:
        fmt.Println(k, "is of a type I don't know how to handle")
    }
}
/**
Servers is an array:
0 map[serverName:Shanghai_VPN serverIP:127.0.0.1]
1 map[serverName:Beijing_VPN serverIP:127.0.0.2]
map[Servers:[map[serverName:Shanghai_VPN serverIP:127.0.0.1] map[serverName:Beijing_VPN serverIP:127.0.0.2]]]
 */
 ```

