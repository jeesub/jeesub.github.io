---
layout: post
title:  "jekyll blog 만들기"
date:   2017-09-12 17:51:30 +0900
categories: jekyll
---
Heroku에 Ruby on Rails 5로 만든 앱을 올리다 보니, Ruby on Rails 4를 사용하던 때와는 다른 에러들이 나오기 시작했다. 
홈페이지를 여러개 만들어야 하는 상황이라 문제와 해결방법을 기록할 블로그를 만들기로 했다. 기왕 블로그를 시작하는 김에 새로운 블로그 툴을 사용해보려고 Jekyll로 만들었다. 
기존에는 Tistory, Naver blog, Blogger 등 기본 제공형 블로그와 Wordpress를 사용해본 경험이 있다. 
기존 블로그에서 느낀 가장 불편한 점은 editor였다. 종종 글을 작성할 때 editor와 구현된 글(HTML로 변환된 글) 사이의 괴리가 있었기때문에 html 편집기로 들어가 태그를 수정해줘야했다. 
Jekyll은 마크다운 언어로 글을 작성하기때문에 해당 문제는 없을 것으로 기대했다.

# 설치하기

설치 방법은 다음 링크에 잘 정리가 되어있다. Jekyll은 Ruby로 만들어졌기때문에 mac과 linux를 쓴다면 편할 것 같다. git과 terminal을 기본적인것만 사용할 줄 안다면 쉽게 설치가 가능하다. 하지만, 잘 사용하지 못하더라도 아래 블로그에 정리된 것을 따라하면 설치할 수 있을 것 같다.<br>
<https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/>

# 설치 및 블로그 생성

<https://jekyllrb-ko.github.io/docs/installation/><br>
Jekyll 공식 홈페이지를 방문해서 한 번 살펴볼 것을 추천한다.<br>
Ruby가 설치되어 있다면, 아래 명령어를 통해 Jekyll을 설치할 수 있다.<br>
Ruby gem으로 설치할 수 있다.

{% highlight bash %}
$ gem install jekyll bundler
{% endhighlight %}

Jekyll 사이트를 만든다.

{% highlight bash %}
$ jekyll new [username].github.com
$ cd [username].github.com
{% endhighlight %}

GitHub에 deploy

{% highlight bash %}
$ git init
$ git remote add origin [저장소 URL]
$ git add -A
$ git commit -m "init"
$ git push origin master
{% endhighlight %}

[username].github.com에 접속하면 deploy된 블로그를 확인할 수 있다.

# 마크다운

Jekyll 블로그는 마크다운 언어로 작성을 하면 HTML로 변환해서 화면에 출력해준다. 마크다운 언어의 사용법에 대해서는 다음 링크를 참조<br>
<https://gist.github.com/ihoneymon/652be052a0727ad59601>

# 포스팅하기

github을 사용하듯이 하면 된다. 로컬에서 글을 쓰고 origin repository에 push 해주면 된다.

{% highlight bash %}
$ git add -A
$ git commit -m "add new post"
$ git push origin master
{% endhighlight %}

# 발행 하기 전에 local에서 확인하기

local 환경에서 미리 사이트를 확인할 수 있다.

{% highlight bash %}
$ bundle exec jekyll serve --watch
{% endhighlight %}