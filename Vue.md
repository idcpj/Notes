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
    methods:{}
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
1. 一个组件根 id 只有一个
```
<template>
  	<div id="app1">	</div>
    <!--错误-->
    <div></div>
    <!--错误-->
	<div id="test"></div>
</template>
```
2. 结合 `v-for` 与`class`
通过对 item 值的判断来是否添加 class
```html
<li v-for="item in items" v-bind:class="{red:item.isred}">
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