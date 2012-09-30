---
comments: true
date: 2010-11-16 20:36:15
layout: post
slug: forest-extension-fixes-for-mercurial-1-7
title: Forest extension fixes for Mercurial 1.7
wordpress_id: 649
categories:
- Mercurial
- OpenJDK
---

I'm using Mercurial 1.7 from MacPorts to sync with OpenJDK sources. This operation is usually done with **hg fclone**

[bash]
hg fclone http://hg.openjdk.java.net/bsd-port/bsd-port
[/bash]

**fclone** came from **forest**

Mercurial 1.7 changes some API and call to **do_read** should be changed to **_call**.

Hopefully, I found a maintained **Forest** for Mercurial by GXTI and they now handle correctly  pre/post Mercurial 1.6 or 1.7.

To install this updated extension.

[bash]
hg clone https://bitbucket.org/gxti/hgforest
[/bash]

Make sure this forest.py is included in your **~/.hgrc**

[bash]
hgext.forest=/Users/henri/hgforest/forest.py
[/bash]
