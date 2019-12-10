---
layout: post
title:  "sublime text 자동완성 snippet 사용하기"
categories: etc
---

# snippet - 스니펫
스니펫이란, 단축키를 통해 자주 쓰는 문구를 자동 완성하는 기능이라고 생각하면 될 것 같다.<br>
참고: <https://ko.wikipedia.org/wiki/스니펫><br>
sublime text 3에서는 문구 + Tab을 통해 스니펫을 이용할 수 있다.
jekyll 블로그를 사용하다 보니 마크다운 형식을 많이 사용한다. 이 중 highlight 기능을 자동화 했다.<br>
[메뉴 - Tools - Snippets]에 보면 사용 가능한 snippet을 확인할 수 있다.<br>


# 새로운 스니펫 등록
새로운 스니펫의 등록은 [메뉴 - Tools - Developer - New Snippet...]에서 할 수 있다.
위의 메뉴로 들어가면, 새 탭에 아래와 같은 코드가 나온다.

{% highlight xml %}
{% raw %}
<snippet>
  <content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
  <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
  <!-- <tabTrigger>hello</tabTrigger> -->
  <!-- Optional: Set a scope to limit where the snippet will trigger -->
  <!-- <scope>source.python</scope> -->
</snippet>
{% endraw %}
{% endhighlight %}

content 안에 자동 완성할 구문을 넣으면 되고,<br>
tabTrigger 안에 단축키로 활용할 구문을 넣으면 된다.<br>
예를 들어, hi + Tab 키를 통해 highlight를 완성하는 코드는 다음과 같다.

{% highlight xml %}
{% raw %}
<snippet>
  <content><![CDATA[
{% highlight $1 %}

{% endhighlight %}
]]></content>
  <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
  <!-- <tabTrigger>hello</tabTrigger> -->
  <tabTrigger>hi</tabTrigger>
  <!-- Optional: Set a scope to limit where the snippet will trigger -->
  <!-- <scope>source.python</scope> -->
</snippet>
{% endraw %}
{% endhighlight %}

$1 으로 되어있는 부분은 자동완성 후 커서의 위치이다.
자주 쓰는 문구가 있다면, 스니펫을 만들어 활용하면 편하다.<br>
주의할 점, 맥에서는 그냥 저장할 경우 스니펫이 동작하지 않는다.
확장자 명 .sublime-snippet을 넣어서 저장해줘야만 스니펫이 동작한다. 예를 들어, 파일명은 md-highlight.sublime-snippet과 같은 형식이어야 한다.