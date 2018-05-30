---
layout: post
title:  "Ruby on Rails - test with devise gem"
categories: rails
---

Rails test를 하다보면, session 상태에 따른 테스트를 해야할 경우가 많다.
devise에서는 이를 위한 helper를 제공한다.
공식문서를 참고했지만, 다양한 경우에 대한 문서는 없어서 조금 애를 먹었다.


### include 설정

controller test에 넣어도 되지만, 거의 모든 controller test에 쓰이기 때문에 test_helper에 넣어주었다.<br>

{% highlight ruby %}
# /test/test_helper.rb
include Devise::Test::IntegrationHelpers
{% endhighlight %}

### controller test 설정

각각의 test.rb 파일에서 로그인 되었을 경우를 설정해주었다.
여러 모델을 사용하는 경우, scope을 지정해줘야 한다.

{% highlight ruby %}
setup do
  sign_in users(:duck), scope: :user
end
{% endhighlight %}

### yml 설정

공식 문서에서 찾기 힘든 부분이 yml 설정이었다.
본인의 model에 맞게 설정해주어야 한다.
confirmation을 사용할 경우, confirmed_at을 꼭 넣어줘야 에러가 나지 않는다.

{% highlight ruby %}
duck:
  name: duck
  email: duck@duck.com
  encrypted_password: <%= Devise::Encryptor.digest(User, '1234567890') %>
  confirmed_at: <%= Time.zone.now %>
{% endhighlight %}