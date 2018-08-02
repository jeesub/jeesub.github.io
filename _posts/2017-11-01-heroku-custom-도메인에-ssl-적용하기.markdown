---
layout: post
title:  "heroku custom 도메인에 SSL 적용하기"
categories: heroku
---
heroku에서 돌아가고 있는 web application에 SSL을 적용했다.
2월에 다른 web application에서 진행했었지만, 다시 하려니 잘 기억이 안나서 다시 기록한다.
실제 web application으로 사용하기 위해 hobby plan으로 변경을 했다.
예전에는 별도의 add-on을 사용해야 했으나, 이제는 인증서가 있고, 유료 plan을 사용 중이면 SSL 적용을 할 수 있다.

### SSL 인증서 구매하기
예전에 한 번 이용한 적 있는 <https://www.gogetssl.com>에서 인증서를 구매했다.
gogetssl에서 살 경우 인증서가 엄청나게 저렴하다.<br>

![저렴해]({{ site.url }}/assets/img/2017-11-01/01.jpg)<br>
도메인은 하나만 사용하기때문에 comodo positive SSL을 구매했다.
여러 도메인을 사용할 경우 다른 인증서를 구매해야 한다.
cf) www와 non-www의 경우 comodo positive SSL로도 가능하다.<br>

![CSR Configuration]({{ site.url }}/assets/img/2017-11-01/02.jpg)<br>
CSR Generator로 CSR을 만들어서 붙여넣어준다.
private key는 노출되면 안된다! 불안하다면, 직접 만들어서 사용한다.

![validation]({{ site.url }}/assets/img/2017-11-01/03.jpg)<br>
도메인에 대한 본인 확인을 해야 한다.
저번에는 도메인 메일을 사용하지 않아서 server에 파일을 올려 인증을 받았지만, 이번엔 메일 인증을 사용했다.<br>

메일로 crt file과 ca-bundle file이 올 것이다.
두 파일을 합하면, 최종적으로 사용 가능한 인증서가 만들어진다.<br>

{% highlight bash %}
$ cat yourdomain_com.crt yourdomain_com.ca-bundle > server.crt
{% endhighlight %}

### heroku에 인증서 등록하기
CLI 등록도 가능하고, 웹 등록도 가능하다.
이전엔 CLI 등록을 해봤으니 이번엔 웹으로 등록해봤다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01/05.jpg)<br>
Configure SSL을 누르면, 다음과 같이 나온다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01/06.jpg)<br>
우리는 구매한 인증서를 사용할 것이므로 Manually를 눌러준다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01/07.jpg)<br>
public crt와 private key에 아까 구매한 인증서의 정보들을 넣어준다. 파일로 넣어도 된다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01/08.jpg)<br>
DNS를 업데이트한다.<br>
CNAME 레코드에 @.yourdomain.com - yourdomain.com.herokudns.com를 추가해준다.

#### 참고
<https://www.gogetssl.com><br>
<https://devcenter.heroku.com/articles/ssl>
