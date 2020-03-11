---
title: mybatis逆向工程
tags:
  - mybatis
categories: 后端
date: 2019-07-07 13:26:13
---

使用mybatis逆行工程生成sql文件和model类很方便，配置，记一下配置文件，方便创建项目使用


- 引入mavan依赖
<!-- more -->
```xml
    <dependencies>
        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.1</version>
        </dependency>

    </dependencies>

    <!--插件-->
    <build>
        <plugins>
            <!--spring boot maven插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>

            <!--MyBatis自动生成工具插件-->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.5</version>
                <configuration>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>

        </plugins>
    </build>

```
- 在resource路径下创建generatorConfig.xml文件

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!--数据库驱动 引入的本地的驱动包,直接拷贝maven构建的路径即可-->
    <classPathEntry location="C:\Users\user\.m2\repository\mysql\mysql-connector-java\8.0.16\mysql-connector-java-8.0.16.jar"/>

    <context id="manger" targetRuntime="MyBatis3" defaultModelType="flat">

        <!--自动实现Serializable接口-->
        <plugin type="org.mybatis.generator.plugins.SerializablePlugin"/>

        <!-- 去除自动生成的注释 -->
        <commentGenerator>
            <property name="suppressAllComments" value="true" />
        </commentGenerator>

        <!--数据库链接地址账号密码-->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/spring?useUnicode=true&amp;characterEncoding=utf-8&amp;serverTimezone=UTC&amp;useSSL=false&amp;tinyInt1isBit=false"
                        userId="root"
                        password="root">
        </jdbcConnection>

        <!--生成Model类存放位置-->
        <javaModelGenerator targetPackage="cn.dlm.model" targetProject="./src/main/java">

        </javaModelGenerator>


        <!--生成映射文件存放位置-->
        <sqlMapGenerator targetPackage="mapper" targetProject="./src/main/resources">

        </sqlMapGenerator>

        <!--生成Dao类存放位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="cn.dlm.mapper" targetProject="./src/main/java">
            <property name="enableSubPackages" value="false"/>
        </javaClientGenerator>


        <table tableName="user" catalog="spring" >
            <property name="ignoreQualifiersAtRuntime" value="true"/>
            <property name="constructorBased" value="true"/>
        </table>


    </context>
</generatorConfiguration>
```

- 在maven下使用generator插件即可生成