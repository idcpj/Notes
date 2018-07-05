[TOC]

## urllib包
> 是Python3.x中提供的一系列操作URL的库,可以模拟用户使用浏览器访问网页

### 不带请求头实例
     resp = request.urlopen('http://www.baidu.com')
     print(resp.read().decode('utf-8'))
     
### 带请求头
     req = request.Request('http://www.baidu.com')
     req.add_header("User-Agent","Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36")
     resp = request.urlopen(req)
     print(resp.read().decode('utf-8'))
     
### Post带参数
    req = Request('http://www.thsrc.com.tw/tw/TimeTable/SearchResult')
    postData = parse.urlencode([
        ('StartStation', '977abb69-413a-4ccf-a109-0272c24fd490'),
        ('EndStation', '2f940836-cedc-41ef-8e28-c2336ac8fe68'),
        ('SearchDate', '2017/10/06'),
        ('SearchTime', '17:00'),
        ('SearchWay', 'DepartureInMandarin')
    ])
    req.add_header('Origin','http://www.thsrc.com.tw')
    req.add_header("User-Agent","Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36")
    resp = request.urlopen(req,data=postData.encode('utf-8'))
    print(resp.read().decode('utf-8'))