---
comments: true
date: 2011-04-16 14:52:06
layout: post
slug: apple-jdks-openjdk-back-to-benchs
title: Apple JDK's / OpenJDK - back to benchs
wordpress_id: 769
categories:
- OpenJDK
- OS/X
---

It's good to see works in progress for Aqua/Cocoa - AWT ports but what about JVM performances ?



## Test vms


I selected 4 VMs to be tested

`
Apple Java 1.6.0_22 - java version "1.6.0_22"
Java(TM) SE Runtime Environment (build 1.6.0_22-b04-314-10M3406a)
Java HotSpot(TM) 64-Bit Server VM (build 17.1-b03-314, mixed mode)
`

`
Apple Java 1.6.0_24 - java version "1.6.0_24"
Java(TM) SE Runtime Environment (build 1.6.0_24-b07-348-10M3406a)
Java HotSpot(TM) 64-Bit Server VM (build 19.1-b02-348, mixed mode)
`

`
OpenJDK 7 bsd-port - openjdk version "1.7.0-internal"
OpenJDK Runtime Environment (build 1.7.0-internal-henri_2011_04_11_08_24-b00)
OpenJDK 64-Bit Server VM (build 21.0-b07, mixed mode)
`

`
OpenJDK 7 macosx-port - openjdk version "1.7.0-internal"
OpenJDK Runtime Environment (build 1.7.0-internal-b00)
OpenJDK 64-Bit Server VM (build 21.0-b07, mixed mode)
`



## Test system


My test system is an Apple iMac (iMac11,1 )  with Intel i7 2.80Ghz and 8Gb DDR3 1067Mhz, running under SnowLeopard 10.6.7 64bits.
I wanted to test 64bits VMs on a 64bits machine and this time use a stronger processor with more threads (ie: 4 cores with hyperthreading).



### DaCapo Benchmarks


I keep the [DaCapo 9.12-bach](http://www.dacapobench.org/).

Bench tests launched with -n X, ie (java -jar dacapo-9.12-bach.jar -n 10 pmd)

[table id=4 /]

[![](http://blog.hgomez.net/wp-content/uploads/2011/04/Benchs4-1024x576.png)](http://blog.hgomez.net/wp-content/uploads/2011/04/Benchs4.png)


## Conclusion



Latest Apple JVM, 1.6.0-24 perform better than the old 1.6.0-22 in all of the tests and is near OpenJDK 7 results.

OpenJDK 7 from the bsd-port perform a little better than the macosx-port. The main difference in build is bsd-port is using stock gcc whereas macos-port use llvm-gcc.



### bsd-port using stock-gcc during OpenJDK build



[bash]
Compiling /Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/share/vm/adlc/arena.cpp
rm -f ../generated/adfiles/arena.o
/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/ALT_COMPILER_PATH/g++ -D_ALLBSD_SOURCE -D_GNU_SOURCE -DAMD64 -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/share/vm/prims -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/share/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/cpu/x86/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/os_cpu/bsd_x86/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/os/bsd/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/os/posix/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/share/vm/adlc -I../generated -DASSERT -DTARGET_OS_FAMILY_bsd -DTARGET_ARCH_x86 -DTARGET_ARCH_MODEL_x86_64 -DTARGET_OS_ARCH_bsd_x86 -DTARGET_OS_ARCH_MODEL_bsd_x86_64 -DTARGET_COMPILER_gcc -DCOMPILER2 -DCOMPILER1  -fno-rtti -fno-exceptions -pthread -fcheck-new -m64 -pipe -Werror -g -c -o ../generated/adfiles/arena.o /Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-bsdport-x86_64/workspace/hotspot/src/share/vm/adlc/arena.cpp 
[/bash]



### macosx-port using llvm-gcc during OpenJDK build



[bash]
Compiling /Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/share/vm/adlc/arena.cpp
rm -f ../generated/adfiles/arena.o
llvm-g++ -D_ALLBSD_SOURCE -D_GNU_SOURCE -DIA32 -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/share/vm/prims -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/share/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/cpu/x86/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/os_cpu/bsd_x86/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/os/bsd/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/os/posix/vm -I/Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/share/vm/adlc -I../generated -DASSERT -DTARGET_OS_FAMILY_bsd -DTARGET_ARCH_x86 -DTARGET_ARCH_MODEL_x86_32 -DTARGET_OS_ARCH_bsd_x86 -DTARGET_OS_ARCH_MODEL_bsd_x86_32 -DTARGET_COMPILER_gcc -DCOMPILER2 -DCOMPILER1  -fno-rtti -fno-exceptions -pthread -fcheck-new -m32 -march=i586 -mstackrealign -pipe -Werror -g -c -o ../generated/adfiles/arena.o /Users/henri/Documents/jenkins/data/jobs/openjdk-1.7-macosx-universal/workspace/hotspot/src/share/vm/adlc/arena.cpp 
[/bash]

Performances gain in OpenJDK7 VM vs latest Apple 6 VM is smaller than previously (see previous articles on Apple JDK vs OpenJDK 6), switching to OpenJDK 7 will not be only for pure speed but for functionalities.


