---
layout: post
title:  "jekyll blog title 바꾸기"
categories: jekyll
---
jekyll 블로그를 만드니 header의 site의 이름 부분에 'Your awesome tilte'이라고 되어있다. footer 부분에도 기본적으로 적용되어 있는 문구들이 나타난다. 해당 부분은 간단하게 바꿀 수 있다.

#### title, description, github 등을 내 것으로 바꾸기
기본 directory에 _config.yml이라는 파일이 있다. 해당 파일을 열어 내용부분을 고쳐주면 된다.
~~~
title: 블로그 이름
email: 이메일
description: > # this means to ignore newlines until "baseurl:"
	블로그의 description
	여러가지 설정을 추가, 수정, 변경할 수 있다.
~~~
위의 예시처럼 수정해주고 push해주면 새 title, email, description이 적용된 것을 볼 수 있다.
