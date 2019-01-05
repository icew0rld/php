#回调类型(callable)

#取值

callable指能够被调用的语言结构，包括函数、对象方法、静态方法、closure、匿名函数等。

#调用

PHP中，通过给函数传递callable的string类型的名字来调用callable结构，比如用string表示的函数名、对象方法名和静态方法名。具体格式：

- 普通函数直接使用其名字。
- 一个已实例化的对象的方法被作为数组传递，下标 0 包含该对象，下标 1 包含方法名。
- 静态类方法也可不经实例化该类的对象而传递，只要在下标 0 中包含类名而不是对象。自 PHP 5.2.3 起，也可以传递 'ClassName::methodName'。

注意事项：
- 合法的回调类型包括任何内置或用户自定义函数，但除了语言结构例如：array()，echo，empty()，eval()，exit()，isset()，list()，print 和 unset()。
- 除了普通的用户自定义函数外，create_function() 可以用来创建一个匿名回调函数。自 PHP 5.3.0 起也可传递 closure 给回调参数。

示例：

```
// An example callback function
function my_callback_function() {
    echo 'hello world!';
}

// Type 1: Simple callback
call_user_func('my_callback_function');

// An example callback method
class MyClass {
    static function myCallbackMethod() {
        echo 'Hello World!';
    }
} 

// Type 2: Static class method call
call_user_func(array('MyClass', 'myCallbackMethod')); 

// Type 3: Object method call
$obj = new MyClass();
call_user_func(array($obj, 'myCallbackMethod'));

// Type 4: Static class method call (As of PHP 5.2.3)
call_user_func('MyClass::myCallbackMethod');

// Type 5: Relative static class method call (As of PHP 5.3.0)
class A {
    public static function who() {
        echo "A\n";
    }
}

class B extends A {
    public static function who() {
        echo "B\n";
    }
}

call_user_func(array('B', 'parent::who')); // A


// Our closure
$double = function($a) {
    return $a * 2;
};

// This is our range of numbers
$numbers = range(1, 5);

// Use the closure as a callback here to 
// double the size of each element in our 
// range
$new_numbers = array_map($double, $numbers);

print implode(' ', $new_numbers);

```

