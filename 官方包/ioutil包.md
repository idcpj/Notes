[TOC]
### 写入文件
```go
ioutil.WriteFile(filename, data, 0666)
```

## 获取实现`Read`接口的全部数据
```
// Read(p []byte) (n int, err error)  
ioutil.ReadAll(r.Body.Read())
```