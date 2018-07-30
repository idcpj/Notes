
[TOC]

```go
type person struct {
	Name string `xml:"name"`
	Age  int    `xml:"age,attr"`  //设置为 person 标签的属性
}

func main() {
	//序列化
	a := person{Name: "cpj", Age: 12}
	str, e := xml.Marshal(a)
	if e != nil {
		fmt.Println(e)
		return
	}
	fmt.Println(string(str)) //<person><Name>cpj</Name><Age>12</Age></person>

	//xml.MarshalIndent(a, "", " ")
	/**
	<person>
	 <Name>cpj</Name>
	 <Age>12</Age>
	</person>
	*/

	//反序列化
	p := new(person)
	err := xml.Unmarshal(str, p)
	if err != nil {
		fmt.Println(err)
		return
	}
	p.Name = "asdsad"
	fmt.Println(p.Name) //cpj

}
```