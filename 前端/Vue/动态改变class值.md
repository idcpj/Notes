
[TOC]
## 切换选中状态
根据索引
```
<dd v-for="(price,index) in priceFilter" @click="currentPrice=index" >
   <a :class="{'current-price':currentPrice==index}"></a>
</dd>
```

## 已拼接形式动态改变 class
> [官网 computed 例子](https://cn.vuejs.org/v2/guide/computed.html)
```
<template>
    <div class="star" :class="starType">
    </div>
</template>

<script>
export default {
      computed: { //计算属性
        starType() { //  需要计算的值,可用户类,内容等
          return "star-"+this.size
        },
    }
}
</script>
```