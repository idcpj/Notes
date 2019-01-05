[TOC]

> [loader 插件列表](https://webpack.docschina.org/loaders/)


## 列表
### 文件
```
raw-loader 加载文件原始内容（utf-8）
val-loader 将代码作为模块执行，并将 exports 转为 JS 代码
url-loader 像 file loader 一样工作，但如果文件小于限制，可以返回 data URL
file-loader 将文件发送到输出文件夹，并返回（相对）URL
JSON
json-loader 加载 JSON 文件（默认包含）
json5-loader 加载和转译 JSON 5 文件
cson-loader 加载和转译 CSON 文件
```
### 转换编译(Transpiling)
```
script-loader 在全局上下文中执行一次 JavaScript 文件（如在 script 标签），不需要解析
babel-loader 加载 ES2015+ 代码，然后使用 Babel 转译为 ES5
buble-loader 使用 Bublé 加载 ES2015+ 代码，并且将代码转译为 ES5
traceur-loader 加载 ES2015+ 代码，然后使用 Traceur 转译为 ES5
ts-loader 或 awesome-typescript-loader 像 JavaScript 一样加载 TypeScript 2.0+
coffee-loader 像 JavaScript 一样加载 CoffeeScript
```
### 模板(Templating)
```
html-loader 导出 HTML 为字符串，需要引用静态资源
pug-loader 加载 Pug 模板并返回一个函数
jade-loader 加载 Jade 模板并返回一个函数
markdown-loader 将 Markdown 转译为 HTML
react-markdown-loader 使用 markdown-parse parser(解析器) 将 Markdown 编译为 React 组件
posthtml-loader 使用 PostHTML 加载并转换 HTML 文件
handlebars-loader 将 Handlebars 转移为 HTML
markup-inline-loader 将内联的 SVG/MathML 文件转换为 HTML。在应用于图标字体，或将 CSS 动画应用于 SVG 时非常有用。
```
### 样式
```
style-loader 将模块的导出作为样式添加到 DOM 中
css-loader 解析 CSS 文件后，使用 import 加载，并且返回 CSS 代码
less-loader 加载和转译 LESS 文件
sass-loader 加载和转译 SASS/SCSS 文件
postcss-loader 使用 PostCSS 加载和转译 CSS/SSS 文件
stylus-loader 加载和转译 Stylus 文件
```

### 清理和测试(Linting && Testing)
```
mocha-loader 使用 mocha 测试（浏览器/NodeJS）
eslint-loader PreLoader，使用 ESLint 清理代码
jshint-loader PreLoader，使用 JSHint 清理代码
jscs-loader PreLoader，使用 JSCS 检查代码样式
coverjs-loader PreLoader，使用 CoverJS 确定测试覆盖率
```

### 框架(Frameworks)
```
vue-loader 加载和转译 Vue 组件
polymer-loader 使用选择预处理器(preprocessor)处理，并且 require() 类似一等模块(first-class)的 Web 组件
angular2-template-loader 加载和转译 Angular 组件
```