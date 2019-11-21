---
layout: default
---

# Arduino Theremin

## Overview

* Date: 2015
* Category: [#arduino](https://www.google.com/search?q=arduino)
* Project Size: 1 week
* Tools: Arduino

## Description

Arduino와 초음파 센서를 이용해 Arduino Theremin을 만들었다. 
Arduino의 다양한 사용 방법을 테스트해보기 위해 토이 프로젝트로 진행했다. 
실제 Theremin과는 달리 1차원 거리를 측정해 상응하는 주파수의 음을 내도록 설계했다. 

## Problem

앙트러프러너십 교육 콘텐츠는 학생들이 직접 해보면서 배우도록 설계했다. 
학생들이 프로젝트를 진행할 때 낮은 난이도로 높은 효과를 낼 수 있는 방법이 필요했다. 

## Solution

Arduino를 앙트러프러너십 교육에 활용할 수 있는지를 알아보았다. 
몇 가지 작은 프로젝트들을 진행해보며, 일반 중고등학생 수준에서 습득이 가능한 기술인지 파악해보았다. 
센서 없이 가능한 것들부터 만들어보기 시작해서 센서를 늘려가며 다양한 프로젝트를 진행했다. 
그 중 가장 난이도가 높은 것이 Theremin이었다. 

## Process

전자공학과 학부생 때 전자피아노를 설계해본 경험이 있었다. 
우리가 듣고 있는 음계는 특정 주파수를 가진 음파이다. 
즉, 특정 주파수를 만들어서 스피커를 통해 출력하면, 우리는 익숙한 음계를 듣게 되는 것이다. 
이 경험을 활용해 간단한 Theremin을 만들어보고자 했다. 
Theremin은 두 개의 안테나에서 발생되는 전자기장에 간섭현상을 일으켜 특정 소리를 내는 악기이다. 
하나의 안테나는 음의 높낮이를 담당하고, 다른 하나는 음의 크기를 담당한다. 
구현할 때는 안테나 대신 초음파 센서를 하나만 사용했다. 
초음파를 보낸 뒤 돌아오는 시간을 계산했고, 해당 왕복 시간에 따라 다른 음의 주파수가 출력되도록 프로그래밍 했다. 

## Conclusion

<iframe width="560" height="315" src="https://www.youtube.com/embed/cbRFlvc7tzE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

거리에 따라 다른 주파수를 발생시키는 간이 Theremin이 완성되었다. 
실제 Arduino Project를 진행해보니, 기반지식이 없는 중고등학생들이 짧은 시간에 배워서 활용하기는 어려울 것으로 생각되었다. 
그래서 Arduino 교육은 이미 교육을 잘 하고있는 분들에게 맡기기로 했다. 
그 대신 Arduino를 활용하는 방법에 대해서 고민해보는 ideation 교육 프로그램의 prototype을 만들었다. 
하지만 교육을 전달하는 강사들이 Arduino를 배우고 익혀야하는 문제가 있었기 때문에 실제 상품화되지는 못했다. 