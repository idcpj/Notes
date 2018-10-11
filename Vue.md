[TOC]


## 快速构建
```
$ npm install --global vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm run dev
```


## Vue 对象属性
输出模板,用于多页面
```js
new Vue({
	el:"",
    data:{},
    methods:{},
    watch:{}
});
```
模块化,输出模块,用于单页面
```
export default {
    data:function {
        return{
            msg:"helloaa",
        }
    },
    methods:{},
}
```


### watch 监控属性值
```js
export default {
    data() {
        return {
             items: ['seee', 'eee']
        }
    },
    watch:{
        items:{  //当items 变化是触发函数
            console.log("items is change");
        },
     	c: {//如何 c 是具有[{},{}] 那么对象中的key或 vlue 要监听变化需要使用 deep:true
          handler: function (val, oldVal) { /* ... */ },
          deep: true
    	},
    }
}
```




## 技巧
### 结合 `v-for` 与`class`
通过对 item 值的判断来是否添加 class
```html
<li v-for="item in items" v-bind:class="{red:item.isred}" v-on:click="functinname(item)">
</li>
```
```js
items:[{
    name:'test1',
    isred:false
},
{
    name:'test2',
    isred:true
}]
```
### 绑定 一个回车事件
```      
<input type="text"  v-on:keyup.enter="enterFun">
```

### 获取DOM元素

```
//旧版
<div class="menu-wrapper"  v-el:food-wrapepr></div>

//script
 this.$els.foodWrapper

//新版
<div class="menu-wrapper"  ref="menuWrapper">
//script
this.$refs.menuWrapper
```


###  使用 `Vue.nextTick(functon)` 渲染完后执行
```js
created(){
  this.$http.get(config.apiHost.goods).then((response)=>{
    if (response.status === ERR_OK){
        this.goods = response.body
        // 由于 goods 的渲染是异步方式,所以加入 nextTick 时,使其可精确计算DOM 高度
        this.$nextTick(()=>{
            //在 dom 渲染完成后计算 dom 的高度
          this._initScroll()
          this._calculateHeight()
        })
    }

  })
}
```
### ` Vue.set` 向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新
```
//引入 vue
import Vue from "vue"

addCart(){
    if (!this.food.count){
    	//像 this.food  添加 count 元素 ,且赋值为一
      Vue.set(this.food, 'count', 1)
    } else {
      this.food.count++
    }
}
```
### 切换路由(选项卡) 保留数据
```
<keep-alive>
    <router-view :seller="seller" ></router-view>
</keep-alive>
```

### slot 插槽
> [参考文档](https://cn.vuejs.org/v2/guide/components-slots.html)
可以在组件中写入自定义的内容

### 导出并引入自定义模块
在`src/store.js`
```
const STOREGE_KEY = 'todo-vuejs'
export default{
    fetch(){
        alert(STOREGE_KEY);
    },
    save(items){
        alert(items);
    }
}
```

在`src/App.vue`
```
import store from './store'; //引入

export default {
    methods: {
        enterFun: function () {
            store.save(this.tiems);
        }
    }
}
```
