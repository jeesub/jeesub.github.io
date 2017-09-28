---
layout: post
title:  "Ruby on Rails css background-image 경로 에러"
categories: RoR
---
문제가 발생한 application은 heroku에서 돌아가고 있다.<br>
<br>
~~~
background-image: url(/assets/image.png);
~~~
div에 background-image를 적용시키기 위해 css 파일에 위와 같은 코드를 넣었다.
local 테스트에서는 제대로 적용되었지만, product 모드에서는 이미지가 나오지 않았다.
문제의 원인은 이미지 주소 뒤에 붙는 hash값을 제대로 받아오지 못했기 때문이다.<br>
<br>
개발자도구를 통해 rails application의 이미지를 보면 `69adcb7be4b13d1e0cc20d6aca...`와 같이 이미지의 주소 뒤에 hash가 붙는다.
제대로 된 hash 값이 붙은 이미지 주소를 가져오면 해결 가능하다.

#### Sprockets 활용하기
sass를 이용 중이라면 쉽게 해결할 수 있다.<br>
~~~
background-image: image-url("image.png")
~~~
와 같이 넣어주면 제대로 된 경로를 불러와준다.<br><br>
참고<br>
<https://stackoverflow.com/questions/15257555/how-to-reference-images-in-css-within-rails-4>
