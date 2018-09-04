
[TOC]

> [github](https://github.com/pagekit/vue-resource)

## 安装
`npm install vue-resource`

```
{
  // GET /someUrl
  this.$http.get('/someUrl').then(response => {

    // get body data
    this.someData = response.body;

  }, response => {
    // error callback
  });
}
```

## 配置
在` main.js` 中
```
import VueResource from 'vue-resource'
Vue.use(VueResource)
```