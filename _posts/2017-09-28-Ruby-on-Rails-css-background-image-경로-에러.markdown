---
layout: post
title:  "Ruby on Rails css background-image 경로 에러"
categories: rails
---
background-image를 적용시키기 위해 css 파일에 위와 같은 코드를 넣었다.
{% highlight css %}
background-image: url(/assets/image.png);
{% endhighlight %}
local 테스트에서는 제대로 적용되었지만, product 모드에서는 이미지가 나오지 않았다.
이는 이미지 주소 뒤에 붙는 hash값을 제대로 받아오지 못했기 때문이다.
rails는 asset pipeline을 사용하는데, 이 때 hash값이 생긴다.
개발자도구를 통해 rails application의 이미지를 보면 `69adcb7be4b13d1e0cc20d6aca...`와 같이 이미지의 주소 뒤에 hash가 붙어 있는 것을 확인할 수 있다.<br>
asset pipeline: <http://guides.rubyonrails.org/asset_pipeline.html>
<br><br>

# Sprockets 활용하기
sass를 이용 중이라면 쉽게 해결할 수 있다.<br>
{% highlight css %}
background-image: image-url("image.png")
{% endhighlight %}
와 같이 넣어주면 제대로 된 경로를 불러와준다.<br><br>

# 참고
* <https://stackoverflow.com/questions/15257555/how-to-reference-images-in-css-within-rails-4>