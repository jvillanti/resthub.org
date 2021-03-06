============
Spring Stack
============

RESThub 2 Spring stack provides a server side full stack and guidelines for building Java/Spring application (usually web application, but not only).

.. contents::
    :depth: 4

It provides a coherent stack based on:
    * `Java <http://www.oracle.com/technetwork/java/javase/downloads/index.html>`_ (at least JDK6, JDK7 recommended)
    * `Tomcat 7 <http://tomcat.apache.org/download-70.cgi>`_ (RESThub can also be used for non web applications)
    * Spring 3.1 (`reference manual <http://static.springsource.org/spring/docs/3.1.x/spring-framework-reference/html>`_ and `Javadoc <http://static.springsource.org/spring/docs/3.1.x/javadoc-api/>`_)
    * SQL and NoSQL Persistence with `Spring Data <http://www.springsource.org/spring-data>`_
    * Logging with SLF4J (`manual <http://www.slf4j.org/manual.html>`_) and Logback (`manual <http://logback.qos.ch/manual/index.html>`_)
    * Maven 3.0 (`complete reference <http://www.sonatype.com/books/mvnref-book/reference/public-book.html>`_) is the reference build tool used.

It provides the following modules:
    * **resthub-archetypes**: project templates (WAR or multi-module layout) to start quickly a new project
    * **resthub-jpa**: support for JPA based persistence based on Spring Data, including embedded H2 database for testing
    * **resthub-mongodb**: support for MongoDB based on Spring Data
    * **resthub-test**: testing stack based on TestNG, Mockito and Fest Assert 2
    * **resthub-web-server**: generic REST webservices support based on Spring MVC 3.1 including exception mapping to HTTP status codes
    * **resthub-web-client**: simple to use HTTP client based on AyncHttpClient

The whole RESThub 2.0 Spring stack `Javadoc <http://resthub.org/javadoc/2.0>`_ is available.

Changelog
=========

* 2012-12-04: `RESThub Spring stack 2.0.0 GA has been released <http://pullrequest.org/2012/12/04/resthub-2.html>`_!
* 2012-11-13: RESThub Spring stack 2.0-rc4 has been released
* 2012-10-24: RESThub Spring stack 2.0-rc3 has been released
* 2012-10-22: `RESThub Spring stack 2.0-rc2 <https://github.com/resthub/resthub-spring-stack/issues?milestone=12&state=closed>`_ has been released
* 2012-10-01: `RESThub Spring stack 2.0-rc1 <https://github.com/resthub/resthub-spring-stack/issues?milestone=13&state=closed>`_ has been released
* 2012-08-29: `RESThub Spring stack 2.0-beta2 <https://github.com/resthub/resthub-spring-stack/issues?milestone=11&state=closed>`_  has been released
* 2012-05-06: `RESThub Spring stack 2.0-beta1 <https://github.com/resthub/resthub-spring-stack/issues?milestone=8&state=closed>`_ has been released
* 2011-06-19: RESThub 1.1 and RESThub JS 1.1 have been released
* 2010-11-17: RESThub 1.0 has been released

Bootstrap your project
======================

Java and Maven 3 should be installed on your computer. RESThub based applications are usually developed thanks to a Java IDE like Eclipse, Netbeans or IntelliJ IDEA. If you don't know which IDE to choose, `Netbeans <http://netbeans.org/>`_ is recommended since it is free and has great Maven support and Java/Javascript capabilities.

The easiest way to start is to use RESThub archetypes to create your first web application.

You will have to choose between the following RESThub archetypes:
    * **resthub-jpa-backbonejs-archetype**: simple HTML5 web application with JPA persistence
    * **resthub-mongodb-backbonejs-archetype**: simple HTML5 web application with MongoDB persistence
    * **resthub-jpa-backbonejs-multi-archetype**: Multimodules HTML5 web application with JPA persistence
    * **resthub-mongodb-backbonejs-multi-archetype**: Multimodules HTML5 web application with MongoDB persistence

To create your project based or RESThub archetypes, just open a command line terminal, and copy/paste the line related to the archetype you chosed:

.. code-block:: bash

    mvn archetype:generate -DarchetypeArtifactId=resthub-jpa-backbonejs-archetype -DarchetypeGroupId=org.resthub -DarchetypeVersion=2.0.0
    mvn archetype:generate -DarchetypeArtifactId=resthub-mongodb-backbonejs-archetype -DarchetypeGroupId=org.resthub -DarchetypeVersion=2.0.0
    mvn archetype:generate -DarchetypeArtifactId=resthub-jpa-backbonejs-multi-archetype -DarchetypeGroupId=org.resthub -DarchetypeVersion=2.0.0
    mvn archetype:generate -DarchetypeArtifactId=resthub-mongodb-backbonejs-multi-archetype -DarchetypeGroupId=org.resthub -DarchetypeVersion=2.0.0
 
After choosing the right archetype and answering a few questions, your project is generated and ready to use.
You can run it thanks to built-in Jetty support:

.. code-block:: bash

    mvn jetty:run

Tutorial
========

You should follow `RESThub Spring Stack tutorial <tutorial/spring.html>`_ in order to learn step by step how to use it.

Project layout
==============

Let's take a look at a typical RESThub based application...

RESThub stack based projects follow the "Maven standard" project layout:
    * /pom.xml: the Maven configuration file which defines dependencies, plugins, etc.
    * /src/main/java: your java classes go there
    * /src/main/java/\*\*/WebAppInitializer.java: Java based WebApp configuration (replaces your old web.xml file)
    * /src/main/resources: your xml and properties files go there
    * /src/main/resources/applicationContext.xml: this is your Spring application configuration file. Since we mainly use annotation based configuration, 
    * /src/main/webapp: your HTML, CSS and javascript files go there
 
RESThub based applications usually use one of these 2 layouts:
    * A single WAR project
    * A multi-module project with the following sub-modules:
        * myproject-webapp (WAR): it is your web application, it contains static resources, environment specific configuration and it declares dependencies to other modules in the pom.xml
        * myproject-contract (JAR): contains your POJOs (Entities, DTO ...) and service interface. This module should be used by web client or RPC mechanism to know the public classes and interfaces of your application without retreiving all the implementation dependencies. As a consequence, if you need to add some implementation dependencies (usually needed for annotations), add them as optional Maven dependencies.
        * myproject-core (JAR): your project implementation (controllers, service implementations, repositories)

Check the `RESThub 2 Todo example application <https://github.com/resthub/todo-example>`_ source code to learn how to design your RESThub based web application.
 
How to run the todo application:
    * Download the `zip file <https://github.com/resthub/todo-backbone-example/zipball/master>`_ and extract it
    * Install `MongoDB <http://www.mongodb.org/downloads>`_, create the data folder (C:\\data\\db or /data/db by default) and run mondgod
    * Run mvn jetty:run in the todo-backbone-example directory
    * Open your browser and browse http://localhost:8080/index.html

Configuration
-------------

You will find below the typical configuration file for your application.

Maven
~~~~~

Your project pom.xml defines your project name, version, dependencies and plugins used.
Please notice that it is easier to let RESThub archetypes create the pom.xml automatically for you.

pom.xml example:

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>com.mycompany</groupId>
        <artifactId>myproject</artifactId>
        <version>1.0-SNAPSHOT</version>
        <packaging>war</packaging>

        <name>My project</name>

        <properties>
            <resthub.spring.stack.version>2.0.0</resthub.spring.stack.version>
        </properties>

        <dependencies>
            <dependency>
                <groupId>org.resthub</groupId>
                <artifactId>resthub-mongodb</artifactId>
                <version>${resthub.spring.stack.version}</version>
            </dependency>
            <dependency>
                <groupId>org.resthub</groupId>
                <artifactId>resthub-web-server</artifactId>
                <version>${resthub.spring.stack.version}</version>
            </dependency>
            <dependency>
                <groupId>javax.servlet</groupId>
                <artifactId>javax.servlet-api</artifactId>
                <version>3.0.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>

        <build>
            <finalName>todo</finalName>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>2.5.1</version>
                    <configuration>
                        <encoding>UTF-8</encoding>
                        <source>1.7</source>
                        <target>1.7</target>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-resources-plugin</artifactId>
                    <version>2.6</version>
                    <configuration>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-war-plugin</artifactId>
                    <version>2.3</version>
                    <configuration>
                        <failOnMissingWebXml>false</failOnMissingWebXml>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.mortbay.jetty</groupId>
                    <artifactId>jetty-maven-plugin</artifactId>
                    <version>8.1.7.v20120910</version>
                    <configuration>
                        <!-- We use non NIO connector in order to avoid read only static files under windows -->
                        <connectors>
                            <connector implementation="org.eclipse.jetty.server.bio.SocketConnector">
                                <port>8080</port>
                                <maxIdleTime>60000</maxIdleTime>
                            </connector>
                        </connectors>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </project>

RESThub dependencies are available on Maven Central:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-jpa</artifactId>
        <version>2.0.0</version>
    </dependency>

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-mongodb</artifactId>
        <version>2.0.0</version>
    </dependency>

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-web-server</artifactId>
        <version>2.0.0</version>
    </dependency>

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-web-client</artifactId>
        <version>2.0.0</version>
    </dependency>

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-test</artifactId>
        <version>2.0.0</version>
        <scope>test</scope>
    </dependency>

Web application initializer
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Web application initializer replaces the old web.xml file used with Servlet 2.5 or older webapps. It has the same goal, but since it is Java based, it is safer (compilation check, autocomplete).

WebAppInitializer.java example:

.. code-block:: java

    public class WebAppInitializer implements WebApplicationInitializer {

        @Override
        public void onStartup(ServletContext servletContext) throws ServletException {
            XmlWebApplicationContext appContext = new XmlWebApplicationContext();
            appContext.getEnvironment().setActiveProfiles("resthub-jpa", "resthub-web-server");
            String[] locations = { "classpath*:resthubContext.xml", "classpath*:applicationContext.xml" };
            appContext.setConfigLocations(locations);

            ServletRegistration.Dynamic dispatcher = servletContext.addServlet("dispatcher", new DispatcherServlet(appContext));
            dispatcher.setLoadOnStartup(1);
            dispatcher.addMapping("/*");

            servletContext.addListener(new ContextLoaderListener(appContext));
        }
    }

Spring profiles
~~~~~~~~~~~~~~~

RESThub 2 uses `Spring 3.1 profiles <http://blog.springsource.com/2011/02/14/spring-3-1-m1-introducing-profile/>`_ to let you activate or not each module. It allows you to add Maven dependencies for example on resthub-jpa and resthub-web-server and let you control when you activate these modules. It is especially useful when running unit tests: when testing your service layer, you may not need to activate the resthub-web-server module.

You can also use Spring profile for your own application Spring configuration.

Profile activation on your webapp is done very early in the application lifecycle, and is done in your Web application initializer (Java equivalent of the web.xml) described just before. Just provide the list of profiles to activate in the onStartup() method:

.. code-block:: java

    XmlWebApplicationContext appContext = new XmlWebApplicationContext();
    appContext.getEnvironment().setActiveProfiles("resthub-mongodb", "resthub-web-server");

In your tests, you should use the @ActiveProfiles annotation to activate the profiles you need:

.. code-block:: java

    @ActiveProfiles("resthub-jpa") // or @ActiveProfiles({"resthub-jpa","resthub-web-server"})
    public class SampleTest extends AbstractTransactionalTest {

    }

RESThub web tests comes with a helper to activate profiles too:

.. code-block:: java

    public class SampleControllerTest extends AbstractWebTest {

        public SampleControllerTest() {
            // Call AbstractWebTest(String profiles) constructor
            super("resthub-web-server,resthub-jpa");
        }
    }

RESThub built-in Spring profiles have the same name than their matching module:
    * resthub-jpa: enable JPA database support (resthub-jpa dependency needed)
    * resthub-mongodb: enable MongoDB support (resthub-mongodb dependency needed)
    * resthub-web-server: enable default web server configuration (resthub-web-server dependency needed)
    * resthub-client-logging: enable a webservice use to send logs from client to server (resthub-web-server dependency needed)

Spring based configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

By default RESThub webservices and unit tests scan and automatically include all resthubContext.xml (RESThub context files) and applicationContext.xml files (your application context files) available in your application classpath, including its dependencies.

Here is an example of a typical RESThub based src/main/resources/applicationContext.xml (this one uses JPA, you may adapt it if you use MongoDB):

.. code-block:: xml

    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:jpa="http://www.springframework.org/schema/data/jpa"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans 
                               http://www.springframework.org/schema/beans/spring-beans.xsd
                               http://www.springframework.org/schema/context 
                               http://www.springframework.org/schema/context/spring-context.xsd
                               http://www.springframework.org/schema/data/jpa 
                               http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">

        <context:component-scan base-package="org.mycompany.myproject" />
        <jpa:repositories base-package="org.mycompany.myproject.repository" />

    </beans>

logback.xml
~~~~~~~~~~~

You'll usually have a src/main/resources/logback.xml file in order to configure logging:

.. code-block:: xml

    <configuration> 
        <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
            <encoder>
                <pattern>%d{HH:mm:ss} [%thread] %-5level %logger{26} - %msg%n%rEx</pattern>
            </encoder>
        </appender>
        <root level="info"> 
            <appender-ref ref="CONSOLE"/> 
        </root> 
    </configuration>

Beans declaration and injection
-------------------------------

You should use JEE6 annotations to declare and inject your beans.

To declare a bean:

.. code-block:: java

   @Named("beanName")
   public class SampleClass {
   
   }

To inject a bean by type (default):

.. code-block:: java

   @Inject
   public void setSampleProperty(...) {
   
   }

Or to inject a bean by name (Allow more than one bean implementing the same interface):

.. code-block:: java

   @Inject @Named("beanName")
   public void setSampleProperty(...) {
   
   }

CRUD services
-------------

RESThub is designed to give you the choice between a 2 layers (Controller -> Repository) or a 3 layers (Controller -> Service -> Repository) software architecture. If you choose the 3 layers one, you can use the RESThub CRUD service when it is convenient:

.. code-block:: java

    @Named("sampleService")
    public class SampleServiceImpl extends CrudServiceImpl<Sample, Long, SampleRepository> implements SampleService {

        @Override @Inject
        public void setRepository(SampleRepository sampleRepository) {
            super.setRepository(sampleRepository);
        }
    }

Environment specific properties
-------------------------------

There are various ways to configure your environment specific properties in your application: the one described below is the most simple and flexible way we have found. 

Maven filtering (search and replace variables) is not recommended because it is done at compile time (not runtime) and makes usually your JAR/WAR specific to an environment. This feature can be useful when defining your target path (${project.build.directory}) in your src/test/applicationContext.xml for testing purpose.

Spring properties placeholders + @Value annotation is the best way to do that.

.. code-block:: xml

   <context:property-placeholder location="classpath*:mymodule.properties"
                                 ignore-resource-not-found="true"
                                 ignore-unresolvable="true" />

You should now be able to inject dynamic values in your code, where InMemoryRepository is the default:

.. code-block:: java

    @Configuration
    public class RequestConfiguration {

        @Value(value = "${repository:InMemoryRepository}")
        private String repository;
    }

JPA support
===========

JPA support is based on Spring Data JPA and includes by default the H2 in memory database. It includes the following dependencies:
    * Spring Data JPA (`reference manual <http://static.springsource.org/spring-data/data-jpa/docs/current/reference/html/>`_ and `Javadoc <http://static.springsource.org/spring-data/data-jpa/docs/current/api/>`_)
    * Hibernate `documentation <http://www.hibernate.org/docs.html>`_
    * `H2 embedded database <http://www.h2database.com/html/main.html>`_

Thanks to Spring Data, it is possible to create repositories (also sometimes named DAO) by writing only the interface.

Configuration
-------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-jpa</artifactId>
        <version>2.0.0</version>
    </dependency>

In order to import its `default configuration <https://github.com/resthub/resthub-spring-stack/blob/master/resthub-jpa/src/main/resources/resthubContext.xml>`_, your should activate the resthub-jpa Spring profile in your WebAppInitializer class:

.. code-block:: java

    XmlWebApplicationContext appContext = new XmlWebApplicationContext();
    appContext.getEnvironment().setActiveProfiles("resthub-jpa", "resthub-web-server");

Spring 3.1 allows to scan entities in different modules using the same PersitenceUnit, which is not possible with default JPA behaviour. You have to specify the packages where Spring should scan your entities by creating a database.properties file in your resources folder, with the following content:


.. code-block:: properties

   persistenceUnit.packagesToScan = com.myproject.model

Now, entities within the com.myproject.model packages will be scanned, no need for persistence.xml JPA file.


You also need to add an applicationContext.xml file in order to scan your repository package.

.. code-block:: xml

    <beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:jpa="http://www.springframework.org/schema/data/jpa"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
                               http://www.springframework.org/schema/beans/spring-beans.xsd
                               http://www.springframework.org/schema/data/jpa
                               http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">

        <jpa:repositories base-package="com.myproject.repository" />

    </beans>

You can customize the default configuration by adding a database.properties resource with one or more of the following keys customized with your values. You should include only the customized ones.

RESThub JPA default properties are:
    * dataSource.driverClassName = org.h2.Driver
    * dataSource.url = jdbc\:h2\:mem\:resthub;DB_CLOSE_DELAY=-1;MVCC=TRUE
    * dataSource.maxActive = 50
    * dataSource.maxWait = 1000
    * dataSource.poolPreparedStatements = true
    * dataSource.username = sa
    * dataSource.password = 
    * dataSource.validationQuery = SELECT 1

RESThub Hibernate default properties are:
    * hibernate.dialect = org.hibernate.dialect.H2Dialect
    * hibernate.show_sql = false
    * hibernate.format_sql = true
    * hibernate.hbm2ddl.auto = update
    * hibernate.cache.use_second_level_cache = true
    * hibernate.cache.provider_class = net.sf.ehcache.hibernate.SingletonEhCacheProvider
    * hibernate.id.new_generator_mappings = true
    * persistenceUnit.packagesToScan = 

If you need to do more advanced configuration, just override dataSource and entityManagerFactory beans in your applicationContext.xml.

Usage
-----

.. code-block:: java

    public interface TodoRepository extends JpaRepository<Todo, String> {

        List<Todo> findByContentLike(String content);
    }

Console
-------

H2 console allows you to provide a SQL requester for your embedded default H2 database. It is included by default in JPA archetypes.

In order to add it to your JPA based application, add these lines to your WebAppInitializer class: 

.. code-block:: java

    public void onStartup(ServletContext servletContext) throws ServletException {
        ...
        ServletRegistration.Dynamic h2Servlet = servletContext.addServlet("h2console", WebServlet.class);
        h2Servlet.setLoadOnStartup(2);
        h2Servlet.addMapping("/console/database/*");
    }

When running the webapp, the database console will be available at http://localhost:8080/console/database/ URL with following parameters:
    * JDBC URL: jdbc\:h2\:mem\:resthub
    * Username: sa
    * Password:

MongoDB support
===============

MongoDB support is based on Spring Data MongoDB (`reference manual <http://static.springsource.org/spring-data/data-mongodb/docs/current/reference/html/>`_ and `Javadoc <http://static.springsource.org/spring-data/data-mongodb/docs/current/api/>`_).

Configuration
-------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-mongodb</artifactId>
        <version>2.0.0</version>
    </dependency>

In order to import the `default configuration <https://github.com/resthub/resthub-spring-stack/blob/master/resthub-mongodb/src/main/resources/resthubContext.xml>`_, your should activate the resthub-mongodb Spring profile in your WebAppInitializer class:

.. code-block:: java

    XmlWebApplicationContext appContext = new XmlWebApplicationContext();
    appContext.getEnvironment().setActiveProfiles("resthub-mongodb", "resthub-web-server");

You also need to add an applicationContext.xml file in order to scan your repository package.

.. code-block:: xml

    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:mongo="http://www.springframework.org/schema/data/mongo"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
                               http://www.springframework.org/schema/beans/spring-beans.xsd
                               http://www.springframework.org/schema/data/mongo
                               http://www.springframework.org/schema/data/mongo/spring-mongo.xsd">

        <mongo:repositories base-package="com.myproject.repository" />

    </beans>

You can customize them by adding a database.properties resource with one or more following keys customized with your values. You should include only the customized ones.

RESThub MongoDB default properties are:
    * database.dbname = resthub
    * database.host = localhost
    * database.port = 27017
    * database.username =
    * database.password =
    * database.connectionsPerHost = 10
    * database.threadsAllowedToBlockForConnectionMultiplier = 5
    * database.connectTimeout = 0
    * database.maxWaitTime = 120000
    * database.autoConnectRetry = false
    * database.socketKeepAlive = false
    * database.socketTimeout = 0
    * database.slaveOk = false
    * database.writeNumber = 0
    * database.writeTimeout = 0
    * database.writeFsync = false

Usage
-----

.. code-block:: java

    public interface TodoRepository extends MongoRepository<Todo, String> {

        List<Todo> findByContentLike(String content);
    }

Web common
==========

RESThub Web Common comes with built-in XML and JSON support for serialization based on `Jackson 2.1 <http://wiki.fasterxml.com/JacksonHome>`_. RESThub uses `Jackson 2.1 XML capabilities <https://github.com/FasterXML/jackson-dataformat-xml>`_ instead of JAXB since it is more flexible. For example, you don't need to add classes to a context. Please read `Jackson annotation guide <http://wiki.fasterxml.com/JacksonAnnotations>`_ for details about configuration capabilities.

Maven dependency
----------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-web-common</artifactId>
        <version>2.0.0</version>
    </dependency>

Usage
-----

.. code-block:: java

    // JSON
    SampleResource r = (SampleResource) JsonHelper.deserialize(json, SampleResource.class);
    JsonHelper.deserialize("{\"id\": 123, \"name\": \"Albert\", \"description\": \"desc\"}", SampleResource.class);

    // XML
    SampleResource r = (SampleResource) XmlHelper.deserialize(xml, SampleResource.class);
    XmlHelper.deserialize("<sampleResource><description>desc</description><id>123</id><name>Albert</name></sampleResource>", SampleResource.class);

Web server
==========

RESThub Web Server module is designed for REST webservices development. Both JSON (default) and XML serialization are supported out of the box.

.. warning::

    Currently Jackson XML dataformat does not support non wrapped List serialization. As a consequence, the findAll (GET /) method is not supported for XML content-type yet. `You can follow the related Jackson issue on GitHub <https://github.com/FasterXML/jackson-dataformat-xml/issues/38>`_.

It provides some abstract REST controller classes, and includes the following dependencies:
    * Spring MVC 3.1 (`reference manual <http://static.springsource.org/spring/docs/3.1.x/spring-framework-reference/html/mvc.html>`_)
    * Jackson 2.1 (`documentation <http://wiki.fasterxml.com/JacksonDocumentation>`_)

RESThub exception resolver allow to map common exceptions (Spring, JPA) to the right HTTP status codes:
    * IllegalArgumentException -> 400
    * ValidationException -> 400
    * NotFoundException, EntityNotFoundException and ObjectNotFoundException -> 404
    * NotImplementedException -> 501
    * EntityExistsException -> 409
    * Any uncatched exception -> 500

Configuration
-------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-web-server</artifactId>
        <version>2.0.0</version>
    </dependency>

In order to import the `default configuration <https://github.com/resthub/resthub-spring-stack/blob/master/resthub-web/resthub-web-server/src/main/resources/resthubContext.xml>`_, your should activate the resthub-web-server Spring profile in your WebAppInitializer class:

.. code-block:: java

    XmlWebApplicationContext appContext = new XmlWebApplicationContext();
    appContext.getEnvironment().setActiveProfiles("resthub-web-server", "resthub-mongodb");

Usage
-----

RESThub comes with a REST controller that allows you to create a CRUD webservice in a few lines. You have the choice to use a 2 layers (Controller -> Repository) or 3 layers (Controller -> Service -> Repository) software design.

You can  find more details about these generic webservices, including their REST API description, on RESThub `Javadoc <http://resthub.org/javadoc/2.0>`_.

**2 layers software design**

.. code-block:: java

    @Controller @RequestMapping("/repository-based")
    public class SampleRestController extends RepositoryBasedRestController<Sample, Long, WebSampleResourceRepository> {

        @Override @Inject
        public void setRepository(WebSampleResourceRepository repository) {
            this.repository = repository;
        }
    }

**3 layers software design**

.. code-block:: java

    @Controller @RequestMapping("/service-based")
    public class SampleRestController extends ServiceBasedRestController<Sample, Long, SampleService> {

        @Override @Inject
        public void setService(SampleService service) {
            this.service = service;
        }
    }

    @Named("sampleService")
    public class SampleServiceImpl extends CrudServiceImpl<Sample, Long, SampleRepository> implements SampleService {

        @Override @Inject
        public void setRepository(SampleRepository SampleRepository) {
            super.setRepository(SampleRepository);
        }
    }

By default, generic controller use the database identifier (table primary key for JPA on MongoDB ID) in URLs to identify a resource. You can change this behaviour by overriding controller implementations to use the field you want. For example, this is common to use a human readable identifier called reference or slug to identify a resource. You can do that with generic repositories only by overriding findById() controller method:

.. code-block:: java

    @Controller @RequestMapping("/sample")
    public class SluggableSampleController extends RepositoryBasedRestController<Sample, String, SampleRepository> {

        @Override @Inject
        public void setRepository(SampleRepository repository) {
            this.repository = repository;
        }

        @Override
        public Sample findById(@PathVariable String id) {
            Sample sample = this.repository.findBySlug(id);
            if (sample == null) {
                throw new NotFoundException();
            }
            return sample;
        }   
    }

With default behaviour we have URL like GET /sample/32.
With sluggable behaviour we have URL lke GET /sample/niceref.

.. warning::

    Be aware that when you override a Spring MVC controller method, your new method automatically reuse method level annotations from parent classes, but not parameter level annotations. That's why you need to specify parameters annotations again in order to make it work, like in the previous code sample.

Model and DTOs with ModelMapper
-------------------------------

The previous ``SluggableSampleController`` example shows one thing: when your application starts to grow, you usually want to address some specific needs:

* tailoring data for your client (security, performance...)
* changing your application behaviour without changing service contracts with your clients

For that, you often need to decorrelate serialized objects (`DTOs <http://en.wikipedia.org/wiki/Data_transfer_object>`_) from your model.

RESThub includes `ModelMapper <http://modelmapper.org/>`_ in its resthub-common module.

.. code-block:: java

    ModelMapper modelMapper = new ModelMapper();
    UserDTO userDTO = modelMapper.map(user, UserDTO.class);

Modelmapper has sensible defaults and can often map objects without additional configuration. For specific needs, you can use `property maps <http://modelmapper.org/user-manual/property-mapping/>`_.

Client logging
--------------

In order to make JS client application debugging easier, RESThub provides a webservice used to send client logs to the server. In order to activate it, you should enable the **resthub-client-logging** Spring profile.

POST api/log webservice expect this kind of body:

.. code-block:: javascript

    {"level":"warn","message":"log message","time":"2012-11-13T08:18:52.972Z"}

POST api/logs webservice expect this kind of body:

.. code-block:: javascript

    [{"level":"warn","message":"log message 1","time":"2012-11-13T08:18:53.342Z"},
    {"level":"info","message":"log message 1","time":"2012-11-13T08:18:52.972Z"}]

Web client
==========

RESThub Web client module aims to give you an easy way to request other REST webservices. It is based on AsyncHttpClient and provides a `client API wrapper <http://resthub.org/javadoc/2.0/index.html?org/resthub/web/Client.html>`_ and OAuth2 support.

In order to limit conflicts it has no dependency on Spring, but only on:
    * AsyncHttpClient `documentation <https://github.com/sonatype/async-http-client>`_ and `Javadoc <http://sonatype.github.com/async-http-client/apidocs/reference/packages.html>`_
    * Jackson 2.1 (`documentation <http://wiki.fasterxml.com/JacksonDocumentation>`_)

Configuration
-------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-web-client</artifactId>
        <version>2.0.0</version>
    </dependency>

Usage
-----

You can use resthub web client in a synchronous or asynchronous way. The synchronous API is easy to use, but blocks the current Thread until the remote server sends the full Response.

.. code-block:: java

    // One-liner version
    Sample s = httpClient.url("http//...").jsonPost(new Sample("toto")).resource(Sample.class);

    // List<T> and Page<T> use TypeReference due to Java type erasure issue
    List<Sample> p = httpClient.url("http//...").jsonGet().resource(new TypeReference<List<Sample>>() {});
    Page<Sample> p = httpClient.url("http//...").jsonGet().resource(new TypeReference<Page<Sample>>() {});

Asynchronous API is quite the same, every HTTP request returns a `Future <http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Future.html>`_ <Response> object. Just call get() on this object in order to make the call synchronous.
The ``Future.get()`` method can throw Exceptions, so the method call should be surrounded by a try/catch or let the exceptions bubble up.

.. code-block:: java

    // 4 lines example
    Client httpClient = new Client();
    Future<Response> fr = httpClient.url("http//...").asyncJsonPost(new Sample("toto"));
    // do some computation while we're waiting for the response...

    // calling .get() makes the code synchronous again!
    Sample s = httpClient.url("http//...").asyncJsonPost(new Sample("toto")).get().resource(Sample.class);

Because the remote web server sometimes responds 4xx (client error) and 5xx (server error) HTTP status codes, RESThub HTTP Client wraps those error statuses and throws `specific runtime exceptions <https://github.com/resthub/resthub-spring-stack/tree/master/resthub-web/resthub-web-common/src/main/java/org/resthub/web/exception>`_. 

OAuth 2.0 integration
---------------------

Here is an example of a simple OAuth2 support

.. code-block:: java

    String username = "test";
    String password = "t&5t";
    String clientId = "app1";
    String clientSecret = "";
    String accessTokenUrl = "http://.../oauth/token";

    Client httpClient = new Client().setOAuth2(username, password, accessTokenUrl, clientId, clientSecret);
    String result = httpClient.url("http://.../api/sample").get().getBody();

You can also use a specific OAuth2 configuration. For example, you can override the HTTP Header
used to send the OAuth token.

.. code-block:: java

    OAuth2Config.Builder builder = new OAuth2Config.Builder();
    builder.setAccessTokenEndpoint("http://.../oauth/token")
           .setUsername("test").setPassword("t&5t")
           .setClientId("app1").setClientSecret("")
           .setOAuth2Scheme("OAuth"); // override default OAuth HTTP Header name

    Client httpClient = new Client().setOAuth2Builder(builder);
    String result = httpClient.url("http://.../api/sample").get().getBody();

Validation API
==============

In a RIA, form validation could be a heavy process because you have to implement validation on both client and server side
of your application.

To be able to build, on client side, a validation behaviour based on server side constraints definition, **Resthub provides
an API to export, for a given model class, the complete list of its constraints definitions**.

Resthub Spring Stack integrates the `JSR303 specification <http://beanvalidation.org/1.0/spec/>`_ (BeanValidation) 
and its reference implementation: `Hibernate Validator <http://docs.jboss.org/hibernate/validator/4.3/reference/en-US/html_single/>`_.

These validations cosntraints are, in fact, annotation hold by a Java Bean Model. e.g :

.. code-block:: java

    @NotNull
    public String getLogin() {
        return this.login;
    }


All these constraints and their parameters are exported by Resthub Validation API.

Resthub provides, in client side, a full support of this API to implement client side validation natively 
(see `Backbone Stack documentation <./backbone-stack.html#resthub-validation-features>`_).
    

Usage and configuration
-----------------------

Validation API is not activated by default and should be first configured.

Activation
~~~~~~~~~~

To activate, edit your WebAppInitializer and add ``resthub-validation`` as a spring active profile :

.. code-block:: java

    public class WebAppInitializer implements WebApplicationInitializer {

        @Override
        public void onStartup(ServletContext servletContext) throws ServletException {
            XmlWebApplicationContext appContext = new XmlWebApplicationContext();
            appContext.getEnvironment().setActiveProfiles("resthub-jpa", "resthub-web-server", "resthub-validation");
            
            ...
        }
    }


API access and parameters
~~~~~~~~~~~~~~~~~~~~~~~~~

Validation REST API can then be reached through ``/api/validation`` but takes some parameters : 

1. **className**

   Mandatory path parameter containing the complete className of the Java Bean to export (i.e. package + className - e.g. 
   ``org.resthub.validation.model.User``). This parameter must be provided. If not or if an invalid className is provided,
   a 404 NotFound response is returned.
   
   For example, you can reach validation API at: http://localhost:8181/api/validation/org.resthub.validation.model.User

2. **locale**

   As an optional request parameter, the API takes the locale string indicating your internationalization preferences. You can
   then provide a valid i18n locale string to choose the disired message locale.
   
   e.g : http://localhost:8181/api/validation/org.resthub.validation.model.User?locale=en-us
   
   Available locales are those supported by Hibernate Validator or provided by your custom properties files. If no locale
   parameter is provided or if the locale parameter is invalid, the default server locale is used.
   
   If some of your validation constraints (e.g. custom ones) doesn't have any default error message, only the key is exported
   by the API (e.g. ``org.resthub.validator.constraints.TelephoneNumber.message``).


Response format
~~~~~~~~~~~~~~~

The response format could be XML or JSON and contains the following:

- The complete model className
- A list of constraints (JSON object or dedicated XML element) containing all Java Bean property description.
- Each property contains a list (JSON array or multiple XML element) of its constraints.
- Each constraint contains different properties:
 
    + *type*: contains the constraint type (e.g. *NotNull*, *Size*, *Email*).
    + *message*: contains the constraint error message.
    + any other(s) property(ies) depending on the constraint type and its custom parameters (e.g. the *Size*
      constraint contains two additionals properties *min* and *max*). To get the complete list of JSR303 parameters,
      see `specification <http://beanvalidation.org/1.0/spec/#d0e5601>`_, for hibernate validator, see
      `documentation <http://docs.jboss.org/hibernate/validator/5.0/reference/en-US/html_single/#validator-defineconstraints-hv-constraints>`_


**JSON sample:**

.. code-block:: javascript

    {
        "model": "org.resthub.validation.model.User",
        "constraints": {
            "lastName": [{
                "type": "NotBlank",
                "message": "may not be empty"
            }],
            "email": [{
                "type": "NotNull",
                "message": "may not be null"
            }, {
                "type": "Email",
                "message": "not a well-formed email address",
                "flags": [],
                "regexp": ".*"
            }],
            "login": [{
                "type": "NotNull",
                "message": "may not be null"
            }, {
                "type": "Length",
                "message": "length must be between 8 and 2147483647",
                "min": 8,
                "max": 2147483647
            }],
            "firstName": [{
                "type": "NotBlank",
                "message": "may not be empty"
            }]
        }
    }

    
**XML sample:**    

.. code-block:: xml

    <ModelConstraint>
        <model>org.resthub.validation.model.User</model>
        <constraints>
            <lastName>
                <type>NotBlank</type>
                <message>may not be empty</message>
            </lastName>
            <email>
                <type>NotNull</type>
                <message>may not be null</message>
            </email>
            <email>
                <type>Email</type>
                <message>not a well-formed email address</message>
                <regexp>.*</regexp>
            </email>
            <login>
                <type>NotNull</type>
                <message>may not be null</message>
            </login>
            <login>
                <type>Length</type>
                <message>length must be between 8 and 2147483647</message>
                <min>8</min>
                <max>2147483647</max>
            </login>
            <firstName>
                <type>NotBlank</type>
                <message>may not be empty</message>
            </firstName>
        </constraints>
    </ModelConstraint>


Supported annotations
---------------------

Resthub Validation API is based on `JSR303 specification <http://beanvalidation.org/1.0/spec/>`_ (BeanValidation) Validation constraints. **Any standard BeanValidation
Constraint is supported** (and exported) by this API.

As `Hibernate Validator <http://docs.jboss.org/hibernate/validator/4.3/reference/en-US/html_single/>`_ is used as BeanValidation implementation, Resthub Validation also exports and supports specific
Hibernate Validators constraints which format are JSR303 compliant are also supported. More globally, **any extension of JSR303 specification
would be supported** if the standard BeanValidation constraint definition API is used.

Testing
=======

The following test stack is included in the RESThub test module:
    * Test framework with `TestNG <http://testng.org/doc/documentation-main.html>`_. If you use Eclipse, don't forget to install the `TestNG plugin <http://testng.org/doc/eclipse.html>`_.
    * Assertion with `Fest Assert 2 <https://github.com/alexruiz/fest-assert-2.x/wiki>`_
    * Mock with `Mockito <http://code.google.com/p/mockito/>`_

RESThub also provides generic classes in order to make testing easier.
    * AbstractTest: base class for your non transactional Spring aware unit tests
    * AbstractTransactionalTest: base class for your transactional unit tests, preconfigured with Spring test framework
    * AbstractWebTest: base class for your unit tests that need to run an embedded servlet container.

Maven dependency
----------------

In order to use it in your project, add the following snippet to your pom.xml:

.. code-block:: xml

    <dependency>
        <groupId>org.resthub</groupId>
        <artifactId>resthub-test</artifactId>
        <version>2.0.0</version>
        <scope>test</scope>
    </dependency>

Data provisioning and cleanup
------------------------------

It is recommended to initialize and cleanup test data shared by your tests using methods annotated with TestNG's @BeforeMethod and @AfterMethod and using your repository or service classes.

.. warning::

    With JPA the default deleteAll() method does not manage cascade delete, so for your data cleanup you should use the following code in order to get your entities removed with cascade delete support:

.. code-block:: java

    Iterable<MyEntity> list = repository.findAll();
    for (MyEntity entity : list) {
        repository.delete(entity);
    }

Usage
-----

AbstractTest or AbstractTransactionalTest

.. code-block:: java

    @ActiveProfiles("resthub-jpa")
    public class SampleRepositoryTest extends AbstractTransactionalTest {

        private SampleRepository repository;

        @Inject
        public void setRepository(SampleRepository repository) {
            this.repository = repository;
        }

        @AfterMethod
        public void tearDown() {
            for (SampleRepository resource : repository.findAll()) {
                repository.delete(resource);
            }
        }

        @Test
        public void testSave() {
            Sample entity = repository.save(new Sample());
            Assertions.assertThat(repository.exists(entity.getId())).isTrue();
        }
    }

AbstractWebTest

.. code-block:: java

    public class SampleRestControllerTest extends AbstractWebTest {

        public SampleRestControllerTest() {
            // Call AbstractWebTest(String profiles) constructor
            super("resthub-web-server,resthub-jpa");
        }   

        // Cleanup after each test
        @AfterMethod
        public void tearDown() {
            this.request("sample").delete();
        }

        @Test
        public void testCreateResource() {
            Sample r = this.request("sample").jsonPost(new Sample("toto")).resource(Sample.class);
            Assertions.assertThat(r).isNotNull();
            Assertions.assertThat(r.getName()).isEqualTo("toto");
        }
    }

A sample assertion

.. code-block:: java

    Assertions.assertThat(result).contains("Albert");

Integration test
----------------

A good practice is to separate unit tests from integration tests. The unit tests are designed to test only a specific layer of your application, ignoring other layers by mocking them (see `Mockito <http://code.google.com/p/mockito/>`_). The integration tests are designed to test all the layers of your application in real condition with complex scenarii.

Maven allow us to do this separation by introducing the integration-test phase.
To use this phase, add the following snippet to your pom.xml:

.. code-block:: xml

    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-failsafe-plugin</artifactId>
        <version>2.12.4</version>
        <executions>
            <execution>
                <goals>
                    <goal>integration-test</goal>
                    <goal>verify</goal>
                </goals>
            </execution>
        </executions>
    </plugin>

With this plugin, Maven will seek Java files matching "\*IT.java" in test directory. And run them during the integration-test phase.

You have 2 way (mutually exclusives) for writing you integration tests. Both approaches have pros and cons, so choose the one that fit the best to your needs. In both case the test you write is not in a Spring context (Spring is runned in the embeded Jety server), so you should write your test using mainly RESThub web client (that does not ue Spring at all) and assertions.

Option 1 - Use embedded Jetty
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Extend your test with AbstractWebTest (as the exemple above). This class will take care to run jetty.
Jetty will run once (by default) for all tests and will stop at the end of the JVM.

Option 2 - Use Maven Jetty plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the following snippet to the jetty configuration in your pom.xml:

.. code-block:: xml

    <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <executions>
            <execution>
                <id>start-jetty</id>
                <phase>pre-integration-test</phase>
                <goals>
                    <goal>run</goal>
                </goals>
                <configuration>
                    <scanIntervalSeconds>0</scanIntervalSeconds>
                    <daemon>true</daemon>
                </configuration>
            </execution>
            <execution>
                <id>stop-jetty</id>
                <phase>post-integration-test</phase>
                <goals>
                    <goal>stop</goal>
                </goals>
            </execution>
        </executions>
    </plugin>

Now if you build the project, maven will run unit tests, then package the application, then run jetty, then run integration test en finaly stop jetty. You can also run your application with jetty:run and run separately and manualy you integration test in your IDE. It's usefull to build quickly all your integration tests.

Spring MVC Router
=================

Spring MVC Router adds route mapping capacity to any "Spring MVC based" webapp à la PlayFramework or Ruby on Rails. For more details, check its `detailed documentation <http://resthub.github.com/springmvc-router/>`_.

AMQP/Hessian based RPC
======================

Spring AMQP Hessian is a high performance and easy to monitore RPC mechanism based on RabbitMQ client and Hessian. For more details, check its `detailed documentation <https://github.com/resthub/spring-amqp-hessian>`_.
