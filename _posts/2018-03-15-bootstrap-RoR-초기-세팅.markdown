---
layout: post
title:  "bootstrap RoR 초기 세팅"
categories: rails
---

# 환경
ruby version: 2.3.4<br>
rails version: 5.1.4<br>
bootstrap version: 3.3<br>

# gemfile 추가
{% highlight ruby %}
gem 'rails',              '~> 5.1.4'
gem 'puma',               '~> 3.9.1'
gem 'sqlite3',            '~> 1.3.13'
gem 'bootstrap-sass',     '~> 3.3.7'
gem 'sass-rails',         '~> 5.0.6'
gem 'uglifier',           '~> 3.2.0'
gem 'coffee-rails',       '~> 4.2.2'
gem 'turbolinks',         '~> 5.0.1'
gem 'jbuilder',           '~> 2.7.0'
gem 'redis',              '~> 3.0'
gem 'bcrypt',             '~> 3.1.11'
gem 'font-awesome-rails', '~> 4.7'
gem 'jquery-rails',       '~> 4.3.1'
{% endhighlight %}

* 본인이 구현할 application에 맞게 추가 수정 필요

# javascript 파일에 부트스트랩 등 추가
app/assets/javascripts/application.js<br>

{% highlight javascript %}
//= require rails-ujs
//= require jquery
//= require jquery_ujs
//= require bootstrap
//= require turbolinks
//= require_tree .
{% endhighlight %}

# css import 추가
app/assets/stylesheets/custom.scss

{% highlight scss %}
@import "bootstrap-sprockets";
@import "bootstrap";
@import "font-awesome";
{% endhighlight %}

# IE 대응을 위한 shim 추가
app/views/layouts/_shim.html.erb


{% highlight html %}
<!--[if lt IE 9]>
    <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/r29/html5.min.js">
    </script>
<![endif]-->
{% endhighlight %}

# header, footer 추가

app/views/layouts/_header.html.erb
app/views/layouts/_footer.html.erb


# application.html.erb에 shim, header, footer 추가
+ viewport 추가, debug를 위한 구문 추가
app/views/layouts/application.html.erb

{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <title>TITLE</title>
    <%= csrf_meta_tags %>
 
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= render 'layouts/shim' %>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  </head>
 
  <body>
    <%= render 'layouts/header' %>
    <%= yield %>
    <%= render 'layouts/footer' %>
    <%= debug(params) if Rails.env.development? %>
  </body>
</html>
{% endhighlight %}

# time_zone 세팅
{% highlight ruby %}
module Yourapp
  class Application < Rails::Application
    config.time_zone = 'Seoul'
  end
end
{% endhighlight %}