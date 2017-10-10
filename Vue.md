# Vue

---
[TOC]

简单引入
```
<script src="https://unpkg.com/vue"></script>
```
## 1.快速入门
### 1.绑定前端
```
<div id="app">
  {{message}}
  {{message1}}
	<p>{{message2}}</p>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello ',
	message1:"word",
	message2:"Vue"
  }
})
</script>
```
### 2.绑定DOM属性
```
<div id="app">
  <input type="text" v-bind:value="message" v-bind:name="name">
</div>

<script>
new Vue({
  el: '#app',	
  data: {
    message: 'Hello ',
	name:"word"
  }
})
</script>
```

### 3.条件
```javascript
<div id="app">
  <p v-if="seen===1">如果seen为true 就可以看到我</p>
  <p v-else-if="seen===2">如果seen为true 就可以看到我</p>
  <p v-else>No</p>
  
  //对整体进行判定
  <template v-if="ok">
      <h1>Title</h1>
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
 </template>

  
</div>



<script>
new Vue({
  el: '#app',	
  data: {
	seen:false
  }
})
</script>
```
### 4.循环
#### 1.对数据渲染
```js
<div id="app">
  <ol>
    <li v-for="todo in todos"> //v-for="(item, index) in items"
      {{ todo.text }}
    </li>
  </ol>
</div>

<script>
var Vue3 = new Vue({
  el: '#app',	
  data: {
	todos:[{text:"hello"},{text:"word"},{text:"Vue"}]
  }
})
Vue3.todos.push({text:"!!!"}); //会增加一行
</script>
```
#### 2.对数组属性渲染
```js
<ul id="v-for-object" class="demo">
  <li v-for="value in object"> //v-for="(value, key) in object"
    {{ value }}
  </li>
</ul>
<script>
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
})
</script>
```

### 5.绑定事件
```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">点击弹窗</button>
</div>

<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      alert(this.message);//不需要this.data.message
    }
  }
})
</script>
```
### 6.表单输入和应用状态绑定信息
```js
<div id="app-6">
  <p>{{ message }}</p>
  <input type="text" v-model="message">
</div>

<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
</script>
```
### 7.组件化
```js
<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>

<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '随便其他什么人吃的东西' }
    ]
  }
})
</script>
```
### 8.缩写
```js
<a v-bind:href="url"></a>
<a :href="url"></a>  //缩写

<a v-on:click="doSomething"></a>
<a @click="doSomething"></a>  //缩写
```
### 9.computed 计算属性
该属性会把计算结果进行缓存 而watch 不会
```js
<div id="demo">{{ fullNameF }}</div>

<script>
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullNameF: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
<script/>
```
### 10.计算属性的 setter
```
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```
*现在再运行 vm.fullName = 'John Doe' 时，setter 会被调用，vm.firstName 和 vm.lastName 也相应地会被更新。*
### 11.watch的用法
watch  可用于执行异步操作,并设置操作频率 [链接][1]
```js
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
  <p>newQuestion:{{ newQuestion }}</p>
  <p>oldQuestion:{{ oldQuestion }}</p>
</div>
<script>
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!',
	newQuestion:'',
	oldQuestion:''
  },
  watch: {
    // 如果 question 发生改变，这个函数就会运行
    question: function (newQuestion,oldQuestion) {
	this.newQuestion=newQuestion;
	this.oldQuestion=oldQuestion;
      this.answer = 'Waiting for you to stop typing...'
    }
  }
})
</script>
</body>
```


  [1]: https://cn.vuejs.org/v2/guide/computed.html#%E8%A7%82%E5%AF%9F%E8%80%85