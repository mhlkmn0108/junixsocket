# Quick Start #

Building junixsocket requires [Apache Ant](http://ant.apache.org) (>= 1.7) and [JUnit](http://junit.sourceforge.net/) (>= 4.0).

In most cases, compilation is as easy as to just run the `build.xml` ant script:
```
   ant
```

If you get an error, first of all check if the JAVA\_HOME environment variable is set and points to the correct JDK directory. You may override this setting by specifying the ant property "jdk.home", e.g.

```
   ant -Djdk.home=/usr/lib/jvm/java-6-sun
```

Compiling the native libraries probably requires GCC 4. For some platforms, you might need to specify the exact location of the gcc binary. Specify it using the "gcc" property, e.g.:

```
   ant -Dgcc=/usr/bin/gcc-4.3.2
```

# Automated JUnit tests #

If you do not want to run JUnit tests along with the compilation process, use the following switch:

```
   ant -DskipTest=true
```

You may then later run the tests separately using

```
   ant test
```



# Platform-specific Notes #

## Linux ##

If you are running Fedora, RHEL or CentOS, you probably need to install ant-nodeps (for the `javah` ant target) and ant-junit from [jpackage](http://jpackage.org/).

If you have configured yum to use jpackage, but still only get junit 1.6 RPMs, try disabling the base repository:

```
   yum --disablerepo=base install ant-nodeps ant-junit
```


## Mac OS X ##

It should work without installing additional software.

Tested on Leopard (10.5) and Snow Leopard (10.6). Leopard-PPC untested.

## Solaris ##

You need to install GCC 4 (e.g., package `gcc-4.3.2`) and Jakarta ANT (package `SUNWant`).

## Other Platforms ##

In order to use junixsocket, a native JNI library needs to be compiled. This inherently is platform-specific. The binary distribution already provides code for Mac OS X and Linux (both Intel 32-bit and 64-bit).

junixsocket probably runs on other Unixoid systems, but not all of them have been tested. You need to change `build.xml` a little, and it should build. If not, you will have to modify the [JNI C code](http://code.google.com/p/junixsocket/source/browse/trunk/junixsocket/src/main/org/newsclub/net/unix/org_newsclub_net_unix_NativeUnixSocket.c). Use GCC 4 to compile the code.

## 32-bit / 64-bit ##

Some platforms cannot compile code for both 32-bit and 64-bit architectures.
Use one of the following switches to forcibly deactivate compilation of the corresponding architecture:

```
   ant -Dskip32=true
```

```
   ant -Dskip64=true
```