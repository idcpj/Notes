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
## 引入单纯的 c 文件
由于直接引入 c 文件不便于调试
test.h
```
#ifndef __TEST_H__
#define __TEST_H__
void hello();
#endif
```
test.c
```
#include <stdio.h>
#include "test.h"
void hello() {
    printf("Hello, World!\n");
}
#ifdef __TEST__ // 避免和 Go bootstrap main 冲突。
int main(int argc, char *argv[]) {
    hello();
    return 0;
}
#endif
```
main.go
```
package main
/*
 #include "test.h"
*/
import "C"

func main() {
   C.hello()
}
```