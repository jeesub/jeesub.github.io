---
layout: post
title:  "Ruby on Rails Controller Module 사용하기"
categories: rails
---

### Controller Module
Ruby on Rails application을 만들다보면, Controller가 많아진다.
이 때 module로 관리하면 정돈해서 사용할 수 있다.

### 시작부터 controller module 생성하기

{% highlight bash %}
$ rails generate controller Admin::Posts
{% endhighlight %}

위와 같은 명령어를 통해 app/controllers/admin/posts_controller.rb를 생성할 수 있다.<br />
view 파일들은 app/views/admin/posts/에 만들면 된다.<br />
view helper의 경우, admin_posts_path, admin_post_path(:id)와 같은 형태가 된다.

### 이미 사용중인 View, Controller를 module로 변경하는 법
scaffold로 만든 파일들을 모듈로 관리하려고 변경할 경우, routes, View files, Controller files, test files를 수정해야 한다.

#### controller module로 바꾸기
controller 파일의 위치를 /app/controllers/admin/ 아래로 옮겨준다.<br />
그리고 class 상속을 다음과 같이 바꿔준다.

{% highlight ruby %}
class Admin::PostsController < ApplicationController
{% endhighlight %}
<br />
해당하는 view 파일들도 app/views/admin/ 아래로 옮겨준다.

#### routes 수정하기
/admin/post URL을 사용하고자 하기 위해 routes.rb 파일을 다음과 같이 수정한다.
namespace 안에 다른 controller들을 넣으면 마찬가지로 /admin/ URL을 사용할 수 있다.
{% highlight ruby %}
namespace :admin do
	resources :posts
 end
{% endhighlight %}

#### view 파일의 path 수정하기
view 파일의 path들을 잘 수정해줘야 한다.<br>
다음과 같이 사용하던 path 요소들을

{% highlight ruby %}
@posts.each do |post|
  link_to 'Show', post
  link_to 'Edit', edit_post_path(post)
  link_to 'Destroy', post, method: :delete
end
{% endhighlight %}

아래와 같이 수정한다.

{% highlight ruby %}
@posts.each do |post|
  link_to 'Show', admin_post_path(post)
  link_to 'Edit', edit_admin_post_path(post)
  link_to 'Destroy', admin_post_path(post), method: :delete
end
{% endhighlight %}

#### form 수정하기
form의 경우

{% highlight ruby %}
form_with(model: post, local: true) do |f|
{% endhighlight %}

와 같이 되어있는 form의 시작 부분을 변경해준다.

{% highlight ruby %}
form_with(model: [ :admin, @post ], local: true) do |f|
{% endhighlight %}

#### controller redirect 수정하기
controller의 redirect_to method에서도 helper들을 변경해주어야 한다.<br />

##### * scaffold로 만들었을 때, 수정해야할 파일들
routes.rb, posts_controller.rb, index.html.erb, new.html.erb, show.html.erb, edit.html.erb, \_form.html.erb

#### test files 수정하기
/test/controllers 안에 /admin 폴더를 만들고, test files를 옮겨준다.<br />
class 상속을 다음과 같이 바꿔준다.

{% highlight ruby %}
class Admin::PostsControllerTest < ActionDispatch::IntegrationTest
{% endhighlight %}

#### 참고
<http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html#method-i-form_with>