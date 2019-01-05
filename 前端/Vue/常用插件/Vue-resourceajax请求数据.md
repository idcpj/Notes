
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
### interceptors 拦截器
对所有请求做些 统一的前置操作
```
 mounted:function () {
    Vue.http.interceptors.push(function(request) {
        console.log("进入前置操作);
        // modify method
        request.method = 'POST';
        // modify headers
        request.headers.set('X-CSRF-TOKEN', 'TOKEN11111');
        return function(response) {
            // modify response
            response.body = '修改返回值'
        };
    });
},
methods:{
  get:function () {
      this.$http.get("package.json").then(function (res) {
          console.log(res.data);
          this.getData = res.data
      })
  }
}
```


