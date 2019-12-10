---
layout: post
title: "CSS-framework-Bulma-소개"
categories: [web-development, ruby-on-rails, css]
---

# Bulma

Flexbox 기반의 무료, 오픈소스 CSS framework. 
2019년 12월 9일 현재, github에서 37.7k의 Star를 받은 나름 유명한 framework이다. 

<https://bulma.io/>

# 장단점

가장 유명한 CSS framework인 Bootstrap과 비교를 해보았다. 
Bootstrap에 비해 Bulma가 가지는 장단점은 다음과 같다. 

## 장점

1. 가볍다. JavaScript 없이 CSS만을 사용하기 때문에 엄청 가볍다. 
2. CSS3의 최신 기술들을 활용하기 때문에 상황에 따라 굉장히 편리하다. 
3. Learning curve가 낮은 편이다. Element에 class를 추가하는 형태로 동작하기 때문에 익히고 적용하기가 쉽다. 
4. Customize가 쉽다. 애초에 customize를 많이 염두에 둔 듯 하다. 변수 선언을 통해 customize할 수 있다. 
5. Bulma가 정해놓은 class를 지정해야지만 style이 적용되기 때문에 내가 적용한 다른 CSS를 오염시키지 않는다. 가장 마음에 들었던 장점이다. Bulma에서 제공하는 class를 적용시키지 않으면, 내 HTML 문서는 전혀 변하지 않는다. 이 덕분에 custom은 더 쉬워지고, CSS error를 발견하기 쉬워진다. 
6. Bootstrap보다 사용자가 적기 때문에, 참신한 느낌을 준다. 이미 사용자들은 Bootstrap으로 만든 웹사이트에 익숙해졌고, 개발자들은 참신함을 주기 위해 Bootstrap의 느낌을 빼는데 시간을 들인다. Bulma로 만든 웹사이트는 아직까지는 기시감을 주지 않는다. 

## 단점

1. JavaScript 없이 동작하기때문에 한계가 있다. 아직까지는 CSS만으로 역동적인 frontend를 만드는데 제약이 존재한다. 
2. 브라우저 호환성이 낮다. JavaScript를 사용하지 않았고 CSS3의 최신 기술들을 활용하기 때문에 100% 호환되지 않는 브라우저들이 존재한다. 이는 구형 브라우저 사용이 많은 한국에서는 특히 심각한 단점이다. 
3. 한국어 가이드 문서를 구하기 어렵다. 

몇 가지의 단점이 있지만, 명확한 장점이 있기 때문에 프로젝트에 따라 Bulma의 장점이 빛을 발할 수 있다. 
디자이너 없이 혼자 웹사이트를 만들어야 할 경우 Bulma를 사용하면 빠른 작업이 가능하다. 
그리고 방문자들이 mobile 비중이 높고, 최신 브라우저를 사용할 경우 Bulma를 사용할 수 있다. 

# Ruby on Rails에서 활용하기

Bulma 홈페이지에 가면 여러 환경에서 활용하는 방법이 나와있다. 
다운로드 가능한 파일로도 제공이 되고, CDN도 있고, npm으로 설치하는 방법도 잘 설명되어 있다. 

Ruby on Rails로 프로젝트를 진행했기 때문에 gem을 활용했다. 
21만 다운로드를 기록한 bulma-rails gem을 사용했다. 

<https://rubygems.org/gems/bulma-rails>

gem을 사용하기 위해 Gemfile에 bulma-rails gem을 추가해준다. 

{% highlight ruby %}
# Gemfile
gem 'bulma-rails'
{% endhighlight %}

gem을 설치한다. 

{% highlight bash %}
$ bundle
{% endhighlight %}

CSS에 import 해준다. 

{% highlight css %}
# app/assets/stylesheets/application.scss
@import 'bulma';
{% endhighlight %}

viewport 메타 태그를 추가해준다. 

{% highlight html %}
# app/views/layouts/application.html.erb
<meta name="viewport" content="width=device-width, initial-scale=1">
{% endhighlight %}

CSS 적용이 끝났다. 
이제는 미리 지정된 class를 적용하는 방식으로 활용하기만 하면 된다. 
공식 문서를 참고하면 쉽게 활용할 수 있을 것이다. 

{% highlight html %}
<div class="container">
  <section class="section">
    <h1 class="title">
      Hello, World!
    </h1>
    <h2 class="subtitle">
      Thanks, Bulma.
    </h2>
    <div class="columns">
	  <div class="column">column 1</div>
	  <div class="column">column 2</div>
	  <div class="column">column 3</div>
	</div>
  </section>
</div>
{% endhighlight %}