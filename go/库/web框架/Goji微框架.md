
[TOC]

> [官网](https://goji.io/)


## 安装
```
go get goji.io
```

## demo
```
package main

import (
	"fmt"
	"net/http"

	"goji.io"
	"goji.io/pat"
)

func hello(w http.ResponseWriter, r *http.Request) {
	name := pat.Param(r, "name")
	fmt.Fprintf(w, "Hello, %s!", name)
}

func main() {
	mux := goji.NewMux()
	mux.HandleFunc(pat.Get("/hello/:name"), hello)

	http.ListenAndServe("localhost:8000", mux)
}
```