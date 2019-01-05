[TOC]

## 安装
`npm install vue-infinite-loading --save`
## 使用
组件形式应用

html
```
<ul>
    <li v-for="(goods,index) in goodsList" :key="index">
    </li>
</ul>
<infinite-loading @infinite="loadMore" spinner="waveDots"></infinite-loading>
```

xxx.vue
```
import InfiniteLoading from 'vue-infinite-loading';

export default {
    methos:{
        loadmore(){
            //todo
            if(res.data.result.count<this.pageSize){
                $state.complete()
            }else {
                $state.loaded();
            }
    }
  components: {
    InfiniteLoading,
  },
};
```
