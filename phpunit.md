#phpunit

##why unit test

good things

- 测试优先的思想，使程序可测试、强制解耦

- 单元改动后进行回归，改动可能因为：1. 功能改动 2.debug 3.重构

- 展示函数或类如何使用的最佳文档

bad things

- 你需要开发它单测代码，而这些代码并不运行于实际产品之中。特别是当代码修改时，单测的代码也要跟着同步修改，这对于工期来说，是个负担！


##what is phpunit

phpunit是php的单元测试框架

它是在PHP5下面对JUnit3系列版本的完整移植，是xUnit测试框架家族的一员(它们都基于模式先锋Kent Beck的设计)。

注：Kent Beck:是软件开发方法学的泰山北斗，是最早研究软件开发的模式和重构的人之一，是敏捷开发的开创者之一，更是极限编程和测试驱动开发的创始人，同时还是JUnit的作者，对当今世界的软件开发影响深远。

##how to use phpunit

###basic usage

####install

phpunit以phar（php achive）提供，下载后，赋予可执行权限，再放到$PATH路径，即安装完毕，可在命令行中执行。

更多请参考：

- [install ref](https://phpunit.de/getting-started.html)

####basic example

dir_root/src/Money.php

```
<?php
class Money
{
    private $amount;

    public function __construct($amount)
    {
        $this->amount = $amount;
    }

    public function getAmount()
    {
        return $this->amount;
    }

    public function negate()
    {
        return new Money(-1 * $this->amount);
    }

    // ...
}
```

dir_root/tests/MoneyTest.php

```
<?php
include dirname(__FILE__) . '/../src/Money.php';
class MoneyTest extends PHPUnit_Framework_TestCase
{
    // ...

    public function testCanBeNegated()
    {
        // Arrange
        $a = new Money(1);

        // Act
        $b = $a->negate();

        // Assert
        $this->assertEquals(-1, $b->getAmount());
    }

    // ...
}
```

runing test:

```
phpunit tests/MoneyTest
```
output:

```
PHPUnit 5.1.3 by Sebastian Bergmann and contributors.

.                                                                   1 / 1 (100%)

Time: 112 ms, Memory: 10.25Mb

OK (1 test, 1 assertion)
```

####some more basic things

- test

xxTest类中的一个testXx方法算一个test

- assertions

	- assertEquals($arg1, $arg2): 判等(不包括类型，但如果其中一个变量是数值零，无论整数还是浮点数，另一个变量是字符串，那么会同时比较变量的类型，换言之，会用 === 比较操作符，而不是普通的 == 比较操作符)，常用，几乎是最常用的assertion
	- assertInstanceOf($arg1, $arg2): 判断$arg2是不是string $arg1指定的类型
	- assertSame($arg1, $arg2)：判等，包括值和类型
	- assertTrue($arg1):判断参数是否为true（包括类型必须为bool，比如1就不通过）

所有assert函数的参数列表最后都可以跟一个message参数，默认为空字符串。

see more assertion methods: [assertions](https://phpunit.de/manual/current/zh_cn/appendixes.assertions.html)

- exceptions

采用@expectedException 标注来测试被测代码中是否抛出了异常。

更多异常测试方式参见：[exceptions](https://phpunit.de/manual/current/zh_cn/writing-tests-for-phpunit.html#writing-tests-for-phpunit.exceptions.examples.ExceptionTest.php)

- read the whole example of Money and MoneyTest in site of phpunit, **you can learn how to write test cases more than you expected**

	- [Money](https://github.com/sebastianbergmann/money/blob/master/src/Money.php)

	- [MoneyTest](https://github.com/sebastianbergmann/money/blob/master/tests/MoneyTest.php)

- 常用标注

	- @covers: 指明测试方法想要对哪些方法进行测试
	- @uses: 用来指明那些将会在测试中执行到但同时又不打算让其被测试所覆盖的代码。在对代码单元进行测试时所必须的值对象就是个很好的例子。
	- @expectedException: 指明测试被测代码中是否抛出了异常。
	- @depends：指定本测试方法依赖的其他测试方法。
	
- 测试依赖

方法间的依赖关系允许生产者(producer)返回一个测试基境(fixture)的实例，并将此实例传递给依赖于它的消费者(consumer)们。

一个方法所依赖的测试方法没有通过测试，则这个方法会被跳过(skipped).

[to be continue 20160108]


- fixture

在编写测试时，最费时的部分之一是编写代码来将整个场景设置成某个已知的状态，并在测试结束后将其复原到初始状态。这个已知的状态称为测试的 基境(fixture)。

基境(fixture)是对开始执行某个测试时应用程序和数据库所处初始状态的描述。

PHPUnit 支持共享建立基境的代码。在运行某个测试方法前，会调用一个名叫 setUp() 的模板方法。setUp() 是创建测试所用对象的地方。当测试方法运行结束后，不管是成功还是失败，都会调用另外一个名叫 tearDown() 的模板方法。tearDown() 是清理测试所用对象的地方。

测试类的每个测试方法都会运行一次 setUp() 和 tearDown() 模板方法（同时，每个测试方法都是在一个全新的测试类实例上运行的）。

另外，setUpBeforeClass() 与 tearDownAfterClass() 模板方法将分别在测试用例类的第一个测试运行之前和测试用例类的最后一个测试运行之后调用。

支持在每个测试前备份和在测试后恢复全局变量和类静态变量。see:[how to backup and recover globals and static member variable](https://phpunit.de/manual/current/zh_cn/appendixes.annotations.html#appendixes.annotations.backupGlobals)

- db

DbUnit 扩展大大简化了为测试设置数据库的操作，并且可以在对数据执行了一系列操作之后验证数据库的内容。

提供数据集（dataset）抽象，比较从数据库和从文件构造的dataset之间的异同来进行测试。

[对包含数据库的逻辑进行测试的难题和简化方法](https://phpunit.de/manual/current/zh_cn/database.html)

- autoload

运行`phpunit --bootstrap autoload.php tests/MoneyTest`指定autoload注册函数所在文件，则可以不在xxTest.php中include类文件。
autoload.php示例：
```
<?

spl_autoload_register(function ($class) {
    include dirname(__FILE__) . '/src/' . $class . '.php';
});
```

- run all tests

`phpunit tests`

Using tests instead of tests/MoneyTest would instruct the PHPUnit command-line test runner to execute all tests found declared in *Test.php sourcecode files in the tests directory.

###advanced usage

####stubs

####代码覆盖率分析

####logging

####advanced features

####with xdebug

####with phing

####with selenium

##ref

- [phpunit百度百科](http://baike.baidu.com/link?url=lVntk2c_hQWzja3RYePP410VY7GyYCs0vcJ5NxxxheHaL86zd3oqaajvTkPoQQRTpsczTNlPUT2KxuKNw7r68_)
- [phpunit官网](https://phpunit.de/)