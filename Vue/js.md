[TOC]
## 非默认模块
`src/common/js/date.js`
```js
export function formatDate (date) {  
  return "1212"  
}
// =========//
//调用
import { formatDate } from '@/common/js/date.js'

```

## 默认模块
`src/common/js/date.js`
```js
export  default function formatDate (date) {  
  return "1212"  
}
// =========//
// 调用
import  formatDate  from '@/common/js/date.js'
```