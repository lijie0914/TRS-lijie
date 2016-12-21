# 搭建season开发环境,熟悉spring boot
## 一、Hello World项目
#### 1 新建maven项目：File-->New-->Project...
###### 1.1 选择maven项目，jdk选择1.7及以上，点击next
![](http://p1.bqimg.com/581766/0c6b46b52265766e.png)
###### 1.2 填写maven信息
GroupId必须填写为trs.com.cn，ArtifactId填写为你的应用名称，版本号默认即可
![](http://p1.bpimg.com/581766/72c44687128e66ea.png)
###### 1.3 填写项目信息
![](http://p1.bpimg.com/581766/71998e8c86cbfc0c.png)
###### 1.4 点击Finish，项目创建完成，结构如下图
![](http://p1.bpimg.com/581766/e8ce0fe1c1cde94d.png)
#### 2 配置pom.xml如下：
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>trs.com.cn</groupId>
    <artifactId>SeasonTest</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--添加打包格式，war或jar都可以-->
    <packaging>war</packaging>

    <!--添加season的支持-->
    <parent>
        <artifactId>season-parent</artifactId>
        <groupId>trs.com.cn</groupId>
        <version>1.2</version>
    </parent>

    <!--添加season-core的依赖-->
    <dependencies>
        <dependency>
            <groupId>trs.com.cn</groupId>
            <artifactId>season-core</artifactId>
        </dependency>
    </dependencies>

    <!--添加打包插件-->
    <build>
        <finalName>SeasonTest</finalName>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <!--添加海尔maven仓库地址-->
    <repositories>
        <repository>
            <id>haier-maven-repository</id>
            <url>http://test.haier.com/nexus/content/groups/public/</url>
        </repository>
    </repositories>

</project>
```
#### 3 创建类
###### 3.1 创建一个启动类，继承`com.season.core.spring.SeasonApplication`，添加`main`方法:
```
public class App extends com.season.core.spring.SeasonApplication{
    public static void main(String[] args) {
        SeasonRunner.run(App.class);
    }
}
```
###### 3.2 创建Controller，继承`com.season.core.Controller`，添加`@ControllerKey("hello")`注解，新建类所属的包名必须是com开始，因 Season 默认配置的 Spring 扫描包为com。
```
@ControllerKey("hello")
public class HelloController extends com.season.core.Controller{
    public void season(){
        renderText("hello season!!!123");
    }
}
```
#### 4 启动main方法，访问http://localhost:8080/hello/season，即可看见效果：
![](http://i1.piimg.com/581766/c82d25a63415ba0a.png)
## 二、学习spring boot
#### 1 什么是spring boot
Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。
#### 2 spring boot Demo
###### 2.1 创建maven项目，在pom.xml中引入Spring Boot的依赖
```
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.2.5.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```
###### 2.2 编写测试类
```
@Controller
@EnableAutoConfiguration
public class test {
    @RequestMapping("/")
    @ResponseBody
    String home(){
        return "hello spring boot";
    }
    public static void main(String[] args) {
        SpringApplication.run(test.class,args);
    }
}
```
###### 2.3 启动main方法，浏览器访问http://localhost:8080就可以看到结果。
![](http://p1.bpimg.com/581766/60ea59442d2be916.png)
#### 3 spring boot依赖库
- spring-boot-starter-web:支持全栈web开发，里面包括了Tomcat和Spring-webmvc
- spring-boot-starter-mail:提供对javax.mail的支持
- spring-boot-starter-ws: 提供对Spring Web Services的支持
- spring-boot-starter-test:提供对常用测试框架的支持，包括JUnit，Hamcrest以及Mockito等
- spring-boot-starter-actuator:支持产品环境下的一些功能，比如指标度量及监控等
- spring-boot-starter-log4j:引入默认的log框架（logback）
- spring-boot-starter-jetty:支持jetty容器
