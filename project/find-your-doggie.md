---
layout: default
---

# find your doggie

## Overview

* Date: 2018
* Category: [#web_application](https://www.google.com/search?q=web+application)
* Project Size: 2 Web Developers, 1 week
* My Contribution: Web Development(Ruby on Rails)
* Tools: Ruby on Rails, Heroku, Github

## Description

2018년 피츠버그에 갔을 때 선우와 진행한 side project. 
질문에 대한 답변을 통해 나와 성격이 가장 유사한 강아지 종을 찾아준다. 

![binoo]({{"/assets/img/project/binoo_1.png"}})

## Problem

해마다 많은 수의 반려견이 버려지거나 길을 잃어 보호소에 가고 있다. 
대한민국에서는 2017년 기준 10만 마리 이상의 동물이 유기, 유실 되었다. 
보호소에서 구조된 동물들 가운데 27%는 자연사, 20%는 안락사 되고 있다. (출처: [2017 동물 보호센터 현황 - 농림축산검역본부](http://www.qia.go.kr/getZipwebQiaCom.do?id=44931&type=6_18_1bdsm))

## Solution

새로운 반려견을 맞이하려는 사람들이 펫샵에서 강아지를 사지 않고 보호소의 강아지를 입양할 경우 이러한 문제를 조금이나마 해결할 수 있을 것이다. 
이를 위해서 사람들에게 강아지를 입양할 수 있도록 넛지 하기로 했다. 
간단한 질의응답 게임을 통해 강아지와의 유대감이 생성되도록 한다. 
게임 결과로 본인과 유사한 성격의 강아지를 추천하고, 주변의 강아지 보호소 지도를 보여준다. 

![binoo]({{"/assets/img/project/binoo_2.jpg"}})

## Process

Hackerthon처럼 짧은 시간에 완성하기로 했다. 
아이데이션부터 퍼블리싱까지 이틀동안 진행했다. 
'Brainstorming - Design - Coding'의 순서로 진행을 했다. 

### Brainstorming

여러가지 아이디어 중 짧은 시간 내에 구현 가능한 프로젝트를 선정하기로 했다. 
둘 다 웹을 공부하고 있었기 때문에 웹과 관련된 프로젝트를 해보기로 했다. 
둘 다 강아지를 좋아했기 때문에 반려견과 관련된 아이디어가 많이 나왔다. 

### Design

MBTI, 에니어그램 등의 성격 검사와 유사한 방식으로 질문과 그에 대한 답변을 통해 성격을 분류하는 방식을 사용했다. 
강아지의 종에 따른 성격은 Google 검색 결과값으로 보여주는 태그들을 활용했다. 
성향의 카테고리 별로 점수를 매겨두고 질문자의 답변과 유사도를 계산해서 가장 유사한 강아지를 결과값으로 보여주도록 했다. 

![binoo]({{"/assets/img/project/binoo_3.jpg"}})

### Coding

선우는 front-end를, 나는 back-end를 맡아 진행했다. 
개발은 자주 사용해본 Ruby on Rails로 진행했다. 

![binoo]({{"/assets/img/project/binoo_4.jpg"}})

DB에는 성격을 6가지로 카테고리화 하여 강아지의 종 별로 점수를 입력해놓았다. 
질문자가 12개의 질문에 답변을 하면, 6개의 카테고리 점수가 계산이 된다. 
이 점수를 DB의 강아지 별 점수와 비교하여 가장 차이가 적은 강아지를 결과값으로 돌려준다. 

![binoo google analytics]({{"/assets/img/project/binoo_5.png"}})

* source code: <https://github.com/jeesub/project-binoo>
* URL: <http://binoo.herokuapp.com/>