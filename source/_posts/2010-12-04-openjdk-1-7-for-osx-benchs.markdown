---
comments: true
date: 2010-12-04 10:17:10
layout: post
slug: openjdk-1-7-for-osx-benchs
title: OpenJDK 1.7 for OS/X benchs
wordpress_id: 720
categories:
- OpenJDK
- OS/X
---

After building and packaging OpenJDK 1.7 for OS/X, I wanted to see how performed new VMs.


## Test vms


Recents OpenJDK 1.7 32 and 64bits where used :

`
openjdk version "1.7.0-internal"
OpenJDK Runtime Environment (build 1.7.0-internal-henri_2010_12_01_00_46-b00)
OpenJDK Server VM (build 20.0-b02, mixed mode)
`

`
openjdk version "1.7.0-internal"
OpenJDK Runtime Environment (build 1.7.0-internal-henri_2010_12_01_00_49-b00)
OpenJDK 64-Bit Server VM (build 20.0-b02, mixed mode)
`


## Test system


My test system is an Apple Mac Book Pro (MacBookPro5,1) with Intel Core 2 Duo 2.66Ghz and 4Gb DDR3 1067Mhz, running under SnowLeopard 10.6.5 32bits.


### DaCapo Benchmarks


I used again [DaCapo 9.12-bach](http://www.dacapobench.org/), discarding **batik** test, this one requiring a working AWT/Swing support .

Bench tests launched with -n X, ie (java -jar dacapo-9.12-bach.jar -n 10 pmd)

[table id=3 /]


## Conclusion


Good news, two tests **Tomcat** and **tradebeans** now pass the bench

OpenJDK 1.7 64bits perform better than OpenJDK 1.7 32bits and OpenJDK 6.

Even if OpenJDK 1.7 32bits performances are better than Apple Java 6, it's allways behind OpenJDK 1.7 64bits version on OS/X, so you should select the 64bits version if performance is the key for your use.

Next article will cover OpenJDK 1.7 and [jtreg](http://openjdk.java.net/jtreg/), the Regression Test Harness for the OpenJDK platform.
