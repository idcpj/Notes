[TOC]

## 安装
`npm install vue-infinite-scroll --save`

## 使用
```
import infiniteScroll from 'vue-infinite-scroll'
Vue.use(infiniteScroll)
```
xx.vue
```
<div v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="10">
    <img v-show="!this.busy" width="32px" height="32px" src="../assets/img/loading-spinning-bubbles.svg" alt="">
</div>
```

script
```
loadMore(){
    this.busy = true; //使滚动加载失效
    setTimeout(() => {  //使用 setTImeout 防止 连续发送请求
        this.page++;
        this.getGoodsList(true)
    }, 1000);
},
```