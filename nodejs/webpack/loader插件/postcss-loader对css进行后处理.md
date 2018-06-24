[TOC]

> [参考](https://webpack.docschina.org/loaders/postcss-loader/)
> [ github postcss 的其他插件](https://github.com/postcss/postcss)
## 添加 css 前缀的demo
在`webpack.config.js`
```
{
    test: /\.css$/,
    use: [ 'style-loader', 'css-loader','postcss-loader',]//添加 postcss-loader, 配置以倒叙执行
}
```

在新建`postcss.config.js`
```
module.exports = {
    plugins: {
        'autoprefixer': {
            browsers: 'last 5 version' // 代表意思为每个主流浏览器的最后5个版本
        }
    }
}
```
