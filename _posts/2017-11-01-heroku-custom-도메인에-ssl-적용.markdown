---
layout: post
title:  "heroku-custom-도메인에-ssl-적용"
categories: heroku, SSL
---
heroku에서 돌아가고 있는 web application에 SSL을 적용했다.<br>
2월에 다른 web application에서 진행했었지만, 다시 하려니 잘 기억이 안나서 다시 기록한다.<br>
실제 web application으로 사용하기 위해 hobby plan으로 변경을 했다.<br>
예전에는 별도의 add-on을 사용해야 했으나, 이제는 인증서가 있고, 유료 plan을 사용 중이면 SSL 적용을 할 수 있다.

#### SSL 인증서 구매하기
예전에 한 번 이용한 적 있는 <https://www.gogetssl.com>에서 인증서를 구매했다.<br>
gogetssl에서 살 경우 인증서가 엄청나게 저렴하다.<br>

![저렴해]({{ site.url }}/assets/img/2017-11-01-01.jpg)
도메인은 하나만 사용하기때문에 comodo positive SSL을 구매했다.<br>
여러 도메인을 사용할 경우 다른 인증서를 구매해야 한다.<br>
cf) www와 non-www의 경우 comodo positive SSL로도 가능하다.<br>

![CSR Configuration]({{ site.url }}/assets/img/2017-11-01-02.jpg)
CSR Generator로 CSR을 만들어서 붙여넣어준다.<br>

![validation]({{ site.url }}/assets/img/2017-11-01-03.jpg)
도메인에 대한 본인 확인을 해야 한다.<br>
저번에는 도메인 메일을 사용하지 않아서 server에 파일을 올려 인증을 받았지만, 이번엔 메일 인증을 사용했다.<br>

모든 과정이 완료 되면 인증서와 private key가 메일로 와 있을 것이다. (다운로드도 가능하다.) 나중을 위해 잘 보관해 놓는다.<br>
private key 정보는 유출되지 않도록 유의한다.

#### heroku에 인증서 등록하기
CLI 등록도 가능하고, 웹 등록도 가능하다.<br>
이전엔 CLI 등록을 해봤으니 이번엔 웹으로 등록해봤다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01-05.jpg)
Configure SSL을 누르면, 다음과 같이 나온다.
![heroku setting]({{ site.url }}/assets/img/2017-11-01-06.jpg)
우리는 구매한 인증서를 사용할 것이므로 Manually를 눌러준다.
![heroku setting]({{ site.url }}/assets/img/2017-11-01-07.jpg)
public crt와 private key에 아까 구매한 인증서의 정보들을 넣어준다. 파일로 넣어도 된다.<br>
![heroku setting]({{ site.url }}/assets/img/2017-11-01-08.jpg)
DNS를 업데이트한다.<br>
CNAME 레코드에 @.yourdomain.com - yourdomain.com.herokudns.com를 추가해준다.

참고<br>
<https://www.gogetssl.com><br>
<https://devcenter.heroku.com/articles/ssl>
