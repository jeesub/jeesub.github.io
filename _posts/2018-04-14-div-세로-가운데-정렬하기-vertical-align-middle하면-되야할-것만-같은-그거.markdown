---
layout: post
title:  "div 세로 가운데 정렬하기(vertical align: middle하면 되야할 것만 같은 그거)"
categories: css
---

# div 세로 가운데 정렬

div 안의 div를 세로 가운데에 정렬하려는 시도는 오래전부터 있었지만, 계속 어려움으로 남아있다. w3 school, stack over flow등을 뒤져봐도 lineheight를 준다던지 하는 다양한 편법(?)들을 통해 구현한다.

고정된 height에서는 다양한 편법들을 활용하면 쉽게 해결할 수 있지만, 요즘 유행하는 반응형 height에서는 위의 편법들이 무용지물이다.

그대신 flexbox를 활용하면 세로 가운데 정렬을 할 수 있다.

단, 구형 브라우저에서는 지원하지 않으니, 사용에 유의해야 한다. 익스플로러는 11부터 지원한다.

![미니언즈인가]({{ "/assets/img/2018-04-01/01.png" | relative_url }}) <br />
위 그림과 같이 민트색 div 안에 미니언즈 뒤집어 놓은듯한 div 두개를 위치시키고자 한다.

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
  <style>
    .flex-container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #66ffcc;
      flex-direction: column;
    }
    .a {
      background-color: #99ccff;
      width: 100px;
      height: 100px;
    }
    .b {
      background-color: #ffff66;
      width: 100px;
      height: 100px;
    }
  </style>
</head>
<body>
  <div class="flex-container">
    <div class="a"></div>
    <div class="b"></div>
  </div>
</body>
</html>
{% endhighlight %}

감싸고 있는 div에 display: flex, align-items: center를 적용하면 안의 div들이 가운데에 위치하게 된다.

flex-direction: column을 적용하면, 안의 div가 세로로 정렬된다.