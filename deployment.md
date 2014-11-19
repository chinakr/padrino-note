# 把Padrino应用部署到服务器


## 服务器环境

Ubuntu 12.04 LTS 64bit

Ruby 2.1

nginx 1.6

Puma 2.9

MySQL 5.5


## 参考资料

[Nginx, Sinatra, and Puma.](https://gist.github.com/ctalkington/4448153 "Google关键字：padrino deploy nginx puma")

[How to Setup Rails App with Puma and nginx](https://github.com/joneslee85/ruby-journal-source/blob/master/source/_posts/2013-03-16-how-to-setup-rails-app-with-puma-and-nginx.markdown "Google关键字：bundle puma daemon")


## 用ssh手工部署

### 登录服务器

以普通帐号登录服务器。

创建应用目录：

    $ sudo mkdir -p /var/www/www.hdjxbm.com/

    $ sudo chown user:user /var/www/www.hdjxbm.com/

    $ ls -l /var/www/

注：以下如未特别说明，均默认在服务器上。

安装Padrino：

    $ gem install padrino

### 本地上传应用源代码

在本地：

    $ cd ~/workspace/www.hdjxbm.com/

    $ scp -r . user@www.hdjxbm.com:/var/www/www.hdjxbm.com/

在服务器上生成数据库：

    $ cd /var/www/www.hdjxbm.com/

    $ bundle

    $ padrino rake ar:create

    $ padrino rake ar:migrate

    $ padrino rake seed

### 配置Puma

    $ cd /var/www/www.hdjxbm.com/

    $ vim Gemfile

    ...
    gem 'puma'

    $ bundle

    $ vim app/app.rb

    ...
    configure do
      ...
      set :server, :puma
    end
    ...

    $ vim config/puma.rb

    root = "#{Dir.getwd}"

    bind "unix://#{root}/tmp/puma/socket"
    pidfile "#{root}/tmp/puma/pid"
    state_path "#{root}/tmp/puma/state"
    rackup "#{root}/config.ru"

    threads 4, 8

    activate_control_app

    $ mkdir -p tmp/puma/

    $ RAKE_ENV='production' bundle exec puma -d --config config/puma.rb

### 配置nginx

    $ cd /etc/nginx/sites-available/

    $ sudo vim www.hdjxbm.com

    upstream app {
        server unix:///var/www/www.hdjxbm.com/tmp/puma/socket;
    }

    server {
        listen 80;
        server_name www.hdjxbm.com;

        root /var/www/www.hdjxbm.com/public;
        access_log /var/www/www.hdjxbm.com/log/nginx.access.log;
        error_log /var/www/www.hdjxbm.com/log/nginx.error.log info;

        location / {
            try_files $uri @puma;
        }

        location @puma {
            include proxy_params;

            proxy_pass http://app;
        }
    }

    $ cd ../sites-enabled/

    $ sudo ln -s ../sites-available/www.hdjxbm.com .

    $ ls -l

    $ sudo service nginx restart

### 访问测试

    $ firefox http://www.hdjxbm.com/