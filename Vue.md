[TOC]

## 简单安装

1. `<script >`引入
```
<!-- 开发环境版本，包含了用帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```
2. npm 安装
`npm install  [-g] vue`


## 用命令行快速初始化项目
```bash
# 安装 vue-cli
$ npm install --global vue-cli
# 使用 "webpack" 模板创建一个新项目
$ vue init webpack my-project
# 安装依赖，然后开始！
$ cd my-project
$ npm run dev
```
通过 `run dev` 的项目 会自动进行更新

## Vue 对象属性
输出模板
```js
new Vue({
	el:"",
    data:{},
    methods:{},
    watch:{}
});
```
模块化,输出模块
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

## 模板指令

### 数据渲染
```html
<p>{{ a }}</p>
<p v-text="a"></p>
<p v-html="a"></p>
```
### 控制模块隐藏
```html
<p v-if="isShow"></p>
<p v-if="isShow"></p>
```

### 渲染列表
```html
<li v-for="item in items">
	<p v-text="item.lable"></p>
</li>
```
### 事件绑定
```
<button v-on:click="doThis"></button>
<button @click="doThis"></button>  //简写
```
```js
method:{
	doTHis:function(param){ }
}
```

### 属性赋值
```
<img v-bind:src="imageSrc" >
<div :class="{red:isRed}"></div>   //是否有 通过 isRed 来判断是否添加 red 这个 class 
<div :class="[classA,classB]"></div>  //添加 多个 class
<div :class="[classA,{classB:isB,classC:isC}]"></div>  //混合
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



## 模块输出
```
export default {
  name: 'HelloWorld',
  data :function(){
    return {
      msg: 'Welcome to Your Vue.js App1111'
    }
  }
}

// data 的赋值  等同于
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
```

## 技巧
### 一个组件根 id 只有一个
```
<template>
  	<div id="app1">	</div>
    <!--错误-->
    <div></div>
    <!--错误-->
	<div id="test"></div>
</template>
```
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
旧版:
```
<div class="menu-wrapper"  v-el:food-wrapepr></div>

//通过 v-el 绑定元素,在通过 this.$els.foodWrapper 获取绑定的元素
 this.menuScroll = new BScroll(this.$els.foodWrapper)
```

新版
```
<div class="menu-wrapper"  ref="menuWrapper">


this.menuScroll = new BScroll(this.$refs.menuWrapper, {})
```

###  使用 `Vue.nextTick()` 异步获取数据后,计算 dom 元素
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