---
layout: post
title:  "Ruby on Rails 연결되는 model 사용하기"
categories: rails
---

# 연결되는 model
post와 댓글이 있다면, post와 댓글은 서로 연결되어 있다.
댓글은 post 없이는 존재할 수 없다.
이런 경우를 Ruby on Rails에서는 association이라고 표현한다.<br>
참고: <http://guides.rubyonrails.org/association_basics.html><br>

# references
댓글은 post 없이는 만들어질 수 없다.
post가 먼저 있고, 해당 post에 대한 댓글만 만들 수 있다.
댓글은 post를 reference로 한다.

{% highlight bash %}
$ rails generate model Reply content:text post:references
{% endhighlight %}

# has_many, belongs_to
post는 여러 개의 댓글을 가질 수 있고, 댓글은 하나의 post에만 속해야 한다.
이럴 경우, post는 'has_many' 댓글이고, 댓글은 'belongs_to' post이다.

{% highlight ruby %}
class Post < ApplicationRecord
  has_many :replies
end
{% endhighlight %}

{% highlight ruby %}
class Reply < ApplicationRecord
   belongs_to :post
end
{% endhighlight %}

# dependent: :destroy
post가 삭제된다면, 댓글도 지워져야 한다.
post 없이 댓글 혼자서는 존재할 수 없기 때문이다.

{% highlight ruby %}
class Post < ApplicationRecord
  has_many :replies, dependent: :destroy
end
{% endhighlight %}

# post가 있을 경우, reply 만들기

{% highlight bash %}
$ rails generate model Reply content:text post:references
{% endhighlight %}

{% highlight ruby %}
# app/models/post.rb
class Post < ApplicationRecord
  has_many :replies, dependent: :destroy
end
{% endhighlight %}

{% highlight bash %}
$ rails db:migrate
{% endhighlight %}

이후 본인의 application에 맞게 routes 설정을 해주고, create, edit, destroy등의 controller action과 view page들을 추가해주면 된다.

# Routes
association을 사용할 때, nested URL을 쓰면 편하다.

{% highlight ruby %}
# routes.rb
resources :posts do
  resources :replies
end
{% endhighlight %}

위와 같이 routes 설정을 해주면, <code>/posts/1/replies/2</code>와 같이 사용할 수 있다.
이렇게 설정할 경우, new, create, destroy 등의 action에서 post의 정보를 쉽게 활용할 수 있다.

# Controller

{% highlight ruby %}
before_action :set_post

def new
  @reply = @post.replies.build
end

def create
  @reply = @post.replies.build(reply_params)
  if @reply.save
    redirect_to post_reply_path(@post, @reply)
  else
    render :new
  end
end

private
  def set_post
    @post = Post.find(params[:post_id])
  end
{% endhighlight %}

실제 어플리케이션에서는 post의 show action에 form이 들어가기 때문에 new action이 필요 없겠지만, 예시로 적었다.
association을 사용할 경우 <code>@post.replies.build</code>와 같이 두 개체를 연결해서 사용할 수 있고, build가 new method와 같은 역할을 해준다.