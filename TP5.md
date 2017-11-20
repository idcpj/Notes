[TOC]

## 技巧
>自带.htaccess  无效

修改为: `RewriteRule ^(.*)$ index.php/$1 [QSA,PT,L]  -->  RewriteRule ^(.*)$ index.php?/$1 [QSA,PT,L]`



### 获取请求中的数据  (类 name="id[]" form元素)
```
$this->request->post('tid/a');
```

###  闭包(在闭包中传值)  且模型中用静态方法
```php
public static function getLoan($where=array(),$page=0,$sizePage=10,$order=''){
    $list  = LoanModel::all(function($query) use($where,$page,$sizePage,$order){
        $query->where($where)->page($page,$sizePage)->field('id,name,img,min_money,max_money,loan_rate,tip');
        if(!empty($order)){
            $query->order($order);
        }

    });
}
```
### 自定义不存在的字段
```
//$data 为该条记录数组
public function getLoanRateAttr($value,$data){
		$loan = LoanModel::get($data['id']);
		$value = "参考".$loan['time_type']."利率:  ".strval($value)."%";
		return  $value;
}
```

### 更个别新字段
```
$loan = LoanModel::get($id);
$loan->show_app = $loan->getData('show_app')==1?0:1;
$loan->save();
```

### 获取原始数据
```php
$user = User::get(1);
// 获取原始字段数据
echo $user->getData('status');
// 获取全部原始数据
dump($user->getData());
```

### 查询某条记录的某个值  
```
//使用 ->value
$loanTypeId = LoanTypeModel::where(['name' => $loanTypeId])->value('id');
//返回  3
```
### 带条件分页
```
$loanData = LoanModel::where($where)->paginate(10,false,[
    'query'=>$this->request->param(),
]);
```


### 目录结构
![配置目录格式](images/371400619-581858ef3ed37_articlex.png)




## 安装
### git 安装
```
git clone --depth=1 https://github.com/top-think/think.git think_git
cd think_git
git clone --depth=1 https://github.com/top-think/framework.git thinkphp 
```
### composer 安装
```
composer create-project --prefer-dist topthink/think think_composer
```

## 配置
### 扩展配置
在`config/extra/email.php`,写入配置参数email会被当作建名.
```php
//例子:  创建db.php
config/extra/databases.php
    return array(
        //code
);
```
### 场景配置
在`config/extra/config.php` 或 `app`中 的`config.php`中
配置  `'app_status'             => 'office'`,
创建`config/extra/office.php`   和`config/extra/home.php`
调节`app_status`的值`office`或`home`的参数.选择不同配置.
在不同场景下 databases 的设置不同

## 路由
**在新建的config/config.php中开启路由**
```
// 是否开启路由
'url_route_on'           => true,
// 是否强制使用路由
'url_route_must'         => false,
```

**在新建config/route.php**
```php
//route.php
    return array(
    'news/:id/:age' =>'index/index/demo',  
);
//控制器中
public function demo($id,$age)
{
    return "id:{$id} age:{$age} ";
}
//访问地址
http://www.tp5.com/news/5/10
//生成url
在配置了路由规则后
echo url('index/index/demo',['id'=>5,'age'=>10]);  //news/5.html
```
## 视图
### 模版位置
默认路径,在index模块下
```
view/index/index.html
return  view();
```
### 四种赋值总结
```php
1. $this->assign('key', 'value');
2. $this->view-> keyname = 'value';
3. return $this->fetch('html模板名', [
       'key'   => 'value',
       'key2' => 'value2'
]);
4. View::share('key', 'value'); # 使用该方法必须先 use think\View;
```

### 配置文件
```php
'view_replace_str'=>[
    '__123__'=>'一二三',
]

#在模版中
<h3>__123__</h3>  			#输出为一二三
```
```php
#官方自带
<h3>__URL__</h3>  			#输出/index/index
<h3>__STATIC__</h3> 	    #输出/static
<h3>__CSS__</h3>  			#输出  /static/css
<h3>__JS__</h3>  			#输出  /static/js
```

## 静态增删改查操作

### 增
```
$user = User::create([
    'name'  =>  'thinkphp',
    'email' =>  'thinkphp@qq.com'
]);
echo $user->email;
echo $user->id; // 获取自增ID
```
### 删
#### 根据主键删除
```
User::destroy(1);
//或
User::destroy([1,2,3]);
```
#### 条件删除
```
User::destroy(['status' => 0]);
//或
User::where('id','>',10)->delete();
```

### 改

#### 查找并更新 
```
$user = User::get(1);
$user->name     = 'thinkphp';
$user->save();
```

#### 直接更新数据
```
User::update(['id' => 1, 'name' => 'thinkphp']);
```
### 复杂界面更新
```
User::where(['status'=>1,'name'=>'cpj'])->update(['name' => 'thinkphp']);
```

### 查
#### 获取单个数据
```
$user = User::get(1);
echo $user->name;

// 使用数组查询
$user = User::get(['name' => 'thinkphp']);

// 使用闭包查询
$user = User::get(function($query){
    $query->where('name', 'thinkphp');
});
echo $user->name;
```

#### 获取多个数据
```
// 或者使用数组
$list = User::all([1,2,3]);

// 使用条件查询(只能对where操作)
$list = User::all(['status'=>1]);

//闭包 比条件查找强大
$list = User::all(function($query){
    $query->where('status', 1)->limit(3)->order('id', 'asc');
});
```

### 一对一关联
#### 隐藏关联的数组,绑定父元素 加别名
```
//模型中方法,注意使用return进行
public function Reloan(){
    //外键id  reloanModel 的外键id
    return $this->hasOne('ReloanModel','lid')->bind('tid');  //->bind('username'=>'name')  把name改为username
}
//调用
LoanModel::get(8,'reloan')->hidden(['reloan'])     //hidden 先用bind绑定到父类 然后用hidden 隐藏关联表
LoanModel::all(8,'reloan')->hidden(['reloan','users'])
```
####  更新关联表
```
$loan = LoanModel::get(8);
$loan->reloan->tid=12;
$loan->reloan->save();
```