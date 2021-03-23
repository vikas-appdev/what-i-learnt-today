Various properties can be specified inside `application.properties`. Some of the common properties that are frequently being used during development are listed below.

`logging.level.org.springframework = info`

Above pair enables the info level logging inside console for the springframework package.

`server.port=7373`

Server.port helps us to change the default configured port of embedded server.

`spring.datasource.url=jdbc:mysql://localhost:3306/databaseName?createDatabaseIfNotExist=true`
 
 Above pair helps us to configure the database for the boot application. Here I am using MySQL database on 3306 port with `createDatabaseIfNotExist=true` query string to create database automatically if database is already not present inside mysql.
 
 `spring.jpa.hibernate.ddl-auto=update`
 
 Above key can be used with `update` and `create` value. It helps us in auto creation of tables inside database. Creates will deleted all the table and recreate all record when application re-start. Update will look for any changes and implement those changes only.
 
 `spring.datasource.username=root`
 
 Using above pair we can configure the username for the database
 
 `spring.datasource.password=sql1`
 
 With the help of above pair we can simply pass the database password to the spring boot application for the various operations.
 
 `hibernate.dialect=org.hibernate.dialect.MySQL8Dialect`
 
 Some times we need to configure the Dialect to work with Hibernate And JPA in that case we can use above mentioned key value pair or we can simply switch the dialect.
 
 `dataSource.driverClassName=com.mysql.jdbc.Driver`
 
 Optinally we can configure the driver class for the jdbc.
 
 