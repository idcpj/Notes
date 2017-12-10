	
    
    
## 解除对sudo对限制
`El Capitan` 加入了`Rootless`机制

重启按住 Command+R，进入恢复模式，打开Terminal。

`csrutil disable`

重启即可。如果要恢复默认，那么

`csrutil enable`