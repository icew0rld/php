#trait

自 PHP 5.4.0 起，PHP 实现了trait。

trait是为了解决单继承的不足而被设计的。

trait是一个方法、属性的集合，自身不可以被实例化，但可以被类使用(通过关键词use)，而使类具有trait中的属性和方法。

语法示例：

```
trait A{

	public $b = 'b';
	private $c = 'c';
	public static $d = 'd';
	
	public function f1(){
		echo $this->c;
	}	

	private function f2(){
		echo $this->b;
	}
	
	public static function f4(){
		echo self::$d;
	}
}

class B{
	use A;
	public function f3(){
		$this->f2();
	}
}

$b = new B();
$b->f1();//output:c
$b->f3();//output:b
echo $b->b;//output:b
B::f4();//output:d
```

注意：

- 如果有同名方法，自当前类的成员覆盖了 trait 的方法，而 trait 则覆盖了被继承的方法。（如果 trait 定义了一个属性，那类将不能定义同样名称的属性，否则会产生一个错误。）
- 通过逗号分隔，在 use 声明列出多个 trait，可以都插入到一个类中。
- 当多个trait中的成员有名字冲突时，必须使用instanceof和as来解决冲突。示例：

```
trait A {
    public function smallTalk() {
        echo 'a';
    }
    public function bigTalk() {
        echo 'A';
    }
}

trait B {
    public function smallTalk() {
        echo 'b';
    }
    public function bigTalk() {
        echo 'B';
    }
}

class Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
        B::bigTalk as talk;
    }
}

$t = new Talker();
$t->smallTalk();//output:b
$t->bigTalk();//output:A
$t->talk();//output:B
```

- as还可以用来调整方法的访问控制。
- 正如类能够使用 trait 一样，其它 trait 也能够使用 trait。
- trait 支持抽象方法。
- trait可以支持静态属性和静态方法。

