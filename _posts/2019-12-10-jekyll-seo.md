---
layout: post
title: "Jekyll SEO"
categories: jekyll
---

# SEO

Search Engine Optimization. 
자세한 내용은 [이전 포스트]({% post_url 2018-11-20-SEO %}) 참고. 

# Jekyll SEO

Jekyll의 기능을 활용해 다음과 같은 SEO를 진행할 수 있다. 

## permalink

URL에 해당 포스트의 제목이 들어갈 경우, SEO에 더욱 유리하다. 
이를 위해 Jekyll blog의 URL이 제목을 활용하도록 바꿔줄 필요가 있다. 
아래의 코드를 _config.yml 파일에 넣어준다. 

{% highlight md %}
permalink: blog/:title/
{% endhighlight %}

## sitemap

root 폴더에 sitemap.xml 파일을 만든다. 
post가 새로 작성되면 sitemap이 갱신되도록 하려면 아래와 같이 작성하면 된다. 

{% highlight md %}
{% raw %}
---
layout: null
---
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
  <url>
    <loc>{{ site.url }}/</loc>
    <priority>1.00</priority>
  </url>
  {% for post in site.posts %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      <priority>0.5</priority>
    </url>
  {% endfor %}
</urlset>
{% endraw %}
{% endhighlight %}

## robots.txt

root 폴더에 robots.txt 파일을 만든다. 
모든 검색엔진에게 열어줄 경우 아래와 같이 작성한다. 

{% highlight text %}
User-agent: *
Allow: /
{% endhighlight %}