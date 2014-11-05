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

在坚持Sinatra核心理念的同时，Padrino提供了一系列工具(tools)、助手(helpers)和函数(functions)库，从而具有了上述优势。


## Padrino比Sinatra多了哪些功能

* `Agnostic`：对众多流行的测试、模板、模仿(mocking)和数据库的库提供了支持。

* 生成器(generators)：创建Padrino应用、模型、控制器。

* 可安装(mountable)：和其他Ruby框架不同，主要用于安装多个应用。

* 路由(routing)：提供完整的URL命名路由、命名参数、`respond_to`、前/后置过滤器支持。

* 标签助手(tag helpers)：视图助手，例如`tag`、`content_tag`、`input_tag`。

* 资产助手(asset helpers)：视图助手，例如`link_to`、`image_tag`。

* 表单助手(form helpers)：生成器(builder)支持，例如`form_tag`、`form_for`、`field_set_tag`。

* 文本助手(text helpers)：有用格式，例如`relative_time_ago`、`js_escape_html`。

* 邮件程序(mailer)：快速简单的邮件发送支持，类似`ActionMailer`。

* 缓存(caching)：简单的路由和碎片(fragment)缓存，使加速Web请求变得很容易。

* 管理工具(admin)：内建包括认证的管理工具，类似Django。

* 日志(loggin)：提供同ORM或任何库交互的统一的记录器。

* 重新加载(reloading)：在开发阶段自动重载服务器代码。

* 本地化(localization)：提供完整的i18n本地化支持。


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