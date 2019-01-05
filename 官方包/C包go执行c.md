[TOC]

## 在go 程序中
```
/*
 #include <stdio.h>
 #include <stdlib.h>
 void hello() {
 printf("Hello, World!\n");
 }
*/
import "C"

func main() {
   C.hello()
}
```