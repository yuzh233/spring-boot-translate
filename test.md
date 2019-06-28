> Spring Boot Reference Guide
2.1.5.RELEASE
https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-spring-beans-and-dependency-injection.html

<h1 style="color:green; text-align:center;">Part III. Using Spring Boot</h1>
<!-- TOC -->

- [17 Spring Bean ����ע��](#17-spring-bean-%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5)
- [18. ʹ�� @SpringBootApplication ע��](#18-%E4%BD%BF%E7%94%A8-springbootapplication-%E6%B3%A8%E8%A7%A3)
- [19. �������Ӧ��](#19-%E8%BF%90%E8%A1%8C%E4%BD%A0%E7%9A%84%E5%BA%94%E7%94%A8)
	- [19.1 �� IDE ����](#191-%E4%BB%8E-ide-%E8%BF%90%E8%A1%8C)
	- [19.2 ��Ϊ���Ӧ�ó�������](#192-%08%E4%BD%9C%E4%B8%BA%E6%89%93%E5%8C%85%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E8%BF%90%E8%A1%8C)
	- [19.3 ʹ�� Maven ���](#193-%E4%BD%BF%E7%94%A8-maven-%E6%8F%92%E4%BB%B6)
	- [19.4 ʹ�� Gradle ���](#194-%E4%BD%BF%E7%94%A8-gradle-%E6%8F%92%E4%BB%B6)
	- [19.5 �Ȳ���](#195-%E7%83%AD%E9%83%A8%E7%BD%B2)
- [20. �����߹���](#20-%E5%BC%80%E5%8F%91%E8%80%85%E5%B7%A5%E5%85%B7)
	- [20.1 Ĭ������](#201-%E9%BB%98%E8%AE%A4%E5%B1%9E%E6%80%A7)
	- [20.2 �Զ�����](#202-%E8%87%AA%E5%8A%A8%E9%87%8D%E5%90%AF)
		- [20.2.1. ��״̬������condition evaluation���м�¼�仯](#2021-%E5%9C%A8%E7%8A%B6%E6%80%81%E8%AF%84%E4%BC%B0condition-evaluation%E4%B8%AD%E8%AE%B0%E5%BD%95%08%E5%8F%98%E5%8C%96)
		- [20.2.2. �ų���Դ](#2022-%E6%8E%92%E9%99%A4%E8%B5%84%E6%BA%90)
		- [20.2.3. ���Ӷ����·��](#2023-%E7%9B%91%E8%A7%86%E9%A2%9D%E5%A4%96%E7%9A%84%E8%B7%AF%E5%BE%84)
		- [20.2.4. ��������](#2024-%E7%A6%81%E7%94%A8%E9%87%8D%E5%90%AF)
		- [20.2.5. ʹ�ô����ļ�](#2025-%E4%BD%BF%E7%94%A8%E8%A7%A6%E5%8F%91%E6%96%87%E4%BB%B6)
		- [20.2.6. ���������������](#2026-%E5%AE%9A%E5%88%B6%E9%87%8D%E5%90%AF%E7%B1%BB%E5%8A%A0%E8%BD%BD%E5%99%A8)
		- [20.2.7. ��֪����](#2027-%E5%B7%B2%E7%9F%A5%E9%99%90%E5%88%B6)
	- [20.3 �ȼ���](#203-%E7%83%AD%E5%8A%A0%E8%BD%BD)
	- [20.4 ȫ������](#204-%E5%85%A8%E5%B1%80%E8%AE%BE%E7%BD%AE)
	- [20.5 Զ��Ӧ��](#205-%E8%BF%9C%E7%A8%8B%E5%BA%94%E7%94%A8)
		- [20.5.1 ����Զ��Ӧ�ÿͻ���](#2051-%E8%BF%90%E8%A1%8C%E8%BF%9C%E7%A8%8B%E5%BA%94%E7%94%A8%E5%AE%A2%E6%88%B7%E7%AB%AF)
		- [20.5.2 Զ�̸���](#2052-%E8%BF%9C%E7%A8%8B%E6%9B%B4%E6%96%B0)
- [21. Ϊ��������������Ӧ��](#21-%E4%B8%BA%E7%94%9F%E4%BA%A7%E7%8E%AF%E5%A2%83%E6%89%93%E5%8C%85%E4%BD%A0%E7%9A%84%E5%BA%94%E7%94%A8)
- [22. ��һ����ʲô](#22-%08%E4%B8%8B%E4%B8%80%E6%AD%A5%E6%98%AF%E4%BB%80%E4%B9%88)

<!-- /TOC -->
<!-- more -->
# 17 Spring Bean ����ע��
��������ʹ�������׼�� Spring ��ܼ������������� bean �͹�������ע�롣Ϊ�˼򵥣����Ǿ�������ʹ�� @ComponentScan ��������� bean����ʹ�� @Autowired ��������ע�룩Ч���ܺã�work well����
<!-- more -->
�����������Ľ��鹹����Ĵ��루�ڸ����ж�λӦ�ó����ࣩ������������ɵģ�without arguments����� @ComponentScan����Ӧ�õ����������@Component��@Service��@Repository��@Controller�������Զ�ע�ᵽ Spring bean�

����ʵ��չʾ��һ�� @Service bean����ʹ�ÿ�����ע���Ի�ñ�Ҫ�� `RiskAssessor` bean��

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

������ bean ��һ���������������ʡ�� @Autowired����������ʾ��
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

> ע�⣬���ʹ�ÿ�����ע���� riskAssessor �ֶα��Ϊ final���������indicating�������subsequently�����ܱ��޸ġ�

# 18. ʹ�� @SpringBootApplication ע��
��� Spring Boot �Ŀ�����ϲ�����ǵ�Ӧ��ʹ���Զ����ã����ɨ����ܹ���be able to�������ǵ������϶������ģ�extra�������á�һ����һ�� @SpringBootApplication ע���Ϳ��Ա�����������Щ�������ԣ������ǣ�

- `@EnableAutoConfiguration`������[Spring Boot ���Զ����û���](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-auto-configuration.html)
- `@ComponentScan`����Ӧ�ó������ڵİ����� @Component ɨ�裨[���ʵս](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-structuring-your-code.html)��
- `@Configuration`��������������ע������ bean ���ߵ�������������

��� @SpringBootApplication ע��ȼ��ڣ�equivalent��ʹ�� @Configuration��@EnableAutoConfiguration���� @ComponentScan ���ǵ�Ĭ�����ԣ�������ʾ��

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

> @SpringBootApplication ͬ���ṩ�������� @EnableAutoConfiguration���� @ComponentScan ������

��Щ���ܶ�����ǿ���Եģ�mandatory���������ѡ��ͨ�����κε��������滻�������ע�⡣���磺����ܲ��������Ӧ����ʹ��ע��ɨ�裺

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

����������У�Application ���������� Spring Boot Ӧ��һ������ @Component ע���಻�ᱻ��⵽���û������ bean ����ʽ�ĵ��루�� @Import����

# 19. �������Ӧ��
������Ӧ����Ϊһ�� jar ��ʹ����Ƕ�� HTTP ��������һ�����������ǣ������������Ӧ�ó���һ���������Ӧ�á�Spring Boot �ĵ���Ҳͬ���򵥣��㲻��Ҫ�κ��ض��� IDE �������չ����

> ����½�ֻ���ǻ��ڰ��� jar�������ѡ�������Ӧ����Ϊһ�� war ���ļ�������Բο��������� IDE �ĵ���

## 19.1 �� IDE ����
����Դ���� IDE ��Ϊһ���򵥵� Java Ӧ������ Spring Boot��Ȼ������������Ҫ���������Ŀ������Ĳ���Ĳ�ͬ��vary�������ڣ�depending on����� IDE �͹���ϵͳ������� IDE ����ֱ�ӵ��� maven ��Ŀ�����磺Eclipse �û�����ѡ�� `import` -> `existing maven projects` ���ļ��˵���

����㲻��ֱ�ӵ��������Ŀ����� IDE�������ͨ��ʹ�ù���������� IDE Ԫ���ݡ�Maven ������ IDEA �� Eclipse �����gradle Ϊ���֣�various�� ide �ṩ�����

> ����㲻С�ģ�accidentally�����������Ӧ�ó������Σ�����Բ鿴���˿��ѱ�ʹ�á�����STS �û�����ʹ�� `Relaunch` ��ť�����ǣ�rather than��`Run` ��ť��ȷ����ensure���κδ��ڵ�ʵ���ǹرյġ�

## 19.2 ��Ϊ���Ӧ�ó�������
�����ʹ�� Spring Boot Maven �� Gradle �������һ����ִ�� jar��������������Ӧ��ʹ�� `java -jar`����������ʾ��

```sh
java -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

������������Զ�̵���֧�ֵ���������д��Ӧ�ó�������������ʹ������һ�������������Ӧ�ó�����������ʾ��

```sh
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n \
       -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

## 19.3 ʹ�� Maven ���
Spring Boot Maven �������һ�� `run` Ŀ�����ʹ������������������������Ӧ�á�Ӧ�ó����Էֽ���ʽ��exploded�����У�������� IDE һ����������һ������չʾ��һ�����͵� maven ����������� spring boot Ӧ�ã�

	mvn spring-boot:run

�������Ҫʹ�� `MAVEN_OPTS` ����ϵͳ����������������ʾ��

	export MAVEN_OPTS=-Xmx1024m


## 19.4 ʹ�� Gradle ���
Spring Boot Gradle ���ͬ������ `bootRun` ������Ա�ʹ�����ֽ�ʽ���������Ӧ�á�ÿ����Ӧ�� `org.springframework.boot` �� `java` ���ʱ������� `bootRun`��������ʾ��

	gradle bootRun

�������Ҫʹ�� `JAVA_OPTS` ����ϵͳ����������������ʾ��

	export JAVA_OPTS=-Xmx1024m

## 19.5 �Ȳ���
���� Spring Boot Ӧ��ֻ��һ����ͨ�ģ�plain���� Java Ӧ�ã�JVM �Ȳ�����Կ��伴�ã�work out of the box����JVM �Ȳ����е������ڣ�somewhat limited with���������滻���ֽ��롣����ı���������������ʹ�� [JRebel](https://zeroturnaround.com/software/jrebel/)

`spring-boot-devtools` ģ��ͬ��������֧��Ӧ�ÿ����������鿴���½�����ģ�later in this chapter��[20 �� ���� ��������](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/html/using-boot-devtools.html) �� [���ʹ���Ȳ���](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/reference/html/howto-hotswapping.html) ��ø���ϸ�ڡ�

# 20. �����߹���
Spring Boot �����˶�������߼�������ʹ���Ӧ�ÿ���������΢��죨pleasant��һ�㡣`spring-boot-devtools` ģ����Ա���ӵ�������Ŀ�����ṩ����Ŀ���ʱ���ԡ�Ҫ�������Թ���֧�֣����ģ����������������У�����չʾ�� Maven �� Gradle ���嵥��

Maven��
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

> �����߹��������������������Ӧ��ʱ�Զ����á���������� `java -jar` ������������������ض������������ʼ����ô��Ϊ��considered������һ������Ӧ�á�����������������������Ӧ���Ǵ��������У�����Ϊ�ų��˿����߹��߻���������ϵͳ���ԣ�`-Dspring.devtools.restart.enabled=false`

> ��Maven�н���������Ϊ��ѡ�ģ�������Gradle��ʹ�ö��Ƶġ�ֻ����������(��������ʾ)�Ƿ�ֹDevTools����ʱӦ�õ�ʹ��������Ŀ������ģ������ʵ����

> Ĭ����������´��������������߹��ߡ��������ʹ��ĳЩԶ�̿������ԣ�����Ҫ���� `excludeDevtools` �����԰��������������ͬʱ֧�� Maven �� Gradle �����

## 20.1 Ĭ������
һЩ���ͨ��֧��ʹ�� Spring Boot ʹ�û�����������ܣ�improve performance�������磺ģ�����滺������ģ���Ա��⣨avoid���ظ���repeatedly������ģ���ļ���ͬ����������̬��Դʱ Spring MVC  ������� HTTP ����ͷ����Ӧ��Ϣ�С�

�������������Ƿǳ�����ģ�beneficial����Ȼ�����ڿ�����������ʵ��䷴��counter-productive������ֹ��preventing���㿴����ո���Ӧ�ó����в����ĸ��ġ��������ԭ��spring-boot-devtools Ĭ�Ͻ��û���ѡ�

����ѡ��ͨ������� `application.properties` �ļ��������á����磺Thymeleaf �ṩ�� `spring.thymeleaf.cache` ���ԣ��������ֶ�������Щ���ԣ�spring-boot-devtools ģ���Զ�����Ӧ�ÿ���ʱ���á�

��Ϊ����Ҫ������Ϣ���� web �������Ϣ�ڿ��� spring mvc �� spring WebFlux Ӧ��ʱ�������߹��߽���Ϊ web ��־��¼���� debug ����־��¼���⽫�����������������Ϣ�������г��򣬷��ؽ���ȡ������ϣ����¼���������ϸ�ڣ����ܰ���������Ϣ��������Դ� `spring-http.log-request-detail` �������ԡ�

> ����㲻��Ӧ�ø�Ĭ���������������� application.properties ������ spring-http.log-request-detail Ϊ false��

> Ӧ���� devtools �����е������б��鿴 [DevToolsPropertyDefaultsPostProcessor.](https://github.com/spring-projects/spring-boot/tree/v2.1.6.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java)

## 20.2 �Զ�����
ʹ�� spring-boot-devtools ��Ӧ�û��Զ�������ÿ����·���µ��ļ��ı䡣�� IDE ����ʱ������һ�����õ����ԣ���Ϊ��Ϊ����ı��ṩ����ٵķ���ѭ������ΪĬ�ϣ�ָ��point to����·���µ�������Ŀ���ᱻ����Ϊ�˸��ġ�ע��ĳЩ��Դ�磺��̬��Դ����ͼģ�棬[����Ҫ��������Ӧ��](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-restart-exclude)��

**��������**
�� DevTools ������·���µ���Դ������������Ψһ��ʽ�Ǹ�������·�������£�cause����·�����µķ�ʽ��������ʹ�õ� IDE���� Eclipse �У�������޸��ļ�������·�����ºͳ����������� IDEA��������Ŀ��ͬ����Ч����

> ֻҪ�˷ֲ汻�򿪣������ͬ���������Ӧ��ͨ��ʹ��֧�ֵĹ����������Ϊ DevTools ��Ҫһ��������Ӧ�ó������������ȷ��������ΪĬ�ϣ�Gradle �� Maven ����·���ϼ�⵽ DevTools ʱ����������

> �� LiveReload ����ʱ�Զ������������ã�[�鿴 LiveReload �½ڻ�ø���ϸ��](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-livereload)�������ʹ�� JReble���Զ���������ã������ڣ�in favor of����Ķ�̬���ء����� devtools �������磺LiveReload �� ���Ը��ǿ���һֱʹ�á�

> DevTools ������Ӧ�ó��������ĵ� shutdown �������������ڼ�ر����� ��������� shutdown �ҹ������޷�����������

> ����������·���ϵ���Ŀ�Ƿ�Ӧ���ڸ���ʱ������������ʱ��Devztools �Զ�������Ϊ spring-boot, spring-boot-devtools, spring-boot-autoconfigure, spring-boot-actuator, spring-boot-starter ����Ŀ��

> DevTools ��Ҫͨ�� ApplicationContext ������ ResourceLoader���������Ӧ���Ѿ��ṩ��һ����������������������֧��ֱ�Ӹ��� ApplicationContext �ϵ� getResource ������

**���������¼���**
Spring Boot �����ṩ��������������ʹ���������������������ı���ࣨ���磺������jar�������ص���loaded into������������С������ڻ����������౻���ص����������������Ӧ�ó�����������������������ᱻ������thrown away�������´���һ���µġ����ַ�����ζ��Ӧ�ó�������ͨ���ȡ�����������ö࣬��Ϊ����װ�����Ѿ����ò�����䡣

�����������������Ӧ�ó�����˵�����죬����������������⡣����Կ�������ѡ�������� ZeroTurnaround ��� JReble����Щ������ͨ���ڼ�����ʱ��д������ɵģ���ʹ���Ǹ��������¼��ء�

### 20.2.1. ��״̬������condition evaluation���м�¼�仯
��ΪĬ�ϣ�ÿ�����Ӧ������������¼��ʾ״̬���������ı����ñ���չʾ�����Ӧ�õ��Զ����õĸı������ӻ�ɾ��bean�������������ԡ�

Ҫ������־��¼���棬�����������ԣ�

	spring.devtools.restart.log-condition-evaluation-delta=false

### 20.2.2. �ų���Դ
ĳЩ��Դ�����Ǹı�ʱû�б�Ҫ�����������磺Thymeleaf ģ����Ծ͵أ�in-place���༭��Ĭ������£��ı� /META-INF/maven, /META-INF/resources, /resources, /static, /public, or /templates �е���Դ���ᴥ���������ᴥ�� [live reload](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-livereload)�� ������붨����Щ�ų�������ʹ�� `spring.devtools.restart.exclude` ���ԡ��磺Ҫ�����ų� `/static` �� `/public` ����Ҫ�����������

	spring.devtools.restart.exclude=static/**,public/**

> �����Ҫ����Ĭ��ֵ����Ӷ�����ų��ʹ�� `spring.devtools.restart.additional-exclude` ��Ϊ�滻��

### 20.2.3. ���Ӷ����·��
�������Ҫ���Ӧ�ó����������ؼ��ص���������·���¸ı��ļ���Ҫ��������ʹ�� `spring.devtools.restart.additional-paths` �������ö����·�������ӡ�ǰ���������ǿ����ڶ���·���µĸ����Ƿ�ᴥ����ȫ�������������¼��ء�

### 20.2.4. ��������
����㲻��ʹ���������ԣ������ͨ�� `spring.devtools.restart.enabled` ���Խ����������������£����������� `application.properties` ����������ԡ�����������Ȼ��ʼ��ʱ���������������������������ļ����ģ�

�������Ҫ��ȫ��������֧�֣����磺�����ض�������в��ܹ�����������Ҫ�ڵ��� `SpringApplication.run(��