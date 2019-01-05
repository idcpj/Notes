[TOC]


## 配置 cordova
[cordova 部署](https://www.kancloud.cn/idcpj/python/818333)

## 配置vue
`config/index.js `
```
 build: {
        // Template for index.html
        index: path.resolve(__dirname, '../App/www/index.html'),

        // Paths
        assetsRoot: path.resolve(__dirname, '../App/www'),
}
```
`package.json`
```
"scripts": {
    "build:android": "node build/build.js && cd App &&  cordova run android"  //自动打包安卓的例子
 },
```