JAMP
====
A portable platform-independent PHP, webserver and database stack in Java.
[See blog post.](http://www.webdevelopersdiary.com/1/post/2012/07/jamp-an-ultra-portable-php-web-server-and-database-stack-in-java.html)

php.ini
=======
php.ini is located at src/main/webapp/WEB-INF/php.ini.

Internal database
===================
By default the database is temporary, meaning if you stop the web server, the data is erased.
If you want to use a persistent database file instead of the temporary in-memory database,
go to src/main/webapp/WEB-INF/jetty-env.xml and change line

	<Set name="url">jdbc:h2:mem:;MODE=MYSQL</Set>


to

	<Set name="url">jdbc:h2:filename;MODE=MYSQL</Set>


Where you replace 'filename' with a relative path to a file (relative to pom.xml)
or an absolute path to a file. Note that "mem:" has an extra ":" after it and "filename" does not.
For more information about the H2 JDBC URL see [H2's feature list](http://www.h2database.com/html/features.html#database_url).

External MySQL database
=======================
If you want to connect to an external MySQL database, go to src/main/webapp/WEB-INF/web.xml
and comment the following block:

	<init-param>
		<param-name>database</param-name>
		<param-value>java:comp/env/jdbc/h2</param-value>
	</init-param>

With this code block still enabled, Quercus will just ignore all connect parameters
and connect you with the internal database instead.
