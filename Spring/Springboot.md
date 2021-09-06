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
## 怎么让Spring把Body变成一个对象
- @RequestBody注解原理
- 详细看springmvc的处理流程
## SpringBoot的starter实现原理是什么？
原理就是因为在@EnableAutoConfiguration注解，会自动的扫描jar包下的META-INF/spring.factories文件的配置类，写在这里面的类都是需要被自动加载的