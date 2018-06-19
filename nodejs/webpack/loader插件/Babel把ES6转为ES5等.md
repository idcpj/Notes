[TOC]
> [参考手册](https://webpack.docschina.org/loaders/babel-loader/)

## demo
```
rules: [
    {
        test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
        include:true_path+'/src',
        use: {
            loader: 'babel-loader',
            options: {
                // presets: ['@babel/preset-env']
            }
        }
    },
]
```