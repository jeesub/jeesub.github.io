---
layout: post
title: "elastic beanstalk으로 ruby on rails deploy 하기"
categories: [rails, aws]
---

# Elastic Beanstalk

Elastic Beanstalk은 AWS의 EC2, DBS, CloudWatch, Auto Scaling 등을 편리하게 활용할 수 있도록 해준다.
Elastic Beanstalk을 사용하면 EC2를 세팅하고, DBS를 연결하고, Deploy 하는 과정을 한번에 진행할 수 있다.
Elastic Beanstalk을 사용해서 Ruby on Rails 웹사이트를 deploy해보았다.

# Deploy

## 1. Ruby on Rails Application 생성

{% highlight bash %}
$ rails new sample_app
{% endhighlight %}

## 2. Gemfile에 PostgreSQL 추가

{% highlight ruby %}
gem 'pg'
{% endhighlight %}

## 3. database.yml 설정

{% highlight ruby %}
{% raw %}
# /config/database.yml

default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  timeout: 5000

development:
  <<: *default
  database: sample_app_development
  host: localhost
  port: 5432

test:
  <<: *default
  database: sample_app_test
  host: localhost
  port: 5432

production:
  <<: *default
  database: <%= ENV['RDS_DB_NAME'] %>
  username: <%= ENV['RDS_USERNAME'] %>
  password: <%= ENV['RDS_PASSWORD'] %>
  host: <%= ENV['RDS_HOSTNAME'] %>
  port: <%= ENV['RDS_PORT'] %>
{% endraw %}
{% endhighlight %}

## 4. Controller, Model, View 생성

{% highlight bash %}
$ rails generate scaffold Post title:string content:text
{% endhighlight %}

## 5. migration 및 running 테스트

{% highlight bash %}
$ rails db:create
$ rails db:migrate
$ rails server
{% endhighlight %}

## 6. secret key 생성

{% highlight bash %}
$ rake secret
{% endhighlight %}

생성된 secret key는 나중에 Elastic Beanstalk에서 사용한다.

## 7. AWS 가입, Elastic Beanstalk 새 애플리케이션 생성

* 기본 구성: 미리 구성된 플랫폼에서 Ruby 선택
* 애플리케이션 코드: 코드 업로드. Local 환경에서 만든 sample_app을 압축해서 업로드 한다.
* 추가 구성: DB 연결을 선택하고, PostgreSQL DB를 생성한다.

## 8. SECRET_KEY 설정

구성 - 소프트웨어 - 환경 속성에 새로운 변수 key, value를 입력한다.
key는 SECRET_KEY_BASE, 값은 아까 생성한 secret key를 입력한다.

## 9. 완료

URL/posts 접속을 통해 동작을 확인한다.

# 참고

* <https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/GettingStarted.html>
* <https://aws.amazon.com/ko/getting-started/tutorials/launch-an-app/?trk=gs_card>
* <https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/create_deploy_Ruby.rds.html>