---
title: spring boot数据库配置
tags:
  - spring
categories: 后端
date: 2019-07-24 13:26:13
---

# 框架配置

## jpa

- 导入依赖
<!-- more -->
``` xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<scope>runtime</scope>
</dependency>

```

- 配置

``` yaml
spring: 
    jpa: 
        hibernate: 
            ddl-auto: update
        show-sql: true
```

- dao接口继承JpaRepository就可以调用其中的方法操纵数据库了

## mybatis

- 导入依赖

``` xml
<dependency>
	<groupId>org.mybatis.spring.boot</groupId>
	<artifactId>mybatis-spring-boot-starter</artifactId>
</dependency>
```
- 配置

``` yaml
mybatis:
    mapper-locations: classpath:mapper/*.xml # mapper文件位置
    type-aliases-package: com.xxx.model # 实体类的位置
```

在spring boot启动类上加`@MapperScan(basePackages = "com.xxx")`

# Mysql

广泛使用的关系型数据库,在spring boot中配置方式为

```yaml
spring:
    datasource:
        url: jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=utf8&useSSL=false
        username: 
        password:
```

# H2

java实现的嵌入数据库，不需要安装，适合编写damo使用，在spring boot中的配置方式为

```yaml
spring:
    h2:
        console:
            enabled: true # 启用自带的控制台界面访问/h2-console
    datasource:
        url: jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
        driverClassName: org.h2.Driver
        username: 
        password:
```