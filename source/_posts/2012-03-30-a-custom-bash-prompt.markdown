---
layout: post
title: "A custom bash prompt"
date: 2012-03-30 13:03
comments: true
categories:
- dev
- code
- bash
- colors
---

Yesterday, I fiddled around entirely too much with the style of my terminal prompt. I was inspired by [@krismolendyke](http://twitter.com/#!/krismolendyke)‘s use of the new line for input (note the `\n`), which helps me see things a little clearer when scrolling back in history. Here are some notes about its compoisition:

* The `\u` and `\h` (separated by an `@`) are responsible for username and hostname, respectively.
* `\w` yields the current working directory.. similar, but not the same output as executing pwd. pwd gives you an absolute path, whereas `\w` will print relative to `~` if you happen to be under there.
* The pretty yellow output in parentheses is the current git branch I’m on, if any.
* `\t` displays a 24 hour timestamp
* And finally that `\n` I mentioned to drop the `$` and cursor to a new line.
* Also, the colors are in ASCII (the numbers with an `m\]` after them).
* Take a look at the full `PS1` directive, added to `.bashrc` or `.profile` (don’t forget to source!), and the resulting prompt formatting..

``` bash
PS1='\[\033[01;34m\]\u@\h\[\033[00m\]:\[\033[01;36m\]\w\[\033[01;33m\]$(__git_ps1 "(%s)")\[\033[00m\]:\t\n\[\033[01;33m\]$\[\033[00m\] '
```


