
[TOC]

两种方式的等效

```
<template>
<div v-if="seller.supports" class="supports">
	//通过 seller.supports[0].type 的数组来选择 class
     <span class="icon " :class="classMap[seller.supports[0].type]"></span>
     <span class="text">{{seller.supports[0].description}}</span>
</div>
</template>

let newVar = {
  data() {
    return {
      classMap: ['decrease', 'discount', 'guarantee', 'special']
    }
  },
  props: {
    seller: {
      type: Object
    }
  },
  created(){
    this.classMap = ['decrease', 'discount', 'guarantee', 'special']
  },
   components: {}
}
````