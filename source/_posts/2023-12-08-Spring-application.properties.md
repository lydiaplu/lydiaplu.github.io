---
title: Spring application.properties
date: 2023-12-08 19:05:30
toc: true  
categories:  
- Spring Boot 3

---

# Spring application.properties

In a Spring Boot application, the `application.properties` file is an essential configuration file used to define various settings such as database connection information, server port, logging configuration, and more. This file is typically located in the `src/main/resources` directory.

Here are some common configuration items found in the `application.properties` file:

### 1. Database Connection Configuration

Used to configure the details of the data source, such as URL, username, password, and Hibernate dialect for a specific database.

```properties
# DataSource Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA / Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
```

### 2. Server Configuration

Set the server port and context path.

```properties
# Server Port
server.port=8080 # The port on which the application will run

# Context Path
server.servlet.context-path=/myapp # The base URL path for the application
```

### 3. Logging Configuration

Configure the logging level.

```properties
# Logging Levels
logging.level.org.springframework=INFO  # Log level for Spring framework
logging.level.com.mycompany.mypackage=DEBUG # Log level for a specific package
logging.level.root=WARN # Reduce logging level to WARN
```

### 4. Spring Boot Specific Configuration

Configure Spring Boot features such as the startup banner.

```properties
# Disable Startup Banner
spring.main.banner-mode=off
```

### 5. Custom Application Configuration

Define application-specific configurations.

```properties
# Custom Application Configuration
myapp.feature-x.enabled=true        # Whether a custom feature is enabled
myapp.message-of-the-day=Hello World # Custom message
```

### 6. Security Configuration

Configure Spring Security related properties.

```properties
# Spring Security
spring.security.user.name=admin   # Default username
spring.security.user.password=secret # Default password
```

### 7. Service Discovery and Registration

If your application is part of a microservice architecture and uses a service discovery mechanism.

```properties
# Service Registration and Discovery
spring.application.name=my-service-name # Application name
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/ # Eureka server URL
```

### 8. Message Queue Configuration

Configure message queues (such as RabbitMQ, Kafka) related properties.

```properties
# RabbitMQ
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

These configuration items are loaded when the application starts and can be accessed in the application using annotations like `@Value` or configuration classes.

The actual configuration items will depend on the needs and frameworks used by your application. Spring Boot provides a wide range of configuration options, covering data sources, transaction management, message queues, security settings, custom application parameters, and more.