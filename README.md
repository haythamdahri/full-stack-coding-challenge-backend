# Shop Server Side Application

Shop is a full-stack application released with [Spring Boot Framework](https://spring.io/projects/spring-boot) in the back-end server side and [Angular Framework](https://angular.io/) in the web front-end client side.
The objective behind this project is creating a secured rest api that will be consumed by a [front-end](https://github.com/haythamdahri/full-stack-coding-challenge-front-end) application.
In this project, we are using JWT authentication which is the alternative solution of Cookies and session based authentication.

## Getting Started
To use the project, we need to establish the connection with a local or a remote database where the data will be stored for later use by editing **application.yml** or **application.properties** file depending on developer flexibility.

## Prerequisites
Before starting, we need to make sure that all prerequisites are installed.
 - [Maven](https://maven.apache.org/) - Dependency Management
 - [MySQL server](https://dev.mysql.com/downloads/mysql/) - Database server for data serving (MySQL or any other SQL server)

***Note:*** *Supported NoSQL databases are able to be used but there are many required changes in the architecture. Therefore, it is preferred to stay on a SQL system*

 - Install all dependencies that are written in [pom.xml](https://github.com/haythamdahri/full-stack-coding-challenge-back-end/blob/master/pom.xml) by updating project or force dependencies installation.

## Setting up back-end server

1. First of all, we need to create a new MySQL database manually by accessing mysql command line interface **(CLI)**.
```mysql
mysql> create database fullstack_coding_challenge;
mysql> use fullstack_coding_challenge;
```
2. Add database configuration **(url, username and password)**, hibernate logging, maximum file upload size, maximum request size, rest api base path and jwt secret in **application.properties** or **application.yml**
```yaml
## Author: HAYTHAM DAHRI

## Spring DATASOURCE (DataSourceAutoConfiguration & DataSourceProperties)
## Set database access username and password
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/fullstack_coding_challenge?useSSL=false
    username: haytham
    password: toortoor

  ## Hibernate Properties
  # The SQL dialect makes Hibernate generate better SQL for the chosen database ddl-auto = update
  ## Hibernate Logging
  jpa:
    hibernate:
      ddl-auto: update

  ## MULTIPART (MultipartProperties)
  # Enable multipart uploads=true
  servlet:
    multipart:
      enabled: true
      # Threshold after which files are written to disk.
      file-size-threshold: 2KB
      # Max file size.
      max-file-size: 200MB
      # Max Request Size=215MB
      max-request-size: 215MB

  ## Spring security configuration
  security:
    user:
      name: haytham
      password: toortoor
  data:

    ## Rest api configuration
    rest:
      base-path: /rest

## jwt security configuration
jwt:
  secret: topsecret
```
**In our case, we are using the embedded tomcat server. Therefore, there is no need to install any application or web server to run the application.**

3. At this point, everything is **established successfully**, it remains only clean and install the project to run it using **mvn** command.
Please note that the application is configured to generate database automatically **(```ddl-auto: update```)**
```bash
mvn clean install
mvn spring-boot:run
```
Otherwise, you can use your Integrated development environment **(IDE)** to start the project such as **Intellij** or **Eclipse**. 

After running up the server, the api will be available in: [http://localhost:8080](http://localhost:8080). The current configuration allows any client application to access to the resources even if the hosting domain is different than the server one.

## Running the tests
Some Application tests are already written in advance. So that, you can run the tests directly either by using your **IDE** or by running the following maven test command to run all unit testing classes.
```bash
mvn test
```
The aim behind written tests is to check the **rest api** end points **security** and to compare **returned results** with **the expected ones**. 

## Application supported End points and methods
Mainly, many end points are auto-generated by **[SPRING DATA REST](https://spring.io/projects/spring-data-rest)** in addition to the created ones.

The implemented end points are specified and required to be consumed by the client [front-end](https://github.com/haythamdahri/full-stack-coding-challenge-front-end) application.
 - **/authenticate** Authentication end point -- Login ***(POST)***
 - **/rest/v1/** Home end point ***(GET)***
 - **/rest/v1/save-user** Add or update the sent user from the client (Signup) end point ***(POST)***
 - **/rest/v1/near-by-shops** Retrieve the authenticated user near shops by distance end point ***(GET)***
 - **/rest/v1/user-preferred-shops** Retrieve authenticated user preferred shops end point ***(GET)***
 - **/rest/v1/shop/image/{id}** Retrieve a shop image (IMAGE JPEG as response) end point ***(GET - POST)***
 - **/rest/v1/add-user-shop/{id}** Add a shop to the authenticated user preferred shops end point ***(POST)***
 - **/rest/v1/dislike-shop/{id}** Dislike a shop by the authenticated user end point ***(POST)***
 - **/rest/v1/remove-preferred-shop/{id}** Remove a shop from the authenticated user preferred shops end point ***(POST)***
 - **/rest/users** AUTO GENERATED REST API end point ***(GET - POST - PUT - PATCH)***
 - **/rest/roles** AUTO GENERATED REST API end point ***(GET - POST - PUT - PATCH)***
 - **/rest/shops** AUTO GENERATED REST API end point ***(GET - POST - PUT - PATCH)***
 - **/rest/dislikedShops** AUTO GENERATED REST API end point ***(GET - POST - PUT - PATCH)***

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## Author
 - HAYTHAM DAHRI

**[Linkedin](https://www.linkedin.com/in/haytham-dahri/)** - **[Github](https://github.com/haythamdahri)** - **[Facebook](https://www.facebook.com/Haytham.dahri)**

***
Thank you for taking time to read the documentation. :+1: