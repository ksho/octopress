---
layout: post
title: "Movie fingerprints with pyffmpeg and PIL"
date: 2012-07-03 13:25
comments: true
categories: 
- dev
- monetate
- python
published: false
---

It's been over a month since Monetate's second round of hack days, time engineers get to spend working on whatever we like to scratch a techincal itch, and I'm just finally getting around to writing a bit about it.

For those two days (and more time since), I worked on a script that extracts every frame from a video file, compresses each frame to 1 pixel by [pixel height of the video] and stitches them all together, side by side. This process creates an interesting landscape oriented piece of art.. ideal for hanging in your home, maybe? To do this, I leveraged a poorly supported python library called pyffmpeg to extract the video frames, and PIL, the Python Imaging Library, to manipulate the resulting frame images.

the pseudo-code goes something like this:
{% codeblock lang:python %}
# Loop through all frames
for frame in frames:
    # Resize frame to 1x720, for example (for a 720p video). Using and ANTIALIAS filter smooths the compressed frame nicely.
    compress_frame_to_slice(frame)
    # Append each 1 pixel-wide slice to the right side of a larger canvas
    composite_image.paste(frame)
composite_image.save('final_image.png')
{% endcodeblock %}
