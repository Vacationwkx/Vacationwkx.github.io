---
title: Note Learn Jekyll
date: 2020-04-01T21:55:38+08:00
tags:
  - jekyll
---
Note of learning creating Blog in Jekyll

# Guide / Tutorial
## For Jekyll
- [Quick Start - Official Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
  Official one is the most basis and reliabel.
- [What is Jekyll? and How it works? - Jekyll Bootstrap](http://jekyllbootstrap.com/lessons/jekyll-introduction.html) 
  Better first go though the official one to understand what is **Variables** **Front Matter** ..
- Sinple guides of jekyll from [CarlBoettiger](https://www.carlboettiger.info/2012/12/30/learning-jekyll.html) 
  Pure Guide, what do first, what next.
- Fast guide for those, who know html[CloudCannon](https://learn.cloudcannon.com/jekyll-blogging/#list)
## For HTML
- No Base No Building: What is HTML / HTML5 und CSS [Basic Knowledge in Mozilla](https://developer.mozilla.org/en-US/docs/Web)
- Basic Example & Code Training [HTML - W3School](https://www.w3school.com.cn/html/html_attributes.asp) and [JS -W3School](https://www.w3school.com.cn/js/index.asp)

# Front Matter
```
---
title: Antigragile - Book Review
layout: post
author: Vac
categories: [Book]
tags: [Probability]
---
```
## Front Matter default

default your font matters in _config.yml. for all the file(`path: ""`) in _posts(`type: "posts"`), set front matter values: layout to post, author to Vac, excerpt_separator to <!-- more -->(normally the first paragraph).
```
defaults:
  - 
    scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
      author: "Vac"
      excerpt_separator: <!-- more -->
```
## Tags
more tags can be listed like:
```
tags:
  - tag1 
  - tag2
```
to make sure it works, use 2 spaces before the subtags
Also, you can add properties to the subtags:
```
tags:
  - name: tag1
    type: math
  - name: tag2
    type: art
```
and cite it in liquid with:
```
 {% raw %}
 {% for tag in page.tags %}
    {{ tag.name }}, {{ tag.type }}
 {% endfor %}
 {% endraw %}
```
# Markdown
## Index
The homepage of the site, accepting front matter

## Image
```
{% highlight markdown %}
![caption of image](/assest/path/to/image.jpg){: width="50%"}
{% endhighlight %}
```
- {: class=} can add any css to the image part
- no need for plug-in

## Code
- Way 1
  ``` 
  {% raw %}
  {% hightlight [code type]%}
  some code here.
  {% endhighlight %}
  {% endraw %}
  ```
- Way 2 - markdown type
  ```
  {% highlight markdown %}
  ` ` `[code type]
  
  ` ` `
  {% endhighlight %}
  ```
- when liquid wrongly translate your code to error

  `{&#37; raw &#37;} your code is safe now.{&#37; endraw &#37;}`
  
## Link to Post
```liquid
{% raw %}
[say something]({% post_url 2019-11-2-name-of-it %})
{% endraw %}
```
- no type at end

## Emoji
recommend website [Full Emoji List](https://unicode.org/emoji/charts/full-emoji-list.html#1f602), or you can just google one
1. find your one in the list;
2. get the UTF-8 code like `U+1F642`;
3. wirte direct in format `&#x1F642;`;
4. and it will be like &#x1F642;.

# Liquid
2 types
1. ```liquid
   {% raw %}
   {{ page.title | upcase }}
   {% endraw %}
   ```
2. ```liquid
   {% raw %}
   {% if ... %} {% %}
   {% endraw %}
   ```
## Include + Parameters
you can add a new layout as a common used piece in the blog
for example, insite a youtube video:
- in the layout file `youtube.html` use `include.parameter`:
  ```
  {% highlight markdown %}
  <div class="spacing youtube">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/{{ include.youtube_id }}" frameborder="0" allowfullscreen></iframe>
  </div>
  {% endhighlight %}
  ```
  
- in the blog add the parameter after the include:
  ```
  {% raw %}
  {% include youtube.html youtube_id="YIiHiMXOeYU" %}
  {% endraw %}
  ```
