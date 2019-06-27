---
title: 20190608 spring-boot | part2 - 11,12
date: 2019-06-08
tag: spring-boot
category:
- english-learning
- spring-boot
thumbnail: http://img.yuzh.xyz/blog/94.jpg
toc: true
---

> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#getting-started-first-application

<h1 style="color:green; text-align:center;">Part II. Getting Started</h1>

<!-- TOC -->

- [11. Developing Your First Spring Boot Application](#11-developing-your-first-spring-boot-application)
	- [11.1 Creating the POM](#111-creating-the-pom)
	- [11.2 Adding Classpath Dependencies](#112-adding-classpath-dependencies)
	- [11.3 Writing the Code](#113-writing-the-code)
		- [11.3.1 The @RestController and @RequestMapping Annotations](#1131-the-restcontroller-and-requestmapping-annotations)
		- [11.3.2 The @EnableAutoConfiguration Annotation](#1132-the-enableautoconfiguration-annotation)
		- [11.3.3 The “main” Method](#1133-the-main-method)
	- [11.4 Running the Example](#114-running-the-example)
	- [11.5 Creating an Executable Jar](#115-creating-an-executable-jar)
- [12. What to Read Next](#12-what-to-read-next)
- [11 开发你的第一个 Spring Boot 应用](#11-%E5%BC%80%E5%8F%91%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA-%08spring-boot-%E5%BA%94%E7%94%A8)
	- [11.1 创建 pom](#111-%E5%88%9B%E5%BB%BA-pom)
	- [11.2 添加 ClassPath 依赖项](#112-%E6%B7%BB%E5%8A%A0-classpath-%E4%BE%9D%E8%B5%96%E9%A1%B9)
	- [11.3 编写代码](#113-%E7%BC%96%E5%86%99%E4%BB%A3%E7%A0%81)
		- [11.3.1 @RestController 和 @RequestMapping 注解](#1131-restcontroller-%E5%92%8C-requestmapping-%E6%B3%A8%E8%A7%A3)
		- [11.3.2 @EnableAutoConfiguration 注解](#1132-enableautoconfiguration-%E6%B3%A8%E8%A7%A3)
		- [11.3.3 main 方法](#1133-main-%E6%96%B9%E6%B3%95)
	- [11.4 运行案例](#114-%E8%BF%90%E8%A1%8C%E6%A1%88%E4%BE%8B)
	- [11.5 创建可执行 jar](#115-%E5%88%9B%E5%BB%BA%E5%8F%AF%E6%89%A7%E8%A1%8C-jar)
- [接下来要阅读的内容](#%E6%8E%A5%E4%B8%8B%E6%9D%A5%E8%A6%81%E9%98%85%E8%AF%BB%E7%9A%84%E5%86%85%E5%AE%B9)

<!-- /TOC -->
<!-- more -->
# 11. Developing Your First Spring Boot Application
This section describes how to develop a simple “Hello World!” web application that highlights some of Spring Boot’s key features. We use Maven to build this project, since most IDEs support it.

> The `spring.io` web site contains many “Getting Started” [guides] that use Spring Boot. If you need to solve a specific problem, check there first.
\
You can shortcut the steps below by going to `start.spring.io` and choosing the "Web" starter from the dependencies searcher. Doing so generates a new project structure so that you can `start coding right away`. Check the `Spring Initializr documentation` for more details.

Before we begin, open a terminal and run the following commands to ensure that you have valid versions of Java and Maven installed:

```
$ java -version
java version "1.8.0_102"
Java(TM) SE Runtime Environment (build 1.8.0_102-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.102-b14, mixed mode)
```

```
$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T14:33:14-04:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_102, vendor: Oracle Corporation
```

> This sample needs to be created in its own folder. Subsequent instructions assume that you have created a suitable folder and that it is your current directory.


## 11.1 Creating the POM
We need to start by creating a Maven `pom.xml` file. The `pom.xml` is the recipe that is used to build your project. Open your favorite text editor and add the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>myproject</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.5.RELEASE</version>
	</parent>

	<!-- Additional lines to be added here... -->

</project>
```

The preceding listing should give you a working build. You can test it by running `mvn package` (for now, you can ignore the “jar will be empty - no content was marked for inclusion!” warning).

> At this point, you could import the project into an IDE (most modern Java IDEs include built-in support for Maven). For simplicity, we continue to use a plain text editor for this example.

## 11.2 Adding Classpath Dependencies
Spring Boot provides a number of “Starters” that let you add jars to your classpath. Our sample application has already used `spring-boot-starter-parent` in the `parent` section of the POM. The `spring-boot-starter-parent` is a special starter that provides useful Maven defaults. It also provides a [dependency-management] section so that you can omit `version` tags for “blessed” dependencies.

Other “Starters” provide dependencies that you are likely to need when developing a specific type of application. Since we are developing a web application, we add a `spring-boot-starter-web` dependency. Before that, we can look at what we currently have by running the following command:

```
$ mvn dependency:tree

[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT
```

The `mvn dependency:tree` command prints a tree representation of your project dependencies. You can see that `spring-boot-starter-parent` provides no dependencies by itself. To add the necessary dependencies, edit your `pom.xml` and add the spring-boot-starter-web dependency immediately below the `parent` section:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>
```

If you run `mvn dependency:tree` again, you see that there are now a number of additional dependencies, including the Tomcat web server and Spring Boot itself.

## 11.3 Writing the Code
To finish our application, we need to create a single Java file. By default, Maven compiles sources from `src/main/java`, so you need to create that folder structure and then add a file named `src/main/java/Example.java` to contain the following code:


```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

	@RequestMapping("/")
	String home() {
		return "Hello World!";
	}

	public static void main(String[] args) {
		SpringApplication.run(Example.class, args);
	}

}
```

Although there is not much code here, quite a lot is going on. We step through the important parts in the next few sections.

### 11.3.1 The @RestController and @RequestMapping Annotations

The first annotation on our `Example` class is `@RestController`. This is known as a stereotype annotation. It provides hints for people reading the code and for Spring that the class plays a specific role. In this case, our class is a web `@Controller`, so Spring considers it when handling incoming web requests.

The `@RequestMapping` annotation provides “routing” information. It tells Spring that any HTTP request with the `/` path should be mapped to the `home` method. The `@RestController` annotation tells Spring to render the resulting string directly back to the caller.

> The `@RestController` and `@RequestMapping` annotations are Spring MVC annotations. (They are not specific to Spring Boot.) See the MVC section in the Spring Reference Documentation for more details.

### 11.3.2 The @EnableAutoConfiguration Annotation

The second class-level annotation is `@EnableAutoConfiguration`. This annotation tells Spring Boot to “guess” how you want to configure Spring, based on the jar dependencies that you have added. Since `spring-boot-starter-web` added Tomcat and Spring MVC, the auto-configuration assumes that you are developing a web application and sets up Spring accordingly.

> **Starters and Auto-configuration**
\
Auto-configuration is designed to work well with “Starters”, but the two concepts are not directly tied. You are free to pick and choose jar dependencies outside of the starters. Spring Boot still does its best to auto-configure your application.

### 11.3.3 The “main” Method

The final part of our application is the `main` method. This is just a standard method that follows the Java convention for an application entry point. Our main method delegates to Spring Boot’s `SpringApplication` class by calling `run`. `SpringApplication` bootstraps our application, starting Spring, which, in turn, starts the auto-configured Tomcat web server. We need to pass `Example.class` as an argument to the `run` method to tell `SpringApplication` which is the primary Spring component. The `args` array is also passed through to expose any command-line arguments.

## 11.4 Running the Example
At this point, your application should work. Since you used the spring-boot-starter-parent POM, you have a useful run goal that you can use to start the application. Type `mvn spring-boot:run` from the root project directory to start the application. You should see output similar to the following:

```
$ mvn spring-boot:run

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.1.5.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
```

If you open a web browser to localhost:8080, you should see the following output:

```
Hello World!
```

To gracefully exit the application, press `ctrl-c.`

## 11.5 Creating an Executable Jar
We finish our example by creating a completely self-contained executable jar file that we could run in production. Executable jars (sometimes called “fat jars”) are archives containing your compiled classes along with all of the jar dependencies that your code needs to run.

>**Executable jars and Java**
\
Java does not provide a standard way to load nested jar files (jar files that are themselves contained within a jar). This can be problematic if you are looking to distribute a self-contained application.
\
To solve this problem, many developers use “uber” jars. An uber jar packages all the classes from all the application’s dependencies into a single archive. The problem with this approach is that it becomes hard to see which libraries are in your application. It can also be problematic if the same filename is used (but with different content) in multiple jars.
\
Spring Boot takes a different approach and lets you actually nest jars directly.


To create an executable jar, we need to add the `spring-boot-maven-plugin` to our `pom.xml`. To do so, insert the following lines just below the `dependencies` section:

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

> The spring-boot-starter-parent POM includes `<executions>` configuration to bind the `repackage` goal. If you do not use the parent POM, you need to declare this configuration yourself. See the [plugin documentation] for details.

Save your `pom.xml` and run `mvn package` from the command line, as follows:

```xml
$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.1.5.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

If you look in the `target` directory, you should see `myproject-0.0.1-SNAPSHOT.jar`. The file should be around 10 MB in size. If you want to peek inside, you can use `jar tvf`, as follows:

```
$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar
```

You should also see a much smaller file named `myproject-0.0.1-SNAPSHOT.jar.original` in the `target` directory. This is the original jar file that Maven created before it was repackaged by Spring Boot.

To run that application, use the `java -jar` command, as follows:

```
$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.1.5.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.536 seconds (JVM running for 2.864)
```

As before, to exit the application, press ctrl-c.

# 12. What to Read Next
Hopefully, this section provided some of the Spring Boot basics and got you on your way to writing your own applications. If you are a task-oriented type of developer, you might want to jump over to [spring.io] and check out some of the [getting started] guides that solve specific “How do I do that with Spring?” problems. We also have Spring Boot-specific “How-to” reference documentation.

The [Spring Boot repository] also has a [bunch of samples] you can run. The samples are independent of the rest of the code (that is, you do not need to build the rest to run or use the samples).

Otherwise, the next logical step is to read [Part III, “Using Spring Boot”]. If you are really impatient, you could also jump ahead and read about [Spring Boot features.]

---
# 11 开发你的第一个 Spring Boot 应用
这一章节描述了如何开发一个简单的“hello world！”web应用，以重点介绍Spring Boot的一些主要功能。我们使用 Maven 构建这个项目，因为（since）大多数 IDE 都支持它。

> 这个 spring.io 站点包含了一些使用 Spring Boot 的“快速开始”指南。如果你要解决（solve）一个具体（specific）的问题，首先点击这里。
> 您可以通过转到start.spring.io并从依赖关系搜索器中选择“Web”启动器来快捷执行（shortcut the steps）以下步骤。这样做会生成一个新的项目结构，以便（so that）您可以立即（right away）开始编码。点击 Spring Initializr 文档查看更多细节。

在开始之前，打开终端运行以下命令确保你安装的 Java 和 Maven 是有效的版本：

```sh
$ java -version
java version "1.8.0_102"
Java(TM) SE Runtime Environment (build 1.8.0_102-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.102-b14, mixed mode)
```

```sh
$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T14:33:14-04:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_102, vendor: Oracle Corporation
```

> 这个案例需要在自己的目录中创建。随后（subsequent）的指南假定（assume）你已经创建了合适（suitable）的目录并且是你的当前文件夹。

## 11.1 创建 pom
我们需要从创建 Maven 的 `pom.xml` 文件开始，这个 pom.xml 是用于（use to）构建你的项目的配方（recipe）。打开你喜欢的文本编辑器添加以下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>myproject</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.5.RELEASE</version>
	</parent>

	<!-- 这里还会额外添加其他行... -->

</project>
```

前面的列表应该可以给你有效（a working）的构建。你可以通过 `mvn package` 测试它（现在，你可以忽略“jar will be empty - no content was marked for inclusion!”警告）

> 在此时（At this point），你可以导入这个项目到你的 IDE（大多数现代Java IDE都包含对Maven的内置支持）。为了简单（simplicy）起见，我们继续为此示例使用纯文本编辑器。

## 11.2 添加 ClassPath 依赖项
Spring Boot 添加了许多（a number of）“启动器” 允许你添加 jars 到你的类路径下。我们的示例应用程序已经在POM的父节中使用了spring-boot-starter-parent。`spring-boot-starters-parent` 是一个特殊的启动器，它提供了可用的 maven 默认配置。它同样提供一个 `dependency-management` 节点以便（so that）你可以省略（omit）`version` “blessed”依赖项的版本标签。

其他“启动器”提供了你在开发特定类型应用时或许（likely）需要的依赖项。当（since）我们正在开发Web应用程序，我们添加 `spring-boot-starter-web` 依赖。在此之前，我们可以通过运行以下命令来查看（look at）当前的内容：

```sh
$ mvn dependency:tree

[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT
```

该 `mvn dependency:tree` 命令打印输来表示（representation）你项目依赖。您可以看到 `spring-boot-starter-parent` 本身（itself）不提供依赖关系。要添加必要（necessary）的依赖，编辑你的 pom.xml， 添加 `spring-boot-starters-web` 依赖紧接（immediately）与 `parent` 节点之下（below）。

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>
```

如果你再次运行 `mvn dependency:tree`，你会看到这里有多个额外的依赖项，包含来 Tomcat Web 服务器和 Spring Boot 本身。

## 11.3 编写代码
为了完成我们的项目，我们需要创建一个单个java文件。默认情况下（by default），maven 编译的资源来源自 `src/main/java`，所以你需要创建这个目录结构然后添加名字为 `src/main/java/Example.java` 文件，包含以下代码：

```Java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

	@RequestMapping("/")
	String home() {
		return "Hello World!";
	}

	public static void main(String[] args) {
		SpringApplication.run(Example.class, args);
	}

}
```

虽然（Although）这里的代码并不多，但是很多（quite a lot）事情在发生（is going on）。我们将在接下来的（next few）几节中逐步介绍重要部分（important part）。

### 11.3.1 @RestController 和 @RequestMapping 注解
在我们的 Example 类上第一注解是 `@RestController`，这被称为（known as）构造型注解。它为阅读代码的人提供了提示（hints），而为Spring提供了特定角色的提示。在这个用例，我们的类是一个web `@Controller`，所以Spring在处理传入的Web请求时会考虑（considers）它。

这个 `@RequestMapping` 注解提供了 “路由” 信息，它告诉 Spring 任何的 `/` 路径的 Http 请求都将映射到 `home` 方法。该 `@RestController` 注解告诉 Spring 将结果字符串直接（directly）渲染回调用者。

> `@RequestMapping` 和 `@RestController` 注解是 Spring MVC 注解。（他们不是 Spring Boot 特有的），更多详情请查看 Spring 参考文档的 [MVC 章节](https://docs.spring.io/spring/docs/5.1.7.RELEASE/spring-framework-reference/web.html#mvc)

### 11.3.2 @EnableAutoConfiguration 注解
第二个类级别的注解是 `@EnableAutoConfiguration`，该注解告诉 Spring Boot “猜测”你想如何配置 Spring，这都基于您添加的jar依赖项。由于 `spring-boot-startes-web` 添加了 Tomcat 和 Spring MVC，这个自动配置假定（assumes）你正在开发web应用，于是（accordingly）相应的设置好Spring。

> 启动器和自动配置
> 自动配置被设计为让启动器更好的工作，但是这两个概念（concept）并没有联合在一起（directly tied）。你可以挑选（pick）和选择（choose）启动器之外的 jar 依赖。Spring Boot 仍然尽力最好的自动配置你的应用。

### 11.3.3 main 方法
最后一个单元是我们应用的 main 方法，这是一个遵循 java 惯例（convertion）的标准方法，是应用的入口点（entry point）。我们的主方法通过调用 `run` 来委托（delegates 代表、委托）spring boot 的 `SpringApplication`， `SpringApplication` 引导我们的应用启动 Spring，自动配置 Tomcat web 服务器。我们需要传递（pass） `Example.class` 作为（as an）一个参数给 `run` 方法，以便告诉 `SpringApplication` 这是主要的Spring组件。该 `args` 参数数组同样被传递到暴露的任何命令行参数中。

## 11.4 运行案例
在此时，你的应用可以工作。当你使用 `spring-boot-starter-parent` POM 文件时，你有一个可用的 `run` 目标 （goals），可用于启动应用。从项目根目录输入 `mvn spring-boot:run` 以启动该应用。你可以看到类似以下的输出：

```sh
$ mvn spring-boot:run

 :: Spring Boot ::  (v2.1.5.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
```

如果你在浏览器打开 localhost:8080，你可以看到以下输出：

```
Hello World!
```

要优雅的（gracefully）退出该应用，按下 `ctrl - c`

## 11.5 创建可执行 jar
通过创建一个完全独立的可执行 jar 文件完成我们的案例，他们可以在生产环境下运行。可执行 jar 是一个包含你的所有编译后的类文件和所有代码运行所需要的 jar 依赖的归档。

> **可执行 jar 和 java**
java 没有提供标准的方式去加载嵌套的 jar 文件（java 文件本身(themsevles)在 jar 里面(within)）。如果你要分发自包含的应用，将会造成一些问题（problematic）。
\
要解决（solve）这个问题，大多数开发者使用“uber” jar。一个 uber jar 从所有应用的依赖项中的所有字节码文件打包到一个单独的归档中。这种方法（approach）的问题在于：查看哪一个类库在你的应用中变得困难（become hard）。如果在多个 jars 中使用相同的文件名（但是内容不同）同样也会造成问题。
\
Spring Boot 用不同的方法，让你直接嵌套 jars

要创建一个可执行 jar，我们需要添加 `spring-boot-maven-plugin` 到你的 `pom.xml`。这样做，插入以下行紧接着 `denpendency` 节点：

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

> 该 `spring-boot-maven-plugin` POM 包含了 `<excutions>` 配置绑定到 `repackage` 目标。如果你不使用父 POM，你需要定义你自己的这个配置项。查看 [插件文档](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/maven-plugin/usage.html) 获得更多详情。

保存你的 `pom.xml` 并从命令行运行 `mvn package`，如下：

```sh
$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.1.5.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

如果你查看 target 目录，你会看到 `myproject-0.0.1-SNAPSHOT.jar`。该文件大小应该为 10M。如果你想要偷看里面（peek inside），你可以使用 `jar tvf`，如下：

```sh
jar tvf target/myproject-0.0.1-SNAPSHOT.jar
```

你同样会在 target 目录下看到大量类似名字为 `myproject-0.0.1-SNAPSHOT.jar.original` 的文件。这是Maven在Spring Boot重新打包之前创建的原始jar文件。

要运行该应用，使用 `java -jar` 命令，如下：

```sh
$ java -jar target/myproject-0.0.1-SNAPSHOT.jar
```

像上次一样，退出应用请按 ctrl - c。

# 接下来要阅读的内容
希望，这个章节提供了一些 Spring Boot 的基础知识能让你开始编写自己的应用。如果您是面向任务的开发人员，你可能想要跳到（jump over） spring.io，查看（check out）一些入门指南，解决具体的“如何使用Spring？”问题。 我们同样有 Spring Boot具体的“如何使用”参考文档。

这个 spring boot 存储库同样有一堆（a bunch of）你可以运行的样本。这些样本独立于（independent of）其余（rest of）的代码。（你不需要构建其余的来运行或使用样本）

总之，下一个合乎逻辑的步骤（logical step）是阅读第III部分“使用Spring Boot”。如果你真的很不耐烦，你也可以跳过去阅读 [Spring Boot功能](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#boot-features)。
