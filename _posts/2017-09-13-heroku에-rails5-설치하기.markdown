---
layout: post
title:  "heroku에 rails5 설치하기"
categories: heroku, rails
---

### rails5 설치하기
rails5의 최신 버전을 확인한다.<br>
<https://rubygems.org/gems/rails/versions/5.0.0.beta1>

rails를 설치한다.<br>

{% highlight bash %}
$ gem install rails -v 5.1.4
{% endhighlight %}

새로운 app을 만든다.

{% highlight bash %}
$ rails _5.1.4_ new application_name
{% endhighlight %}

gem file에서 sqlite3를 test, development에, pg를 production으로 이동 및 추가

{% highlight ruby %}
group :development, :test do
  gem 'sqlite3', '1.3.13'
end

group :production do
  gem 'pg', '0.20.0'
end
{% endhighlight %}

gem install 및 서버 구동 테스트

{% highlight bash %}
$ bundle install
$ rails server
{% endhighlight %}

git 연동

{% highlight bash %}
$ git config --global user.name "Your Name"
$ git config --global user.email your@email.com
$ git init
$ git add -A
$ git commit -m "Initialize repository"
{% endhighlight %}

github또는 bitbucket 등 git 서비스와 연동 후 push(설명 생략)

heroku login(toolbelt가 설치되어있지 않다면 설치), heroku의 git에 push

{% highlight bash %}
$ heroku version
$ heroku login
$ git push heroku
{% endhighlight %}
