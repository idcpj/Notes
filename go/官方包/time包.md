[TOC]

## time.Ticker 间隔执行功能
每3秒输出 hello word
```
type hello struct {
	say    string
	ticker *time.Ticker
}

func NewHello(interval time.Duration, say string) *hello {
	return &hello{
		say:    say,
		ticker: time.NewTicker(interval * time.Second),
	}
}

func (h *hello) start() {
	for {
		select {
		case <-h.ticker.C:
			fmt.Println(h.say)
		}
	}
}

func main() {
	// 每个3秒输出一个 hello word
	h := NewHello(3, "hello word")
	h.start()
}
```