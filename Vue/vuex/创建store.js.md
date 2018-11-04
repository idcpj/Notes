[TOC]

## 创建`store.js` 并调用
`store.js`
```
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);
export default new Vuex.Store({
    state:{
        nickName:"",
        cartCount:0,
    },
    mutations:{
        updateName(state,nickName){
            state.nickName = nickName
        },
        updateCartCount(state,count){
            state.cartCount += count;
        }
    }
})
```
在 `main.js`
```
import store from "@/store";

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  store, //引入
  components: { App },
  template: '<App/>'
})
```
在组件中
```
return this.$store.state.cartCount
```