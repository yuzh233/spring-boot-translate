---
title: 20190609 spring-boot | part3(13~16)
date: 2019-06-09
tag: spring-boot
category:
- english-learning
- spring-boot
thumbnail: http://img.yuzh.xyz/blog/90.jpg
toc: true
---

> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#using-boot

<h1 style="color:green; text-align:center;">Part III. Using Spring Boot</h1>

<!-- TOC -->

- [13. 构建系统](#13-%E6%9E%84%E5%BB%BA%E7%B3%BB%E7%BB%9F)
	- [13.1 依赖项管理](#131-%E4%BE%9D%E8%B5%96%E9%A1%B9%E7%AE%A1%E7%90%86)
	- [13.2 Maven](#132-maven)
		- [13.2.1 继承 Starter Parent](#1321-%E7%BB%A7%E6%89%BF-starter-parent)
		- [13.2.2 没有 Parent Pom 使用 Spring Boot](#1322-%E6%B2%A1%E6%9C%89-parent-pom-%E4%BD%BF%E7%94%A8-spring-boot)
		- [13.2.3 使用 Spring Boot Maven 插件](#1323-%E4%BD%BF%E7%94%A8-spring-boot-maven-%E6%8F%92%E4%BB%B6)
	- [13.3 Gradle](#133-gradle)
	- [13.4 Ant](#134-ant)
	- [13.5 启动器](#135-%E5%90%AF%E5%8A%A8%E5%99%A8)
- [14. 代码结构](#14-%E4%BB%A3%E7%A0%81%E7%BB%93%E6%9E%84)
	- [14.1 使用“默认的”包](#141-%E4%BD%BF%E7%94%A8%E9%BB%98%E8%AE%A4%E7%9A%84%E5%8C%85)
	- [14.2 定位（Location）主应用类](#142-%E5%AE%9A%E4%BD%8Dlocation%E4%B8%BB%E5%BA%94%E7%94%A8%E7%B1%BB)
- [15. 配置类](#15-%E9%85%8D%E7%BD%AE%E7%B1%BB)
	- [15.1 导入额外的配置类](#151-%E5%AF%BC%E5%85%A5%E9%A2%9D%E5%A4%96%E7%9A%84%E9%85%8D%E7%BD%AE%E7%B1%BB)
	- [15.2 导入 XML 配置](#152-%08%E5%AF%BC%E5%85%A5-xml-%E9%85%8D%E7%BD%AE)
- [16. 自动配置](#16-%E8%87%AA%E5%8A%A8%E9%85%8D%E7%BD%AE)
	- [16.1 逐步（gradually）更换（replacing）自动配置](#161-%E9%80%90%E6%AD%A5gradually%E6%9B%B4%E6%8D%A2replacing%E8%87%AA%E5%8A%A8%E9%85%8D%E7%BD%AE)
	- [16.2 禁用特定的自动配置类](#162-%E7%A6%81%E7%94%A8%E7%89%B9%E5%AE%9A%E7%9A%84%E8%87%AA%E5%8A%A8%E9%85%8D%E7%BD%AE%E7%B1%BB)

<!-- /TOC -->
<!-- more -->
这个章节将详细介绍更多细节关于你如何使用Spring Boot。它涵盖了一些主题（covers topics），例如构建系统、自动配置、和如何运行你的应用。我们同样涵盖了一些 Spring Boot 最佳实战。虽然Spring Boot没有什么特别之处（它只是你可以使用的另一个类库而已。）这里有一些建议，如果遵循（when allowed），将会使你的应用开发进度相对容易一些（easier）。

如果你是从 Spring Boot 开始的（starting out），你可能（probably）需要阅读“[快速开始](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#getting-started)”指南，在进入（diving into）这个章节之前。

# 13. 构建系统
这里强烈建议你选择一个支持 [依赖项管理](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#using-boot-dependency-management) 和可以使用 artifacts 发布到 Maven 中央仓库的构建系统。我们将建议您使用 Maven 或 Gradle。有可能使（it is possible to）Spring Boot 与其他构建工具一起工作，但是他们并没有得到专门的支持。

## 13.1 依赖项管理
每一个 Spring Boot 的发行版都对依赖项管理列表提供支持，在实践当中（in practice），你不需要在你的构建配置中添加这些依赖的任何一个 version 节点，spring boot 帮您管理。当你升级 spring boot 本身，这些依赖以同样的（consistent way）方式升级。

> 如果你需要这样做你可以一直指定（specify） version 节点以覆盖 spring boot 的建议。

该列表包含了所有你使用的 Spring Boot 的所有模块以及（as well as）精确（refind）的第三方类库列表。该列表可作为标准的物料清单(spring-boot-dependencies)提供，可与Maven和Gradle一起使用。

> 每一个 spring boot 的发行版版本与 Spring 框架的基本版本相关联。我们强烈建议你不要定制自己的版本号。

## 13.2 Maven
Maven 用户可以继承自 `spring-boot-starters-parent` 项目获得（obain）合理（sensible）的默认值。该父项目提供以下功能：

- java8 作为默认的编辑级别
- UTF-8 资源编码
- 一个[依赖管理节点](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#using-boot-dependency-management)，继承自 spring-boot-dependencies pom文件，用来管理公共依赖项的 version。该依赖项管理允许你忽略（omit）version 标签为了依赖项当你在你自己的 pom 文件中。
- 使用 repackage 的执行 id 执行 repackge 目标
- 合理（sensible）的资源过滤
- 合理的插件配置（exec plugin、git commit ID 和 shade）
- 用于 application.xml 和 application.Properties 的合理过滤，包含特殊的配置文件（如：applicatino-dev.properties 和 application-dev.yml）

请注意（note that），从 `application.properties` 和 `application.yml` 文件支持 Spring 风格的占位符(`${...}`)，Maven 过滤改变为使用`@...@`占位符。（你可以设置 maven 属性名为 `resource.dilimiter` 充血该属性）

### 13.2.1 继承 Starter Parent
继承你的项目自 `spring-boot-starter-parent`，设置 parent 节点如下：

```xml
<!-- Inherit defaults from Spring Boot -->
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.1.5.RELEASE</version>
</parent>
```

> 你只需要在这个依赖项中指定 Spring Boot 的特定版本号，如果你导入额外的启动器，你可以安全地（savely）省略该版本号。

通过该配置（with setup），你可以在你项目中通过覆盖属性来覆盖单个依赖项（individual dependencies ）。例如，升级另外的 Spring Data 发行版，你可以添加以下到你的 pom.xml:

```xml
<properties>
	<spring-data-releasetrain.version>Fowler-SR2</spring-data-releasetrain.version>
</properties>
```

> 点击这个 spring-boot-dependencies [pom](https://github.com/spring-projects/spring-boot/blob/v2.1.5.RELEASE/spring-boot-project/spring-boot-dependencies/pom.xml) 插件支持的属性列表

### 13.2.2 没有 Parent Pom 使用 Spring Boot
不是每个人都喜欢继承自 spring-boot-starters-parent pom，你可能有你自己的企业的（corporate）标准 parent 要使用，或者你想明确的（exlictily）定义所有你的 maven 配置。

如果你不想要使用 spring-boot-starters-parent，你可以通过使用一个 `scope=import` 依赖一直保持依赖管理器的好处(benefit)（但不是插件管理），如下：

```xml
<dependencyManagement>
	<dependencies>
		<dependency>
			<!-- Import dependency management from Spring Boot -->
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-dependencies</artifactId>
			<version>2.1.5.RELEASE</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>
```

上面的（preveding）示例设置不允许通过使用属性覆盖各个依赖项，如上所述（as explained above）。要达到（achieve）同样的效果，你需要在你的项目中，`spring-boot-dependencies` 之前，添加一个条目到 `dependencyManagement`。例如：要更新其他的 Spring data 发行版，你需要添加以下元素到你的 pom.xml:

```xml
<dependencyManagement>
	<dependencies>
		<!-- Override Spring Data release train provided by Spring Boot -->
		<!-- 在 spring-boot-dependencies 之前指定这个 -->
		<dependency>
			<groupId>org.springframework.data</groupId>
			<artifactId>spring-data-releasetrain</artifactId>
			<version>Fowler-SR2</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-dependencies</artifactId>
			<version>2.1.5.RELEASE</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>
```

> 如上面例子，我们指定一个 POM，但是但是任何的依赖项类型以相同的方式覆盖。

### 13.2.3 使用 Spring Boot Maven 插件
Spring Boot 包含一个 Maven 插件，可以打包项目作为一个可执行 jar。如果你想使用它添加以下插件到你的 `<plugins>` 节点，如以下示例所示：

```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
```

> 如果你使用 Spring Boot 父启动器 pom，你只需要添加插件。这里不需要配置除非你想要改变在 parent 中的设置定义。

## 13.3 Gradle
要学习使用 Spring Boot 的 Gradle，请参考（refer）Spring Boot 的 Gradle 插件文档：

- 参考（HTML 和 PDF）
- API

## 13.4 Ant

可以使用 ApacheAnt + Ivy 构建 SpringBoot 项目。这个 `spring-boot-antlib`，“ant-lib”模块同样可用于（available to）帮助 Ant 创建可执行jar。

要定义这个依赖项，一个典型的（a typical）的 `ivy.xml` 文件看起来像下面的例子：

```xml
<ivy-module version="2.0">
	<info organisation="org.springframework.boot" module="spring-boot-sample-ant" />
	<configurations>
		<conf name="compile" description="everything needed to compile this module" />
		<conf name="runtime" extends="compile" description="everything needed to run this module" />
	</configurations>
	<dependencies>
		<dependency org="org.springframework.boot" name="spring-boot-starter"
			rev="${spring-boot.version}" conf="compile" />
	</dependencies>
</ivy-module>
```

一个典型的 `build.xml` 文件看起来像下面的实例：

```xml
<project
	xmlns:ivy="antlib:org.apache.ivy.ant"
	xmlns:spring-boot="antlib:org.springframework.boot.ant"
	name="myapp" default="build">

	<property name="spring-boot.version" value="2.1.5.RELEASE" />

	<target name="resolve" description="--> retrieve dependencies with ivy">
		<ivy:retrieve pattern="lib/[conf]/[artifact]-[type]-[revision].[ext]" />
	</target>

	<target name="classpaths" depends="resolve">
		<path id="compile.classpath">
			<fileset dir="lib/compile" includes="*.jar" />
		</path>
	</target>

	<target name="init" depends="classpaths">
		<mkdir dir="build/classes" />
	</target>

	<target name="compile" depends="init" description="compile">
		<javac srcdir="src/main/java" destdir="build/classes" classpathref="compile.classpath" />
	</target>

	<target name="build" depends="compile">
		<spring-boot:exejar destfile="build/myapp.jar" classes="build/classes">
			<spring-boot:lib>
				<fileset dir="lib/runtime" />
			</spring-boot:lib>
		</spring-boot:exejar>
	</target>
</project>
```

> 如果你不想使用 `spring-boot-antlib` 模块，查看章节 91.9：不使用 spring-boot-ant 从 Ant 构建可执行归档。

## 13.5 启动器
启动器是一组（set of）方便的（convenient）依赖描述符（descriptors），可以包含在你的应用中。你获得所有 Spring 和与之关联的技术的一站式（one-stop）服务，你不需要（need without）寻找（hunt throught）相似代码和复制粘贴大量的依赖描述符。如：如果你想开始获得 Spring 和 JPA 访问数据库，包含 `spring-data-jpa`依赖到你的项目中。

该启动器包含了大量的依赖项，你需要这些才可以方便的获得项目一致性和快速运行。支持管理传递（transitive）依赖。

> 名字里有什么？
所有官方的启动器遵循相似的命令规范；`spring-boot-starters-*`，其中 `*` 是特定（particular）类型的应用。这个命名结构是为了（intented to）帮助你寻找启动器。Maven 集成了许多 IDE 允许你通过名字查找依赖项。例如：安装了适当的 Eclipse 或 STS 插件，你可以在 Pom 编辑器按下 `ctrl + space` 并输入 `spring-boot-starter` 一个完整清单。
\
如 “创建你自己的启动器” 章节解释（explained）的一样，第三方启动器不需要以 `spring-boot` 开头，因为它是为官方的 Spring Boot 制品保留的。相反（Rather），一个第三方启动器典型的以项目名字开始，如：一个第三方应用叫做 `thirdpartyproject` 将会命名为 `thirdpartyproject-spring-boot-starter`

以下应用程序由 Spring Boot 在 `org.springframework.boot` 组下提供：

Name                                        | Description                                                                                             | Pom
--------------------------------------------|---------------------------------------------------------------------------------------------------------|----
spring-boot-starter                         | 核型启动器，包含自动配置支持，日志和 YAML                                                               | Pom
spring-boot-starter-activemq                | 使用 Apache ActiveMQ 的 JMS 消息启动器                                                                  | Pom
spring-boot-starter-amqp                    | Starter for using Spring AMQP and Rabbit MQ                                                             | Pom
spring-boot-starter-aop                     | 使用 Spring AOP 和 AspectJ 面向（oriented）切面编程的启动器                                             | Pom
spring-boot-starter-artemis                 | 使用 Apache Artemis 的 JMS 消息启动器                                                                   | Pom
spring-boot-starter-batch                   | Starter for using Spring Batch                                                                          | Pom
spring-boot-starter-cache                   | Starter for using Spring Framework’s caching support                                                    | Pom
spring-boot-starter-cloud-connectors        | 使用SpringCloud连接器，简化了与云平台中服务，如 Cloud Foundry and Heroku                                | Pom
spring-boot-starter-data-cassandra          | 使用 Cassandra      分布式数据库和 Spring Data Cassandra                                                | Pom
spring-boot-starter-data-cassandra-reactive | 使用 Cassandra      分布式数据库和 Spring Data Cassandra   反应                                         | Pom
spring-boot-starter-data-couchbase          | 使用 Couchbase 面向文档数据库和 Spring Data Couchbase                                                   | Pom
spring-boot-starter-data-couchbase-reactive | 使用 Couchbase 面向文档数据库和 Spring Data Couchbase   反应                                            | Pom
spring-boot-starter-data-elasticsearch      | 使用 Elasticsearch 搜索和分词引擎 和 Spring Data Elasticsearch                                          | Pom
spring-boot-starter-data-jdbc               | Starter for using Spring Data JDBC                                                                      | Pom
spring-boot-starter-data-jpa                | Starter for using Spring Data JPA with Hibernate                                                        | Pom
spring-boot-starter-data-ldap               | Starter for using Spring Data LDAP                                                                      | Pom
spring-boot-starter-data-mongodb            | 使用 MongoDB 面向文档数据库 和 Spring Data MongoDB                                                      | Pom
spring-boot-starter-data-mongodb-reactive   | 使用 MongoDB 面向文档数据库 和 Spring Data MongoDB  反应                                                | Pom
spring-boot-starter-data-neo4j              | 使用 Neo4j 图数据库 和 Spring Data Neo4j                                                                | Pom
spring-boot-starter-data-redis              | 使用 Redis 键值存储和 Spring Data Redis and the Lettuce client                                          | Pom
spring-boot-starter-data-redis-reactive     | 使用 Redis 键值存储和 Spring Data Redis and the Lettuce client                                          | Pom
spring-boot-starter-data-rest               | 使用 Spring Data REST 曝光 Spring Data 存储库为 rest                                                    | Pom
spring-boot-starter-data-solr               | 使用 Spring Data Solr 的 Apache Solr 搜索平台                                                           | Pom
spring-boot-starter-freemarker              | 使用 FreeMarker 视图构建 MVC Web 应用                                                                   | Pom
spring-boot-starter-groovy-templates        | 使用 Groovy 模版构建 MVC Web 应用                                                                       | Pom
spring-boot-starter-hateoas                 | 使用 Spring MVC 和 Spring HATEOAS 构建基于超媒体的 RestFul web 应用                                     | Pom
spring-boot-starter-integration             | 使用 Spring 整合                                                                                        | Pom
spring-boot-starter-jdbc                    | 使用 HikariCP 连接池的JDBC                                                                              | Pom
spring-boot-starter-jersey                  | 使用 JAX-RS 和 Jersey 构建 restfull web 应用. 另一种选择（An alternative to）是 spring-boot-starter-web | Pom
spring-boot-starter-jooq                    | 使用 jOOQ 访问 SQL 数据库. 另一种选择是 spring-boot-starter-data-jpa 或 spring-boot-starter-jdbc        | Pom
spring-boot-starter-json                    | 读写 json                                                                                               | Pom
spring-boot-starter-jta-atomikos            | 使用 Atomikos 的 JTA 事务                                                                               | Pom
spring-boot-starter-jta-bitronix            | 使用 Bitronix 的 JTA 事务                                                                               | Pom
spring-boot-starter-mail                    | 使用 Java Mail 和 Spring Framework’s 邮件发送支持                                                       | Pom
spring-boot-starter-mustache                | 使用 Mustache views 构建 web 应用                                                                       | Pom
spring-boot-starter-oauth2-client           | 使用 Spring Security’s OAuth2/OpenID 连接客户端特性                                                     | Pom
spring-boot-starter-oauth2-resource-server  | 使用 Spring Security’s OAuth2 资源服务器特性                                                            | Pom
spring-boot-starter-quartz                  | 使用 Quartz 任务调度                                                                                    | Pom
spring-boot-starter-security                | 使用 Spring Security                                                                                    | Pom
spring-boot-starter-test                    | 用库或者 Junit Hamcrest 和 Mockito 测试 Spring Boot 应用                                                | Pom
spring-boot-starter-thymeleaf               | 使用 Thymeleaf views 构建 web 应用                                                                      | Pom
spring-boot-starter-validation              | 在 Hibernate Validator 中使用 Java Bean 验证                                                            | Pom
spring-boot-starter-web                     | 使用 Spring MVC 构建 restfull web 应用. 使用 tomcat 作为默认内嵌容器                                    | Pom
spring-boot-starter-web-services            | 使用 Spring Web 服务                                                                                    | Pom
spring-boot-starter-webflux                 | 使用 Spring Framework’s 响应式 web 支持构建 WebFlux 应用                                                | Pom
spring-boot-starter-websocket               | 使用 Spring Framework’s WebSocket 支持构建 WebSocket 应用                                               | Pom

除了（in addition to）应用启动器，以下启动器可用来添加到“生产可读”特性：

Name                         | Description                                                       | POM
-----------------------------|-------------------------------------------------------------------|----
spring-boot-starter-actuator | 使用 Spring Boot 的监控提供生产可读的特性帮助你监视并管理你的应用 | POM

最终，如果你想排除（exclude）或替换（swap）特定的技术方面，Spring Boot 同样包含以下启动器可以使用：

name                              | Description                                                                              | Pom
----------------------------------|------------------------------------------------------------------------------------------|----
spring-boot-starter-jetty         | 使用 Jetty 作为内嵌服务器，另一个可替代的（alternative）是：spring-boot-starter-tomcat   | Pom
spring-boot-starter-log4j2        | 使用 Log4j2 作为日志记录，可替代的是：spring-boot-starter-logging                        | Pom
spring-boot-starter-logging       | 使用 Logback 作为日志记录，是默认的日志记录启动器                                        | Pom
spring-boot-starter-reactor-netty | 使用 Reactor Netty 作为内嵌的响应式 HTTP 服务器                                          | Pom
spring-boot-starter-tomcat        | 使用 Tomcat 作为内嵌的 servlet 服务器，spring-boot-starter-web 使用的默认 servlet 服务器 | Pom
spring-boot-starter-undertow      | 使用 Undertow 作为内嵌服务器，一个可替代的是：spring-boot-starter-tomcat                 | Pom

> 更多的社区贡献的启动器列表，请在 GITHUB 的 spring-boot-starters 模块中查看 README file

# 14. 代码结构
Spring Boot 不要求你工作时的任意特定的代码结构布局。但是，这里有最佳实践可以帮助你。

## 14.1 使用“默认的”包
当一个类没有包含 `package` 声明（declaration），它被认为是（it is considered to）在默认的包中。使用默认的包通常（generally）不被鼓励（discouraged）应该尽量避免（avoided）。在 Spring Boot 使用 `@ComponentScan`,`@EntityScan`,`@SpringBootApplication` 时这会导致一些特定的问题，因为每个类每个 jar 都是可读的。

> 我们建议你遵循 java 推荐的包命名约定（Convertions）并反转域名名字（例如：com.example.project）

## 14.2 定位（Location）主应用类
我们通常建议你在其他类之上的根包中放置（Locate）您的主应用程序类，该 `@SpringBootApplication` 注解经常被放在（place）你的主类，它隐式（implicitly）定义某些（cartain）“查询包”。例如：如果你要写一个 JPA 应用，`@SpringBootApplication` 注解类的包用于搜索 `@Entity` 项。使用根包还允许注解只扫描你的应用。

> 如果你不想使用 `@SpringBootApplication`，`@EnableAutoConfiguration` 和 `@ComponentScan` 注解导入了定义的行为，所以你同样可以使用他们。

以下列表展示了典型的布局：

```
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

一个 `Application.java` 文件会定义一个 main 方法，连同基础的 `@SpringBootApplication`，如下：

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}
```

# 15. 配置类
spring boot 支持（favors）基于 java 的配置，虽然能够使用基于 XML 资源的 `SpringApplication`，我们通常建议你主要资源是一个（be a）单个 `@Configuration` 类。通常定义 main 方法的类是 @Configuration 的主要候选者。

> 许多 Spring 配置样例使用 XML 配置在网络上发布。如果可能，永远尝试使用相等的基于 Java 的配置。搜索 `Enable*` 注解是一个很好的开始。

## 15.1 导入额外的配置类
你不需要把所有的 @Configuration 都放在一个配置类中。@Import 注解可以被用来导入额外的配置类。另外（Alternatively），你可以使用 @CompomentScan 去动态的获取（pick up）所有的 Spring 组件，包含 @Configuration 类。

## 15.2 导入 XML 配置
如果你绝对（Absolutely）要用基于 XML 的配置，我们建议你仍然（still）从 @Configuration 类开始。你可以使用 @ImportResource 注解加载 XML 配置文件。

# 16. 自动配置
Spring Boot 自动配置尝试（attempts）去动态的配置你的 Spring 应用基于在你添加的 jar 依赖项之上。例如：如果 `HSQLDB` 在你的类路径下，并且你没有手动（manually）配置任何数据库连接 bean，spring boot 会在内存中自动配置数据库。

你需要添加 @EnableAutoConfiguration 或者 @SpringBootApplication 其中一个注解到你的一个 @Configuration 配置类上来选择自动配置。

> 你应该只添加一个注解 @EnableAutoConfiguration 或者 @SpringBootApplication。我们通常建议你只添加一个或另外一个到您的 @Configuration 配置类上。

## 16.1 逐步（gradually）更换（replacing）自动配置
自动配置是非侵入型的（non-invasive）。任何时候，你可以开始定义你自己的配置类来替换特定部分的自动配置。例如：如果你添加你自己的 DataSource bean，默认内嵌的数据库将不再支持（backs away）。

如果你想找出（find out）当前（currently）正在应用（being applied）的自动配置，和为什么，使用 `--debug` 开关（switch）开始你的应用。这样做使调试日志可以选择核心日志记录器，并将条件报告记录到控制台。

## 16.2 禁用特定的自动配置类
如果你发现一些自动配置类并不想它被应用，你可以为 @EnableAutoConfiguration 使用 exclude 属性关闭他们，as shown in the following example:

```java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
```

如果该 class 不在类路径下，你可以使用注解的 `excludeName` 属性并指定完全限定名。最终，你同样可以控制要排除的自动配置列表通过 `spring.autoconfigure.exclude` 属性。

> 可以在注释级别和使用属性定义排除。
