#类型

## 动态弱类型

动态类型

- 变量不需要声明其所属的类型
- 编译时不检查类型错误，运行时检测

```php
$a = 1; //变量不需要声明其所属的类型
function f($a) { //编译时不检查类型错误，运行时检测
    strlen($a);
}
f($a);
```

弱类型

- 变量的类型随其值的类型的改变而改变
- 可以在不同类型之间进行隐式类型转换

```php
$a = 1;
echo gettype($a);//int
$a = 1.1;//变量的类型随其值的类型的改变而改变
echo gettype($a);//float

$b = 1;
$c = $a + $b;//可以在不同类型之间进行隐式类型转换：$b被转化为float后参与计算
```

详见：[类型系统](./类型系统.md)

## 类型

标量类型：

- [boolean](boolean.md)
- [int](int.md)
- [float](float.md)
- [string](string.md)

复合类型：

- [array](array.md)
- [object](object.md)

特殊类型：

- [null](null.md)
- [resource](resource.md)

回调类型：

- [callable](callable.md)

## 类型转换

- [类型转换](类型转换.md)

## 类型相关函数

- [类型相关函数](../../function/类型相关函数.md)
