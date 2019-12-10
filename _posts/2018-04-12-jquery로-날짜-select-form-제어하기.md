---
layout: post
title:  "jquery로 날짜 select form 제어하기"
categories: [web-development, javascript]
---

# javascript 날짜 format

{% highlight javascript %}
var date = new Date();			// 2018-04-12
var year = date.getFullYear();  // 2018
var month = date.getMonth();    // 3
var date = date.getDate();      // 12
{% endhighlight %}

javascript의 날짜 값은 new Date()를 통해 만들 수 있다. 
그런데, 특이한 점은 '월'의 경우 0..11의 값을 가진다는 것이다. 
영어권 문화에서는 달마다 이름을 붙이기 때문에 array에 저장하기 위해서 인 것 같다. 

new Date() 안에 날짜 형식을 넣어주면, 원하는 날짜를 지정할 수 있다. 

{% highlight javascript %}
var date = new Date("2020-01-01");
// 2020-01-01
{% endhighlight %}

# jQuery로 selectbox의 날짜 제어하기

users table의 birthday 날짜를 원하는 날짜로 바꾸는 코드 예제 

{% highlight html %}
<script>
  // 2016-09-03
  $("#user_birthday_1i").val("2016");
  $("#user_birthday_2i").val("9");
  $("#user_birthday_3i").val("3");
</script>
{% endhighlight %}

val()로 월을 지정할때는 javascript와는 다르게 실제 월을 넣어주면 된다. 