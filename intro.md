# Padrino简介


## 相关链接

[Padrino官网](http://www.padrinorb.com/ "Padrino web framework")

[Padrino项目主页](https://github.com/padrino/padrino-framework "Padrino project @GitHub")

[Sinatra官网](http://www.sinatrarb.com/ "Sinatra web framework")


## Padrino是什么

Padrino是用Ruby语言开发的、基于Sinatra的Web开发框架。

截至2014年11月4日，Padrino的最新版本是`0.12.4`。


## 为什么要选择Padrino

相比Rails，Padrino要更加简单，这不仅使学习成本更低，在大多数场景下还具有更好的性能。和Sinatra相比，Padrino同样简洁、易用，同时具有更加完善的功能，更适合Web开发的需要。

在坚持Sinatra核心理念的同时，Padrino提供了一系列工具、helper和函数库，从而具有了上述优势。


## Padrino比Sinatra多了哪些功能

* `Agnostic`

* `Generators`

* `Mountable`

* `Routing`

* `Tag Helpers`

* `Asset Helpers`

* `Form Helpers`

* `Text Helpers`

* `Mailer`

* `Caching`

* `Admin`

* `Logging`

* `Reloading`

* `Localization`


## 如何安装Padrino

    $ gem install padrino --verbose --no-ri

注：

1. `--verbose`显示安装过程的具体步骤，可以避免网速慢、等待时间长带来的疑惑。

2. `--no-ri`不安装gem的ri文档，可以节约安装时间，需要文档时可直接在Web浏览器中查阅网上文档。


## 第一个Padrino应用

### 无数据库版本

    $ cd ~/workspace/

    $ padrino g project helloworld

    $ cd helloworld

    $ padrino start

### 带数据库版本

    $ cd ~/workspace/

    $ padrino g project myapp -d datamappter -b

    $ cd myapp

    $ padrino g admin

    $ padrino rake db:migrate seed

    $ padrino start