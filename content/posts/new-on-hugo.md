---
title: "New on Hugo\U0001F93A"
date: 2020-10-22T21:55:38+08:00
draft: false
tags:
  - hugo
---
> Starting from hexo, changing to jekyll, now i am on HUGO

# My Steps to HUGO
1. Follow the official website [basic installation](https://gohugo.io/getting-started/quick-start/);
2. Find a great (better stable) theme at [official theme library](https://themes.gohugo.io/)
3. Config the `config.yml` or `config.toml` by instruction from the theme producer.



## something you may want to pay attention to

### images

In hugos, the post use image from `static` folder, you can insert a image in a markdown method:

```markdown
![some caption](/static/image.jpg)
![some caption](/static/folder/image2.jpg)
```

In this condition the folder is like:

```markdown
contents
|  |
|  --- posts
|       |
|       ---- example.md
static
   |
   --- folder
   |     |
   |     ---- image2.jpg
   ---- image.jpg
```

### youtube

A embedded youtube video in post can be simple add as a [shortcode](https://gohugo.io/content-management/shortcodes/): 
```
  {{</* youtube w7Ft2ymGmfc */>}}
```

For a youtube video from link https://www.youtube.com/watch?v=w7Ft2ymGmfc

- if you also want to display shortcode in .md check [this website](https://liatas.com/posts/escaping-hugo-shortcodes/) from [Chris Liatas](https://liatas.com/).

# Theme Configuration - [hugo-PaperMod](https://adityatelange.github.io/hugo-PaperMod/)

Most of the parameter can be changed simply in `config.yml` or `config.toml`, like `title`, `author`. To use emoji in the `config.yml` go straight to the [emoji website](http://unicode.org/emoji/charts/full-emoji-list.html), find one :smile: with code `U+1F604` , replace the +1 with 000, namely insert `\U000F604`. 

PS: in the .md file, `:simle:` is a emoji, but the `\U000F604` is also d

## Archive / Tags

To tiggle the archive and tags do cost me some time. The answer is in the `config.yml` for the [theme temple website](https://github.com/adityatelange/hugo-PaperMod/blob/exampleSite/config.yml), where

```yaml
menu:
  main:
    - name: Archives
      url: /archives/
      weight: 5
    - name: Tags
      url: /tags/
      weight: 10

taxonomies:
  category: categories
  tag: tags
  series: series

...
```

is needed to add at the end of your `config.yml`.

## favicon.png

Chose the logo you want to use, go to [favicon.io](https://favicon.io/) to generate the icon, replace the ones in the `themes/hugo-PaperMod/static`.

In case you find no changes, may be the browser still has cache, clear it or switch another one will work.



# Adding more...

## Mathjax

Only simple 3 changing sperately in `css`, `layout/.html` and `head.html` or `header.html`. The tutorial you can find [here](https://bwaycer.github.io/hugo_tutorial.hugo/tutorials/mathjax/).

if you find multilines flattened into one line (check [this issue](https://bwaycer.github.io/hugo_tutorial.hugo/tutorials/mathjax/) ) change all `\\` at end to `\\\\\\`.

### Small problems fix:

- infinity symbol in MathJax $\infty$ code is `\infty` .

# now:

- [ ] add more blogs

- [x] fixed on the archive head...

- [x] image

- [x] file share

- [x] video insert
