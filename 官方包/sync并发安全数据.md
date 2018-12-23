[TOC]

## 并发安全的 map
```
errorMap := &sync.Map{}
errorMap.Store(key, value) //更新或者新增
errorMap.Load(key) //取
errorMap.delete(key)//删
errorMap.Range(function(k,v interface{})bool{//todo }) //遍历
```