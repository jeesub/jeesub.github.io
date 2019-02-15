---
layout: post
title:  "rails kaminari 페이지네이션"
categories: rails
---

# Pagination

페이지네이션은 게시판에서 흔히 볼 수 있다.
전체 정보량이 많을 경우, 한 번에 보여줄 정보의 양을 정하고 페이지 별로 보여주는 방법이다.
기본적으로는 책처럼 페이지를 만드는 형태로 구현한다.
타임라인과 모바일이 대중화되면서 요즘은 '스크롤 해서 더 보기'도 많이 쓰이고 있다.
Ruby on Rails에서는 kaminari gem을 활용하면 페이지네이션을 쉽게 구현할 수 있다.

# kaminari

<https://github.com/kaminari/kaminari>
Ruby on Rails의 페이지네이션 gem 중에는 will_paginate이 많이 쓰이는 것으로 알고 있었다.
다운로드 수 2,000만을 넘는 유명한 gem이다.
여러 pagination gem을 비교해보던 중 kaminari를 발견하게 되었다.
다운로드 수는 3,000만을 넘는다.
설명 페이지의 첫 줄 Does not globally pollute Array, Hash, Object or AR::Base이 마음에 들어서 써보기로 했다.

# 설치 및 설정

공식 문서에 설명이 잘 되어있지만, 기록할 겸 적어본다.

## gem 설치

{% highlight ruby %}
# Gemfile
gem 'kaminari'
{% endhighlight %}

{% highlight bash %}
$ bundle
{% endhighlight %}

## 설정

kaminari config 파일 생성

{% highlight bash %}
$ rails generate kaminari:config
{% endhighlight %}

파일에서 설정 값 적용

{% highlight ruby %}
# app/config/initializers/kaminari_config.rb
default_per_page      # 25 by default
max_per_page          # nil by default
max_pages             # nil by default
window                # 4 by default
outer_window          # 0 by default
left                  # 0 by default
right                 # 0 by default
page_method_name      # :page by default
param_name            # :page by default
params_on_first_page  # false by default
{% endhighlight %}

## Controllers 수정

{% highlight ruby %}
@users = User.order(:name).page params[:page]
{% endhighlight %}

## View 파일에 페이지네이션 부분 추가

{% highlight html %}

<%= paginate @users %>

{% endhighlight %}

페이지네이션 customizing을 위해서 views 파일을 만들어준다.

{% highlight bash %}
$ rails generate kaminari:views default
{% endhighlight %}

## /page/:page routes 사용하기

이 부분은 옵션이다.
하지만, ? 이후 parameter로 넘기는 것 보다는 /page/:page을 사용하는 것이 더 좋다.
Ruby on Rails 4 이후 버전에서는 concern 기능을 사용할 수 있다.

{% highlight ruby %}
# /config/routes.rb
concern :paginatable do
  get '(page/:page)', action: :index, on: :collection, as: ''
end

resources :my_resources, concerns: :paginatable
{% endhighlight %}

# 참고

* <https://github.com/kaminari/kaminari>
* <https://rubygems.org/gems/kaminari>