
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



