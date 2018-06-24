[TOC]
> [中文手册](https://webpack.docschina.org/loaders/url-loader/)

url-loader 功能类似于 file-loader，但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。

如果使用`url-loader` 可无需使用`file-loader`


## 安装
`npm install --save-dev url-loader`

## 配置

```
{
    test: /\.(png|jpg|gif|svg)$/i,
    use: {
        loader: 'url-loader',
        options: {
            limit: 10000,  //小于10kb 的转为 base64位
                name: '[path][name].[ext]'
        },
    }
},
```
## 分析
优点
1. 减少请求数
缺点
1. 没有了图片的缓存
2. 增加了 html 文件的体积

