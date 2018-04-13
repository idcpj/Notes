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

### 函数应该只做一件事情


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

###  不要使用单例模式

单例模式是个 反模式。 以下转述 Brian Button 的观点：

1. 单例模式常用于 全局实例， 这么做为什么不好呢？ 因为在你的代码里 你隐藏了应用的依赖关系，而没有通过接口公开依赖2. 关系 。避免全局的东西扩散使用是一种 代码味道.
3. 单例模式违反了 单一责任原则： 依据的事实就是 单例模式自己控制自身的创建和生命周期.
4. 单例模式天生就导致代码紧 耦合。这使得在许多情况下用伪造的数据 难于测试。
5. 单例模式的状态会留存于应用的整个生命周期。 这会对测试产生第二次打击，你只能让被严令需要测试的代码运行不了收场，根本不能进行单元测试。为何？因为每一个单元测试应该彼此独立。

### 封装条件语句

不友好的:
```
if ($article->state === 'published') {
    // ...
}
```
友好的:
```
if ($article->isPublished()) {
    // ...
}
```

### 避免使用条件语句

不好的:
```
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```
好的:
> 这些类可放在同一个文件中,通过取不同的命名空间即可
```
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

## 对象和数据结构

### 使用对象封装
使用对象封装,而不是直接对属性值进行操作
不好的:
```
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

好的:

```
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdraw(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function deposit(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdraw($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

## 类

## 组合优于继承
> 我们应该尽量优先选择组合而不是继承的方式。使用继承和组合都有很多好处。
这个准则的主要意义在于当你本能的使用继承时，试着思考一下组合是否能更好对你的需求建模。

答案依赖于你的问题，当然下面有一些何时继承比组合更好的说明：

你的继承表达了“是一个”而不是“有一个”的关系（例如人类“是”动物，而用户“有”用户详情）。
你可以复用基类的代码（人类可以像动物一样移动）。
你想通过修改基类对所有派生类做全局的修改（当动物移动时，修改它们的能量消耗）。

糟糕的:
```
class Employee {
    private $name;
    private $email;

    public function __construct(string $name, string $email){
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}
// 不好，因为Employees "有" taxdata
// 而EmployeeTaxData不是Employee类型的

class EmployeeTaxData extends Employee {
    private $ssn;
    private $salary;

    public function __construct(string $name, string $email, string $ssn, string $salary){
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

}
```
棒棒哒:
```
class EmployeeTaxData{
    private $ssn;
    private $salary;

    public function __construct(string $ssn, string $salary){
        $this->ssn = $ssn;
        $this->salary = $salary;
    }
}

class Employee{
    private $name;
    private $email;
    private $taxData;

    public function __construct(string $name, string $email)    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(string $ssn, string $salary)    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

}
```

### 避免流式接口

既避免链式调用,
如tp中
`D("dmeo")->where([])->find();`


### 别写重复代码 (DRY)
