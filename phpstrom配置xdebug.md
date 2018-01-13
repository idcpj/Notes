[TOC]

## 安装xdebug

```
brew install php55-xdebug
```

在`/usr/local/etc/php/5.5/conf.d/ext-xdebug.ini`

```
[xdebug]
zend_extension=/usr/local/Cellar/php55-xdebug/2.5.5/xdebug.so
xdebug.remote_autostart=on
xdebug.remote_enable=on
xdebug.remote_enable=1
xdebug.remote_mode="req"
xdebug.remote_log="/var/log/xdebug.log"
xdebug.remote_port=9000
xdebug.remote_handler="dbgp"
xdebug.idekey="PhpStorm"
```