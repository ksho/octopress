---
layout: post
title: "Movie fingerprints with pyffmpeg and PIL"
date: 2013-03-28 13:25
comments: true
categories:
- dev
- monetate
- python
published: true
---

This week Monetate had a round of Hack Days, and since I'm in Mexico I thought I'd write a short bit about something I worked on last year for the event.

A few times a year, Monetate sets a stretch of days aside for our engineering team to spend working on whatever we like to scratch a technical itch. It can be related to our product, or something completely unrelated. Famously, the only rule is that each person/team has only two minutes to present their hack. So for two days last June (and a bit more time since), I worked on a script that extracts every frame from a video file, compresses each frame to 1 pixel in width, and stitches them all together, side by side. This process creates an interesting landscape oriented image.. ideal for hanging in your home, maybe? To do this, I leveraged a poorly supported python library called [pyffmpeg](https://code.google.com/p/pyffmpeg/) to extract the video frames, and [PIL, the Python Imaging Library](http://www.pythonware.com/products/pil/), to manipulate the resulting frame images.

The pseudo-code goes something like this:
{% codeblock lang:python %}
# Loop through all frames
for frame in frames:
    # Resize frame to 1x720, for example (for a 720p video). Using an ANTIALIAS filter smooths the compressed frame nicely.
    compress_frame_to_slice(frame)
    # Append each 1 pixel-wide slice to the right side of a larger canvas
    composite_image.paste(frame)
composite_image.save('final_image.png')
{% endcodeblock %}

The following is Wall-E after processing. Performance is still a bit crumby -- this film took about 25 minutes utilizing two cores on a 2.4ghz core i5. Time to process completion seems to be constrained purely to the number of frames in the video file. This makes sense since navigation from one frame to the next and doing a resize operation on a frame is agnostic to the actual content of a frame. In other words, a detailed frame from, say, an action scene will resize in the same amount of time as a solid black frame. More examples can be seen below.

![Wall-E](http://farm9.staticflickr.com/8389/8599564758_3ff882c185_b.jpg)

It's a simple idea, and to be quite frank, most of my time was spent trying to get pyffmpeg built on various systems. I finally got it working on an install of Ubuntu 10.10.

You can checkout my github repo at [https://github.com/ksho/film-fingerprints](https://github.com/ksho/film-fingerprints)

_Top Gun_
![Top Gun](http://farm9.staticflickr.com/8092/8598480061_6489f8767a_b.jpg)

_Looper_
![Looper](http://farm9.staticflickr.com/8371/8598480415_3d0a0c32c6_b.jpg)

_Eternal Sunshine_
![Eternal Sunshine](http://farm9.staticflickr.com/8230/8599580048_ccc6bccea2_b.jpg)

_Walk the Line_
![Walk the Line](http://farm9.staticflickr.com/8249/8599579688_cde24ac9c1_b.jpg)


