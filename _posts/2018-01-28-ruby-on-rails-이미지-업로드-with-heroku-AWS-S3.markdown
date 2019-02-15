---
layout: post
title:  "Ruby on Rails 이미지 업로드 with heroku, AWS S3"
categories: [rails, heroku, aws]
---
heroku에서 돌아가고 있는 RoR 어플리케이션의 특정 Model에 이미지를 추가하기로 했다.
그리고 선택한 방법은 AWS S3로 이미지를 저장하는 것.

# gem
Gemfile에 필요한 gem을 추가한다.

{% highlight ruby %}
# Gemfile
gem 'carrierwave', '1.2.2'
gem 'mini_magick', '4.7.0'
group :production do
    gem 'fog', '1.42'
end
{% endhighlight %}

{% highlight bash %}
$ bundle install
{% endhighlight %}

* carrierwave: 파일 업로드 gem - <https://github.com/carrierwaveuploader/carrierwave><br>
* mini_magick: 이미지 편집 gem - <https://github.com/minimagick/minimagick><br>
* fog: cloud에 파일 업로드 gem - <https://github.com/fog/fog><br>

# uploader
uploader를 생성한다.

{% highlight bash %}
$ rails generate uploader Picture
{% endhighlight %}

예시를 위해 기본적인 요소들을 생성했다.

{% highlight bash %}
$ rails generate scaffold Post post:text picture:string
$ rails db:migrate
{% endhighlight %}

Model에 uploader를 적용한다.

{% highlight ruby %}
# app/models/post.rb
class Post < ApplicationRecord
    mount_uploader :picture, PictureUploader
end
{% endhighlight %}

# View

form field를 수정해준다. accept option을 통해 파일 validation을 적용할 수 있다.

{% highlight ruby %}
{% raw %}
# app/views/posts/_form.html.erb
<%= f.file_field :picture, accept: 'image/jpeg,image/gif,image/png' %>
{% endraw %}
{% endhighlight %}

이미지 태그를 생성해준다.
{% highlight ruby %}
# app/views/posts/index.html.erb
<%= image_tag(post.picture.url, alt: post.name) if post.picture? %>
{% endhighlight %}


# validation

uploader validation

{% highlight ruby %}
# app/uploaders/picture_uploader.rb
class PictureUploader < CarrierWave::Uploader::Base
    def extension_whitelist
        %w(jpg jpeg gif png)
    end
end
{% endhighlight %}

Model validation

{% highlight ruby %}
# app/models/teammate.rb
class Post < ApplicationRecord
  validate  :picture_size
  private
    def picture_size
      if picture.size > 1.megabyte
        errors.add(:picture, "1MB 이하 사진을 선택해주세요.")
      end
    end
end
{% endhighlight %}

jquery validation

{% highlight html %}
# app/views/teammates/_form.html.erb
<script type="text/javascript">
  $('#post_picture').bind('change', function() {
    var pictureSize = this.files[0].size/1024/1024;
    if (pictureSize > 1) {
      alert('1MB 이하 사진을 선택해주세요.');
    }
  });
</script>
{% endhighlight %}


# Imagemagick - 리사이징

Imagemagick 설치 

{% highlight bash %}
# Ubuntu
$ sudo apt-get install imagemagick
# Mac OS
$ brew install imagemagick
{% endhighlight %}

Resize 설정 및 production mode에서만 cloud 업로드 설정

{% highlight ruby %}
# app/uploaders/picture_uploader.rb
class PictureUploader < CarrierWave::Uploader::Base
    include CarrierWave::MiniMagick
    process resize_to_limit: [400, 400]
    if Rails.env.production?
        storage :fog
    else
        storage :file
    end
end
{% endhighlight %}

# AWS S3

AWS 가입, S3 bucket 생성.
region은 seoul로 했다.
<br>
주의할점: butcket 이름에 "."이 들어가면 Rails가 경로를 제대로 읽어오지 못해 에러가 난다.

carrier wave 설정

{% highlight ruby %}
# /app/config/initializers/carrier_wave.rb
if Rails.env.production?
  CarrierWave.configure do |config|
    config.fog_credentials = {
      :provider              => 'AWS',
      :aws_access_key_id     => ENV['S3_ACCESS_KEY'],
      :aws_secret_access_key => ENV['S3_SECRET_KEY'],
      :region                => 'ap-northeast-2'
    }
    config.fog_directory     =  ENV['S3_BUCKET']
  end
end
{% endhighlight %}

* region은 본인이 사용중인 S3의 region을 기입한다.<br>
region 찾기 - <https://docs.aws.amazon.com/ko_kr/general/latest/gr/rande.html>

heroku config. 보안을 위해, 파일에 직접 기입하지 않는다.

{% highlight bash %}
$ heroku config:set S3_ACCESS_KEY=<access key>
$ heroku config:set S3_SECRET_KEY=<secret key>
$ heroku config:set S3_BUCKET=<bucket name>
{% endhighlight %}

테스트용 업로드는 .gitignore
{% highlight bash %}
# .gitingore
/public/uploads
{% endhighlight %}


완료. heroku에 upload한 후 db:migrate을 해주면 끝이 난다.

{% highlight bash %}
$ heroku run rails db:migrate
{% endhighlight %}

# 참고
* <https://www.railstutorial.org/>
* <https://github.com/carrierwaveuploader/carrierwave>
* <https://github.com/minimagick/minimagick>
* <https://github.com/fog/fog>