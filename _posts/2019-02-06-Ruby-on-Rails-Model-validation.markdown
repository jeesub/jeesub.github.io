---
layout: post
title: "Ruby on Rails Model validation"
categories: rails
---

#### Model validation

Ruby on Rails의 MVC 패턴 중 M에 해당하는 Model에서는 data validation을 적용하게 된다.
Database에 data를 저장 혹은 업데이트하기 전, 적절한 data인지 확인한다.
이 때, validation을 통과하지 못하면 Query를 보내지 않는다.

Ruby on Rails를 사용하며 자주 활용한 Model validation을 모아보았다.

##### required validation

{% highlight ruby %}
validates :title, :description, :tags, presence: true
{% endhighlight %}

##### uniqueness validation

{% highlight ruby %}
validates :sequence, uniqueness: true
# case insensitive
validates :permalink, uniquness: { case_sensitive: false }
{% endhighlight %}

##### length validation

{% highlight ruby %}
# 최단
validates :title, length: { minimum: 5 }
# 최장
validates :content, length: { maximum: 40 }
# 범위
validates :phone, length: { in: 10.. 15 }
# 딱 정해진 길이
validates :pin, length: { is: 6 }
{% endhighlight %}

##### format validation

{% highlight ruby %}
# 숫자
validates :amount, numericality: true
# 정수
validates :sequence, numericality: { only_integer: true }
# http 혹은 https로 시작(allow nil 포함)
validates :url,
	format: { with: URI.regexp(%w(http https)) },
		allow_nil: true
# 유효한 email 주소
EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
	validates :email, 
		length: { in: 6..50 }, 
		format: { with: EMAIL_REGEX }
{% endhighlight %}

##### conditional validation

{% highlight ruby %}
validates :url,
	format: { with: URI.regexp(%w(http https)) },
		if: Proc.new { |company| !company.url.blank? }
{% endhighlight %}

##### inclusion validation

{% highlight ruby %}
validates :language, inclusion: { in: %w(ruby phtyon java c) }
{% endhighlight %}

#### 참고
<https://guides.rubyonrails.org/active_record_validations.html>