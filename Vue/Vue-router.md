
[TOC]

> [参考文档](https://www.jianshu.com/p/4c5c99abb864)

1. 安装
`npm i vue-router -S`
2. 在`router.js`
```
import Vue from 'vue';
import Router from 'vue-router';
import goodlist from '@/views/goodlist';

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: '/',
      name: 'goodlist',
      component: goodlist,
    },
  ]
})

```
3. 在 `main.js ` 中
```
//code
import router from './router'
//code
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
});
```      

3. 在`app.vue`中
```
<template>
      <nav-header></nav-header>
      <router-view :goods="goods"></router-view>  //todo
      <nav-footer></nav-footer>
</template>
```
路由也允许使用 props 传值

## 设置 url 的显示
### hash 值
url :`http://127.0.0.1:8080/#/ratings`
```
const router = new VueRouter({
  mode: 'hash',
  lineActiveClass: 'active',
  routes // (缩写) 相当于 routes: routes
})
```
### 
url:`http://127.0.0.1:8080/goods`
```
const router = new VueRouter({
  mode: 'history',
  lineActiveClass: 'active',
  routes // (缩写) 相当于 routes: routes
})
```
## 动态路由
路由配置
```
export default new Router({
  routes: [
    {
      path: '/goods/:id',
      name: 'HelloWorld',
      component: HelloWorld
    },
  ]
})
```
vue 文件
```
<span>{{ $route.params.goodsId }}</span>
```
在 url 中访问
`http://localhost:8080/#/goods/12`
注意 `hash`模式中 `#` 在最前面

## 嵌套路由
需要在模板中在添加 `router-view`
```
const User = {
  template: `
    <div class="user">
      <h2>User {{ $route.params.id }}</h2>
      <router-view></router-view>
    </div>
}
```
配置路由
```
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```
## 编程式的导航
```
// 字符串
router.push('home')

// 命名的路由
router.push({ name: 'user', params: { userId: 123 }}) // -> /user/123
```
### router.go(n)
```
// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)

// 后退一步记录，等同于 history.back()
router.go(-1)

// 前进 3 步记录
router.go(3)
``` 
## 命名视图
带 name 属性的` router-view`会直接显示.
```
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>
```
router 配置
```
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {  //注意 component得改成components  记得到加 s
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
})
```



