---
title: 20190602 spring-boot | part1
date: 2019-06-02
tag: spring-boot
category:
- english-learning
- spring-boot
thumbnail: http://img.yuzh.xyz/blog/83.jpg
toc: true
---

> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/htmlsingle/

<h1 style="color:green; text-align:center;">Part I. Spring Boot Documentation</h1>

<!-- TOC -->

- [Part I. Spring Boot Documentation](#part-i-spring-boot-documentation)
	- [1. About the Documentation](#1-about-the-documentation)
	- [2. Getting Help](#2-getting-help)
	- [3. First Steps](#3-first-steps)
	- [4. Working with Spring Boot](#4-working-with-spring-boot)
	- [5. Learning about Spring Boot Features](#5-learning-about-spring-boot-features)
	- [6. Moving to Production](#6-moving-to-production)
	- [7. Advanced Topics](#7-advanced-topics)
- [第一单元：Spring Boot 文档](#%E7%AC%AC%E4%B8%80%E5%8D%95%E5%85%83spring-boot-%E6%96%87%E6%A1%A3)
	- [1. 关于文档](#1-%E5%85%B3%E4%BA%8E%E6%96%87%E6%A1%A3)
	- [2. 获得帮助](#2-%E8%8E%B7%E5%BE%97%E5%B8%AE%E5%8A%A9)
	- [3. 第一步](#3-%E7%AC%AC%E4%B8%80%E6%AD%A5)
	- [4. 使用 spring boot 工作](#4-%E4%BD%BF%E7%94%A8-spring-boot-%E5%B7%A5%E4%BD%9C)
	- [5. 学习 spring boot 的特性功能](#5-%E5%AD%A6%E4%B9%A0-spring-boot-%E7%9A%84%E7%89%B9%E6%80%A7%E5%8A%9F%E8%83%BD)
	- [6. 移动到生产](#6-%E7%A7%BB%E5%8A%A8%E5%88%B0%E7%94%9F%E4%BA%A7)
	- [7. 高级主题](#7-%E9%AB%98%E7%BA%A7%E4%B8%BB%E9%A2%98)

<!-- /TOC -->
<!-- more -->
# Part I. Spring Boot Documentation
This section provides **a brief overview** of Spring Boot **reference documentation**. It **serves as** a **map for** the **rest of** the document.

## 1. About the Documentation
The Spring Boot reference guide is available as

- HTML
- PDF
- EPUB

The latest copy is available at docs.spring.io/spring-boot/docs/current/reference.

**Copies of** this document may be **made for** your own use and for **distribution** to others, **provided that** you do not **charge** any fee for such copies and **further provided that** each copy contains this Copyright Notice, **whether** distributed in print or electronically.

## 2. Getting Help
If you have trouble with Spring Boot, we would like to help.

- Try the **How-to** documents. They provide solutions to the most common questions.

- Learn the Spring basics. Spring Boot builds on many other Spring projects. Check the spring.io web-site for **a wealth of** reference documentation. If you are starting out with Spring, try one of the guides.

- Ask a question. We **monitor** stackoverflow.com for questions tagged with spring-boot.

- Report bugs with Spring Boot at github.com/spring-projects/spring-boot/issues.

All of Spring Boot is open source, including the documentation. If you find problems with the docs or if you want to improve them, please get involved.

## 3. First Steps
If you are getting started with Spring Boot or 'Spring' in general, start with the following topics:

- **From scratch**: Overview | Requirements | Installation
- **Tutorial**: Part 1 | Part 2  |
- Running your example: Part 1 | Part 2

## 4. Working with Spring Boot
Ready to **actually** start using Spring Boot? We have you **covered**:

- Build systems: Maven | Gradle | Ant | Starters
- Best practices: Code Structure | @Configuration | @EnableAutoConfiguration | Beans and Dependency Injection
- Running your code: IDE | Packaged | Maven | Gradle
- Packaging your app: Production jars
- Spring Boot CLI: Using the CLI

## 5. Learning about Spring Boot Features
Need more details about Spring Boot’s core features? The following content is for you:

- Core Features: SpringApplication | External Configuration | Profiles | Logging
- Web Applications: MVC | Embedded Containers
- Working with data: SQL | NO-SQL
- Messaging: Overview | JMS
- Testing: Overview | Boot Applications | Utils
- **Extending**: Auto-configuration | @Conditions

## 6. Moving to Production
When you are ready to push your Spring Boot application to production, we have **some tricks** that you might like:

- Management endpoints: Overview | Customization
- Connection options: HTTP | JMX
- Monitoring: Metrics | Auditing | Tracing | Process

## 7. Advanced Topics
Finally, we have **a few** topics for more advanced users:

- Spring Boot Applications Deployment: Cloud Deployment | OS Service
- Build tool plugins: Maven | Gradle
- **Appendix**: Application Properties | Auto-configuration classes | Executable Jars

---
# 第一单元：Spring Boot 文档
这一章节提供对spring boot参考文档的简要概述（a brief overview）。它可以作为（serves as）文档其余部分（rest of）的映射。

## 1. 关于文档
该 spring boot 参考文档可用有

- html
- pdf
- EPUB

最新的副本可在 docs.spring.io/spring-boot/docs/current/reference.

此文档的副本（copies of this document）可以为（made for）你自己使用，也可以分发（distribution）给别人。但需（provided that）要你对这些副本（such copies）不收取（charge）任何费用，并且每一个副本需要包含版权申明，无论（whether）是印刷发行还是电子发行。

## 2. 获得帮助

如果你使用 spring boot 有问题，我们愿意（would like）帮助：

- 尝试使用操作（how-do）文档。他们对大多数问题提供了解决方案。
- 学习 spring 基础，spring boot 建立在许多 spring 项目之上。查看spring.io网站获取大量（a wealth of）参考文档。如果您从 spring 开始，尝试其中一个指南。
- 询问问题，我们会监视（monitor） stackoverflow.com 获取标签为 spring-boot 的问题。
- 在 github.com/spring-projects/spring-boot/issues. 上反馈 spring boot 的bug。

```
spring boot 的所有都是开源的，包裹参考文档。如果你在该文档中发现问题并想改善（improve）他们，请参与进来（get involved）。
```

## 3. 第一步
如果您要开始使用 spring boot 或者通用的 spring，从以下主题开始：

- 从头开始（From scratch）：概览 | 要求 | 安装
- 指南：单元1 | 单元2
- 运行你的案例：单元1 | 单元2

## 4. 使用 spring boot 工作

确定（actually）准备开始使用 spring boot？我们为您涵盖了（以下内容）：

- 构建系统：maven | gradle | ant  starters
- 最佳实战（parctices）：代码结构 | @Configuration | @EnableAutoConfiguration | Beans 和依赖注入（Dependency Injection）
- 运行你的代码：IDE | Packaged | Maven | Gradle
- 打包你的应用：生产的jar
- spring boot CLI： 使用 CLI

## 5. 学习 spring boot 的特性功能
想要更多 spring boot 核心功能的细节？以下内容供您参考：

- 核心功能：SpringApplication | External Configuration外部配置 | Profiles | Logging
- web 容器：MVC | Embedded（嵌入式） Containers
- 使用数据：SQL | NO-SQL
- 消息：概述 | JMS
- 测试：概述 | Boot 应用 | 单元测试
- 拓展（Extending）：自动配置 | @Conditions

## 6. 移动到生产
当您准备推送你的 spring boot 应用到生产环境，我们提供一个一些小窍门（some tricks ）你可能喜欢：

- 管理端点（Management endpoints）: Overview | Customization
- 链接选项（Connection options）: HTTP | JMX
- 监测（Monitoring）: Metrics | Auditing | Tracing | Process

## 7. 高级主题
最后，我们为更高级用户提供了一些（a few）的主题：

- spring boot 应用部署：Cloud Deployment | OS Service
- 构建工具插件：Maven | Gradle
- 附录（Appendix）：Application Properties | Auto-configuration classes | Executable Jars 可执行jar
