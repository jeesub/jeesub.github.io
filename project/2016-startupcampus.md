---
layout: default
---

# startupcampus.com

## Overview

* Date: 2016
* Main Purpose: program web brochure
* Project Size: 1 Web Developer and 1 Web Designer, 4 weeks
* My Contribution: PM, planning, web development
* Stacks: HTML, SCSS, bootstrap, JavaScript, Ruby on Rails, heroku

![startupcampus.com]({{"/assets/img/project/2016_startupcampus_com.jpg"}})
(홈페이지 중 일부)

## Description

신규 사업인 스타트업캠퍼스 프로그램의 참가자 모집을 위한 웹사이트. 
기존의 LAMP(Linux, Apache, MySQL, PHP)에서 벗어나 Ruby on Rails로 작업했다. 
Lean Startup 이론대로 간단한 one-page 웹사이트로 시작했다. 
지원서 제출받기는 Dropbox의 파일요청 기능을 활용하여 개발 리소스를 최소화했다. 

## Takeaway

* 실제 업무에는 처음으로 Ruby on Rails를 사용했다. 
LAMP(Linux, Apache, MySQL, PHP)보다 빠른 속도로 개발이 가능했다. 
* 적절한 대안을 활용했을 때의 이점을 알게 되었다. 
사용자로부터 파일을 받는 기능을 만들기 위해서는 많은 부분을 고려해야 한다. 
해킹을 방지하기 위해 업로드 되는 파일의 형식을 제한해야 하고, 파일 크기를 제한해야 하고, 업로드 되는 폴더의 권한을 잘 관리해야 한다. 
사용자로부터 받은 파일을 관리자가 확인할 수 있도록 만들어줘야 하고, 다운로드 받아 사용할 수 있는 기능을 만들어야 한다. 
이 많은 부분을 Dropbox의 파일요청 기능을 통해 손쉽게 해결했다. 
* 대안 기능의 한계를 알게 되었다. 
지원서 파일을 Dropbox와 Google Drive를 이용해 제공해보았지만, UX가 만족스럽지 못했다. 
결국 지원서 파일은 서버에서 직접 제공하는 방식으로 바꾸었다. 