
[TOC]

## 给 data 中 元素一个初始值
--: 调用一个立即执行的函数
```
data(){
  return {
    classMap: ['decrease', 'discount', 'guarantee', 'invoice', 'special'],
    favorite: (()=>{
      return loadFromLocal(this.seller.id, 'favorite', false)
    })()
  }
},
````