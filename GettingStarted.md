# Introduction #

junixsocket is a Java/JNI library that allows the use of Unix Domain Sockets (AF\_UNIX sockets) from Java. It also provides glue code such that one can actually use RMI over AF\_UNIX.

junixsocket has been written by Christian Kohlschütter. It is released under the Apache 2.0 License.

# Getting the files #

  1. Download the binary and/or source tarball from the [Downloads page](http://code.google.com/p/junixsocket/downloads/list)
  1. Extract the files somewhere
```
    tar xvjf junixsocket-X.Y-bin.tar.bz2
    tar xvjf junixsocket-X.Y-src.tar.bz2
```
> > (where _X.Y_ stands for the version number, e.g. _1.2_)

# Installation #

junixsocket consists of pure Java component that is platform-independent and a platform-dependent JNI-native C library component (for each platform a different library file is provided.

## Installing the native JNI libraries ##

In order to use the Java classes the JNI library needs to be installed on a particular location on your system.

The following native libraries are provided in the [binary tarball](http://code.google.com/p/junixsocket/downloads/list) (directory `lib-native`):

  * `libjunixsocket-linux-1.5-amd64.so`  Linux Intel 64bit
  * `libjunixsocket-linux-1.5-i386.so`  Linux Intel 32bit
  * `libjunixsocket-macosx-1.5-i386.dylib`  OS X Intel 32bit
  * `libjunixsocket-macosx-1.5-x86_64.dylib` OS X Intel 64bit

You can put the native library anywhere in your `java.library.path` (see
http://java.sun.com/docs/books/jni/html/start.html), into the path specified for the Java system property `org.newsclub.net.unix.library.path` and into the path stored in the LIBRARY\_PATH static attribute of the `NativeUnixSocketConfig` class (which is `/opt/newsclub/lib-native` by default (as a platform-independent fall-back), but this can be changed by replacing the class against a custom one).

For initial testing, it is recommended to put the libraries into `/opt/newsclub/lib-native`.

After updating the junixsocket jars, please do not forget to also update the native libraries.

## Installing the jars ##

junixsocket currently comes with four jar files:

  1. `junixsocket-X.Y.jar`  The core library
  1. `junixsocket-rmi-X.Y.jar`  The RMI extension (RMI over AF\_UNIX)
  1. `junixsocket-mysql-X.Y.jar`  MySQL support
  1. `junixsocket-demo-X.Y.jar`  Demo classes (the jar archive contains the Java sources, too).

The core library is required, all the others are optional.

# Basic Usage #

junixsocket supports the [Java Socket API](http://java.sun.com/javase/6/docs/api/java/net/Socket.html). `AFUNIXSocket` and `AFUNIXServerSocket` work just as their AF\_INET (TCP/IP) Socket counterparts, they extend `java.net.Socket` and `java.net.ServerSocket` respectively.

## Connecting to an existing AF\_UNIX Socket ##

```
File socketFile = new File("/path/to/your/socket");
AFUNIXSocket sock = AFUNIXSocket.newInstance();
sock.connect(new AFUNIXSocketAddress(socketFile));
```

## Creating a new AF\_UNIX Server Socket ##

```
File socketFile = new File("/path/to/your/socket");
AFUNIXServerSocket server = AFUNIXServerSocket.newInstance();
server.bind(new AFUNIXSocketAddress(socketFile));
```

# Complete Examples #

junixsocket provides working demos for:

  * [plain Unix Domain Socket client/server communication](http://code.google.com/p/junixsocket/source/browse/#svn/trunk/junixsocket/src/demo/org/newsclub/net/unix/demo) and for
  * [RMI-over-Unix-Socket](http://code.google.com/p/junixsocket/source/browse/#svn/trunk/junixsocket/src/demo/org/newsclub/net/unix/demo/rmi).
  * [MySQL-over-Unix-Socket](http://code.google.com/p/junixsocket/source/browse/trunk/junixsocket/src/demo/org/newsclub/net/mysql/).

# Caveats #

## Maximum path length ##

At system-level the pathname of a Unix domain sockets is limited in length. The maximum varies from one OS to another. Currently, junixsocket limits the maximum pathname length to 103 bytes (this may mean less characters). If the maximum length is exceeded an Exception is thrown.

It is therefore recommended to use short pathnames whenever possible.

## Security ##

Unix domain server sockets are created with read-write privileges for everybody on the sytem, just like TCP/IP sockets are accessible for local users.

If you want to restrict access to a particular user or group, simply create the socket in a directory that has proper access restrictions.

## Ports ##

Whereas TCP/IP sockets point to ports at particular Internet addresses, AF\_UNIX sockets point to special files on the local file system. The notion of "port" is not necessary in this case.

However, we need ports for RMI. This is why `AFUNIXSocketAddress` also supports them. Port support may also come handy in other situations, especially when an existing application expects a particular port on a Socket. Please be aware that specifying a particular port number has no effect for non-RMI connections.