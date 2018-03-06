[TOC]


## 定时备份

如果 `php /data/www/demo/index.php  app sendApi cron`  无法备份,
可以使用访问地址的形式 `curl  http://www.demo.com/app/sendapi/cron`

使用命令备份时,需要注意的地方.
1. 文件权限是否限制
2. 如果php输出地方为相对路径,则保存的地方在 服务器 cd ~ 目录下,所以务必使用 绝对路径