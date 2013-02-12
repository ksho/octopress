---
layout: post
title: "Retina display support for images"
date: 2012-10-02 15:14
comments: true
categories: 
- dev
---

The header image of karlshouler.com is _finally_ compatible with retina displays. I'm leveraging the popular [retina.js](http://retinajs.com/), which, when placing a high-resolution version of an image (with a '@2x' specifier at the end of the filename) alongside the standard-res version, will swap in the high-res image when viewed on a retina display.

As the developer's site describes, it's as simple as placing retina.js on your server and including the following line in `<head>`:
{% codeblock lang:html %}
<script type="text/javascript" src="/scripts/retina.js"></script>
{% endcodeblock %}

Finally, say you have an image file `image.png` on your site. Place a version of that image alongside it called `image@2x.png` that is doubled in width and height. Now go enjoy all those pixels.

NB: It's necessarily a concern that these `*@2x*` images will take longer to load on a user's first visit, so keep this in mind when optimizing for load time.
