---
comments: true
date: 2012-03-21 08:31:18
layout: post
slug: building-universal-apache-tomcat-connector-mod_jk-on-osx
title: Building Universal Apache Tomcat Connector (mod_jk) on OSX
wordpress_id: 1006
categories:
- jk
- OS/X
- Tomcat
---

Build Universal Apache Tomcat Connector (mod_jk) for OSX follow tricks used for Apache Tomcat Native Library.

``` bash
CFLAGS='-arch i386 -arch x86_64' APXSLDFLAGS='-arch i386-arch x86_64'
```

Here is a small script to do it :

``` bash
#!/bin/sh
#

JK_VERSION=1.2.37

curl http://mir2.ovh.net/ftp.apache.org/dist/tomcat/tomcat-connectors/jk/tomcat-connectors-${JK_VERSION}-src.tar.gz -o tomcat-connectors-${JK_VERSION}-src.tar.gz
tar xvzf tomcat-connectors-${JK_VERSION}-src.tar.gz
cd tomcat-connectors-${JK_VERSION}-src/native
 
./configure --with-apxs=/usr/sbin/apxs CFLAGS='-arch i386 -arch x86_64' APXSLDFLAGS='-arch i386-arch x86_64'
make clean
make
```

Installation is pretty simple : 

``` bash
sudo cp apache-2.0/.libs/mod_jk.so /usr/libexec/apache2/
```

You could then restart your Apache HTTPd server to get new mod_jk used :

``` bash
sudo /usr/sbin/apachectl restart
```
