# Connecting to a MySQL database via Unix Domain Sockets #

With junixsocket, this is now really easy.

Just add junixsocket-_X.Y_.jar and junixsocket-mysql-_X.Y_.jar (as well as MySQL Connector/J) to your classpath (whereas _X.Y_ stands for the junixsocket version, e.g. 1.3).

You may then connect to the specified MySQL server's unix socket (in our example: `/tmp/mysql.sock`) using the following code:

```

 import org.newsclub.net.mysql.AFUNIXDatabaseSocketFactory;

 ...

 Class.forName("com.mysql.jdbc.Driver").newInstance();
 
 Properties props = new Properties();
 props.put("user", "test");
 props.put("password", "test");
 props.put("socketFactory", AFUNIXDatabaseSocketFactory.class.getName());
 props.put("junixsocket.file", "/tmp/mysql.sock");

 Connection conn = DriverManager.getConnection("jdbc:mysql://",
                    props);

```


A complete, working demo class is included in the distribution ([source code](http://code.google.com/p/junixsocket/source/browse/trunk/junixsocket/src/demo/org/newsclub/net/mysql/AFUNIXDatabaseSocketFactoryDemo.java)).