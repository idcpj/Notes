
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