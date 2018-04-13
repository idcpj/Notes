[TOC]

> [参考网址]( https://laravel-china.org/topics/7774/the-conciseness-of-the-php-code-php-clean-code)

> PHP版本>7.1.*


## 变量

### 数字可读

不好：
```
// 见鬼的 4 又是什么意思？
if ($user->access & 4) {
    // ...
}
```
好：
```
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```

### 正则
一般：
```
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

list(, $city, $zipCode) = $matches;
saveCityZipCode($city, $zipCode);
```
很棒：

```
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(?<city>.+?)\s*(?<zipCode>\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

### 避免嵌套太深
写执行报错

不好：
```
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```
很棒：
```
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n > 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```
### 避免心理映射
不好：
```
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```
很棒：

```
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

### 不要增加不需要的上下文
小坏坏：
```
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```
好的方式：
```
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

### 使用默认参数而不是使用短路运算或者是条件判断
不好的做法:

**这是不太好的因为 $breweryName 可以是 NULL.**
```
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```
好的做法:

 类型提示 而且可以**保证 $breweryName 不会为空 NULL.**
```
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```
## 函数

### 函数参数（2 个或更少）

不友好的:
```
function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
{
    // ...
}
```
友好的:
把多个参数变为 对象传入

```
//----------*创建对象*-------//
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

//----------*实例化对象*-------//
$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

//----------*闯入对象*-------//
function createMenu(MenuConfig $config): void
{
    // ...
}
```

## 函数应该只做一件事情


不好的:
```
function emailClients(array $clients): void
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

好的:
```
function emailClients(array $clients): void
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients(array $clients): array
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive(int $client): bool
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```