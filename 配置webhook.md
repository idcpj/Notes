
## 修改php.ini
```bash

	
vim /usr/local/php/etc/php.ini

 #搜索disable_function 将其中的 exec 和 shell_exec 删除。
 


```

## webhook.php
```php
//echo exec('whoami');
$gitroot = "/data/wwwroot/wjdd";
$password = '654321';

$request = file_get_contents('php://input');
//writeLog($request);
$request = json_decode($request,true);
if($request && $request['password'] == $password) {
	switch($request['hook_name']) {
		case 'push_hooks':
			$a=shell_exec("cd $gitroot ;sudo git fetch --all;sudo git reset --hard origin/master");
			break;
	}
}

/**
 * @param str $msg
 */
function writeLog($msg){
	date_default_timezone_set("Asia/Shanghai");
	file_put_contents('log.txt',"\r\n".date("h:i:sa").': '.$msg,FILE_APPEND|LOCK_EX);
}


```