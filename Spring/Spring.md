# spring

## 架构图

<img src="../img/spring/spring架构图.png" width="50%" />

## 模块

### Core Container

核心容器(Core Container)

- `spring-beans` 该模块是依赖注入IoC与DI的最基本实现
- `spring-core` 该模块是Bean工厂与bean的装配
- `spring-context` 该模块构架于核心模块之上，它扩展了 BeanFactory，为它添加了 Bean 生命周期控制、框架事件体系以及资源加载透明化等功能。ApplicationContext 是该模块的核心接口，它的超类是
  BeanFactory。与BeanFactory 不同，ApplicationContext 容器实例化后会自动对所有的单实例 Bean 进行实例化与依赖关系的装配，使之处于待用状态
- `spring-context-indexer` 该模块是 Spring 的类管理组件和 Classpath 扫描
- `spring-context-support` 该模块是对 Spring IOC 容器的扩展支持，以及 IOC 子容器
- `spring-expression` 该模块是Spring表达式语言块是统一表达式语言（EL）的扩展模块，可以查询、管理运行中的对象，同时也方便的可以调用对象方法、操作数组、集合等

### Data Access/Integration

数据访问/集成

- `spring-jdbc` 该模块提供了 JDBC抽象层，它消除了冗长的 JDBC 编码和对数据库供应商特定错误代码的解析
- `spring-tx` 该模块支持编程式事务和声明式事务，可用于实现了特定接口的类和所有的 POJO 对象。编程式事务需要自己写beginTransaction()、commit()、rollback()
  等事务管理方法，声明式事务是通过注解或配置由 spring 自动处理，编程式事务粒度更细
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

- `spring-instrument` 该模块是基于JAVA SE 中的"java.lang.instrument"进行设计的，应该算是 AOP的一个支援模块，主要作用是在 JVM
  启用时，生成一个代理类，程序员通过代理类在运行时修改类的字节，从而改变一个类的功能，实现 AOP 的功能

### 消息(Messaging)

- `spring-messaging` 是从 Spring4 开始新加入的一个模块，主要职责是为 Spring 框架集成一些基础的报文传送应用

### 测试(Test)

- `spring-test` 主要为测试提供支持的，通过 JUnit 和 TestNG 组件支持单元测试和集成测试。它提供了一致性地加载和缓存 Spring 上下文，也提供了用于单独测试代码的模拟对象（mock object）

## IOC

### IOC是什么？

控制反转即IoC (Inversion of Control)，它把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。所谓的“控制反转”概念就是对组件对象控制权的转移，从程序代码本身转移到了外部容器。

Spring IOC 负责创建对象，管理对象（通过依赖注入（DI），装配对象，配置对象，并且管理这些对象的整个生命周期。

### 使用IOC的好处

- 不用自己组装，拿来就用。
- 享受单例的好处，效率高，不浪费空间
- 便于单元测试，方便切换mock组件
- 便于进行AOP操作，对于使用者是透明的
- 统一配置，便于修改

## BeanFactory 和 ApplicationContext有什么区别

BeanFactory和ApplicationContext是Spring的两大核心接口，都可以当做Spring的容器。其中ApplicationContext是BeanFactory的子接口。

### 依赖关系

BeanFactory：是Spring里面最底层的接口，包含了各种Bean的定义，读取bean配置文档，管理bean的加载、实例化，控制bean的生命周期，维护bean之间的依赖关系。

ApplicationContext接口作为BeanFactory的派生，除了提供BeanFactory所具有的功能外，还提供了更完整的框架功能：

- 继承MessageSource，因此支持国际化。
- 统一的资源文件访问方式。
- 提供在监听器中注册bean的事件。
- 同时加载多个配置文件。
- 载入多个（有继承关系）上下文 ，使得每一个上下文都专注于一个特定的层次，比如应用的web层。

### 加载方式

BeanFactroy采用的是延迟加载形式来注入Bean的，即只有在使用到某个Bean时(调用getBean())
，才对该Bean进行加载实例化。这样，我们就不能发现一些存在的Spring的配置问题。如果Bean的某一个属性没有注入，BeanFacotry加载后，直至第一次使用调用getBean方法才会抛出异常。

ApplicationContext，它是在容器启动时，一次性创建了所有的Bean。这样，在容器启动时，我们就可以发现Spring中存在的配置错误，这样有利于检查所依赖属性是否注入。
ApplicationContext启动后预载入所有的单实例Bean，通过预载入单实例bean ,确保当你需要的时候，你就不用等待，因为它们已经创建好了。

相对于基本的BeanFactory，ApplicationContext 唯一的不足是占用内存空间。当应用程序配置Bean较多时，程序启动较慢。

### 创建方式

BeanFactory通常以编程的方式被创建，ApplicationContext还能以声明的方式创建，如使用ContextLoader。

### 注册方式

BeanFactory和ApplicationContext都支持BeanPostProcessor、BeanFactoryPostProcessor的使用，但两者之间的区别是：BeanFactory需要手动注册，而ApplicationContext则是自动注册。

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
    -
    懒加载情况下，refresh只是把BeanDefinition注册到BeanFactory中，而不是把Bean注册到BeanFactory中。在调用上下文的getBean的时候才会去根据BeanDefinition生成具体的bean对象
- `BeanDefinitionMap`
- `BeanFactory`
    - spring的基础bean容器
    - 相当于存放所有bean的容器
    - 主要负责管理和提供各种 bean 的生命周期
- `ApplicationContext`
    - BeanFactory 的子接口，在 BeanFactory 的基础上构建，是相对比较高级的 IoC 容器实现。包含 BeanFactory
      的所有功能，还提供了其他高级的特性，比如：事件发布、国际化信息支持、统一资源加载策略等。正常情况下，我们都是使用的 ApplicationContext
    - 相当于丰富了beanfactory的功能，这里理解为上下文就好
- `FactoryBean`
    - FactoryBean 是 Spring 提供的一个接口，允许开发者通过实现该接口来创建复杂的 bean 对象。
    - 用于自定义对象的创建过程
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
public static void main(String[]args){
        ApplicationContext context=new ClassPathXmlApplicationContext("classpath:applicationfile.xml");
}
```

这里ApplicationContext是一个接口，主要的实现类有：

- ClassPathXmlApplicationContext 需要一个 xml 配置文件在系统中的路径
- FileSystemXmlApplicationContext 需要一个 xml 配置文件在系统中的路径
- AnnotationConfigApplicationContext 基于注解，大势所趋

下面的分析都基于 ClassPathXmlApplicationContext 进行分析，因为比较好理解点

在 resources 目录新建一个配置文件，文件名随意，通常叫 application.xml 或 application-xxx.xml就可以了,对应的类实现一个：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
       default-autowire="byName">

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
public void refresh()throws BeansException,IllegalStateException{
    // 1. 首先是一个synchronized加锁，当然要加锁，不然你先调一次refresh()然后这次还没处理完又调一次，就会乱套了；
    synchronized (this.startupShutdownMonitor){
        // 2. 这个方法是做准备工作的，记录容器的启动时间、标记“已启动”状态、处理配置文件中的占位符，可以点进去看看，这里就不多说了。
        prepareRefresh();

        // 3. 这个就很重要了，这一步是把配置文件解析成一个个Bean，并且注册到BeanFactory中，注意这里只是注册进去，并没有初始化。先继续往下看，等会展开这个方法详细解读
        ConfigurableListableBeanFactory beanFactory=obtainFreshBeanFactory();

        //4. 这个方法的作用是：设置 BeanFactory 的类加载器，添加几个 BeanPostProcessor，手动注册几个特殊的 bean，这里都是spring里面的特殊处理，然后继续往下看
        prepareBeanFactory(beanFactory);

        try{
            // 5. 方法是提供给子类的扩展点，到这里的时候，所有的 Bean 都加载、注册完成了，但是都还没有初始化，具体的子类可以在这步的时候添加一些特殊的 BeanFactoryPostProcessor 的实现类，来完成一些其他的操作。
            postProcessBeanFactory(beanFactory);
    
            // 6. 接下来是这个方法是调用 BeanFactoryPostProcessor 各个实现类的 postProcessBeanFactory(factory) 方法；
            invokeBeanFactoryPostProcessors(beanFactory);
    
            // 7. 然后这个方法注册 BeanPostProcessor 的实现类，和上面的BeanFactoryPostProcessor 是有区别的，这个方法调用的其实是PostProcessorRegistrationDelegate类的registerBeanPostProcessors方法；
            // 这个类里面有个内部类BeanPostProcessorChecker，BeanPostProcessorChecker里面有两个方法postProcessBeforeInitialization和postProcessAfterInitialization，这两个方法分别在 Bean 初始化之前和初始化之后得到执行。
            // 然后回到refresh()方法中继续往下看
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
        } catch(BeansException ex){
            if(logger.isWarnEnabled()){
                logger.warn("Exception encountered during context initialization - "+"cancelling refresh attempt: "+ex);
            }

            // Destroy already created singletons to avoid dangling resources.
            // 销毁已经初始化的 singleton 的 Beans，以免有些 bean 会一直占用资源
            destroyBeans();
    
            // Reset 'active' flag.
            cancelRefresh(ex);
    
            // Propagate exception to caller.
            throw ex;
        } finally{
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
  - Spring 容器根据 bean 的定义创建一个 bean 实例。这可以通过调用构造函数或使用工厂方法实现。
- 属性赋值 Populate
    - Spring 容器将配置的属性值注入到 bean 中，这个过程可以通过依赖注入来完成，包括简单类型属性和引用其他 bean。
- 初始化 Initialization
    - 在 bean 属性设置完成后，Spring 调用初始化方法，确保 bean 在使用之前处于有效状态，且具备运行所需的所有配置和资源。可以通过以下方式实现：
        - @PostConstruct 注解的方法。
        - 实现 InitializingBean 接口，重写 afterPropertiesSet() 方法。
        - 在配置文件中指定初始化方法。
- 销毁 Destruction
    - 当 bean 的生命周期结束时，Spring 容器负责调用销毁方法。可以通过以下方式实现：
        - @PreDestroy 注解的方法。
        - 实现 DisposableBean 接口，重写 destroy() 方法。
        - 在配置文件中指定销毁方法。

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

类似标准的http session作用域，不过仅仅在基于portlet的web应用当中才有意义。Portlet规范定义了全局的Session的概念。他被所有构成某个portlet外部应用中的各种不同的portlet所共享。在global
session作用域中所定义的bean被限定于全局的portlet session的生命周期范围之内。

### 循环依赖问题

#### [三级缓存](#三级缓存)

Spring 解决循环依赖的核心就是提前暴露对象，而提前暴露的对象就是放置于第二级缓存中。下表是三级缓存的说明：

|名称|    描述|
| --- | --- |
|singletonObjects |    一级缓存，存放完整的 Bean。|
|earlySingletonObjects    |二级缓存，存放提前暴露的Bean，Bean 是不完整的，未完成属性注入和执行 init 方法。|
|singletonFactories    |三级缓存，存放的是 Bean 工厂，主要是生产 Bean，存放到二级缓存中。|

所有被Spring 管理的 Bean，最终都会存放在 singletonObjects 中，这里面存放的 Bean 是经历了所有生命周期的（除了销毁的生命周期），完整的，可以给用户使用的。

earlySingletonObjects 存放的是已经被实例化，但是还没有注入属性和执行 init 方法的 Bean。

singletonFactories 存放的是生产 Bean 的工厂。

Bean 都已经实例化了，为什么还需要一个生产 Bean 的工厂呢？这里实际上是跟 AOP 有关，如果项目中不需要为 Bean 进行代理，那么这个 Bean 工厂就会直接返回一开始实例化的对象，如果需要使用 AOP 进行代理，那么这个工厂就会发挥重要的作用了，这也是本文需要重点关注的问题之一。

#### 三级缓存的作用

- Spring 会先从一级缓存 singletonObjects 中尝试获取 Bean。
- 若是获取不到，而且对象正在建立中，就会尝试从二级缓存 earlySingletonObjects 中获取 Bean。
- 若还是获取不到，且允许从三级缓存 singletonFactories 中经过 singletonFactory 的 getObject() 方法获取 Bean 对象，就会尝试从三级缓存 singletonFactories 中获取 Bean。
- 若是在三级缓存中获取到了 Bean，会将该 Bean 存放到二级缓存中。


#### 解决循环依赖
Spring 是如何通过上面介绍的三级缓存来解决循环依赖的呢？这里只用 A，B 形成的循环依赖来举例：

1. 实例化 A，此时 A 还未完成属性填充和初始化方法（@PostConstruct）的执行，A 只是一个半成品。
2. 为 A 创建一个 Bean 工厂，并放入到  singletonFactories 中。
3. 发现 A 需要注入 B 对象，但是一级、二级、三级缓存均为发现对象 B。
4. 实例化 B，此时 B 还未完成属性填充和初始化方法（@PostConstruct）的执行，B 只是一个半成品。
5. 为 B 创建一个 Bean 工厂，并放入到  singletonFactories 中。
6. 发现 B 需要注入 A 对象，此时在一级、二级未发现对象 A，但是在三级缓存中发现了对象 A，从三级缓存中得到对象 A，并将对象 A 放入二级缓存中，同时删除三级缓存中的对象 A。（注意，此时的 A 还是一个半成品，并没有完成属性填充和执行初始化方法）
7. 将对象 A 注入到对象 B 中。
8. 对象 B 完成属性填充，执行初始化方法，并放入到一级缓存中，同时删除二级缓存中的对象 B。（此时对象 B 已经是一个成品）
9. 对象 A 得到对象 B，将对象 B 注入到对象 A 中。（对象 A 得到的是一个完整的对象 B）
10. 对象 A 完成属性填充，执行初始化方法，并放入到一级缓存中，同时删除二级缓存中的对象 A。

#### 为什么需要三级缓存，二级缓存能解决么
- 尝试使用两级缓存解决依赖冲突

第三级缓存的目的是为了延迟代理对象的创建，因为如果没有依赖循环的话，那么就不需要为其提前创建代理，可以将它延迟到初始化完成之后再创建。

既然目的只是延迟的话，那么我们是不是可以不延迟创建，而是在实例化完成之后，就为其创建代理对象，这样我们就不需要第三级缓存了。因此，我们可以将 addSingletonFactory() 方法进行改造。

```java
protected void addSingletonFactory(String beanName, ObjectFactory<?> singletonFactory) {
    Assert.notNull(singletonFactory, "Singleton factory must not be null");

    synchronized (this.singletonObjects) {
        // 判断一级缓存中不存在此对象
        if (!this.singletonObjects.containsKey(beanName)) { 
            // 直接从工厂中获取 Bean
            Object o = singletonFactory.getObject();

            // 添加至二级缓存中
            this.earlySingletonObjects.put(beanName, o);
            this.registeredSingletons.add(beanName);
        }
    }
}
```
这样的话，每次实例化完 Bean 之后就直接去创建代理对象，并添加到二级缓存中。

测试结果是完全正常的，Spring 的初始化时间应该也是不会有太大的影响，因为如果 Bean 本身不需要代理的话，是直接返回原始 Bean 的，并不需要走复杂的创建代理 Bean 的流程。

- 三级缓存的意义

测试证明，二级缓存也是可以解决循环依赖的。为什么 Spring 不选择二级缓存，而要额外多添加一层缓存，使用三级缓存呢？

如果 Spring 选择二级缓存来解决循环依赖的话，那么就意味着所有 Bean 都需要在实例化完成之后就立马为其创建代理，而 Spring 的设计原则是在 Bean 初始化完成之后才为其创建代理。

<font color="lightblue">
使用三级缓存而非二级缓存并不是因为只有三级缓存才能解决循环引用问题，其实二级缓存同样也能很好解决循环引用问题。使用三级而非二级缓存并非出于 IOC 的考虑，而是出于 AOP 的考虑，即若使用二级缓存，在 AOP 情形注入到其他 Bean的，不是最终的代理对象，而是原始对象。
</font>

## Spring框架中的单例bean是否线程安全

Spring框架中的单例bean是线程安全的吗？它是如何处理线程并发问题的?

不是，Spring框架中的单例bean不是线程安全的。

spring 中的 bean 默认是单例模式，spring 框架并没有对单例 bean 进行多线程的封装处理。实际上大部分 spring bean 是无状态的（比如 dao 类），在某种程度上来说 bean 也是安全的，但如果 bean
有状态的话（比如 view model ）就要开发者自己去保证线程安全了，最简单的就是改变 bean 的作用域，把“singleton”变更为“prototype”，这样请求 bean 相当于 new Bean()了， 保证线程安全了。

- 有状态就是有数据存储功能。
- 无状态就是不会保存数据。

Spring如何处理线程并发问题?

一般只有无状态的Bean才可以在多线程下共享，大部分是无状态的Bean。当存有状态的Bean的时候，spring一般是使用ThreadLocal进行处理，解决线程安全问题。

ThreadLocal和线程同步机制都是为了解决多线程中相同变量的访问冲突问题。 同步机制采用了“时间换空间”的方式，仅提供一份变量，不同的线程获取锁，没获得锁的线程则需要排队。而ThreadLocal采用了“空间换时间”的方式。
ThreadLocal会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。因为每一个线程都拥有自己的变量副本，所以没有相同变量的访问冲突问题。所以在编写多线程代码时，可以把不安全的变量封装进ThreadLocal。

## AOP

OOP(Object-Oriented Programming)面向对象编程，允许开发者定义纵向的关系，但并适用于定义横向的关系，导致了大量代码的重复，而不利于各个模块的重用。

AOP(Aspect-Oriented Programming)
，一般称为面向切面编程，作为面向对象的一种补充，用于将那些与业务无关，但却对多个对象产生影响的公共行为和逻辑，抽取并封装为一个可重用的模块，这个模块被命名为“切面”（Aspect），减少系统中的重复代码，降低了模块间的耦合度，同时提高了系统的可维护性。可用于权限认证、日志、事务处理等。

### AOP原理

原理是在IOC过程中，创建bean实例时，最后都会对bean进行处理来实现增强，对于AOP来说就是创建代理类

- 底层是动态代理技术
    - JDK动态代理(基于接口)
    - CGLib动态代理(基于类)
    - 在Spring AOP中，如果使用的是单例，推荐使用CGLib代理

### JDK动态代理

(一）实现原理

JDK的动态代理是基于反射实现。JDK通过反射，生成一个代理类，这个代理类实现了原来那个类的全部接口，并对接口中定义的所有方法进行了代理。当我们通过代理对象执行原来那个类的方法时，代理类底层会通过反射机制，回调我们实现的InvocationHandler接口的invoke方法。并且这个代理类是Proxy类的子类（记住这个结论，后面测试要用）。这就是JDK动态代理大致的实现方式。

（二）优点

JDK动态代理是JDK原生的，不需要任何依赖即可使用；

通过反射机制生成代理类的速度要比CGLib操作字节码生成代理类的速度更快；

（三）缺点

如果要使用JDK动态代理，被代理的类必须实现了接口，否则无法代理；

JDK动态代理无法为没有在接口中定义的方法实现代理，假设我们有一个实现了接口的类，我们为它的一个不属于接口中的方法配置了切面，Spring仍然会使用JDK的动态代理，但是由于配置了切面的方法不属于接口，为这个方法配置的切面将不会被织入。

JDK动态代理执行代理方法时，需要通过反射机制进行回调，此时方法执行的效率比较低；

### CGLib动态代理

（一）实现原理

CGLib实现动态代理的原理是，底层采用了ASM字节码生成框架，直接对需要代理的类的字节码进行操作，生成这个类的一个子类，并重写了类的所有可以重写的方法，在重写的过程中，将我们定义的额外的逻辑（简单理解为Spring中的切面）织入到方法中，对方法进行了增强。而通过字节码操作生成的代理类，和我们自己编写并编译后的类没有太大区别。

（二）优点

使用CGLib代理的类，不需要实现接口，因为CGLib生成的代理类是直接继承自需要被代理的类；

CGLib生成的代理类是原来那个类的子类，这就意味着这个代理类可以为原来那个类中，所有能够被子类重写的方法进行代理；

CGLib生成的代理类，和我们自己编写并编译的类没有太大区别，对方法的调用和直接调用普通类的方式一致，所以CGLib执行代理方法的效率要高于JDK的动态代理；

（三）缺点

由于CGLib的代理类使用的是继承，这也就意味着如果需要被代理的类是一个final类，则无法使用CGLib代理；

由于CGLib实现代理方法的方式是重写父类的方法，所以无法对final方法，或者private方法进行代理，因为子类无法重写这些方法；

CGLib生成代理类的方式是通过操作字节码，这种方式生成代理类的速度要比JDK通过反射生成代理类的速度更慢；

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

##### @Retention
定义该注解的生命周期

- RetentionPolicy.SOURCE : 在编译阶段丢弃。这些注解在编译结束之后就不再有任何意义，所以它们不会写入字节码。@Override, @SuppressWarnings都属于这类注解。
- RetentionPolicy.CLASS : 在类加载的时候丢弃。在字节码文件的处理中有用。注解默认使用这种方式
- RetentionPolicy.RUNTIME : 始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息。我们自定义的注解通常使用这种方式。

##### @Target
表示该注解用于什么地方。默认值为任何元素，表示该注解用于什么地方。可用的ElementType 参数包括

- ElementType.CONSTRUCTOR: 用于描述构造器
- ElementType.FIELD: 成员变量、对象、属性（包括enum实例）
- ElementType.LOCAL_VARIABLE: 用于描述局部变量
- ElementType.METHOD: 用于描述方法
- ElementType.PACKAGE: 用于描述包
- ElementType.PARAMETER: 用于描述参数
- ElementType.TYPE: 用于描述类、接口(包括注解类型) 或enum声明

##### @Documented
一个简单的Annotations 标记注解，表示是否将注解信息添加在java文档中。

##### @Inherited
定义该注释和子类的关系

@Inherited 元注解是一个标记注解，@Inherited 阐述了某个被标注的类型是被继承的。如果一个使用了@Inherited 修饰的annotation 类型被用于一个class，则这个annotation 将被用于该class
的子类。

### 示例

自定义一个检查是否登录的注解

```java

@Target({ElementType.TYPE, ElementType.METHOD})
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
    public void before(JoinPoint joinPoint) {
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();
        Method method = signature.getMethod();
        CheckLogin annotation = method.getAnnotation(CheckLogin.class);

        if (annotation == null) {
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
            if (ssoToken != null) {
                String loginUserTokenKey = AuthRedisKeyUtil.getLoginUserTokenKey(ssoToken);
                if (redisTemplate.hasKey(loginUserTokenKey)) {
                    //通过
                } else {
                    throw new LoginException("登录已过期");
                }
            } else {
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

#### 1、编程式事务管理

- TransactionTemplate

```java
@Autowired
private TransactionTemplate transactionTemplate;

public void testTransaction(){
    transactionTemplate.execute(new TransactionCallbackWithoutResult(){
        @Override
        protected void doInTransactionWithoutResult(TransactionStatus status){
                try{
                    //...业务代码
                }catch(Exception e){
                    status.setRollbackOnly();
                }
        }
    });
}
```

- TransactionManager

```java
    @Autowired
private PlatformTransactionManager transactionManager;

public void testTransaction2(){
        TransactionStatus status=transactionManager.getTransaction(new DefaultTransactionDefinition());
        try{
            //...业务代码
            transactionManager.commit(status);
        }catch(Exception e){
            transactionManager.rollback(status);
        }
}
```

#### 2、注解

- @Transactional

### 事务的传播性 Propagation

① PROPAGATION_REQUIRED：如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，该设置是最常用的设置。

② PROPAGATION_SUPPORTS：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行。

③ PROPAGATION_MANDATORY：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常。

④ PROPAGATION_REQUIRES_NEW：创建新事务，无论当前存不存在事务，都创建新事务。

⑤ PROPAGATION_NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。

⑥ PROPAGATION_NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。

⑦ PROPAGATION_NESTED：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则按REQUIRED属性执行。

### spring事务失效的场景

1. 非被Spring管理的Bean上的事务： 如果你在一个非被Spring容器管理的Bean（例如通过new关键字直接创建的对象）上使用事务注解，事务将不会生效。Spring的事务管理是基于AOP（面向切面编程）实现的，因此只能在由Spring容器管理的Bean上起作用。

2. 未捕获的异常： 如果在事务内发生未捕获的运行时异常，事务将回滚。但是，如果异常被捕获并在方法内处理，事务可能不会回滚。确保在事务边界内处理异常或者允许异常传播到事务管理器以便正确回滚。

    ```java
    @Transactional
    public void transactionalMethod() {
        try {
            // some code that may throw an exception
        } catch (Exception e) {
            // handle the exception (not recommended within a transaction)
        }
    }
    ```

3. 嵌套事务问题： Spring事务支持嵌套事务，但是嵌套事务的行为取决于底层事务管理器的支持。如果使用的事务管理器不支持嵌套事务，嵌套事务可能会被忽略，导致事务行为不一致。

4. 方法调用问题： Spring事务是通过AOP实现的，它依赖于代理对象来拦截方法调用并处理事务。如果你在同一个类内部调用一个带有事务注解的方法，事务可能不会起作用，因为代理对象无法拦截内部方法的调用。确保事务注解生效，要么调用方法是通过代理对象，要么通过self-invocation，例如通过this关键字。
    ```java
    @Transactional
    public class MyService {
        public void outerMethod() {
            innerMethod(); // Transactional annotation may not work here
            this.innerMethod(); // Transactional annotation should work here
        }
    
        @Transactional
        public void innerMethod() {
            // some transactional logic
        }
    }
    
    ```
5. 异步方法问题： 如果使用了异步方法（通过@Async注解），事务可能会失效。在异步方法内，事务上下文可能无法正确传播，导致事务不起作用。要在异步方法中使用事务，可以使用TransactionContext传播方式。


## spring使用的设计模式

### 简单工厂

**实现方式：**

BeanFactory。Spring中的BeanFactory就是简单工厂模式的体现，根据传入一个唯一的标识来获得Bean对象，但是否是在传入参数后创建还是传入参数前创建这个要根据具体情况来定。

**实现原理：**

bean容器的启动阶段：

读取bean的xml配置文件,将bean元素分别转换成一个BeanDefinition对象。
然后通过BeanDefinitionRegistry将这些bean注册到beanFactory中，保存在它的一个ConcurrentHashMap中。
将BeanDefinition注册到了beanFactory之后，在这里Spring为我们提供了一个扩展的切口，允许我们通过实现接口BeanFactoryPostProcessor
在此处来插入我们定义的代码。典型的例子就是：PropertyPlaceholderConfigurer，我们一般在配置数据库的dataSource时使用到的占位符的值，就是它注入进去的。

容器中bean的实例化阶段：

实例化阶段主要是通过反射或者CGLIB对bean进行实例化，在这个阶段Spring又给我们暴露了很多的扩展点：

各种的Aware接口 ，比如 BeanFactoryAware，对于实现了这些Aware接口的bean，在实例化bean时Spring会帮我们注入对应的BeanFactory的实例。 BeanPostProcessor接口
，实现了BeanPostProcessor接口的bean，在实例化bean时Spring会帮我们调用接口中的方法。 InitializingBean接口
，实现了InitializingBean接口的bean，在实例化bean时Spring会帮我们调用接口中的方法。 DisposableBean接口
，实现了DisposableBean接口的bean，在该bean死亡时Spring会帮我们调用接口中的方法。

**设计意义：**

松耦合。
可以将原来硬编码的依赖，通过Spring这个beanFactory这个工厂来注入依赖，也就是说原来只有依赖方和被依赖方，现在我们引入了第三方——spring这个beanFactory，由它来解决bean之间的依赖问题，达到了松耦合的效果.

bean的额外处理。 通过Spring接口的暴露，在实例化bean的阶段我们可以进行一些额外的处理，这些额外的处理只需要让bean实现对应的接口即可，那么spring就会在bean的生命周期调用我们实现的接口来处理该bean。[非常重要]

### 工厂方法

**实现方式：**

FactoryBean接口。

**实现原理：**

实现了FactoryBean接口的bean是一类叫做factory的bean。其特点是，spring会在使用getBean()调用获得该bean时，会自动调用该bean的getObject()
方法，所以返回的不是factory这个bean，而是这个bean.getOjbect()方法的返回值。

### 单例模式

Spring依赖注入Bean实例默认是单例的。

Spring的依赖注入（包括lazy-init方式）都是发生在AbstractBeanFactory的getBean里。getBean的doGetBean方法调用getSingleton进行bean的创建。

### 适配器模式

**实现方式：**

SpringMVC中的适配器HandlerAdatper。

**实现原理：**

HandlerAdatper根据Handler规则执行不同的Handler。

**实现过程：**

DispatcherServlet根据HandlerMapping返回的handler，向HandlerAdatper发起请求，处理Handler。

HandlerAdapter根据规则找到对应的Handler并让其执行，执行完毕后Handler会向HandlerAdapter返回一个ModelAndView，最后由HandlerAdapter向DispatchServelet返回一个ModelAndView。

### 装饰器模式

**实现方式：**

Spring中用到的包装器模式在类名上有两种表现：一种是类名中含有Wrapper，另一种是类名中含有Decorator。

**实质：**

动态地给一个对象添加一些额外的职责。

就增加功能来说，Decorator模式相比生成子类更为灵活。

### 代理模式

**实现方式：**

AOP底层，就是动态代理模式的实现。

**动态代理：**

在内存中构建的，不需要手动编写代理类

## spring中properties和yml的加载顺序

相同内容properties和yml的加载顺序是properties优先

## 使用@Autowired注解自动装配的过程是怎样的？

使用@Autowired注解来自动装配指定的bean。在使用@Autowired注解之前需要在Spring配置文件进行配置，<context:annotation-config />。

在启动spring
IoC时，容器自动装载了一个AutowiredAnnotationBeanPostProcessor后置处理器，当容器扫描到@Autowied、@Resource或@Inject时，就会在IoC容器自动查找需要的bean，并装配给该对象的属性。在使用@Autowired时，首先在容器中查询对应类型的bean：

- 如果查询结果刚好为一个，就将该bean装配给@Autowired指定的数据；
- 如果查询的结果不止一个，那么@Autowired会根据名称来查找；
- 如果上述查找的结果为空，那么会抛出异常。解决方法是，使用required=false。

## @Autowired和@Resource之间的区别

@Autowired可用于：构造函数、成员变量、Setter方法

@Autowired和@Resource之间的区别

- @Autowired默认是按照类型装配注入的，默认情况下它要求依赖对象必须存在（可以设置它required属性为false）。
- @Resource默认是按照名称来装配注入的，只有当找不到与名称匹配的bean才会按照类型来装配注入。

## Spring中BeanFactory与FactoryBean的区别

### BeanFactory

BeanFactory是一个接口，它是Spring中工厂的顶层规范，是SpringIoc容器的核心接口，它定义了getBean()、containsBean()等管理Bean的通用方法。Spring的容器都是它的具体实现如：

- DefaultListableBeanFactory
- XmlBeanFactory
- ApplicationContext

这些实现类又从不同的维度分别有不同的扩展。

### FactoryBean

首先它是一个Bean，但又不仅仅是一个Bean。它是一个能生产或修饰对象生成的工厂Bean，类似于设计模式中的工厂模式和装饰器模式。它能在需要的时候生产一个对象，且不仅仅限于它自身，它能返回任何Bean的实例。

FactoryBean表现的是一个工厂的职责。 即一个Bean A如果实现了FactoryBean接口，那么A就变成了一个工厂，根据A的名称获取到的实际上是工厂调用getObject()
返回的对象，而不是A本身，如果要获取工厂A自身的实例，那么需要在名称前面加上'&'符号。

- getObject('name')返回工厂中的实例
- getObject('&name')返回工厂本身的实例

# 参考文章

- https://www.jianshu.com/p/5e7c0713731f
- https://blog.csdn.net/nuomizhende45/article/details/81158383
- https://www.cnblogs.com/javazhiyin/p/10905294.html
- https://www.jianshu.com/p/1dec08d290c1
- https://blog.csdn.net/icarus_wang/article/details/51586776
- https://cloud.tencent.com/developer/article/1512235
- https://zhuanlan.zhihu.com/p/114244039
- https://blog.csdn.net/qq_41701956/article/details/116354268
- https://blog.csdn.net/weixin_41980692/article/details/105803311
- https://juejin.cn/post/6844903967600836621
- https://juejin.cn/post/6882266649509298189