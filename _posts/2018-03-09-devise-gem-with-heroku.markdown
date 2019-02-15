---
layout: post
title:  "devise gem with heroku"
categories: [rails, heroku]
---

# devise
Ruby on Rails application의 유저 관리를 도와주는 gem이다. <br />
<https://github.com/plataformatec/devise>

## gemfile 설정

{% highlight ruby %}
gem 'devise'
{% endhighlight %}

## bundle install

{% highlight bash %}
$ bundle install
{% endhighlight %}

## devise 설치
{% highlight bash %}
$ rails generate devise:install
{% endhighlight %}

## host 설정

{% highlight ruby %}
# /config/environments/development.rb
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
{% endhighlight %}
개발 IDE로 cloud9를 사용하고 있는데, cloud9은 mail 발송이 막혀있다. 테스트 환경에서는 로그를 통해 메일 confirm을 진행할 수 있다.

## model 생성(ex_ Admin model)

{% highlight bash %}
rails generate devise Admin
{% endhighlight %}

## 여러 model을 사용하기 위한 view 분리 설정

{% highlight ruby %}
# /config/initializers/devise.rb
config.scoped_views = true
{% endhighlight %}

## mail sender 주소 변경

{% highlight ruby %}
# /config/initializers/devise.rb
config.mailer_sender = 'please-change-me-at-config-initializers-devise@example.com'
{% endhighlight %}

## view 생성
{% highlight bash %}
$ rails generate devise:views admins
{% endhighlight %}

## model에서 confirmation 활성화<br />
mail confirmation을 사용할 경우에만 설정해주면 된다.

{% highlight ruby %}
# app/models/admin.rb
class Admin < ApplicationRecord
  devise :database_authenticatable, :registerable,
    :recoverable, :rememberable, :trackable, :validatable,
    :confirmable
end
{% endhighlight %}

## migrate file에 주석처리 된 메일 confirmation을 활성화

{% highlight ruby %}
# /db/migrate/xxxxxxxx.rb
## Confirmable
t.string   :confirmation_token
t.datetime :confirmed_at
t.datetime :confirmation_sent_at
t.string   :unconfirmed_email
 
add_index :admins, :confirmation_token,   unique: true
{% endhighlight %}

## db migrate

{% highlight bash %}
$ rails db:migrate
{% endhighlight %}

설치가 완료 되면, 다양한 helper를 사용할 수 있다.

{% highlight ruby %}
before_action :authenticate_member!
member_signed_in?
current_member
member_session
{% endhighlight %}

rails routes를 통해 생성된 routes를 살펴보고 활용하면 끝.

{% highlight bash %}
$ rails routes
{% endhighlight %}

## 추가. admin email 검증 설정
admin을 만들 경우, 특정 도메인의 메일로만 가입이 가능하도록 해야 한다.
직접 model을 만들었을 때와 마찬가지로, model 파일에 메일 주소를 검증하는 코드를 넣어주면 된다.
정규식을 원하는 검증 형태로 바꾸어 사용하면 된다.

{% highlight ruby %}
# /app/models/admin.rb
EMAIL_REGEX = /\A[\w+\-.]+@yourdomain+\.com+\z/i
validates :email, format: { with: EMAIL_REGEX }
{% endhighlight %}

# devise with heroku
하지만 이대로는 heroku에서 production mode로 사용이 불가능하다.
confirm mail을 보낼 수 없기 때문이다.
add-on을 추가함으로써 해결할 수 있다.

## sendgrid 추가

{% highlight bash %}
$ heroku addons:create sendgrid:starter
{% endhighlight %}

<https://devcenter.heroku.com/articles/sendgrid>

## 설정 확인

{% highlight bash %}
$ heroku config:get SENDGRID_USERNAME
{% endhighlight %}

heroku add-on 설정시 자동으로 입력된 변수 출력을 확인한다.

## SMTP 설정

{% highlight ruby %}
# /config/environments/production.rb
config.action_mailer.raise_delivery_errors = true
config.action_mailer.delivery_method = :smtp
host = '<your-domain.com>'
config.action_mailer.default_url_options = { host: host }
ActionMailer::Base.smtp_settings = {
    :address        => 'smtp.sendgrid.net',
    :port           => '587',
    :authentication => :plain,
    :user_name      => ENV['SENDGRID_USERNAME'],
    :password       => ENV['SENDGRID_PASSWORD'],
    :domain         => '<<your-domain.com>>',
    :enable_starttls_auto => true
}
{% endhighlight %}

# 참고
* <https://github.com/plataformatec/devise>
* <https://www.railstutorial.org/book/account_activation>
* <https://guides.rubyonrails.org/action_mailer_basics.html>
* <https://devcenter.heroku.com/articles/sendgrid>