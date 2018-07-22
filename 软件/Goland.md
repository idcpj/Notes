
[TOC]

## 配置 - 使运行时,自动过滤 多余的 import
下载
`go get golang.org/x/tools/cmd/goimports`
goland 打开配置选项

`go  -> no save  ->file watch跳转 -> 添加 -> 选中`
![](../images/1CCE8E8A-D96D-4670-B715-664866717B6F.jpg)

 此时运行时,就会自动过滤不加载的 import 
 若没有效果 ,在`工具 -> gotool `中先运行一次 `goimport` 即可


## 快捷键
mac 
```
ctrl + p			查看 method 参数信息	
ctrl + shift + p	查看表达式类型
ctrl + alt + v		自动生成表达式返回值	
ctrl + shift + space	智能类型推断式返回
```