---
layout: post
title:  "jekyll blog 만들기"
date:   2017-09-12 17:51:30 +0900
categories: jekyll
---
heroku에 rails5로 만든 앱을 올리다 보니, rails4를 사용하던 때와는 다른 에러들이 나오기 시작했다. 홈페이지를 여러개 만들어야 하는 상황이라 문제와 해결방법을 기록할 블로그를 만들기로 했다. 기왕 블로그를 시작하는 김에 새로운 블로그 툴을 사용해보려고 jekyll로 만들었다. 기존에는 tistory, naver blog, blogger 등 기본 제공형 블로그와 wordpress를 사용해본 경험이 있다. 기존 블로그에서 느낀 가장 불편한 점은 editor였다. 종종 글을 작성할 때 editor와 구현된 글(html로 변환된 글) 사이의 괴리가 있었기때문에 html 편집기로 들어가 태그를 수정해줘야했다. jekyll은 마크다운 언어로 글을 작성하기때문에 해당 문제는 없을 것으로 기대했다.

#### 설치하기
설치 방법은 다음 링크들에 잘 정리가 되어있다. jekyll은 ruby로 만들어졌기때문에 mac과 linux를 쓴다면 편할 것 같다. git과 terminal을 기본적인것만 사용할 줄 안다면 쉽게 설치가 가능하다. 하지만, 잘 사용하지 못하더라도 아래 블로그에 정리된 것을 따라하면 설치할 수 있을 것 같다.<br>
<https://brunch.co.kr/@hee072794/39><br>
<https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/>

#### 마크다운
kekyll 블로그는 마크다운 언어로 작성을 하면 html로 변환해서 화면에 출력해준다. 마크다운 언어의 사용법에 대해서는 다음 링크를 참조<br>
<https://gist.github.com/ihoneymon/652be052a0727ad59601><br>

#### 실제 포스팅하기
github을 사용하듯이 하면 된다. 로컬에서 글을 쓰고 repository에 push 해주면 된다.

#### 포스팅 하기 전에 local에서 확인하기
`jekyll serve --watch`<br>
명령어로 local에서 미리 볼 수 있다.
