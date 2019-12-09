---
layout: post
title: "Ruby on Rails test"
categories: [web-development, ruby-on-rails]
---

# test

Ruby on Rails는 테스트 자동생성을 포함하고 있다.
Model이나 Controller가 생성될 때 skeleton test code를 함께 만들기 때문에 쉽게 테스트를 작성하고 진행할 수 있다.
test 관련 파일들은 /test/ 안에 존재한다.

# fixtures

Ruby on Rails가 테스트를 진행할 때 data는 DB에서 가져오지 않는다.
/test/fixtures/에 위치한 fixtures에서 가져오게 된다.
그렇기 때문에 Model 테스트를 위해서는 fixtures를 미리 설정해야 한다.
fixtures는 테스트할 때 사용할 만큼만 생성하면 된다.
ERB도 사용할 수 있기 때문에, 여러 데이터가 필요할 경우 반복문을 활용할 수 있다.
아래의 fixture는 예시이다.

{% highlight yml %}
one:
  title: MyString
  description: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  posted_at: 2019-02-13
  category: 1
{% endhighlight %}

참고: <https://api.rubyonrails.org/v2.3/classes/Fixtures.html>

# models test

/test/models/에 위치한다.
MVC의 M에 해당하는 테스트를 진행한다.

{% highlight ruby %}
setup do
  @post = Post.new(title: "title", description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.", posted_at: Time.now, category: 1)
end

test "should be valid" do
  assert @post.valid?
end

test "title should be present" do
  @post.title = "   "
  assert_not @post.valid?
end

test "title should be shorter than 60" do
  @post.title = "a" * 61
  assert_not @post.valid?
end

test "category should be integer" do
  invalid_categories = ["a", 2.71828]
  invalid_categories.each do |invalid_category|
    @post.category = invalid_category
    assert_not @post.valid?, "#{invalid_category.inspect} is invalid."
  end
end

{% endhighlight %}

# controllers test

/test/controllers/에 위치한다.
MVC 패턴의 C, V에 해당하는 테스트를 진행한다.

## request handling test

controller가 수행하는 기능에 대한 테스트를 진행한다.
get, post, patch, put, head, delete에 대해 진행할 수 있다.

{% highlight ruby %}
setup do
  @post = posts(:one)
end

test "should get index" do
  get posts_url
  assert_response :success
end

test "should show post" do
  get post_url(@post)
  assert_response :success
end

test "should create post" do
  assert_difference('Post.count') do
    post posts_url, params: { post: { title: @post.title, description: @post.description, posted_at: @post.posted_at, category: @post.category }}
  end
  assert_redirect_to post_url(@post)
end

test "should update post" do
  patch posts_url(@post), params: { post: { title: @post.title, description: @post.description, posted_at: @post.posted_at, category: @post.category }}
  assert_redirected_to post_url(@post)
end

test "should destroy post" do
  assert_difference('Post.count', -1) do
    delete post_url(@post)
  end
  assert_redirected_to posts_url
end
{% endhighlight %}

## routes test

Routing 테스트.
routes 선언이 제대로 되어 있는지 확인한다.

{% highlight ruby %}
test "should get home" do
  get root_url
  assert_response :success
end

test "should get about" do
  get about_url
  assert_response :success
end
{% endhighlight %}

## views test

View에 대한 테스트도 /test/controllers/ 안에서 진행한다.
assert_selector를 활용하여 여러 요소를 테스트할 수 있다.

{% highlight ruby %}
test "should display home title"
  get root_path
  assert_select "title", "섭사장의 블로그"
end

test "should provide links" do
  get root_path
  assert_select "a[href=?]", root_path, count: 2
  assert_select "a[href=?]", about_path
end
{% endhighlight %}

# helpers test

Ruby on Rails helper에 대한 테스트를 진행한다.
Helper는 app/helpers에 있으며, 주로 application의 view에서 사용하는 module이다.
helpers에 대한 테스트는 /test/helpers에 위치한다.

{% highlight ruby %}
test "should return the full title" do
  assert_equal full_title("About"), "About | 섭사장의 블로그"
end
{% endhighlight %}

# integration test

Integration test는 workflow를 테스트 한다.
/test/integration에 위치한다.
아래 명령어를 통해 생성할 수 있다.

{% highlight bash %}
$ rails generate integration_test user_flows
{% endhighlight %}

앞에서 사용한 다양한 테스트들을 조합해 만들어 사용한다.

# 참고

* <https://guides.rubyonrails.org/testing.html>