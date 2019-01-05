#对象(object)

#取值

PHP支持面向对象，object是类(class)的实例。

对象也是复合类型，它的由各种类型的属性组合而成。

新建对象用`new`关键字，示例如下：

```
class foo
{
    function do_foo()
    {
        echo "Doing foo."; 
    }
}

$bar = new foo;
$bar->do_foo();
```