
[TOC]

## $http
> [github](https://github.com/pagekit/vue-resource)

### 安装
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

### 配置
在` main.js` 中
```
import VueResource from 'vue-resource'
Vue.use(VueResource)
```

## axios
> [github](https://github.com/axios/axios)

可在vue 中直接使用
```
// Make a request for a user with a given ID
axios.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .then(function () {
    // always executed
  });
```

