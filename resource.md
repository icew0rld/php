#资源类型(resource)

##取值

资源 resource 是一种特殊变量，保存了到外部资源的一个引用。

##资源类型示例
- curl：由curl_init()创建，被curl_*()函数使用，被curl_close()销毁。
- ftp：由ftp_connect()创建，被ftp_*()函数使用，被ftp_close()销毁。
- mysql link:由mysql_connect()创建，被mysql_*()函数使用，被mysql_close()销毁。

##销毁

由于 PHP 4 Zend 引擎引进了引用计数系统，可以自动检测到一个资源不再被引用了（和 Java 一样）。这种情况下此资源使用的所有外部资源都会被垃圾回收系统释放。因此，很少需要手工释放内存。但持久数据库连接比较特殊，它们不会被垃圾回收系统销毁。

是否需要调用资源的销毁函数（一般为xxclose)依不同的资源而定，比如curl资源就需要调用curl_close()来销毁资源，而COM资源就不需要。