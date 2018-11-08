[TOC]

## 生成 npm 的账户
`www.npmjs.com`
> 注:申请完账户后,需验证邮箱
## 初始化
`npm init `

## 目录结构
```
npmjs
├─┬ lib
│ └── npmjs.js
├─┬ test
│ └── test.js
├── .gitignore
├── .npmignore
├── .travis.yml
├── index.js
├── LICENSE
├── makefile
├── package.json
├── README.md
```
- lib 目录下存放业务逻辑文件
test 目录下存放单元测试用例
.npmignore 记录哪些文件不需要被发布到npmjs.org
.travis.yml 是持续集成服务travis的描述文件
index.js 是入口文件
makefile 方便我们用make test进行测试
README.md 是此module的描述和使用方法

> LICENSE 可在github 中生成:create new file 文件名输入LICENSE -> 右侧选择类型，这里一般选择MIT。

## 代码内容


## 发布
首次发布
```
npm adduser

npm publish .
```
再发布
```
npm version patch
npm publish
```
