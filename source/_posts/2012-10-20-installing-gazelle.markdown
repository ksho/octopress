---
layout: post
title: "Installing Gazelle"
date: 2012-10-20 15:02
comments: true
categories: 
published: false
---

I've wanted to host my own [bittorrent tracker](http://en.wikipedia.org/wiki/BitTorrent_tracker) for some time. Mostly as a excercise, but also to share files among a small group of friends. I had heard about [Gazelle](http://code.google.com/p/gazellewhatcd/), written by the devs at what.cd, and thought this might be a good place to start. What follows is how I got it up and running over the course of a day or so. I'll continue assuming you have some basic knowledge on getting around in unix, but will do my best to go into detail and discuss the pitfalls I encountered that weren't as well documented. Here it goes.

I'll be moving through [the guide](http://code.google.com/p/gazellewhatcd/wiki/InstalationDebian) provided by the gazelle dev team.

I use [Linode](http://www.linode.com) to host my VPS, but any similar service will do, I'm sure. 

First, spin up a new instance with a 32 bit version of Debian 6. Then update the package index and upgrade all existing packages.
```
$ apt-get update
$ apt-get upgrade
```

Install dependencies for Gazelle.
```
$ apt-get install build-essential apache2 php5 libapache2-mod-php5 mysql-server libmysqlclient15-dev php5-mysql memcached php5-memcache php5-gd php5-mcrypt subversion automake
$ apt-get install cmake g++ libboost-date-time-dev libboost-dev libboost-filesystem-dev libboost-program-options-dev libboost-regex-dev libboost-serialization-dev make zlib1g-dev
```

Make a directory for your gazelle site to live in.
```
$ mkdir -p /home/webapps/gaz/
```

Create a file at `/etc/apache2/sites-available/` named for the domain you're using for your site (no extension is necessary on this file). Inside it, paste the following, while changing the ServerAdmin, ServerName, ServerAlias, and paths:
```
# Standard http port
# NameVirtualHost *:80

<VirtualHost *:80>
    ServerAdmin leet@sysop.com
    ServerName server.org
    ServerAlias www.server.org

    DocumentRoot /home/webapps/gaz/

    <Directory “/home/webapps/gaz/captcha”>
    Order deny,allow
    Deny from all
    </Directory>

    <Directory “/home/webapps/gaz/classes”>
    Order deny,allow
    Deny from all
    </Directory>

    <Directory “/home/webapps/gaz/sections”>
    Order deny,allow
    Deny from all
    </Directory>

    <Directory “/home/webapps/gaz/torrents”>
    Order deny,allow
    Deny from all
    </Directory>

    <Files ~ “^\.ht|\.ini|\.inc|\.sql”>
    Order deny,allow
    Deny from all
    </Files>

</VirtualHost>
```

The guide mentions how to enable SSL if you'd like. I have yet to set this up.


