
* [spring](#spring)
  * [架构图](#架构图)
  * [模块](#模块)
    * [Core Container](#core-container)
    * [Data Access/Integration](#data-accessintegration)
    * [Web](#web)
    * [面向切面编程(AOP和Aspects)](#面向切面编程aop和aspects)
    * [设备(Instrumentation)](#设备instrumentation)
    * [消息(Messaging)](#消息messaging)
    * [测试(Test)](#测试test)
  * [IOC](#ioc)
    * [IOC和DI的概念](#ioc和di的概念)
      * [IOC (控制反转)](#ioc-控制反转)
      * [DI (依赖注入)](#di-依赖注入)
    * [使用IOC的好处](#使用ioc的好处)
    * [Spring IoC的初始化过程](#spring-ioc的初始化过程)
      * [IOC粗略总结](#ioc粗略总结)
      * [重要的组件](#重要的组件)
      * [源码解析](#源码解析)
    * [Spring bean的生命周期](#spring-bean的生命周期)
    * [bean的作用域](#bean的作用域)
    * [循环依赖问题](#循环依赖问题)
  * [AOP](#aop)
    * [AOP原理](#aop原理)
    * [AOP术语](#aop术语)
      * [连接点(Join point)](#连接点join-point)
      * [切点(Poincut)](#切点poincut)
      * [增强/通知(Advice)](#增强通知advice)
      * [织入(Weaving)](#织入weaving)
      * [引入/引介(Introduction)](#引入引介introduction)
      * [切面(Aspect)](#切面aspect)
    * [Spring对AOP的支持](#spring对aop的支持)
  * [怎么定义一个注解](#怎么定义一个注解)
    * [引入依赖](#引入依赖)
    * [定义注解](#定义注解)
      * [元注解](#元注解)
        * [@Retention – 定义该注解的生命周期](#retention--定义该注解的生命周期)
        * [@Target – 表示该注解用于什么地方。默认值为任何元素，表示该注解用于什么地方。可用的ElementType 参数包括](#target--表示该注解用于什么地方默认值为任何元素表示该注解用于什么地括)
        * [@Documented – 一个简单的Annotations 标记注解，表示是否将注解信息添加在java文档中。](#documented--一个简单的annotations-标记注解表示是否将注解信息添加在java文档中)
        * [@Inherited – 定义该注释和子类的关系](#inherited--定义该注释和子类的关系)
    * [示例](#示例)
  * [事务](#事务)
    * [Spring 支持两种方式的事务管理](#spring-支持两种方式的事务管理)
    * [事务的传播性 Propagation](#事务的传播性-propagation)
* [参考文章](#参考文章)


# spring
## 架构图
![](../img/spring/spring架构图.png)
## 模块
### Core Container
核心容器(Core Container)
- `spring-beans` 该模块是依赖注入IoC与DI的最基本实现
- `spring-core` 该模块是Bean工厂与bean的装配
- `spring-context` 该模块构架于核心模块之上，它扩展了 BeanFactory，为它添加了 Bean 生命周期控制、框架事件体系以及资源加载透明化等功能。ApplicationContext 是该模块的核心接口，它的超类是 BeanFactory。与BeanFactory 不同，ApplicationContext 容器实例化后会自动对所有的单实例 Bean 进行实例化与依赖关系的装配，使之处于待用状态
- `spring-context-indexer` 该模块是 Spring 的类管理组件和 Classpath 扫描
- `spring-context-support` 该模块是对 Spring IOC 容器的扩展支持，以及 IOC 子容器
- `spring-expression` 该模块是Spring表达式语言块是统一表达式语言（EL）的扩展模块，可以查询、管理运行中的对象，同时也方便的可以调用对象方法、操作数组、集合等
### Data Access/Integration
数据访问/集成 
- `spring-jdbc` 该模块提供了 JDBC抽象层，它消除了冗长的 JDBC 编码和对数据库供应商特定错误代码的解析
- `spring-tx` 该模块支持编程式事务和声明式事务，可用于实现了特定接口的类和所有的 POJO 对象。编程式事务需要自己写beginTransaction()、commit()、rollback()等事务管理方法，声明式事务是通过注解或配置由 spring 自动处理，编程式事务粒度更细
- `spring-orm` 该模块提供了对流行的对象关系映射 API的集成，包括 JPA、JDO 和 Hibernate 等。通过此模块可以让这些 ORM 框架和 spring 的其它功能整合，比如前面提及的事务管理
- `spring-oxm` 该模块提供了对 OXM 实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等
- `spring-jms` 该模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了 spring-messaging 模块
### Web
网络部分
- `spring-web` 该模块为 Spring 提供了最基础 Web 支持，主要建立于核心容器之上，通过 Servlet 或者 Listeners 来初始化 IOC 容器，也包含一些与 Web 相关的支持
- `spring-webmvc` 该模块众所周知是一个的 Web-Servlet 模块，实现了 Spring MVC（model-view-Controller）的 Web 应用
- `spring-websocket` 该模块主要是与 Web 前端的全双工通讯的协议
- `spring-webflux` 该模块是一个新的非堵塞函数式 Reactive Web 框架，可以用来建立异步的，非阻塞，事件驱动的服务，并且扩展性非常好。
### 面向切面编程(AOP和Aspects)
- `spring-aop` 该模块是Spring的另一个核心模块，是 AOP 主要的实现模块
- `spring-aspects` 该模块提供了对 AspectJ 的集成，主要是为 Spring AOP提供多种 AOP 实现方法，如前置方法后置方法等
### 设备(Instrumentation)
- `spring-instrument` 该模块是基于JAVA SE 中的"java.lang.instrument"进行设计的，应该算是 AOP的一个支援模块，主要作用是在 JVM 启用时，生成一个代理类，程序员通过代理类在运行时修改类的字节，从而改变一个类的功能，实现 AOP 的功能
### 消息(Messaging)
- `spring-messaging` 是从 Spring4 开始新加入的一个模块，主要职责是为 Spring 框架集成一些基础的报文传送应用
### 测试(Test)
- `spring-test` 主要为测试提供支持的，通过 JUnit 和 TestNG 组件支持单元测试和集成测试。它提供了一致性地加载和缓存 Spring 上下文，也提供了用于单独测试代码的模拟对象（mock object）
## IOC
### IOC是什么？

IOC（Inverse of Contro）控制反转，有时候也被称为DI（Dependency injection）依赖注入，它是一种降低对象耦合关系的一种设计思想。

2004年，Martin Fowler探讨了一个问题，既然IOC是控制反转，那么到底是哪些方面的控制被反转了呢？，经过详细地分析和论证后，他得出了答案：获得依赖对象的过程被反转了。控制被反转之后，获得依赖对象的过程由自身管理变为了由IOC容器主动注入。于是，他给“控制反转”取了一个更合适的名字叫做“依赖注入（Dependency Injection）”。他的这个答案，实际上给出了实现IOC的方法：注入。所谓依赖注入就是：由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。

控制反转（IOC）是一种思想，而依赖注入（Dependency Injection）则是实现这种思想的方法。

### 使用IOC的好处
- 不用自己组装，拿来就用。
- 享受单例的好处，效率高，不浪费空间
- 便于单元测试，方便切换mock组件
- 便于进行AOP操作，对于使用者是透明的
- 统一配置，便于修改
### Spring IoC的初始化过程
#### IOC粗略总结
1. 首先入口是xml或者注解或者其他形式，要实现beanDefinationReader接口，然后 读取的时候，会将他们解析为bean的定义信息；
2. beanFactory在加载bean信息实例化（底层用的反射）之前，spring加了一个接口beanFactoryPostProcessor,用作扩展用。
3. beanFactory内部实例化bean之后，在要初始化bean对象之前，增加了一个一系列aware接口，将他的容器，以及工厂都暴露出来供使用者做扩展用。
4. 经过一些列容器以及容器对象的注入之后，在初始化之前，spring又增加了一个接口 beanPostProcessor,该接口是可以作用于所有创建的bean,在初始化前后，均能通过重写该接口获取bean对象进行定制操作。
5. 经过实现初始化接口完成初始化功能。
6. 经过实现销毁接口disposableBean结束其生命。
#### 重要的组件
- `BeanDefinition` 描述bean的属性的接口，例如bean的scope是单例还是多例，构造方法，有哪些property value，依赖等，相当于对这个bean的一份身份描述
  - Bean配置 --> BeanDefinition --> Bean对象
  - 懒加载情况下，refresh只是把BeanDefinition注册到BeanFactory中，而不是把Bean注册到BeanFactory中。在调用上下文的getBean的时候才会去根据BeanDefinition生成具体的bean对象
- `BeanDefinitionMap`
- `BeanFactory`
  - spring的基础bean容器
  - 相当于存放所有bean的容器
- `ApplicationContext`
  - BeanFactory 的子接口，在 BeanFactory 的基础上构建，是相对比较高级的 IoC 容器实现。包含 BeanFactory 的所有功能，还提供了其他高级的特性，比如：事件发布、国际化信息支持、统一资源加载策略等。正常情况下，我们都是使用的 ApplicationContext
  - 相当于丰富了beanfactory的功能，这里理解为上下文就好
- `FactoryBean`
#### 源码解析
首先抛开其他组件的启动，我们只需要引入spring-context就可以启动一个容器了
```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
</dependency>
```
而在springboot出来之前最常见的加载bean的方式是读取配置文件
```java
public static void main(String[] args) {
    ApplicationContext context = new ClassPathXmlApplicationContext("classpath:applicationfile.xml");
}
```
这里ApplicationContext是一个接口，最要的实现类有：
- ClassPathXmlApplicationContext 需要一个 xml 配置文件在系统中的路径
- FileSystemXmlApplicationContext 需要一个 xml 配置文件在系统中的路径
- AnnotationConfigApplicationContext 基于注解，大势所趋

下面的分析都基于 ClassPathXmlApplicationContext 进行分析，因为比较好理解点

在 resources 目录新建一个配置文件，文件名随意，通常叫 application.xml 或 application-xxx.xml就可以了,对应的类实现一个：
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd" default-autowire="byName">
 
    <bean id="messageService" class="com.javadoop.example.MessageServiceImpl"/>
</beans>
```
main
```java
public class App {
    public static void main(String[] args) {
        // 用我们的配置文件来启动一个 ApplicationContext
        ApplicationContext context = new ClassPathXmlApplicationContext("classpath:application.xml");
 
        System.out.println("context 启动成功");
 
        // 从 context 中取出我们的 Bean，而不是用 new MessageServiceImpl() 这种方式
        MessageService messageService = context.getBean(MessageService.class);
        // 这句将输出: hello world
        System.out.println(messageService.getMessage());
    }
}
```
在构造方法中的refresh()方法是启动加载整个容器的关键方法

方法在springboot容器启动时也会加载,方法为 
- org.springframework.boot.SpringApplication#run
- org.springframework.boot.SpringApplication#refreshContext
```java
@Override
public void refresh() throws BeansException, IllegalStateException {
    // 1. 首先是一个synchronized加锁，当然要加锁，不然你先调一次refresh()然后这次还没处理完又调一次，就会乱套了；
    synchronized (this.startupShutdownMonitor) {
        // 2. 这个方法是做准备工作的，记录容器的启动时间、标记“已启动”状态、处理配置文件中的占位符，可以点进去看看，这里就不多说了。
        prepareRefresh();
        
        // 3. 这个就很重要了，这一步是把配置文件解析成一个个Bean，并且注册到BeanFactory中，注意这里只是注册进去，并没有初始化。先继续往下看，等会展开这个方法详细解读
        ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

        //4. 这个方法的作用是：设置 BeanFactory 的类加载器，添加几个 BeanPostProcessor，手动注册几个特殊的 bean，这里都是spring里面的特殊处理，然后继续往下看
        prepareBeanFactory(beanFactory);

        try {
            // 5. 方法是提供给子类的扩展点，到这里的时候，所有的 Bean 都加载、注册完成了，但是都还没有初始化，具体的子类可以在这步的时候添加一些特殊的 BeanFactoryPostProcessor 的实现类，来完成一些其他的操作。
            postProcessBeanFactory(beanFactory);

            // 6. 接下来是这个方法是调用 BeanFactoryPostProcessor 各个实现类的 postProcessBeanFactory(factory) 方法；
            invokeBeanFactoryPostProcessors(beanFactory);

            // 7. 然后这个方法注册 BeanPostProcessor 的实现类，和上面的BeanFactoryPostProcessor 是有区别的，这个方法调用的其实是PostProcessorRegistrationDelegate类的registerBeanPostProcessors方法；这个类里面有个内部类BeanPostProcessorChecker，BeanPostProcessorChecker里面有两个方法postProcessBeforeInitialization和postProcessAfterInitialization，这两个方法分别在 Bean 初始化之前和初始化之后得到执行。然后回到refresh()方法中继续往下看
            registerBeanPostProcessors(beanFactory);
            
            // 8. 方法是初始化当前 ApplicationContext 的 MessageSource，国际化处理，继续往下
            initMessageSource();

            // 9. 方法初始化当前 ApplicationContext 的事件广播器继续往下
            initApplicationEventMulticaster();

            // 10. 方法初始化一些特殊的 Bean（在初始化 singleton beans 之前）；继续往下
            onRefresh();

            // 11. 方法注册事件监听器，监听器需要实现 ApplicationListener 接口；继续往下
            registerListeners();

            // 12. 重点到了 初始化所有的 singleton beans（单例bean），懒加载（non-lazy-init）的除外，这个方法也是等会细说
            finishBeanFactoryInitialization(beanFactory);

            // 13. 方法是最后一步，广播事件，ApplicationContext 初始化完成
            finishRefresh();
        }

        catch (BeansException ex) {
            if (logger.isWarnEnabled()) {
                logger.warn("Exception encountered during context initialization - " +
                        "cancelling refresh attempt: " + ex);
            }

            // Destroy already created singletons to avoid dangling resources.
            // 销毁已经初始化的 singleton 的 Beans，以免有些 bean 会一直占用资源
            destroyBeans();

            // Reset 'active' flag.
            cancelRefresh(ex);

            // Propagate exception to caller.
            throw ex;
        }

        finally {
            // Reset common introspection caches in Spring's core, since we
            // might not ever need metadata for singleton beans anymore...
            resetCommonCaches();
        }
    }
}
```
### Spring bean的生命周期
Spring Bean的生命周期分为四个阶段和多个扩展点。扩展点又可以分为影响多个Bean和影响单个Bean。整理如下：

四个阶段
- 实例化 Instantiation
- 属性赋值 Populate
- 初始化 Initialization
- 销毁 Destruction

多个扩展点

- 影响多个Bean
  - BeanPostProcessor(作用于初始化阶段的前后)
  - InstantiationAwareBeanPostProcessor(作用于实例化阶段的前后)
- 影响单个Bean
  - Aware(Aware类型的接口的作用就是让我们能够拿到Spring容器中的一些资源)
    - Aware Group1
      - BeanNameAware
      - BeanClassLoaderAware
      - BeanFactoryAware
    - Aware Group2
      - EnvironmentAware
      - EmbeddedValueResolverAware(实现该接口能够获取Spring EL解析器，用户的自定义注解需要支持spel表达式的时候可以使用)
      - ApplicationContextAware(ResourceLoaderAware\ApplicationEventPublisherAware\MessageSourceAware)
  - 生命周期(实例化和属性赋值都是Spring帮助我们做的，能够自己实现的有初始化和销毁两个生命周期阶段)
    - InitializingBean
    - DisposableBean

### bean的作用域
Spring Bean 中所说的作用域，在配置文件中即是“scope”

在面向对象程序设计中作用域一般指对象或变量之间的可见范围。

而在Spring容器中是指其创建的Bean对象相对于其他Bean对象的请求可见范围。

在Spring 容器当中，一共提供了5种作用域类型，在配置文件中，通过属性scope来设置bean的作用域范围

#### singleton
```xml
<bean id="userInfo" class="cn.lovepi.UserInfo" scope="singleton"></bean>
```
当Bean的作用域为singleton的时候,Spring容器中只会存在一个共享的Bean实例，所有对Bean的请求只要id与bean的定义相匹配，则只会返回bean的同一实例。单一实例会被存储在单例缓存中，为Spring的缺省作用域。
#### prototype
```xml
<bean id="userInfo" class="cn.lovepi.UserInfo" scope=" prototype "></bean>
```
每次对该Bean请求的时候，Spring IoC都会创建一个新的作用域。

对于有状态的Bean应该使用prototype，对于无状态的Bean则使用singleton
#### request
```xml
<bean id="userInfo" class="cn.lovepi.UserInfo" scope=" request "></bean>
```
Request作用域针对的是每次的Http请求，Spring容器会根据相关的Bean的

定义来创建一个全新的Bean实例。而且该Bean只在当前request内是有效的。
#### session
```xml
<bean id="userInfo" class="cn.lovepi.UserInfo" scope=" session "></bean>
```
针对http session起作用，Spring容器会根据该Bean的定义来创建一个全新的Bean的实例。而且该Bean只在当前http session内是有效的。
#### global session
```xml
<bean id="userInfo" class="cn.lovepi.UserInfo" scope="globalSession"></bean>
```
类似标准的http session作用域，不过仅仅在基于portlet的web应用当中才有意义。Portlet规范定义了全局的Session的概念。他被所有构成某个portlet外部应用中的各种不同的portlet所共享。在global session作用域中所定义的bean被限定于全局的portlet session的生命周期范围之内。

### 循环依赖问题
![](../img/spring/循环依赖.png)
				
## AOP
### AOP原理
原理是在IOC过程中，创建bean实例时，最后都会对bean进行处理来实现增强，对于AOP来说就是创建代理类
- 底层是动态代理技术
  - JDK动态代理(基于接口)
  - CBLib动态代理(基于类)
  - 在Spring AOP中，如果使用的是单例，推荐使用CGLib代理
### AOP术语
#### 连接点(Join point)
能够被拦截的地方
#### 切点(Poincut)
具体定位的连接点
#### 增强/通知(Advice)
表示添加到切点的一段逻辑代码，并定位连接点的方位信息
#### 织入(Weaving)
将增强/通知添加到目标类的具体连接点上的过程。
#### 引入/引介(Introduction)
允许我们向现有的类添加新方法或属性。是一种特殊的增强！
#### 切面(Aspect)
切面由切点和增强/通知组成，它既包括了横切逻辑的定义、也包括了连接点的定义
### Spring对AOP的支持
- 基于代理的经典SpringAOP：需要实现接口，手动创建代理
- 纯POJO切面：使用XML配置，aop命名空间
- @AspectJ注解驱动的切面：使用注解的方式，这是最简洁和最方便的！

## 怎么定义一个注解

### 引入依赖
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```
### 定义注解
#### 元注解
java.lang.annotation 提供了四种元注解，专门注解其他的注解（在自定义注解的时候，需要使用到元注解）：
- @Documented – 注解是否将包含在JavaDoc中
- @Retention – 什么时候使用该注解
- @Target – 注解用于什么地方
- @Inherited – 是否允许子类继承该注解

##### @Retention – 定义该注解的生命周期
- RetentionPolicy.SOURCE : 在编译阶段丢弃。这些注解在编译结束之后就不再有任何意义，所以它们不会写入字节码。@Override, @SuppressWarnings都属于这类注解。
- RetentionPolicy.CLASS : 在类加载的时候丢弃。在字节码文件的处理中有用。注解默认使用这种方式
- RetentionPolicy.RUNTIME : 始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息。我们自定义的注解通常使用这种方式。

##### @Target – 表示该注解用于什么地方。默认值为任何元素，表示该注解用于什么地方。可用的ElementType 参数包括
- ElementType.CONSTRUCTOR: 用于描述构造器
- ElementType.FIELD: 成员变量、对象、属性（包括enum实例）
- ElementType.LOCAL_VARIABLE: 用于描述局部变量
- ElementType.METHOD: 用于描述方法
- ElementType.PACKAGE: 用于描述包
- ElementType.PARAMETER: 用于描述参数
- ElementType.TYPE: 用于描述类、接口(包括注解类型) 或enum声明

##### @Documented – 一个简单的Annotations 标记注解，表示是否将注解信息添加在java文档中。

##### @Inherited – 定义该注释和子类的关系
@Inherited 元注解是一个标记注解，@Inherited 阐述了某个被标注的类型是被继承的。如果一个使用了@Inherited 修饰的annotation 类型被用于一个class，则这个annotation 将被用于该class 的子类。

### 示例
自定义一个检查是否登录的注解
```java
@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface CheckLogin {

}
```
实现
```java
@Aspect
@Component
@Slf4j
@Order(1)
public class CheckLoginAspect {

    @Autowired
    RedisTemplate redisTemplate;

    @Before("execution(* *..controller..*(..))")
    public void before(JoinPoint joinPoint){
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();
        Method method = signature.getMethod();
        CheckLogin annotation = method.getAnnotation(CheckLogin.class);

        if (annotation == null){
            //获取类上注解
            annotation = joinPoint.getTarget().getClass().getAnnotation(CheckLogin.class);
        }
        if (annotation != null) {
            //获取到请求的属性
            ServletRequestAttributes attributes =
                    (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
            //获取到请求对象
            HttpServletRequest request = attributes.getRequest();
            String ssoToken = HttpUtil.getSsoToken(request);
            if(ssoToken != null){
                String loginUserTokenKey = AuthRedisKeyUtil.getLoginUserTokenKey(ssoToken);
                if (redisTemplate.hasKey(loginUserTokenKey)) {
                    //通过
                }else {
                    throw new LoginException("登录已过期");
                }
            }else {
                throw new IllegalRequestException("非法请求");
            }
        }
    }
}
```
使用
```java
@RestController
public class AccountController {

    @CheckLogin
    @GetMapping("/query")
    public JSONObject queryRegulation(Integer pageNum, Integer pageSize) {
          //....业务逻辑
    }
}
```

## 事务
### Spring 支持两种方式的事务管理
- 编程式事务管理
  - TransactionTemplate
    ![](../img/spring/SpringTransactionTemplate.png)				
  - TransactionManager
    ![](../img/spring/SpringTransactionManager.png)				
- 注解
  - @Transactional
### 事务的传播性 Propagation
- `REQUIRED` 这是默认的传播属性，如果外部调用方有事务，将会加入到事务，没有的话新建一个。
- `PROPAGATION_SUPPORTS` 如果当前存在事务，则加入到该事务；如果当前没有事务，则以非事务的方式继续运行。
- `PROPAGATION_NOT_SUPPORTED` 以非事务方式运行，如果当前存在事务，则把当前事务挂起。
- `PROPAGATION_NEVER` 以非事务方式运行，如果当前存在事务，则抛出异常。

# 参考文章
- https://www.jianshu.com/p/5e7c0713731f
- https://blog.csdn.net/nuomizhende45/article/details/81158383
- https://www.cnblogs.com/javazhiyin/p/10905294.html
- https://www.jianshu.com/p/1dec08d290c1
- https://blog.csdn.net/icarus_wang/article/details/51586776
- https://cloud.tencent.com/developer/article/1512235