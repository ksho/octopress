---
layout: post
title: "Using Icon Font for Social Links"
date: 2014-01-27 18:33:26 -0500
comments: true
published: true
categories: 
- dev
---

I've never liked the terrible `rss.png` I had right floated in the navigation. It wasn't cross-browser compatible with Firefox for some reason I didn't care to dig into, and it looked terrible on high resolution displays. So a few nights back, after [my snow photo adventure](http://karlshouler.com/blog/2014/01/22/late-night-snow/), I thought I'd look around for a nice icon font as a replacement.

Why use an icon font? Well, for me, the characters in an icon font can be transformed and styled (e.g. scale, color, shadow, opacity) all in CSS without having to open Photoshop. In addition, icon fonts are seriously lightweight and only require a single HTTP request for the whole set, rather than a GET for each image.

Not sure what my Google query was, but I ended up stumbling upon [Mono Social Icons Font](http://drinchev.github.io/monosocialiconsfont/) -- a really wide selection of simple social icons.

I had never installed an icon font before, but after pulling down the files, all that's required is a `@font-face` block to start using the icons, like so:
{% codeblock lang:css %}
@font-face {
    font-family: 'Mono Social Icons Font';
    src: url('monosocialicons/MonoSocialIconsFont-1.10.eot');
    src: url('monosocialicons/MonoSocialIconsFont-1.10.eot?#iefix') format('embedded-opentype'),
         url('monosocialicons/MonoSocialIconsFont-1.10.woff') format('woff'),
         url('monosocialicons/MonoSocialIconsFont-1.10.ttf') format('truetype'),
         url('monosocialicons/MonoSocialIconsFont-1.10.svg#MonoSocialIconsFont') format('svg');
    src: url('monosocialicons/MonoSocialIconsFont-1.10.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}
{% endcodeblock %}

Then you could do something like:
{% codeblock lang:css %}
.symbol, a.symbol:before {
    font-family: 'Mono Social Icons Font';
    font-size: 40px;
}
{% endcodeblock %}

Now, when you add the `.symbol` class to an element it will take a look at the text inside that element and instead of displaying it's inner-text, say 'twitterbird', it will render the corresponding icon character -- the twitter bird logo in this case. Inspect the HTML/CSS of the icons on the navigation to see what's going on.

One optimization I could make to improve load time is cut down the contents of the font files to only include icons I care about -- this would effectively make the request for them free.

Finally, though I did spend a bit of time tweaking their size and spacing, it took me only 15 minutes or so to get the icon font installed and working.
