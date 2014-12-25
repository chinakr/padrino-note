# 使用Capistrano 3部署Padrino应用


## Capistrano基础

### Capistrano是什么

Capistrano是一个自动化部署工具，它使用Ruby语言开发。Capistrano在底层是通过SSH在远程服务器上执行命令，以此来完成不同的部署任务。用户还可以用Capistrano定义的DSL(领域专用语言)来扩展更多任务。Capistrano常用于部署Rails应用，当然也可以用于部署Padrino应用。

### 使用Capistrano对远程服务器的要求

可以通过SSH访问；可以用`sh`调用Shell；建议使用公钥而不是用户名密码来访问。

### 查看Capistrano使用帮助

查看命令行参数：

    $ cap -h

查看可用的任务：

    $ cap -T

Capistrano官方网站：<http://capistranorb.com/>

Capistrano项目主页：<https://github.com/capistrano/capistrano>


## Capistrano的基本用法

### 使用Capistrano的准备工作

进入项目目录：

    $ cd /path/to/project/

安装所需gem(Capistrano及所需插件)：

    $ subl Gemfile

    gem 'capistrano', '~> 3.3.0'
    gem 'capistrano-rvm'
    gem 'capistrano-bundler', '~> 1.1.2'

`capistrano-rvm`这个gem的作用是增加了一个在`deploy`任务之前自动运行的任务`rvm:hook`，这样就可让Capistrano在`rvm ... do ...`的环境下运行`rake`、`gem`、`bundle`或`ruby`命令。

`capistrano-bundler`这个gem的作用是为`bundle_bins`中的可执行命令添加`bundle exec`前缀，包括`gem`、`rake`和`rails`.

初始化Capistrano：

    $ bundle exec cap install

这个命令会在项目目录下生成`Capfile`、`config/deploy.rb`、`config/deploy/staging.rb`和`config/deploy/production.rb`文件。

`config/deploy.rb`中用`lock '3.3.5'`语句锁定了Capistrano的版本号。

其中`bundle exec`表示在bundle的上下文环境中执行命令，也就是使用Gemfile中指定的gem。

启用所需插件：

    $ subl Capfile

    require 'capistrano/rvm'
    require 'capistrano/bundler'

修改Capistrano配置：

    $ subl config/deploy.rb

    set :application, 'zuoye'
    set :repo_url, 'https://github.com/chinakr/zuoye'

其中`zuoye`是应用名称，同时还配置了应用源代码仓库的URL。从文件中的注释可以看到，应用源代码默认将部署在远程服务器的`/var/www/zuoye`目录下。

    $ subl config/deploy/production.rb

    server 'zuoye.haijia.net.cn', user: 'zuoye', roles: %w{web app db}

`role :app, %w{deploy@example.com}`等3条语句要注释掉。

### 配置Capistrano所需掌握的知识

role：web(如nginx)，app(如puma)，db(如MySQL)。

### 开始部署

测试部署(测试所有部署命令，但不发生实际部署行为)：

    $ bundle exec cap production deploy --dry-run

开始部署：

    $ bundle exec cap production deploy

注：1) 如果出现权限问题，可以在远程服务器上执行`sudo chmod 777 /var/www`。2) 如果出现长时间挂起，可尝试中断后带`--trace`参数重新执行。

到此为止，Padrino应用的源代码就部署完成了，还需要配置nginx和Puma。

### 出现问题时怎么办

回滚到上一次部署的版本：

    $ bundle exec cap production deploy:rollback


## 扩展Capistrano任务

### Capistrano定义的DSL

定义任务的基本语法如下：

    desc 'Task description'
    task :task_name do
      ...
    end

包括了任务说明和任务定义这两个部分。

`on`, `in`


## 参考资料

[Capistrano官方网站](http://capistranorb.com/)

[Capistrano项目主页(GitHub)](https://github.com/capistrano/capistrano)

[man: bundle exec](http://bundler.io/man/bundle-exec.1.html)

[Capistrano 3 实现 Rails 自动化部署](https://ruby-china.org/topics/18616)

[Capistrano + Nginx + Unicorn + Sinatra on Ubuntu](https://gist.github.com/wlangstroth/3740923 "deploy.rb, nginx.conf, unicorn.rb")