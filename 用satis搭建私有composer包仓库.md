# 用satis搭建私有composer包仓库

## 安装satis



composer create-project composer/satis --stability=dev --keep-vcs 



cd satis 



\# 定义satis.json



{ 

  "name": "My Repository", 

  "homepage": "http://127.0.0.0:9917", 

  "repositories": [ 

​    { 

​        "type": "vcs", 

​        "url": "http://192.168.4.239/php-package/urlscanner.git" 

​    } 

  ], 

  "require-all": true, 

  "config": { 

​    "secure-http": false 

  } 

} 



Note: 

  

\- secure-http should be false if url is not https 



\# build static web site



php bin/satis build satis.json public 



cd /data/satis/satis/; /application/php7/bin/php bin/satis build satis.json public 



php -S 0.0.0.0:9917 -t public/ 



Note: may change to web server in production 



visit: <http://homestead.app:9917/>, see: 



![satis-repo](satis-repo.png)



\# use package



composer.json: 

{ 

​    "repositories": [ 

​      { "type": "composer", "url": "http://127.0.0.1:9917" } 

​    ], 

​    "require": { 

​        "bluepay/urlscanner": "*", 

​        "monolog/monolog": "^1.23" 

​    }, 

​    "config": { 

​        "secure-http": false 

​    } 

} 



composer update 



index.php: 

<?php 

require 'vendor/autoload.php'; 



$urls = [ 

​        'http://www.baidu.com', 

​        'http://www.apple.com', 

​        'http://www.bad_link.com', 

]; 

$s = new \Looking4soul\UrlScanner\UrlScanner($urls); 

print_r($s->getInvalidUrls()); 



use Monolog\Logger; 

use Monolog\Handler\StreamHandler; 



// create a log channel 

$log = new Logger('name'); 

$log->pushHandler(new StreamHandler('log.log', Logger::WARNING)); 



// add records to the log 

$log->addWarning('Foo'); 

$log->addError('Bar'); 



php index.php 



show:  



output and log.log 



done successfully 



\# issue



a composer package should be tagged 



\# refer



[Handling private packages](<https://getcomposer.org/doc/articles/handling-private-packages-with-satis.md>) 

[使用 satis 搭建一个私有的 Composer 包仓库](<http://www.cnblogs.com/maxincai/p/5308284.html>) 

