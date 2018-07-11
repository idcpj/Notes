[TOC]

## 在window 下的配置
### 修改配置
安装好后打开`redis.windows.conf`
```
# 注释 bind 127.0.0.1
#bind 127.0.0.1     

# 模式 改为 no
protected-mode no
```

## 启动
方法一:
`redis-server  redis.windows.conf`

方法二:
创建
`startup.bat ` 写入方法一的脚本 启动