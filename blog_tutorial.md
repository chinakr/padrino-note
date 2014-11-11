# 用Padrino开发博客系统


参考资料：[官方入门教程：用Padrino开发博客系统](http://www.padrinorb.com/guides/blog-tutorial "Blog Tutorial")

实践是学习编程的最好办法，学习开发一个简单的博客系统是Web开发框架入门教程的常见方式，本教程就是如此。通过学习本教程，我们可以快速掌握使用Padrino开发Web应用的基本流程和方法。


## 安装Padrino

在确认系统中安装有Ruby和RubyGems后，可以通过下列命令安装Padrino：

    $ gem install padrino --verbose --no-ri


## 创建项目

    $ mkdir -p ~/workspace/ruby/padrino/
    $ cd ~/workspace/ruby/padrino/

    $ padrino g project sample_blog -e erb -c sass -s jquery -d activerecord -b

          create  
          create  .gitignore
          create  config.ru
          create  config/apps.rb
          create  config/boot.rb
          create  public/favicon.ico
          create  public/images
          create  public/javascripts
          create  public/stylesheets
          create  .components
          create  app
          create  app/app.rb
          create  app/controllers
          create  app/helpers
          create  app/views
          create  app/views/layouts
          append  config/apps.rb
          create  Gemfile
          create  Rakefile
          create  bin/sample_blog
          create  tmp
          create  tmp/.keep
          create  log
          create  log/.keep
        applying  activerecord (orm)...
           apply  orms/activerecord
          insert  Gemfile
          insert  Gemfile
          create  config/database.rb
          create  lib/connection_pool_management_middleware.rb
          insert  app/app.rb
        skipping  test component...
        skipping  mock component...
        applying  jquery (script)...
           apply  scripts/jquery
          create  public/javascripts/jquery.js
          create  public/javascripts/jquery-ujs.js
          create  public/javascripts/application.js
        applying  erb (renderer)...
           apply  renderers/erb
          insert  Gemfile
        applying  sass (stylesheet)...
           apply  stylesheets/sass
          insert  Gemfile
          insert  app/app.rb
          create  lib/sass_initializer.rb
          create  app/stylesheets
       identical  .components
           force  .components
           force  .components
    Bundling application dependencies using bundler...
             run  bundle install from "."
    Fetching gem metadata from https://rubygems.org/...........
    Resolving dependencies...
    Using rake 10.3.2
    Using i18n 0.6.11
    Using json 1.8.1
    Installing minitest 5.4.2
    Using thread_safe 0.3.4
    Using tzinfo 1.2.2
    Installing activesupport 4.1.7
    Using builder 3.2.2
    Installing activemodel 4.1.7
    Using arel 5.0.1.20140414130214
    Installing activerecord 4.1.7
    Using bundler 1.6.2
    Using erubis 2.7.0
    Using rack 1.5.2
    Using url_mount 0.2.1
    Using http_router 0.11.1
    Using mime-types 1.25.1
    Using polyglot 0.3.5
    Using treetop 1.4.15
    Using mail 2.5.4
    Using moneta 0.7.20
    Using padrino-support 0.12.4
    Using rack-protection 1.5.3
    Using tilt 1.4.1
    Using sinatra 1.4.5
    Using thor 0.19.1
    Using padrino-core 0.12.4
    Using padrino-helpers 0.12.4
    Using padrino-admin 0.12.4
    Using padrino-cache 0.12.4
    Using padrino-gen 0.12.4
    Using padrino-mailer 0.12.4
    Using padrino 0.12.4
    Installing sass 3.4.7
    Installing sqlite3 1.3.10
    Your bundle is complete!
    Use `bundle show [gemname]` to see where a bundled gem is installed.

    =================================================================
    sample_blog is ready for development!
    =================================================================
    $ cd ./sample_blog
    =================================================================

    $ cd sample_blog/


    $ tree

    .
    ├── Gemfile
    ├── Gemfile.lock
    ├── Rakefile
    ├── app
    │   ├── app.rb
    │   ├── controllers
    │   ├── helpers
    │   ├── stylesheets
    │   └── views
    │       └── layouts
    ├── bin
    │   └── sample_blog
    ├── config
    │   ├── apps.rb
    │   ├── boot.rb
    │   └── database.rb
    ├── config.ru
    ├── lib
    │   ├── connection_pool_management_middleware.rb
    │   └── sass_initializer.rb
    ├── log
    ├── public
    │   ├── favicon.ico
    │   ├── images
    │   ├── javascripts
    │   │   ├── application.js
    │   │   ├── jquery-ujs.js
    │   │   └── jquery.js
    │   └── stylesheets
    └── tmp

    15 directories, 15 files

    $ subl app/app.rb 

    get '/' do
      'Hello world!'
    end

    get :about, :map => '/about_us' do
      render :erb, '<p>This is a sample blog created to demostrate how Padrino works!'
    end


## 创建管理工具

    $ padrino g admin

    Error loading RubyGems plugin "/Users/hyx/.rvm/gems/ruby-2.1.1@global/gems/executable-hooks-1.3.1/lib/rubygems_plugin.rb": dlopen(/Users/hyx/.rvm/rubies/ruby-2.1.1/lib/ruby/2.1.0/x86_64-darwin13.0/openssl.bundle, 9): Library not loaded: /usr/local/opt/openssl/lib/libssl.1.0.0.dylib

    $ brew install openssl

    $ padrino g admin

    /Users/hyx/.rvm/rubies/ruby-2.1.1/lib/ruby/2.1.0/yaml.rb:4:in `<top (required)>':
    It seems your ruby installation is missing psych (for YAML output).
    To eliminate this warning, please install libyaml and reinstall your ruby.
    /Users/hyx/.rvm/rubies/ruby-2.1.1/lib/ruby/2.1.0/psych.rb:1:in `require': dlopen(/Users/hyx/.rvm/rubies/ruby-2.1.1/lib/ruby/2.1.0/x86_64-darwin13.0/psych.bundle, 9): Library not loaded: /usr/local/lib/libyaml-0.2.dylib (LoadError)

    $ brew install libyaml

    $ padrino g admin

    /Users/hyx/.rvm/gems/ruby-2.1.1/gems/activesupport-4.1.7/lib/active_support/dependencies.rb:247:in `require': dlopen(/Users/hyx/.rvm/rubies/ruby-2.1.1/lib/ruby/2.1.0/x86_64-darwin13.0/openssl.bundle, 9): Symbol not found: _SSLv2_client_method (LoadError)

    $ rvm reinstall ruby-2.1.1

    $ padrino g admin

           force  .components
          create  admin
           exist  admin
          create  admin/controllers/base.rb
          create  admin/controllers/sessions.rb
          create  public/admin
          create  public/admin/images/favicon.ico
          create  public/admin/images/font/FontAwesome.otf
          create  public/admin/images/font/fontawesome-webfont.eot
          create  public/admin/images/font/fontawesome-webfont.svg
          create  public/admin/images/font/fontawesome-webfont.ttf
          create  public/admin/images/font/fontawesome-webfont.woff
          create  public/admin/images/logo.png
          create  public/admin/javascripts/application.js
          create  public/admin/javascripts/bootstrap/affix.js
          create  public/admin/javascripts/bootstrap/alert.js
          create  public/admin/javascripts/bootstrap/bootstrap.min.js
          create  public/admin/javascripts/bootstrap/button.js
          create  public/admin/javascripts/bootstrap/carousel.js
          create  public/admin/javascripts/bootstrap/collapse.js
          create  public/admin/javascripts/bootstrap/dropdown.js
          create  public/admin/javascripts/bootstrap/modal.js
          create  public/admin/javascripts/bootstrap/popover.js
          create  public/admin/javascripts/bootstrap/scrollspy.js
          create  public/admin/javascripts/bootstrap/tab.js
          create  public/admin/javascripts/bootstrap/tooltip.js
          create  public/admin/javascripts/bootstrap/transition.js
          create  public/admin/javascripts/jquery-1.11.0.min.js
          create  public/admin/stylesheets/application.css
          create  public/admin/stylesheets/bootstrap.css
          create  public/admin/stylesheets/fonts/FontAwesome.otf
          create  public/admin/stylesheets/fonts/fontawesome-webfont.eot
          create  public/admin/stylesheets/fonts/fontawesome-webfont.svg
          create  public/admin/stylesheets/fonts/fontawesome-webfont.ttf
          create  public/admin/stylesheets/fonts/fontawesome-webfont.woff
          create  admin/app.rb
          insert  config/apps.rb
          insert  admin/app.rb
           apply  orms/activerecord
          create  models/account.rb
          create  db/migrate/001_create_accounts.rb
          create  admin/views/accounts
          create  admin/controllers/accounts.rb
          create  admin/views/accounts/_form.erb
          create  admin/views/accounts/edit.erb
          create  admin/views/accounts/index.erb
          create  admin/views/accounts/new.erb
          insert  admin/app.rb
           force  models/account.rb
          create  db/seeds.rb
           exist  admin/controllers
           exist  admin/views
          create  admin/views/base
          create  admin/views/layouts
          create  admin/views/sessions
          create  admin/views/errors
          create  admin/views/base/index.erb
          create  admin/views/layouts/application.erb
          create  admin/views/layouts/error.erb
          create  admin/views/sessions/new.erb
          create  admin/views/errors/403.erb
          create  admin/views/errors/404.erb
          create  admin/views/errors/500.erb
          insert  admin/app.rb
          insert  Gemfile
            gsub  admin/controllers/accounts.rb

    =================================================================
    The admin panel has been mounted! Next, follow these steps:
    =================================================================
      1) Run 'bundle'
      2) Run 'bundle exec rake db:create' if you have not created a database yet
      3) Run 'bundle exec rake db:migrate'
      4) Run 'bundle exec rake db:seed'
      5) Visit the admin panel in the browser at '/admin'
=================================================================

    $ bundle install

    $ padrino rake ar:create

    $ padrino rake ar:migrate

    $ padrino rake seed

    Which email do you want use for logging into admin? chinakr@gmail.com
    Tell me the password to use: ******


## 检查工作成果

    $ padrino start

    $ firefox http://localhost:3000/

    Hello world!

    $ firefox http://localhost:3000/about_us/

    This is a sample blog created to demostrate how Padrino works!

    $ firefox http://localhost:3000/admin/

    Padrino is a ruby framework built upon the Sinatra web library.

    It was created to make it fun and easy to code more advanced web applications while still adhering to the spirit that makes Sinatra great!

    Padrino comes shipped with a slick and beautiful Admin Interface, with the following features:

    Orm Agnostic  Authentication  Template Agnostic  Multi Language  Scaffold


## 添加文章

    $ padrino g model post title:string body:text -a app

     apply  orms/activerecord
    create  app/models/post.rb
    create  db/migrate/002_create_posts.rb

    $ padrino rake ar:migrate

    $ padrino g controller posts get:index get:show

    create  app/controllers/posts.rb
    create  app/views/posts
    create  app/helpers/posts_helper.rb

    $ subl app/controllers/posts.rb

    get :index do
      @posts = Post.all
      render 'posts/index'
    end

    get :show, :with => :id do
      @post = Post.find_by_id(params[:id])
      render 'posts/show'
    end

    $ subl app/views/posts/index.erb

    <% @title = 'Welcome' %>
    <ul>
      <% @posts.each do |post| %>
      <li><%= link_to post.title, url_for(:posts, :show, post.id) %></li>
      <% end %>
    </ul>

    $ subl app/views/posts/show.erb

    <% @title = @post.title %>
    <h1><%= @post.title %></h1>
    <div class="content">
      <%= @post.body %>
    </div>
    <p><%= link_to 'View all posts', url_for(:posts, :index) %></p>

    $ padrino g admin_page post

    create  admin/views/posts
    create  admin/controllers/posts.rb
    create  admin/views/posts/_form.erb
    create  admin/views/posts/edit.erb
    create  admin/views/posts/index.erb
    create  admin/views/posts/new.erb
    insert  admin/app.rb

    $ firefox http://localhost:3000/admin/

在`posts`标签页下添加2篇文章。

    $ padrino rake routes

    => Executing Rake routes ...

    Application: SampleBlog::Admin
        URL                           REQUEST  PATH
        (:accounts, :index)             GET    /admin/accounts
        (:accounts, :new)               GET    /admin/accounts/new
        (:accounts, :create)           POST    /admin/accounts/create
        (:accounts, :edit)              GET    /admin/accounts/edit/:id
        (:accounts, :update)            PUT    /admin/accounts/update/:id
        (:accounts, :destroy)         DELETE   /admin/accounts/destroy/:id
        (:accounts, :destroy_many)    DELETE   /admin/accounts/destroy_many
        (:base, :index)                 GET    /admin/
        (:posts, :index)                GET    /admin/posts
        (:posts, :new)                  GET    /admin/posts/new
        (:posts, :create)              POST    /admin/posts/create
        (:posts, :edit)                 GET    /admin/posts/edit/:id
        (:posts, :update)               PUT    /admin/posts/update/:id
        (:posts, :destroy)            DELETE   /admin/posts/destroy/:id
        (:posts, :destroy_many)       DELETE   /admin/posts/destroy_many
        (:sessions, :new)               GET    /admin/sessions/new
        (:sessions, :create)           POST    /admin/sessions/create
        (:sessions, :destroy)         DELETE   /admin/sessions/destroy

    Application: SampleBlog::App
        URL                 REQUEST  PATH
        (:about)              GET    /about_us
        (:posts, :index)      GET    /posts
        (:posts, :show)       GET    /posts/show/:id

    $ firefox http://localhost:3000/posts/show/1

    $ firefox http://localhost:3000/posts

## 把用户和文章关联起来

修改应用设计，使添加文章时同时记录作者(用户名)。

    $ padrino g migration AddAccountToPost account_id:integer

     apply  orms/activerecord
    create  db/migrate/003_add_account_to_post.rb

    $ subl db/migrate/003_add_account_to_post.rb

    def self.up
      change_table :posts do |t|
        t.integer :account_id
      end
      first_account = Account.first
      Post.all.each do |p|
        p.update_attribute(:account, first_account)
      end
    end

    $ subl app/models/post.rb

    belongs_to :account
    validates_presence_of :title
    validates_presence_of :body

    $ padrino rake db:migrate

    => Executing Rake db:migrate ...
      DEBUG -  ActiveRecord::SchemaMigration Load (0.6ms)  SELECT "schema_migrations".* FROM "schema_migrations"
       INFO -  Migrating to AddAccountToPost (3)
      DEBUG -   (0.1ms)  begin transaction
    == 3 AddAccountToPost: migrating ==============================================
    -- change_table(:posts)
      DEBUG -   (1.1ms)  ALTER TABLE "posts" ADD "account_id" integer
       -> 0.0046s
      DEBUG -  Account Load (0.3ms)  SELECT  "accounts".* FROM "accounts"   ORDER BY "accounts"."id" ASC LIMIT 1
      DEBUG -  Post Load (0.4ms)  SELECT "posts".* FROM "posts"
      DEBUG -  SQL (0.2ms)  UPDATE "posts" SET "account_id" = ?, "updated_at" = ? WHERE "posts"."id" = 1  [["account_id", 1], ["updated_at", "2014-11-08 17:57:24.228578"]]
      DEBUG -  SQL (0.1ms)  UPDATE "posts" SET "account_id" = ?, "updated_at" = ? WHERE "posts"."id" = 2  [["account_id", 1], ["updated_at", "2014-11-08 17:57:24.233995"]]
    == 3 AddAccountToPost: migrated (0.0296s) =====================================

      DEBUG -  SQL (0.2ms)  INSERT INTO "schema_migrations" ("version") VALUES (?)  [["version", "3"]]
      DEBUG -   (3.0ms)  commit transaction
      DEBUG -  ActiveRecord::SchemaMigration Load (0.2ms)  SELECT "schema_migrations".* FROM "schema_migrations"

    $ subl admin/controllers/posts.rb

    post :create do
      @post = Post.new(params[:post])
      @post.account = current_account

    $ subl app/views/posts/show.erb

    <h1><%= @post.title %></h1>
    <p class="author"><%= @post.account.email %></p>

    $ firefox http://localhost:3000/posts/show/1

## 网站布局

    $ subl app/views/layouts/application.erb

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <title><%= [@title, 'Padrino Sample Blog'].compact.join(' | ') %></title>
        <%= stylesheet_link_tag 'reset', 'application' %>
        <%= javascript_include_tag 'jquery', 'application' %>
        <%= yield_content :include %>
      </head>
      <body>
        <div class="header">
          <h1>Sample Padrino Blog</h1>
          <ul class="menu">
            <li><%= link_to 'Blog', url_for(:posts, :index) %></li>
            <li><%= link_to 'About', url_for(:about) %></li>
          </ul>
        </div>
        <div class="container">
        </div>
          <div class="main">
            <%= yield %>
          </div>
          <div class="sidebar">
            <% form_tag url_for(:posts, :index), :method => 'get' do %>
              Search for:
              <%= text_field_tag 'query', :value => params[:query] %>
              <%= submit_tag 'Search' %>
            <% end %>
          </div>
          <div class="footer">
          </div>
      </body>
    </html>

    $ firefox http://localhost:3000/posts


## 创建RSS订阅源(RSS Feed)

    $ subl app/controllers/posts.rb

    get :index, :provides => [:html, :rss] do

    $ subl app/views/posts/index.erb

    <% content_for :include do %>
      <%= feed_tag :rss, url(:posts, :index, :format => :rss), :title => 'RSS' %>
    <% end %>

    $ subl app/views/posts/index.rss.builder

    xml.instruct!
    xml.rss "version" => "2.0", "xmlns:dc" => "http://purl.org/dc/elements/1.1/" do
      xml.channel do
        xml.title "Padrino Blog"
        xml.description "The fantastic padrino sample blog"
        xml.link url_for(:posts, :index)

        for post in @posts
          xml.item do
            xml.title post.title
            xml.description post.body
            xml.pubDate post.created_at.to_s(:rfc822)
            xml.link url_for(:posts, :show, :id => post)
          end
        end
      end
    end

    $ firefox http://localhost:3000/posts

    $ firefox http://localhost:3000/posts.rss


## 布署应用

把应用部署到Heroku上。

    $ git init

    $ git add .

    $ git commit -m 'Initial commit.'

    $ heroku create

    $ git push heroku master

    !     Failed to install gems via Bundler.
    !     
    !     Detected sqlite3 gem which is not supported on Heroku.
    !     https://devcenter.heroku.com/articles/sqlite3
    !

    !     Push rejected, failed to compile Ruby app

    $ subl Gemfile

    gem 'sqlite3', :group => [:development, :test]
    gem 'pg', :group => :production

    $ subl config/database.rb

    ActiveRecord::Base.configurations[:production] = {
      :adapter  => 'postgresql',
      :encoding => 'utf8',
      :database => postgres.path[1..-1],
      :username => postgres.user,
      :password => postgres.password,
      :host     => postgres.host
    }

    $ padrino rake gen

    An error occurred while installing pg (0.17.1), and Bundler cannot continue.
    Make sure that `gem install pg -v '0.17.1'` succeeds before bundling.

    $ gem install pg

    Building native extensions.  This could take a while...
    ERROR:  Error installing pg:
        ERROR: Failed to build gem native extension.

    $ brew update

    $ brew install postgresql

    $ gem install pg

    $ bundle

    $ padrino rake gen

    => Executing Rake gen ...
    /Users/hyx/.rvm/gems/ruby-2.1.1/gems/rake-10.3.2/lib/rake/task_manager.rb:62:in `[]': Don't know how to build task 'gen' (RuntimeError)

    $ subl db/seeds.rb

    $ padrino rake db:seed

    => Executing Rake db:seed ...
      ERROR -  NameError - undefined local variable or method `postgres' for main:Object:
     /Users/hyx/workspace/ruby/padrino/sample_blog/config/database.rb:25:in `<top (required)>'
    /Users/hyx/workspace/ruby/padrino/sample_blog/config/database.rb:25:in `<top (required)>': undefined local variable or method `postgres' for main:Object (NameError)

    $ git add .

    $ git commit -m 'Add PostgreSQL support for Heroku.'

    $ git push heroku master

    Initializing repository, done.
    Counting objects: 111, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (102/102), done.
    Writing objects: 100% (111/111), 396.54 KiB | 168.00 KiB/s, done.
    Total 111 (delta 12), reused 0 (delta 0)

    -----> Ruby app detected
    -----> Compiling Ruby/Rack
    -----> Using Ruby version: ruby-2.0.0
    -----> Installing dependencies using 1.6.3
           Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
           Fetching gem metadata from https://rubygems.org/.........
           Installing i18n 0.6.11
           Installing rake 10.3.2
           Installing minitest 5.4.2
           Installing thread_safe 0.3.4
           Installing arel 5.0.1.20140414130214
           Installing builder 3.2.2
           Installing json 1.8.1
           Installing erubis 2.7.0
           Installing mime-types 1.25.1
           Installing rack 1.5.2
           Installing polyglot 0.3.5
           Installing moneta 0.7.20
           Installing tilt 1.4.1
           Using bundler 1.6.3
           Installing bcrypt 3.1.9
           Installing thor 0.19.1
           Installing sass 3.4.7
           Installing tzinfo 1.2.2
           Installing url_mount 0.2.1
           Installing rack-protection 1.5.3
           Installing treetop 1.4.15
           Installing activesupport 4.1.7
           Installing http_router 0.11.1
           Installing sinatra 1.4.5
           Installing mail 2.5.4
           Installing activemodel 4.1.7
           Installing padrino-support 0.12.4
           Installing activerecord 4.1.7
           Installing padrino-core 0.12.4
           Installing padrino-helpers 0.12.4
           Installing padrino-mailer 0.12.4
           Installing padrino-gen 0.12.4
           Installing padrino-cache 0.12.4
           Installing padrino-admin 0.12.4
           Installing padrino 0.12.4
           Installing pg 0.17.1
           Your bundle is complete!
           Gems in the groups development and test were not installed.
           It was installed into ./vendor/bundle
           Bundle completed (27.96s)
           Cleaning up the bundler cache.
    -----> Writing config/database.yml to read from DATABASE_URL

    ###### WARNING:
           You have not declared a Ruby version in your Gemfile.
           To set your Ruby version add this line to your Gemfile:
           ruby '2.0.0'
           # See https://devcenter.heroku.com/articles/ruby-versions for more information.

    ###### WARNING:
           No Procfile detected, using the default web server (webrick)
           https://devcenter.heroku.com/articles/ruby-default-web-server

    -----> Discovering process types
           Procfile declares types -> (none)
           Default types for Ruby  -> console, rake, web

    -----> Compressing... done, 21.4MB
    -----> Launching... done, v6
           https://boiling-peak-2203.herokuapp.com/ deployed to Heroku

    To git@heroku.com:boiling-peak-2203.git
     * [new branch]      master -> master

    $ heroku run rake ar:migrate

    Running `rake ar:migrate` attached to terminal... up, run.8270
    rake aborted!
    NameError: undefined local variable or method `postgres' for main:Object

    $ subl config/database.rb

    postgres = URI.parse(ENV['DATABASE_URL'] || '')

    ActiveRecord::Base.configurations[:production] = {
      :adapter  => 'postgresql',
      :encoding => 'utf8',
      :database => postgres.path[1..-1],
      :username => postgres.user,
      :password => postgres.password,
      :host     => postgres.host
    }

    $ git add .

    $ git commit -m 'Fix databse.rb.'

    $ git push heroku master

    $ heroku run rake ar:migrate

    Running `rake ar:migrate` attached to terminal... up, run.9509
    == 1 CreateAccounts: migrating ================================================
    -- create_table(:accounts)
       -> 0.0552s
    == 1 CreateAccounts: migrated (0.0557s) =======================================

    == 2 CreatePosts: migrating ===================================================
    -- create_table(:posts)
       -> 0.0403s
    == 2 CreatePosts: migrated (0.0406s) ==========================================

    == 3 AddAccountToPost: migrating ==============================================
    -- change_table(:posts)
       -> 0.0116s
    == 3 AddAccountToPost: migrated (0.0203s) =====================================

    $ heroku run rake seed

输入用户名、密码。

    $ heroku open

    $ firefox https://boiling-peak-2203.herokuapp.com/posts

    $ firefox https://boiling-peak-2203.herokuapp.com/admin

登录并添加2篇文章。

    $ firefox https://boiling-peak-2203.herokuapp.com/posts

测试成功！

本教程到此结束。