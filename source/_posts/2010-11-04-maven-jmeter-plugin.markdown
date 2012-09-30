---
comments: true
date: 2010-11-04 18:13:48
layout: post
slug: maven-jmeter-plugin
title: 'Maven JMeter plugin '
wordpress_id: 592
categories:
- Java
- Maven
---

While playing with JMeter Maven plugin, I got some problems :

First the official Jakarta plugin is pretty old and no more maintened.

So you should get a new one, from [GoogleCode](http://code.google.com/p/jmeter-maven-plugin/) 
This project moved to [GitHub](https://github.com/Ronnie76er/jmeter-maven-plugin)

Great project but it miss 2 dependencies, **commons-logging** and **soap**
Without **commons-logging** your tests may fail and you could see :
[bash]
Error in NonGUIDriver java.lang.NullPointerException
[INFO] ------------------------------------------------------------------------
[ERROR] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] There were test errors
[/bash]

The fix is easy, get the plugin project and add the following dependencies in it :

[xml]
		
			soap
			soap
			2.3.1
		

		
			commons-logging
			commons-logging
			1.1.1
		
[/xml]

Just rebuild and install (or deploy), this updated plugin, may be changing it's version from **1.0** to **1.1-SNAPSHOT** to avoid conflict with current one.

Full pom.xml is here :

[xml]

	4.0.0
	org.apache.jmeter
	maven-jmeter-plugin
	maven-plugin
	1.0
	Maven JMeter Plugin
	http://jakarta.apache.org/jmeter

	
		
			ant
			ant
			1.6
		
		
			commons-io
			commons-io
			1.2
		
		
			org.apache.maven
			maven-plugin-api
			2.0
		
		
			org.apache.maven
			maven-project
			2.0.9
		
		
			junit
			junit
			3.8.1
			test
		
		
			org.apache.jmeter
			jmeter
			2.3
		

		
			soap
			soap
			2.3.1
		

		
			commons-logging
			commons-logging
			1.1.1
		

		
			org.apache.jmeter
			jmeter
			2.3
		
		
			org.apache.maven.wagon
			wagon-webdav
			1.0-beta-2
		
	
	
		
			central
			Gestalt Central Repo
			dav://artifactory.int.gestalt-llc.com:8080/archiva/repository/repo
		

	

	
		
			
				org.apache.maven.plugins
				maven-compiler-plugin
				2.0.2
				
					1.5
					1.5
				
			
			
				org.apache.maven.plugins
				maven-surefire-plugin
				2.3
			
		
	

 
[/xml]

I hope this plugin will soon include these fixes and update JMeter to its latest version, 2.4 :)

