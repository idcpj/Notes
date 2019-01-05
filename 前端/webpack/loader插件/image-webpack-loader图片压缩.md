[TOC]
> [github](https://github.com/tcoopman/image-webpack-loader)
> 自动压缩图片
## 安装
`$ npm install image-webpack-loader --save-dev`

## 配置
需要配合` file-loader`  貌似不能与`url-loader` 配置
```js
{
    test: /\.(png|jpg|gif|svg)$/i,
    use: [
            {
                loader: 'file-loader',
                options: {
                    name: '[path][name].[ext]'
                },
            },
            {
                loader: 'image-webpack-loader',

            },
        ]
},
```