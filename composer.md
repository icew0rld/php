#composer

##why

There is a huge trend of reinventing the wheel over and over in the PHP world. The lack of a package manager means that every library author has an incentive not to use any other library, otherwise users end up in dependency hell when they want to install it. A package manager solves that since users do not have to care anymore about what your library depends on, all they need to know is they want to use your stuff. 

Suppose:

a) You have a project that depends on a number of libraries.

b) Some of those libraries depend on other libraries.

Composer:

c) Enables you to declare the libraries you depend on.

d) Finds out which versions of which packages can and need to be installed, and installs them (meaning it downloads them into your project).

Why not use PEAR?

PEAR(PHP Extension and Application Repository)

PEAR 系统级 

PEAR started as a system-wide package manager, much like apt-get or other similar solutions.如果一台机器上有多个php project，不同的project如果依赖同一个库，但不同版本，则PEAR同时安装一个库的不同版本较为不容易。

包的依赖很模糊。

Composer 应用级

依赖包的版本确定
依赖关系明确
依赖包集中在一起

 Another related feature is the composer.lock file that is generated when you install or update dependencies. It stores the exact version of every dependency that was used. If you commit it, anyone checking out the project will be able to install exactly the same versions as you did when you last updated that file, avoiding issues because of minor incompatibilities or regressions in different versions of a dependency. If you ever had bugs appear only on one team member’s machine while the others were fine because of some too-new or too-old version of something, you will know this is very useful.

Composer forces you to declare your project dependencies in a one-stop location(composer.json at the root). You just checkout the code, install dependencies, and they will sit in the project directory, not disturbing anything else on the machine. 

Composer is not a package manager in the same sense as Yum or Apt are. Yes, it deals with "packages" or libraries, but it manages them on a per-project basis, installing them in a directory (e.g. vendor) inside your project. By default it will never install anything globally. Thus, it is a dependency manager.

##what

composer是PHP的包(packages or librarys)依赖管理器。

composer提供了一种标准的格式来管理PHP软件的依赖和所需要的库。

和 node's npm and ruby's bundler是一个概念。

##how(usage)

###installation

Composer offers a convenient installer that you can execute directly from the commandline. The installer is writen by PHP. 用PHP解释器执行该installerPHP脚本便可安装Composer.

可通过网络请求，比如`curl 'url of installer' | PHP` 来执行installer！

`curl -sS https://getcomposer.org/installer | php`

该命令请求installer，抛给PHP执行。执行installer，会check a few PHP settings and then download composer.phar to your working directory.

composer.phar是一个PHP archive， which is an archive format for PHP which can be run on the command line。Now just run `php composer.phar` in order to run Composer.

如果进而`mv composer.phar /usr/local/bin/composer`,便可将composer安装到系统，并且通过`composer`直接运行composer了。

更多安装详情请参考：[installation of composer](https://getcomposer.org/doc/00-intro.md)

###basic usage

- 用composer.json描述project的依赖，以及其他元数据。
- 用`php composer.phar install`安装依赖
- 用`php composer.phar update`更新依赖的版本，`php composer.phar update monolog/monolog [...]`只更新指定依赖。
- 用composer.lock记录所安装的依赖包的版本
- 有一个主要的Composer repository作为package source，可以从中获得package。
- 支持autoloading

在composer.json新增依赖后，运行`php composer.phar install`安装，而不是update。



## 解决require卡住的问题 

[中国全量镜像](https://pkg.phpcomposer.com/)


##ref

- [wiki Composer_(software)](https://en.wikipedia.org/wiki/Composer_(software))
- [composer official site](http://getcomposer.org/)
- [installation of composer](https://getcomposer.org/doc/00-intro.md)
- [Composer: Part 1 – What & Why](http://blog.nelm.io/2011/12/composer-part-1-what-why/)