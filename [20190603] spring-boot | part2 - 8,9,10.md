---
title: 20190603 spring-boot | part2 - 8,9,10
date: 2019-06-03
tag: spring-boot
category:
- english-learning
- spring-boot
thumbnail: http://img.yuzh.xyz/blog/89.jpg
toc: true
---

> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#getting-started

<h1 style="color:green; text-align:center;">Part II. Getting Started</h1>

<!-- TOC -->

- [8. Introducing Spring Boot](#8-introducing-spring-boot)
- [9. System Requirements](#9-system-requirements)
	- [9.1 Servlet Containers](#91-servlet-containers)
- [10. Installing Spring Boot](#10-installing-spring-boot)
	- [10.1 Installation Instructions for the Java Developer](#101-installation-instructions-for-the-java-developer)
		- [10.1.1 Maven Installation](#1011-maven-installation)
		- [10.1.2 Gradle Installation](#1012-gradle-installation)
	- [10.2 Installing the Spring Boot CLI](#102-installing-the-spring-boot-cli)
		- [10.2.1 Manual Installation](#1021-manual-installation)
		- [10.2.2 Installation with SDKMAN!](#1022-installation-with-sdkman)
		- [10.2.3 OSX Homebrew Installation](#1023-osx-homebrew-installation)
		- [10.2.4 MacPorts Installation](#1024-macports-installation)
		- [10.2.5 Command-line Completion](#1025-command-line-completion)
		- [10.2.6 Windows Scoop Installation](#1026-windows-scoop-installation)
		- [10.2.7 Quick-start Spring CLI Example](#1027-quick-start-spring-cli-example)
		- [10.3 Upgrading from an Earlier Version of Spring Boot](#103-upgrading-from-an-earlier-version-of-spring-boot)
- [8. spring boot 介绍](#8-%08spring-boot-%E4%BB%8B%E7%BB%8D)
- [9. 系统要求](#9-%E7%B3%BB%E7%BB%9F%E8%A6%81%E6%B1%82)
	- [9.1 Servlet 容器](#91-%08servlet-%E5%AE%B9%E5%99%A8)
- [10. 安装 spring boot](#10-%E5%AE%89%E8%A3%85-spring-boot)
	- [10.1 java 开发者的安装介绍](#101-java-%E5%BC%80%E5%8F%91%E8%80%85%E7%9A%84%E5%AE%89%E8%A3%85%E4%BB%8B%E7%BB%8D)
		- [10.1.1 Maven 安装](#1011-maven-%E5%AE%89%E8%A3%85)
		- [10.1.2 继承 Gradle](#1012-%E7%BB%A7%E6%89%BF-gradle)
	- [10.2 安装 Spring Boot CLI（命令行工具）](#102-%E5%AE%89%E8%A3%85-spring-boot-cli%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7)
		- [10.2.1 手动安装](#1021-%E6%89%8B%E5%8A%A8%E5%AE%89%E8%A3%85)
		- [10.2.2  SDKMAN 安装](#1022--sdkman-%E5%AE%89%E8%A3%85)
		- [10.2.3 OSX Homebrew 安装](#1023-osx-homebrew-%E5%AE%89%E8%A3%85)
		- [10.2.4 MacPorts 安装](#1024-macports-%E5%AE%89%E8%A3%85)
		- [10.2.5 命令行编译](#1025-%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%BC%96%E8%AF%91)
		- [10.2.6 Windows Scoop 安装](#1026-windows-scoop-%E5%AE%89%E8%A3%85)
		- [10.2.7 Spring CLI 案例快速开始](#1027-spring-cli-%E6%A1%88%E4%BE%8B%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)
	- [10.3 从 SpringBoot 的早期（Earlier）版本升级](#103-%E4%BB%8E-springboot-%E7%9A%84%E6%97%A9%E6%9C%9Fearlier%E7%89%88%E6%9C%AC%E5%8D%87%E7%BA%A7)

<!-- /TOC -->
<!-- more -->

If you are getting started with Spring Boot, or “Spring” in general, start by reading this section. It answers the basic “what?”, “how?” and “why?” questions. It includes an introduction to Spring Boot, along with installation instructions. We then walk you through building your first Spring Boot application, discussing some core principles as we go.

# 8. Introducing Spring Boot
Spring Boot makes it easy to create stand-alone, production-grade Spring-based Applications that you can run. We take an opinionated view of the Spring platform and third-party libraries, so that you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

You can use Spring Boot to create Java applications that can be started by using java -jar or more traditional war deployments. We also provide a command line tool that runs “spring scripts”.

Our primary goals are:

- Provide a radically faster and widely accessible getting-started experience for all Spring development.
- Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
- Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
- Absolutely no code generation and no requirement for XML configuration.

# 9. System Requirements
Spring Boot 2.1.5.RELEASE requires Java 8 and is compatible up to Java 11 (included). Spring Framework 5.1.7.RELEASE or above is also required.

Explicit build support is provided for the following build tools:

Build Tool | Version
-----------|--------
Maven      | 3.3+
Gradle     | 4.4+

## 9.1 Servlet Containers
Spring Boot supports the following embedded servlet containers:

Name         | Servlet Version
-------------|----------------
Tomcat 9.0   | 4.0
Jetty 9.4    | 3.1
Undertow 2.0 | 4.0

You can also deploy Spring Boot applications to any Servlet 3.1+ compatible container.

# 10. Installing Spring Boot
Spring Boot can be used with “classic” Java development tools or installed as a command line tool. Either way, you need Java SDK v1.8 or higher. Before you begin, you should check your current Java installation by using the following command:

```
$ java -version
```

If you are new to Java development or if you want to experiment with Spring Boot, you might want to try the Spring Boot CLI (Command Line Interface) first. Otherwise, read on for “classic” installation instructions.


## 10.1 Installation Instructions for the Java Developer
You can use Spring Boot in the same way as any standard Java library. To do so, include the appropriate spring-boot-*.jar files on your classpath. Spring Boot does not require any special tools integration, so you can use any IDE or text editor. Also, there is nothing special about a Spring Boot application, so you can run and debug a Spring Boot application as you would any other Java program.

Although you could copy Spring Boot jars, we generally recommend that you use a build tool that supports dependency management (such as Maven or Gradle).

### 10.1.1 Maven Installation

Spring Boot is compatible with Apache Maven 3.3 or above. If you do not already have Maven installed, you can follow the instructions at maven.apache.org.

> On many operating systems, Maven can be installed with a package manager. If you use OSX Homebrew, try `brew install maven`. Ubuntu users can run `sudo apt-get install maven`. Windows users with Chocolatey can run `choco install maven `from an elevated (administrator) prompt.


Spring Boot dependencies use the `org.springframework.boot` `groupId`. Typically, your Maven POM file inherits from the `spring-boot-starter-parent` project and declares dependencies to one or more [“Starters”]. Spring Boot also provides an optional [Maven plugin] to create executable jars.

The following listing shows a typical `pom.xml` file:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>myproject</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<!-- Inherit defaults from Spring Boot -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.5.RELEASE</version>
	</parent>

	<!-- Add typical dependencies for a web application -->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<!-- Package as an executable jar -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```

> The `spring-boot-starter-parent` is a great way to use Spring Boot, but it might not be suitable all of the time. Sometimes you may need to inherit from a different parent POM, or you might not like our default settings. In those cases, see Section 13.2.2, [“Using Spring Boot without the Parent POM”] for an alternative solution that uses an `import` scope.

### 10.1.2 Gradle Installation

Spring Boot is compatible with Gradle 4.4 and later. If you do not already have Gradle installed, you can follow the instructions at gradle.org.

Spring Boot dependencies can be declared by using the `org.springframework.boot` `group`. Typically, your project declares dependencies to one or more “Starters”. Spring Boot provides a useful Gradle plugin that can be used to simplify dependency declarations and to create executable jars.


```
Gradle Wrapper

The Gradle Wrapper provides a nice way of “obtaining” Gradle when you need to build a project. It is a small script and library that you commit alongside your code to bootstrap the build process. See docs.gradle.org/4.2.1/userguide/gradle_wrapper.html for details.
```

More details on getting started with Spring Boot and Gradle can be found in the Getting Started section of the Gradle plugin’s reference guide.

## 10.2 Installing the Spring Boot CLI
The Spring Boot CLI (Command Line Interface) is a command line tool that you can use to quickly prototype with Spring. It lets you run [Groovy] scripts, which means that you have a familiar Java-like syntax without so much boilerplate code.

You do not need to use the CLI to work with Spring Boot, but it is definitely the quickest way to get a Spring application off the ground.

### 10.2.1 Manual Installation

You can download the Spring CLI distribution from the Spring software repository:

- spring-boot-cli-2.1.5.RELEASE-bin.zip
- spring-boot-cli-2.1.5.RELEASE-bin.tar.gz

Cutting edge snapshot distributions are also available.

Once downloaded, follow the INSTALL.txt instructions from the unpacked archive. In summary, there is a `spring` script (`spring.bat` for Windows) in a `bin/` directory in the `.zip` file. Alternatively, you can use `java -jar` with the `.jar` file (the script helps you to be sure that the classpath is set correctly).

### 10.2.2 Installation with SDKMAN!

SDKMAN! (The Software Development Kit Manager) can be used for managing multiple versions of various binary SDKs, including Groovy and the Spring Boot CLI. Get SDKMAN! from sdkman.io and install Spring Boot by using the following commands:

```
$ sdk install springboot
$ spring --version
Spring Boot v2.1.5.RELEASE
```

If you develop features for the CLI and want easy access to the version you built, use the following commands:

```
$ sdk install springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-2.1.5.RELEASE-bin/spring-2.1.5.RELEASE/
$ sdk default springboot dev
$ spring --version
Spring CLI v2.1.5.RELEASE
```

The preceding instructions install a local instance of `spring` called the `dev` instance. It points at your target build location, so every time you rebuild Spring Boot, `spring` is up-to-date.

You can see it by running the following command:

```
$ sdk ls springboot

================================================================================
Available Springboot Versions
================================================================================
> + dev
* 2.1.5.RELEASE

================================================================================
+ - local version
* - installed
> - currently in use
================================================================================
```

### 10.2.3 OSX Homebrew Installation

If you are on a Mac and use Homebrew, you can install the Spring Boot CLI by using the following commands:

```
$ brew tap pivotal/tap
$ brew install springboot
```

Homebrew installs `spring` to `/usr/local/bin.`

> If you do not see the formula, your installation of brew might be out-of-date. In that case, run `brew update` and try again.

### 10.2.4 MacPorts Installation

If you are on a Mac and use MacPorts, you can install the Spring Boot CLI by using the following command:

```
$ sudo port install spring-boot-cli
```

### 10.2.5 Command-line Completion

The Spring Boot CLI includes scripts that provide command completion for the `BASH` and `zsh` shells. You can `source` the script (also named `spring`) in any shell or put it in your personal or system-wide bash completion initialization. On a Debian system, the system-wide scripts are in `/shell-completion/bash` and all scripts in that directory are executed when a new shell starts. For example, to run the script manually if you have installed by using SDKMAN!, use the following commands:

```
$ . ~/.sdkman/candidates/springboot/current/shell-completion/bash/spring
$ spring <HIT TAB HERE>
  grab  help  jar  run  test  version
```

> If you install the Spring Boot CLI by using Homebrew or MacPorts, the command-line completion scripts are automatically registered with your shell.

### 10.2.6 Windows Scoop Installation

If you are on a Windows and use `Scoop`, you can install the Spring Boot CLI by using the following commands:

```
> scoop bucket add extras
> scoop install springboot
```

Scoop installs `spring` to `~/scoop/apps/springboot/current/bin`.


> If you do not see the app manifest, your installation of scoop might be out-of-date. In that case, run scoop update and try again.

### 10.2.7 Quick-start Spring CLI Example

You can use the following web application to test your installation. To start, create a file called `app.groovy`, as follows:

```java
@RestController
class ThisWillActuallyRun {

	@RequestMapping("/")
	String home() {
		"Hello World!"
	}

}
```

Then run it from a shell, as follows:

```
$ spring run app.groovy
```

> The first run of your application is slow, as dependencies are downloaded. Subsequent runs are much quicker.
>
Open localhost:8080 in your favorite web browser. You should see the following output:

```
Hello World!
```

### 10.3 Upgrading from an Earlier Version of Spring Boot
If you are upgrading from an earlier release of Spring Boot, check the [“migration guide” on the project wiki] that provides detailed upgrade instructions. Check also the [“release notes”] for a list of “new and noteworthy” features for each release.

When upgrading to a new feature release, some properties may have been renamed or removed. Spring Boot provides a way to analyze your application’s environment and print diagnostics at startup, but also temporarily migrate properties at runtime for you. To enable that feature, add the following dependency to your project:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-properties-migrator</artifactId>
	<scope>runtime</scope>
</dependency>
```


> Properties that are added late to the environment, such as when using `@PropertySource`, will not be taken into account.

> Once you’re done with the migration, please make sure to remove this module from your project’s dependencies.
>
To upgrade an existing CLI installation, use the appropriate package manager command (for example, `brew upgrade`) or, if you manually installed the CLI, follow the [standard instructions], remembering to update your `PATH` environment variable to remove any older references.

---
如果您通过 spring boot、通用的 spring 获得快速开始。阅读这个章节，它会回答你基于 “是什么？”，“怎么样？”，“为什么？”的问题。它包含了 Spring boot 的介绍，以及（along with）安装说明。然后我们（we then）引导你（walk you）通过构建你的第一个 spring boot 应用，讨论（discussing）一些核心原则（principles）。

# 8. spring boot 介绍

spring boot 使得单体应用创建变得简单。你可以运行生产级别（grage）基于 spring 的应用。我们对Spring平台和第三方库有自己的看法，所以你可以最小化的获得开始。大多数 spring boot 应用只需要很少的配置。

你可以使用 spring boot 创建 java 应用，那样你可以使用 `java -jar` 或者 更多传统（traditional）的 war 包部署。我们同样提供命令行工具运行“spring 脚本”。

我们主要的目标是：

- 为所有的 spring 开发提供一种更加快速（pradically faster）和广泛访问（widly accessiblw）的快速开始体验。
- 开箱即用（Be opinionated out of the box），但随着需求（requirements）开始偏离（diverge）默认值而迅速摆脱困境。
- 提供一些（a range of）非功能性（non-functional）的特性，（这些特性）是大型项目通用的。例如嵌入式服务器、安全、测量、健康检查和外部化配置。
- 确实没有没有代码生成和 xml 配置的要求。

# 9. 系统要求

Spring Boot 2.1.5.RELEASE 需要 java 8，向上兼容（compatible up） java 11（包括）。Spring Framework 5.1.7.RELEASE 或更高版本同样是必须的。

为以下构建工具提供了显式（Explicit）构建支持：

Build Tool | Version |
-----------|---------|--
Maven      | 3.3+    |
Gradle     | 4.4+    |

## 9.1 Servlet 容器

spring boot 提供了以下嵌入式服务器：

Name         | Servlet Version |
-------------|-----------------|--
Tomcat 9.0   | 4.0             |
Jetty 9.4    | 3.1             |
Undertow 2.0 | 4.0             |

你可以同样部署 spring boot 应用到兼容 servlet 3.1+ 的容器。

# 10. 安装 spring boot
spring boot 可以使用“经典的”的java部署工具或者安装命令行工具。
无论哪种方式（either way），你需要 jdk 1.8 或更高的版本。在开始之前，你需要使用以下命令检查你当前的java安装。

```sh
java -version
```

如果你是 java 开发新手，或者你想尝试（experiment） spring boot。你可能首先想要尝试 [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/#getting-started-installing-the-cli)（命令行接口）。否则，请阅读经典的安装介绍。

## 10.1 java 开发者的安装介绍
你可以像使用任意标准 java 类库同样的方式（in the same way as）一样使用 spring boot。这样做，包含一个合适的 `spring-boot-*.jar` 的文件在你的类路径下。spring boot 不需要与任何特定工具集成，所以你可以使用任一 IDE 或文本编辑器。同样，Spring boot 也没有特定的应用。因此，你可以像使用其他java程序一样运行或调试 spring boot 应用。

虽然（although）你可以拷贝 spring boot 的jar，我们通常建议（generally recommend）您使用支持依赖管理的构建工具。

### 10.1.1 Maven 安装
Spring Boot 兼容 Apache Maven 3.3 或更高版本。如果你还没有（not alreay）安装 Maven，你可以按照 maven.apache.org 操作使用。

> 在一些操作系统上，maven 可以通过包管理安装。如果你使用 OSX Homebrew，尝试 `brew install maven`。Ubuntu 用户可以运行 `sudo apt-get inst6all maven`，巧克力 window 用户可以从管理员提示符运行 `choco install maven` 。

Spring Boot 依赖使用 `org.springframework.boot` 的 groupId，通常（typically），你的 maven pom 文件继承 `spring-boot-starter-parent` 父项目，向一个或多个“启动器”声明依赖。Spring Boot 提供可选的 maven 插件创建可执行jar。

以下列表展示了一个典型的 `pom.xml` 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>myproject</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<!-- 默认继承 spring boot -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.5.RELEASE</version>
	</parent>

	<!-- 添加 web 应用的典型依赖项 -->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<!-- 打包为可执行 jar -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
```

> spring-boot-starters-parent 是使用 Spring Boot 的好的方式，但是它不可能适合（suitable）所有情况。有的时候你可能需要继承不同的父 pom，或者你可能不需要我们的默认设置。在那些情况下（in those cases），查看“13.2.2章，在没有 parent pom 下使用 spring boot，对于使用 `import` 域的可代替（alternative）方案。

### 10.1.2 继承 Gradle
Spring Boot 兼容 Gradle 4.4 和更高版本，如果你还没有安装 Gradle，你可以在 gradle.org 找到使用说明。

spring boot 依赖项可以通过使用 `org.springframework.boot` 这一 group 来申明（declared），通常，你的项目声明依赖关系为一个或多个“启动器”。Spring boot 提供可用的 gradle 插件，它可以简化依赖声明和创建可执行jar。

> **Gradle Wrapper**
> 当你需要构建一个项目时 Gradle Wrapper 提供了一种好的方式“获得”Gradle。它是一个小脚本和库，您可以与代码一起（alongside）提交以引导（bootstrap）构建过程。更多详情请查看 https://docs.gradle.org/4.2.1/userguide/gradle_wrapper.html

更多获得 spring boot 和 Gradle 的信息可以在 Gradle 插件的参考指南的 [“快速开始章节”](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/gradle-plugin/reference/html/#getting-started) 找到。

## 10.2 安装 Spring Boot CLI（命令行工具）
Spring Boot 命令行接口是一个命令行工具，你可以使用 Spring 快速原型。它允许你运行 Groovy 脚本，这意味着你有一个熟悉的类似（familiar）Java的语法没有这么多的样板代码（boilerplate code）。

你不必非要使用 CLI 在 Spring Boot 中，但这绝对（difinitely）是获得 Spring 应用程序的最快方法。

### 10.2.1 手动安装
你可以从spring软件仓库下载 Spring CLI 发行版：

- spring-boot-cli-2.1.5.RELEASE-bin.zip
- spring-boot-cli-2.1.5.RELEASE-bin.tar.gz

最新的（cutting edge）快照版本同样可用。

下载完成后，按照 [INSTALL.txt](https://raw.githubusercontent.com/spring-projects/spring-boot/v2.1.5.RELEASE/spring-boot-project/spring-boot-cli/src/main/content/INSTALL.txt) 引导从解压缩归档。总之，`.zip` 文件中的 `bin/` 目录下有一个 `spring` 脚本。或者（Alternatively），你可以在 jar 文件中使用 java -jar（脚本帮助您确保正确设置了类路径）

### 10.2.2  SDKMAN 安装
SDKMAN!（一个软件开发工具包管理器）可以用来管理多个各种（various）版本的 SDK，包含 Groovy 和 Spring Boot CLI。从 sdkman.io 获得 SDKMAN 并从以下命令安装：

```sh
$ sdk install springboot
$ spring --version
Spring Boot v2.1.5.RELEASE
```

如果你通过 CLI 开发功能，并且想要快速访问你构建的版本，使用以下命令行：

```sh
$ sdk install springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-2.1.5.RELEASE-bin/spring-2.1.5.RELEASE/
$ sdk default springboot dev
$ spring --version
Spring CLI v2.1.5.RELEASE
```

前面的指令（preceding instructions）安装了一个名为（called） `dev` 的本地 `spring` 实例。它指向了你的构建路径，所以每当你重新构建 Spring Boot，`spring` 都是最新的。

通过运行以下命令可以看到它：
```sh
$ sdk ls springboot

================================================================================
Available Springboot Versions
================================================================================
> + dev
* 2.1.5.RELEASE

================================================================================
+ - local version
* - installed
> - currently in use
================================================================================
```

### 10.2.3 OSX Homebrew 安装

如果你在 Mac 上使用 Homebrew，你可以通过以下命令安装 Spring Boot CLI：

```sh
$ brew tap pivotal/tap
$ brew install springboot
```

Homebrew 安装 `spring` 到了 `/usr/local/bin.`

> 如果你看不到公式（formula），您安装的 brew 可能过时。那样的话（in that case），再次运行 `run update`。

### 10.2.4 MacPorts 安装

如果你在 mac 上使用 MacPorts，你可以使用以下命令安装 Spring Boot CLI：

```sh
$ sudo port install spring-boot-cli
```

### 10.2.5 命令行编译
Spring Boot CLI包含为 BASH 和 zsh shell 提供命令完成的脚本。你可以在任何 shell 中获得脚本（也称之为 spring），或者将其放入个人或系统范围的bash完成初始化。在 Debian 系统上，该系统范围内的脚本在 `/shell-completion/bash`，并且当新shell启动时，该目录中的所有脚本都将被执行。例如：如果你使用 SDKMAN 安装了脚本，可以通过以下命令手动运行该脚本：

```sh
$ . ~/.sdkman/candidates/springboot/current/shell-completion/bash/spring
$ spring <HIT TAB HERE>
  grab  help  jar  run  test  version
```

> 如果你使用 Homebrew 或 MacPorts 安装的 Spring Boot CLI，该命令行编译脚本将自动注册到你的 shell。

### 10.2.6 Windows Scoop 安装
如果你在 Windows 上面使用 Scoop，你可以通过以下命令安装 Spring Boot CLI：

```sh
scoop bucket add extras
scoop install springboot
```

Scoop 安装 `spring` 到了 `~/scoop/apps/springboot/current/bin.`

> 如果您没有看到应用程序清单（app manifest），你安装的 scoop 可能不是最新版。这样的话，运行 scoop update 然后重试。

### 10.2.7 Spring CLI 案例快速开始
你可以使用以下 Web 应用测试你的安装，开始，创建一个名为 `app.groovy` 的文件，如下：

```Groovy
@RestController
class ThisWillActuallyRun {

	@RequestMapping("/")
	String home() {
		"Hello World!"
	}

}
```

然后从脚本运行，如下：

```sh
spring run app.groovy
```

> 在下载依赖项时首次运行会很慢，随后的运行会很快速。

在你喜爱的浏览器上打开 localhost:8080，你可以看到以下输出：

```
Hello World!
```

## 10.3 从 SpringBoot 的早期（Earlier）版本升级
如果你从早期的 spring boot 发行版升级，从项目的 wiki 上点击 “迁移指南”，它提供了更详细的说明。另请查看“发行说明”，了解每个版本的“新的和值得注意的（noteworthy）”功能列表。

当升级到了最新发行版，一些属性可能已经（have been）重命名或者删除。Spring Boot 提供一种方式分析的你的应用环境，和在启动时打印诊断（diagnostics），还可以（but also）在运行时（runtime）临时（temporarily）迁移（migrate）属性。要打开这个功能，添加以下依赖到你的项目：

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-properties-migrator</artifactId>
	<scope>runtime</scope>
</dependency>
```

> 晚加入到环境之后的属性，例如 `@PropertySource`，将不会被考虑在内。
> 一旦你完成了迁移，请确保从项目中移除该模块。

要更新已存在的 CLI 安装，使用适当的包管理器命令（例如：brew update）或者，如果你手动安装CLI，从请遵守（follow）标准说明，记住更新PATH环境变量以删除任何旧的引用。
