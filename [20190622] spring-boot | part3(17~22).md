---
title: 20190622 spring-boot | part3(17~22)
date: 2019-06-09
tag: spring-boot
category:
- english-learning
- spring-boot
thumbnail: http://img.yuzh.xyz/blog/wallhaven-201451.jpg
toc: true
---

> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-spring-beans-and-dependency-injection.html

<h1 style="color:green; text-align:center;">Part III. Using Spring Boot</h1>
<!-- TOC -->

- [17 Spring Bean 依赖注入](#17-spring-bean-%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5)
- [18. 使用 @SpringBootApplication 注解](#18-%E4%BD%BF%E7%94%A8-springbootapplication-%E6%B3%A8%E8%A7%A3)
- [19. 运行你的应用](#19-%E8%BF%90%E8%A1%8C%E4%BD%A0%E7%9A%84%E5%BA%94%E7%94%A8)
	- [19.1 从 IDE 运行](#191-%E4%BB%8E-ide-%E8%BF%90%E8%A1%8C)
	- [19.2 作为打包应用程序运行](#192-%08%E4%BD%9C%E4%B8%BA%E6%89%93%E5%8C%85%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E8%BF%90%E8%A1%8C)
	- [19.3 使用 Maven 插件](#193-%E4%BD%BF%E7%94%A8-maven-%E6%8F%92%E4%BB%B6)
	- [19.4 使用 Gradle 插件](#194-%E4%BD%BF%E7%94%A8-gradle-%E6%8F%92%E4%BB%B6)
	- [19.5 热部署](#195-%E7%83%AD%E9%83%A8%E7%BD%B2)
- [20. 开发者工具](#20-%E5%BC%80%E5%8F%91%E8%80%85%E5%B7%A5%E5%85%B7)
	- [20.1 默认属性](#201-%E9%BB%98%E8%AE%A4%E5%B1%9E%E6%80%A7)
	- [20.2 自动重启](#202-%E8%87%AA%E5%8A%A8%E9%87%8D%E5%90%AF)
		- [20.2.1. 在状态评估（condition evaluation）中记录变化](#2021-%E5%9C%A8%E7%8A%B6%E6%80%81%E8%AF%84%E4%BC%B0condition-evaluation%E4%B8%AD%E8%AE%B0%E5%BD%95%08%E5%8F%98%E5%8C%96)
		- [20.2.2. 排除资源](#2022-%E6%8E%92%E9%99%A4%E8%B5%84%E6%BA%90)
		- [20.2.3. 监视额外的路径](#2023-%E7%9B%91%E8%A7%86%E9%A2%9D%E5%A4%96%E7%9A%84%E8%B7%AF%E5%BE%84)
		- [20.2.4. 禁用重启](#2024-%E7%A6%81%E7%94%A8%E9%87%8D%E5%90%AF)
		- [20.2.5. 使用触发文件](#2025-%E4%BD%BF%E7%94%A8%E8%A7%A6%E5%8F%91%E6%96%87%E4%BB%B6)
		- [20.2.6. 定制重启类加载器](#2026-%E5%AE%9A%E5%88%B6%E9%87%8D%E5%90%AF%E7%B1%BB%E5%8A%A0%E8%BD%BD%E5%99%A8)
		- [20.2.7. 已知限制](#2027-%E5%B7%B2%E7%9F%A5%E9%99%90%E5%88%B6)
	- [20.3 热加载](#203-%E7%83%AD%E5%8A%A0%E8%BD%BD)
	- [20.4 全局设置](#204-%E5%85%A8%E5%B1%80%E8%AE%BE%E7%BD%AE)
	- [20.5 远程应用](#205-%E8%BF%9C%E7%A8%8B%E5%BA%94%E7%94%A8)
		- [20.5.1 运行远程应用客户端](#2051-%E8%BF%90%E8%A1%8C%E8%BF%9C%E7%A8%8B%E5%BA%94%E7%94%A8%E5%AE%A2%E6%88%B7%E7%AB%AF)
		- [20.5.2 远程更新](#2052-%E8%BF%9C%E7%A8%8B%E6%9B%B4%E6%96%B0)
- [21. 为生产环境打包你的应用](#21-%E4%B8%BA%E7%94%9F%E4%BA%A7%E7%8E%AF%E5%A2%83%E6%89%93%E5%8C%85%E4%BD%A0%E7%9A%84%E5%BA%94%E7%94%A8)
- [22. 下一步是什么](#22-%08%E4%B8%8B%E4%B8%80%E6%AD%A5%E6%98%AF%E4%BB%80%E4%B9%88)

<!-- /TOC -->
<!-- more -->
# 17 Spring Bean 依赖注入
你可以免费使用任意标准的 Spring 框架技术来定义的你的 bean 和管理依赖注入。为了简单，我们经常发现使用 @ComponentScan （查找你的 bean）和使用 @Autowired （做依赖注入）效果很好（work well）。
<!-- more -->
如果按照上面的建议构造你的代码（在根包中定位应用程序类），你可以无理由的（without arguments）添加 @ComponentScan。你应用的所有组件（@Component、@Service、@Repository、@Controller）都会自动注册到 Spring bean里。

以下实例展示了一个 @Service bean，它使用控制器注入以获得必要的 `RiskAssessor` bean：

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class DatabaseAccountService implements AccountService {

	private final RiskAssessor riskAssessor;

	@Autowired
	public DatabaseAccountService(RiskAssessor riskAssessor) {
		this.riskAssessor = riskAssessor;
	}

	// ...

}
```

如果这个 bean 有一个控制器，你可以省略 @Autowired，如以下所示：
```java
@Service
public class DatabaseAccountService implements AccountService {

	private final RiskAssessor riskAssessor;

	public DatabaseAccountService(RiskAssessor riskAssessor) {
		this.riskAssessor = riskAssessor;
	}

	// ...

}
```

> 注意，如果使用控制器注入让 riskAssessor 字段标记为 final。这表明（indicating）它随后（subsequently）不能被修改。

# 18. 使用 @SpringBootApplication 注解
许多 Spring Boot 的开发者喜欢他们的应用使用自动配置，组件扫描和能够（be able to）在他们的主类上定义额外的（extra）的配置。一个单一的 @SpringBootApplication 注解就可以被用于启用这些三个特性，他们是：

- `@EnableAutoConfiguration`：开启[Spring Boot 的自动配置机制](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-auto-configuration.html)
- `@ComponentScan`：对应用程序所在的包启用 @Component 扫描（[最佳实战](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-structuring-your-code.html)）
- `@Configuration`：允许在上下文注册额外的 bean 或者导入额外的配置类

这个 @SpringBootApplication 注解等价于（equivalent）使用 @Configuration，@EnableAutoConfiguration，和 @ComponentScan 他们的默认属性，如下所示：

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}
```

> @SpringBootApplication 同样提供别名定义 @EnableAutoConfiguration，和 @ComponentScan 的属性

这些功能都不是强制性的（mandatory），你可以选择通过打开任何的特性来替换这个单个注解。例如：你可能不想在你的应用中使用注解扫描：

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

@Configuration
@EnableAutoConfiguration
@Import({ MyConfig.class, MyAnotherConfig.class })
public class Application {

	public static void main(String[] args) {
			SpringApplication.run(Application.class, args);
	}

}
```

在这个例子中，Application 就像其他的 Spring Boot 应用一样除了 @Component 注解类不会被监测到，用户定义的 bean 被显式的导入（见 @Import）。

# 19. 运行你的应用
打包你的应用作为一个 jar 和使用内嵌的 HTTP 服务器的一个最大的优势是：你可以像其他应用程序一样运行你的应用。Spring Boot 的调试也同样简单，你不需要任何特定的 IDE 插件或拓展程序。

> 这个章节只涵盖基于包的 jar，如果你选择打包你的应用作为一个 war 包文件，你可以参考服务器和 IDE 文档。

## 19.1 从 IDE 运行
你可以从你的 IDE 作为一个简单的 Java 应用运行 Spring Boot。然而，你首先需要导入你的项目。导入的步骤的不同（vary）依赖于（depending on）你的 IDE 和构建系统。大多数 IDE 可以直接导入 maven 项目。例如：Eclipse 用户可以选择 `import` -> `existing maven projects` 从文件菜单。

如果你不想直接导入你的项目到你的 IDE，你可以通过使用构建插件生成 IDE 元数据。Maven 包含了 IDEA 和 Eclipse 插件。gradle 为各种（various） ide 提供插件。

> 如果你不小心（accidentally）运行了你的应用程序两次，你可以查看“端口已被使用”错误。STS 用户可以使用 `Relaunch` 按钮而不是（rather than）`Run` 按钮以确保（ensure）任何存在的实例是关闭的。

## 19.2 作为打包应用程序运行
如果你使用 Spring Boot Maven 或 Gradle 插件创建一个可执行 jar，你可以运行你的应用使用 `java -jar`，如以下所示：

```sh
java -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

还可以在启用远程调试支持的情况下运行打包应用程序。这样做可以使你依附一个调试器到你的应用程序，如以下所示：

```sh
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n \
       -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

## 19.3 使用 Maven 插件
Spring Boot Maven 插件包含一个 `run` 目标可以使用它快速启动编译和运行你的应用。应用程序以分解形式（exploded）运行，如在你的 IDE 一样。以下的一个例子展示了一个典型的 maven 命令运行你的 spring boot 应用：

	mvn spring-boot:run

你可能想要使用 `MAVEN_OPTS` 操作系统环境变量，如下所示：

	export MAVEN_OPTS=-Xmx1024m


## 19.4 使用 Gradle 插件
Spring Boot Gradle 插件同样包含 `bootRun` 任务可以被使用来分解式的运行你的应用。每当你应用 `org.springframework.boot` 和 `java` 插件时都会添加 `bootRun`，如下所示：

	gradle bootRun

你可能想要使用 `JAVA_OPTS` 操作系统环境变量，如下所示：

	export JAVA_OPTS=-Xmx1024m

## 19.5 热部署
由于 Spring Boot 应用只是一个普通的（plain）的 Java 应用，JVM 热部署可以开箱即用（work out of the box）。JVM 热部署有点受限于（somewhat limited with）它可以替换的字节码。更多的编译解决方案，可以使用 [JRebel](https://zeroturnaround.com/software/jrebel/)

`spring-boot-devtools` 模块同样包括了支持应用快速重启。查看本章节后面的（later in this chapter）[20 章 —— 开发工具](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/html/using-boot-devtools.html) 和 [如何使用热部署](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/html/howto-hotswapping.html) 获得更多细节。

# 20. 开发者工具
Spring Boot 包含了额外的工具集，可以使你的应用开发体验稍微愉快（pleasant）一点。`spring-boot-devtools` 模块可以被添加到任意项目中以提供额外的开发时特性。要包含测试工具支持，添加模块依赖到你的构建中，如下展示了 Maven 和 Gradle 的清单：

Maven：
```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<optional>true</optional>
	</dependency>
</dependencies>
```

Gradle:
```xml
configurations {
	developmentOnly
	runtimeClasspath {
		extendsFrom developmentOnly
	}
}
dependencies {
	developmentOnly("org.springframework.boot:spring-boot-devtools")
}
```

> 开发者工具在你运行完整打包的应用时自动禁用。如果你的类从 `java -jar` 启动，或者如果你从特定的类加载器开始，那么认为（considered）它是一个生产应用。如果不是这种情况（如果你的应用是从容器运行），认为排除了开发者工具或者设置了系统属性：`-Dspring.devtools.restart.enabled=false`

> 在Maven中将依赖项标记为可选的，或者在Gradle中使用定制的“只开发”配置(如上面所示)是防止DevTools被临时应用到使用您的项目的其他模块的最佳实践。

> 默认情况下重新打包不会包含开发者工具。如果你想使用某些远程开发特性，你需要禁用 `excludeDevtools` 属性以包含它。这个属性同时支持 Maven 和 Gradle 插件。

## 20.1 默认属性
一些类库通过支持使用 Spring Boot 使用缓存来提高性能（improve performance），例如：模版引擎缓存编译的模版以避免（avoid）重复（repeatedly）解析模版文件。同样，当服务静态资源时 Spring MVC  可以添加 HTTP 缓存头到响应信息中。

缓存在生产中是非常有益的（beneficial），然而它在开发环境则会适得其反（counter-productive），阻止（preventing）你看到你刚刚在应用程序中产生的更改。由于这个原因，spring-boot-devtools 默认禁用缓存选项。

缓存选项通常在你的 `application.properties` 文件里面设置。例如：Thymeleaf 提供了 `spring.thymeleaf.cache` 属性，而不用手动设置这些属性，spring-boot-devtools 模块自动合理应用开发时配置。

因为你需要更多信息关于 web 请求的信息在开发 spring mvc 和 spring WebFlux 应用时，开发者工具将会为 web 日志记录开启 debug 的日志记录。这将会给你进来的请求的信息，处理中程序，返回结果等。如果你希望记录所有请求的细节（可能包含敏感信息），你可以打开 `spring-http.log-request-detail` 配置属性。

> 如果你不想应用该默认属性你可以在你的 application.properties 中设置 spring-http.log-request-detail 为 false。

> 应用于 devtools 的所有的属性列表，查看 [DevToolsPropertyDefaultsPostProcessor.](https://github.com/spring-projects/spring-boot/tree/v2.1.6.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java)

## 20.2 自动重启
使用 spring-boot-devtools 的应用会自动重启，每当类路径下的文件改变。在 IDE 工作时，这是一个有用的特性，因为它为代码改变提供类快速的反馈循环。作为默认，指向（point to）类路径下的所有条目都会被监视为了更改。注意某些资源如：静态资源和视图模版，[不需要重新启动应用](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-restart-exclude)。

**触发重启**
当 DevTools 监视类路径下的资源，触发重启的唯一方式是更新其类路径。导致（cause）类路径更新的方式依赖于你使用的 IDE。在 Eclipse 中，保存和修改文件导致类路径更新和出发重启。在 IDEA，编译项目有同样的效果。

> 只要此分叉被打开，你可以同样启动你的应用通过使用支持的构建插件，因为 DevTools 需要一个独立的应用程序加载器来正确操作。作为默认，Gradle 和 Maven 在类路径上检测到 DevTools 时会这样做。

> 与 LiveReload 工作时自动重启工作良好，[查看 LiveReload 章节获得更多细节](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-livereload)。如果你使用 JReble，自动重启会禁用，有利于（in favor of）类的动态加载。其他 devtools 的特性如：LiveReload 和 属性覆盖可以一直使用。

> DevTools 依赖于应用程序上下文的 shutdown 钩子来在重启期间关闭它。 如果禁用了 shutdown 挂钩，则无法正常工作。

> 当决定在类路径上的条目是否应该在更改时触发重新启动时，Devztools 自动忽略名为 spring-boot, spring-boot-devtools, spring-boot-autoconfigure, spring-boot-actuator, spring-boot-starter 的项目。

> DevTools 需要通过 ApplicationContext 来定制 ResourceLoader。如果您的应用已经提供来一个，它将被包裹起来。不支持直接覆盖 ApplicationContext 上的 getResource 方法。

**重启和重新加载**
Spring Boot 程序提供的重新启动技术使用了两个类加载器。不会改变的类（例如：第三方jar）被加载到（loaded into）基类加载器中。你正在积极开发的类被加载到重启类加载器。当应用程序重启，该重启类加载器会被丢掉（thrown away）并重新创建一个新的。这种方法意味着应用程序重启通常比“冷启动”快得多，因为基类装入器已经可用并已填充。

如果发现重新启动对应用程序来说不够快，或者遇到类加载问题。你可以考虑重新选择技术如从 ZeroTurnaround 获得 JReble。这些工作是通过在加载类时重写类来完成的，以使它们更易于重新加载。

### 20.2.1. 在状态评估（condition evaluation）中记录变化
作为默认，每当你的应用重启，将记录显示状态评估增量的报表。该报告展示了你的应用的自动配置的改变如增加或删除bean，设置配置属性。

要禁用日志记录报告，设置以下属性：

	spring.devtools.restart.log-condition-evaluation-delta=false

### 20.2.2. 排除资源
某些资源当他们改变时没有必要触发重启。如：Thymeleaf 模版可以就地（in-place）编辑，默认情况下，改变 /META-INF/maven, /META-INF/resources, /resources, /static, /public, or /templates 中的资源不会触发重启但会触发 [live reload](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-livereload)。 如果你想定制这些排除项，你可以使用 `spring.devtools.restart.exclude` 属性。如：要仅仅排除 `/static` 和 `/public` 你需要设置以下命令：

	spring.devtools.restart.exclude=static/**,public/**

> 如果你要保持默认值并添加额外的排除项，使用 `spring.devtools.restart.additional-exclude` 作为替换。

### 20.2.3. 监视额外的路径
你可能想要你的应用程序重启或重加载当你不在类路径下改变文件。要这样做，使用 `spring.devtools.restart.additional-paths` 属性配置额外的路径并监视。前面描述的是控制在额外路径下的更改是否会触发完全重新启动或重新加载。

### 20.2.4. 禁用重启
如果你不想使用重启特性，你可以通过 `spring.devtools.restart.enabled` 属性禁用它。大多数情况下，你可以在你的 `application.properties` 设置这个属性。（这样做仍然初始化时重启类加载器，但是他不会监视文件更改）

如果你想要完全禁用重启支持（例如：他在特定的类库中不能工作），你需要在调用 `SpringApplication.run(…​),` 之前设置 `spring.devtools.restart.enabled` 系统属性为 false，如下所示：

```Java
public static void main(String[] args) {
	System.setProperty("spring.devtools.restart.enabled", "false");
	SpringApplication.run(MyApp.class, args);
}
```

### 20.2.5. 使用触发文件
如果你工作的 IDE 不断的（continuouslt）编译改变文件，你可能希望仅在特定时间内触发重启。要这样做，你可以使用“触发文件”，这是一个特殊的文件，当您想要实际触发重新启动检查时，必须修改该文件。更改文件只会触发检查，只有在 Devtools 检测到必须执行某些操作时才会重新启动。

使用触发文件，设置 `spring.devtools.restart.trigger-file` 属性为触发文件的路径。

> 你可能想要设置 spring.devtools.restart.trigger-file 作为一个全局设置，这样所有的项目都以同样的方式运作。

### 20.2.6. 定制重启类加载器
如在前面的“重启和重加载”章节所述，重启功能是使用两个类加载器实现的。对于更多的应用，这种方法（approack）工作良好。然而，它有时会导致一些类加载问题。

作为默认，你的 IDE 中任何打开的项目都加载类“重启”类加载器，任何普通的（regular）的 jar 文件都带有“基础”类加载器。如果你在多模块项目中工作，并且不是每个项目都导入到了 IDE，你可能需要定制一些东西。要这样做的话，你可以创建一个 `META-INF/spring-devtools.properties` 文件。

该 ` spring-devtools.properties`  文件可以包含有 `restart.exclude` 和 `restart.include` 前缀的属性。include 元素下的项都会被拉取（pulled up）到 “重启” 类加载器，exclude 元素下的项都被推进到（pushed down）“基础”类加载器。该属性值是应用在类路径下的正则模式，如下所示：

```yml
restart.exclude.companycommonlibs=/mycorp-common-[\\w\\d-\.]+\.jar
restart.include.projectcommon=/mycorp-myproj-[\\w\\d-\.]+\.jar
```

> 所有的属性关键字都是必须的。只要（as long as）属性以 `restart.include` 或 `resatrt.exclude` 开头都被考虑进去。

> 加载类路径中的所有 META-INF/Spring-devtools.properties。您可以在项目中或项目所消耗的库中打包文件。

### 20.2.7. 已知限制
重启功能（functionality）不适用使用标准 `ObjectInputStream` 反序列化的对象。如果你需要反序列化对象，你可能需要使用 Spring 的 ConfigurableObjectInputStream 结合于（in combination with）`Thread.currentThread().getContextClassLoader()`。

不幸的是（Unfortunately），一些第三方类库在不考虑类加载器上下文的情况下反序列化。如果你发现一些问题，你需要请求原作者解决。

## 20.3 热加载
Spring Boot Devtools 模块包括一个内嵌的 LiverLoad 服务器，当资源被改变时，它可以用来触发浏览器刷新。livereload.com 免费提供 LiveReload 浏览器插件 Chrome、Firefox，Safari版。

如果你想当你的应用启动时启动 LiveReload，你可以设置 `spring.devtools.livereload.enabled` 属性为 false。

> 一次（at a time）只能运行一个LiveReload服务器。在你的应用启动之前，确保没有其他的 LiveReload 服务器在运行。如果你从你的 IDE 启动了多个应用程序，只有第一个 LiveReload 会提供支持。

## 20.4 全局设置
你可以通过在你的 `$HOME` 文件夹下添加一个名为 `.spring-boot-devtools.properties` 的文件来配置开发工具的全局设置（注意文件名从 . 开始）。添加到这个文件的所有属性会应用到所有的 Spring Boot 应用程序，在你的机器上使用开发工具。如：要配置永远使用 触发文件 重启，你需要添加以下属性：

**~/.spring-boot-devtools.properties.**

	spring.devtools.reload.trigger-file=.reloadtrigger

> 在.spring-boot-devtools.properties中激活的配置文件不会影响（affect）[特定于配置文件](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties)的加载。

## 20.5 远程应用
Spring Boot 开发者工具没有限制于本地开发，你同样可以在运行的远程应用上使用一些特性功能。远程支持是可选的，要开启它，你需要确保 devtools 包含在重新打包后的归档文件中，如下列表所示：

```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
			<configuration>
				<excludeDevtools>false</excludeDevtools>
			</configuration>
		</plugin>
	</plugins>
</build>
```

如果你需要设置 spring.devtools.remote.secret 属性，如下所示：

	spring.devtools.remote.secret=mysecret

> 在远程应用开启 spring-boot-devtools 是有安全风险的（risk）。你应该永远都不开启对生产环境的支持。

远程开发工具提供以下两个单元的支持：一个服务器断点，接受在你的 IDE 中运行的应用和连接。当 spring.devtools.remote.secret 属性被设置了该服务组件会自动开启。客户端组件必须手动运行。

### 20.5.1 运行远程应用客户端
该远程客户端应用被设计为在你的 IDE 中运行。你需要运行 `org.springframework.boot.devtools.RemoteSpringApplication` 使用和你连接的远程个项目相同的类路径。该应用程序所需的唯一参数是需要连接到的远程服务器的 URL。

如，如果你使用 Eclipse 或 STS，并且你有一个名为 my-app 的项目被部署到了云服务器，你可这样做：

- 从 Run  菜单构建 Run Configurations...
- 创建一个新的 Java Application 启动配置
- 浏览 my-app 应用
- 使用 org.springframework.boot.devtools.RemoteSpringApplication 作为主类
- 添加 https://myapp.cfapps.io 到 程序参数。（或者不管您的远程URL是什么）

正在运行的远程客户端可能类似于下列列表：

	.   ____          _                                              __ _ _
	/\\ / ___'_ __ _ _(_)_ __  __ _          ___               _      \ \ \ \
	( ( )\___ | '_ | '_| | '_ \/ _` |        | _ \___ _ __  ___| |_ ___ \ \ \ \
	\\/  ___)| |_)| | | | | || (_| []::::::[]   / -_) '  \/ _ \  _/ -_) ) ) ) )
	'  |____| .__|_| |_|_| |_\__, |        |_|_\___|_|_|_\___/\__\___|/ / / /
	=========|_|==============|___/===================================/_/_/_/
	:: Spring Boot Remote :: 2.1.6.RELEASE

	2015-06-10 18:25:06.632  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Starting RemoteSpringApplication on pwmbp with PID 14938 (/Users/pwebb/projects/spring-boot/code/spring-boot-devtools/target/classes started by pwebb in /Users/pwebb/projects/spring-boot/code/spring-boot-samples/spring-boot-sample-devtools)
	2015-06-10 18:25:06.671  INFO 14938 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@2a17b7b6: startup date [Wed Jun 10 18:25:06 PDT 2015]; root of context hierarchy
	2015-06-10 18:25:07.043  WARN 14938 --- [           main] o.s.b.d.r.c.RemoteClientConfiguration    : The connection to http://localhost:8080 is insecure. You should use a URL starting with 'https://'.
	2015-06-10 18:25:07.074  INFO 14938 --- [           main] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
	2015-06-10 18:25:07.130  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Started RemoteSpringApplication in 0.74 seconds (JVM running for 1.105)

> 因为远程客户端使用与实际应用程序相同的类路径，所以它可以直接的读取你的应用配置 。这是Spring.devtools.remote.secret属性的读取和传递到服务器进行身份验证的方式。

> 总是建议使用 https:// 作为连接协议，因此，通信是加密的（traffic is encrypted），密码不能被截获（intercepted）。

> 如果你使用代理访问远程应用，配置 spring.devtools.remote.proxy.host 和 spring.devtools.remote.proxy.port 属性。

### 20.5.2 远程更新
远程客户端以与本地重新启动相同的方式监视应用程序类路径以进行更改。任何更新的资源被推到远程应用程序，（如果需要的话）触发重新启动。如果你需要迭代本地没有的云服务功能，这样十分有用。远程更新和重新启动要比完整的（full）重建和部署周期快得多（quicker than）。

> 只有当远程客户端在运行时才会监视文件，如果你在远程客户端其中之前改变文件，它不会推送到远程服务器。

# 21. 为生产环境打包你的应用
可执行 jar 可用于生产部署，因为他们是独立的（self-contained），它们也非常适合（ideally suited）基于云的部署。

如需要额外的“生产准备”特性，例如健康，升级，和度量 Rest 或者 JMX 端点，考虑添加 spring-boot-actuator。查看 [第四章 Spring Boot 监控：生产可读的特性 ](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/production-ready.html) 获得更多细节。

# 22. 下一步是什么
你现在应该理解如何使用 Spring Boot 和一些遵循的最佳实践。现在可以深入学习特定的 Spring Boot 特性，或者你可以跳过前面（ahead），阅读关于 “生产可读” 各方面的 Spring Boot。
