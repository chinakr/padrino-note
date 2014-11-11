# 在Padrino中使用Bootstrap


## Bootstrap简介

[Bootstrap官网](http://getbootstrap.com/)

Bootstrap是最流行的HTML、CSS和JavaScript框架之一，目前只有[Foundation](foundation.zurb.com/)能与之媲美。基于Bootstrap开发响应式、移动优先的网站，可以达到事半功倍的效果。

截至2014年11月9日，Bootstrap的最新版本为`3.3.0`。


## 准备工作

下载最新版本的Bootstrap并解压缩，然后拷贝相关的CSS和JavaScript文件到Padrino项目的相应目录下。

    $ cp /path/to/bootstrap.min.css public/stylesheets/

    $ cp /path/to/bootstrap-theme.min.css public/stylesheets/

    $ cp /path/to/bootstrap.min.js public/javascripts/

    $ cp /path/to/html5shiv.min.js public/javascripts/

    $ cp /path/to/respond.min.js public/javascripts/

    $ cp -r /path/to/fonts/ public/

检查所有文件是否已经正确拷贝。

    $ ls public/

    admin       fonts       javascripts
    favicon.ico images      stylesheets

    $ ls public/stylesheets/

    bootstrap-theme.min.css bootstrap.min.css

    $ ls public/javascripts/

    application.js      html5shiv.min.js    jquery.js
    bootstrap.min.js    jquery-ujs.js       respond.min.js

    $ ls public/fonts/

    glyphicons-halflings-regular.eot    glyphicons-halflings-regular.ttf
    glyphicons-halflings-regular.svg    glyphicons-halflings-regular.woff


## 未使用栅格系统的版本

基于Bootstrap编写Padrino项目的页面布局文件，未使用栅格系统。

    $ subl app/views/layouts/application.erb

    <!DOCTYPE html>
    <html lang="zh-cmn-Hans">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title><%= [@title, 'Site Title'].compact.join(' | ') %></title>
        <%= stylesheet_link_tag 'bootstrap.min', 'application' %>
        <%= yield_content :include %>
        <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
        <!--[if lt IE 9]>
          <%= javascript_include_tag 'html5shiv.min', 'respond.min' %>
        <![endif]-->
      </head>
      <body>
        <div class="container">
          <%= yield %>
        </div>
        <%= javascript_include_tag 'jquery', 'bootstrap.min', 'application' %>
      </body>
    </html>


## 使用栅格系统的版本

基于Bootstrap编写Padrino项目的页面布局文件，栅格系统使用经典的`页头-(内容|边栏)-页尾`的结构。

    <!DOCTYPE html>
    <html lang="zh-cmn-Hans">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title><%= [@title, 'Site Title'].compact.join(' | ') %></title>
        <%= stylesheet_link_tag 'bootstrap.min', 'application' %>
        <%= yield_content :include %>
        <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
        <!--[if lt IE 9]>
          <%= javascript_include_tag 'html5shiv.min', 'respond.min' %>
        <![endif]-->
      </head>
      <body>
        <div class="container">
          <div class="header">
            <div class="row">
              <div class="col-xs-12">
                <!-- header -->
              </div>
            </div>
          </div>
          <div class="content">
            <div class="row">
              <div class="main">
                <div class="col-xs-12 col-sm-10">
                  <%= yield %>
                </div>
              </div>
              <div class="sidebar">
                <div class="col-sm-2">
                    <!-- sidebar -->
                </div>
              </div>
            </div>
          </div>
          <div class="footer">
            <div class="row">
              <div class="col-xs-12">
                <!-- footer -->
              </div>
            </div>
          </div>
        </div>
        <%= javascript_include_tag 'jquery', 'bootstrap.min', 'application' %>
      </body>
    </html>
