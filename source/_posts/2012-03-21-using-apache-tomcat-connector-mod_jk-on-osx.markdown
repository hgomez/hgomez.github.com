---
comments: true
date: 2012-03-21 08:48:34
layout: post
slug: using-apache-tomcat-connector-mod_jk-on-osx
title: Using Apache Tomcat Connector (mod_jk) on OSX
wordpress_id: 1017
categories:
- jk
- OS/X
---

You'll need first mod_jk installed, follow [Building Guide](http://blog.hgomez.net/2012/03/21/building-universal-apache-tomcat-connector-mod_jk-on-osx/).

Create /etc/apache2/other/jk.conf :

``` bash
# Load JK Module
LoadModule jk_module     libexec/apache2/mod_jk.so
# JK workers.properties
JkWorkersFile /etc/apache2/other/workers.properties
# JK shared memory location
JkShmFile     /var/log/apache2/mod_jk.shm
# JK logs
JkLogFile     /var/log/apache2/mod_jk.log
# JK log level [debug/error/info]
JkLogLevel    info
# JK timestamp log format
JkLogStampFormat "[%a %b %d %H:%M:%S %Y] "
```

Create /etc/apache2/other/workers.properties

``` bash
worker.list=jenkins,watch,manage

# Set properties for worker jenkins (ajp13)
worker.jenkins.type=ajp13
worker.jenkins.host=localhost
worker.jenkins.port=8009

# status workers
worker.watch.type=status
worker.watch.read_only=true
worker.watch.mount=/user/status/jk
worker.manage.type=status
worker.manage.mount=/admin/status/jk
```

I choose to use VirtualName Hosting and so defined one into /etc/apache2/extra/httpd-vhosts.conf :

``` bash
NameVirtualHost *:80

<VirtualHost *:80>

    ServerName  mbpbuilder.hgomez.net
    ServerAlias mbpbuilder
    ServerAdmin webmaster@mbpbuilder.hgomez.net

    ErrorLog    "/var/log/apache2/mbpbuilder.org-error_log"
    CustomLog   "/var/log/apache2/mbpbuilder-access_log" common

    JkMount  /* jenkins

</VirtualHost>
```
