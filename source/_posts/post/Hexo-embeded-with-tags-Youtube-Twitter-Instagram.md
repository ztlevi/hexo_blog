---
title: 'Hexo embeded with tags (Youtube, Twitter, Instagram)'
date: 2018-01-27 17:14:52
categories: hexo
tags: hexo
---

# Embed web pages in your post

Recently, I found Hugo, which is another static site generator, comes with some useful [shortcodes](https://gohugo.io/content-management/shortcodes/) that allows you embed html figure, instagram, speakerdeck, youtube, twitter and so on in your post. That's a great feature for some social guys.

And of course, we can do this in hexo with some plugins.

Thanks god. I don't even play Instagram, twitter. And my youtube channel is just full with school stuff. What a boring man am I.😂😂😂 So I just put other people's nice one here as examples.

<!--more-->

## Youtube

For youtube or other video resources, you can embed videos with [hexo-tag-video](https://github.com/geekplux/hexo-tag-video). Thanks geekplux for this interesting plugin.

Very easy to install. Here is an example.

* embed code for youtube

```
{% video <iframe width="560" height="315" src="https://www.youtube.com/embed/k5X2Hb3tc2s" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe> %}
```

{% video <iframe width="560" height="315" src="https://www.youtube.com/embed/k5X2Hb3tc2s" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe> %}

## Instagram & Twitter

For Instagram, [hexo-tag-instagram](https://github.com/tea3/hexo-tag-instagram) is built by [tea3](https://github.com/tea3). He built [hexo-tag-twitter](https://github.com/tea3/hexo-tag-twitter) as well. Great job done, tea3!

* embed code for instgram

```
{% instagram instgram-url %}
```

{% instagram https://www.instagram.com/p/BeduoAYHKFY/?tagged=cat %}

* embed code for twitter

```
{% twitter tweet-url %}
```

{% twitter https://twitter.com/spacemacs/status/956407087868862464 %}
