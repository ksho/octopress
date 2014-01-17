---
layout: post
title: "Simplifying my VPS Footprint"
date: 2014-01-15 17:32:53 -0500
comments: true
categories: 
---

Over the years, I've gone through a number of different hosting services as home to my personal web projects. Having a space to hack and build always taught me a lot, and early on in my years it ended up filling in a lot of gaps in knowledge if I had relied only on school/classes. I learned pretty early on that a substantial slice of my skills as a creative person come from actually making things.

The first host I ever signed up for, back in '98 or '99, was a provider called phenominet -- I gave my parents $4 every month, and they paid my bill. It was great, and looking back probably some of the best money I ever spent -- I had a few friends that were into building blogs and doing cool things in Photoshop, and now I had my own space to showcase everything I made.

A few years later in college, I went through a godaddy phase, another shared service, because of how cheap it was (and is!). That came at a price though. There wasn't anything particularly interesting about GoDaddy, except my eventually learning what I didn't want in a hosting service.

Sometime after I graduated from school, I discovered there was this world of virtual private servers I could use to have a whole machine, virtually anyway ;), all to myself. I'd be reponsible for everything but the hardware -- it was more or less leasing a computer in some clandestine location. After starting my first job, it was trivial handing over $20 every month for something I got so much value out of. I signed up and stuck it out with Linode for years -- their lowest tier of service was more than enough for me.

Fast forward, to November 2013. My roster of servers stands at two of those Linode instances with automatic snapshot backups enabled, four droplet instances at Digital Ocean, and incremental backups of my photos, music, recordings, documents on Amazon S3 and Glacier -- this totals to about $75 per month.

Here's a breakdown:  
Linode ![Linode invoice](./images/posts/linodeInvoice112013.png)  
Digital Ocean ![DO invoice](./images/posts/doInvoice112013.png)  
AWS ![AWS](./images/posts/awsInvoice112013.png)

What I realized was, the only non-static site I host is kenshouler.com, a wordpress site. So why pay for all the Linodes? Well, I learned how to do some basic sysadmin type stuff, consider security, and setup nginx among other things -- though now that I've done these things once, I don't really care to worry about that layer of involvement for a few low-traffic static sites. It's over-engineered.

In an effort to cut down on my monthly costs, with the added benefit of simplifying and abstracting out the whole task of managing a web server, I did a few things.
- Terminated my personal Linode, and started hosting all static sites (including this one), on S3.
- Terminated the Linode instance for kenshouler.com and migrated to Digital Ocean -- their droplets (a silly name for a VPS instance) run $5/mo for what the site needs.
- Terminate 3 random droplets I forgot were running at Digital Ocean.

As it stands today:
- Digital Ocean droplet- $5/mo
- S3 (karlshouler.com, Arq backups of photos, documents, recordings)- $8/mo
- Glacier (~200 GB of Arq backups)- $2/mo

It's really nice having one bill at amazon for everything.