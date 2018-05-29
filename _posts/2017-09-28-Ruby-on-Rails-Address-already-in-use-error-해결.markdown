---
layout: post
title:  "Ruby on Rails Address already in use error 해결"
categories: [rails]
---
{% highlight bash %}
$ rails server
{% endhighlight %}

명령어를 실행했지만 error가 났다. Error 메시지를 보니 이전 puma가 제대로 꺼지지 않은 것 같다.<br>

{% highlight bash %}
Address already in use - bind(2) for "0.0.0.0" port 8080 (Errno::EADDRINUSE)
{% endhighlight %}

port8080이 이미 선점되어있기 때문으로 보인다.<br>

### port8080에서 돌아가는 프로세스 확인하기

{% highlight bash %}
$ lsof -wni tcp:8080

COMMAND   PID   USER   FD   TYPE     DEVICE SIZE/OFF NODE NAME
ruby    17816 ubuntu   11u  IPv4 2009126466      0t0  TCP *:http-alt (LISTEN)
ruby    17873 ubuntu   11u  IPv4 2009126466      0t0  TCP *:http-alt (LISTEN)
{% endhighlight %}

실행 결과 2개의 ruby 프로세스가 돌아가고 있다.<br>
모두 종료해준다.<br>

{% highlight bash %}
$ kill -9 17816
$ kill -9 17873
{% endhighlight %}

해결 완료
<br><br>
참고<br>
<https://stackoverflow.com/questions/31039998/address-already-in-use-bind2-errnoeaddrinuse><br>
<https://www.lesstif.com/pages/viewpage.action?pageId=20776078>
