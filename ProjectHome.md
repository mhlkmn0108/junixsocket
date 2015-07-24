# This project has moved to Github #

This project has moved to https://github.com/kohlschutter/junixsocket

```



```

The following information is outdated and only provided for reference.


# junixsocket #

junixsocket is a Java/JNI library that allows the use of [Unix Domain Sockets](http://www.wsinnovations.com/softeng/articles/uds.html) (AF\_UNIX sockets) from Java.

In contrast to other implementations, junixsocket extends the Java Sockets API (`java.net.Socket, java.net.SocketAddress` etc.) and even supports RMI over AF\_UNIX. It is also possible to use it in conjunction with Connector/J to connect to a local MySQL server via Unix domain sockets.

junixsocket has been written by Christian Kohlschütter. It is released under the Apache 2.0 License.

Commercial support is available through [Kohlschütter Search Intelligence](http://www.kohlschutter.com/).

# News #

  * _(2010-08-11)_ **junixsocket 1.3 released.**
    * Solaris support
    * `InputStream#available()` may now return values > 0 ([Issue 11](http://code.google.com/p/junixsocket/issues/detail?id=11)).
    * Added explicit mapping of java.net.SocketOptions values ([Issue 12](http://code.google.com/p/junixsocket/issues/detail?id=12))
    * Fixed "protocol not available" and "invalid argument" errors occuring in rare cases ([Issue 14](http://code.google.com/p/junixsocket/issues/detail?id=14))
    * Improved some warnings and error messages
    * Improved build process, can now skip building for 32/64 bit

  * _(2010-04-22)_ **junixsocket 1.2 released.**
    * [Bugfixes and improvements](http://code.google.com/p/junixsocket/issues/list?can=1&q=milestone%3ARelease1.2+status%3AFixed%2CVerified%2CDone&colspec=ID+Type+Status+Priority+Milestone+Owner+Summary&cells=tiles).
    * [MySQL unix socket factory](http://code.google.com/p/junixsocket/wiki/ConnectingToMySQL) now available as a separate jar (and with demo code)
    * Now compiles under FreeBSD.
    * Initial support for Tru64.
    * Improved handling of stale socket files.

# Documentation #

Please refer to the [Wiki](http://code.google.com/p/junixsocket/w/list).

Quick links:
  * [Getting Started](http://code.google.com/p/junixsocket/wiki/GettingStarted)
  * [Socket Demo](http://code.google.com/p/junixsocket/source/browse/#svn/trunk/junixsocket/src/demo/org/newsclub/net/unix/demo)
  * [RMI Demo](http://code.google.com/p/junixsocket/source/browse/#svn/trunk/junixsocket/src/demo/org/newsclub/net/unix/demo/rmi)
  * [MySQL Socket Demo](http://code.google.com/p/junixsocket/wiki/ConnectingToMySQL)
  * [API Javadocs](http://junixsocket.googlecode.com/svn/trunk/junixsocket/javadoc/index.html)

# Related work #

  * [JUDS](http://code.google.com/p/juds/) (LGPL, no RMI, not using Java Sockets API)
  * J-BUDS (LGPL, no RMI, not using Java Sockets API, orphaned)
  * gnu.net.local (GPL with Classpath exception, no RMI, not using Java Sockets API, orphaned) -- [Archive.org Mirror](http://web.archive.org/web/20060702213439/http://www.nfrese.net/software/gnu_net_local/overview.html)