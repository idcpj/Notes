[TOC]
> [参考网站](https://github.com/JingwenTian/awesome-php)

## 验证

### fzaninotto/faker -生成验证数据
`composer requrie fzaninotto/faker`

```
$factory = Factory::create();
echo $factory->name;
echo $factory->city;
echo $factory->email;
```