---
layout: post
title:  "Ruby on Rails 설치하기"
categories: [web-development, ruby-on-rails]
---

설치환경: Mac OS

Mac의 system Ruby는 최신 버전이 아니기 때문에, ruby를 설치해줘야 한다.
일단, Homebrew를 설치한다. 설치 방법은 url 참고

<https://brew.sh/index_ko.html>

Ruby 설치를 위해 rbenv를 설치한다. (rbenv 외에 rvm도 사용할 수 있다)

{% highlight bash %}
$ brew update
$ brew install rbenv
{% endhighlight %}

rbenv를 이용해 Ruby를 설치한다. 

{% highlight bash %}
$ rbenv install 2.5.0 && rbenv rehash
$ rbenv global 2.5.0
{% endhighlight %}

최신 업데이트 된 루비를 사용하기위해 ruby-build를 먼저 업데이트 해준다. 

{% highlight bash %}
$ brew update ruby-build
{% endhighlight %}

terminal을 종료 후 재실행 해준다. Ruby 버전을 확인해 설정이 잘 되었는지 확인한다. 

{% highlight bash %}
$ ruby -v
{% endhighlight %}

새로 설치한 버전이 나오지 않을 경우, 아래 링크를 참조해서 해결할 수 있다. 

<https://stackoverflow.com/questions/10940736/rbenv-not-changing-ruby-version><br>

gem을 이용해 Rails를 설치한다. 

{% highlight bash %}
$ gem install rails -v 5.1.4
{% endhighlight %}

Rails application을 생성한다. 

{% highlight bash %}
$ rails _5.1.4_ new welcome_app
{% endhighlight %}

bundle install 

{% highlight bash %}
$ cd welcome_app
$ bundle install
{% endhighlight %}

local server를 구동해서 확인한다. 

{% highlight bash %}
$ rails server
{% endhighlight %}

브라우저로 http://localhost:3000 접속

![yay]({{ "/assets/img/2018-01-23/01.png" | relative_url }})

설치 과정은 쉽지 않다. 
시스템마다 생각지 못한 문제들이 발생하기 때문. 
Google신을 활용해서 문제를 해결해야 한다. 
초심자라면, 구름 IDE, cloud9 등 IDE를 활용하면 난이도가 조금이나마 내려간다. 

# 참고
* <https://www.ruby-lang.org/ko/>
* <https://rubyonrails.org/>
* <https://github.com/rbenv/rbenv>