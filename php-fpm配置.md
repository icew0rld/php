# php-fpm配置

来自《modern php》的推荐配置（并不能马上使用，需要调整）：

```ini

; 全局配置
emergency_restart_threshold = 10
emergency_restart_interval = 1m

; 进程池配置
user = deploy
group = deploy
listen = 127.0.0.1:9000
listen.allowed_clients = 127.0.0.1
pm.max_children = 51
pm.start_servers = 3
pm.min_spare_servers = 2
pm.max_spare_servers = 4
pm.max_requests = 1000
slowlog = /path/to/slowlog.log
request_slowlog_timeout = 5s

```



-y, --fpm-config <file> 

指定php-fpm.conf 



-t, --test 

测试php-fpm.conf 



[php-fpm配置的官方文档](http://php.net/manual/en/install.fpm.configuration.php)



