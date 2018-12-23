[TOC]

## redis 连接池

> [参考文档](https://blog.csdn.net/stevefang/article/details/40474827)

```
//通过redis struct已对象形式构建
import (
	"time"

	"github.com/astaxie/beego"
	"github.com/garyburd/redigo/redis"
)

var (
	// 定义常量
	RedisClient *redis.Pool
	REDIS_HOST  string
	REDIS_DB    int
)

func init() {
	// 从配置文件获取redis的ip以及db
	//REDIS_HOST = beego.AppConfig.String("redis_ip")
	REDIS_HOST = "127.0.0.1:6379"
	REDIS_DB = 0
	// 建立连接池
	RedisClient = &redis.Pool{
		// 从配置文件获取maxidle以及maxactive，取不到则用后面的默认值
		MaxIdle:     beego.AppConfig.DefaultInt("redis.maxidle", 3),
		MaxActive:   beego.AppConfig.DefaultInt("redis.maxactive", 100),
		IdleTimeout: 180 * time.Second,
		Dial: func() (redis.Conn, error) {
			c, err := redis.Dial("tcp", REDIS_HOST)
			if err != nil {
				return nil, err
			}
			// 选择db
			c.Do("SELECT", REDIS_DB)
			return c, nil
		},
	}
}

func Set(key string, value interface{}) error {
	pool := RedisClient
	get := pool.Get()

	defer get.Close()
	_, err := get.Do("set", key, value)

	return err
}
func Get(key string) string {
	pool := RedisClient
	get := pool.Get()
	defer get.Close()
	reply, err := get.Do("get", key)
	if err != nil {
		beego.Debug(err)
	}
	s := ByteToString(reply)
	return s
}

func ByteToString(inter interface{}) string {
	var str string
	if inter == nil {
		str = ""
	} else {
		str = string(inter.([]byte))
	}
	return str
}
```

## 其他redis 的操作

> [参考路径](https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/05.6.md)

1. [https://github.com/garyburd/redigo](https://github.com/garyburd/redigo)

```
package main

import (
	"fmt"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/garyburd/redigo/redis"
)

var (
	Pool *redis.Pool
)

func init() {
	redisHost := ":6379"
	Pool = newPool(redisHost)
	close()
}

func newPool(server string) *redis.Pool {

	return &redis.Pool{

		MaxIdle:     3,
		IdleTimeout: 240 * time.Second,

		Dial: func() (redis.Conn, error) {
			c, err := redis.Dial("tcp", server)
			if err != nil {
				return nil, err
			}
			return c, err
		},

		TestOnBorrow: func(c redis.Conn, t time.Time) error {
			_, err := c.Do("PING")
			return err
		}
	}
}

func close() {
	c := make(chan os.Signal, 1)
	signal.Notify(c, os.Interrupt)
	signal.Notify(c, syscall.SIGTERM)
	signal.Notify(c, syscall.SIGKILL)
	go func() {
		<-c
		Pool.Close()
		os.Exit(0)
	}()
}

func Get(key string) ([]byte, error) {

	conn := Pool.Get()
	defer conn.Close()

	var data []byte
	data, err := redis.Bytes(conn.Do("GET", key))
	if err != nil {
		return data, fmt.Errorf("error get key %s: %v", key, err)
	}
	return data, err
}

func main() {
	test, err := Get("test")
	fmt.Println(test, err)
}
```

1. [https://github.com/astaxie/goredis](https://github.com/astaxie/goredis)

```
package main

import (
	"fmt"

	"github.com/astaxie/goredis"
)

func main() {
	var client goredis.Client
	// 设置端口为redis默认端口
	client.Addr = "127.0.0.1:6379"
	
	//字符串操作
	client.Set("a", []byte("hello"))
	val, _ := client.Get("a")
	fmt.Println(string(val))
	client.Del("a")

	//list操作
	vals := []string{"a", "b", "c", "d", "e"}
	for _, v := range vals {
		client.Rpush("l", []byte(v))
	}
	dbvals,_ := client.Lrange("l", 0, 4)
	for i, v := range dbvals {
		println(i,":",string(v))
	}
	client.Del("l")
}
```