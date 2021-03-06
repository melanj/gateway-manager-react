# Gateway Manager UI and backend
This is a sample application based on Spring Boot 2.6 backend and React 17 front end. It is the React version of my sample application on https://github.com/melanj/gateway-manager/

## Prerequisites

- [x] JDK 8 or later 
- [x] Apache Maven 3.5 or later 
- [x] Node.js (v16.14.2 or compatible)
- [x] MySQL (v5.7 or compatible)
- [x] git client


## how to run this application

1. clone this repository using git command or alternatively , you may be able to download ZIP archive and extract it

```bash
git clone https://github.com/melanj/gateway-manager.git
```

2. Create a database named 'app' (or alternative name) and restore the database.sql file in the project

3. Update src/main/resources/application.yml file according to MySQL server hostname, database and user credentials

e.g.
```yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/app?serverTimezone=UTC
    username: root
    password: root
  dbcp2:
    max-wait-millis: 30000
    validation-query: "SELECT 1"
    validation-query-timeout: 30
  jpa:
    hibernate:
      ddl-auto: update
    open-in-view: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL5InnoDBDialect
        jdbc:
          lob:
            non_contextual_creation: true
        id:
          new_generator_mappings: true
springdoc:
  pathsToMatch: /api/**
```


4. Use "mvn clean install" to build the package, maven invokes 'npm run build' command package react application into Jar file alone with spring boot application.

e.g
```bash
$ mvn clean install  -DskipTests
[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------< org.example:gateway-admin-app-react >-----------------
[INFO] Building gateway-admin-app-react 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:3.1.0:clean (default-clean) @ gateway-admin-app-react ---
[INFO] 
[INFO] --- exec-maven-plugin:1.2.1:exec (build-react-app) @ gateway-admin-app-react ---

> gateway-manager-fe@0.1.0 build
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  43.73 kB  public/static/js/main.68a43468.js
  1.79 kB   public/static/js/787.3a65c882.chunk.js
  541 B     public/static/css/main.073c9b0a.css

The project was built assuming it is hosted at /.
You can control this with the homepage field in your package.json.

The ../src/main/resources/public folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s ../src/main/resources/public

Find out more about deployment here:

  https://cra.link/deployment

[INFO] 
[INFO] --- jacoco-maven-plugin:0.8.7:prepare-agent (default) @ gateway-admin-app-react ---
[INFO] argLine set to -javaagent:/home/melan/.m2/repository/org/jacoco/org.jacoco.agent/0.8.7/org.jacoco.agent-0.8.7-runtime.jar=destfile=/home/melan/wks/gateway-manager-react/target/jacoco.exec
[INFO] 
[INFO] --- maven-resources-plugin:3.2.0:resources (default-resources) @ gateway-admin-app-react ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] Copying 1 resource
[INFO] Copying 15 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ gateway-admin-app-react ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 19 source files to /home/melan/wks/gateway-manager-react/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:3.2.0:testResources (default-testResources) @ gateway-admin-app-react ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] skip non existing resourceDirectory /home/melan/wks/gateway-manager-react/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ gateway-admin-app-react ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 3 source files to /home/melan/wks/gateway-manager-react/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.22.2:test (default-test) @ gateway-admin-app-react ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- jacoco-maven-plugin:0.8.7:report (report) @ gateway-admin-app-react ---
[INFO] Skipping JaCoCo execution due to missing execution data file.
[INFO] 
[INFO] --- maven-jar-plugin:3.2.2:jar (default-jar) @ gateway-admin-app-react ---
[INFO] Building jar: /home/melan/wks/gateway-manager-react/target/gateway-admin-app-react-1.0.0-SNAPSHOT.jar
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.6.4:repackage (repackage) @ gateway-admin-app-react ---
[INFO] Replacing main artifact with repackaged archive
[INFO] 
[INFO] --- maven-install-plugin:2.5.2:install (default-install) @ gateway-admin-app-react ---
[INFO] Installing /home/melan/wks/gateway-manager-react/target/gateway-admin-app-react-1.0.0-SNAPSHOT.jar to /home/melan/.m2/repository/org/example/gateway-admin-app-react/1.0.0-SNAPSHOT/gateway-admin-app-react-1.0.0-SNAPSHOT.jar
[INFO] Installing /home/melan/wks/gateway-manager-react/pom.xml to /home/melan/.m2/repository/org/example/gateway-admin-app-react/1.0.0-SNAPSHOT/gateway-admin-app-react-1.0.0-SNAPSHOT.pom
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  14.478 s
[INFO] Finished at: 2022-03-19T20:01:22+05:30
[INFO] ------------------------------------------------------------------------

```

5. use "java -jar target/gateway-admin-app-1.0.0-SNAPSHOT.jar" run the application and application can be accessible via a browser using http://localhost:8080/ and swagger API specifications http://localhost:8080/swagger-ui.html 

application logs can be seen in console
```bash
$ java -jar target/gateway-admin-app-1.0.0-SNAPSHOT.jar 

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.4.4)

2021-04-08 17:41:25.266  INFO 14310 --- [           main] org.example.app.AppApplication           : Starting AppApplication v1.0.0-SNAPSHOT using Java 11.0.10 on sequoia with PID 14310 (/home/melan/wks/app/target/gateway-admin-app-1.0.0-SNAPSHOT.jar started by melan in /home/melan/wks/app)
2021-04-08 17:41:25.273  INFO 14310 --- [           main] org.example.app.AppApplication           : No active profile set, falling back to default profiles: default
2021-04-08 17:41:26.270  INFO 14310 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2021-04-08 17:41:26.352  INFO 14310 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 69 ms. Found 2 JPA repository interfaces.
2021-04-08 17:41:27.499  INFO 14310 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2021-04-08 17:41:27.523  INFO 14310 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2021-04-08 17:41:27.524  INFO 14310 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.44]
2021-04-08 17:41:27.622  INFO 14310 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2021-04-08 17:41:27.623  INFO 14310 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 2249 ms
2021-04-08 17:41:27.928  INFO 14310 --- [           main] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2021-04-08 17:41:28.028  INFO 14310 --- [           main] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 5.4.29.Final
2021-04-08 17:41:28.232  INFO 14310 --- [           main] o.hibernate.annotations.common.Version   : HCANN000001: Hibernate Commons Annotations {5.1.2.Final}
2021-04-08 17:41:28.360  INFO 14310 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2021-04-08 17:41:28.828  INFO 14310 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2021-04-08 17:41:28.856  INFO 14310 --- [           main] org.hibernate.dialect.Dialect            : HHH000400: Using dialect: org.hibernate.dialect.MySQL5InnoDBDialect
2021-04-08 17:41:29.777  INFO 14310 --- [           main] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2021-04-08 17:41:29.787  INFO 14310 --- [           main] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2021-04-08 17:41:30.685  INFO 14310 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2021-04-08 17:41:30.940  INFO 14310 --- [           main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page: class path resource [public/index.html]
2021-04-08 17:41:31.966  INFO 14310 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2021-04-08 17:41:31.979  INFO 14310 --- [           main] org.example.app.AppApplication           : Started AppApplication in 7.562 seconds (JVM running for 8.278)
2021-04-08 17:42:08.778  INFO 14310 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2021-04-08 17:42:08.778  INFO 14310 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2021-04-08 17:42:08.779  INFO 14310 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 1 ms
2021-04-08 17:58:29.445  INFO 14310 --- [io-8080-exec-10] o.springdoc.api.AbstractOpenApiResource  : Init duration for springdoc-openapi is: 680 ms
```

## how to see coverage

Tests can be run using following maven command and test reports are available at 'target/site/jacoco/index.html'

```bash
mvn clean test jacoco:report
```
