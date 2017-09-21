---
layout: post
title: "2017-09-21-管理数据库版本Flyway应用"
date: 2017-09-20 
description: "Flyway"
tag: Java
---   
## Flyway简介
- Flyway是什么？

	Flyway是独立于数据库的应用、管理并跟踪数据库变更的数据库版本管理工具。Arun Gupta, Director of Developer Advocacy, Red Hat 曾说Flyway应该是所有Java企业应用开发的一个基础部分，它让数据库迁移无缝整合在整个应用生命周期。

- 为什么要用Flyway？
	Flyway的官网是如此介绍的：
	
	如果有一个软件叫Shiny Soft，以及它对应的数据库Shiny DB。简单的呈现如下图  

	![](/blogImages/flywayshinny.jpg)

	但是在大多数项目中，它应该如下图
	
	![](/blogImages/flywaySchema.jpg)	

	这样一来，我们就不仅要处理一个环境的备份，而是好几个。这样就会带来一系列问题
	代码版本进行很好的控制和定义，而数据库呢？ 产品在一个环境不停的迭代，而在另一个环境数据库的版本应该是哪个版本呢？目前大多数项目还是依赖人工执行sql脚本。
	
	![](/blogImages/flywayshinnyDB.jpg)

	所以数据库迁移其实重点是对数据库版本进行控制，此时Flyway应运而生。

- Flyway工作原理
	最简单的场景是当你的Flyway指向一个空数据库
	
	![](/blogImages/EmptyDb.jpg)

	Flyway会去检查数据库中的Flyway的基础表，如果当你的数据库是空数据库是，Flyway将创建它的基础表。这是数据库就有了一个叫`SCHEMA_VERSION`的空表，这张表会用于跟踪数据库的状态。Flyway会扫描sql文件，根据版本号排序，依次执行sql语句。如果已有基础表，Flyway会根据已有的`SCHEMA_VERSION`中的版本号，对此版本号之后的脚本进行升级。

	![](/blogImages/Migration-1-2.jpg)


## SpringMVC+Maven如何整合Flyway

- 在pom.xml文件中，加入依赖，版本号自行决定，在此选用4.0.3版本
  ```bash
	<dependency>
	    <groupId>org.flywaydb</groupId>
	    <artifactId>flyway-core</artifactId>
	    <version>4.0.3</version>
	</dependency>
  ```

- 建立数据库迁移拦截器，以自身项目为例，建立DBMigrationInterceptor.java
	```java
	import javax.annotation.PostConstruct;
	import org.flywaydb.core.Flyway;
	import com.alibaba.druid.support.logging.Log;
	import com.alibaba.druid.support.logging.LogFactory;
	public class DBMigrationInteceptor {
	    private Log log = LogFactory.getLog(DBMigrationInteceptor.class);  
	    private Flyway flyway;  
	    
	    @PostConstruct  
	    public void run() {  
	        log.info("[Start] DbMigration run .. ");
	        flyway.setBaselineOnMigrate(true);
	        flyway.migrate();   
	        log.info("[End] DbMigration run .. ");  
	    }  
	    public void setFlyway(Flyway flyway) {  
	        this.flyway = flyway;  
	    }  
	}
	```

- 建立数据库脚本：在对应的resource下建立文件夹，记录每次升级sql脚本并在名称上进行版本约束。注意：sql脚本的命名规则是严格的，V<version>[_<SEQ>][__description] 。版本号的数字间以小数点（. ）或下划线（_ ）分隔开，版本号与描述间以连续的两个下划线（__ ）分隔开。如`V1_1_0__Update.sql `
	![](/blogImages/sql.jpg)

- 在Spring中配置flyway的Java bean。
	```java
	<bean id="flyway" class="org.flywaydb.core.Flyway" depends-on="dataSource1" lazy-init="false">  
    	<property name="dataSource" ref="dataSource1"/>
	</bean>  
	<bean id="jFlyway" class="com.interceptor.DBMigrationInteceptor" lazy-init="false" depends-on="flyway">  
	    <property name="flyway" ref="flyway"/>  
	</bean>  
	```
	其中id=flyway的bean中需提前配置dataSource，dataSource指向了当前的dataSource1。
	id=JFlyway的bean中需配置拦截器地址。

- 至此为止，当项目重新启动时，flyway就会正常工作。

更多问题可以参考flyway官网，https://flywaydb.org/