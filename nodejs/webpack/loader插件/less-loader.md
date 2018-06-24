[TOC]
> [中文手册](https://webpack.docschina.org/loaders/less-loader)

## 安装
`npm install --save-dev less-loader less`

## 配置
```
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            use: [
                {loader: "style-loader" // creates style nodes from JS strings
                }, {loader: "css-loader" // translates CSS into CommonJS
                }, {loader: "postcss-loader" //
                }, {loader: "less-loader" // compiles Less to CSS
                }]
        }]
    }
};
```
> 加入` postcss-loader` 会对 less 进行加浏览器前缀
