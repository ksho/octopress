---
layout: post
title: "Resist the future"
date: 2012-05-03 09:32
comments: true
categories: 
- dev
- octopress
- twitter
- mobile
- design
- yaml
---

On Tuesday, I spent a good bit of time tweaking the layout here.. I was looking for something a little different, but still minimal (I think I'll keep the gifs and flash on the shelf for now/ever). Anyway, once I was close to my vision for the design, which is just a modified version of the classic octopress theme, I fired it up on my iPhone's retina display and was reminded that octopress is built to render differently on mobile devices. Mostly, it makes the content of your site easier to read, which is a good thing. However, it also adheres to some other world of rules when it comes to rendering the layout. Debugging was difficult, since I'm not familiar with any tools to inspect css from inside mobile safari, so I became frustrated. At this point, I turned to firing off a tweet to the author of octopress, figuring I'd save myself some time poking around:

<blockquote class="twitter-tweet tw-align-center" data-in-reply-to="197378588385869824"><p>@<a href="https://twitter.com/kmano8">kmano8</a> Why would you do that?</p>&mdash; Octopress (@octopress) <a href="https://twitter.com/octopress/status/197379137546104832" data-datetime="2012-05-01T17:37:08+00:00">May 1, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

So that didn't go very well, and [the conversation continued for a short while](https://twitter.com/#!/kmano8/status/197378588385869824). My request was simple and absolutely legitimate. And later on, [Mr. Octopress](https://twitter.com/#!/imathis) used my question as inspiration for some fodder:

<blockquote class="twitter-tweet tw-align-center"><p>Someone just asked for a way to disable "mobile rendering" on @<a href="https://twitter.com/octopress">octopress</a>.in _config.yml set resist_the_future: true</p>&mdash; Brandon Mathis (@imathis) <a href="https://twitter.com/imathis/status/197413965343625216" data-datetime="2012-05-01T19:55:31+00:00">May 1, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

A desire to see my site render without mobile optimization doesn't necessarily mean I'm resistant to the future. The fact is, I have this [highly dense mobile display](http://www.apple.com/iphone/features/retina-display.html) that renders even smaller font sizes beautifully. Unfortunately, I'm not familiar with mobile design/layouts, so I was stuck in the mud for the time being.

Since I wasn't going to get any help from the author, I decided to find a way to unplug the mobile optimization myself. So I futzed around for about an hour, and it turns out, this is pretty simple. I found these three lines were being inserted in `<head>`:

{% codeblock lang:html %}
<meta name="HandheldFriendly" content="True">
<meta name="MobileOptimized" content="320">
<meta name="viewport" content="width=device-width, initial-scale=1">
{% endcodeblock %}

These three tags, the most important of which is viewport, are all a part of my site telling the browser it's optimized for mobile. There's a comprehensive description of what viewport does [over at the mozilla developer network](https://developer.mozilla.org/en/mobile/viewport_meta_tag), but in short, it's overriding control of things like screen width and zoom, resulting in smaller content appearing larger. Commenting out these lines in `<head>` resulted in my octopress site rendering as it would in any desktop browser. I added a yaml config item, `resist_the_future: true` to my _config.yml, and wrapped those three lines in a conditional.

{% gist 2587371 %}

Finally, this whole thing wouldn't be complete without submitting a pull request to the octopress repo and a follow-up response:

<blockquote class="twitter-tweet tw-align-center" data-in-reply-to="197739272504229888"><p>@<a href="https://twitter.com/kmano8">kmano8</a> touché</p>&mdash; Brandon Mathis (@imathis) <a href="https://twitter.com/imathis/status/197739852081545217" data-datetime="2012-05-02T17:30:29+00:00">May 2, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>