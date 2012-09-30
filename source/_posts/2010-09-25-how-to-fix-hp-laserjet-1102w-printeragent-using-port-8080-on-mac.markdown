---
comments: true
date: 2010-09-25 13:07:22
layout: post
slug: how-to-fix-hp-laserjet-1102w-printeragent-using-port-8080-on-mac
title: How to fix HP Laserjet 1102w printerAgent using port 8080 on Mac ?
wordpress_id: 562
categories:
- OS/X
---

I recently bought a new Laser printer, a HP Laserjet 1102w. A very good printer bundled with a very rich firmware supporting WIFI Wep/WPA/WPA2,  Bonjour, SNMP v1/v2, a web interface and much more. A definitive good choice but with a real problem for the Java developer.

Why ? Because HP printer agent is using the 8080 port, the default http port for Tomcat, JBoss and others servlet engines/application servers.

Of course, you could update Tomcat or JBoss default listen ports but you could also try to update the HP printerAgent default port. 
There is no way for now from the UI but you could hack the driver properties.

The settings live under user directory, ie : ~/Library/LaunchAgents/com.hp.printerAgent.plist

[xml]




       Label
       com.hp.printerAgent
       OnDemand
       
       Program
       /Library/Printers/hp/laserjet/P1100_1560_1600Series/printerAgent
       ProgramArguments
       
       /Library/Printers/hp/laserjet/P1100_1560_1600Series/printerAgent
       
       RunAtLoad
       
       ServiceIPC
       
       Sockets
       
               MyListenerSocket
               
                       SockServiceName
                       8080
               
       


[/xml]

Just change the **SockServiceName** from 8080 to another port, ie 58080.

Use a Text editor or a good old sed :

[bash]
sudo sed -i "" -e "s|8080|58080|g" ~/Library/LaunchAgents/com.hp.printerAgent.plist
[/bash]

Restart your Mac and check the ports in listening mode :

[bash]
MacBook-Pro-de-Rico:~ henri$ netstat -an | grep LISTEN
tcp6       0      0  *.3689                 *.*                    LISTEN
tcp4       0      0  *.3689                 *.*                    LISTEN
tcp4       0      0  *.88                   *.*                    LISTEN
tcp6       0      0  *.88                   *.*                    LISTEN
tcp4       0      0  *.3306                 *.*                    LISTEN
tcp46      0      0  *.80                   *.*                    LISTEN
tcp46      0      0  *.5900                 *.*                    LISTEN
tcp4       0      0  *.58080                *.*                    LISTEN
tcp6       0      0  *.58080                *.*                    LISTEN
tcp46      0      0  *.5204                 *.*                    LISTEN
tcp4       0      0  *.5204                 *.*                    LISTEN
tcp4       0      0  *.22                   *.*                    LISTEN
tcp6       0      0  *.22                   *.*                    LISTEN
tcp4       0      0  *.139                  *.*                    LISTEN
tcp4       0      0  *.445                  *.*                    LISTEN
tcp4       0      0  *.548                  *.*                    LISTEN
tcp6       0      0  *.548                  *.*                    LISTEN
tcp4       0      0  127.0.0.1.631          *.*                    LISTEN
tcp6       0      0  ::1.631                *.*                    LISTEN
[/bash]

Et voila

