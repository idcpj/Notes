
[TOC]

> [参考文档](https://www.jianshu.com/p/4c5c99abb864)

1. 安装
`npm i vue-router -S`
2. 在`main.js`
```
import Vue from 'vue';
import VueRouter from 'vue-router';

//主体
import App from './components/app.vue';
import goods from './components/goods.vue'
//安装插件
Vue.use(VueRouter); //挂载属性
//创建路由对象并配置路由规则

const routes = [
  { path: '/goods', component: goods },
]

const router = new VueRouter({
  routes   //把 router 传入 VueRouter
})

new Vue({
    el: '#app',
    router
    render: c => c(App),
})
```

3. 在`app.vue`中
```
<template>
    <div>
	    <router-link to="/goods">商品</router-link>
        <!-- 留坑，非常重要 -->
        <router-view></router-view>
    </div>
</template>
```