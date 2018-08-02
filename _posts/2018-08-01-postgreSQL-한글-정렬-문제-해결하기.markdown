---
layout: post
title:  "postgreSQL 한글 정렬 문제 해결하기"
categories: rails
---

### postgreSQL의 한글 정렬 문제
Ruby on Rails Application에 postgreSQL을 DB로 쓰고 있는 프로그램에서 이름순 정렬을 적용했다.

{% highlight ruby %}
@lists = List.order(:name)
{% endhighlight %}

그런데, 정렬이 일부만 된 것 같은 결과물이 출력되었다.
그 이유는, postgreSQL의 collation 때문이라고 한다.

참고: <https://stackoverflow.com/questions/14191848/postgresql-order-by-is-very-weird><br />
참고: <https://www.postgresql.org/docs/10/static/collation.html>

### collation 해결
문제를 해결하기 위해서는 query에 collate C를 지정해주면 된다.<br />
{% highlight ruby %}
@lists = List.order('name collate "C" asc')
{% endhighlight %}
참고: <http://tech.jinto.pe.kr/165><br />
참고: <http://susemi99.kr/2558><br />

더 근본적인 해결을 위해서는 처음 postgreSQL을 설치할 때, 환경변수 설정에서 collate C를 지정해주어야 한다.<br />
참고: <https://hashcode.co.kr/questions/2637/postgresql%EC%97%90%EC%84%9C-%ED%95%9C%EA%B8%80-%EC%88%9C%EC%84%9C%EB%8C%80%EB%A1%9C-%EC%A0%95%EB%A0%AC%EC%9D%B4-%EC%95%88%EB%90%A9%EB%8B%88%EB%8B%A4>

### 다른 해결 방법
여러가지 해결방법을 두고 고민하다가, ruby 자체의 sort_by 기능을 활용하기로 결정했다.

이미 live로 돌아가고 있는 app이기 때문에, DB를 다시 설치하는 위험을 감수하지 않기로 했다.
query에 collate을 지정하는 방법은 DB 의존성이 생기기 때문에 선택하지 않기로 했다.

불러오는 데이터 양이 많지 않기때문에, ruby의 sort_by 기능을 사용해도, 부하가 없을 것으로 판단했다.

{% highlight ruby %}
@lists = List.all.sort_by { |list| list.name }
{% endhighlight %}

### 결론
아직 postgreSQL을 설치하지 않았거나 사용자가 많지 않아서 DB를 재설치 하는데 부담이 없다면, 환경변수 설정을 통해서 해결하는 것이 가장 좋아보인다.
그렇지 않다면, 부하를 고려해보고 ruby method로 해결하는 것이 좋을 것 같다.