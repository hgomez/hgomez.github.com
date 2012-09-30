---
comments: true
date: 2011-04-18 19:39:20
layout: post
slug: apple-jdk%e2%80%99s-openjdks-%e2%80%93-core2duo-vs-core-i7
title: Apple JDK’s / OpenJDK's – Core2Duo vs Core i7
wordpress_id: 825
categories:
- OpenJDK
- OS/X
---

Previously I did benchmark of Apple VMs and OpenJDK 6 and I wanted to see how all of the JVMs available today on our Mac on two systems, an old Core2Duo and a newer Core i7. And also see how they perform 32 / 64 bits kernel mode.

So I redo full dacapo bench suite to include OpenJDK 6, and we have now 5 VMs (3 Java 6 and 2 Java 7) :




	
  * Apple Java 1.6.0_22 - Java HotSpot(TM) 64-Bit Server VM (build 17.1-b03-314, mixed mode)

	
  * Apple Java 1.6.0_24 - Java HotSpot(TM) 64-Bit Server VM (build 19.1-b02-348, mixed mode)

	
  * OpenJDK 7 bsd-port - OpenJDK 64-Bit Server VM (build 21.0-b07, mixed mode)

	
  * OpenJDK 7 macosx-port - OpenJDK 64-Bit Server VM (build 21.0-b07, mixed mode)

	
  * OpenJDK 6 macports - OpenJDK 64-Bit Server VM (build 17.0-b16, mixed mode)





### Results on MacBook Pro - Core2Duo 2.66Ghz - 32bits kernel



[table id=6 /]

[![](http://blog.hgomez.net/wp-content/uploads/2011/04/BenchJVMs-MBP-1024x555.png)](http://blog.hgomez.net/wp-content/uploads/2011/04/BenchJVMs-MBP.png)



### Results on iMac - Core i7 2.8Ghz -  64bits kernel



[table id=5 /]

[![](http://blog.hgomez.net/wp-content/uploads/2011/04/BenchIMac-1024x549.png)](http://blog.hgomez.net/wp-content/uploads/2011/04/BenchIMac.png)





## Conclusion



As seen if [previous article](http://blog.hgomez.net/2011/04/16/apple-jdks-openjdk-back-to-benchs/),  latest Apple JVM, 1.6.0-24 perform better than the old 1.6.0-22, and still behind OpenJDK 7 and even OpenJDK 6.  OpenJDK 7 bsd-port is still faster (by a small factor) than OpenJDK 7 from macosx-port (built with LLVM), in both simple threaded (Core2Duo, 2 cores) and large threaded (i7 4 cores with hyperthreading).

This benchmark show how good is [Intel Core i7](http://ark.intel.com/Product.aspx?id=41316) comparing to previous generation [Intel Core2Duo](http://ark.intel.com/Product.aspx?id=37130&code=T9550), roughly twice as fast.

