---
layout: default
---

# find your doggie

## description

2018년 피츠버그에 갔을 때 선우와 진행한 side project. 
질문에 대한 답변을 통해 나와 성격이 가장 유사한 강아지 종을 찾아준다. 

![binoo]({{"/assets/img/project/binoo.jpg"}})

## Process

'Brainstorming - Planning - Design - Coding - QA'의 순서로 진행을 했다. 

평소에 둘 다 강아지를 좋아했기 때문에 강아지에 대한 아이디어가 많이 나왔고, 그 중 짧은 시간 내에 구현 가능한 프로젝트를 선정했다. 
MBTI, 에니어그램 등의 성격 검사와 유사한 방식으로 질문과 그에 대한 답변을 통해 성격을 분류하는 방식을 사용했다. 
강아지의 종에 따른 성격은 Google 검색 결과값으로 보여주는 태그들을 활용했다. 
성향의 카테고리 별로 점수를 매겨두고 질문자의 답변과 유사도를 계산해서 가장 유사한 강아지를 결과값으로 보여주도록 했다. 
선우는 front-end를, 나는 back-end를 맡아 진행했다. 
개발은 자주 사용해본 Ruby on Rails로 진행했다. 

* source code: <https://github.com/jeesub/project-binoo>
* URL: <http://binoo.herokuapp.com/>