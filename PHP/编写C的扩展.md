[TOC]

> [简书参考](https://www.jianshu.com/p/24449949e945)
> [鸟哥参考](http://www.laruence.com/2009/04/28/719.html)
> [php7 的扩展](https://segmentfault.com/a/1190000007575322)

## 下载php源码包
如: http://php.net/get/php-5.6.1.tar.bz2/from/a/mirror

以下内容属于php5.6
 
进入php的`ext` 目录,执行
`./ext_skel --extname=demo_name`


## 编写具体代码
1. `config.m4`
```
//修改成如下
PHP_ARG_WITH(hello, for hello support,

[ --with-hello Include hello support])
```

2.  ` php_demo_name.h`
```c
PHP_FUNCTION(hello);  //在.h 的头文件声明你要是实现的函数名
```

3.  `demo_name.c`

```
//在中间插入你的函数名
const zend_function_entry dmeo_functions[] = {
    PHP_FE(confirm_dmeo_compiled, NULL)
    PHP_FE(hello,	NULL)		/*此处是自己添加的 */
    PHP_FE_END
};


//文件最后,加上具体实现
PHP_FUNCTION(hello) {
    php_printf("Hello World!\n");
    RETURN_TRUE;
}
```

4. 编译安装
```
> phpize
> ./configure --with-php-config=/you/ath/bin/php-config
> make
> sudo make install
> php -r"demo_name();";
```
> 如果没有效果 可以重启`php-fpm`

## 分析某个自定义函数
```
PHP_FUNCTION(self_concat){
 
    char *str = NULL;

    int argc = ZEND_NUM_ARGS();

    int str_len;

    long n;

    if (zend_parse_parameters(argc TSRMLS_CC, "sl", &str, &str_len, &n) == FAILURE)

    return;

    php_error(E_WARNING, "self_concat: not yet implemented");
 
}
```
```
zend_parse_parameters(int num_args TSRMLS_DC, char *type_spec, …);

参数:
int num_args	传递给函数的参数个数,通常做法是`ZEND_NUM_ARGS()` 来确定传递参数个数

TSRMLS_DC 		为了线程安全

char *type_spec	 指定了函数期望的参数类型,例子中 是"sl",定义的函数接受的每次参数都需要定义类型

                    类型指定符	对应的C类型		描述
                    l			long			符号整数
                    d			double			浮点数
                    s			char *, int		二进制字符串，长度
                    b			zend_bool		逻辑型（1或0）
                    r			zval *			资源（文件指针，数据库连接等）
                    a			zval *			联合数组
                    o			zval *			任何类型的对象
                    O			zval *			指定类型的对象。需要提供目标对象的类类型
                    z			zval *			无任何操作的zval


```

## 函数返回值
|设置返回值并且结束函数 |			设置返回值 |		宏返回类型和参数 |
|---|---|---|
|RETURN_LONG(l)	| RETVAL_LONG(l) |	整数 |
|RETURN_BOOL(b)	| RETVAL_BOOL(b) | 	布尔数(1或0)| 
|RETURN_NULL()|	RETVAL_NULL()	|NULL
|RETURN_DOUBLE(d)	|RETVAL_DOUBLE(d)	|浮点数|
|RETURN_STRING(s, dup)|	RETVAL_STRING(s, dup)	|字符串。如果dup为1，引擎会调用estrdup()重复s，使用拷贝。如果dup为0，就使用s|
|RETURN_STRINGL(s, l, dup)	|RETVAL_STRINGL(s, l, dup)	|长度为l的字符串值。与上一个宏一样，但因为s的长度被指定，所以速度更快。|
|RETURN_TRUE	|RETVAL_TRUE	|返回布尔值true。注意到这个宏没有括号。|
|RETURN_FALSE|	RETVAL_FALSE	|返回布尔值false。注意到这个宏没有括号。|
|RETURN_RESOURCE(r) | 	RETVAL_RESOURCE(r) |	资源句柄。|


