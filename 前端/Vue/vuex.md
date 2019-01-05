[TOC]

## 安装
```

```
## 目录结构
![](../images/BC775958-5425-449C-B46B-E4E9336605F0.jpg)

## 核心概念
### Getter - 以`state`数据为基准,创建新的数据
```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
//访问
this.$store.getters.doneTodosCount
```
###  Mutation - store 中的状态的唯一方法
```
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state, n) {
    state.count += n
  }
})
//调用
store.commit('increment', 10)
```
### actions 
Action 可以包含任意异步操作。
Action 提交的是 mutation

## 简单调用
```
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}
```