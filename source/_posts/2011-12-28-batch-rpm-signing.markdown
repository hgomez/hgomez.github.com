---
comments: true
date: 2011-12-28 17:05:42
layout: post
slug: batch-rpm-signing
title: Batch rpm signing
wordpress_id: 939
categories:
- RPM
---

I'm using [Jenkins](http://jenkins-ci.org/) to build RPMs with free-style scripts.  

Decent RPM packager should sign his RPMs so they could be checked by yum/zypper tools.




Here you could be in trouble since rpm signing require a password to be passed in command line :






[bash]
rpm --addsign -D "_signature gpg" -D "_gpg_name packagers@myforge.org" RPMS/noarch/myjenkins-1.0.0-1.noarch.rpm<br />
Enter pass phrase:<br />
[/bash]






It's quite problematic for a RPM build factory.




After digging around Internet, best solution appears to be using [expect](http://expect.sourceforge.net/) and I developped a simple script for such purpose with following constraints :






  * packager gpg name should be parametized (to avoid injecting it in ~/.rpmmacros)


  * gpg passphrase should be provided to command line (could be read from a secret file)



[bash]
#!/usr/bin/expect -f
#
# rpmsign-batch.expect : expect powered rpm signing command
#

proc usage {} {
        send_user "Usage: rpmsign-batch.expect gpgname passphrase rpmfile\n\n"
        exit
}

if {[llength $argv]!=3} usage

set gpgname [lrange $argv 0 0]
set passphrase [lrange $argv 1 1]
set rpmfile [lrange $argv 2 2]

send_user "passphrase=$passphrase gpgname=$gpgname\n"

spawn rpm --addsign -D "_signature gpg" -D "_gpg_name $gpgname" $rpmfile
expect -exact "Enter pass phrase: "
send -- "$passphrase\r"
expect eof
[/bash]

You could then use it to sign rpms from your freestyle jobs like :

[bash]
# Password provided in clear in job (weird)
rpmsign-batch.expect packagers@myforge.org mypassphrase RPMS/noarch/myjenkins-1.0.0-1.noarch.rpm

# Password grabbed from a secret file (better)
PASSPHRASE=`cat /my/secret-passphrase-file`
rpmsign-batch.expect packagers@myforge.org $PASSPHRASE RPMS/noarch/myjenkins-1.0.0-1.noarch.rpm
[/bash]

