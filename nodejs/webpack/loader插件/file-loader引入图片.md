[TOC]

## 安装
`npm install --save-dev file-loader`

在`webpack.config.js`配置
```
{
    test: /\.(png|jpg|gif|svg)$/i,
    use: {
        loader: 'file-loader',
        options: {
              name: '[path][name].[ext]'
        }
    }
},
```
1. 在`添加背景图片与在 index.hmtl 添加图片`,设置相同,直接写图片的 相对路径即可

2. 在模板文件中添加图片如`layer.tpl`
```
<img src="${require('../../assets/1.jpg')}" alt="">
```