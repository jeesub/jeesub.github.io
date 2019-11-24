---
layout: default
---

# entshipschool.com

## Overview

* Date: 2018
* Main Purpose: program web brochure
* Project Size: 2 Web Developers and 1 Web Designer, 8 weeks
* My Contribution: PM, planning, web development (HTML, CSS 제외)
* Stacks: HTML, SCSS, JavaScript, jQuery, Ruby on Rails, PostgreSQL, heroku, AWS S3

![entshipschool.com]({{"/assets/img/project/2018_entshipschool_com_1.jpg"}})

![entshipschool.com]({{"/assets/img/project/2018_entshipschool_com_2.jpg"}})

(홈페이지 중 일부)

## Description

앙트십 프로그램을 리브랜딩하면서 홈페이지 개편의 필요성이 있었다. 
일단 기존 entship.kr 웹사이트에 혼재되어있던 블로그성 글과 프로그램 브로셔를 분리해냈다. 
블로그성 포스트들은 앙트십 네이버 블로그로 이전했고, 프로그램 브로셔들만 entshipschool.com으로 옮기기로 했다. 
비즈니스 측에서는 확장성을 고려한 대학생, 일반인 대상 프로그램이 함께 홈페이지에 노출되기를 요청했다. 
다양한 프로그램을 고객 대상으로 카테고리화 하여 청소년, 청년, 기업 프로그램으로 나누었고, 각각의 페이지에서 세부 정보와 프로그램을 소개했다. 
각 프로그램의 필요 정보들은 세부 페이지에서 보여주었으며, 관리자가 손쉽게 프로그램을 관리할 수 있도록 하였다. 
프로그램 문의 및 교육 신청은 Slack의 webhook 기능과 연동해놓아서 등록되면 Slack 알림을 받도록 했다. 

## Takeaway

* 여러 이해관계자의 의견을 모아 하나로 만들어가는 과정을 거쳤다. 
홈페이지에 청소년, 청년, 일반을 대상으로하는 교육프로그램이 모두 노출되기 위해서 회사의 모든 구성원이 이해관계자가 되었다. 
커뮤니케이션으로 모두의 다른 목적을 한데 모아 하나의 홈페이지 기획안을 만들어냈다. 
* 이번 회사에서는 처음으로 다른 개발자와 협업을 진행했다. 
HTML, CSS만 전담으로 하는 외부 개발자와 협업을 진행했다. 
덕분에 빠른 시간 안에 개발이 가능했다. 
* 리모트 협업을 진행했다. 
본인을 제외한 개발자, 디자이너는 모두 회사 외부 사람이었다. 
이들과 온라인 커뮤니케이션으로 웹사이트를 만드는 경험을 했다. 
* 향상된 admin 기능을 제공했다. 
admin 기능만으로도 상품 생성, 수정, 삭제가 가능하도록 했다. 
폭 넓은 교육 상품군을 다뤄야하기 때문에 DB와 admin page를 설계할 때 많이 고민해야 했다. 
* 처음으로 AWS S3에 직접 웹폰트를 업로드해 사용했다. 
이를 통해 웹폰트와 CORS policy에 대해 자세히 알게 되었다. 