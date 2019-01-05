\# 资料 



[pecl](<http://pecl.php.net/package/yaf>) 

[github](<https://github.com/laruence/yaf>) 

[php.net manual](<http://php.net/manual/en/book.yaf.php>) 

[Yaf(Yet Another Framework)用户手册](<http://www.laruence.com/manual/>) 

[Yaf (Yet Another Framework)](<http://www.yafdev.com/>) 

[鸟哥博客yaf标签](<http://www.laruence.com/tag/yaf>) 



\## 性能 

[02 Dec 11 Yaf 2.1性能测试(Yaf 2.1 Benchmark)](<http://www.laruence.com/2011/12/02/2333.html>) 

[1.4. Yaf的性能](<http://www.laruence.com/manual/yaf.bench.html>) 



\## quickstart 



[github readme](<https://github.com/laruence/yaf>) 



[Examples](<http://php.net/manual/en/yaf.tutorials.php>) 



[第 3 章 快速开始](<http://www.laruence.com/manual/yaf.tutorial.html>) 



\# 安装 



最新yaf3.0.4依赖php7，先编译安装php7 



然后pecl install yaf 



然后再php.ini中加入extension=yaf.so 



然后重启php 



DONE 



\# quickstart 



见任意一个quickstart中的参考，文档有稍微不一致，参考第一个即可 



\# 配置 

yaf runtime配置 

<http://php.net/manual/en/yaf.configuration.php>



yaf 应用配置 

<http://php.net/manual/en/yaf.appconfig.php>

<http://www.laruence.com/manual/yaf.config.optional.html>



\# 自动加载器 

<http://www.laruence.com/manual/yaf.autoloader.html>

<http://php.net/manual/en/class.yaf-loader.php>



[spl_autoload_register](<http://php.net/manual/zh/function.spl-autoload-register.php>) 

[类的自动加载](<http://php.net/manual/zh/language.oop5.autoload.php>) 



框架相关的MVC类：类名-映射到-目录 

非框架MVC相关的类：产品之间共享的类，yaf runtime配置yaf.library 

非框架MVC相关的类：产品自身的类，yaf 应用配置application.library，在Yaf_Loader的registerLocalNamespace方法注册的前缀将在application.library中找，否则在yaf.library中找 



而类的加载规则, 都是一样的: Yaf规定类名中必须包含路径信息, 也就是以下划线"_"分割的目录信息.（MVC类也是） 

现在可以使用命名空间代替_。 



\# bootstrap 

app运行之前，做一些全局的初始化工作 

比如： 

  public function _initLoader($dispatcher) { 

​       Yaf_Loader::getInstance()->registerLocalNameSpace(array("Foo", "Bar")); 

  } 



\# 插件 



实现6个Hook的方法。 

多个插件按注册顺序调用 

<http://www.laruence.com/manual/yaf.plugin.html>

<http://php.net/manual/en/class.yaf-plugin-abstract.php>



\# 路由 



url语法 

<schema>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag> 

一般没有<user>:<password>@, #<frag> 

query_string一般指<query> 

request_uri一般指<port>后的斜杠开始到url结束的部分 



http报文 

GET uri HTTP/1.1 

Host: xxx 

其中uri基本等同于request_uri，get参数放在这里 

POST参数放在Body里，编码格式和Content-Type有关 



所谓路由 

PHP框架里的所谓路由，是request_uri到函数的映射方式的定义。函数在yaf里是某module的某controller的某action方法。 



yaf路由使用 

​     实例化：实例化6种内置路由方式类，或先自定义路由类，再实例化这个类。可在配置文件或bootstrap中进行。 

​     注册：注册路由类实例。 

​     默认路由：默认路由无需实例化和注册，自动完成 

​     顺序：注册的倒序调用（这里坑爹），失败会调用下一个 

​      

yaf的6种内置路由方式 

​     默认的：static: /base_uri/module/controller/action/key/value 

​     simple: ?m=x&c=x&a=x 

​     supervar:?r=m/c/a 

​     map: /foo/bar直接变成foo_bar action 

​     rewrite：/product/value 在路由类实例中指定controller、action，有点像restful api 

​     regex：/product/value，和rewrite类似，不过可以做正则匹配 



​     默认值：base_uri, modules, 默认module、controller、action都可在yaf application配置中配置 

​      

yaf自定义路由 

​     继承Yaf_Route_Interface 

​     <http://php.net/manual/en/class.yaf-route-interface.php> 



\# 配置 

Yaf_Application::app()->getConfig()返回Yaf_Config_Ini对象，由Yaf_Appliaction初始化传入的配置初始化。 



Yaf_Config_Abstract 

​     Yaf_Config_Ini：主要使用 

​     Yaf_Config_Simple：和ini几乎一样，只差构造函数是array 



通过Yaf_Registry在Bootstrap中注册Yaf_Config_Ini，后续可用Yaf_Registry::get()访问参数。 



\# 控制器 

请求 

​     $r =Yaf_Application::app()->getDispatcher()->getRequest(),更好：Yaf_Controller_Abstract::getRequest 

​      [Yaf_Request_Abstract](http://php.net/manual/zh/class.yaf-request-abstract.php) 

​      [Yaf_Request_Http](http://php.net/manual/zh/class.yaf-request-http.php)  

响应 

​     Yaf_Response_Abstract 

​     Yaf_Response_Http 

​     设置会自动echo 

​     

\# 模型 

yaf的model只是一个普通类，没有提供任何数据库相关的功能，比如querybuilder、orm等，都没有。 



\# 视图 

​     模板引擎没有自己的语法，就是php本身 

​     controller中返回false将关闭视图自动渲染 



\# 错误 

​     支持异常和错误 

​     定义类内置的异常类 

​     优雅写法：要捕获所有异常，通过注册异常处理函数 

\# 其他 