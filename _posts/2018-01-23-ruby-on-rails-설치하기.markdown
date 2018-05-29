---
layout: post
title:  "Ruby-on-Rails-설치하기"
categories: etc
---
설치환경: Mac OS
<br><br>
Mac의 system Ruby는 최신 버전이 아니기 때문에, ruby를 설치해줘야 한다.
일단, Homebrew를 설치한다. 설치 방법은 url 참고
<br><https://brew.sh/index_ko.html><br>
ruby 설치를 위해 rbenv를 설치한다. (rbenv 외에 rvm도 사용할 수 있다)
<br>
~~~
$ brew update
$ brew install rbenv
~~~

rbenv를 이용해 ruby를 설치한다.
~~~
$ rbenv install 2.5.0 && rbenv rehash
$ rbenv global 2.5.0
~~~

최신 업데이트 된 루비를 사용하기위해 ruby-build를 먼저 업데이트 해준다.
~~~
$ brew update ruby-build
~~~

Rails를 설치한다.
~~~
$ gem install rails -v 5.1.4
~~~

Rails application을 생성한다.
~~~
$ rails _5.1.4_ new welcome_app
~~~

bundle install
~~~
$ cd welcome_app
$ bundle install
~~~

local server를 구동해서 확인한다.
~~~
$ rails server
~~~
브라우저로 http://localhost:3000 접속
![yay]({{ site.url }}/assets/img/2018-01-23/01.png)<br>
<br>
설치 과정은 쉽지 않다. 시스템마다 생각지 못한 문제들이 발생하기 때문. google신을 활용해서 문제를 해결해야 한다.
초심자라면, 구름 IDE, cloud9 등 IDE를 활용하면 난이도가 조금이나마 내려간다.

참고<br>
<https://www.ruby-lang.org/ko/>
<https://rubyonrails.org/>
<https://github.com/rbenv/rbenv>
