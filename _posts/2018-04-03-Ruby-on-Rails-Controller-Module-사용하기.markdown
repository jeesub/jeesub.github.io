---
layout: post
title:  "Ruby on Rails Controller Module 사용하기"
categories: rails
---

### Controller Module
Ruby on Rails application을 만들다보면, Controller가 많아진다.
이 때 module로 관리하면 정돈해서 사용할 수 있다.

### 기본적인 module 생성법
{% highlight bash %}
$ rails generate controller Admin::Posts
{% endhighlight %}

위와 같은 명령어를 통해 app/controllers/admin/posts_controller.rb를 생성할 수 있다.<br>
view 파일들은 app/views/admin/posts/에 만들면 된다.<br>
view helper의 경우, admin_posts_path, admin_post_path(:id)와 같은 형태가 된다.<br>
<br>
scaffold로 만든 파일들을 모듈로 관리하려고 변경할 경우, view 파일의 path들을 잘 수정해줘야 한다.<br>
다음과 같이 scaffold로 만들어진 요소들을
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

form의 경우
{% highlight ruby %}
form_with(model: post, local: true) do |f|
{% endhighlight %}
와 같이 되어있는 form의 시작 부분을 변경해준다.
{% highlight ruby %}
form_with(model: [ :admin, @post ], local: true) do |f|
{% endhighlight %}

controller의 redirect_to method에서도 helper들을 변경해주어야 한다.
<br>
* scaffold로 만들었을 때, 수정해야할 파일들
<br>
index.html.erb, new.html.erb, show.html.erb, edit.html.erb, _form.html.erb, posts_controller.rb
<br>

참고<br>
<http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html#method-i-form_with>