---
layout: post
title:  "heroku-custom-도메인-ACM으로-인증서-적용하기"
categories: [heroku, SSL, 인증서, TLS, rails]
---
heroku에서 돌아가고 있는 web application에 SSL을 적용하는 방법을 알아봤다.
그런데, heroku 메뉴얼을 뒤지다 보니 Automated Certificate Management라는 새로운 기능을 발견했다.
결론부터 이야기하면, heroku 유료 plan을 사용 중이라면, 추가 비용 없이 TLS 인증서를 적용할 수 있다.
TLS는 SSL과 같은 것이라고 보고 넘어가자.

#### ACM
[Automated Certificate Management](https://devcenter.heroku.com/articles/automated-certificate-management).<br>
Let's Encrypt 인증서를 자동으로 관리해준다.
custom domain이 추가될때마다 인증서도 등록되고, 마감 한 달 전에 자동 연장된다고 한다.<br>
너무나 편리하다.<br>
안 쓸 이유가 없으니 적용하도록 한다.
네임서버의 CNAME 세팅은 'your-domain.herokudns.com'으로 되어있어야 한다.<br>
~~~
$ heroku certs:auto:enable
~~~

![TLS적용완료]({{ site.url }}/assets/img/2017-11-06/01.jpg)<br>
적용 되었다.<br>
앞으로도 heroku를 이용하면 돈 주고 인증서를 구매하지 않아도 될 것 같다.

참고<br>
<https://devcenter.heroku.com/articles/automated-certificate-management><br>
<https://letsencrypt.org/>
