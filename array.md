#数组(array)

##取值

array是PHP中非常常用的一个类型。

PHP的array是一个有序映射(ordered map)，每个元素由key和value对构成。

key的类型只能是int或string，而value的可以是任意类型，即可以是PHP定义的所有8种类型，包括array、object、null、resouce等。

可见数组是一种复合类型(compound)，即它是由其他类型的元素构成的。

创建一个array，需要注意：

- key 会有如下的强制转换
	- 包含有合法整型值的字符串会被转换为整型。例如键名 "8" 实际会被储存为 8。但是 "08" 则不会强制转换，因为其不是一个合法的十进制数值。
	- 浮点数也会被转换为整型，意味着其小数部分会被舍去。例如键名 8.7 实际会被储存为 8。
	- 布尔值也会被转换成整型。即键名 true 实际会被储存为 1 而键名 false 会被储存为 0。
	- Null 会被转换为空字符串，即键名 null 实际会被储存为 ""。
	- 数组和对象不能被用为键名。坚持这么做会导致警告：Illegal offset type。
- 如果在数组定义中多个单元都使用了同一个键名，则只使用了最后一个，之前的都被覆盖了。
- 如果对给出的值没有指定键名，则取当前最大的整数索引值，而新的键名将是该值加一。
- 可以只对某些单元指定键名而对其它的空置。

##运算

数组元素访问符`[]`:
- 方括号和花括号可以互换使用来访问数组单元.
- 自 PHP 5.4 起可以用数组间接引用函数或方法调用的结果。之前只能通过一个临时变量:

```
function getArray() {
    return array(1, 2, 3);
}

// on PHP 5.4
$secondElement = getArray()[1];
```
- 试图访问一个未定义的数组键名与访问任何未定义变量一样：会导致 E_NOTICE 级别错误信息，其结果为 NULL。
- 如果给出方括号但没有指定键名，则取当前最大整数索引值，新的键名将是该值加上 1（但是最小为 0）。如果当前还没有整数索引，则键名将为 0。
- 应该始终在用字符串表示的数组索引上加上引号。



# 数组处理函数

数组处理函数的完整列表参见：[数组处理函数][1]

以下介绍一些常用的函数。

## 求数组元素个数

```
int count ( mixed $var [, int $mode = COUNT_NORMAL ] )
$size = count(array(1, 2, 3));
echo $size;//output:3
```

## 拼接多个数组

```
array array_merge ( array $array1 [, array $... ] )

$a = array(1 => "a", 2 => "b");
$b = array(1 => "c", 3 => "d");

$c = array_merge($a, $b);//int key被从新索引
var_dump($c);

/*output:
array(4) {
  [0]=>
  string(1) "a"
  [1]=>
  string(1) "b"
  [2]=>
  string(1) "c"
  [3]=>
  string(1) "d"
}
*/

$d = array_merge($a, null);//产生warning类型错误，输出null
var_dump($d);

/*output:
NULL
PHP Warning:  array_merge(): Argument #2 is not an array in /home/Jf3bFP/prog.php on line 11
*/

$e = $a + $b;//int key保持不变，重复key的元素被忽略
var_dump($e);
/*
array(3) {
  [1]=>
  string(1) "a"
  [2]=>
  string(1) "b"
  [3]=>
  string(1) "d"
}
*/

$a = array("a" => "a", "b" => "b");
$b = array("a" => "c", "d" => "d");

$c = array_merge($a, $b);//string key的元素被覆盖
var_dump($c);

/*output:
array(3) {
  ["a"]=>
  string(1) "c"
  ["b"]=>
  string(1) "b"
  ["d"]=>
  string(1) "d"
}
*/
```

## 判断元素是否在数组中

检查给定的key是否存在于数组中:

```
bool array_key_exists ( mixed $key , array $search )

$search_array = array('1' => null, '2' => 4);

// returns true
array_key_exists('1', $search_array);
// returns true
array_key_exists(1, $search_array);
```

​	

```
// 对比isset, returns false
isset($search_array['1']);
```

检查给定的value是否在数组中:

```
bool in_array ( mixed $needle , array $haystack [, bool $strict = FALSE ] )

$a = array(array('p', 'h'), array('p', 'r'), 'o');
echo in_array(array('p', 'h'), $a);//output:true
```

[1]: http://php.net/manual/zh/ref.array.php