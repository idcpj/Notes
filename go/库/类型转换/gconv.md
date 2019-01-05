[TOC]

> [教程](https://www.ctolib.com/topics-135944.html)

## 安装
`gitee.com/johng/gf/g/util/gconv`

## 接口
```
// 基本类型
func Bool(i interface{}) bool
func Float32(i interface{}) float32
func Float64(i interface{}) float64
func Int(i interface{}) int
func Int16(i interface{}) int16
func Int32(i interface{}) int32
func Int64(i interface{}) int64
func Int8(i interface{}) int8
func String(i interface{}) string
func Uint(i interface{}) uint
func Uint16(i interface{}) uint16
func Uint32(i interface{}) uint32
func Uint64(i interface{}) uint64
func Uint8(i interface{}) uint8

// slice类型
func Bytes(i interface{}) []byte
func Ints(i interface{}) []int
func Floats(i interface{}) []float64
func Strings(i interface{}) []string
func Interfaces(i interface{}) []interface{}

// 时间类型
func Time(i interface{}, format ...string) time.Time
func TimeDuration(i interface{}) time.Duration

// 对象转换
func Struct(params interface{}, objPointer interface{}, attrMapping ...map[string]string) error

// 根据类型名称执行基本类型转换(非struct转换))
func Convert(i interface{}, t string, extraParams ...interface{}) interface{}
```

##  struct 转换
使用tag 标签
```
type user struct {
	Name string
	Agg  int `gconv:"age"`  //可使用tag 标签
}

a := map[string]string{
	"name": "coj",
	"age":  "12",
}

User := new(user)
gconv.Struct(a, User)
fmt.Println(User)
```