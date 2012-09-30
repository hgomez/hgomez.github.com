---
comments: true
date: 2012-01-28 09:13:42
layout: post
slug: uninstalling-macfuse-on-lion
title: Uninstalling MacFuse on Lion
wordpress_id: 958
categories:
- OS/X
---

If you installed MacFuse on Lion (10.7) and tried to uninstall you may encountered the following error :

``` bash
sudo /Library/Filesystems/fusefs.fs/Support/uninstall-macfuse-core.sh
MacFUSE Uninstaller: Can not find the Archive.bom for MacFUSE Core package.
```

Uninstaller didn't check for Lion (uname -r reporting 11.x).
So fix is easy, just edit uninstaller script **/Library/Filesystems/fusefs.fs/Support/uninstall-macfuse-core.sh** and add 11*) in case next to 10*)

``` bash
...

OS_RELEASE=`/usr/bin/uname -r`
case "$OS_RELEASE" in 
  8*)
    log "Incorrect uninstall. Use the Tiger version please."
    exit 1
    ;;
  9*)
    PACKAGE_RECEIPT="$INSTALL_VOLUME/Library/Receipts/MacFUSE Core.pkg"
    OUTER_PACKAGE_RECEIPT="$INSTALL_VOLUME/Library/Receipts/MacFUSE.pkg"
    BOMFILE="$PACKAGE_RECEIPT/Contents/Archive.bom"
    ;;
  10*|11*)
     PACKAGE_RECEIPT=""
     BOMFILE="$INSTALL_VOLUME/var/db/receipts/com.google.macfuse.core.bom"
     ;;
esac
```
