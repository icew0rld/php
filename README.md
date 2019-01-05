
# PHP

## 语言

### 基础

[变量](变量.md) [常量](常量.md) [类型](type.md) [运算符](运算符.md) [控制语句](控制语句.md) [函数](函数.md) [引用](引用.md)

### 面向对象

类：

- [类的定义和使用](类的定义和使用.md)

- [静态成员](静态成员.md)
- [继承](继承.md)

- [抽象类](抽象类.md)

- [匿名类](匿名类.md)

[接口](接口.md)

[trait](trait.md)

对象：

- [比较](对象比较.md)
- [复制](对象复制.md)
- [遍历](对象遍历.md)

- [序列化](对象序列化.md)

其他：

- [overloading](重载.md)
- [魔术方法](魔术方法.md)
- [延迟静态绑定](延迟静态绑定.md)

### 错误

[错误处理](错误处理.md) [错误报告](错误报告.md) [异常](异常.md)

### 模块

[标记](标记.md) [文件包含](文件包含.md) [命名空间](命名空间.md)

### 其他

[生成器](生成器.md)

## 库

日志：[monolog](https://packagist.org/packages/monolog/monolog)

关系型数据库：

- [pdo](pdo.md)
- [laravel的eloquent orm](https://laravel.com/docs/5.7/eloquent)

Redis：

- [predis](https://packagist.org/packages/predis/predis): laravel使用的，纯php
- [phpredis](https://github.com/phpredis/phpredis)：c扩展，可能有更好的性能

Http Client: 

- [guzzle](http://docs.guzzlephp.org/en/latest/) 
- curl

Mongodb: [jenssegers/mongodb](https://packagist.org/packages/jenssegers/mongodb):具有Eloquent ORM风格

RabbitMQ: [php-amqplib](https://packagist.org/packages/php-amqplib/php-amqplib)

时间和日期：[carbon](https://packagist.org/packages/nesbot/carbon)

密码：openssl

push: 

- apns
- fcm

模板引擎：

- [blade](blade.md)：来自laravel
- twig：来自Symfony，易用
- smarty: 老，更新不频繁，缺少部分现代特性。最早。

[composer](composer.md)

psr-4：自动加载器

[用satis搭建私有composer包仓库](用satis搭建私有composer包仓库.md)

[PHP官网库列表](http://php.net/manual/zh/funcref.php)

[github awesome php 列表](https://github.com/ziadoz/awesome-php)

[packagist](https://packagist.org/)

## 框架

框架选型目前一般选Laravel，如果对性能有较高需求，可选Laravel的变体Lumen。

- [laravel](laravel.md)
- [yii](yii.md)
- [yaf](yaf.md)

## 开发环境

phpStorm

## 生产

- [运行机制](运行机制.md)
- [php-fpm配置](php-fpm配置.md)
- [php-cgi配置](php-cgi配置.md)

- [nginx配置](nginx配置.md)

## [编码规范](编码规范.md)

## 安全

防止sql注入

- prepare statement

密码机密性

- hash function

xss

csrf

https?

## 单元测试

[phpuint](phpunit.md)

## 分析

Xdebug

XHProf

XHGUI

New Relic

Blackfire

## 管理

[安装php](安装php.md)

## 扩展开发

[扩展开发资料](扩展开发资料.md)

## 有用的资源

官方文档:

- [PHP官方文档中文版](http://php.net/manual/zh/)

- [Laravel官方文档](https://laravel.com/docs)


书:

《modern php》

《深入PHP:面向对象、模式与实践(第3版)》

《Php和Mysql Web开发(原书第4版)》

《PHP核心技术与最佳实践》

《PHP经典实例》

《Head First PHP & MySQL》

《PHP编程》

社区:

- [PHP-FIG framework interop group](php-fig.org)

## todo

- laravel vue / css

