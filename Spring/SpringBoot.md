# springboot
## springboot启动流程
### 启动类上注解：@SpringBootApplication
#### @SpringBootConfiguration
根据Javadoc可知，该注解作用就是将当前的类作为一个JavaConfig，然后触发注解@EnableAutoConfiguration和@ComponentScan的处理，本质上与@Configuration注解没有区别
#### @EnableAutoConfiguration
@EnableAutoConfiguration:实现自动装配的核心注解
- @AutoConfigurationPackage
  - 注册当前启动类的根 package
  - 注册 org.springframework.boot.autoconfigure.AutoConfigurationPackages 的 BeanDefinition
- @Import(AutoConfigurationImportSelector.class)
  - 自动装配核心功能的实现实际是通过 AutoConfigurationImportSelector(加载自动装配类)类
  - AutoConfigurationImportSelector 类实现了 ImportSelector接口
    - 实现了这个接口中的 selectImports方法
      - 方法实现 重要的getAutoConfigurationEntry()方法
        1. 判断自动装配是否打开，默认是true可以通过application.yml设置
        2. 获取@EnableAutoConfiguration里的exclude和excludeName内容以便排除
        3. 获取需要自动装配的所有配置类，读取META-INF/spring.factories druid 数据库连接池的 Spring Boot Starter 就创建了META-INF/spring.factories文件
        4. 筛选满足@ConditionalOnXXX注解的类，生效才会被加载
      - 该方法主要用于获取所有符合条件的类的全限定类名，这些类需要被加载到 IoC 容器中
#### @ComponentScan
扫描的 Spring 对应的组件，如 @Componet，@Repository
- 我们可以通过 basePackages 等属性来细粒度的定制 @ComponentScan 自动扫描的范围，如果不指定，则默认Spring框架实现会从声明 @ComponentScan 所在类的package进行扫描，所以 SpringBoot 的启动类最好是放在根package下，我们自定义的类就放在对应的子package下，这样就可以不指定 basePackages
### 启动类中的main方法：org.springframework.boot.SpringApplication#run(java.lang.Class<?>, java.lang.String...)
- 从spring.factories配置文件中加载EventPublishingRunListener对象，该对象拥有SimpleApplicationEventMulticaster属性，即在SpringBoot启动过程的不同阶段用来发射内置的生命周期事件;
  - spring-bean包下META-INF/spring.factories
- 准备环境变量，包括系统变量，环境变量，命令行参数，默认变量，servlet相关配置变量，随机值以及配置文件（比如application.properties）等;
  - 而后就会去创建Environment——这个时候会去加载application配置文件
- 控制台打印SpringBoot的bannner标志；
- 根据不同类型环境创建不同类型的applicationcontext容器，因为这里是servlet环境，所以创建的是AnnotationConfigServletWebServerApplicationContext容器对象；
- 从spring.factories配置文件中加载FailureAnalyzers对象,用来报告SpringBoot启动过程中的异常；
- 为刚创建的容器对象做一些初始化工作，准备一些容器属性值等，对ApplicationContext应用一些相关的后置处理和调用各个ApplicationContextInitializer的初始化方法来执行一些初始化逻辑等；
- 刷新容器，这一步至关重要。比如调用bean factory的后置处理器，注册BeanPostProcessor后置处理器，初始化事件广播器且广播事件，初始化剩下的单例bean和SpringBoot创建内嵌的Tomcat服务器等等重要且复杂的逻辑都在这里实现，主要步骤可见代码的注释，关于这里的逻辑会在以后的spring源码分析专题详细分析；
  - // 1）在context刷新前做一些准备工作，比如初始化一些属性设置，属性合法性校验和保存容器中的一些早期事件等；
  - // 2）让子类刷新其内部bean factory,注意SpringBoot和Spring启动的情况执行逻辑不一样
  - // 3）对bean factory进行配置，比如配置bean factory的类加载器，后置处理器等
  - // 4）完成bean factory的准备工作后，此时执行一些后置处理逻辑，子类通过重写这个方法来在BeanFactory创建并预准备完成以后做进一步的设置
    - // 在这一步，所有的bean definitions将会被加载，但此时bean还不会被实例化
  - // 5）执行BeanFactoryPostProcessor的方法即调用bean factory的后置处理器：
    - // BeanDefinitionRegistryPostProcessor（触发时机：bean定义注册之前）和BeanFactoryPostProcessor（触发时机：bean定义注册之后bean实例化之前）
  - // 6）注册bean的后置处理器BeanPostProcessor，注意不同接口类型的BeanPostProcessor；在Bean创建前后的执行时机是不一样的
  - // 7）初始化国际化MessageSource相关的组件，比如消息绑定，消息解析等
  - // 8）初始化事件广播器，如果bean factory没有包含事件广播器，那么new一个SimpleApplicationEventMulticaster广播器对象并注册到bean factory中
  - // 9）AbstractApplicationContext定义了一个模板方法onRefresh，留给子类覆写，比如ServletWebServerApplicationContext覆写了该方法来创建内嵌的tomcat容器
  - // 10）注册实现了ApplicationListener接口的监听器，之前已经有了事件广播器，此时就可以派发一些early application events
  - // 11）完成容器bean factory的初始化，并初始化所有剩余的单例bean。这一步非常重要，一些bean postprocessor会在这里调用。
  - // 12）完成容器的刷新工作，并且调用生命周期处理器的onRefresh()方法，并且发布ContextRefreshedEvent事件
- 执行刷新容器后的后置处理逻辑，注意这里为空方法；
- 调用ApplicationRunner和CommandLineRunner的run方法，我们实现这两个接口可以在spring容器启动后需要的一些东西比如加载一些业务数据等;
- 报告启动异常，即若启动过程中抛出异常，此时用FailureAnalyzers来报告异常;
- 最终返回容器对象，这里调用方法没有声明对象来接收。
```java
public static void main(String[] args) throws Exception {
   SpringApplication.run(new Class<?>[0], args);
}
public static ConfigurableApplicationContext run(Class<?>[] primarySources, String[] args) {
   // 新建SpringApplication对象，再调用run方法
   return new SpringApplication(primarySources).run(args);
}
public ConfigurableApplicationContext run(String... args) {
   // stopWatch用于统计run启动过程时长
   StopWatch stopWatch = new StopWatch();
   // 开始计时
   stopWatch.start();
   // 创建ConfigurableApplicationContext对象
   ConfigurableApplicationContext context = null;
   // exceptionReporters集合用来存储SpringApplication启动过程的异常，SpringBootExceptionReporter且通过spring.factories方式来加载
   Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList<>();
   // 配置headless属性
   configureHeadlessProperty();
   /**
    * 从spring.factories配置文件中加载到EventPublishingRunListener对象并赋值给SpringApplicationRunListeners
    * # Run Listeners
    * org.springframework.boot.SpringApplicationRunListener=\
    * org.springframework.boot.context.event.EventPublishingRunListener
    */
   SpringApplicationRunListeners listeners = getRunListeners(args);
   // 启动SpringApplicationRunListeners监听
   listeners.starting();
   try {
      // 创建ApplicationArguments对象，封装了args参数
      ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
      // 备配置参数有app.properties，外部配置参数比如jvm启动参数等
      ConfigurableEnvironment environment = prepareEnvironment(listeners, applicationArguments);
      // 配置spring.beaninfo.ignore属性
      configureIgnoreBeanInfo(environment);
      // 打印springboot的bannner
      Banner printedBanner = printBanner(environment);
      // 根据不同类型创建不同类型的spring applicationcontext容器
      context = createApplicationContext();
      /**
       * 异常报告
       * 从spring.factories配置文件中加载exceptionReporters，其中ConfigurableApplicationContext.class作为FailureAnalyzers构造方法的参数
       * # Error Reporters
       * org.springframework.boot.SpringBootExceptionReporter=\
       * org.springframework.boot.diagnostics.FailureAnalyzers
       */
      exceptionReporters = getSpringFactoriesInstances(SpringBootExceptionReporter.class,
            new Class[] { ConfigurableApplicationContext.class }, context);
      // 准备容器事项：调用各个ApplicationContextInitializer的initialize方法
      // 和触发SpringApplicationRunListeners的contextPrepared及contextLoaded方法等
      prepareContext(context, environment, listeners, applicationArguments, printedBanner);
      // 刷新容器，这一步至关重要
      refreshContext(context);
      // 执行刷新容器后的后置处理逻辑，注意这里为空方法
      afterRefresh(context, applicationArguments);
      // 停止stopWatch计时
      stopWatch.stop();
      // 打印springboot的启动时常
      if (this.logStartupInfo) {
         new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
      }
      // 触发SpringApplicationRunListener的started方法，通知spring容器已经启动
      listeners.started(context);
      // 调用ApplicationRunner和CommandLineRunner的run方法，实现spring容器启动后需要做的一些东西
      callRunners(context, applicationArguments);
   }
   // 若上面的方法抛出异常，将异常添加到exceptionReporters集合中，并抛出 IllegalStateException 异常。
   catch (Throwable ex) {
      handleRunFailure(context, ex, exceptionReporters, listeners);
      throw new IllegalStateException(ex);
   }

   try {
      // 当容器刷新完毕等，触发SpringApplicationRunListeners数组的running方法
      listeners.running(context);
   }
   catch (Throwable ex) {
      // 若上面的方法抛出异常，将异常添加到exceptionReporters集合中，并抛出 IllegalStateException 异常。
      handleRunFailure(context, ex, exceptionReporters, null);
      throw new IllegalStateException(ex);
   }
   return context;
}

```

### 简化

Spring Boot的启动流程大致如下：

1. 引导类（Main Class）
Spring Boot应用通常包含一个主类，使用@SpringBootApplication注解标记。该注解结合了@Configuration、@EnableAutoConfiguration和@ComponentScan注解。
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
2. SpringApplication.run()调用SpringApplication.run()方法，起始启动过程：创建SpringApplication实例：并设置初始属性。

3. 准备环境（prepareEnvironment）创建ConfigurableEnvironment对象，设置应用程序的属性和环境变量。

4. 创建上下文（createApplicationContext）根据应用类型创建ApplicationContext（常用的如AnnotationConfigServletWebServerApplicationContext）。

5. 注册Listeners（registerListeners）注册各种ApplicationListener，比如监听Spring应用的事件（如ApplicationEnvironmentPreparedEvent、ApplicationPreparedEvent等）。

6. 准备上下文（prepareContext）设置上下文的属性、环境和资源等，进行初始化。

7. 加载Sources（load）根据注解（如@SpringBootApplication）加载配置类，进行组件扫描并注册到Spring容器。

8. 执行自动配置（auto-configuration）通过@EnableAutoConfiguration，Spring Boot会根据classpath中的库自动配置Bean。例如，检测到Tomcat会自动配置相应的Servlet。

9. 刷新上下文（refreshContext）触发上下文的刷新，完成所有Bean的初始化和配置。

10. 调用CommandLine runners和Application runners如果定义了CommandLineRunner或ApplicationRunner，会在上下文刷新后执行。

11. 启动嵌入式容器如果应用是Web应用，Spring Boot会启动嵌入式Tomcat、Jetty或Undertow等。

12. 应用就绪最后，Spring Boot应用进入就绪状态，等待请求或事件。

**总结**

Spring Boot的启动过程整合了多个步骤，通过自动配置和注解简化了Spring应用的开发过程。整个过程涉及环境处理、上下文创建、Bean注册和必要的监听器等，使得开发者可以专注于业务逻辑，而无需关注复杂的配置。

## 怎么让Spring把Body变成一个对象
- @RequestBody注解原理
- 详细看springmvc的处理流程
## SpringBoot的starter实现原理是什么？
原理就是因为在@EnableAutoConfiguration注解，会自动的扫描jar包下的META-INF/spring.factories文件的配置类，写在这里面的类都是需要被自动加载的

将configuration类中定义的bean加入spring到容器中。就相当于加载之前我们自己配置组件的xml文件。而现在SpringBoot自己定义了一个默认的值，然后直接加载进入了Spring容器。

SpringBoot提供的自动配置依赖模块都以spring-boot-starter-为命名前缀，并且这些依赖都在org.springframework.boot下。 所有的spring-boot-starter都有约定俗成的默认配置，但允许调整这些配置调整默认的行为。
## spring 和springboot的区别
Spring Boot基本上是Spring框架的扩展，它消除了设置Spring应用程序所需的XML配置，为更快，更高效的开发生态系统铺平了道路。

Spring Boot中的一些特征：

- 创建独立的Spring应用。
- 嵌入式Tomcat、Jetty、 Undertow容器（无需部署war文件）。
- 提供的starters 简化构建配置
- 尽可能自动配置spring应用。
- 提供生产指标,例如指标、健壮检查和外部化配置
- 完全没有代码生成和XML配置要求

Maven依赖

首先，让我们看一下使用Spring创建Web应用程序所需的最小依赖项
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.1.0.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.1.0.RELEASE</version>
</dependency>
```
与Spring不同，Spring Boot只需要一个依赖项来启动和运行Web应用程序：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.0.6.RELEASE</version>
</dependency>
```
在进行构建期间，所有其他依赖项将自动添加到项目中。

另一个很好的例子就是测试库。我们通常使用Spring Test，JUnit，Hamcrest和Mockito库。在Spring项目中，我们应该将所有这些库添加为依赖项。但是在Spring Boot中，我们只需要添加spring-boot-starter-test依赖项来自动包含这些库。

spring在运行前需要使用xml文件做很多配置，而springboot帮我们实现了这些配置的自动加载，基于注解和简单的yml配置即可

spring的web程序还是打包为war然后再Tomcat里运行，而springboot内嵌了Tomcat直接打成可运行的jar

## Spring Boot 可执行 Jar 包运行原理
Spring Boot 有一个很方便的功能就是可以将应用打成可执行的 Jar。那么大家有没想过这个 Jar 是怎么运行起来的呢？本篇博客就来介绍下 Spring Boot 可执行 Jar 包的运行原理。

### 打可执行 Jar 包
将 Spring Boot 应用打成可执行 Jar包很容易，只需要在 pom 中加上一个 Spring Boot 提供的插件，然后在执行mvn package即可
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
运行完mvn package后，我们会在 target 目录下看到两个 jar 文件。myproject-0.0.1-SNAPSHOT.jar 和 myproject-0.0.1-SNAPSHOT.jar.original。第一个 jar 文件就是我们应用的可执行 jar 包，第二个 Jar 文件是应用原始的 jar 包。

### 可执行 Jar 包内部结构
```text
可执行 jar 目录结构
├─BOOT-INF
│  ├─classes
│  └─lib
├─META-INF
│  ├─maven
│  ├─app.properties
│  ├─MANIFEST.MF      
└─org
    └─springframework
        └─boot
            └─loader
                ├─archive
                ├─data
                ├─jar
                └─util

```
我们先来重点关注两个地方：META-INF 下面的 Jar 包描述文件和 BOOT-INF 这个目录。

MANIFEST.MF 文件
```properties
Manifest-Version: 1.0
Archiver-Version: Plexus Archiver
Built-By: xxxx
Start-Class: com.xxxx.AppServer
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/lib/
Spring-Boot-Version: 2.1.6.RELEASE
Created-By: Apache Maven 3.3.9
Build-Jdk: 1.8.0_73
Main-Class: org.springframework.boot.loader.JarLauncher

```
在上面我们看到一个熟悉的配置Main-Class: org.springframework.boot.loader.JarLauncher。我们大概能猜到这个类是整个系统的入口。

再看下 BOOT-INF 这个目录下面，我们会发现里面是我们项目打出来的 class 文件和项目依赖的 Jar 包。看到这里，你可能已经猜到 Spring Boot 是怎么启动项目的了。

### JarLauncher
```java
public class JarLauncher extends ExecutableArchiveLauncher {

	static final String BOOT_INF_CLASSES = "BOOT-INF/classes/";

	static final String BOOT_INF_LIB = "BOOT-INF/lib/";

	public JarLauncher() {
	}

	protected JarLauncher(Archive archive) {
		super(archive);
	}

	@Override
	protected boolean isNestedArchive(Archive.Entry entry) {
		if (entry.isDirectory()) {
			return entry.getName().equals(BOOT_INF_CLASSES);
		}
		return entry.getName().startsWith(BOOT_INF_LIB);
	}

	public static void main(String[] args) throws Exception {
        //项目入口，重点在launch这个方法中
		new JarLauncher().launch(args);
	}

}

```
```java
//launch方法
protected void launch(String[] args) throws Exception {
    JarFile.registerUrlProtocolHandler();
    //创建LaunchedURLClassLoader。如果根类加载器和扩展类加载器没有加载到某个类的话，就会通过LaunchedURLClassLoader这个加载器来加载类。这个加载器会从Boot-INF下面的class目录和lib目录下加载类。
    ClassLoader classLoader = createClassLoader(getClassPathArchives());
    //这个方法会读取jar描述文件中的Start-Class属性，然后通过反射调用到这个类的main方法。
    launch(args, getMainClass(), classLoader);
}

```
简单总结
- Spring Boot 可执行 Jar 包的入口点是 JarLauncher 的 main 方法；
- 这个方法的执行逻辑是先创建一个 LaunchedURLClassLoader，这个加载器加载类的逻辑是：先判断根类加载器和扩展类加载器能否加载到某个类，如果都加载不到就从 Boot-INF 下面的 class 和 lib 目录下去加载；
- 读取Start-Class属性，通过反射机制调用启动类的 main 方法，这样就顺利调用到我们开发的 Spring Boot 主启动类的 main 方法了。
# 参考文章
- https://www.jianshu.com/p/ffe5ebe17c3a
- https://www.cnblogs.com/54chensongxia/p/11419796.html

