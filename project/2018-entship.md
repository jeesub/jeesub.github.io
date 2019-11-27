---
layout: default
---

# entship.kr

## Overview

* Date: 2018
* Main Purpose: 앙트십 관련 새소식 전달 웹사이트 / 404 content redirection
* Project Size: 1 Web Developer, 6 weeks
* My Contribution: PM, planning, web design, web development
* Stacks: HTML, SCSS, Bulma, JavaScript, Ruby on Rails, PostgreSQL, heroku, AWS S3

![entship.kr]({{"/assets/img/project/2018_entship_kr.jpg"}})
(홈페이지 중 일부)

## Description

리브랜딩 이후 앙트십 대표 사이트로 entship.kr 대신 entshipschool.com을 도메인으로 사용하였다. 
초반에는 entship.kr 접속자들을 entshipschool.com으로 리디렉션 해주었고, entship.kr의 리디렉션이 필요없게 되었다. 

새로 만드는 entship.kr은 앙트십 관련 소식을 전달하는 플랫폼으로 기획했다. 
사용자에게 앙트십 관련 뉴스, 칼럼, 블로그, 영상, 행사 관련 새 소식을 소개한다. 

또한 새로운 entship.kr은 문제점 한 가지를 해결하려 했다. 
문제는 wordpress로 만든 기존의 entship.kr은 5년 가까이 운영이 되었다는 점이었다. 
그동안 콘텐츠를 착실히 쌓아온 덕분에 사용자가 기업가정신 관련 검색을 할때마다 entship.kr의 콘텐츠가 상단에 노출되었고 404 Error가 노출되었다. 
이를 해결하기위해 새로운 entship.kr 웹사이트에는 기존 콘텐츠와 새로운 콘텐츠의 맵핑 리디렉션 기능을 만들어 넣었다. 
검색봇에는 새로운 URL로 이전되었음을 전달했고, 사용자는 이전된 홈페이지로 리디렉션 되었다. 
그리고 7,000회가 넘는 리디렉션이 이루어졌다. 

## Takeaway

* 검색결과에 상위권으로 노출된 페이지들을 redirection함으로써 웹사이트 개편에 따르는 정보유실을 최소화 했다. 
이 과정을 통해 검색로봇과 HTTP 상태 코드에 대해 자세히 알게 되었다. 
* 업무에는 처음으로 Bulma를 사용했다. 
Bulma는 JavaScript 없이 CSS3를 사용하기 때문에 더 가볍게 사용할 수 있었다. 
그리고 사람들이 Bootstrap의 기본 디자인에는 익숙한 반면 Bulma의 디자인은 잘 모르기 때문에 별도의 customizing 없이도 새로운 느낌을 줄 수 있었다. 