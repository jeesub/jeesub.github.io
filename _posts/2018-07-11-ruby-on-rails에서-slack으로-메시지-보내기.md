---
layout: post
title:  "Ruby on Rails에서 slack으로 메시지 보내기"
categories: [web-development, ruby-on-rails]
---

Ruby on Rails 어플리케이션에서 특정 이벤트 발생시 slack으로 알림을 주는 간단한 기능을 구현하려고 한다. 

# slack 메시지

slack에 메시지를 보내기 위해서는 세 가지 중 한 방법을 사용하면 된다. 

1. slack 어플리케이션을 이용해 메시지를 보낸다. 
2. slack Web API를 사용한다. 
3. slack incoming webhooks를 사용한다. 

참고: <https://api.slack.com/docs/messages>


slack Web API는 slack의 다양한 기능을 외부에서 제어할 때 유용하다. 
간단한 메시지만을 전달하고자 하면 slack incoming webhooks로 충분하다. 
일단은 메시지만 전달하기 위해 incoming webhook을 사용해보았다. 

# slack incoming webhooks

<https://api.slack.com/incoming-webhooks>

slack 공식 문서에 따르면, 총 네 단계를 따르면 끝이 난다.

1. slack app을 만든다. 
2. incoming webhook을 활성화한다. 
3. incoming webhook을 만든다. 
4. incoming webhook을 사용한다. 

## 1. slack app을 만든다.

<https://api.slack.com/apps/new>로 접속해서 새로운 앱을 만든다. 
앱 이름을 정해주고, 앱을 사용하고자 하는 workspace를 선택한다. 

## 2. incoming webhook을 활성화한다. 

앱을 선택하고 나오는 화면에서 incoming webhook을 선택하고 활성화한다. 

## 3. incoming webhook을 만든다. 

활성화 화면에서 맨 아래로 내려가면 Add New Webhook to Workspace 버튼이 있다. 
클릭해서 새로운 webhook을 만든다. 
post 채널을 선택하도록 나오는데, 실험용 채널을 먼저 선택해서 테스트하고, 정상 작동하면 실제 채널에 적용하면 된다. 

## 4. incoming webhook을 사용한다. 

incoming webhook을 만들면 URI가 하나 주어진다. 이 URI로 post 요청을 보내면 사용이 된다. 

{% highlight bash %}
$ curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' https://hooks.slack.com/services/XXXXX/XXXX/XXXX
{% endhighlight %}

본인의 설정에 맞게 테스트해보면, slack 메시지를 받을 수 있다. 

# Ruby on Rails에서 POST 요청하기

Ruby on Rails 어플리케이션과 연동하려면, ruby의 net::http를 활용하면 된다. 
slack API 문서에 주어진 요소들을 넣어서 ruby code로 만들었다. 

{% highlight ruby %}
require 'net/http'

uri = URI("https://hooks.slack.com/services/XXXXX/XXXX/XXXX")

Net::HTTP.start(uri.host, uri.port, :use_ssl => true) do |http|
  req = Net::HTTP::Post.new(uri)
  req.content_type = 'application/json'
  req.body = "{'text':'Hello, World!'}"
  http.request(req)
end
{% endhighlight %}

참고: <https://ruby-doc.org/stdlib-2.5.1/libdoc/net/http/rdoc/Net/HTTP.html>

ruby의 http 접속 기능을 활용하기 때문에, 안정적으로 사용하려면 active job, queue 등을 활용하는 것이 좋을 것 같다. 