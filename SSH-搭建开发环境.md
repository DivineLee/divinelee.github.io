---
title: SSH-搭建开发环境
date: 2017-10-29
categories:
- Java
tags:
- SSH
---
1、创建一个web工程:

2、引入jar包和配置文件:
    * struts2:
        * jar包:
            struts-2.3.15.3\apps\struts2-blank.war\WEB-INF\lib\*.jar
            struts-2.3.15.3\lib\struts2-json-plugin-2.3.15.3.jar
            struts-2.3.15.3\lib\struts2-spring-plugin-2.3.15.3.jar
        * 配置文件:
             * web.xml
                <!-- 配置Struts2的核心过滤器 -->
                <filter>
                     <filter-name>struts2</filter-name>
                     <filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
                 </filter>
 
                 <filter-mapping>
                     <filter-name>struts2</filter-name>
                     <url-pattern>/*</url-pattern>
                  </filter-mapping>
               * struts.xml 

    * Spring:
        * jar包:
            Spring3.2 开发最基本jar包
                spring-beans-3.2.0.RELEASE.jar
                spring-context-3.2.0.RELEASE.jar
                spring-core-3.2.0.RELEASE.jar
                spring-expression-3.2.0.RELEASE.jar
                com.springsource.org.apache.commons.logging-1.1.1.jar
                com.springsource.org.apache.log4j-1.2.15.jar
            AOP开发
                spring-aop-3.2.0.RELEASE.jar
                spring-aspects-3.2.0.RELEASE.jar
                com.springsource.org.aopalliance-1.0.0.jar
                com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
            Spring Jdbc开发
                spring-jdbc-3.2.0.RELEASE.jar
                spring-tx-3.2.0.RELEASE.jar
            Spring事务管理
                spring-tx-3.2.0.RELEASE.jar
            Spring整合其他ORM框架
                spring-orm-3.2.0.RELEASE.jar
            Spring在web中使用
                spring-web-3.2.0.RELEASE.jar
            Spring整合Junit测试
                spring-test-3.2.0.RELEASE.jar
        * 配置文件:
            * web.xml
                 <!-- 配置Spring的核心监听器 -->
                 <listener>
                     <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
                 </listener>
 
                 <context-param>
                     <param-name>contextConfigLocation</param-name>
                     <param-value>classpath:applicationContext.xml</param-value>
                 </context-param>
            * applicationContext.xml
            * log4j.properties

    * Hibernate:
        * jar包:
            hibernate-distribution-3.6.10.Final\hibernate3.jar
            hibernate-distribution-3.6.10.Final\lib\required\*.jar
            hibernate-distribution-3.6.10.Final\lib\jpa\*.jar
            * slf4j-log4j整合的jar包 :
            * 数据库驱动:
            * 连接池:(c3p0连接池)
        * 配置文件:
            * 没有hibernate的核心配置文件的方式整合:
            * 映射文件:

3、配置基本配置信息:
    * C3P0连接池:
    * 引入外部属性文件:
        * jdbc.properties
    * 配置连接池:
         <!-- 配置连接池: -->
         <!-- 引入外部属性文件 -->
         <context:property-placeholder location="classpath:jdbc.properties"/>
         <!-- 配置C3P0连接池: -->
         <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
             <property name="driverClass" value="${jdbc.driver}"/>
             <property name="jdbcUrl" value="${jdbc.url}"/>
             <property name="user" value="${jdbc.user}"/>
             <property name="password" value="${jdbc.password}"/>
         </bean>
    * Hibernate相关信息:
         <!-- Hibernate的相关信息 -->
         <bean id="sessionFactory" class="org.springframework.orm.hibernate3.LocalSessionFactoryBean">
             <!-- 注入连接池 -->
             <property name="dataSource" ref="dataSource"/>
             <!-- 配置Hibernate的其他的属性 -->
             <property name="hibernateProperties">
                 <props>
                     <prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
                     <prop key="hibernate.show_sql">true</prop>
                     <prop key="hibernate.format_sql">true</prop>
                     <prop key="hibernate.connection.autocommit">false</prop>
                     <prop key="hibernate.hbm2ddl.auto">update</prop>
                 </props>
             </property>
             <!-- 配置Hibernate的映射文件 -->  
         </bean>
    * 事务管理:
         <!-- 事务管理: -->
         <!-- 事务管理器 -->
         <bean id="transactionManager" class="org.springframework.orm.hibernate3.HibernateTransactionManager">
             <property name="sessionFactory" ref="sessionFactory"/>
         </bean>
 
         <!-- 开启注解事务 -->
         <tx:annotation-driven transaction-manager="transactionManager"/>
