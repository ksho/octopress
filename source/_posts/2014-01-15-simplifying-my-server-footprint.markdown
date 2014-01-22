---
layout: post
title: "Simplifying My Server Footprint"
date: 2014-01-20 17:32:53 -0500
comments: true
published: true
categories:
- dev
- simplifying
---

Lately, I've been looking at ways to cut down on recurring monthly payments for services, subscriptions, and utilities. The costs associated with keeping web servers have added up in recent history and seemed like a good place to start.

Over the years, I've used a number of different hosting services to house my personal web projects. Having a space to hack and build always taught me a lot, and early on in my technical years it ended up filling in a lot of gaps in knowledge if I had relied only on school/classes. From a young age, I learned a substantial slice of my skills as a creative person would come from actually making things.

Some history..

The first host I ever signed up for, back in '98 or '99, was a provider called phenominet -- I gave my parents $4 every month, and they paid my bill. It was great, and looking back probably some of the best money I ever spent -- I had a few friends that were into building blogs and doing cool things in Photoshop, and now I had my own space to showcase everything I made.

A few years later, I went through a GoDaddy phase, another shared hosting provider, because of how cheap it was -- which I learned came at the price of poor performance and lack of control over my server. There wasn't anything particularly interesting about GoDaddy, except eventually learning what I didn't want in a hosting service.

Sometime after I graduated from school, I discovered the world of virtual private servers -- for 20ish dollars I got an entire souped up virtual machine to myself. Not having to worry about hardware, say having a physical server in the closet at home, was a pretty cool value proposition. I signed up and stuck it out with Linode for years -- their lowest tier of service was always more than enough for me.

Fast forward, to November 2013. My roster of servers stands at two of those Linode instances with automatic snapshot backups enabled, four droplet instances at Digital Ocean, and incremental backups of my photos, music, recordings, documents on Amazon S3 and Glacier -- this totals to about $75 per month.

What I realized was, the only non-static site I host is [kenshouler.com](http://kenshouler.com), a wordpress site. So why pay for all the Linodes? When I first spun them up, I learned how to do some basic sysadmin type stuff, consider security, and setup nginx among other things -- though now that I've done those things once, I don't really care to worry about that layer of involvement for a few low-traffic static sites. It's over-engineered.

In an effort to cut down on my monthly costs, with the added benefit of simplifying and abstracting out the whole task of managing a web server, I did a few things.

- Terminated my personal Linode, and started hosting all static sites (including this one), on S3. I looked at a few overviews outlining moving an octopress/jekyll site to S3 [here](https://snikt.net/blog/2012/11/03/moving-octopress-to-amazon-s3-and-cloudfront/) and [here](http://www.ryanonrails.com/blog/2013/05/13/hosting-octopress-with-amazon-s3-and-cloudfront/). Amazon makes it really easy to point a CNAME record at an S3 bucket and render the site living there. Note, that though they both include a recommendation to use [CloudFront](http://en.wikipedia.org/wiki/Amazon_CloudFront) (Amazon's CDN offering) -- I gave it a try, and didn't find the invalidation costs worth the small improvement in page load times.
- Terminated the Linode instance for kenshouler.com and migrated to Digital Ocean -- their droplets (a silly name for a VPS instance) run $5/mo for what the site needs.
- Terminated 3 random droplets I forgot were running at Digital Ocean. At $5, they're easy to spin up and forget to shut down.

Where does that leave me?
<table class="tg-table-light center">
  <tr>
    <th>Service</th>
    <th class="tg-right">11/2013 cost</th>
    <th class="tg-right">01/2014 cost</th>
  </tr>
  <tr class="tg-even">
    <td style="background-color: #ffffff">Linode #1</td>
    <td class="tg-right" style="background-color: #ffffff">$25.00</td>
    <td class="tg-right" style="background-color: #ffffff">$0.00</td>
  </tr>
  <tr>
    <td style="background-color: #ffffff">Linode #2</td>
    <td class="tg-right" style="background-color: #ffffff">$25.00</td>
    <td class="tg-right" style="background-color: #ffffff">$0.00</td>
  </tr>
  <tr class="tg-even">
    <td style="background-color: #ffffff">Digital Ocean</td>
    <td class="tg-right" style="background-color: #ffffff">$17.00</td>
    <td class="tg-right" style="background-color: #ffffff">$5.00</td>
  </tr>
  <tr>
    <td style="background-color: #ffffff">AWS S3</td>
    <td class="tg-right" style="background-color: #ffffff">$6.77</td>
    <td class="tg-right" style="background-color: #ffffff">$8.35</td>
  </tr>
  <tr class="tg-even">
    <td style="background-color: #ffffff">AWS Glacier</td>
    <td class="tg-right" style="background-color: #ffffff">$0.11</td>
    <td class="tg-right" style="background-color: #ffffff">$1.73</td>
  </tr>
  <tr>
    <td class="tg-bf" style="background-color: #F0F0F0">Total</td>
    <td class="tg-right tg-bf" style="background-color: #F0F0F0">$73.88</td>
    <td class="tg-right tg-bf" style="background-color: #F0F0F0">$15.08</td>
  </tr>
</table>

The big gains came from shutting down the Linode VPS's -- I'm sad to see them go, since they were fun to hack around with, but paying for all that power doesn't make sense if I'm not getting anything out of it. Other bonuses will be having most of my bill consolidated at Amazon and the reliability of S3 over an nginx server I have to maintain. The bottom line is I'll save myself ~$60 every month going forward.

Now, onto minimizing my t-shirt footprint.

Karl



