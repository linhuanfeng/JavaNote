## 其它

### typora快捷键

- 无序列表：- + 空格
- 有序列表：输入数字+“.”之后输入空格
- 任务列表：-[空格]空格 文字
- 标题：ctrl+数字
- 表格：ctrl+t
- 生成目录：`[TOC]`按回车
- 选中一整行：ctrl+l
- 选中单词：ctrl+d
- 选中相同格式的文字：ctrl+e
- 跳转到文章开头：ctrl+home
- 跳转到文章结尾：ctrl+end
- 搜索：ctrl+f
- 替换：ctrl+h
- 引用：输入>之后输入空格
- 代码块：ctrl+alt+f
- 加粗：ctrl+b
- 倾斜：ctrl+i
- 下划线：ctrl+u
- 删除线：alt+shift+5
- 插入图片：直接拖动到指定位置即可或者ctrl+shift+i
- 插入链接：ctrl + k
- 打开类结构： ctrl+f12
- ![image-20211016131100677](javaNote.assets/image-20211016131100677.png)

### idea

#### 微服务多个显示

view->tool windows->service

#### 一键启动多个微服务

+compound

#### 快捷键

- 全局查找: 双击shift: 


- 格式化代码：ctrl+alt+l 
- 整行上下移动：ctrl+shift+上下键
- 注释：ctrl+shirft+/
- 查看类的继承关系：ctrl+H
- 缩进:shift+tab / tab
- 查看文件popu : ctl+1e
- 弹窗类的方法：ctl+F12
- 生成try-catch：ctl+alt+t
- 抽取方法：ctrl+alt+m
- 查看方法直接跳转实现类：ctrl+alt+左键
- 查源码查看调用者：ctrl+alt+<-

### windows命令

```bash
services.msc 查看服务器（windows）

找到占用端口的进程
netstat -ano | findstr "4000"

找到继承名字
tasklist | findstr "20616"

杀死进程
taskkill /f /t /im "node.exe"

hexo clean // 删除public文件的内容
hexo g // 生成静态文件到public
hexo s // 本地运行
hexo d // 发布静态文件
博客标题
---
title
---
```

#### 无法打开文件，包含病毒

[博客](https://jingyan.baidu.com/article/36d6ed1fb7b35f1bce488379.html)

#### github加速

##### **通过修改 HOSTS 文件进行加速**

手动把cdn和ip地址绑定。

第一步：获取 github 的 global.ssl.fastly 地址访问：http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo 获取cdn和ip域名：

![连不上github怎么办，10种解决方案](javaNote.assets/1902a141641a5236004f666ef641dc64.png)

得到：199.232.69.194 [https://github.global.ssl.fastly.net](https://github.global.ssl.fastly.net/)

第二步：获取github.com地址

访问：https://github.com.ipaddress.com/#ipinfo 获取cdn和ip：

![连不上github怎么办，10种解决方案](javaNote.assets/d5e7e1b11d863b0018f3644714d4a25a.png)

得到：140.82.114.4 [http://github.com](http://github.com/)

第三步：修改 host 文件映射上面查找到的 IP

windows系统：

1、修改C:WindowsSystem32driversetchosts文件的权限，指定可写入：右击->hosts->属性->安全->编辑->点击Users->在Users的权限“写入”后面打勾。如下：

![连不上github怎么办，10种解决方案](javaNote.assets/066ef56066991694388d76bb24032389.png)

然后点击确定。

2、右击->hosts->打开方式->选定记事本（或者你喜欢的编辑器）->在末尾处添加以下内容：

```
199.232.69.194 github.global.ssl.fastly.net
140.82.114.4 github.com
```

#### vaware安装虚拟机

[博客](https://www.runoob.com/w3cnote/vmware-install-centos7.html)

#### 安装vueDevtools

1. 克隆

```
git clone -b v5.1.1 https://github.com/vuejs/devtools.git
cd devtools
```

2. 修改persistant属性为true

修改manifest.json文件中的persistant属性为true

3. npm i 安装依赖包
4. npm run build

5. 添加扩展程序
   点击Chrome浏览器右上角的三个点>更多工具>扩展程序>加载已解压的扩展程序>选定chrome文件夹，得到如下结果：

## Spring

### Bean的作用域

- **singleton** : IoC 容器中只有唯一的 bean 实例。Spring 中的 bean 默认都是单例的，是对单例设计模式的应用。
- **prototype** : 每次获取都会创建一个新的 bean 实例。也就是说，连续 `getBean()` 两次，得到的是不同的 Bean 实例。
- **request** （仅 Web 应用可用）: 每一次 HTTP 请求都会产生一个新的 bean（请求 bean），该 bean 仅在当前 HTTP request 内有效。
- **session** （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean（会话 bean），该 bean 仅在当前 HTTP session 内有效。
- **application/global-session** （仅 Web 应用可用）： 每个 Web 应用在启动时创建一个 Bean（应用 Bean），，该 bean 仅在当前应用启动时间内有效。
- **websocket** （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。

### Resource&Autowire

#### Resource

```
@Target({TYPE, FIELD, METHOD})
@Retention(RUNTIME)
public @interface Resource {
	String name() default "";
	Class<?> type() default java.lang.Object.class;
	...
}
```

jdk提供，默认按名称注入（找不到再按类型注入）。

可作用在类，字段，方法

#### Autowire

```
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
	boolean required() default true;
}
```

spring提供，默认按类型注入（找不到再按名称注入）。如果有多个，配合@Qualify(name="")指定名称使用（当然注入bean的时候可以使用@Primary）。

可作用在字段，方法，**构造方法**，注解

### VO&DTO&PO&DO%POJO

举个实际例子，你就了解各种OO

```
pubclic class Controller{
	public R save(VO){
		helloService.save(DTO);
	}
}
pubclic class HelloService(DTO){
	public String save(DTO){
		helloDao.save(PO);
	}
}
```

**VO**（View Object）：视图对象，用于展示层，它的作用是把某个指定页面（或组件）的所有数据封装起来。

**DTO**（Data Transfer Object）：泛指用于展示层与服务层之间的数据传输对象。

**PO**（Persistent Object）：持久化对象，它跟持久层（通常是关系型数据库）的数据结构形成一一对应的映射关系，如果持久层是关系型数据库，那么，数据表中的每个字段（或若干个）就对应PO的一个（或若干个）属性。等价于**Entity**。

**DO**（Domain Object）：领域对象，就是从现实世界中抽象出来的有形或无形的业务实体。

**POJO**（plain ordinary java object）纯的传统意义的 java 对象，最基本的 Java Bean ，只有属性字段及 setter 和 getter 方法，可认为是 DO/DTO/BO/VO 的统称。

Java Bean典型特征:

- 提供一个默认的无参构造函数。
- 需要被序列化并且实现了 Serializable 接口。
- 可能有一系列可读写属性，并且一般是 private 的。
- 可能有一系列的 getter 或 setter 方法。

### Spring IOC四种注入方式

setter方法，构造方法，字段，P命名空间

### Servlet

单例，线程不一定安全。

加载和实例化。

init方法 读取配置文件封装传递给ServletConfig

service

destory

#### 1、生命周期

[servlet](https://so.csdn.net/so/search?q=servlet&spm=1001.2101.3001.7020) 声明周期可以分四个阶段：

- 类装载过程
- init() 初始化过程
- service() 服务过程，选择doGet \ doPost
- destroy() 销毁过程

servlet接口如下

```java
public interface Servlet {


    void init(ServletConfig var1) throws ServletException;

    ServletConfig getServletConfig();

    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    String getServletInfo();

    void destroy();

}
```

1、创建servlet实例

时期：默认是第一个请求该servlet的时候就初始化此servlet，该servlet实例便一直存在，直到长

 时间不调用、服务器关闭才销毁 或者 类文件更新后重新载入 。也可手动设置：在服务器

 启动时便加载此servlet 。

```java
<servlet>

	<servlet-name>Xxx</servlet-name>

     <servlet-class>com.lingz.Xxx</servlet-class>

     <load-on-startup>1</load-on-startup>

</servlet>
```

2、init()初始化

 servlet实例一创建出来，便调用init(ServletConfig var1) 进行初始化， 其中的ServletConfig参数对象携带了该servlet的配置信息，比如初始化参数，此ServletConfig参数由服务器创建。

（1）那么，如何配置 servlet的初始化参数？

```java
<servlet>

	<servlet-name>Xxx</servlet-name>

	<servlet-class>com.lingz.Xxx</servlet-class>

  	<!--两个自定义的初始化参数-->

  	<init-param>

  		<param-name>value1</param-name>

  		<param-value>key1</param-value>

  	</init-param>

    　　<init-param>

  		<param-name>value2</param-name>

  		<param-value>key2</param-value>

  	</init-param>

</servlet>
```

 通过这种配置方式，就不需要在Servlet中添加、修改，直接修改xml文件即可。

（2）如何读取上面的参数呢？

 通过 ServletConfig类提供的 getInitParameter(String name) 获取初始化参数

```java
public interface ServletConfig {

    String getServletName();

    ServletContext getServletContext();

    String getInitParameter(String var1);

    Enumeration<String> getInitParameterNames();

}
```

（3）init(ServletConfig var1) 在Servlet生命周期中，只执行一次。并且是单线程执行，不需要担心多线程安全。

3、service() 服务过程

（1）请求发到对应的Servlet，Servlet调用service（）,service() 根据请求调用doGet \ doPost

 service方法是处理业务的核心。

（2）service() 与多线程

 servlet 是单例的，当多个请求请求同一个servlet时，需要主要注意线程安全，不过也存在可以不必考虑线程安全的情况。

①线程安全情况

- 如果service()方法没有访问Servlet的成员变量也没有访问全局的资源比如静态变量、文件、数据库连接等，而是只使用了当前线程自己的资源，比如非指向全局资源的临时变量、request和response对象等。该方法本身就是线程安全的，不必进行任何的同步控制。
- 如果service()方法访问了Servlet的成员变量，但是对该变量的操作是只读操作，该方法本身就是线程安全的，不必进行任何的同步控制。

②线程不安全情况

- 如果service()方法访问了全局的静态变量，如果同一时刻系统中也可能有其它线程访问该静态变量，如果既有读也有写的操作，通常需要加上同步控制语句。
- 如果service()方法访问了全局的资源，比如文件、数据库连接等，通常需要加上同步控制语句。

4 、destroy()销毁

 当web服务器认为此servlet没有存在的必要、类重新加载、服务器关闭、长时间未被访问，则可以从内存中销毁。而回收该Servlet内存前必须调用destroy()，web服务器保证该方法被调用时已经结束了请求调用的service()或等待剩余的请求执行完，并且不会再接收请求。当全部请求处理完并响应后，即可destroy() 并进行内存回收

 

#### 2、执行流程

通过上面的描述，其实我们对执行流程已有了大体的认知：

```markdown
1. 根据时机，Web容器加载对应的Servlet类,加载后进行init()初始化。
 - 设置了容器启动时初始化
 - 请求第一次请求此Servlet时初始化
 - Servlet类文件被更新后，重新装载Servlet

2. 接收到请求，容器根据配置将请求交给对应的Servlet，同时创建HttpServletRequest 和 HttpServletResponse 对象，一并交给Servlet。

3. 在service()中根据HttpServletRequest得请求类型等信息，调用doGet\doPost 进行业务处理。

4. 处理后通过HttpServletResponse获得相应信息，返回给Web容器。

5. Web容器再将响应返回给客户端。
```

### SpringBoot自动装配

SpringBootApplication被由下面三个注解标注

#### 1、@SpringBootConfiguration

#### 2、@EnableAutoConfiguration

使用@EnableAutoConfiguration开启自动装配，它又被@AutoConfigurationPackage和@Import(AutoConfigurationImportSelector.class)标注

@AutoConfigurationPackage负责扫描

@Import(AutoConfigurationImportSelector.class)导入了**AutoConfigurationImportSelector**这个类，由它扫描META-INFO下面的spring.factories里面的类，类似Java SPI机制。

自动配置类本身也是条件加载，注入各种需要的类

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass(RedisOperations.class)
@EnableConfigurationProperties(RedisProperties.class)
@Import({ LettuceConnectionConfiguration.class, JedisConnectionConfiguration.class })
public class RedisAutoConfiguration {

	@Bean
	@ConditionalOnMissingBean(name = "redisTemplate")
	@ConditionalOnSingleCandidate(RedisConnectionFactory.class)
	public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
		RedisTemplate<Object, Object> template = new RedisTemplate<>();
		template.setConnectionFactory(redisConnectionFactory);
		return template;
	}
```



```java
	/**
	 * Return the {@link AutoConfigurationEntry} based on the {@link AnnotationMetadata}
	 * of the importing {@link Configuration @Configuration} class.
	 * @param annotationMetadata the annotation metadata of the configuration class
	 * @return the auto-configurations that should be imported
	 */
	protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
		if (!isEnabled(annotationMetadata)) {
			return EMPTY_ENTRY;
		}
		AnnotationAttributes attributes = getAttributes(annotationMetadata);
		List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes); // 获取spring.factories中的全类名
		configurations = removeDuplicates(configurations);
		Set<String> exclusions = getExclusions(annotationMetadata, attributes);
		checkExcludedClasses(configurations, exclusions);
		configurations.removeAll(exclusions);
		configurations = getConfigurationClassFilter().filter(configurations);
		fireAutoConfigurationImportEvents(configurations, exclusions);
		return new AutoConfigurationEntry(configurations, exclusions);
	}
```



AutoConfigurationImportSelector中getCandidateConfigurations方法类似Java SPI负责扫描META-INF/spring.factories下的包

```java
	protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
		List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
				getBeanClassLoader());
		Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
				+ "are using a custom packaging, make sure that file is correct.");
		return configurations;
	}
```

#### 3、@ComponentScan

### Spring事务传播行为

事务传播行为是为了解决业务层方法之间互相调用的事务问题。

当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行。

正确的事务传播行为可能的值如下:TransactionDefinition.PROPAGATION_**

#### 1.REQUIRED

使用的最多的一个事务传播行为，我们平时经常使用的`@Transactional`注解**默认使用**就是这个事务传播行为。如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。

#### 2.REQUIRES_NEW

创建一个新的事务，如果当前存在事务，则把当前事务挂起。也就是说不管外部方法是否开启事务，`Propagation.REQUIRES_NEW`修饰的内部方法会**新开启自己的事务**，且开启的事务相互独立，互不干扰。

#### 3.NESTED

如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于`TransactionDefinition.PROPAGATION_REQUIRED`。

#### 4.MANDATORY

如果当前存在事务，则加入该事务；如果当前没有事务，则**抛出异常。（mandatory：强制性）**

这个使用的很少。

若是错误的配置以下 3 种事务传播行为，事务将不会发生回滚：

- **SUPPORTS**: 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
- **NOT_SUPPORTED**: 以非事务方式运行，如果当前存在事务，则把当前**事务挂起**。
- **NEVER**: 以非事务方式运行，如果当前存在事务，则**抛出异常**

### Spring设计模式

#### 1、简单工厂

spring中的BeanFactory就是简单工厂模式的体现，**传入id来获取bean对象**

#### 2、工厂方法

通常由应用程序直接使用new创建新的对象，为了将对象的创建和使用相分离，采用工厂模式，即应用程序将对象的创建及初始化职责交给工厂对象。

实现了**FactoryBean**接口的bean是一类叫做factory的bean。其特点是，spring会在使用getBean()调 用获得该bean时，会自动调用该bean的getObject()方法，所以返回的不是factory这个bean，而是这个 bean.getOjbect()方法的返回值。

#### 3、单例模式

spring的bean模式都是单例的 **singleton**

#### 4、代理模式

切面在应用运行的时刻被织入。一般情况下，在织入切面时，**AOP**容器会为目标对象创建动态的创建一个代理 对象。SpringAOP就是以这种方式织入切面的。

织入：把切面应用到目标对象并创建新的代理对象的过程。

#### 5、模板方法

各种**template**，但是 Spring 并没有使用这种方式，而是使用Callback 模式与模板方法模式配合，既达到了代码复用的效果，同时增加了灵活性。

spring启动流程有个**onRefresh()**方法是空方法，留给子类来重写，在springboot中来内嵌tomcat。

模板方法：**不改变算法的骨架**而重定义该算法的某些具体实现

#### 6、适配器模式

在**Spring MVC中的HandlerAdapter**

当Spring容器启动后，会将所有定义好的适配器对象存放在一个List集合中，当一个请求来临时，DispatcherServlet会通过handler的类型找到对应适配器，并将该适配器对象返回给用户，然后就可以统一通过适配器的hanle()方法来调用Controller中的用于处理请求的方法。

#### 7、装饰器模式

**不改变原类的情况下动态功能增强**，通过组合的方式

Spring中用到的包装器模式在类名上有两种表现：一种是类名中含有**Wrapper**，另一种是类名中含有 **Decorator**。

#### 8、观察者模式

spring的**事件驱动模型**使用的是观察者模式，**listener**的实现

#### 9、策略模式

在不同的场景下切换不同的算法，可以替代代码中大量的 if-else。

### @lookup

https://blog.csdn.net/Wisimer/article/details/110880047

1、**单例bean**获取**原型bean**，为了每次**获取到最新的实例**，spring提供了方法级别的注入,实现了与spring代码的解耦
2、原理是当调用这个方法的时候，spring使用**cglib动态代理**，调用代理方法**获取proto最新的对象**
3、实现**解耦**：如果使用applicationContext获取到bean的话，就跟spring代码耦合了；@Autowire的话只能得到最初的bean

应用场景：lookup-method 方 法的返回值对象即可实现动态的对象返回。 

 在工厂方法难以定制的时候使用。 也是模板的一种应用。是工厂方法的扩展。 如：工厂方法返回对象类型为接口类型。且不同版本应用返回的对象未必相同时使用。 可以避免多次开发工厂类。

```java
@RestController
@RequestMapping("/lookup")
public class LookUpTest {

    @GetMapping("/proto")
    public String toy(){
        Toy toy = getToy();
        return "利用ciglib自动获取最新的proto对象:"+toy;
    }

    @Lookup // 自动获取最新的proto对象
    public Toy getToy(){
        return null;
    }
}

@Component
@Scope(scopeName = ConfigurableBeanFactory.SCOPE_PROTOTYPE) // 原型bean
public class Toy {
    public Toy(){
        System.out.println("create proto 对象");
    }
}

```

@replaced-method原理类似，动态替换掉 bean 中的一些方法

### IOC

有很多够钩子函数，主要分为BeanFactoryPostProcessor，BeanPostProcessor

#### refresh方法（spring启动流程）

首先，总体下refresh主要干了什么事

1、记录下容器的启动时间、标记“已启动”状态

2、创建容器DefaultListableBeanFactory，并加载beanDefinitions

3、对容器进行配置，比如注册类加载器ClassLoader和post-processors

4、调用 BeanFactoryPostProcessor 的 postProcessBeanFactory ，可对beanDefinition进行修改

5、注册 BeanPostProcessor 的实现类，可用于拦截bean的创建过程

6、国际化，事件广播器

7、初始化所有的 singleton beans（重点重点）

8、最后，广播事件，ApplicationContext 初始化完成



接下来，对代码逐行解析

```java
@Override
public void refresh() throws BeansException, IllegalStateException {
   // 来个锁，不然 refresh() 还没结束，你又来个启动或销毁容器的操作，那不就乱套了嘛
   synchronized (this.startupShutdownMonitor) {

      // 准备工作，记录下容器的启动时间、标记“已启动”状态、处理配置文件中的占位符
      prepareRefresh();
	
      // 创建新的容器。DefaultListableBeanFactory,有旧的容器进行关闭，
      // 自定义beanFactory。(beanFactory.setAllowBeanDefinitionOverriding,setAllowCircularReferences)
      // 加载beanDefinitions。将配置文件就会解析成一个个 BeanDefinition 定义，注册到BeanFactory的map中（beanName-> beanDefinition）
      // 当然，这里说的 Bean 还没有初始化，只是配置信息都提取出来了，
      ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory(); // 调用refreshBeanFactory

      // 设置 BeanFactory 的类加载器，添加几个BeanPostProcessor（ApplicationContextAwareProcessor，ApplicationListenerDetector，LoadTimeWeaverAwareProcessor），手动注册几个特殊的 bean(environment,systemProperties)
      prepareBeanFactory(beanFactory);

      try {
         // Bean 如果实现了BeanFactoryPostProcessor接口，那么在容器初始化以后，Spring 会负责调用里面的 postProcessBeanFactory 方法。

         // 这里是提供给子类的扩展点，到这里的时候，所有的Bean都加载、注册完成了，但是都还没有初始化
         // 子类可添加BeanFactoryPostProcessor的实现类修改beanDefinition
         postProcessBeanFactory(beanFactory);
         // 调用 BeanFactoryPostProcessor 各个实现类的 postProcessBeanFactory(factory) 方法，可修改beanDefinition
         invokeBeanFactoryPostProcessors(beanFactory);

         // 注册 BeanPostProcessor 的实现类，可用于拦截bean的创建过程
         // 此接口两个方法: postProcessBeforeInitialization 和 postProcessAfterInitialization
         // 两个方法分别在 Bean 初始化之前和初始化之后得到执行。注意，到这里 Bean 还没初始化
         registerBeanPostProcessors(beanFactory);

         // 初始化当前 ApplicationContext 的 MessageSource，国际化这里就不展开说了，不然没完没了了
         initMessageSource();

         // 初始化当前 ApplicationContext 的事件广播器，这里也不展开了
         initApplicationEventMulticaster();

         // 从方法名就可以知道，典型的模板方法(钩子方法)，
         // 具体的子类可以在这里初始化一些特殊的 Bean（在初始化 singleton beans 之前）
         onRefresh();

         // 注册事件监听器，监听器需要实现 ApplicationListener 接口。这也不是我们的重点，过
         registerListeners();

         // 重点，重点，重点
         // 初始化所有的 singleton beans
         //（lazy-init 的除外）
         finishBeanFactoryInitialization(beanFactory);

         // 最后，广播事件，ApplicationContext 初始化完成
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

         // 把异常往外抛
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

refreshBeanFactory

```java
@Override
protected final void refreshBeanFactory() throws BeansException {
   // 如果 ApplicationContext 中已经加载过 BeanFactory 了，销毁所有 Bean，关闭 BeanFactory
   // 注意，应用中 BeanFactory 本来就是可以多个的，这里可不是说应用全局是否有 BeanFactory，而是当前
   // ApplicationContext 是否有 BeanFactory
   if (hasBeanFactory()) {
      destroyBeans();
      closeBeanFactory();
   }
   try {
      // 初始化一个 DefaultListableBeanFactory，为什么用这个，我们马上说。
      DefaultListableBeanFactory beanFactory = createBeanFactory();
      // 用于 BeanFactory 的序列化，我想不部分人应该都用不到
      beanFactory.setSerializationId(getId());

      // 下面这两个方法很重要，别跟丢了，具体细节之后说
      // 设置 BeanFactory 的两个配置属性：是否允许 Bean 覆盖、是否允许循环引用
      customizeBeanFactory(beanFactory);

      // 加载 Bean 到 BeanFactory 中
      loadBeanDefinitions(beanFactory);
      synchronized (this.beanFactoryMonitor) {
         this.beanFactory = beanFactory;
      }
   }
   catch (IOException ex) {
      throw new ApplicationContextException("I/O error parsing bean definition source for " + getDisplayName(), ex);
   }
}
```



doCreateBean 真正创建bean和初始化，依赖注入，循环依赖

```java
protected Object doCreateBean(final String beanName, final RootBeanDefinition mbd, final @Nullable Object[] args)
			throws BeanCreationException {

		// Instantiate the bean. 实例化bean
		BeanWrapper instanceWrapper = null;
		if (mbd.isSingleton()) {
			instanceWrapper = this.factoryBeanInstanceCache.remove(beanName);
		}
		if (instanceWrapper == null) {
			instanceWrapper = createBeanInstance(beanName, mbd, args); // 构造器推断，反射创建bean实例
		}
		final Object bean = instanceWrapper.getWrappedInstance();
		Class<?> beanType = instanceWrapper.getWrappedClass();
		if (beanType != NullBean.class) {
			mbd.resolvedTargetType = beanType;
		}

		// Allow post-processors to modify the merged bean definition.
		synchronized (mbd.postProcessingLock) {
			if (!mbd.postProcessed) {
				try {
					applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
				}
				catch (Throwable ex) {
					throw new BeanCreationException(mbd.getResourceDescription(), beanName,
							"Post-processing of merged bean definition failed", ex);
				}
				mbd.postProcessed = true;
			}
		}

		// Eagerly cache singletons to be able to resolve circular references
		// even when triggered by lifecycle interfaces like BeanFactoryAware.
		boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
				isSingletonCurrentlyInCreation(beanName));
		if (earlySingletonExposure) {
			if (logger.isTraceEnabled()) {
				logger.trace("Eagerly caching bean '" + beanName +
						"' to allow for resolving potential circular references");
			}
			addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
		}

		// Initialize the bean instance.
		Object exposedObject = bean;
		try {
			populateBean(beanName, mbd, instanceWrapper); // 属性注入
			exposedObject = initializeBean(beanName, exposedObject, mbd); // 处理各种回调 BP initializeBean
		}
		...

		if (earlySingletonExposure) {
			Object earlySingletonReference = getSingleton(beanName, false);
			if (earlySingletonReference != null) {
				if (exposedObject == bean) {
					exposedObject = earlySingletonReference;
				}
				else if (!this.allowRawInjectionDespiteWrapping && hasDependentBean(beanName)) {
					String[] dependentBeans = getDependentBeans(beanName);
					Set<String> actualDependentBeans = new LinkedHashSet<>(dependentBeans.length);
					for (String dependentBean : dependentBeans) {
						if (!removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
							actualDependentBeans.add(dependentBean);
						}
					}
					if (!actualDependentBeans.isEmpty()) {
						throw new BeanCurrentlyInCreationException(beanName,
								"Bean with name '" + beanName + "' has been injected into other beans [" +
								StringUtils.collectionToCommaDelimitedString(actualDependentBeans) +
								"] in its raw version as part of a circular reference, but has eventually been " +
								"wrapped. This means that said other beans do not use the final version of the " +
								"bean. This is often the result of over-eager type matching - consider using " +
								"'getBeanNamesOfType' with the 'allowEagerInit' flag turned off, for example.");
					}
				}
			}
		}

		// Register bean as disposable.
		try {
			registerDisposableBeanIfNecessary(beanName, bean, mbd);
		}
		catch (BeanDefinitionValidationException ex) {
			throw new BeanCreationException(
					mbd.getResourceDescription(), beanName, "Invalid destruction signature", ex);
		}

		return exposedObject;
	}
```

initializeBean aware接口、 BeanPostProcessor的BeforeInitialization回调、 InitializingBean的afterPropertiesSet、BeanPostProcessor的AfterInitialization回调

```java
	protected Object initializeBean(final String beanName, final Object bean, @Nullable RootBeanDefinition mbd) {
		if (System.getSecurityManager() != null) {
			AccessController.doPrivileged((PrivilegedAction<Object>) () -> {
				invokeAwareMethods(beanName, bean);
				return null;
			}, getAccessControlContext());
		}
		else {
			invokeAwareMethods(beanName, bean); // 如果bean实现了BeanNameAware，BeanClassLoaderAware，BeanFactoryAware接口
		}

		Object wrappedBean = bean;
		if (mbd == null || !mbd.isSynthetic()) { // BeanPostProcessor的BeforeInitialization回调
			wrappedBean = applyBeanPostProcessorsBeforeInitialization(wrappedBean, beanName);
		}

		try {
            // InitializingBean的afterPropertiesSet
            // init-method
			invokeInitMethods(beanName, wrappedBean, mbd); 
		}
		catch (Throwable ex) {
			throw new BeanCreationException(
					(mbd != null ? mbd.getResourceDescription() : null),
					beanName, "Invocation of init method failed", ex);
		}
		if (mbd == null || !mbd.isSynthetic()) { // BeanPostProcessor的AfterInitialization回调
			wrappedBean = applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName);
		}

		return wrappedBean;
	}
```



```java
	protected void invokeInitMethods(String beanName, final Object bean, @Nullable RootBeanDefinition mbd)
			throws Throwable {
			...
				((InitializingBean) bean).afterPropertiesSet();
			...
		}
```

model和session

```
session数据保存在服务器，model数据放入视图中,存入request域中。
session可以在不同页面使用。model只能在Controller返回的页面使用
```

#### Bean生命周期

https://www.cnblogs.com/zrtqsk/p/3735273.html

```
现在开始初始化容器

这是BeanFactoryPostProcessor实现类构造器！！
BeanFactoryPostProcessor调用postProcessBeanFactory方法

这是BeanPostProcessor实现类构造器！！
这是InstantiationAwareBeanPostProcessorAdapter实现类构造器！！

InstantiationAwareBeanPostProcessor调用postProcessBeforeInstantiation方法
【构造器】调用Person的构造器实例化
InstantiationAwareBeanPostProcessor调用postProcessPropertyValues方法

【注入属性】注入属性address
【注入属性】注入属性name
【注入属性】注入属性phone

【BeanNameAware接口】调用BeanNameAware.setBeanName()
【BeanFactoryAware接口】调用BeanFactoryAware.setBeanFactory()

BeanPostProcessor接口方法postProcessBeforeInitialization对属性进行更改！
【InitializingBean接口】调用InitializingBean.afterPropertiesSet()
【init-method】调用<bean>的init-method属性指定的初始化方法
BeanPostProcessor接口方法postProcessAfterInitialization对属性进行更改！

InstantiationAwareBeanPostProcessor调用postProcessAfterInitialization方法

容器初始化成功
Person [address=广州, name=张三, phone=110]
现在开始关闭容器！
【DiposibleBean接口】调用DiposibleBean.destory()
【destroy-method】调用<bean>的destroy-method属性指定的初始化方法
```



![img](javaNote.assets/181453414212066.png)

![img](javaNote.assets/181454040628981.png)

```java
单例bean实例化后调用的方法
// Callback interface triggered at the end of the singleton pre-instantiation phase
// during {@link BeanFactory} bootstrap.
public interface SmartInitializingSingleton {

	void afterSingletonsInstantiated();

}

通过CommandLineRunner接口，可以实现在Spring Boot完全启动后执行一些代码逻辑
```

postProcessBeanDefinitionRegistry负责扫描注解变成beanDefinition对象，放入Map中

![img](javaNote.assets/2020072612595369.png)

### AOP

 AOP（Aspect Orient Programming），作为面向对象编程的一种补充，应用于具有**横切性质的系统级服务**，如**事务**管理、**安全检查**、缓存、对象池管理等、**日志**。AOP 代理则可分为静态代理和动态代理两大类：

#### 静态代理

在编译阶段就可生成 AOP 代理类，因此也称为编译时增强，**ApectJ主要采用的是编译期织入**，在这个期间使用AspectJ的acj编译器(类似javac)把aspect类编译成class字节码后，在java目标类编译时织入，即先编译aspect类再编译目标类。

#### 动态代理

##### jdk动态代理是：反射匿名类

- 利用反射机制 生成一个
- **实现代理接口的匿名类**
- 在调用具体方法前调用InvokeHandler来处理。

##### CGLIB字节码生成：字节码生成

- 利用asm开源包，
- 对代理**对象类的class文件** 加载进来，
- 通过**修改其字节码**生成子类来处理。

1、如果目标对象实现了接口，

- 默认 情况下会 采用JDK的动态代理实现AOP

2、如果目标对象实现了接口，可以强制使用CGLIB实现AOP

3、如果目标对象没有实现了接口，

- 必须采用CGLIB库，spring会自动在JDK动态代理和CGLIB之间转换

##### 如何强制使用CGLIB实现AOP？

（1）添加CGLIB库，SPRING_HOME/cglib/*.jar
（2）在spring配置文件中加入<aop:aspectj-autoproxy proxy-target-class=“true”/>

JDK动态代理和CGLIB字节码生成的区别？
（1）JDK动态代理只能 对实现了接口的类 生成代理，而不能针对类
（2）CGLIB是针对 类 实现代理，

- 主要是对指定的类生成一个子类，
- 覆盖其中的方法
- 因为是继承，所以该类或方法最好不要声明成final

##### 代码实现

用户管理接口

```java
//用户管理接口
public interface UserManager {
    //新增用户抽象方法
    void addUser(String userName,String password);
    //删除用户抽象方法
    void delUser(String userName);
    
}
12345678
```

用户管理接口实现类

```java
//用户管理实现类,实现用户管理接口
public class UserManagerImpl implements UserManager{
    //重写新增用户方法
    @Override
    public void addUser(String userName, String password) {
        System.out.println("调用了新增的方法！");
        System.out.println("传入参数为 userName: "+userName+" password: "+password);
    }
    //重写删除用户方法
    @Override
    public void delUser(String userName) {
        System.out.println("调用了删除的方法！");
        System.out.println("传入参数为 userName: "+userName);
    }
    
}
12345678910111213141516
```

###### JDK动态代理

```java
//JDK动态代理实现InvocationHandler接口
public class JdkProxy implements InvocationHandler {
    private Object target ;//需要代理的目标对象
    
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("JDK动态代理，监听开始！");
        Object result = method.invoke(target, args);
        System.out.println("JDK动态代理，监听结束！");
        return result;
    }
    //定义获取代理对象方法
    private Object getJDKProxy(Object targetObject){
        //为目标对象target赋值
        this.target = targetObject;
        //JDK动态代理只能针对实现了接口的类进行代理，newProxyInstance 函数所需参数就可看出
        return Proxy.newProxyInstance(targetObject.getClass().getClassLoader(), targetObject.getClass().getInterfaces(), this);
    }
    
    public static void main(String[] args) {
        JdkProxy jdkProxy = new JdkProxy();//实例化JDKProxy对象
        UserManager user = (UserManager) jdkProxy.getJDKProxy(new UserManagerImpl());//获取代理对象
        user.addUser("admin", "123123");//执行新增方法
    }
    
}
1234567891011121314151617181920212223242526
```

JDK动态代理运行结果

```
JDK动态代理，监听开始！
调用了新增的方法！
传入参数为 userName: admin password: 123123
JDK动态代理，监听结束！
1234
```

###### Cglib动态代理

Cglib动态代理（需要导入两个jar包，asm-5.2.jar,cglib-3.2.5.jar。版本自行选择）

```java
//Cglib动态代理，实现MethodInterceptor接口
public class CglibProxy implements MethodInterceptor {
    private Object target;//需要代理的目标对象
    
    //重写拦截方法
    @Override
    public Object intercept(Object obj, Method method, Object[] arr, MethodProxy proxy) throws Throwable {
        System.out.println("Cglib动态代理，监听开始！");
        Object invoke = method.invoke(target, arr);//方法执行，参数：target 目标对象 arr参数数组
        System.out.println("Cglib动态代理，监听结束！");
        return invoke;
    }
    //定义获取代理对象方法
    public Object getCglibProxy(Object objectTarget){
        //为目标对象target赋值
        this.target = objectTarget;
        Enhancer enhancer = new Enhancer();
        //设置父类,因为Cglib是针对指定的类生成一个子类，所以需要指定父类
        enhancer.setSuperclass(objectTarget.getClass());
        enhancer.setCallback(this);// 设置回调 
        Object result = enhancer.create();//创建并返回代理对象
        return result;
    }
    
    public static void main(String[] args) {
        CglibProxy cglib = new CglibProxy();//实例化CglibProxy对象
        UserManager user =  (UserManager) cglib.getCglibProxy(new UserManagerImpl());//获取代理对象
        user.delUser("admin");//执行删除方法
    }
    
}
12345678910111213141516171819202122232425262728293031
```

Cglib动态代理运行结果

```
Cglib动态代理，监听开始！
调用了新增的方法！
传入参数为 userName: admin password: 123123
Cglib动态代理，监听结束！
```



并且引入了AOP概念:Aspect、advice、joinpoint等等，同时引入了AspectJ中的一些注解@pointCut,@after,@before等等。

![image-20210919132927505](javaNote.assets/image-20210919132927505.png)

![image-20210919132248570](javaNote.assets/image-20210919132248570.png)

![image-20210919094313571](javaNote.assets/image-20210919094313571.png)

### spring事务

![image-20210922094148429](javaNote.assets/image-20210922094148429.png)

![image-20210922094646547](javaNote.assets/image-20210922094646547.png)

### 循环依赖

```
	/**
	 * 一级缓存，缓存beanName对应经过了完整生命周期的bean
	  */
	private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256);

	/**
	 * 三级缓存，缓存bean的对象工厂ObjectFactory，可通过ObjectFactory得到普通对象或AOP对象（如果bean被代理的话）
	  */
	private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);

	/**
	 * 二级缓存，缓存提前拿原始对象进行AOP之后的代理对象，原始对象还没有进行属性注入和后续BeanPostProcessor生命周期
	  */
	private final Map<String, Object> earlySingletonObjects = new ConcurrentHashMap<>(16);
```

![8f7488526360acb69f9ff188da38e185.png](javaNote.assets/8f7488526360acb69f9ff188da38e185.png)

#### ObjectFactory

将半成品对象提前暴露，本质是一个Lambda表达式`**() ->getEarlyBeanReference(beanName, mbd, bean)**`，被AbstractAutoProxy实现，即该类用来实现APO的。

![在这里插入图片描述](javaNote.assets/7c0145c9941d407a98b5f9e994d903b6.png)

#### 可以用两级缓存吗

用一级缓存和三级缓存就可以解决循环依赖：将半成品对象提前暴露在ObjectFactory中

但如果有aop的话，每次调用ObjectFactory都会产生一个代理对象，这就不能保证单例了，所以需要二级缓存来存代理对象

### 日志级别

```
DEBUG>INFO
ALL、TRACE、DEBUG 、INFO、WARN、ERROR 、FATAL 、OFF
```

### MyBatis批量更新

foreach

[批量更新](https://www.cnblogs.com/exmyth/p/5757137.html)

### beanFactory&factoryBean

factortbean:不需要遵循bean生命周期地创建对象，适合自定义创建一些复杂对象

![image-20220524164924582](javaNote.assets/image-20220524164924582.png)



![img](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lhbWxpaG9uZ3dlaQ==,size_16,color_FFFFFF,t_70#pic_center.png)

### SpringMVC

1. 客户端（浏览器）发送请求， `DispatcherServlet`拦截请求。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据 uri 去匹配查找能处理的 `Handler`（也就是我们平常说的 `Controller` 控制器） ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
3. `DispatcherServlet` 调用 `HandlerAdapter`适配执行 `Handler` 。
4. `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象给`DispatcherServlet`，`ModelAndView` 顾名思义，包含了数据模型以及相应的视图的信息。`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
5. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
6. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
7. 把 `View` 返回给请求者（浏览器）

![img](javaNote.assets/de6d2b213f112297298f3e223bf08f28.png)

### 配置文件加载顺序 

[博客](https://blog.51cto.com/u_3631118/3032964)

**数字小的优先级越高，越先加载。高优先级配置会覆盖低优先级配置内容。**

```
1.命令行参数
2.Java系统属性（System.getProperties()）
3.OS环境变量
4.jar包外部的application-{profile}.properties配置文件
5.jar包内部的application-{profile}.properties配置文件
6.jar包外部的application.properties配置文件（此级别在测试环境经常使用。比如就在jar包同级目录放置一个配置文件，就内覆盖jar包内部所有的配置文件了）
7.jar包内部的application.properties配置文件
8.@Configuration注解类上的@PropertySource（手动指定导入外部配置文件）
```



```
spring boot默认依赖的日志框架是logback，因此必须在zookeeper中把slf4j-log4j12排除掉，zookeeper默认依赖的过时的log4j，log4j和logback会出现包冲突。也不建议在使用log4j。当然这里具体每个依赖使用什么版本最好根据dubbo官方的版本来。
```



### RewritePath

去除前缀或者路径重写

spring cloud gateway利用RewritePath可以实现原来的zuul的stripPrefix的效果，而且功能更强大。

```
spring:
  cloud:
    gateway:
      default-filters:
      - AddResponseHeader=X-Response-Default-Foo, Default-Bar
      routes:
      - id: demo
        uri: http://demo.com.cn:80
        order: 8999 ## 越小越优先
        predicates: 
        - Path=/demo/**
        filters:
        - RewritePath=/demo/(?<segment>.*), /$\{segment}
```

```

 filters:
    - StripPrefix=1
```

### @RequestBody注解

**加@RequestBody**

Content-type**只能处理application/json**

@RequestBody作用： 
      1. 该注解用于读取Request请求的**body**部分数据，使用系统默认配置的**HttpMessageConverter**进行解析，然后把相应的数据绑定到要返回的对象上；

2. 再把HttpMessageConverter返回的对象数据绑定到 controller中方法的参数上。

**不加@RequestBody**

Content-type为x-www-form-urlencoded和form-data，不能处理json对象

### 拦截器

①preHandle：在业务处理器处理请求之前被调用。预处理，可以进行编码、安全控制、权限校验等处理；

②postHandle：在业务处理器处理请求执行完成后，生成视图之前执行。后处理（调用了Service并返回ModelAndView，但未进行页面渲染），有机会修改ModelAndView （这个博主就基本不怎么用了）；
③afterCompletion：在DispatcherServlet完全处理完请求后被调用，可用于清理资源等。返回处理（已经渲染了页面）；

![image-20220317210114627](javaNote.assets/image-20220317210114627.png)

![image-20220317210012557](javaNote.assets/image-20220317210012557.png)

![image-20220317205657402](javaNote.assets/image-20220317205657402.png)

### Pagehelper原理

```
Pagehelper是MyBatis的分页插件，加载PageInterceptor拦截器到拦截链中，PageHelper.startPage相当于向线程上下文中设置ThreadLocal中，拦截从中拿到分页信息，然后对Sql进行拼接，最后再把ThreadLocal清楚
```

```
List<Job> jobDataList = jobDataMapper.getJobDataList(jobId, params);
jobDataList这个已经变成Page分页对象对象了，里面也已经包含了总页数之类的信息了。并且在父类中设置总条数
    public PageSerializable(List<T> list) {
        this.list = list;
        if(list instanceof Page){
            this.total = ((Page)list).getTotal();
        } else {
            this.total = list.size();
        }
    }


public class Page<E> extends ArrayList<E> implements Closeable {}

```

### MyBatis返回自增主键

```java
/**
 * 插入一条数据，返回自增主键
 *
 * @param sysRolePo
 * @return
 */
@Insert({"insert into sys_role(role_name, enable, create_by, create_time)",
        "values(#{roleName}, #{enable}, #{createBy}, #{createTime})"})
@Options(useGeneratedKeys = true, keyProperty = "id")
int insert2(SysRolePo sysRolePo);

/**
 * 插入一条数据，返回非自增主键
 *
 * @param sysRolePo
 * @return
 */
@Insert({"insert into sys_role(role_name, enable, create_by, create_time)",
        "values(#{roleName}, #{enable}, #{createBy}, #{createTime})"})
@SelectKey(statement = "SELECT LAST_INSERT_ID()",
        keyProperty = "id",
        resultType = Long.class,
        before = false)
int insert3(SysRolePo sysRolePo);

```

注解动态sql <if test=''>不用加#去取

![image-20211229222748909](javaNote.assets/image-20211229222748909.png)

### MyBatis TypeHandler

MyBatis 中的 TypeHandler 类型处理器用于 JavaType 与 JdbcType 之间的转换，用于 PreparedStatement 设置参数值和从 ResultSet 或 CallableStatement 中取出一个值。

自定义 TypeHandler

```java
@MappedTypes(value = { Enum1.class, Enum2.class})
public class EnumTypeHandler extends BaseTypeHandler<BaseEnum> {}
```

自定义类型处理器是通过实现 org.apache.ibatis.type.TypeHandler 接口实现的。这个接口定义了类型处理器的基本功能，接口定义如下所示。

![在这里插入图片描述](javaNote.assets/20190520184430201.png)

其中 setParameter 方法用于把 java 对象设置到 PreparedStatement 的参数中，getResult 方法用于从 ResultSet（根据列名或者索引位置获取） 或 CallableStatement（根据存储过程获取） 中取出数据转换为 java 对象。

### Executor执行器

** `SimpleExecutor` ：**每执行一次 update 或 select，就开启一个 Statement 对象，用完立刻关闭 Statement 对象。

** `ReuseExecutor` ：**执行 update 或 select，以 sql 作为 key 查找 Statement 对象，存在就使用，不存在就创建，用完后，不关闭 Statement 对象，而是放置于 Map<String, Statement>内，供下一次使用。简言之，就是重复使用 Statement 对象。

** `BatchExecutor` ：**执行 update（没有 select，JDBC 批处理不支持 select），将所有 sql 都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个 Statement 对象，每个 Statement 对象都是 addBatch()完毕后，等待逐一执行 executeBatch()批处理。与 JDBC 批处理相同。

作用范围：Executor 的这些特点，都严格限制在 SqlSession 生命周期范围内。

### 延迟加载

https://blog.csdn.net/qq_41775769/article/details/120090159

它的原理是，使⽤ CGLIB 或 Javassist( 默认 ) 创建⽬标对象的代理对象。当**调⽤代理对象的延迟加载属性的 getting ⽅法**时，进⼊**拦截器⽅法**。⽐如调⽤ a.getB().getName() ⽅法，进⼊拦截器的invoke(...) ⽅法，发现 a.getB() 需要延迟加载时，那么就会**单独发送事先保存好的查询关联 B对象的 SQL ，把 B 查询上来**，然后调⽤a.setB(b) ⽅法，于是 a 对象 b 属性就有值了，接着完
成a.getB().getName() ⽅法的调⽤。

总结：延迟加载主要是通过**动态代理**的形式实现，通过**代理拦截到指定⽅法**，**执⾏数据加载**。 

有效减少 Java 程序与数据库交互次数，从而提升整个系统的运行效率，延迟加载**适用于多表关联查询的业务场景**，而单表查询本身只涉及到一张数据表的查询，所以也没有优化的余地了

## java基础

### IO/NIO

![image-20220910205954413](javaNote.assets/image-20220910205954413.png)

#### **Java NIO和IO的主要区别**

```text
IO                NIO
面向流            面向缓冲
阻塞IO           非阻塞IO
无                选择器
```

#### **面向流与面向缓冲**

Java NIO和IO之间第一个最大的区别是，IO是面向流的，NIO是面向缓冲区的。

 Java IO面向流意味着**每次从流中读一个或多个字节**，直至读取所有字节，它们**没有被缓存在任何地方**。此外，它**不能前后移动流中的数据**。如果需要前后移动从流中读取的数据，需要先将它缓存到一个缓冲区。 

Java NIO的把数据读取到一个缓冲区，需要时**可在缓冲区中前后移动**。这就增加了处理过程中的灵活性。

**通道是双向的，可同时读写**，而流是单向的**(一个流必须是 InputStream 或者 OutputStream 的子类)。

#### 阻塞与非阻塞IO

Java IO的各种流是阻塞的。这意味着，当一个线程**调用read() 或 write()时，该线程被阻塞**，直到有一些数据被读取，或数据完全写入。该线程**在此期间不能再干任何事情了**。 

Java NIO的非阻塞模式，使一个线程从某**通道**发送请求读取数据，但是它仅能得到目前可用的数据，**如果目前没有数据可用时，就什么都不会获取**。而不是保持线程阻塞，所以直至数据变的可以读取之前，该线程可以继续做其他的事情。 非阻塞写也是如此。一个线程请求写入一些数据到某通道，但**不需要等待它完全写入，这个线程同时可以去做别的事情**。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以**一个单独的线程现在可以管理多个输入和输出通道（channel）**。

#### 选择器（Selectors）

Java NIO的选择器允许**一个单独的线程来监视多个输入通道**，你可以**注册多个通道使用一个选择器**，然后使用一个单独的线程来“选择”通道：这些通道里已经有可以处理的输入，或者选择已准备写入的通道。这种选择机制，使得一个单独的线程很容易来管理多个通道。

#### 数据处理

在IO设计中，我们从InputStream或 Reader逐字节读取数据。假设你正在处理一基于行的文本数据流，例如：

```text
Name: Anna
Age: 25
Email: anna@mailserver.com
Phone: 1234567890
```

该文本行的流可以这样处理：

```text
csharp InputStream input = … ; // get the InputStream from the
client socket
                                view sourceprint?
                                BufferedReader reader = new BufferedReader(new InputStreamReader(input));
                                String nameLine   = reader.readLine();
                                String ageLine    = reader.readLine();
                                String emailLine  = reader.readLine();                                
                                String phoneLine  = reader.readLine()
```

请注意处理状态由程序执行多久决定。换句话说，一旦reader.readLine()方法返回，你就知道肯定文本行就已读完， readline()阻塞直到整行读完，这就是原因。你也知道此行包含名称；同样，第二个readline()调用返回的时候，你知道这行包含年龄等。 正如你可以看到，该处理程序仅在有新数据读入时运行，并知道每步的数据是什么。一旦正在运行的线程已处理过读入的某些数据，该线程不会再回退数据（大多如此）。下图也说明了这条原则：

![img](javaNote.assets/v2-cb5356ba8897eccdfb5bfe7e463eb67e_720w.jpg)





（Java IO: 从一个阻塞的流中读数据） 而一个NIO的实现会有所不同，下面是一个简单的例子：

```text
ByteBuffer buffer = ByteBuffer.allocate(48);
int bytesRead = inChannel.read(buffer);
```

注意第二行，从通道读取字节到ByteBuffer。当这个方法调用返回时，你不知道你所需的所有数据是否在缓冲区内。你所知道的是，该缓冲区包含一些字节，这使得处理有点困难。
假设第一次 read(buffer)调用后，读入缓冲区的数据只有半行，例如，“Name:An”，你能处理数据吗？显然不能，需要等待，直到整行数据读入缓存，在此之前，对数据的任何处理毫无意义。

所以，你怎么知道是否该缓冲区包含足够的数据可以处理呢？好了，你不知道。发现的方法只能查看缓冲区中的数据。其结果是，在你知道所有数据都在缓冲区里之前，你必须检查几次缓冲区的数据。这不仅效率低下，而且可以使程序设计方案杂乱不堪。例如：

```text
ByteBuffer buffer = ByteBuffer.allocate(48);

int bytesRead = inChannel.read(buffer);

while(! bufferFull(bytesRead) ) {

bytesRead = inChannel.read(buffer);
}
```

bufferFull()方法必须跟踪有多少数据读入缓冲区，并返回真或假，这取决于缓冲区是否已满。换句话说，如果缓冲区准备好被处理，那么表示缓冲区满了。

bufferFull()方法扫描缓冲区，但必须保持在bufferFull（）方法被调用之前状态相同。如果没有，下一个读入缓冲区的数据可能无法读到正确的位置。这是不可能的，但却是需要注意的又一问题。

如果缓冲区已满，它可以被处理。如果它不满，并且在你的实际案例中有意义，你或许能处理其中的部分数据。但是许多情况下并非如此。下图展示了“缓冲区数据循环就绪”：

![img](javaNote.assets/v2-add18281f433ed79a8056f517972421e_720w.jpg)


**Java NIO:从一个通道里读数据，直到所有的数据都读到缓冲区里.**
NIO可让您只使用一个（或几个）单线程管理多个通道（网络连接或文件），但付出的代价是解析数据可能会比从一个阻塞流中读取数据更复杂。

如果需要管理同时打开的成千上万个连接，这些连接每次只是发送少量的数据，例如聊天服务器，实现NIO的服务器可能是一个优势。同样，如果你需要维持许多打开的连接到其他计算机上，如P2P网络中，使用一个单独的线程来管理你所有出站连接，可能是一个优势。一个线程多个连接的设计方案如下图所示：

![img](javaNote.assets/v2-12f14ec6330ff873e9504a417f372305_720w.jpg)





**Java NIO: 单线程管理多个连接**
如果你有少量的连接使用非常高的带宽，一次发送大量的数据，也许典型的IO服务器实现可能非常契合。下图说明了一个典型的IO服务器设计：

![img](javaNote.assets/v2-12f14ec6330ff873e9504a417f372305_720w.jpg)


Java IO: 一个典型的IO服务器设计- 一个连接通过一个线程处理.

### JDBC步骤

// 1、加载驱动

Class.forName(driver);

// 2、链接数据库

java.sql.Connection con = DriverManager.getConnection(url, user, password);

if (!con.isClosed()) {// 判断数据库是否链接成功

System.out.println("已成功链接数据库！");

// 3、创建Statement对象

java.sql.Statement st = con.createStatement();

// 4、执行sql语句

rs = st.executeQuery(sql);// 查询之后返回结果集

// 5、打印出结果

while (rs.next()) {

System.out.println( rs.getString("Id") + "\t" + rs.getString("name") + "\t" + rs.getString("password"));

}

}

rs.close();// 关闭资源

con.close();// 关闭数据库

### 类加载器

![image-20220904223340890](javaNote.assets/image-20220904223340890.png)

### sleep&wait&join&yield

1.sleep会使当前线程睡眠指定时间，不释放锁
2.yield会使当前线程重回到可执行状态，等待cpu的调度，不释放锁
3.wait会使当前线程回到线程池中等待，释放锁，当被其他线程使用notify，notifyAll唤醒时进入可执行状态
4.当前线程调用 某线程.join（）时会使当前线程等待某线程执行完毕再结束，**底层调用了wait，释放锁**

sleep，wait和join都会进入阻塞状态

sleep、wait的使用范围：
sleep: sleep是Thread类中的静态方法。因此无论是在a线程中调用b的sleep方法，还是在b线程中调用a的sleep方法，谁调用谁就sleep。也因此，**sleep可以在任何地方使用**。
wait、notify、notifyAll 就很惨了，只能在**同步控制方法**或**同步控制块**中使用。

![image-20220904222523241](javaNote.assets/image-20220904222523241.png)

### 线程池

#### 七大参数

![image-20220904151955781](javaNote.assets/image-20220904151955781.png)

#### 工作流程

![img](javaNote.assets/b1543b01a1134b13ab020887a4aa3566.png)

#### 四种拒绝策略

1. AbortPolicy

当任务添加到线程池中被拒绝时，直接丢弃任务，并抛出

RejectedExecutionException异常。

2. DiscardPolicy

当任务添加到线程池中被拒绝时，丢弃被拒绝的任务，不抛异常。

3. DiscardOldestPolicy

当任务添加到线程池中被拒绝时，丢弃任务队列中最旧的未处理任务，然后将被拒绝的任务添加到等待队列中。

 4. CallerRunsPolicy

被拒绝任务的处理程序，直接在execute方法的调用线程中运行被拒绝的任务。

总结：就是被拒绝的任务，直接在主线程中运行，不再进入线程池。

#### 自带四种线程池

Executors.new**，本质通过ThreadPoolExecutor创建

newSingleThreadExexcutor：单线程数的线程池（核心线程数=最大线程数=1）
newFixedThreadPool：固定线程数的线程池（核心线程数=最大线程数=自定义）
newCacheThreadPool：可缓存的线程池（核心线程数=0，最大线程数=Integer.MAX_VALUE）
newScheduledThreadPool：支持定时或周期任务的线程池（核心线程数=自定义，最大线程数=Integer.MAX_VALUE）

#### 阻塞队列

```
/**
 * 1、ArrayBlockingQueue ：一个由数组结构组成的有界阻塞队列
 *
 * 2、LinkedBlockingQueue ：一个由链表结构组成的有界阻塞队列（常用）
 *
 * 3、PriorityBlockingQueue ：一个支持优先级排序的无界阻塞队列
 *
 * 4、DelayQueue： 一个使用优先级队列实现的无界阻塞队列
 *
 * 5、SynchronousQueue： 一个不存储元素的阻塞队列（常用）
 *
 * 6、LinkedTransferQueue： 一个由链表结构组成的无界阻塞队列
 *
 * 7、LinkedBlockingDeque： 一个由链表结构组成的双向阻塞队列
 */
```

### 避免多线程竞争

1) 不可变对象；

2) 互斥锁；

3) ThreadLocal 对象；

4) CAS；

### 守护线程

1）、当用户线程全部结束，那么守护线程会跟着虚拟机一同退出了。

2）、 **在Daemon线程中产生的新线程也是Daemon的**。 （这一点又是有着本质的区别了：守护进程fork()出来的子进程不再是守护进程，尽管它把父进程的进程相关信息复制过去了，但是子进程的进程的父进程不是init进程，所谓的守护进程本质上说就是“父进程挂掉，init收养，然后文件0,1,2都是/dev/null，当前目录到/”）

3）、thread.setDaemon(true)必须在thread.start()之前设置，否则会跑出一个IllegalThreadStateException异常。你不能把正在运行的常规线程设置为守护线程。 

### String类

#### 不可变性

- 由于字符串无论在任何 Java 系统中都广泛使用，会用来存储敏感信息，如账号，密码，网络路径，文件处理等场景里，保证字符串 String 类的安全性就尤为重要了，如果字符串是可变的，容易被篡改，那我们就无法保证使用字符串进行操作时，它是安全的，很有可能出现 **SQL 注入**，访问危险文件等操作。
- 在多线程中，只有不变的对象和值是**线程安全**的，可以在多个线程中共享数据。由于 String 天然的不可变，当一个线程”修改“了字符串的值，只会产生一个新的字符串对象，不会对其他线程的访问产生副作用，访问的都是同样的字符串数据，**不需要任何同步操作**。
- 字符串作为基础的数据结构，大量地应用在一些**集合容器**之中，尤其是一些散列集合，在散列集合中，存放元素都要根据对象的 **hashCode**() 方法来确定元素的位置。由于字符串 hashcode 属性不会变更，保证了唯一性，使得类似 HashMap，HashSet 等容器才能实现相应的缓存功能。由于 String 的不可变，避免重复计算 hashcode，只要使用缓存的 hashcode 即可，这样一来大大提高了在散列集合中使用 String 对象的性能。
- 当字符串不可变时，**字符串常量池**才有意义。字符串常量池的出现，可以减少创建相同字面量的字符串，让不同的引用指向池中同一个字符串，**为运行时节约很多的堆内存**。若字符串可变，字符串常量池失去意义，基于常量池的 String.intern() 方法也失效，每次创建新的字符串将在堆内开辟出新的空间，占据更多的内存。

#### String构造方法

![image-20220904115721518](javaNote.assets/image-20220904115721518.png)

### StringBuilder

![image-20220907230422145](javaNote.assets/image-20220907230422145.png)

### 反射

- 程序**运行时**，可以通过反射获得任意一个类的Class对象，并通过这个对象查看这个**类的信息**；
- 程序运行时，可以通过反射创建任意一个类的实例，并访问该实例的成员；
- 程序运行时，可以通过反射机制生成一个**类的动态代理类**或动态代理对象。

通过反射机制加载数据库的驱动程序

多数框架都支持注解/XML配置，从配置中解析出来的类是字符串，需要利用反射机制实例化

面向切面编程（AOP）的实现方案，是在程序运行时创建目标对象的代理类，这必须由反射机制来实现

### JWT

#### 1.Header

描述JWT元数据的JSON对象，签名使用的算法，令牌的类型。最后，使用Base64 URL算法将上述JSON对象转换为字符串保存

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

#### 2.Payload

用户信息,过期时间

```
iss：发行人
exp：到期时间
sub：主题
aud：用户
nbf：在此之前不可用
iat：发布时间
jti：JWT ID用于标识该JWT
```

默认情况下JWT是未加密的，因为只是采用base64算法，拿到JWT字符串后可以转换回原本的JSON数据，任何人都可以解读其内容，因此不要构建隐私信息字段，比如用户的密码一定不能保存到JWT中，以防止信息泄露。JWT只是适合在网络中传输一些非敏感的信息

#### 3.Signature

**签名哈希**部分是对上面两部分数据签名，以确保数据不会被篡改

### Object类

Object类的八个方法

```
clone
equals
hashCode
toString
wait
notify
finalize
getClass
```

![image-20220820210529660](javaNote.assets/image-20220820210529660.png)

### classpath

classpath是值类路径，不是环境变量



![image-20220820204348440](javaNote.assets/image-20220820204348440.png)

###  switch

底层转为int类型

Java中Switch支持byte、short、char、int四种基本类型（由于自动拆装箱，对应的包装类型也是支持的）,枚举和String类型(利用hashCode函数)，但不支持long类型
一、底层实现
java中switch是**将所有类型转换成int类型来进行判断**。关于long，因为long类型表示的范围大于int类型，所以无法进行转换，因此switch不支持long类型

二、基本类型以及其包装类转换成int类型
基本类型都为强转，char类型为取ascll码，包装类强转前有个自动拆装箱的操作。

三、枚举类转换成int类型
在switch中枚举类型的int值为枚举元素在枚举类中的序号。

四、String类型转换成int类型
对于String来说其int值即为String类的哈希值，即利用hashCode()函数，考虑到哈希值相等的情况，底层中加入了equals()函数。

jdk8只能是byte、char(两个字节)、int、String

![image-20220815215514009](javaNote.assets/image-20220815215514009.png)

### Ascii码表

![image-20220802102830143](javaNote.assets/image-20220802102830143.png)

### 标识符

标识符可以是字母，数字、下划线和美元符号$。
但不能以数字开头。

注意点不是标识符

![image-20220801221900160](javaNote.assets/image-20220801221900160.png)

静态方法属于类，实例方法属于实例

![image-20220801222017319](javaNote.assets/image-20220801222017319.png)

### @Inherited

子类会继承父类的注解，接口继承和类实现接口都不会生效。

![image-20220726110810427](javaNote.assets/image-20220726110810427.png)

### 卸载自带[jdk](https://www.cnblogs.com/linjiqin/archive/2013/03/23/2977377.html)

```
rpm -qa|grep jdk
rpm -qa|grep gcj
yum -y remove java java-1.6.0-openjdk-1.6.0.0-1.50.1.11.5.el6_3.x86_64
yum list java*
yum install -y java-1.8.0-openjdk-devel.x86_64
```

### 枚举

```
 // XxxEnum->枚举类; e.getXxx()->根据哪个属性获取枚举对象
 public static XxxEnum getEnumObjByKey(Integer key){
        Optional<XxxEnum> any = Arrays.stream(XxxEnum.class.getEnumConstants())
        		.filter(e -> e.getXxx().equals(key)).findAny();
        if (any.isPresent()){
            return any.get();
        }
        return null;
 }

```

### ThreadLocal

#### 设计原理

- 通过threadLocal对象的set方法存储的值实际是存在每个Thread对象的属性中：ThreadLocal.**ThreadLocalMap** threadLocals。
- ThreadLocalMap内部结构为Entry键值对，其**Key为ThreadLocal对象（弱引用）**，**Value为变量副本**。

一言以蔽之：**ThreadLocal是将线程需要访问的数据存储在线程对象自身中，从而避免多线程的竞争**。

ThreadLocalMap的Entry数组的下标就是threadLocal.threadLocalHashCode）

#### 内存泄漏问题

Entry的key是**弱引用**（不管内存是否足够，下一次垃圾回收的就会被清除），如果key被回收了变为null，value又是强引用一直存在，那么造成**内存泄漏**。

解决措施：set和remove配对使用

![在这里插入图片描述](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA54y_5aeL5aSn54yp54yp,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center.png)

#### 为什么不可以设置为强引用

因为用户用完把threadLocal ref=null，但是由于thread对象对ThreadLocalMap是强引用，ThreadLocalMap中key对threadLocal 是强引用，那么就导致threadLocal 还是不能被回收。那么把threadLocal设置为弱引用才不会违背用户想要回收threadLocal 的意图。

#### 最佳实践

spring单例bean如何保证线程安全：使用ThreadLocal，每个线程都保留一个变量副本（注意是新建一个变量副本，如果threadlocal引用同一个对象，那么做不到线程安全）。

比如，数据库连接，每个线程持有的都是新建的connection副本

```
public class TopicDao {  
    //①使用ThreadLocal保存Connection变量  
    private static ThreadLocal <Connection> connThreadLocal = newThreadLocal<Connection>();  
    public static Connection getConnection() {  
       // ②如果connThreadLocal没有本线程对应的Connection创建一个新的Connection，  
       // 并将其保存到线程本地变量中。  
       if (connThreadLocal.get() == null) { 
           Connection conn = getConnection();  
           connThreadLocal.set(conn);  
           return conn;  
       }
       // ③直接返回线程本地变量
       return connThreadLocal.get();  
    }
 
    public void addTopic() {  
       // ④从ThreadLocal中获取线程对应的Connection  
       try {
           Statement stat = getConnection().createStatement();  
       } catch (SQLException e) {  
           e.printStackTrace();  
       }
    }
}
```

#### 源码

threadLocal.set()其实就是设置当前Thread线程对象的成员变量ThreadLocalMap

```java
	// threadLocal.set()    
	public void set(T value) {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
    }
	// 本质调用的是ThreadLocalMap.set()
    private void set(ThreadLocal<?> key, Object value) {
        Entry[] tab = table;
        int len = tab.length;
        int i = key.threadLocalHashCode & (len-1);

        for (Entry e = tab[i];
             e != null;
             e = tab[i = nextIndex(i, len)]) {
            ThreadLocal<?> k = e.get();

            if (k == key) {
                e.value = value;
                return;
            }

            if (k == null) {
                replaceStaleEntry(key, value, i);
                return;
            }
        }

        tab[i] = new Entry(key, value);
        int sz = ++size;
        if (!cleanSomeSlots(i, sz) && sz >= threshold)
            rehash();
    }
```



threadLocal.remove()

```java
    // threadLocal.remove()
	public void remove() {
         ThreadLocalMap m = getMap(Thread.currentThread());
         if (m != null)
             m.remove(this);
     }
    // 本质调用的是ThreadLocalMap.remove()
    private void remove(ThreadLocal<?> key) {
        Entry[] tab = table;
        int len = tab.length;
        int i = key.threadLocalHashCode & (len-1);
        for (Entry e = tab[i];
             e != null;
             e = tab[i = nextIndex(i, len)]) {
            if (e.get() == key) {
                e.clear();
                expungeStaleEntry(i);
                return;
            }
        }
    }
```



threadLocal.get()

```java
    // threadLocal.get()
	public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
	// 本质调用的是ThreadLocalMap.getEntry()
    private Entry getEntry(ThreadLocal<?> key) {
        int i = key.threadLocalHashCode & (table.length - 1);
        Entry e = table[i];
        if (e != null && e.get() == key)
            return e;
        else
            return getEntryAfterMiss(key, i, e);
    }
```

[ThreadLocal内存泄露原因，如何避免](https://blog.csdn.net/qq_38969734/article/details/124001401)

[头条二面：你确定ThreadLocal真的会造成内存泄露？](https://zhuanlan.zhihu.com/p/402856377)

### synchronized

- 修饰实例方法，对当前实例对象this加锁
- 修饰静态方法，对当前类的Class对象加锁
- 修饰代码块，指定一个加锁的对象，给对象加锁

根据上面三条可以去掉AC，D的话我觉得是可重入锁。

![image-20220808203408805](javaNote.assets/image-20220808203408805.png)

#### 锁升级

Java线程和操作系统线程是一一对应的，避免用户态和内核态的频繁切换

**无锁-》偏向锁-》轻量级锁-》重量级锁**

- 无锁：就是不加锁，对象头标志位 0 01

- 偏向锁：大部分场景下只有一个线程来获取资源，该线程访问同步代码块并获取锁时，对象头标志位 1 01（偏向模式），使用CAS把线程id记录在Mark Word中。以后这个线程进来就不用同步操作了

- 轻量级锁：多个线程竞争就会切换到轻量级锁，也就是**自旋锁**，避免了用户态到内核态的切换（monitor会阻塞和唤醒线程，线程的阻塞和唤醒需要CPU从用户态到内核态的切换）

  适应性自旋锁是一种优化，动态调准自旋时间（对某个锁很少自旋成功直接跳过；刚获得过这个锁，那么运行自旋时间长一点）

- 重量级锁：获取不到锁直接阻塞

注意锁的升级是不可逆的

**对象头**

补充：对象在内存中分为三块区域：对象头，实例数据和对齐填充。

对象头包括标记字段（Mark Word）和类型指针（Klass Pointer）

- 标记字段：对象hahCode，分代年龄，锁标志位
- 类型指针：指向类元数据的指针，表示哪个类的实例

### volatile

### AQS

AQS（**AbstractQueuedSynchronizer**）是一个基于FIFO队列实现同步器，帮我们实现了**入队规则**和**线程队列的唤醒**工作，可基于它实现独占锁，共享锁和信号量。

AQS维护了两种队列，一个是本身的FIFO**阻塞队列**（结点叫做Node），另一个基于ConditionObject的**条件队列**。

**Node和ConditionObject是两个重要的内部类**

![image-20220411150131351](javaNote.assets/image-20220411150131351.png)

#### Node

Node是对线程的封装，它有个核心状态**waitStatus**，决定当前结点的后续操作（是否等待唤醒还唤醒后续结点），有如下四种状态

```java
    // 表示线程已取消调度
    static final int CANCELLED =  1;
    // 等待唤醒
    static final int SIGNAL    = -1;
    // 等待同步锁
    static final int CONDITION = -2;
    // 共享模式下无条件传播（递归唤醒下一个结点线程）
    static final int PROPAGATE = -3;
```

- CANCEL(1)：当timeout或中断可变更为此状态，进入该状态的结点将不再发送变化
- SIGNAL(-1)：表示后续结点依赖当前结点唤醒，后继结点入队时，会将前继结点置为SIGNAL
- CONDITION(-2)：表示在获取对应条件的同步锁，当有线程调用Condition.signal()后，处于条件队列的线程就会转移到阻塞队列竞争锁
- PROPAGATE(-3)：共享模式下，前继结点会不断递归唤醒下一个结点
- 0：新节点的默认状态

负值表示为有效状态

#### ConditionObject

比如ReentrantLock.newCondition()就是基于ConditionObject实现的，条件队列的结点也是Node

```java
    public class ConditionObject implements Condition, java.io.Serializable {
        private static final long serialVersionUID = 1173984872572414699L;
        /** First node of condition queue. */
        private transient Node firstWaiter;
        /** Last node of condition queue. */
        private transient Node lastWaiter;
```

![image-20220411145705797](javaNote.assets/image-20220411145705797.png)

#### AQS阻塞队列和条件队列

1. 当多个线程调用lock.lock()的时候只有一个获取到了锁，其他的就会转为node结点添加到阻塞队列中，并CAS自旋竞争锁。

2. 当获取锁的线程的条件变量的await()被调用时，就会释放当前锁，并加入到条件变量对应的条件队列中

3. 有一个线程调用了条件变量的signal()或signalAll()方法，就会把对应条件队列中的线程加入到阻塞队列中

   ![image.png](javaNote.assets/9f0c462d47eaa34e2d445bcb96229536.png)

#### 基于AQS实现并发锁

可重写以下四个方法操控资源变量**state**

- tryAcquire(int arg)：获取独占锁

- tryRelease(int arg)：释放独占锁

- tryAcquireShared(int arg)：获取共享锁

- tryReleaseShared(int arg)：释放共享锁

### maven更改源

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oiR5Lmf5oOz5oiQ5Li65YWJ,size_20,color_FFFFFF,t_70,g_se,x_16.png)

### gradle

```
50		==>		jdk1.6
51		==>		jdk1.7
52		==>		jdk1.8
53		==>		jdk9
54		==>		jdk10
55		==>		jdk11
56		==>		jdk12
57		==>		jdk13
58		==>		jdk14
59		==>		jdk15
```

### 线程安全集合

**Vector和hashtable**使用synchronized关键字实现，效率低

**Collections.synchronized**

![image-20211106144005886](javaNote.assets/image-20211106144005886.png)

**JUC包下的Concurrent和CopyOnwrite**

ConcurrentHashMap  -->volatile 分段锁，效率高

CopyOnWriteArrayList 类型,通过动态数组与线程安全

```java
    /** The lock protecting all mutators */
    final transient ReentrantLock lock = new ReentrantLock();
通过可重入锁ReentrantLock和volatile关键字实现，效率较高

    /** The array, accessed only via getArray/setArray. */
    private transient volatile Object[] array;

public boolean add(E e) {
        final ReentrantLock lock = this.lock;
        lock.lock();
        try {
            Object[] elements = getArray();
            int len = elements.length;
            // 复制新的数组，所以修改效率较低
            Object[] newElements = Arrays.copyOf(elements, len + 1);
            newElements[len] = e;
            setArray(newElements);
            return true;
        } finally {
            lock.unlock();
        }
    }
```

### SPI机制

SPI即**扩展点发现机制**，就是通过读取指定目录下的配置文件，从配置文件中读取扩展点接口的具体实现类并加载，然后依据注解上的配置以及URL参数中的属性值来决定到底要是用哪个实现类执行相应操作。

```
读取指定目录下的配置文件并加载，并根据注解配置以及URL属性值确定哪个实现类执行操作
```

### 八大基本数据类型

注意char和short都是占用两个字节

一个字节的只有byte和boolean

switch支持byte,char,int,String

![image-20220815215718702](javaNote.assets/image-20220815215718702.png)

```
 (byte，short，char)--int--long--float—double
 自动转为访问更大的类型，否则就要强转
 
 char类型向整形转的时候，转为对应的ascii码
 
 像short和char这种是平级的就得强制转换
```

三元运算符自动类型转换，提高成浮点数，所以变成9.0

![image-20220908222205555](javaNote.assets/image-20220908222205555.png)

**数组可以看作是对象，但不是原生类**

### 浮点数比较

#### 1、绝对值比较差值范围 

指定一个误差范围，两个浮点数的差值在此范围之内，则认为是相等的

```
/**
 浮点数比较的第一种方式(失精度的方式)
 指定一个误差范围，两个浮点数的差值在此范围之内，则认为是相等的。
*/
float diff = 1e-6f;
if (Math.abs(value1 - value2) < diff) {
System.out.println("value1的值与value2的值相等");
}
```

#### 2、使用BigDecimal

### 接口和抽象类

**抽象类好处**

**自下而上**的思想

负责方法约定和逻辑调用（**复用**共同的代码和逻辑），让实现**延迟到子类实现**，也让子类更加简洁

注意只能定义变量和方法不能有其他语句。

![image-20220805155237034](javaNote.assets/image-20220805155237034.png)

**接口**

**自上而下**的行为约束

#### 抽象类和接口的关系

看到这里，相信有很多小伙伴会有疑问，能否使用抽象类替换接口，毕竟两者概念上很容易模糊。在个人看来，JAVA中，除了类只能被单继承，但是接口可以多实现(接口之间可以多继承)这个限制外，最重要的是两者设计的一个目的。

**抽象类设计出来的目的是为了抽取出某一个种类的一些共有特性或者默认行为，以达到代码复用的目的。而接口则是为了规定某一种标准而设计出来，它强调的是规范，在面向对象语言中体现就是多态性的使用。** 所以，如果出现该设计为抽象类还是接口纠结的场景，建议可以从设计的动机方面进行考虑，应该能得到一个比较好的结果。

### 实例方法

Java变量分为成员变量和局部变量

成员变量又包括类变量和实例变量

成员变量是有默认初始化的，局部变量要显示初始化，不然会报错



下面答案选D,因为A还受到超类方法修饰符的影响。

因为超类方法是**私有**或者**protect且不同包**则不可以访问

![image-20220425113905730](javaNote.assets/image-20220425113905730.png)

```
在类方法中，不能引用实例成员（变量，方法）

不能使用super、this关键字

不考虑访问修饰符的话，

实例方法可以通过super.方法名，对象名.方法名调用父类的实例方法

实例方法可以通过类名.方法名，super.方法名调用父类的静态方法

实例方法通过this.方法名调用本类的其他方法

本类的静态方法还可以用类名.方法名调用。
```

二、java中super关键字

1.在子类构造器中显示调用父类构造器(super必须出现在子类构造器的第一行)

2..可以在子类中充当临时父类对象，super.方法名调用父类的方法

三、java中this关键字

1.代表当前对象，指向成员变量和成员方法

2.指向某个构造方法，通过this调用其他构造方法。

this();//代表无参构造方法

### 修饰符

```
protect比def不同包子类也可以访问
```

访问级别       访问控制修饰符        同类       同包       子类      不同的包

公开级别：       public                        y          y              y             y

受保护             protected                   y          y              y

默认             没有访问控制符             y          y

私有                 private                       y

### ArrayList的扩容机制

https://zhuanlan.zhihu.com/p/145554951

无参构造的时候，初始为空数组DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {}
第一次add添加元素后，会扩容为10，

```
    private static int calculateCapacity(Object[] elementData, int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
```

大于10之后，每次扩容增加**原来的一半**

```java
    private void grow(int minCapacity) {
    	...
        int newCapacity = oldCapacity + (oldCapacity >> 1);
       	... 
    }
```



### HashMap

**put()方法逻辑**

![image-20220428162738314](javaNote.assets/image-20220428162738314.png)

hashCode()用于获取哈希码（散列码），eauqls()用于比较两个对象是否相等，它们应遵守如下规定：

- 如果两个对象相等，则它们必须有相同的哈希码。
- 如果两个对象有相同的哈希码，则它们未必相等。

**重写equals一定要hashCode方法**

保证equals相等的两个对象hashCode（默认比较地址）一定要相等

#### **put方法**

- 调用key的hashCode方法计算出hash值，再和`数组长度-1`按位与得到哈希表的下标，判断桶是否为null，为null直接插入
- 桶存在，就产生了hash冲突，接下来和桶上的元素比较hash值是否相同，如果不一致，新建一个结点来存储，如果一致，那么再调用equals判断内容相等，相等则覆盖，不相等继续往下找，如果都不相等，再新建结点存储数据

```java
// 负载因子，默认0.75 防止hash冲突过于严重。比如当键值对数量达到达到capacity*loadFactor后就会进行扩容。loadFactor=键值对数目（size）/数组长度(capacity)
final float loadFactor;

// 当桶的元素个数大于等于8且数组长度大于64进行树化，否则进行扩容；从空间时间考虑，利用泊松分布，大于等于8的情况很少
static final int TREEIFY_THRESHOLD = 8;

// 当桶的元素小于等于6重新转换成链表
static final int UNTREEIFY_THRESHOLD = 6;

// 只有桶的个数达到64才会进行树化，还没达到则应该扩容而不是树形化
static final int MIN_TREEIFY_CAPACITY = 64;

// 存储元素的数组，总是2的幂次倍,当hash&(len-1)可减少hash冲突,且其值与取余相同，即hash值%len==hash&(len-1),且性能更高
transient Node<K,V>[] table;

// 阈值（threshold）=数组容量（capacity）*负载因子（loadFactor），键值对数量阈值，超过就会进行扩容，
int threshold;

// 键值对的数目
transient int size;

static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16); // 原理：最终通过hash&(len-1)计算桶的位置，假设len-1=111,这样按位与操作只用到了hash值得后四位，如果hash值高位变化很大，低位变化很小，那么hash冲突就会很严重。经过右移按位异或后，高位
}

// 先比较hashCode是否相同，再比较是否是同个对象或者equals()相同
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
    	// 如果桶位存在
        if ((p = tab[i = (n - 1) & hash]) == null)   // 先判断hash之后的桶位是否存在，为null直接新建node
            tab[i] = newNode(hash, key, value, null);// 重写hashCode之后才会字面量相同的key才会映射到同一个桶上
        // 如果桶位不存在
    	else { 
            Node<K,V> e; K k;
            // 若hashCode相等并且地址或equals相等则表示同一个，所以进行覆盖
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k)))) 
                e = p;
            else if (p instanceof TreeNode) // 是否是红黑树结点类型，是直接插入
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        // 若链表长度大于等于8
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            // 转化为红黑树
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash && // 找到了hashCode相等的并且equals相等，则退出，后面进行覆盖
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e; // 记录下一个结点
                }
            }
            if (e != null) { // 找到了相同的key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value; // 进行覆盖
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold) // 如果键值对长度大于阈值，扩容
            resize();
        afterNodeInsertion(evict);
        return null;
    }
```

![image-20220428155910848](javaNote.assets/image-20220428155910848.png)

```
    // 得到大于给定的最小2的幂次方数
    static final int tableSizeFor(int cap) {
        int n = cap - 1;
        n |= n >>> 1;
        n |= n >>> 2;
        n |= n >>> 4;
        n |= n >>> 8;
        n |= n >>> 16; // 把首位1右边全部置为1，再加一
        return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
    }
```

#### **resize()扩容**

2被扩容

如果长度是2的倍数，那么取模等价于hash&(oldCap-1)

只需要**看看原来的hash值新增的那个bit是1还是0就好了**，是0的话索引没变，是1的话索引变成“原索引+oldCap”

由于2倍（<<1）扩容，所以原桶元素**不用rehash()**,要么在原位置要么在移动原容量。

原理：首先我们知道，**按公式hash&(oldCap-1)**来计算元素下标，而2倍扩容，即高位增加1。

如果增加的哪一位原hash值就是0,那么按位与之后该元素位置不变；

如果为1，那就等于增加原来的容量

```java
    /**
    * 初始化或者扩容2倍	
    */
	final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY; // 第一次插入元素，设置处置容量16
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e; // 只有一个元素直接rehash
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap); // 桉树的逻辑处理，可能会转为链表
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null; // 不需要rehash的元素
                        Node<K,V> hiHead = null, hiTail = null; // 需要rehash的元素
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) { // 如果hash值对应新增的高位值等于0，那么不用移动位置
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {                      // 如果hash值对应新增的高位值等于1，那么移动oldCap位置
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }

	// 数的扩容机制类似，只不过树节点数小于等于6会重新转换成链表
	final void split(HashMap<K,V> map, Node<K,V>[] tab, int index, int bit) {
            TreeNode<K,V> b = this;
            // Relink into lo and hi lists, preserving order
            TreeNode<K,V> loHead = null, loTail = null;
            TreeNode<K,V> hiHead = null, hiTail = null;
            int lc = 0, hc = 0;
            for (TreeNode<K,V> e = b, next; e != null; e = next) {
                next = (TreeNode<K,V>)e.next;
                e.next = null;
                if ((e.hash & bit) == 0) {
                    if ((e.prev = loTail) == null)
                        loHead = e;
                    else
                        loTail.next = e;
                    loTail = e;
                    ++lc;
                }
                else {
                    if ((e.prev = hiTail) == null)
                        hiHead = e;
                    else
                        hiTail.next = e;
                    hiTail = e;
                    ++hc;
                }
            }

            if (loHead != null) {
                if (lc <= UNTREEIFY_THRESHOLD)
                    tab[index] = loHead.untreeify(map);
                else {
                    tab[index] = loHead;
                    if (hiHead != null) // (else is already treeified)
                        loHead.treeify(tab);
                }
            }
            if (hiHead != null) {
                if (hc <= UNTREEIFY_THRESHOLD)
                    tab[index + bit] = hiHead.untreeify(map);
                else {
                    tab[index + bit] = hiHead;
                    if (loHead != null)
                        hiHead.treeify(tab);
                }
            }
        }
```

#### **remove()删除**

判断两个key的hash值相同并且是同一个对象或equals方法相同，那么就删除

```java
f (e.hash == hash &&
                    ((k = e.key) == key ||
                     (key != null && key.equals(k)))) {
                            node = e;
                            break;
                        }
```

#### 初始容量设置

减少扩容

```
initCap/loadfactor+1，如果暂时无法知道初始值，请设置16（初始值）
```

推荐使用entrySet遍历,遍历一次就去出key和value

#### HashMap为什么线程不安全？

HashMap在并发执行**put操作时，可能会导致形成循环链表**，从而引起死循环。

#### HashMap.computeIfAbsent

如果需要向Map中push一个键值对，需要判断K key在当前map中是否已经存在，不存在则通过后面的 Function<? super K, ? extends V> mappingFunction 来进行value计算，且将结果当作value同key一起push到Map中。

#### Class.getEnclosingClass 和 Class.getDeclaringClass

1、getDeclaringClass
  return the declaring class for this class
  获取对应类的声明类Class对象
2、getEnclosingClass
  return the immediately enclosing class of the underlying class
  (获取对应类的直接外部类Class对象)

区别：
两者的区别在于匿名内部类的使用上、getEnclosingClass能够获取匿名内部类对应的外部类Class对象，而getDeclaringClass不能够获取匿名内部类对应的声明类Class对象。

### canal-starter

![img](javaNote.assets/canal UML.jpg)

### addShutdownHook

```
Runtime.getRuntime().addShutdownHook(new Thread(() -> {  // JVM关闭前执行清理工作（钩子函数），这些线程是就绪但未运行
```

**JVM关闭前执行**一些清理工作，注意不能出现死锁或者干太多的话，因为底层操作系统等待你执行的时间也是有限的

##### 触发场景

1. 程序正常关闭：最后一个非守护线程退出或System.exit()
2. 用户中端（比如ctrl+c）

##### 异常情况

1. JVM意外关闭
2. 强制杀死进程钩子函数不执行

### 重写和重载

```
d不同子类对象表现出不同的行为

重写：运行时多态，但当调用父类静态方法表现为编译时多态（因为static是属于类的）

重载：编译时多态
```

![image-20220529223356396](javaNote.assets/image-20220529223356396.png)

### Maven多模块构建找不到指定类Jenkins

```
/root/.jenkins/workspace/pipeLine02/health-community/src/main/java/com/hu/health/community/controller/AreaController.java:[6,34] package com.hu.health.common.utils does not exist
```

因为如果common已经进行build成common.jar,依赖common的其他模块在进行构建的时候，会把common.jar再build一次，导致后面显示找不到指定的类

解决方案：common模块不需要添加build构建插件

另外，如果显示

```
diamond operator is not supported in -source 1.5
```

说明maven默认使用的是1.5进行编译，需要使用1.8进行编译。

解决方案：修改`/opt/maven/conf/settings.xml`路径下全局配置文件为

```
  <profiles>
    <profile>
      <id>jdk1.8</id>
      <activation>
        <activeByDefault>true</activeByDefault>
        <jdk>1.8</jdk>
      </activation>
      <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
      </properties>
    </profile>
  </profiles>

  <activeProfiles>
    <activeProfile>jdk1.8</activeProfile>
  </activeProfiles>
```



### Maven scope

1. compile：默认的scope，运行期有效，需要打入包中
2. provided：编译期有效，运行期不需要提供，不会打入包中
3. runtime：编译不需要，在运行期有效，需要导入包中。（接口与实现分离）
4. test：测试需要，不会打入包中

### 线程池



```
AbortPolicy：丢弃并报异常
DiscardPolicy：丢弃不报异常
DiscardOldestPolicy：丢弃最老的请求
CallerRunsPolicy：让调用者的线程运行任务
```

![image-20220411125053391](javaNote.assets/image-20220411125053391.png)

### 技术路线图

![6](javaNote.assets/6.jpg)

### 集合

![在这里插入图片描述](javaNote.assets/20190722182602226.png)

```java
public E getFirst() {// 会抛出异常
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return f.item;
}
public E peekFirst() {
        final Node<E> f = first;
        return (f == null) ? null : f.item;
}
```

```txt
当key值是Integer类型时，HashMap和TreeMap都是“有序”的；
当key值是String类型的数字时，HashMap和TreeMap都是“无序”的；
当key值是String类型的字母时，HashMap是“无序”的，TreeMap是有序的。
```

#### 双端队列Deque

使用详解 [链接](https://blog.csdn.net/devnn/article/details/82716447)

Deque是一个双端队列接口，继承自Queue接口，Deque的实现类是LinkedList、ArrayDeque、LinkedBlockingDeque，其中LinkedList是最常用的。

**Deque有三种用途：**

- 普通队列(一端进另一端出):

  ```
  Queue queue = new LinkedList()或Deque deque = new LinkedList()
  ```

- 双端队列(两端都可进出)

  ```
  Deque deque = new LinkedList()
  ```

- 堆栈

  ```
  Deque deque = new LinkedList()
  ```

**注意：Java堆栈Stack类已经过时，Java官方推荐使用Deque替代Stack使用。Deque堆栈操作方法：push()、pop()、peek()。**

Deque是一个线性collection，支持在两端插入和移除元素。名称 deque 是“double ended queue（双端队列）”的缩写，通常读为“deck”。大多数 Deque 实现对于它们能够包含的元素数没有固定限制，但此接口既支持有容量限制的双端队列，也支持没有固定大小限制的双端队列。

此接口定义在双端队列两端访问元素的方法。提供插入、移除和检查元素的方法。每种方法都存在两种形式：一种形式在操作失败时抛出异常，另一种形式返回一个特殊值（null 或 false，具体取决于操作）。插入操作的后一种形式是专为使用有容量限制的 Deque 实现设计的；在大多数实现中，插入操作不能失败。

下表总结了上述 12 种方法：

第一个元素 (头部)	最后一个元素 (尾部)
抛出异常	特殊值	抛出异常	特殊值
**插入**	addFirst(e)	offerFirst(e)	addLast(e)	offerLast(e)
**删除**	removeFirst()	pollFirst()	removeLast()	pollLast()
检查	getFirst()	peekFirst()	getLast()	peekLast()
Deque接口扩展(继承)了 Queue 接口。在将双端队列用作队列时，将得到 FIFO（先进先出）行为。将元素添加到双端队列的末尾，从双端队列的开头移除元素。从 Queue 接口继承的方法完全等效于 Deque 方法，如下表所示：

**Queue方法**	等效Deque方法
add(e)	addLast(e)
**offer(e)**	offerLast(e)
remove()	removeFirst()
**poll()**	pollFirst()
element()	getFirst()
peek()	peekFirst()
双端队列也可用作 LIFO（后进先出）**堆栈**。应优先使用此接口而不是遗留 Stack 类。在将双端队列用作堆栈时，元素被推入双端队列的开头并从双端队列开头弹出。堆栈方法完全等效于 Deque 方法，如下表所示：

堆栈方法	等效Deque方法
**push(e)**	addFirst(e)
**pop()**	removeFirst()
peek()	peekFirst()

#### 能否存null值

list（Vector,ArrayList,LinkedList）天生可以,因为是数组或链表

hashSet和LinkedHashSet可以存null，**treeSet不可以**（compareTo报空指针,底层也是基于TreeMap（红黑树）实现）

HashMap,LinkedHashMapk可以存null，**TreeMap key不能为null**（空指针）

**HashTable**,ConcurrentHashMap, 可以和value都不能为null

#### list和set的区别

1、List,Set都是继承自Collection接口
2、

List特点：元素有放入顺序，元素可重复 ；list支持for循环，也就是通过下标来遍历，也可以用迭代器

Set特点：元素无放入顺序，元素不可重复，重复元素会覆盖掉，（元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义equals()方法 ；

set只能用迭代，因为他无序，无法用下标来取得想要的值。）



List 以特定次序来持有元素，可有重复元素。Set 无法拥有重复元素,内部排序

3.

List：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。

Set：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。


1.Vector
底层结构是数组
线程比较安全 也会出现不安全的情况
同步的
2.ArrayList
底层结构是数组
不是同步的
查询速度快 增删速度慢(底层数据结构决定的)
3.LinkedList
链表实现的
不是同步的
增删速度快 查询速度慢(底层数据结构决定的)
不建议使用多态方式创建对象



1.HashSet
无序集合 (存储元素和取出元素的顺序有可能不一致)
底层是一个哈希表结构(查询速度快)
集合元素值可以是null

2.LinkedHashSet
是HashSet的子类
有序集合 (存储元素和取出元素的顺序一致)
底层是一个哈希表结构+链表结构(所以有序)

2.TreeSet
是SortedSet接口的实现类，TreeSet可以确保集合元素处于排序状态
底层是一个红黑树结构，默认整形排序为从小到大。

### ' >> ' 和 ‘ >>> ’

前者是有符号，即符号位不动

后者是无符号

正确的计算方式如下(移位计算是在补码上操作)： 先说>>： 2的二进制为0000~0010(32位)，>>1得到0000~0001，即为1； -2的二进制为1000~0010(32位，原码)=1111~1110(32位，补码)，>>1得到1111~1111(32位，补码)=1000~0001(32位，原码)，即为-1； 再说>>>： 2的二进制为0000~0010(32位)，>>>1得到0000~0001，即为1； -2的二进制为1000~0010(32位，原码)=1111~1110(32位，补码)，>>>1得到0111~1111(32位，补码)=0111~1111(32位，原码)，即为int最大值

```java
    @SuppressWarnings("unchecked")
	// 小根堆插入新节点，寻找合适的位置
    private void siftUpUsingComparator(int k, E x) {
        while (k > 0) {
            int parent = (k - 1) >>> 1;  // 父节点
            Object e = queue[parent];
            if (comparator.compare(x, (E) e) >= 0) 
                // 当前k的值大于父节点，则找到了插入的位置，退出循环
                break;
            queue[k] = e; 
            k = parent; // 否则父节点向上k寻找
        }
        queue[k] = x;
    }
```

### IO流



![1](javaNote.assets/1.png)







![image-20220610155822497](javaNote.assets/image-20220610155822497.png)

### 异常体系

**Throwable**是异常的顶层父类，代表所有的非正常情况。它有两个直接子类，分别是Error、Exception。

**Error**是错误，一般是指与虚拟机相关的问题，如系统崩溃、虚拟机错误、动态链接失败等，这种错误无法恢复或不可能捕获，将导致应用程序中断。通常应用程序无法处理这些错误，因此应用程序不应该试图使用catch块来捕获Error对象。在定义方法时，也无须在其throws子句中声明该方法可能抛出Error及其任何子类。

**Exception**是异常，它被分为两大类，分别是CheckedException和RuntimeException。



所有的RuntimeException类及其子类的实例被称为Runtime异常

其它被称为CheckedException。



RuntimeException则更加灵活，Runtime异常无须显式声明抛出，如果程序需要捕获Runtime异常，也可以使用try...catch块来实现。

Java认为CheckedException都是可以被处理（修复）的异常，所以Java程序必须**显式捕获**Checked异常。如果程序没有处理Checked异常，该程序在编译时就会发生错误，无法通过编译。



RuntimeException不需要显示捕获

CheckedException 需要显示捕获，比如ClassNotFoundException、IllegalAccessException需要显示捕获



```
 一、runtimeException子类：不需要显示捕获
 ClassCastException
 NullPointerException
 IndexOutOfBoundsException
 ArithmeticException

 IllegalMonitorStateException
 IllegalStateException

 UnsupportedOperationException
 ConcurrentModificationException
 NoSuchElementException



 二、CheckedException子类：需要显示捕获
IOException
ClassNotFoundException
IllegalAccessException
InterruptedException
```



![img](javaNote.assets/a56cb21fa0b7b4fdef99df3012fce197.png)

### final关键字

![image-20210914213212811](javaNote.assets/image-20210914213212811.png)

![image-20210914213622393](javaNote.assets/image-20210914213622393.png)

### 位运算

![img](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW95dW5mZWkx,size_16,color_FFFFFF,t_70.png)

从上往下优先级逐渐降低

![img](javaNote.assets/1c950a7b02087bf47171fa88e2d3572c11dfcf36.png)

![image-20210913085350344](javaNote.assets/image-20210913085350344.png)

![image-20210913085613097](javaNote.assets/image-20210913085613097.png)

![image-20210913085933696](javaNote.assets/image-20210913085933696.png)

![image-20210913090409266](javaNote.assets/image-20210913090409266.png)

![image-20210913090748798](javaNote.assets/image-20210913090748798.png)

![image-20210913093706598](javaNote.assets/image-20210913093706598.png)

### 泛型类

```
（2）Box类的泛型定义

public class MyBox<T>{
	private T t;
	
	public void add(T t) {
		this.t = t;
	}
	public T get() {
		return t;
	}
}

在MyBox类的泛型定义中，将类声明中的“public class MyBox”改为“public class MyBox<T>”，并且把MyBox类体中所有的Object都用T进行替换，从而将MyBox定义为能存放各种确定类型对象容器的抽象类型。
```

### 对象序列化

implements Serializable

Java中对象的序列化指的是将对象**转换成以字节序列的形式**来表示，这些字节序列包含了对象的数据和信息，一个序列化后的对象可以被**写到数据库或文件**中，也可用于**网络传输**，一般当我们使用缓存cache（内存空间不够有可能会本地存储到硬盘）或远程调用rpc（网络传输）的时候，经常需要让我们的实体类实现Serializable接口，目的就是为了让其可序列化。

当然，序列化后的**最终目的是为了反序列化，恢复成原先的Java对象**，要不然序列化后干嘛呢，所以序列化后的字节序列都是可以恢复成Java对象的，这个过程就是反序列化。

### transient关键字

概要：transient是短暂的意思，**不被序列化**，生命周期**仅存于调用者的内存**中，不会写到磁盘进行持久化

Java中transient关键字的作用，简单地说，就是让某些被修饰的成员属性变量不被序列化，这一看好像很好理解，就是不被序列化，那么什么情况下，一个对象的某些字段不需要被序列化呢？如果有如下情况，可以考虑使用关键字transient修饰：

1. **类中的字段值可以根据其它字段推导出来**，如一个长方形类有三个属性：长度、宽度、面积（示例而已，一般不会这样设计），那么在序列化的时候，面积这个属性就没必要被序列化了；
2. **银行密码**为了保密，不被序列化哪些字段不想被序列化；

注意：**静态变量不可以序列化**，因为transient修饰的是对象属性，而static是类成员

代码演示：

```java
package tmp;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class Rectangle implements Serializable{

    /**
     *
     */
    private static final long serialVersionUID = 1710022455003682613L;
    private Integer width;
    private Integer height;
    private transient Integer area;



    public Rectangle (Integer width, Integer height){
        this.width = width;
        this.height = height;
        this.area = width * height;
    }

    public void setArea(){
        this.area = this.width * this.height;
    }

    @Override
    public String toString(){
        StringBuffer sb = new StringBuffer(40);
        sb.append("width : ");
        sb.append(this.width);
        sb.append("\nheight : ");
        sb.append(this.height);
        sb.append("\narea : ");
        sb.append(this.area);
        return sb.toString();
    }
}

public class TransientExample{
    public static void main(String args[]) throws Exception {
        Rectangle rectangle = new Rectangle(3,4);
        System.out.println("1.原始对象\n"+rectangle);
        ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream("rectangle"));
        // 往流写入对象
        o.writeObject(rectangle);
        o.close();

        // 从流读取对象
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("rectangle"));
        Rectangle rectangle1 = (Rectangle)in.readObject();
        System.out.println("2.反序列化后的对象\n"+rectangle1);
        rectangle1.setArea();
        System.out.println("3.恢复成原始对象\n"+rectangle1);
        in.close();
    }
}
```

运行结果：

```bash
1.原始对象
width : 3
height : 4
area : 12
2.反序列化后的对象
width : 3
height : 4
area : null
3.恢复成原始对象
width : 3
height : 4
area : 12
```

### String.intern

返回字符串常量池中的地址，如果没有，将对象的地址复制一份放入字符串常量池中再返回

![image-20211107132224715](javaNote.assets/image-20211107132224715.png)

```
public class Demo {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "abc";
        String s3 = new String("abc");
        String s4 = s3.intern();
        System.out.println(s1 == s2); //true
        System.out.println(s1 == s3); // false
        System.out.println(s1 == s4); // true
    }
}
```

节省内存demo

![image-20211107133953519](javaNote.assets/image-20211107133953519.png)

### 深拷贝和浅拷贝

[博客地址](https://www.cnblogs.com/shakinghead/p/7651502.html)

#### 浅拷贝：引用类型的属性指向的是同一个地址

字段如果是引用类型，指向的是同一个地址，如果是基本数据类型则重新复制一份

![img](javaNote.assets/1218256-20171011182513121-1029542999.png)

实现方式一：**拷贝构造方法**指的是该类的构造方法参数为该类的对象。使用拷贝构造方法可以很好地完成浅拷贝，直接通过一个现有的对象创建出与该对象属性相同的新的对象

```java
/* 拷贝构造方法实现浅拷贝 */
public class CopyConstructor {
    public static void main(String[] args) {
        Age a=new Age(20);
        Person p1=new Person(a,"摇头耶稣");
        Person p2=new Person(p1);
        System.out.println("p1是"+p1);
        System.out.println("p2是"+p2);
        //修改p1的各属性值，观察p2的各属性值是否跟随变化
        p1.setName("小傻瓜");
        a.setAge(99);
        System.out.println("修改后的p1是"+p1);
        System.out.println("修改后的p2是"+p2);
    }
}

class Person{
    //两个属性值：分别代表值传递和引用传递
    private Age age;
    private String name;
    public Person(Age age,String name) {
        this.age=age;
        this.name=name;
    }
    //拷贝构造方法
    public Person(Person p) {
        this.name=p.name;
        this.age=p.age;
    }
    
    public void setName(String name) {
        this.name=name;
    }
    
    public String toString() {
        return this.name+" "+this.age;
    }
}

class Age{
    private int age;
    public Age(int age) {
        this.age=age;
    }
    
    public void setAge(int age) {
        this.age=age;
    }
    
    public int getAge() {
        return this.age;
    }
    
    public String toString() {
        return getAge()+"";
    }
}
```

实现方式二：**重写clone()方法:**

```java
/* clone方法实现浅拷贝 */
public class ShallowCopy {
    public static void main(String[] args) {
        Age a=new Age(20);
        Student stu1=new Student("摇头耶稣",a,175);
        
        //通过调用重写后的clone方法进行浅拷贝
        Student stu2=(Student)stu1.clone();
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
        
        //尝试修改stu1中的各属性，观察stu2的属性有没有变化
        stu1.setName("大傻子");
        //改变age这个引用类型的成员变量的值
        a.setAge(99);
        //stu1.setaAge(new Age(99));    使用这种方式修改age属性值的话，stu2是不会跟着改变的。因为创建了一个新的Age类对象而不是改变原对象的实例值
        stu1.setLength(216);
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
    }
}

/*
 * 创建年龄类
 */
class Age{
    //年龄类的成员变量（属性）
    private int age;
    //构造方法
    public Age(int age) {
        this.age=age;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public String toString() {
        return this.age+"";
    }
}
/*
 * 创建学生类
 */
class Student implements Cloneable{
    //学生类的成员变量（属性）,其中一个属性为类的对象
    private String name;
    private Age aage;
    private int length;
    //构造方法,其中一个参数为另一个类的对象
    public Student(String name,Age a,int length) {
        this.name=name;
        this.aage=a;
        this.length=length;
    }
    //eclipe中alt+shift+s自动添加所有的set和get方法
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    
    public Age getaAge() {
        return this.aage;
    }
    
    public void setaAge(Age age) {
        this.aage=age;
    }
    
    public int getLength() {
        return this.length;
    }
    
    public void setLength(int length) {
        this.length=length;
    }
    //设置输出的字符串形式
    public String toString() {
        return "姓名是： "+this.getName()+"， 年龄为： "+this.getaAge().toString()+", 长度是： "+this.getLength();
    }
    //重写Object类的clone方法
    public Object clone() {
        Object obj=null;
        //调用Object类的clone方法，返回一个Object实例
        try {
            obj= super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return obj;
    }
}
```

#### 深拷贝：引用类型的属性也重新拷贝一份

实现方式一：**重写clone方法**

**对象图**的概念。设想一下，一个类有一个对象，其成员变量中又有一个对象，该对象指向另一个对象，另一个对象又指向另一个对象，直到一个确定的实例。这就形成了对象图。那么，对于深拷贝来说，不仅要复制对象的所有基本数据类型的成员变量值，还要为所有引用数据类型的成员变量申请存储空间，并复制每个引用数据类型成员变量所引用的对象，直到该对象可达的所有对象。也就是说，对象进行深拷贝要**对整个对象图进行拷贝**！

解决方法是使用递归，引用类型的字段也进行递归clone

为对象图的**每一层的每一个对象都实现Cloneable接口并重写clone方法**，最后在最顶层的类的重写的clone方法中调用所有的clone方法即可实现深拷贝。简单的说就是：每一层的每个对象都进行浅拷贝=深拷贝

```java
package linearList;
/* 层次调用clone方法实现深拷贝 */
public class DeepCopy {
    public static void main(String[] args) {
        Age a=new Age(20);
        Student stu1=new Student("摇头耶稣",a,175);
        
        //通过调用重写后的clone方法进行浅拷贝
        Student stu2=(Student)stu1.clone();
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
        System.out.println();
        
        //尝试修改stu1中的各属性，观察stu2的属性有没有变化
        stu1.setName("大傻子");
        //改变age这个引用类型的成员变量的值
        a.setAge(99);
        //stu1.setaAge(new Age(99));    使用这种方式修改age属性值的话，stu2是不会跟着改变的。因为创建了一个新的Age类对象而不是改变原对象的实例值
        stu1.setLength(216);
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
    }
}

/*
 * 创建年龄类
 */
class Age implements Cloneable{
    //年龄类的成员变量（属性）
    private int age;
    //构造方法
    public Age(int age) {
        this.age=age;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public String toString() {
        return this.age+"";
    }
    
    //重写Object的clone方法
    public Object clone() {
        Object obj=null;
        try {
            obj=super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return obj;
    }
}
/*
 * 创建学生类
 */
class Student implements Cloneable{
    //学生类的成员变量（属性）,其中一个属性为类的对象
    private String name;
    private Age aage;
    private int length;
    //构造方法,其中一个参数为另一个类的对象
    public Student(String name,Age a,int length) {
        this.name=name;
        this.aage=a;
        this.length=length;
    }
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    
    public Age getaAge() {
        return this.aage;
    }
    
    public void setaAge(Age age) {
        this.aage=age;
    }
    
    public int getLength() {
        return this.length;
    }
    
    public void setLength(int length) {
        this.length=length;
    }
    public String toString() {
        return "姓名是： "+this.getName()+"， 年龄为： "+this.getaAge().toString()+", 长度是： "+this.getLength();
    }
    //重写Object类的clone方法
    public Object clone() {
        Object obj=null;
        //调用Object类的clone方法——浅拷贝
        try {
            obj= super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        //调用Age类的clone方法进行深拷贝
        //先将obj转化为学生类实例
        Student stu=(Student)obj;
        //学生类实例的Age对象属性，调用其clone方法进行拷贝
        stu.aage=(Age)stu.getaAge().clone();
        return obj;
    }
}
```

实现方式二：通过**对象序列化和反序列化**

注意对象得实现serizable, 但transient修饰的属性不能序列化

```java
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

/* 通过序列化实现深拷贝 */
public class DeepCopyBySerialization {
    public static void main(String[] args) throws IOException, ClassNotFoundException  {
        Age a=new Age(20);
        Student stu1=new Student("摇头耶稣",a,175);
        //通过序列化方法实现深拷贝
        ByteArrayOutputStream bos=new ByteArrayOutputStream();
        ObjectOutputStream oos=new ObjectOutputStream(bos);
        oos.writeObject(stu1);
        oos.flush();
        ObjectInputStream ois=new ObjectInputStream(new ByteArrayInputStream(bos.toByteArray()));
        Student stu2=(Student)ois.readObject();
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
        System.out.println();
        //尝试修改stu1中的各属性，观察stu2的属性有没有变化
        stu1.setName("大傻子");
        //改变age这个引用类型的成员变量的值
        a.setAge(99);
        stu1.setLength(216);
        System.out.println(stu1.toString());
        System.out.println(stu2.toString());
    }
}

/*
 * 创建年龄类
 */
class Age implements Serializable{
    //年龄类的成员变量（属性）
    private int age;
    //构造方法
    public Age(int age) {
        this.age=age;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public String toString() {
        return this.age+"";
    }
}
/*
 * 创建学生类
 */
class Student implements Serializable{
    //学生类的成员变量（属性）,其中一个属性为类的对象
    private String name;
    private Age aage;
    private int length;
    //构造方法,其中一个参数为另一个类的对象
    public Student(String name,Age a,int length) {
        this.name=name;
        this.aage=a;
        this.length=length;
    }
    //eclipe中alt+shift+s自动添加所有的set和get方法
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    
    public Age getaAge() {
        return this.aage;
    }
    
    public void setaAge(Age age) {
        this.aage=age;
    }
    
    public int getLength() {
        return this.length;
    }
    
    public void setLength(int length) {
        this.length=length;
    }
    //设置输出的字符串形式
    public String toString() {
        return "姓名是： "+this.getName()+"， 年龄为： "+this.getaAge().toString()+", 长度是： "+this.getLength();
    }
}
```

### maven

##### dependencyManagement

```
子项目中引用一个依赖而不用显示的列出版本号。Maven会沿着父子层次向上走，直到找到一个拥有dependencyManagement元素的项目，然后它就会使用在这个dependencyManagement元素中指定的版本号。

dependencyManagement里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖。如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中写了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且version和scope都读取自父pom;另外如果子项目中指定了版本号，那么会使用子项目中指定的jar版本。
```

##### dependencies

```
相对于dependencyManagement，所有生命在dependencies里的依赖都会自动引入，并默认被所有的子项目继承。
```

### command line is too long. shorten command line for xxx

```
.idea 
在 workspace.xml 文件中搜索：

<component name="PropertiesComponent">
1
在这块配置中加上一条：

<property name="dynamic.classpath" value="true" />
```

### Java Web

#### webapp中的jsp文件访问静态类

webapp中的jsp文件访问不到java下的静态成员frame.jsp访问不到		Constants.USER_SESSION

#### maven的jsp依赖

```xml
<dependency>
  <groupId>javax.servlet.jsp</groupId>
  <artifactId>javax.servlet.jsp-api</artifactId>
  <version>2.3.1</version>
  <scope>provided</scope>
</dependency>

<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
  <version>3.1.0</version>
  <scope>provided</scope>
</dependency>
```

#### jsp异常报错

1. 报错信息

   ```java
   catalina.loader.WebappClassLoaderBase.checkThreadLocalsForLeaks
   ```

2. 在Java 9上运行时，需要在JVM命令行参数中添加“-add opens=Java.base/Java.

3. **原因**：

   - 一个tomcat启动了两个进程。
   - sh shutdown.sh不能完全杀死tomcat或者是不能立马杀死tomcat
   - tomcat的con/server.xml中的context属性reloadable默认为true导致。

#### ${name}无法解析

或者The content of element type "web-app" must match "(icon?,display-name?,description?,

1. **解决**：web.xml版本过低导致不能解析，web-app换成下面高级版本就行

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
	http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
```

#### $pagecontext无法解析

1. **解决**：在jsp页面头部加上

```
<%@ page language="java" contentType="text/html; charset=utf-8" pageEncoding="utf-8" isELIgnored="false"%>
```

#### 解决端口占用

```
#查询出8080端口被那些进程占用着
netstat -ano | findstr 8080
#关闭进程
tasklist | findstr <进程号>
#强制关闭
taskkill -PID <进程号> -F
```

#### HttpServletResponse

NoClassDefFoundError

```java
javax/servlet/http/HttpServletResponse NoClassDefFoundError
```

1. 打开file--ProjectStructure--Libraries
2. 添加tomcat安装目录下lib目录下的Servlet-api.jar包，问题就解决了

#### tomcat10一些莫名奇妙的错误

1. 可能就是tomcat10 需要jakarta,然而jakarta和javax可能许多内容不兼容，所以导致出错
2. 可以降低tomcat为9或8

#### Error java 错误 不支持发行版本5

1. 用maven模板maven-archetype-web-app创建即可解决

#### /**  和 / 等的区别

?    匹配任何单字符         

/  当前页面

/*    匹配0或者任意数量的字符         

/**    匹配0或者更多的目录 

post处理视图解析之前执行

![image-20211012204148150](javaNote.assets/image-20211012204148150.png)

#### jsp访问本地页面

![image-20211004173356407](javaNote.assets/image-20211004173356407.png)

requestMpaping(produces="utf8")解决中文乱码

![image-20211006215128899](javaNote.assets/image-20211006215128899.png)

内容协商：

messageconverter 

获取客户端的accept: xml;q=0.9 json;q=0.8之类

获取服务器能生产的producible 

 进行最佳匹配。能生产什么记得导相应坐标，比如xml得自己导

```xml
 <dependency>
     <groupId>com.fasterxml.jackson.dataformat</groupId>
     <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

![image-20211012204108221](javaNote.assets/image-20211012204108221.png)

![image-20211013203657159](javaNote.assets/image-20211013203657159.png)

可以使用@Ordered(int)来设置优先级

## JVM

### JVM核心参数

**JVM 内存相关的几个核心参数**

| 序号   | 参数                                           | 解释                                                         |
| ------ | ---------------------------------------------- | ------------------------------------------------------------ |
| **1**  | **-Xms**                                       | Java 堆内存初始大小                                          |
| **2**  | **-Xmx**                                       | Java 堆内存最大大小                                          |
| **3**  | **-Xmn**                                       | Java 堆内存新生代大小，堆内存 - 新生代 = 老年代大小          |
| **4**  | **-Xss**                                       | 线程栈内存大小                                               |
| 5      | **-XX:PermSize** / **-XX:MetaspaceSize**       | 永久代 / 元空间初始大小 （jdk 1.7 / jdk 1.8 ）               |
| 6      | **-XX:MaxPermSize** / **-XX:MaxMetaspaceSize** | 永久代 / 元空间（默认无上限）最大大小 （jdk 1.7 / jdk 1.8 ） |
| **7**  | **-XX:MaxTenuringThreshold**                   | 指定次数GC后对象进入老年代                                   |
| 8      | **-XX:HandlePromotionFailure**                 | 是否设置空间分配担保，jdk 1.7 后废弃                         |
| **9**  | **-XX:SurvivorRatio**                          | 新生代 Eden 区域比例（默认8，表示1:1:8）                     |
| 10     | **-XX:TargetSurvivorRatio**                    | 动态年龄判断比例                                             |
| **11** | **-XX:PretenureSizeThreshold**                 | 进入老年代的大对象字节                                       |
| **12** | **-XX:+UseParNewGC**                           | ParNew 垃圾回收器，专用于新生代                              |
| 13     | **-XX:ParallelGCThreads**                      | ParNew 垃圾回收器线程数                                      |
| **14** | **-XX:+UseConcMarkSweepGC**                    | CMS 垃圾回收器，专用于老年代                                 |
| **15** | **-XX:CMSInitiatingOccupancyFraction**         | 触发 CMS 回收的内存比例，默认 92%                            |
| **16** | **-XX:+UseCMSInitiatingOccupancyOnly**         | 使用指定的 CMS 回收比例（no.15），如果不指定，在第一次使用后，JVM 会根据运行时数据动态调整，一般不指定此参数。 |
| **17** | **-XX:+ UseCMSCompactAtFullCollection**        | CMS 回收后进行内存整理，JDK 1.8 已弃用，后续版本可能会删除   |
| **18** | **-XX:+CMSFullGCsBeforeCompaction**            | 几次 CMS 回收后进行内存整理，默认 0，JDK 1.8 已弃用，后续版本可能会删除 |
| **19** | **-XX:+CMSParallelInitialMarkEnabled**         | CMS “初始标记阶段” 开启多线程并发执行                        |
| **20** | **-XX:+CMSScavengeBeforeRemark**               | CMS “重新标记阶段” 前执行 YGC，尽量减少扫描对象              |
| **21** | **-XX:+CMSParallelRemarkEnabled**              | 开启并行的Remark，与（no.20）一起用                          |
| **22** | **-XX:+DisableExplicitGC**                     | 禁止显式触发 GC，如：Runtime.getRuntime().gc();              |
| **23** | **-XX:+HeapDumpOnOutOfMemoryError**            | OOM时自动 dump 内存快照                                      |
| **24** | **-XX:HeapDumpPath**                           | 内存快照存放路径                                             |
| **25** | **-XX:+UseG1GC**                               | 指定 G1 垃圾回收器                                           |
| 26     | **-XX:G1HeapRegionSize**                       | 指定 Region 块的大小                                         |
| 27     | **-XX:G1NewSizePercent**                       | 新生代初始占比，默认 5%                                      |
| 28     | **-XX:G1MaxNewSizePercent**                    | 新生代最大占比，默认 60%                                     |
| 29     | **-XX:InitiatingHeapOccupancyPercent**         | 堆内存中老年代占比多少会触发混合回收，默认 45%               |
| 30     | **-XX:G1MixedGCCountTarget**                   | 混合回收阶段，控制回收次数，默认为 8 次                      |
| 31     | **-XX:G1HeapWastePercent**                     | 混合回收阶段，Region 空闲比例，达到时会暂停回收              |
| 32     | **-XX:G1MixedGCLiveThresholdPercent**          | 指定 Region 中存活对象低于指定值可以回收，默认为 85%         |
| 33     | **-XX:GCTimeRatio**                            | 希望在GC花费不超过应用程序执行时间的1/(1+n)，n为大于0小于100的整数。 |
| **34** | **-XX:MaxGCPauseMillis**                       | STW 的时间                                                   |
| **35** | **-XX:G1ReservePercent**                       | G1为**分配担保预留的空间**比例，即老年代**给新生代预留的空间比例**，超过此比例老年代就会 FGC，默认 10% |
| **36** | **-XX:+PrintGCDetails**                        | 打印 GC 日志详情                                             |
| 37     | **-XX:+PrintFlagsInitial**                     | 打印 JVM 初始化参数                                          |
| 38     | **-XX:+PrintGCTimeStamps**                     | 输出GC的时间戳（以基准时间的形式）                           |
| 39     | **-XX:+PrintGCDateStamps**                     | 输出GC的时间戳（以日期的形式，如 2013-05-04T21:53:59.234+0800） |
| 40     | **-XX:+PrintCommandLineFlags**                 | 打印HotSpotVM 采用的自动优化参数                             |
| 41     | **-XX:+PrintTenuringDistribution**             | JVM 在每次新生代GC时，打印出幸存区中对象的年龄分布。         |
| 42     | **-XX:+PrintGCApplicationStoppedTime**         | 打印 STW 停顿时间                                            |
| 43     | **-XX:+PrintGCApplicationConcurrentTime**      | 打印非 STW 运行时间                                          |
| **44** | **-Xloggc**                                    | 指定GC log的位置，以文件输出                                 |
| 45     | **-XX:CompressedClassSpaceSize**               | 指定 Metaspace 下类压缩空间大小，**指定这个参数时，对 Metaspace 大小的指定才有效** |
| 46     | **-XX:-UseCompressedClassPointers**            | 关闭类压缩功能                                               |
| 47     | **-XX:+UnlockExperimentalVMOptions**           | 解锁实验参数，允许使用实验性参数，JVM中有些参数不能通过-XX直接复制需要先解锁，比如要使用某些参数的时候，可能不会生效，需要设置这个参数来解锁；一般使用在一些低版本jdk想使用高级参数或者可能高版本有的参数情况； |

 **–XX:NewRatio** 默认2，表示new:old=1：2

**JVM模板**

**1. ParNew + CMS 版**

根据服务调整 -Xmx -Xms -Xmn 大小即可

-server 

-Xmx1g  

-Xms640m   

-Xmn512m  

-Xss1m 

-XX:SurvivorRatio=9  

-XX:MetaspaceSize=128m 

-XX:MaxMetaspaceSize=128m 

-XX:CompressedClassSpaceSize=128m

-XX:MaxTenuringThreshold=5 

-XX:+UseParNewGC 

-XX:+UseConcMarkSweepGC 

-XX:CMSInitiatingOccupancyFraction=92 

-XX:+CMSParallelInitialMarkEnabled 

-XX:+CMSScavengeBeforeRemark

-XX:+PrintGCDetails

**2. G1 版**

根据服务调整 -Xmx -Xms -Xmn 大小即可

-server 

-Xmx1g  

-Xms640m   

-Xss1m 

-XX:MetaspaceSize=128m 

-XX:MaxMetaspaceSize=128m 

-XX:CompressedClassSpaceSize=128m

-XX:MaxTenuringThreshold=5 

-XX:+UseG1GC

-XX:+UnlockExperimentalVMOptions

-XX:G1NewSizePercent=30

-XX:G1MaxNewSizePercent=80

-XX:MaxGCPauseMillis=50

-XX:+PrintGCDetails

​    ![0](javaNote.assets/32086)

**基本数据类型占用字节大小**

| 类型     |               | 存储大小                      | 范围                        | 默认值 | 包装类    |
| -------- | ------------- | ----------------------------- | --------------------------- | ------ | --------- |
| 整数类型 | int           | 4字节（32位）                 | -2^31 ~ 2^31 -1             | 0      | Integer   |
| short    | 2字节（16位） | -2^15 ~ 2^15 -1               | 0                           | Short  |           |
| long     | 8字节（64位） | -2^63 ~ 2^63 -1               | 0                           | Long   |           |
| byte     | 1字节（8位）  | -2^7 ~ 2^7 -1                 | 0                           | Byte   |           |
| 浮点类型 | float         | 4字节（32位）                 | 3.402823e+38 ~ 1.401298e-45 | 0.0f   | Float     |
| double   | 8字节（64位） | 1.797693e+308~ 4.9000000e-324 | 0                           | Double |           |
| 字符类型 | char          | 2字节（16位）                 | \u0000~\uFFFF               | ‘0’    | Character |
| 布尔类型 | boolean       | 1/8字节（1位）                | true, false                 | false  | Boolean   |

\1. 分析系统压力点在哪里？ 

\2. 压力点的每秒请求数？ 

\3. 每个请求耗时？ 

\4. 每个请求消耗的内存？ 

\5. 整个系统的所有请求重复1-4。 

\6. 算出部署多少台机器？每个机器多少内存？ 

**大致估算的方法**

1、支付系统高分期需要处理的请求是是不是应该这么算：100万 / （24 * 3600） ≈ 12，根据28法则，大部分请求发生在中午12点到13点以及晚上的18点到19点，所以 80万请求 / （2 * 3600） ≈ 111，即算出如果单台每秒大概是100多个请求

 2、还有就是在完整的支付系统内存占用需要进行预估中，你提到“可以把之前的计算结果扩大10倍~20倍。也就是说每秒除了内存里创建的支付订单对象还创建数十种对象” 这里如果要计算的话 之前的计算结果是 30 * 500字节 * 20倍 = 300000字节=300KB

​    ![0](javaNote.assets/32087)

**JVM 参数设置思路**

​    ![0](javaNote.assets/32088)

### happens-before规则

1、单线程规则：**同一个线程中的每个操作**都happens-before于出现在**其后**的任何一个操作。

2、对一个**监视器的解锁**操作happens-before于每一个**后续对同一个监视器的加锁操作**。

3、对**volatile**字段的**写入**操作happens-before于每一个后续的对同一个volatile字段的**读**操作。

4、**Thread.start**()的调用操作会happens-before于启动线程里面的操作。

5、一个线程中的所有操作都happens-before于其他线程成功返回在该线程上的**join**()调用后的所有操作。

6、一个对象构造函数的结束操作happens-before与该对象的finalize的开始操作。

7、传递性规则：如果A操作happens-before于B操作，而B操作happens-before与C操作，那么A动作happens-before于C操作。

8、实际上这组happens-before规则定义了操作之间的**内存可见性**，如果A操作happens-before B操作，那么A操作的执行结果(比如对变量的写入)必定在执行B操作时可见。

1. **程序顺序**规则
2. **监视器**锁规则
3. **volatile**变量规则
4. **传递性**
5. **start**()规则
6. **join**()规则

简介
happens-before是JMM的核心概念。理解happens-before是了解JMM的关键。


1、设计意图
JMM的设计需要考虑两个方面，分别是程序员角度和编译器、处理器角度：

程序员角度，希望内存模型易于理解、易于编程。希望是一个强内存模型。
编译器和处理器角度，希望减少对它们的束缚，以至于编译器和处理器可以做更多的性能优化。希望是一个弱内存模型。

因此JSR-133专家组设计JMM的核心目标就两个：

为程序员提供足够强的内存模型
对编译器和处理器的限制尽可能少

下面通过一段代码来看JSR-133如何实现这两个目标：

double pi = 3.14;			//A
double r  = 1.0;			//B
double area = pi * r * r 	//C
1
2
3
上述代码存在如下happens-before关系：

A happens-before B
B happens-before C
A happens-before C
这3个happens-before关系中，第二个和第三个是必须的，而第一个是非必须的（A、B操作之间重排序，程序执行结果不会发生改变）。
JMM把happens-before要求禁止的重排序分为下面的两类：

会改变程序执行结果的重排序
不会改变程序执行结果的重排序
JMM对这两种不同性质的重排序，采取了不同的策略：

对于会改变程序执行结果的重排序，JMM要求编译器和处理器必须禁止
对于不会改变程序执行结果的重排序，JMM不做要求（JMM运行）


JMM设计示意图：

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTI1MjE5,size_16,color_FFFFFF,t_70#pic_center.png)

JMM设计示意图
总结：

JMM给程序员提供的happens-before规则能满足程序员的需求。简单易懂，具有足够强的内存可见性保证。
JMM对编译器和处理器的束缚尽可能少。遵循的原则是：不改变程序的执行结果（正确同步或单线程执行），编译器和处理器可以任意优化。
2、happens-before的定义
起源：
happens-before规则来源于Leslie Lamport《Time, Clocks and the Ordering of Events in a Distributed System》。该论文中使用happens-before来定义分布式系统中事件之间的偏序关系（partial ordering），该文中给出了一个分布式算法，能用来将偏序关系扩展为某种全序关系。


Java中的应用：
JSR-133使用happens-before来指定两个操作之间的执行顺序。JMM可以通过happens-before关系向程序员提供跨线程的内存可见性保证。


《JSR-133：Java Memory Model and Thread Specification》对happens-before关系的定义如下：

如果操作A happens-before 操作B，那么A操作的执行结果将会对操作B可见，且操作A的执行顺序排在操作B之前——JMM对程序员的承诺
两个操作存在happens-before关系，并不意味着Java平台的具体实现必须按照happens-before的顺序来执行。如果重排序不改变程序执行结果（与happens-before）规则一致，那么这种重排序是不非法的（JMM允许这种重排序）。——JMM对编译器和处理器的束缚原则

happens-before和as-if-serial语义：
从上述来看，happens-before和as-if-serial语义本质上是一回事

as-if-serial语义保证单线程内程序的执行结果不被改变，happens-before关系保证正确同步的多线程程序的执行结果不改变
as-if-serial语义给编程者一种单线程是按程序顺序执行的幻境；happens-before关系给编程者一种正确同步的多线程是按照happens-before指定的顺序执行的幻境。
两者的目的都是为了在不改变程序执行结果的前提下，尽可能的提高程序的执行效率。


3、happens-before规则
《JSR-133：Java Memory Model and Thread Specification》定义了如下happens-before规则

程序顺序规则
监视器锁规则
volatile变量规则
传递性
start()规则
join()规则

3.1 volatile写-读
volatile写-读建立的happens-before关系

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTI1MjE5,size_16,color_FFFFFF,t_70#pic_center-166234430247113.png)

happens-before关系示意图

分析上图：
1 happens-before 2和3 happens-before 4由程序顺序规则产生。由于编译器和处理器遵循as-if-serial语义，也就是说，as-if-serial语义保证了程序顺序规则。因此可以把程序顺序规则看成是对as-if-serial语义的“封装”。
2 happens-before 3 是有volatile规则产生。一个volatile变量的读，总是能看到（任意线程）对这个volatile变量的最后写入。
1 happens-before 4 是由传递性规则产生的。这里的传递性是由volatile的内存屏障插入策略和volatile的编译器重排序规则来共同保证的。



3.2 start()规则
假设线程A在执行的过程中，通过执行ThreadB.start()来启动线程B；同时，假设线程A在执行ThreadB.start()之前修改了一个共享变量，线程B在执行后会读取这些共享变量。
start()程序对应的happens-before关系图：

![在这里插入图片描述]()


分析上图：

1 happens-before 2 由程序顺序规则产生
2 happens-before 4 由start规则产生
1 happens-before 4 由传递性规则产生
因此线程A执行ThreadB.start()之前对共享变量所做的修改，在线程B执行后都将确保对线程B可见。

3.3 join()规则
假设线程A执行的过程中，通过执行ThreadB.join()来等待线程B终止；则线程B在终止之前修改了一些共享变量，线程A从ThreadB.join()返回后会读这些共享变量。
join()程序的happens-before关系图：

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTI1MjE5,size_16,color_FFFFFF,t_70#pic_center-166234432148217.png)


分析上图：

2 happens-before 4 由join()规则产生
4 happens-before 5 由程序顺序规则产生
2 happens-before 5 由传递性规则产生
因此线程A执行操作ThreadB.join()并成功返回，线程B中任意操作都将对线程A可见。

### JVM四种内存屏障

LoadLoad Barriers	Load1;LoadLoad;Load2	该屏障确保Load1数据的装载先于Load2及其后所有装载指令的的操作

StoreStore Barriers	Store1;StoreStore;Store2	该屏障确保Store1立刻刷新数据到内存(使其对其他处理器可见)的操作先于Store2及其后所有存储指令的操作

LoadStore Barriers	Load1;LoadStore;Store2	确保Load1的数据装载先于Store2及其后所有的存储指令刷新数据到内存的操作

StoreLoad Barriers	Store1;StoreLoad;Load2	该屏障确Store1立刻刷新数据到内存的操作先于Load2及其后所有装载装载指令的操作。它会使该屏障之前的所有内存访问指令(存储指令和访问指令)完成之后,才执行该屏障之后的内存访问指令

### 对象晋升老年代

https://blog.csdn.net/qq_31387317/article/details/124929752

#### 1、动态对象年龄判断机制

假如说当前放对象的survivor区域里，一批对象的总大小大于了这块survivor区域的内存大小的50%，那么此时大于等于这批对象年龄最大的年龄的对象，就可以直接进入老年代了(一岁开始累加：1+2+。。+n>50%内存区域 ,超过n年龄的对象进入老年代)。

#### 2、新生代存活对象太多直接进入老年代

这里优化思路是：主要是在Survivor的大小这块下功夫。我们要避免动态年龄审核和Survivor放不下的情况。要想保证这点，我们就要知道，我们系统的高峰时期，JVM中每秒有多少对象新增，每次YoungGC存活了多少对象。如meimiao这就需要用 jstat 了

#### 3、大对象直接进入老年代

-XX:PretenureSizeThreshold 定义多大才是大对象，默认0意思说所有对象都在eden中分配 （字节数）；G1中呢？
需要注意避免频繁的大对象进入老年代，造成频繁的full gc

#### 4、对象躲过了15次垃圾回收（默认），进入老年代

-XX:MaxTenuringThreshold （可用通过调低该参数，让某些长久存活的对象赶紧进入老年代，释放s区空间）
该参数只有第一次设置的时候有效，后续有动态年龄判断控制，比如当触发动态年龄判断的时候年龄是n，该参数在会动态调整为N+1
调低该参数，降低动态年龄判断机制触发的概率。如果系统1分钟或者30秒一次YoungGC，那没必要非得让对象存活十几分钟才进入老年代，一般存活个两三分钟，这个对象大概率就是要存活很久的了。所以，我们当时是调低了这个参数的，设置了5。不然这个对象一直存活，然后在两个Survivor里来回复制，如果这个对象小一点还好，如果这个对象挺大的，那容易触发Survivor的动态年龄审核机制，让一大批对象进入老年代。

#### 5、空间担保机制

1. 当要MinorGC之前，首先会计算老年代剩余空间是否大于新生代所有对象大小之和(防止极端情况下eden区所有对象都幸存)。

- 如果老年代剩余内存可以放得下年轻代所有对象，那么你尽管去MinorGC，肯定不会OOM。
2. 如果剩余空间不够，但是配置了-XX:-HandlePromotionFailure参数（1.6以后废弃），那么就会计算每次MinorGC后存活对象的平均大小，如果老年代剩余内存大小大于这个平均大小，则大胆认为这次MinorGC回收后，老年代还是可以放得下。
- 试想不配该参数，eden区对象本身就朝生夕死，就会造成jvm过于悲观的判断内存不够，而频繁的full gc
3. 如果该次MinorGC之后老年代的确是放不下就进行Fulll GC，如果Full GC完了还是放不下则oom
4. 所以在MinorGC的时候，可能会发生FullGC

### 触发Full GC

Full GC相对于Minor GC来说，停止用户线程的STW（stop the world）时间过长，至少慢10倍以上，所以要尽量避免，首先说一下Full GC可能产生的原因，接着给出排查方法以及解决策略。

#### 1、System.gc()方法的调用

在代码中调用System.gc()方法会建议JVM进行Full GC，但是注意这只是建议，JVM执行不执行是另外一回事儿，不过在大多数情况下会增加Full GC的次数，导致系统性能下降，一般建议不要手动进行此方法的调用，可以通过-XX:+ DisableExplicitGC来禁止RMI调用System.gc。

#### 3、老年代（Tenured Gen）空间不足

在Survivor区域的对象满足晋升到老年代的条件时，晋升进入老年代的对象大小大于老年代的可用内存，这个时候会触发Full GC。

#### 3、永久代（perm）或元空间（Metaspace）写满

从JDK8开始，永久代(PermGen)的概念被废弃掉了，取而代之的是一个称为Metaspace的存储空间。Metaspace使用的是本地内存，而不是堆内存，也就是说在默认情况下Metaspace的大小只与本地内存大小有关。-XX:MetaspaceSize=21810376B（约为20.8MB）超过这个值就会引发Full GC，这个值不是固定的，是会随着JVM的运行进行动态调整的，与此相关的参数还有多个，详细情况请参考这篇文章[jdk8 Metaspace 调优](https://blog.csdn.net/bolg_hero/article/details/78189621)

#### 4、MaxDirectMemorySize写满

#### 检测JVM堆的情况

1. jvisualvm，jconsole
2. 采用jps找到进行id，然后使用jstat -gc pid来实时进行检测。
3. 运行程序前设置-XX:+PrintGCDetails，-XX:+PrintGCDateStamps参数打印GC的详细信息进行分析。

![img](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hvbGxha2U=,size_16,color_FFFFFF,t_70-16628032355858.png)

![img](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hvbGxha2U=,size_16,color_FFFFFF,t_70-16628032355859.png)

![img](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hvbGxha2U=,size_16,color_FFFFFF,t_70-166280323558510.png)

#### 解决策略

如果是发现由于老年代内存过小频繁引起的Full GC，那么可以适当增加老年代的内存大小，如果是发现是由于老年代没有连续空间来让初生代的对象晋升，如果是采用CMS，那么可以设置进行 n 次 CMS 后进行一次压缩式 Full GC，参数如下：

-XX:+UseCMSCompactAtFullCollection：允许在 Full GC 时，启用压缩式 GC

-XX:CMSFullGCBeforeCompaction=n   在进行 n 次，CMS 后，进行一次压缩的 Full GC，用以减少 CMS 产生的碎片。

除此之外，尽量少创建大对象，不要在代码里调用System.gc()，什么时候进行Full GC这种事情还是交给JVM来做。在读取文件后记得释放资源，不要让JVM无法回收垃圾，造成内存泄漏。

本文如果有哪些地方不对，或者有可以补充的地方希望您可以指出来，谢谢了。

#### 一、cms

1、年轻代满了 元空间满了
2、老年代可用空间小于新生代全部对象的大小，如果没开空间担保，直接Full GC 。
3、老年代可用内存小于历次新生代GC后进入老年代的平均大小，此时会提前Full GC
4、新生代minor GC后存活对象大于Survivor，那么就会进行老年代，此时老年代内存不足
5、老年代内存使用率超过92%（可调）
6、浮动垃圾大于cms可用空间。

#### 二、G1

G1的垃圾回收不一定是年轻代满了，或者老年代满了才去回收。如果是那样，就和ParNew+CMS没区别了，大内存机器也要STW好久。

1、回收年轻代
G1是基于每个Region的**性价比去回收**的，比如，Region1里有20M对象，回收2ms，Region2里有50兆对象回收要4ms。如果我们设置系统停顿时间为5ms，那G1会在要求的时间内，尽可能回收更多的对象，它会选择Region2，因为性价比更高。所以，我们系统运行，一直往Eden放对象，如果G1觉得，此时回收一下垃圾，差不多要5ms，那可能G1就回去回收，不会等到年轻代占用60%才去回收。
2、混合回收
G1的Old G也不是我们能控制的，如果**老年代占比45%**，就会触发混合回收，回收整个堆内存，但是混合回收也是会**控制在我们设置的停顿时间的范围内的，如果时间不够，就会分多次回收**。
混合回收不仅会回收老年代，还会回收新生代和大对象。如果一次性全回收掉，那时间就太久了，可能达不到我们设置的预期停顿时间，所以G1这里是分几批来回收的，回收一次，系统运行一会，然后再回收一次。JVM参数可以设置这个值，分几次去回收，默认值是8次，分8次回收。混合回收还有一个参数我们可以设置，就是空闲的Region达到百分之多少，停止回收，默认是5%。
3、Full GC
G1何时会触发Full GC，其实G1的混合回收就相当于ParNew + CMS的Full GC了，因为回收了所有的区域，只不过回收时间可以控制在我们指定的范围内。但是**G1的Full GC就没法控制了**，可能要卡顿特别久才能回收完。什么情况下会出现呢，因为G1的整体是**基于复制**算法的，如果回收的过程中，发现存活对象找不到可以复制的Region，放不下了。那就Full GC，开始单线程标记、清理、整理空闲出一批Region，这个过程很慢。

### 命令行工具

#### jps

查看正在运行的Java进程（启动JVM参数）

#### jstat

JVM统计信息，包括内存使用情况，垃圾统计次数等

#### jstack

线程堆栈信息，可查看是否会死锁

#### jinfo

实时查看和修改JVM配置参数

#### jmap

堆内存快照，类加载和实例数量

#### jhat

堆分析工具，跟jmap配合使用

#### jcmd

#### jstatd

### 垃圾回收

吞吐量：用户线程/（运行用户代码时间+运行垃圾收集时间）。



标记清除算法（低延迟）

- 从跟集合扫描，标记存活的对象。标记完毕后，再扫描整个空间未标记的对象进行回收。

- 只对未存活对象进行处理，因此适合老年代存活对象比较多的。由于直接清除未存活对象，会造成内存碎片。
- CMS（低延迟）

复制算法

- 在开始时把堆分成一个对象面和空闲面，当对象满了，扫描GC Root标记存活对象，复制到空闲面。
- 直接复制存活对象，因此适合新生代朝生夕死比较多的对象。但会浪费一半的空间。
- Serial，ParNew，Parallel Scavenge（可控制的吞吐量）

标记整理算法（吞吐量高，因为内存分配频率比垃圾回收高）

- 采用和标记清除算法一样的方式标记存活对象，但在清除的时候不同，在回收不存活对象后，会将所有存活对象往左端移动，并更新对应的指针
- 成本较高，但不会产生内存碎片问题
- SerialOld，Parallel Old





JVM系统线程：GC 编译 信号 中断任务调度 虚拟机线程（stop word 栈回收）



如何确定是垃圾

**引用计数，可达性分析**（GCRoot对象)

每次死一堆：用复制算法

存活率高的，如老年代：标记清除或压缩算法，因为只标记活的，然后清除少量死对象

ParNew就是serial的多线程版本，parScange是采用多线程复制，重点在吞吐量（用户线程占cpu的时间）

Serial-old cms parold

Cms:初始标记（stop），并发标记，重新标记（stop），并发清除,

最前沿就是g1 他比较复杂，比较智能，可根据规定的时间，最大努力清楚最多的空间

### 强软弱虚引用

软引用：不够再回收

弱引用：下一次垃圾回收就收

### HotSpot

热点代码探测技术

- 通过计数器找到最具编译价值代码，触发即时编译或栈上替换
- 通过编译器与解释器协同工作，在最优化的程序响应时间与最佳执行性能中取得平衡
- 备注：现代编译器雏形：解释器（一行一行解释，有很好的响应时间，但性能慢）+即时编译器（把经常要用到的代码先编译成机器语言，以提高性能）之间取得平衡

![image-20210919230308062](javaNote.assets/image-20210919230308062.png)

### 类加载子系统

**加载->链接（验证，准备，解析）->初始化**

![image-20201219195150300](javaNote.assets/78e0bcdff5244aeb741ac9ff242b98bb.png)

#### 一、加载load：

将字节码文件加载成方法区的运行时数据结构

#### 二、链接linking

1. 验证（Verify）：文件格式验证等

2. 准备(Prepare)：

   2.1 static类变量**分配内存**和**默认初始值**（零值）

   2.2 static+final修饰的基本数据类型或String类型**显示初始化**（final在编译的时候就会分配）

3. 解析(Resolve）

   常量池的符 b  号引用替换为直接引用

#### 三、初始化initialize

静态变量和静态代码块显示初始化，即执行 clinit() 方法

![img](javaNote.assets/v2-6e4d33e76ec925985e5039faa431ec8b_720w.jpg)

### 触发类的加载

- 访问**类变量**或**类方法**会触发类加载
- 其它启动类的**main**方法，**new**对象，**创建子类对象**，**反射**class.forName

访问编译器常量不会触发类的加载（编译器常量：public static final = 字面量）

![img](javaNote.assets/9BEA91D12AFEC41C7E936186E5BFB4B9.png)

注意事项

```
注意访问编译期常量不会触发类加载(final修饰的基本类型和字符串（用字面量赋值）)
```

![image-20220722152250247](javaNote.assets/image-20220722152250247.png)

```
下面是final修饰，但不是编译器常量（因为通过new）
```

![image-20220722152310926](javaNote.assets/image-20220722152310926.png)

```
下面没有用final修饰，连常量都不是
```

![image-20220722153112711](javaNote.assets/image-20220722153112711.png)

```
ClassLoader.loadClass只会加载把类加载JVM,但不会触发初始化
Class.forName则触发类加载和初始化
```

![image-20220722153404107](javaNote.assets/image-20220722153404107.png)

类的成员变量有默认初始化

### 父子类加载顺序

父类静态子类静态，父类非静态变量代码块构造，子类非静态变量代码块构造

父类 > 子类

静态 > 非静态

变量 > 代码块 > 构造方法

父类静态成员变量--》父类静态代码块--》子类静态成员变量--》子类静态代码块--》父类非静态成员变量--》父类非静态代码块--》父类构造方法--》子类非静态成员变量--》子类非非静态代码块--》子类构造方法

```
father 静态成员变量
father 静态代码块
Son 静态成员变量
Son 静态代码块
father 非静态成员变量
father 非静态代码块
father 构造方法
Son 非静态成员变量
Son 非静态代码块
son 构造方法
```

![image-20210919092301934](javaNote.assets/image-20210919092301934.png)

```
类加载只会初始化静态变量和静态代码块，非静态代码块是在创建对象的时候初始化的
```

![image-20220722101924235](javaNote.assets/image-20220722101924235.png)

### 双亲委派机制

![image-20210905135358218](javaNote.assets/image-20210905135358218.png)

### 运行时数据区

#### 程序计数器

用来存储指令指向下一条的地址，也即将要执行的指令代码。由执行引擎读取下一条指令。

![image-20210905135408660](javaNote.assets/image-20210905135408660.png)

它程序控制流的指示器，控制分支、异常处理等，存储当前指令的位置，大小很小可忽略不计。没有GC（垃圾回收）和OOM（内存溢出）

![image-20210905135414888](javaNote.assets/image-20210905135414888.png)

![image-20210905135419692](javaNote.assets/image-20210905135419692.png)

**面试题一：使用PC寄存器存储字节码指令地址有什么用**

1. 因为CPU需要不停地切换各个线程，这时候切换回来以后，就得知道从哪开始继续执行。

![image-20210905140417417](javaNote.assets/image-20210905140417417.png)

2. JVM的字节码解释器就需要通过改变PC寄存器存储的值来明确下一条应该执行什么样的字节码指令

**面试题二：PC寄存器为什么会被设定为线程私有**

1. 多线程在特定的时间段内只会执行线程的某一个方法，CPU会不停的做任务切换，这样必然导致经常中断或恢复，如何保证分毫无差？为了能够准确的记录各个线程正在执行的当前字节码地址，最好的方法自然是为每一个线程都分配一个PC寄存器，这样一来各个线程之间便可以进行独立计算，从而不会出现相互干扰的情况。
2. 由于CPU的时间片轮限制，众多线程在并发执行过程中，任何一个确定的时刻，一个处理器或者多核处理器的内核，只会执行某个线程中的一条指令
3. 这样必然导致经常中断或恢复，如何保证分毫无差？每个线程在创建后，都会产生自己的程序计数器和栈帧，程序计数器在各个线程之间互不影响。

![image-20210905140841770](javaNote.assets/image-20210905140841770.png)

![image-20210905144455239](javaNote.assets/image-20210905144455239.png)

#### 虚拟机栈

一个线程对应一个虚拟机栈，栈帧对应一个方法

![image-20210905144936445](javaNote.assets/image-20210905144936445.png)

![image-20210905145024545](javaNote.assets/image-20210905145024545.png)

**面试题：栈可能出现的问题**

![image-20210905145745503](javaNote.assets/image-20210905145745503.png)

![image-20210905151736485](javaNote.assets/image-20210905151736485.png)



![image-20210905153218429](javaNote.assets/image-20210905153218429.png)

![image-20210905155249801](javaNote.assets/image-20210905155249801.png)

##### 局部变量表

![image-20210906092332672](javaNote.assets/image-20210906092332672.png)

![image-20210907161754677](javaNote.assets/image-20210907161754677.png)

##### 操作数栈

![image-20210911164223489](javaNote.assets/image-20210911164223489.png)

![image-20210911164243966](javaNote.assets/image-20210911164243966.png)

![image-20210911164317385](javaNote.assets/image-20210911164317385.png)

栈顶缓存技术

![image-20210910102040369](javaNote.assets/image-20210910102040369.png)

##### 动态链接

指向运行时常量池的方法引用

为什么要常量池？使用方便，符号引用就行

![image-20210910104156974](javaNote.assets/image-20210910104156974.png)

![image-20210910103633996](javaNote.assets/image-20210910103633996.png)

##### 方法返回地址

![image-20210911170012416](javaNote.assets/image-20210911170012416.png)

![image-20210911171121249](javaNote.assets/image-20210911171121249.png)

虚拟机栈五道面试题

![image-20210911172850302](javaNote.assets/image-20210911172850302.png)

#### 堆

![image-20210911231331453](javaNote.assets/image-20210911231331453.png)

![image-20210911231717730](javaNote.assets/image-20210911231717730.png)

##### 堆的核心概述：内存细分

![image-20210912100403871](javaNote.assets/image-20210912100403871.png)

![image-20210912101520672](javaNote.assets/image-20210912101520672.png)

##### 堆空间大小的设置

![image-20210912101705981](javaNote.assets/image-20210912101705981.png)



![image-20210912104459293](javaNote.assets/image-20210912104459293.png)

![image-20210912105301194](javaNote.assets/image-20210912105301194.png)

![image-20210912105628115](javaNote.assets/image-20210912105628115.png)

##### 年轻代与老年代及参数占比

![image-20210912151928205](javaNote.assets/image-20210912151928205.png)

![image-20210912152353504](javaNote.assets/image-20210912152353504.png)

![image-20210912153237672](javaNote.assets/image-20210912153237672.png)

##### 对象分配过程

![image-20210912160420056](javaNote.assets/image-20210912160420056.png)

![image-20210912160847690](javaNote.assets/image-20210912160847690.png)

![image-20210912161052807](javaNote.assets/image-20210912161052807.png)

![image-20210912161807846](javaNote.assets/image-20210912161807846.png)

![image-20210912163246601](javaNote.assets/image-20210912163246601.png)

![image-20210912163427800](javaNote.assets/image-20210912163427800.png)

![image-20210912200324878](javaNote.assets/image-20210912200324878.png)

![image-20210912200925693](javaNote.assets/image-20210912200925693.png)

![image-20210912201331278](javaNote.assets/image-20210912201331278.png)

![image-20210912201536309](javaNote.assets/image-20210912201536309.png)

![image-20210912201706320](javaNote.assets/image-20210912201706320.png)

![image-20210912203720380](javaNote.assets/image-20210912203720380.png)

![image-20210912203934247](javaNote.assets/image-20210912203934247.png)

![image-20210912204510773](javaNote.assets/image-20210912204510773.png)



![image-20210912205036911](javaNote.assets/image-20210912205036911.png)

##### TLAB（Thread Local Allocation Buffer线程私有）

所以堆空间的内容不一定都是共享的

![image-20210912211021751](javaNote.assets/image-20210912211021751.png)

![image-20210912211320920](javaNote.assets/image-20210912211320920.png)

![image-20210912212119090](javaNote.assets/image-20210912212119090.png)

![image-20210912215432932](javaNote.assets/image-20210912215432932.png)

##### 堆空间的参数设置

![image-20210912215756662](javaNote.assets/image-20210912215756662.png)

![image-20210912215809307](javaNote.assets/image-20210912215809307.png)

![image-20210912220502348](javaNote.assets/image-20210912220502348.png)

##### 栈上分配

![image-20210912220930453](javaNote.assets/image-20210912220930453.png)

![image-20210912221121736](javaNote.assets/image-20210912221121736.png)

![image-20210912221950808](javaNote.assets/image-20210912221950808.png)

![image-20210914092901624](javaNote.assets/image-20210914092901624.png)

##### 代码优化之标量替换

![image-20210914093241261](javaNote.assets/image-20210914093241261.png)

![image-20210914094422485](javaNote.assets/image-20210914094422485.png)

![image-20210914094845565](javaNote.assets/image-20210914094845565.png)

![image-20210914194140562](javaNote.assets/image-20210914194140562.png)

#### 方法区

##### 存放内容

**类元信息，常量，静态变量，即时编译代码缓存**。运行时常量池（类元信息，常量池表，存放编译器产生的字面量和符号引用）

字符串常量池是存在堆中的

![image-20210914211051382](javaNote.assets/image-20210914211051382.png)

##### 栈、堆、方法区的交互关系

![image-20210914194333267](javaNote.assets/image-20210914194333267.png)

##### 方法区概述

![image-20210914201946249](javaNote.assets/image-20210914201946249.png)

![image-20210914202037929](javaNote.assets/image-20210914202037929.png)

##### 设置方法区内存的大小

![image-20210914205416503](javaNote.assets/image-20210914205416503.png)

![image-20210914210200618](javaNote.assets/image-20210914210200618.png)

##### 方法区内部结构

![image-20210914210539083](javaNote.assets/image-20210914210539083.png)



![image-20210914211516667](javaNote.assets/image-20210914211516667.png)

##### 常量池

![image-20210914215504672](javaNote.assets/image-20210914215504672.png)

![image-20210914215534255](javaNote.assets/image-20210914215534255.png)

![image-20210914220934866](javaNote.assets/image-20210914220934866.png)

##### 运行时常量池

存放编译器产生的各种**字面量**和符号引用（转为**真实地址**）

相对于Class文件常量池，运行时常量池具有动态性

![image-20210915211156855](javaNote.assets/image-20210915211156855.png)

 

![image-20210915211327329](javaNote.assets/image-20210915211327329.png)

##### 指令执行过程

![image-20210916201938788](javaNote.assets/image-20210916201938788.png)

![image-20210916215049324](javaNote.assets/image-20210916215049324.png)

##### 方法区的演进细节

![image-20210916215604340](javaNote.assets/image-20210916215604340.png)

![image-20210916220300399](javaNote.assets/image-20210916220300399.png)

##### 永久代为什么要被元空间替换

比较难以管理，大小难以设置（可能动态加载大量的类），容易OOM

![image-20210916221208074](javaNote.assets/image-20210916221208074.png)

##### 字符串常量池为什么要调整

![image-20210916222628714](javaNote.assets/image-20210916222628714.png)

![image-20210916222819170](javaNote.assets/image-20210916222819170.png)

![image-20210916223857775](javaNote.assets/image-20210916223857775.png)

![image-20210916225015467](javaNote.assets/image-20210916225015467.png)

![image-20210916224544873](javaNote.assets/image-20210916224544873.png)

##### 方法区的垃圾回收

![image-20210916225530992](javaNote.assets/image-20210916225530992.png)

![image-20210916230416886](javaNote.assets/image-20210916230416886.png)

![image-20210917212019389](javaNote.assets/image-20210917212019389.png)

##### 常见面试题

![image-20210917212304856](javaNote.assets/image-20210917212304856.png)

![image-20210917212535279](javaNote.assets/image-20210917212535279.png)

### 对象的实例化

![image-20210917225402526](javaNote.assets/image-20210917225402526.png)

![image-20210917230035603](javaNote.assets/image-20210917230035603.png)

![image-20210917230218021](javaNote.assets/image-20210917230218021.png)

![image-20210919201824294](javaNote.assets/image-20210919201824294.png)

![image-20210919202116673](javaNote.assets/image-20210919202116673.png)

![image-20210919202229200](javaNote.assets/image-20210919202229200.png)

![image-20210919202324536](javaNote.assets/image-20210919202324536.png)

![image-20210919202436758](javaNote.assets/image-20210919202436758.png)

![image-20210919202927147](javaNote.assets/image-20210919202927147.png)

![image-20210919203016331](javaNote.assets/image-20210919203016331.png)

![image-20210919204634088](javaNote.assets/image-20210919204634088.png)

![image-20210919215857599](javaNote.assets/image-20210919215857599.png)

![image-20210919220229199](javaNote.assets/image-20210919220229199.png)

![image-20210919220857355](javaNote.assets/image-20210919220857355.png)

![image-20210919221108965](javaNote.assets/image-20210919221108965.png)

![image-20210919221446852](javaNote.assets/image-20210919221446852.png)

##### 直接内存

![image-20210919221926180](javaNote.assets/image-20210919221926180.png)

![image-20210919222244331](javaNote.assets/image-20210919222244331.png)

![image-20210919223545814](javaNote.assets/image-20210919223545814.png)

![image-20210919223722116](javaNote.assets/image-20210919223722116.png)

![image-20210919223745573](javaNote.assets/image-20210919223745573.png)

![image-20210919224512588](javaNote.assets/image-20210919224512588.png)

<img src="javaNote.assets/image-20210919230134834.png" alt="image-20210919230134834" style="zoom:200%;" />

### 执行引擎

JVM将字节码装在到其内部成字节码指令（仅被JVM识别），再由**执行引擎将字节码指令翻译成本地机器语言**

![image-20210920093417965](javaNote.assets/image-20210920093417965.png)



![image-20210920092702727](javaNote.assets/image-20210920092702727.png)

![image-20210920093121685](javaNote.assets/image-20210920093121685.png)

![image-20210920095612655](javaNote.assets/image-20210920095612655.png)

#### 解释器

![image-20210921130034469](javaNote.assets/image-20210921130034469.png)

![image-20210921130055864](javaNote.assets/image-20210921130055864.png)

### **GC** **Roots**

![image-20211107162107077](javaNote.assets/image-20211107162107077.png)

![image-20211107162521730](javaNote.assets/image-20211107162521730.png)

![image-20211107163833419](javaNote.assets/image-20211107163833419.png)

### **对象的finalize机制**

![image-20211107165830657](javaNote.assets/image-20211107165830657.png)

![image-20211110202838469](javaNote.assets/image-20211110202838469.png)

![image-20211109171108493](javaNote.assets/image-20211109171108493.png)

### CMS

![image-20211110193439041](javaNote.assets/image-20211110193439041.png)

![image-20211110195909278](javaNote.assets/image-20211110195909278.png)

![image-20211110200127901](javaNote.assets/image-20211110200127901.png)

### G1

全能垃圾回收期，大内存，多CPU



局部就是赋值算法，整体就是整理算法

记忆集和卡表，避免跨代引用的全表扫描



1、年轻代并行回收（STW，回收eden园区和survivor区）

2、老年代并发标记（堆达到45%）,会触发yGC

3、混合回收（回收整个年轻代和部分老年代）

4、兜底的Full GC



年轻代GC

GCroot

rset

处理rser

复制存活对象

处理引用，空region记录到空闲链表中

![image-20220915143617545](javaNote.assets/image-20220915143617545.png)



MIX GC

![image-20220915144122582](javaNote.assets/image-20220915144122582.png)

![image-20220915142907040](javaNote.assets/image-20220915142907040.png)

![image-20211110202525372](javaNote.assets/image-20211110202525372.png)

![image-20211110203410075](javaNote.assets/image-20211110203410075.png)

![image-20211110203736253](javaNote.assets/image-20211110203736253.png)

![image-20211110211519869](javaNote.assets/image-20211110211519869.png)

![image-20211111100924269](javaNote.assets/image-20211111100924269.png)

## 操作系统

### MBR

MBR，全称为Master Boot Record，即硬盘的**主引导记录**，它**位于整个硬盘的0磁道0柱面1扇区**（所以**不需要开始标记**），其主要对硬盘进行了组织，是在驱动器最前端的一段引导扇区。

MBR是不属于任何一个操作系统，也不能用操作系统提供的磁盘操作命令来读取它，但可以通过命令来修改和重写。

#### 一、四大组成部分

1、**主引导程序**（偏移地址0000H--0088H），它负责从活动分区中装载，并运行系统引导程序。

2、**出错信息数据区**，偏移地址0089H--00E1H为出错信息，00E2H--01BDH全为0字节。

3、**分区表**（DPT,Disk Partition Table）含4个分区项，偏移地址01BEH--01FDH,每个分区表项长16个字节，共64字节为分区项1、分区项2、分区项3、分区项4。

4、**结束标志字**，偏移地址01FE--01FF的2个字节值为结束标志55AA,称为“魔数”（magic number）。如果该标志错误系统就不能启动。

#### 二、MBR的修复

BR在某些情况下，如病毒或者分区操作不当会引起MBR代码段的损坏，表现的现象就是电脑启动时，屏幕出现黑底一个或几个无意义的字母闪光标或无任何提示闪光标。这种情况在确认硬盘无物理故障后，可以使用一些简单方法进行恢复。

**Dos命令**

使用任意启动盘启动到MSDOS提示符，键入命令：

fdisk /mbr

**Diskgenius**

用启动盘，无论dos版或者pe版均可，启动diskgenius，然后选择菜单“硬盘”-“重建主引导记录”，为避免病毒残留，还可执行一次”硬盘“-”清除保留扇区“

**Windows xp命令**

xp之下，需要安装tool kit附加工具，为系统增加一个fixmbr命令行工具。执行命令之前，先将故障硬盘挂载到一台好的电脑，或者使用xp安装盘启动电脑，然后执行命令：

fixmbr \Device\HardDisk0 此处的0或其他数字需先通过diskpart工具的list driver进行查找。

**Windows 7命令**

修复方式同xp，只是命令换成bootrec /fixmbr

### 子进程

进程得到的是除了代码段是与父进程共享以外，**其他所有的都是得到父进程的一个副本**，子进程的所有资源都继承父进程，得到父进程资源的副本，子进程**可获得父进程的所有堆和栈的数据**，**但二者并不共享地址空间**。两个是单独的进程，继承了以后二者就没有什么关联了，子进程单独运行。

父进程没了，子进程会托管到1号进程中

### 指令周期

指令周期是取出一条指令并执行这条指令的时间

### 线程调度

![image-20220904215024210](javaNote.assets/image-20220904215024210.png)

下列关于线程调度的叙述中，错误的是：( D )

A. 调用线程的sleep()方法,可以使比当前线程优先级低的线程获得运行机会

B. 调用线程的yield()方法,只会使与当前线程相同优先级的线程获得运行机会

C. 当有比当前线程优先级高的线程出现时,高优先级的线程将抢占CPU并运行

D. 具有相同优先级的多个线程的调度一定是分时的.

E.一个线程由于某些原因进入阻塞状态，会放弃CPU

F.分时调度模型是让所有线程轮流获得CPU使用权

解析：

**yield()暂时交出cpu控制权，从running状态转为runnalbe状态**，但是仍有可能被调度，sleep()线程指定休眠一段时间

wait()在其他线程调用此对象的notify()、notifyAll()方法时才能继续执行

### wait()&sleep()&yeild()&join()

1.sleep()方法会给其他线程运行的机会,而**不管其他线程的优先级,**因此会给较低优先级的线程运行的机会;

yeild()方法**只会给优先级相同的或者比自己高的线程运行**的机会

2.sleep()方法声明抛出**InterruptionException**异常,而yeild()方法没有声明抛出任何异常

3.sleep()方法比yeild()方法具有更高的可移植性

4.sleep()方法使线程进入**阻塞**状态yeild()方法使线程进入**就绪**状态当前运行的线程可以调用另一个线程的join()方法,当前运行的线程将转到阻塞状态直到另一个线程运行结束,它才会恢复运行

join()有两种形式:public void join()和public void join(long timeout)可以设置阻塞的时间

sleep()方法进入阻塞状态，当有两个线程（线程1和线程2），线程1的优先级比线程2的优先级高，线程1sleep()则线程2可以获得运行机会

当有比当前线程优先级高的线程出现时，高优先级会抢占CPU并运行，yield()方法，暂停一段时间，且这段时间不确定，它会使与当前线程相同优先级的线程获得运行机会

具有相同优先级的多个线程调度不一定是分时的，**多核CPU可能同时调**

### CPU寻址空间

 前言：
  我们都熟知**32为的操作系统的寻址空间的大小为4G**(2^32)，因此我们安装一个32位系统在配置4g的内存条，这似乎非常完美。但是当我们打开任务管理器发现我们的物理内存只有3g左右。

#### 寻址空间：

  寻址空间一般指的是CPU对于内存寻址的能力。通俗地讲，就是**最多能用到多少内存**的一个问题。数据在存储器（RAM）中存放是有规律的，CPU在运算的时间需要把数据取出来，就必须 需要知道数据储存在哪里，这时我们需要挨家挨户地找（也就是在其能够寻址的空间进行查找），这就叫做寻址。

但是**如果地址超出了CPU的寻址范围，CPU就无法找到数据了**。CPU最大查找多大范围的地址叫做寻址能力，CPU的寻址能力以字节为单位。

  那么我们便可以推出，内存的容量并非需要无限的增大，虽然内存容量越大，处理数据的能力也就越强，但是它要受到系统结构，硬件设计，制造成本等多方面因素的影响。最直接的因素就是：系统地址总线的地址寄存器的宽度（位数）。

  计算机的**寻找范围由总线宽度（处理器的地址总线的位数）决定**的，也可以理解为cpu寄存器位数，这二者一般是匹配的。

386及386往上的地址总线和地址寄存器的**宽度为32位**的，**CPU的寻址能力2^32 = 4096M字节= 4G字节**。

所以呢，早期的CPU即使有很大的内存也不能得到利用，而对于现在的PⅡ级的CPU，其寻址能力已经远远超过目前的内存容量。

  所以：地址总线为N位（N通常为8的整数倍；也说N根数据总线 ）的CPU寻址范围是2的N次方字节，即2^N(B)。

16，32，64位通常指的是什么？
从CPU的发展史来看，从前的8位到现在的64位。

8位就是CPU在一个时钟周期内可以并行处理8位二进制字符0或1，那么16和64以此类推。

从计算的角度理论上来讲64位比32位快一半。但是因为电脑是软硬件相配合才能发挥最佳性能的，所以操作系统也必须从32位的到64位的，而且硬件驱动也必须是64位的。我们在64位CPU的计算机中安装64位的操作系统的32位硬件驱动是不能用的。如果64CPU装32的操作系统的话，那性能不会有明显提升。

为什么是2的N次方，而不是其他数的N次方
  因为**计算机采用二进制计算的，一根地址总线，我们可想而知他最多能对2个存储单元进行寻址**。因为在任何的二进制计算机中，所有物理元件只有0，1两种状态，所以对应这个例子，我们假设已经把这根唯一的地址总线与两个储存单元a和b连上了，那么究竟怎么确定何时读a何时读b？当地址线上的电压是高电压时我们读a，相反是低电压时，我们读b。如此一来，一根地址总线只能对2个存储单元进行寻址，以此类推那么2根就是对应4个储存单元，所以N根就是对应2^N个储存单元。

  一根地址总线是怎么连接到两个存储单元的？？

什么是存储单元
  存储单元一般具有储存数据和读写数据的动能，一般以8位二进制作为一个储存单元，也就是一个字节。每个单元有一个地址，是一个整数编码，可以表示为二进制数。

什么是物理内存
  我们都知道32位的操作系统可以寻找4G大小的内存空间。因此我们安装一个32位系统在配置4G的内存条，看起来是一个完美的方案。可是，当我们安装好系统配好内存，打开任务管理器后，发现我们的物理内存只有3G左右，这是怎么回事呢？

  物理内存：在计算机体系中，物理内存不仅仅包括装在主板上的内存条（RAM），还包括**主板BIOS芯片的ROM**，**显卡上的显存（RAM）和BIOS(ROM)**,以及各种设备上的储存空间。所以说我们的实际的物理内存空间达不到4G，也就是我们那1G空间是给一些**输入输出缓存器等的不可访问的区域**。

### DMA

传统的磁盘IO，整个数据的传输过程，都要需要 CPU 亲自参与搬运数据的过程，而且这个过程，CPU 是不能做其他事情的。

![img](javaNote.assets/I_O 中断.png)



DMA（直接内存访问）

在进行 **I/O 设备和内存的数据传输的时候，数据搬运的工作全部交给 DMA 控制器**，而 CPU 不再参与任何与数据搬运相关的事情，这样 **CPU 就可以去处理别的事务**。

DMA就是**代替CPU完成IO设备到内核缓存区的拷贝**

![img](javaNote.assets/DRM I_O 过程.png)

- 用户进程调用 read 方法，向操作系统发出 I/O 请求，请求读取数据到自己的内存缓冲区中，进程进入阻塞状态；
- 操作系统收到请求后，进一步将 I/O 请求发送 DMA，然后让 CPU 执行其他任务；
- DMA 进一步将 I/O 请求发送给磁盘；
- 磁盘收到 DMA 的 I/O 请求，把数据从磁盘读取到磁盘控制器的缓冲区中，当磁盘控制器的缓冲区被读满后，向 DMA 发起中断信号，告知自己缓冲区已满；
- **DMA 收到磁盘的信号，将磁盘控制器缓冲区中的数据拷贝到内核缓冲区中，此时不占用 CPU，CPU 可以执行其他任务**；
- 当 DMA 读取了足够多的数据，就会发送中断信号给 CPU；
- CPU 收到 DMA 的信号，知道数据已经准备好，于是将数据从内核拷贝到用户空间，系统调用返回；

### 零拷贝

#### 1、mmap+write

`mmap()` 系统调用函数会直接把内核缓冲区里的数据「**映射**」到用户空间，这样，**操作系统内核与用户空间就不需要再进行任何的数据拷贝操作**。

```c
buf = mmap(file, len);
write(sockfd, buf, len);
```

![img](javaNote.assets/mmap %2B write 零拷贝.png)

![img](javaNote.assets/200501092691998.png)

- 应用进程调用了 `mmap()` 后，DMA 会把磁盘的数据拷贝到内核的缓冲区里。接着，应用进程跟操作系统内核「共享」这个缓冲区；
- 应用进程再调用 `write()`，操作系统直接将内核缓冲区的数据拷贝到 socket 缓冲区中，这一切都发生在内核态，由 CPU 来搬运数据；
- 最后，把内核的 socket 缓冲区里的数据，拷贝到网卡的缓冲区里，这个过程是由 DMA 搬运的。

我们可以得知，通过使用 `mmap()` 来代替 `read()`， 可以减少一次数据拷贝的过程。

但这还不是最理想的零拷贝，因为仍然需要通过 CPU 把内核缓冲区的数据拷贝到 socket 缓冲区里，而且**仍然需要 4 次上下文切换**，因为**系统调用还是 2 次**

#### 2、sendfile

在 Linux 内核版本 2.1 中，提供了一个专门发送文件的系统调用函数 `sendfile()`，函数形式如下：

```c
#include <sys/socket.h>
ssize_t sendfile(int out_fd, int in_fd, off_t *offset, size_t count);
```

它的前两个参数分别是目的端和源端的文件描述符，后面两个参数是源端的偏移量和复制数据的长度，返回值是实际复制数据的长度。

首先，它可以**替代前面的 `read()` 和 `write()` 这两个系统调用**，这样就可以减少一次系统调用，也就减少了 2 次上下文切换的开销。

其次，该系统调用，可以直接把内核缓冲区里的数据拷贝到 socket 缓冲区里，不再拷贝到用户态，这样就**只有 2 次上下文切换**，和 **3 次数据拷贝**。如下图：

![img](javaNote.assets/senfile-3次拷贝.png)



如果网卡支持 SG-DMA（*The Scatter-Gather Direct Memory Access*）技术（和普通的 DMA 有所不同），我们可以进一步减少通过 CPU 把内核缓冲区里的数据拷贝到 socket 缓冲区的过程。

 `sendfile()` 系统调用的过程发生了点变化，具体过程如下：

- 第一步，通过 DMA 将磁盘上的数据拷贝到内核缓冲区里；
- 第二步，**缓冲区描述符和数据长度传到 socket 缓冲区**，这样网卡的 SG-DMA 控制器就可以**直接将内核缓存中的数据拷贝到网卡的缓冲区**里，此过程不需要将数据从操作系统内核缓冲区拷贝到 socket 缓冲区中，这样就减少了一次数据拷贝；

所以，这个过程之中，只进行了 2 次数据拷贝，如下图：

![img](javaNote.assets/senfile-零拷贝.png)

这就是所谓的零拷贝（Zero-copy）技术，因为我们没有在内存层面去拷贝数据，也就是说全程没有通过 CPU 来搬运数据，所有的数据都是**通过 DMA 来进行传输**的。

零拷贝技术的文件传输方式相比传统文件传输的方式，减少了 2 次上下文切换和数据拷贝次数，**只需要 2 次上下文切换和数据拷贝次数，就可以完成文件的传输，而且 2 次的数据拷贝过程，都不需要通过 CPU，2 次都是由 DMA 来搬运。**

所以，总体来看，**零拷贝技术可以把文件传输的性能提高至少一倍以上**。



Kafka 作为一个消息队列，涉及到磁盘 I/O 主要有两个操作：

- Provider 向 Kakfa 发送消息，Kakfa 负责将消息以日志的方式持久化落盘；
- Consumer 向 Kakfa 进行拉取消息，Kafka 负责从磁盘中读取一批日志消息，然后再通过网卡发送；

Kakfa 服务端**接收 Provider 的消息**并持久化的场景下使用 **mmap** 机制，能够基于**顺序磁盘 I/O** 提供高效的持久化能力，使用的 Java 类为 java.nio.MappedByteBuffer。

Kakfa 服务端**向 Consumer 发送消息**的场景下使用 **sendfile** 机制[7]，这种机制主要两个好处：

- sendfile 避免了内核空间到用户空间的 CPU 全程负责的数据移动；
- **sendfile 基于 Page Cache 实现，因此如果有多个 Consumer 在同时消费一个主题的消息，那么由于消息一直在 page cache 中进行了缓存，因此只需一次磁盘 I/O，就可以服务于多个 Consumer**；

> 使用 **mmap 来对接收到的数据进行持久化**
>
> 使用 **sendfile 从持久化介质中读取数据然后对外发送**是一对常用的组合。
>
> 但是注意，你无法利用 sendfile 来持久化数据，利用 mmap 来实现 CPU 全程不参与数据搬运的数据拷贝。

### PageCache

#### 缓存和预读

**1、PageCache 来缓存最近被访问的数据**，当空间不足时淘汰最久未被访问的缓存。

**2、PageCache 使用了「预读功能」**

假设 read 方法每次只会读 `32 KB` 的字节，虽然 read 刚开始只会读 0 ～ 32 KB 的字节，但内核会把其后面的 32～64 KB 也读取到 PageCache，这样后面读取 32～64 KB 的成本就很低



由于零拷贝使用了 PageCache 技术，但不适合大文件传输

- PageCache 由于**长时间被大文件占据**，其他「热点」的小文件可能就无法充分使用到 PageCache，于是这样磁盘读写的性能就会下降了；
- PageCache 中的大文件数据，**由于没有享受到缓存带来的好处，但却耗费 DMA 多拷贝到 PageCache 一次**；



### 直接 I/O

异步 I/O 并没有涉及到 PageCache

**大文件传输用什么方式实现**

在**高并发**的场景下，针对大文件的传输的方式，应该使用「**异步 I/O + 直接 I/O**」来替代零拷贝技术。



![img](javaNote.assets/异步 IO 的过程.png)

- 传输大文件的时候，使用「异步 I/O + 直接 I/O」；
- 传输小文件的时候，则使用「零拷贝技术」；

### 父子进程

子进程是父进程的一个副本，得到父进程的**资源**副本和**所有堆和栈数据**。

但两者**不共享虚拟地址**空间，因为是两个独立的进程。

![image-20220727214451070](javaNote.assets/image-20220727214451070.png)

### 上下文切换

1. **内存管理**上下文。 包括加载页表、刷出地址转换后备缓冲器，向内存管理单元提供新的信息。
2. **页表切换**，这就是重新装载全局页表，用于**给进程安装一个新的虚拟地址空间**。
3. 由于进程的栈都在内核态，所以**切换内核态堆栈上下文数据**。
4. 硬件上下文，主要部分就是**进程和CPU的任务状态寄存器**，就是TSS中的字段。在这里CPU为了减轻很多切换的工作，很多地方都是如果有必要，就切换，就是所谓的惰性原则。

进程上下文切换：

保存CPU寄存器和程序计数器

进程状态到PCB中

虚拟内存，内核堆栈



引起上下文切换：

时间片用完

系统资源不足，进程挂起等待资源满足

调用sleep主动挂起

高优先级的进程抢占

硬件中断，CPOU进程挂起，转而执行硬件中断服务程序



进程调度信息，不属于上下文的内容，那是操作系统进程调度的范畴

![image-20220727100545822](javaNote.assets/image-20220727100545822.png)

```
CPU调度的是线程，而不是作业
```

![image-20220724224432728](javaNote.assets/image-20220724224432728.png)

### 文件磁盘分配

文件分配对应于文件的物理结构，是指如何为文件分配磁盘块。常用的磁盘空间分配方 法有三种：连续分配、链接分配和索引分配。

- 顺序分配：顺序 分配方法要求每个文件在磁盘上占有一组连续的块。
- 隐式链接分配： 每个文件对应一个磁盘块的链表；磁盘块分布在磁盘的任何地方，除最后一个盘块外，每一个盘块都有指向下一个盘块的指针，这些指针对用户是透明的。
- 显式链接分配：是指把用于链接文件各物理块的指针，**显式地存放在内存的一张链接表**中。 该表在**整个磁盘仅设置一张**，**每个表项中存放链接指针，即下一个盘块号**。 在该表中，凡是 属于某一文件的第一个盘块号，或者说是每一条链的链首指针所对应的盘块号，均作为文件地址被填入相应文件的FCB的“物理地址”字段中。由于查找记录的过程是在内存中进行 的，因而不仅显著地提高了检索速度，而且大大减少了访问磁盘的次数。由于**分配给文件的所有盘块号都放在该表中**，故称该表为**文件分配表**（File Allocation Table, **FAT)。MS-DOS 采用的就是这种方式**。

![image-20220801141246385](javaNote.assets/image-20220801141246385.png)

### 磁盘调度

**为什么需要磁盘调度算法？**

磁盘调度算法是为了提高磁盘的访问性能，一般是通过优化磁盘的访问请求顺序来做的。其中**寻道是磁盘较为耗时的部分**，因此如果请求顺序得当，可以节省一些不必要的寻道时间。

**寻道算法有几种？**

1、先来先服务 FCFS
根据进程请求的先后顺序进行调度。
优点：**公平**、算法简单，每个进程的请求都可以得到满足，不会出现某进程的长期请求得不到处理的情况。
缺点：没有对寻道算法进行优化，平**均寻道时间可能比较长**。
2、最短寻道时间有限 SSTF
选择要求访问的磁盘与当前磁头所在的磁道距离最近，这样**每次的寻道时间最短**，但不能保证平均寻道时间最短。

可以会来回循环
3、扫描算法 SCAN 电梯算法
优先考虑磁头当前的移动方向，然后是访问的磁道和当前磁道的距离。
4、循环扫描算法 CSCAN

算法 规定磁头只能做**单向移动**，返回时 I confirm that I will attend the online paper test

5、LOOK与C-LOOK算法

LOOK算法和C-LOOK算法分别是对扫描算法和循环扫描算法的优化，优化的思路就是：**磁头在移动到最远的请求位置，然后立刻向反方向移动。**

#### **先来先服务算法**

如果请求的顺序如下：

98，183，37，122，14，124，65，67

那么磁盘的写入顺序如下图：

![img](javaNote.assets/v2-dc0687d0df15832994a877ba659ad1ff_720w.jpg)

大量应用进程竞争使用磁道，访问的磁道一般比较分散，这种算法性能低下，寻道时间过长。

#### **最短寻道算法**

该算法优先选择从当前磁头位置所需寻道时间最短的请求，

如果请求的顺序如下：

98，183，37，122，14，124，65，67

那么磁盘的写入顺序为：65，67，37，14，98，122，如下图：

![img](javaNote.assets/v2-fae404691e68afefeea5954b14f2c299_720w.jpg)

该算法相对于先来先服务寻道时间会减少很多，但是会造成饥饿现象，因为我们的磁盘的请求随时都可能产生，假设后续的请求都是小于183磁道，那么183磁道的请求永远不会被响应，于是就产生了饥饿现象。

#### **扫描算法**（电梯算法）

磁头在一个方向上移动，访问所有未完成的请求，直到磁头到达该方向上的最后的磁道才调换方向。

如果请求的顺序如下：

98，183，37，122，14，124，65，67

假设前进的方向是磁道号减少的方向，那么处理请求的顺序是37，14，0，65，67，98，122，124，183，如下图：

![img](javaNote.assets/v2-62ccffc47bffb4a5ae4eda844fb05d09_720w.jpg)

扫描算法虽然不会产生饥饿，但是对于中间部分的磁道来说响应较快，边缘部分响应较慢。

#### **循环扫描算法**

循环扫描算法规定：磁头只能朝某个方向移动，**返回时直接复位磁头**（这个很快），并且返回过程中不处理任何请求。

如果请求的顺序如下：

98，183，37，122，14，124，65，67

假设磁头先朝磁道增加的方向移动，处理请求顺序则是：65，67，98，122，124，183，199，0，14，37，如下图：

![img](javaNote.assets/v2-df7992f221d1da36aeefa9a12d88054a_720w.jpg)

循环扫描算法相比于扫描算法，每个磁道的响应频率比较平均。

#### **LOOK与C-LOOK算法**

LOOK算法和C-LOOK算法分别是对扫描算法和循环扫描算法的优化，优化的思路就是：**磁头在移动到最远的请求位置，然后立刻向反方向移动。**

- LOOK算法反向移动途中会响应请求
- C-LOOK反向移动途中不响应请求

### Reactor模式

```
NIO+IO多路复用
```

#### IO复用

对于accept、connect、read、write等系统调用，实际上都属于慢系统调用，他可能会永远阻塞直到套接字上发生 可读\可写 事件。事实上，通常不希望一直阻塞直到IO就绪，而应该等待IO就绪之后再通知我们过来处理。

IO复用可以通过 select、poll、epoll来实现。这里只简单说下epoll。

epoll就是实现这个功能的，使用epoll只需要三步：

1. 调用epoll_create创建套接字epfd。
2. 调用epoll_ctl 增加需要关心的套接字的事件，如 listenfd的可读事件。
3. 调用epoll_wait沉睡，直到有关心的事件发生后epoll_wait会主动返回,此时我们去处理发生了IO事件的相应套接字即可。



具体的epoll用法这里不再细说。在这里把epoll看成一个黑匣子即可，暂时不关心原理。我们只需要将关心得套接字事件注册到epoll上，epoll就会在这些事件发生时通知我们。

#### Reactor模型

Reactor 模式主要由 Reactor 和处理资源池这两个核心部分组成，它俩负责的事情如下：

- **Reactor 负责监听和分发**事件，事件类型包含连接事件、读写事件；

- **处理资源池负责处理事件**，如 read -> 业务逻辑 -> send；

  

Netty、Redis等软件都使用到了Reactor模式。

Reacor模式是一种**事件驱动机制**，他逆转了事件处理的流程，不再是主动地等事件就绪，而是它提前注册好的回调函数，当有对应事件发生时就调用回调函数。 Reactor即为非阻塞IO + IO复用，单个Reactor的逻辑大致如下

```text
while(!stop) {
    // 1.取得下次定时任务的时间，与设定time_out去较大值，即若下次定时任务时间超过1s就取下次定时任务时间为超时时间，否则取1s
    int time_out = Max(1000, getNextTimerCallback());
    // 2.调用Epoll等待事件发生，超时时间为上述的time_out
    int rt = epoll_wait(epfd, fds, ...., time_out); 
    if(rt < 0) {
        // epoll调用失败。。
    } else {
        if (rt > 0 ) {
            // 3. 以此处理发生IO时间的fd，调用其回调函数
        }
    }
}
```

它的核心思想就是利用IO复用技术来监听套接字上的读写事件，一旦某个fd上发生相应事件，就反过来处理该套接字上的回调函数。



#### 1、 单Reactor单线程

单Reactor服务器模型就是只有一个主线程运行Reactor。整个线程有一个epoll句柄，用于管理所有的套接字。服务器将listenfd的读事件注册到epoll上，当epoll_wait返回时说明listenfd可读，即有新的连接建立。此时再调用accept函数获取新连接clientfd，然后将clientfd的读写事件也注册到这个epoll上，等待clientfd发生读写事件从epoll_wait返回后，再处理clientfd的事件。

- Reactor 对象通过 select （IO 多路复用接口） 监听事件，收到事件后通过 dispatch 进行分发，具体分发给 Acceptor 对象还是 Handler 对象，还要看收到的事件类型；
- 如果是连接建立的事件，则交由 Acceptor 对象进行处理，Acceptor 对象会通过 accept 方法 获取连接，并创建一个 Handler 对象来处理后续的响应事件；
- 如果不是连接建立事件， 则交由当前连接对应的 Handler 对象来进行响应；
- Handler 对象通过 read -> 业务处理 -> send 的流程来完成完整的业务流程。

![img](javaNote.assets/单Reactor单进程.png)

 **Redis** 6.0 版本之前采用的正是「单 Reactor 单进程」的方案，因为 Redis 业务处理主要是在内存中完成，操作的速度是很快的，性能瓶颈不在 CPU 上，所以 Redis 对于命令的处理是单进程的方案

```cpp
// 单Reactor模型
while(!stop) {
    // 1.取得下次定时任务的时间，与设定time_out去较大值，即若下次定时任务时间超过1s就取下次定时任务时间为超时时间，否则取1s
    int time_out = Max(1000, getNextTimerCallback());
    // 2.调用Epoll等待事件发生，超时时间为上述的time_out
    int rt = epoll_wait(epfd, fds, ...., time_out); 
    if(rt < 0) {
        // epoll调用失败。。
    } else {
        if (rt > 0 ) {
          foreach (fd in fds) {
            if (是listenfd的可读事件) {
            // 如果是连接事件
              1. 获取连接 clientfd = accept();
              2. 将clientfd的IO注册到epoll上
            } else {
            // 不是连接事件，那就是clientfd的读写事件，此时需要处理业务逻辑
              dothing(fds[i]）;
            }
          }
          
        }
    }
}
```

#### 2、单Reactor多线程

对于clienfd发生读写事件后，需要进行业务逻辑处理。业务逻辑处理通常是耗时的，这会影响主线程的执行，也就是说主线程会等到 dothing(fds[i])做完之后才进入下一次循环过程。

加入线程池可以一定程度上优化：

```text
// 单Reactor + 线程池模型
while(!stop) {
    // 1.取得下次定时任务的时间，与设定time_out去较大值，即若下次定时任务时间超过1s就取下次定时任务时间为超时时间，否则取1s
    int time_out = Max(1000, getNextTimerCallback());
    // 2.调用Epoll等待事件发生，超时时间为上述的time_out
    int rt = epoll(epfd, fds, ...., time_out); 
    if(rt < 0) {
        // epoll调用失败。。
    } else {
        if (rt > 0 ) {
          foreach (fd in fds) {
            if (是listenfd的可读事件) {
            // 如果是连接事件
              1. 获取连接 clientfd = accept();
              2. 将clientfd的IO注册到epoll上
            } else {
            // 不是连接事件，那就是clientfd的读写事件，此时需要处理业务逻辑
              // 1.线程池里面取一个线程
              // 2.用该线程处理这个套接字上的业务逻辑
              thread = threadpoll.get();
              thread.dothing(fd[i]);
            }
          }
          
        }
    }
}
```

将业务逻辑处理也可以交给线程池来做，主线程继续进行Reactor循环。从而很大程度上减小了主线程的负担，提高并发量。这就是单Reactor+线程池的模型。

![img](javaNote.assets/单Reactor多线程.png)

#### 3、 多Reactor多线程

要解决「单 Reactor」的问题，就是将「单 Reactor」实现成「多 Reactor」，这样就产生了第 **多 Reactor 多进程 / 线程**的方案。

老规矩，闻其名不如看其图。多 Reactor 多进程 / 线程方案的示意图如下（以线程为例）：

![img](javaNote.assets/主从Reactor多线程.png)

方案详细说明如下：

- 主线程中的 MainReactor 对象通过 select 监控连接建立事件，收到事件后通过 Acceptor 对象中的 accept 获取连接，将新的连接分配给某个子线程；
- 子线程中的 SubReactor 对象将 MainReactor 对象分配的连接加入 select 继续进行监听，并创建一个 Handler 用于处理连接的响应事件。
- 如果有新的事件发生时，SubReactor 对象会调用当前连接对应的 Handler 对象来进行响应。
- Handler 对象通过 read -> 业务处理 -> send 的流程来完成完整的业务流程。

多 Reactor 多线程的方案虽然看起来复杂的，但是实际实现时比单 Reactor 多线程的方案要简单的多，原因如下：

- 主线程和子线程分工明确，主线程只负责接收新连接，子线程负责完成后续的业务处理。
- 主线程和子线程的交互很简单，主线程只需要把新连接传给子线程，子线程无须返回数据，直接就可以在子线程将处理结果发送给客户端。

大名鼎鼎的两个开源软件 Netty 和 Memcache 都采用了「多 Reactor 多线程」的方案。

采用了「多 Reactor 多进程」方案的开源软件是 Nginx，不过方案与标准的多 Reactor 多进程有些差异。

具体差异表现在主进程中仅仅用来初始化 socket，并没有创建 mainReactor 来 accept 连接，而是由子进程的 Reactor 来 accept 连接，通过锁来控制一次只有一个子进程进行 accept（防止出现惊群现象），子进程 accept 新连接后就放到自己的 Reactor 进行处理，不会再分配给其他子进程。

### 一致性哈希

使用传统的hash%n，如果节点增加或减少会导致数据大部分迁移。

哈希环，将节点映射到环上的每个位置

key映射环后下一个就是要找的节点，如果某个节点没了或添加，只需要**部分数据进行迁移**。

为了防止雪崩，使用**虚拟节点**。

![img](javaNote.assets/30c2c70721c12f9c140358fbdc5f2282.png)

部分数据迁移

![img](javaNote.assets/f8909edef2f3949f8945bb99380baab3.png)

![img](javaNote.assets/31485046f1303b57d8aaeaab103ea7ab.png)

### Ext3

**1、高可用性**
系统使用了ext3文件系统后，即使在非正常关机后，系统也不需要检查文件系统。宕机发生后，恢复ext3文件系统的时间只要数十秒钟。
**2、数据的完整性**
ext3文件系统能够极大地提高文件系统的完整性，避免了意外宕机对文件系统的破坏。在保证数据完整性方面，ext3文件系统有2种模式可供选择。其中之一就是“同时保持文件系统及数据的一致性”模式。采用这种方式，你永远不再会看到由于非正常关机而存储在磁盘上的垃圾文件。
**3、文件系统的速度**
尽管使用ext3文件系统时，有时在存储数据时可能要多次写数据，但是，从总体上看来，ext3比ext2的性能还要好一些。这是因为ext3的日志功能对磁盘的驱动器读写头进行了优化。所以，文件系统的读写性能较之Ext2文件系统并来说，性能并没有降低。
**4、数据转换**
由ext2文件系统转换成ext3文件系统非常容易，只要简单地键入两条命令即可完成整个转换过程，用户不用花时间备份、恢复、格式化分区等。用一个ext3文件系统提供的小工具tune2fs，它可以将ext2文件系统轻松转换为ext3日志文件系统。另外，ext3文件系统可以不经任何更改，而直接加载成为ext2文件系统。
**5、多种日志模式**
Ext3有多种日志模式，一种工作模式是对所有的文件数据及metadata（定义文件系统中数据的数据,即数据的数据）进行日志记录（data=journal模式）；另一种工作模式则是只对metadata记录日志，而不对数据进行日志记录，也即所谓data=ordered或者data=writeback模式。系统管理人员可以根据系统的实际工作要求，在系统的工作速度与文件数据的一致性之间作出选择。

### 死锁

![image-20220912113709934](javaNote.assets/image-20220912113709934.png)

**银行家算法用于避免死锁**

**资源有序分配**破坏环路等待条件

死锁：在多道程序设计环境下，多个进程可能竞争一定数量的资源，。一个进程申请资源，如果资源不可用，那么进程进入等待状态。如果所申请的资源被其他等待进程占有，那么该等待的进程有可能无法改变状态，这种情况下称之为死锁。

#### **四个条件**

- 互斥：**至少有一个资源**必须处在**非共享**模式，即一次只能有一个进程使用，如果另一进程申请该资源，那么申请进程必须延迟直到该资源释放为止。

- 占有并等待：一个进程必须**占有**至少一个资源，并**等待**另一个资源，而该资源为其他进程所占有。

- 非抢占：**资源不能被抢占**
- 循环等待：有一组进程{P0,P1,...Pn},P0等待的资源被P1占有，P1等待的资源被P2占有，Pn-1等待的资源被Pn占有，Pn等待的资源被P0占有。

#### 死锁避免

1、**银行家算法**可以避免死锁产生，防止系统进入不安全状态

2、资源**有序分配**（避免环路等待）。

3、**一次性申请所需所有资源**，若满足则全部分配，否则一个也不分配（破坏占用并等待）

4、**请求未果释放已有资源**

#### 死锁检测

**jstack**线程堆栈分析工具

#### 死锁解除

剥夺进程的资源

1. 死锁检测并恢复

- 对于互斥而言：有的资源本身就是互斥的，所以通常无法破坏这一必要条件。

- 对于占有并等待：每一个进程执行前一次性申请完所有资源。或者 每个进程申请当前所需要的资源，当需要使用其他资源时，需要把之前申请的资源释放掉。前者可以理解为破坏**等待**，后者可以理解为破坏**占有**。

  这样做使得资源得利用率很低（最后阶段可能需要用一下打印机，而将其在整个运行期占有）；对于优先级低得进程来说，多次释放资源很容易造成它们饥饿。

- 对于非抢占：破坏它，即对于已经分配的资源可以进行抢占。当一个优先级比较低，那么它的资源往往会被优先级高得剥夺，导致它饥饿。

- 对于循环等待：对所有资源类型进排序，要求每个进程按照资源编号递增顺序申请资源。可以用反证法证明。简要描述一下，在进程按照资源编号递增顺序申请资源的条件下，假设一个循环等待存在，即有一组进程{P0,P1,...Pn},P0等待的资源被P1占有，P1等待的资源被P2占有，Pn-1等待的资源被Pn占有，Pn等待的资源被P0占有。那么Pi+1占有了Ri资源，同时又申请Ri+1，所以资源Ri的编号必然小于Ri+1，那么R0的编号小于R1的....Rn资源的编号小于R0资源的编号（Pn进程）。根据传递性，R0的编号小于R0的编号，显然矛盾，因此，在上述条件下，不会产生循环等待。

#### 不会发生死锁的条件

假设有8个进程，每个需要k个资源，总共有n个资源，那么满足

n-(k-1)*8>=1就不会发生死锁

![image-20220904171451902](javaNote.assets/image-20220904171451902.png)

### 进程线程协程

![image-20220804215734164](javaNote.assets/image-20220804215734164.png)

#### 一、进程

系统资源分配和独立运行的基本单位。

一个进程至少有一个线程，我们将它称为主线程（main线程）

##### 1、进程如何创建

（1）申请一个空白PCB
（2）分配运行所需要的资源，如内存、文件、IO设备、CPU
（3）初始化PCB,比如设置进程为就绪状态或静止就绪状态，优先级，程序计数器指向程序入口地址，栈指针指向栈顶

##### 2、PCB（进程控制块）

保存进程的控制和管理信息

（1）外部标识符（用户提供），内部标识符（OS设置的序号）
（2）进程调度信息：比如当前进程状态（以等待CPU多长时间，已执行多长时间）优先级等
（3）进程控制信息：进程同步和通信机制存放在PCB，比如消息对列指针和信号量，下一个PCB的指针

##### 3、进程的同步

**信号量和管程**（Monitors）
管程：定义公共的数据结构如消息队列，主要进行同步操作
操作系统内核
简介：常用设备的驱动程序，一些频率高的模块如时钟管理和进程调度，他们常驻内存。
作用：比较保护他们防止被破坏，同时提高OS的运行效率。
终止进程：正常结束，异常退出（越界，算术异常等）

#### 二、线程

是进程中的一条执行序列（执行流）

共享进程的资源(地址空间和文件描述符)，所以不用进行页表切换

轻型进程，CPU调度的基本单位。

有自己独立的寄存器和栈，切换开销小

线程之间**传递数据不需要经过内核态**

减少并发执行的时间和空间开销

##### 1、线程的实现

(1)用户级线程
存在用户空间，被用户进程进行创建和调度，无需切换内核，切换速度快，只有当系统调用时，才会映射到内核控制线程LWP(Light Weight Process)

进程内没有特权进行线程切换，所以只能等线程自己执行完

(2)内核级线程
内核线程是由操作系统管理的，线程对应的 TCB 自然是放在操作系统里的，这样线程的创建、终止和管理都是由操作系统负责。

##### 2、线程三种基本状态：

（1）就绪（Ready）: 得到Cpu以外的所有资源，会存入就绪队列
（2）运行（running）: 获得CPU正在执行
（3）阻塞（Block）: 运行中的线程IO请求或申请资源失败，会进入阻塞队列

如何引入挂起操作
（1）用户自己要停止进程查看问题
（2）父进程要修改子进程
（3）系统自己操作，进行负荷调节，系统繁忙，挂起一些不重要的进程



#### 三、协程

1、协程只是一个特殊的函数，是用户态，只是能在某个地方挂起，并且可以在挂起处外继续运行，所以不会太消耗资源
2、进程是内核态，进程包括CPU，数据和PCB进程控制块

A正确  协程不是被操作系统内核所管理的，而是完全由程序所控制，也就是在用户态执行，所以A正确。这样带来的好处是性能大幅度的提升，因为不会像线程切换那样消耗资源。
B正确 操作系统进行资源管理的最小单位是进程，操作系统的最小调度单位是线程，进程给线程提供执行环境。
C错误 协程不是进程也不是线程，而是一个特殊的函数，这个函数可以在某个地方挂起，并且可以重新在挂起处外继续运行。所以说，协程与进程、线程相比并不是一个维度的概念。
D正确  一个进程中可以有多个线程，而线程独有的资源有栈和寄存器和线程局部存储，简称TLS，其实就是个线程私有的全局变量。

![image-20220716134450840](javaNote.assets/image-20220716134450840.png)

### 进程通信方式

进程用户地址空间是相互隔离的，所以要通信要经过内核

#### 1、管道

匿名管道

没有名称，本质是**内核的一段缓存**，采用**半双工通信**,**只能单向通信**，数据是**无格式的字节流**且大小受限，符合先进先出，生命周期跟进程一样.

当管道满时，进程在 写管道会被阻塞，而当管道空时，进程读管道会被**阻塞**

管道可以**同时进行读进程和写进程**

通过调用pipe得到读写描述符进行，由于存在同一个进程中，所以匿名管道**只用于父子进程通信**，子进程会复制父进程的文件描述符。

命名管道

**可进行不同进程的通信**，提前建立了类型为管道的设备文件，访问这个设备文件就可以通信

#### 2、消息队列

保存在内核的**消息链表**，使用用户**自定义数据类型**的消息体为单位传递数据，**发送消息后就可以返回**，读完就删除消息

消息队列**通信不及时**，**消息大小有限制**，内核态到用户态的**消息拷贝开销**

需要主动释放消息队列，如果没有释放消息队列进程终止也还会继续存在

#### 3、共享内存

信号量初始值由用户确定

**解决了数据拷贝的开销**，通过虚拟地址，映射到一块公共的物理内存空间，即共享内存

一个进程读写，另外进程就能够快速看到，**通信速度快**

#### 4、信号量

由于共享内存操作同块内存，所以会有互相覆盖的危险，所以需要信号量来进行同步。

一个**整形计数器**表示资源的数量，实现互斥操作，通过PV原子操作控制信号量

- **P操作**需要**减少**信号量，如果<0表明资源已被占用，需要阻塞等待。相减后>=0，表明还有资源，进程可继续运行

- V操作**增加**信号量，相加后<=0表明有进程处于阻塞，需要唤醒操作。相加后>0表明当前没有阻塞的进程

  ![PV 操作的算法描述](javaNote.assets/17-操作系统PV算法描述.jpg)

#### 5、信号

信号是进程间通信的唯一异步通信机制，可以在任何时候发送信号给某一进程，用户进程收到信号有如下几种处理方式：

忽略信号。SIGKILL和SIGSTOP无法捕捉和忽略，用于任何时候中断或结束某一进程。

执行默认操作。每种信号都规定了默认操作

捕捉信号。我们可以为信号定义一个信号处理函数。当信号发生时，我们就执行相应的信号处理函数。

kill -9就是SIGKILL信号

Ctrl+C产生SIGTINT信号，终止进程

Ctrl+Z产生SIGISTP信号，停止进程

#### 6、Socket

要想跨网络与不同主机通信，就需要Socket通信。

前面提到的管道、消息队列、共享内存、信号量和信号都是在同一台主机上进行进程间通信，那要想**跨网络与不同主机上的进程之间通信，就需要 Socket 通信了。**

实际上，Socket 通信不仅可以跨网络与不同主机的进程间通信，还可以在同主机上进程间通信。

我们来看看创建 socket 的系统调用：

```c
int socket(int domain, int type, int protocal)
```

三个参数分别代表：

- domain 参数用来指定协议族，比如 AF_INET 用于 IPV4、AF_INET6 用于 IPV6、AF_LOCAL/AF_UNIX 用于本机；
- type 参数用来指定通信特性，比如 SOCK_STREAM 表示的是字节流，对应 TCP、SOCK_DGRAM 表示的是数据报，对应 UDP、SOCK_RAW 表示的是原始套接字；
- protocal 参数原本是用来指定通信协议的，但现在基本废弃。因为协议已经通过前面两个参数指定完成，protocol 目前一般写成 0 即可；

根据创建 socket 类型的不同，通信的方式也就不同：

- 实现 TCP 字节流通信： socket 类型是 AF_INET 和 SOCK_STREAM；
- 实现 UDP 数据报通信：socket 类型是 AF_INET 和 SOCK_DGRAM；
- 实现本地进程间通信： 「本地字节流 socket 」类型是 AF_LOCAL 和 SOCK_STREAM，「本地数据报 socket 」类型是 AF_LOCAL 和 SOCK_DGRAM。另外，AF_UNIX 和 AF_LOCAL 是等价的，所以 AF_UNIX 也属于本地 socket；

接下来，简单说一下这三种通信的编程模式。

> 针对 TCP 协议通信的 socket 编程模型

![img](javaNote.assets/12-TCP编程模型.jpg)

- 服务端和客户端初始化 `socket`，得到文件描述符；
- 服务端调用 `bind`，将绑定在 IP 地址和端口;
- 服务端调用 `listen`，进行监听；
- 服务端调用 `accept`，等待客户端连接；
- 客户端调用 `connect`，向服务器端的地址和端口发起连接请求；
- 服务端 `accept` 返回用于传输的 `socket` 的文件描述符；
- 客户端调用 `write` 写入数据；服务端调用 `read` 读取数据；
- 客户端断开连接时，会调用 `close`，那么服务端 `read` 读取数据的时候，就会读取到了 `EOF`，待处理完数据后，服务端调用 `close`，表示连接关闭。

这里需要注意的是，服务端调用 `accept` 时，连接成功了会返回一个已完成连接的 socket，后续用来传输数据。

所以，监听的 socket 和真正用来传送数据的 socket，是「**两个**」 socket，一个叫作**监听 socket**，一个叫作**已完成连接 socket**。

成功连接建立之后，双方开始通过 read 和 write 函数来读写数据，就像往一个文件流里面写东西一样。

> 针对 UDP 协议通信的 socket 编程模型

![img](javaNote.assets/13-UDP编程模型.jpg)

UDP 是没有连接的，所以不需要三次握手，也就不需要像 TCP 调用 listen 和 connect，但是 UDP 的交互仍然需要 IP 地址和端口号，因此也需要 bind。

对于 UDP 来说，不需要要维护连接，那么也就没有所谓的发送方和接收方，甚至都不存在客户端和服务端的概念，只要有一个 socket 多台机器就可以任意通信，因此每一个 UDP 的 socket 都需要 bind。

另外，每次通信时，调用 sendto 和 recvfrom，都要传入目标主机的 IP 地址和端口。

> 针对本地进程间通信的 socket 编程模型

本地 socket 被用于在**同一台主机上进程间通信**的场景：

- 本地 socket 的编程接口和 IPv4 、IPv6 套接字编程接口是一致的，可以支持「字节流」和「数据报」两种协议；
- 本地 socket 的实现效率大大高于 IPv4 和 IPv6 的字节流、数据报 socket 实现；

对于本地字节流 socket，其 socket 类型是 AF_LOCAL 和 SOCK_STREAM。

对于本地数据报 socket，其 socket 类型是 AF_LOCAL 和 SOCK_DGRAM。

本地字节流 socket 和 本地数据报 socket 在 bind 的时候，不像 TCP 和 UDP 要绑定 IP 地址和端口，而是**绑定一个本地文件**，这也就是它们之间的最大区别。

### 同步和互斥

#### 同步

线程在某个点互相等待和唤醒操作，比如线程AB互相协助，A等待B处理完唤醒他

##### 1、哲学家就餐问题

哲学家围着就餐，中间只有一把叉子，但每个则学家需要两把叉子才能就餐

方案一：使用信号量解决，奇数先拿左边再拿右边的叉子，偶数先拿右边再拿左边

![img](javaNote.assets/28-哲学家进餐-方案三示例.jpg)

![方案三可解决问题](javaNote.assets/29-哲学家进餐-方案三-图解.jpg)

方案二：只有左右两边都没有进餐，我才可以进餐

![方案四也可解决问题](javaNote.assets/31-哲学家进餐-方案四-图解.jpg)

比如生**产消费模型**，可使用信号量PV实现同步操作

![img](javaNote.assets/19-互斥信号量同步实现-吃饭例子.jpg)

##### 2、读写问题

「读-读」允许：同一时刻，允许多个读者同时读

「读-写」互斥：没有写者时读者才能读，没有读者时写者才能写

「写-写」互斥：没有其他写者时，写者才能写

读优先锁：读读互斥，读写互斥，当读线程获取锁的时候，另外读线程可以继续获取读锁，可能导致写饥饿

写优先锁：当读获取到锁的时候，写获取锁的时候阻塞，但另外读进程再获取读锁的时候会阻塞

读写公平锁：把所有获取锁的都用队列存起来，按先进先出加锁

方案二：使用一个信号量falg解决,防止读者无线读叠加，避免了读写饥饿问题

![img](javaNote.assets/34-读者写者-方案三示例.jpg)

而这里 `flag` 的作用就是阻止读者的这种特殊权限（特殊权限是只要读者到达，就可以进入读者队列）。

比如：开始来了一些读者读数据，它们全部进入读者队列，此时来了一个写者，执行 `P(falg)` 操作，使得后续到来的读者都阻塞在 `flag` 上，不能进入读者队列，这会使得读者队列逐渐为空，即 `rCount` 减为 0。

这个写者也不能立马开始写（因为此时读者队列不为空），会阻塞在信号量 `wDataMutex` 上，读者队列中的读者全部读取结束后，最后一个读者进程执行 `V(wDataMutex)`，唤醒刚才的写者，写者则继续开始进行写操作

##### 3、过桥问题

问题
独木桥问题1：东西向汽车过独木桥，为了保证安全，只要桥上无车，车过桥，待一方的汽车全部过完后，另一方的汽车才允许过桥。请用信号量和PV操作来写出汽车过独木桥问题的同步算法。

思路
首先对于东西两侧的车辆而言，桥是一个互斥资源，而对东西两侧各自而言，每辆车上桥是同步关系，东西两侧的车辆在抢到这互斥资源后只有最后一辆车通过了独木桥才释放。

```
	semaphore wait,mutex1,mutex2;
	mutex1=1;//东侧车辆的互斥信号量
	mutex2=1;//西侧车辆的互斥信号量
	wait=1;//互斥信号量，表示独木桥的数量
	int count1,count2;
	count1=0;//东侧车辆数
	count2=0;//西侧车辆数
cobegin
	process P 东(){
		P(mutex1);//封锁，防止多个进程同时改变count的值，导致修改被覆盖
		count1++;
		if(count1==1)//第一辆车上桥
			P(wait);
		V(mutex1);
		/*过独木桥*/
		P(mutex1);//与上面count++同理
		count1--;
		if(count1==0)//东侧车辆全部下桥
			V(wait);
		V(mutex1);
	}
	process P 西(){
		P(mutex2);
		count2++;
		if(count2==1)//第一辆车上桥
			P(wait);
		V(mutex2);
		/*过独木桥*/
		P(mutex2);
		count2--;
		if(count2==0)//西侧车辆全部下桥
			V(wait);
		V(mutex2);
	}
coend
```

下面应该是选C

![image-20220912145935598](javaNote.assets/image-20220912145935598.png)

![image-20220912145950896](javaNote.assets/image-20220912145950896.png)

![image-20220912150001115](javaNote.assets/image-20220912150001115.png)

![image-20220912150008816](javaNote.assets/image-20220912150008816.png)

![image-20220912150015511](javaNote.assets/image-20220912150015511.png)

#### 互斥

临界区同一时刻只允许一个线程进行访问

使用加锁或信号量实现

### 中断

1、利用中断功能，处理器**可以在I/O操作的执行过程中执行其它指令**
2、中断处理中，**需要保护被中断进程的所有状态信息**
3、处理多个中断有两种方法：一种方法是正在处理一个中断时，**禁止再发生中断**；另一种方法是**允许高优先级的中断打断低优先级**的中断处理程序的执行
4、如果是因为进程调度引起的中断，那么被中断的进程会被**放入就绪队列里面排队**，所以在中断处理程序执行完成之后被中断的进程**不一定立即获得CPU的控制权**、恢复执行

中断是**多道程序得以实现的基础**

中断的本质：发生中断就意味着需要**操作系统介入**，开展管理工作，CPU要从**用户态转换为核心态**

https://www.jianshu.com/p/4fc0db2b749a

```
异步的时间处理机制，提高CPU并发效率，系统调用的实现方式，比如IO中断

作用：
提高处理器效率，利用中断功能，处理器在IO操作执行过程中执行其它程序，实现并发

分类：
一、IO中断，让CPU执行其它线程，不用干等，提高了CPU的使用效率

二、程序中断（系统调用）：系统调用是通过中断实现，CPU响应中
断，切换内核态进行中断处理程序运行

三、时钟中断

四、硬件失效中断（运算溢出、访问越界、被0除）
```

MMU进程隔离，保护内核

内核：线程调度，文件管理，驱动程序，网络支持

不让用户执行一些特权指令

```
DMA直接内存读取，发一个命令（包含IP设备地址、是否一次读写、字节数）给它就行，处理器继续其它工作。传送完成，DMA发送中断信号给处理器就行了
```

高速缓存：根据局部性原理，把一小部分的指令集合加载到告诉缓存中，匹配CPU的处理速度

![image-20220904214541580](javaNote.assets/image-20220904214541580.png)

### 页面置换算法

LRU(Least Recently Used) 最近最少使用算法

### 补码和原码

```
正数补码是本身
负数补码是各位取反（不包括符号位），末位加一
```

**计算机只有加法**

```
1-1=1原+（-1）原=1（补）+（-1）补=（）补=（）原
```

**为什么byte是-128至127**

```
+0 0000 0000  补码：0000 0000
-0 1000 0000  补码：0000 0000（溢出）
根据补码原则0000 0000表示0，1000 0000却不能表示0（没有-0这种东西），
既然1000 0000谁要表示不了，那就表示-128吧
```

常规文件读将文件页拷贝到也缓存

#### 》》和》》》

```
>>   右移，高位符号位不变
>>>  有符号右移，高位符号位补0
比如负数无符号右移后，符号补0，变成了正数
```

### 大小端

对于大端和小端来说，一字节内部的8位的顺序是一样的

大端：高位存在低地址，低位存在高地址（符合人类习惯）

![在这里插入图片描述](javaNote.assets/20210429171813889.png)

小端：高位存在高地址，低位存在低地址

![在这里插入图片描述](javaNote.assets/20210429172017425.png)

x86是小端模式

### 分布式锁的实现

- 使用数据库的分布式锁
- 使用Redis的setnx和expire
- 基于Zookeeper实现分布式锁

### 电梯调度SCAN

从小到大直到顶再返回

```
根据电梯扫描算法，磁头会一直朝着增加方向走，直到到达磁盘的一端。在到达磁盘的一端后，磁头掉头，再朝着磁盘另一端去扫描。这个过程就跟电梯一样所以叫电梯扫描算法。

```

### 端口访问失败

```
解决：开启安全组，开启防火墙
```

- 查看防火墙所有已开放的端口

  ```bash
  firewall-cmd --list-all
  ```


- 基本使用

  ```bash
  启动与关闭
  systemctl start（stop） firewalld
  查看状态
  systemctl status firewalld
  ```

- 关闭防火墙命令是 

  ```bash
  iptables -P INPUT ACCEPT 
  iptables -P FORWARD ACCEPT 
  iptables -P OUTPUT ACCEPT 
  iptables -F 
  ```


- 给防火墙开启一个端口

  ```bash
  开启端口
  firewall-cmd --zone=public --add-port=3306/tcp --permanent
  重启生效
  firewall-cmd --reload
  ```

- 保存配置

  ```
  service iptables save #保存iptables规则  centOS
  iptables-save > /etc/iptables.up.rules  #保存iptables规则 ubuntu
  ```

- 查看端口号

  ```查看
   iptables -L -n 
  ```

- 查看端口占用情况

  ```
  netstat -ntulp | grep 3306   //查看所有3306端口使用情况
  ```

- centos安装宝塔命令 

  ```bash
  yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh
  ```

- Ubuntu/Deepin安装脚本

  ```bash
  wget -O install.sh http://download.bt.cn/install/install-ubuntu.sh && sudo bash install.sh
  ```

- 切换root用户

  ```bash
  su
  ```


- 查看服务对应的进程

  ```bash
  ps -ef|grep redis
  ```

  

- **lsof命令，用法：lsof -i:端口号，比如redis默认端口号6379，就使用**

  ```bash
  lsof -i:6379
  ```

**windows刷新dns **

```bash
ipconfig /displaydns 
ipconfig /flushdns
```

**hosts目录：C:\Windows\System32\drivers\etc\\hosts**

### 查看IP地址

```
linux：ifconfig
windows：ipconfig # 注意这个是电脑的私有IP，网页看到的才是网关的全球ip
```

### nohup后台运行命令

```bash
# & 表示后台运行
nohup java -jar demo01-0.0.1-SNAPSHOT.jar &
```

### 杀死进程脚本

```
ps -ef|grep XXX|grep -v grep|awk '{printf $2}'|xargs kill -9
或
kill -9 `ps -ef|grep XXX|grep -v grep|awk '{printf $2}'`
```

### 桥连、Nat、仅主机

```
桥接：选择桥接模式的话虚拟机和宿主机在网络上就是平级的关系，相当于连接在同一交换机上。

NAT：NAT模式就是虚拟机要联网得先通过宿主机才能和外面进行通信。

仅主机：虚拟机与宿主机直接连起来
```

### 修改主机名

```
vi /etc/hostname
```

![1564741129-9031-6852280-d07dc33a8be765c2](javaNote.assets/1564741129-9031-6852280-d07dc33a8be765c2.png)

### 虚拟机静态ip设置

[博客](https://blog.csdn.net/qq_36254571/article/details/97146842)

很多人可能在刚开始使用CentOS7的时候，总会发现虚拟机的ip地址随时都会改变。

一、VM平台的配置

1.设置虚拟机的网络连接方式为NAT



2.配置虚拟机的NAT模式具体地址参数

编辑(E)–>虚拟网络编辑器(N)–>更改设置–>选中VMnet8

设置子网IP

由于要设置的地址为192.168.119.121，故在设置子网的时候取前三段，为192.168.119.0

在这里插入图片描述



设置网关

点击NAT设置(S)

在这里插入图片描述



二、 CentOS配置文件配置

首先用 vim /etc/sysconfig/network-scripts/ifcfg-ens33 打开配置文件ifcfg-ens33

修改配置文件中的以下2个属性



再向改配置文件中加入如下代码

![img](javaNote.assets/20190724175548991.png)

IPADDR=192.168.119.121

GATEWAY=192.168.119.2

NETMASK=255.255.255.0

DNS1=8.8.8.8

DNS2=8.8.4.4

IPADDR ：要固定的虚拟机的IP地址，前三位与应主机的ip地址一致

GATEWAY ：之前再VM中设置的网关地址

NETMASK ：广播地址



再向vim etc/resolv.conf中加入

nameserver 8.8.8.8

nameserver 8.8.4.4

nameserver ：定义DNS服务器的IP地址，在此可指定多个DNS服务器，则用户端将会依序提出查询要求。

最后重启网卡

service network restart

检查配置情况

静态IP设置完毕

### 文件系统

为一个文件分配inode节点和目录项

#### 1、inode

磁盘块号（指向数据块）、文件属性（大小，创建时间）

**磁盘**

#### 2、目录项

文件名、目录级联关系

索引节点唯一标识一个文件，所以是目录项和inode是多对一的关系，即多个文件名对于同一个inode文件，这就是硬链接，起到备份的作用

目录也是文件，也是用索引节点唯一标识，和普通文件不同的是，普通文件在磁盘里面保存的是文件数据，而目录文件在磁盘里面保存子目录或文件。

**缓存在内存**

### 文件权限

chmod命令改变文件权限

```
rxw rwx rwx  当前用户 用户组 其它用户
421
文件默认没有x权限；目录默认有x权限
```

![image-20220121214621281](javaNote.assets/image-20220121214621281.png)

```
如果没有x权限，则无法进入对应的目录
```

![image-20220722160834722](javaNote.assets/image-20220722160834722.png)

![image-20220722161433961](javaNote.assets/image-20220722161433961.png)

### 段式存储管理

https://www.cnblogs.com/wkfvawl/p/11733057.html

页式是一维，段式是二维的

页式和段式分配都是动态的，页式分配不是连续的，段式分配段内连续，段之间不连续

段式存储管理更方便共享和安全

![image-20220911104110942](javaNote.assets/image-20220911104110942.png)

#### 1、分段

**进程的地址空间**：按照程序**自身的逻辑**关系**划分为若干个段**，每个段都有一个段名（在低级语言中，程序员使用段名来编程），每段从0开始编址。

**内存分配规则：**以段为单位进行分配，**每个段在内存中占连续空间**，但**各段之间可以不相邻**。

#### 2、段表

每一个程序设置一个段表，放在内存,属于进程的现场信息

![img](javaNote.assets/1358881-20191024161318366-114906606.png)

#### 3、地址变换

逻辑地址是**二维**的，包括**段号+段内地址**

根据段号从**段表**中找到**段基址**

于是**段基址+段内地址**就能定位目标单元

![img](javaNote.assets/1358881-20191024161812951-666406865.png)

![img](javaNote.assets/1358881-20191024161833574-1537867468.png)



#### 4、段的保护

**越界中断处理**
   进程在执行过程中，有时需要扩大分段，如数据段。由于要访问的地址超出原有的段长，所以发越界中断。操作系统处理中断时 ，首先判断该段的“扩充位”，如可扩充，则增加段的长度；否则按出错处理

**缺段中断处理**

检查内存中是否**有足够的空闲**空间
  ①若有，则**装入该段**，修改有关数据结构，中断返回
  ②若没有，检查内存中空闲区的总和是否满足要求，是则应采用**紧缩技术**，转 ① ；否则，淘汰一（些）段，转①

#### 5、段的动态连接

为何要进行段的**动态链接**？
**大型程序由若干程序段，若干数据段组成**
进程的某些程序段在进程运行期间可能根本不用
互斥执行的程序段**没有必要同时驻留内存**
有些程序段执行一次后不再用到
静态链接花费时间，浪费空间

在一个程序运行开始时，只将主程序段装配好并调入主存。其它各段的装配是在主程序段运行过程中逐步进行的。每当需要调用一个新段时，再将这个新段装配好，并与主程序段连接。
**页式存储管理：难以完成动态链接，其逻辑地址是一维的**

#### 6、信息的保护与共享

这里主要与页式存储管理进行一下对比。

**分段比分页更容易实现信息的共享和保护。**

共享：直接指向要共享的段即可；

保护：比如一个页面一部分可访问，一部分不可访问，页表很难进行保护。**段表直接划分为可访问的和不可访问的段区域。**

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024163246922-772131390.png)

 纯代码举例：比如，有一个代码段只是简单的输出“Hello World!”。

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024163539675-1568009948.png)

#### 7、页式系统与段式系统的对比

分页是信息的**物理单位**，实现了离散分配，不易产生内存碎片，是系统行为。

分段是信息的**逻辑单元**，面向用户可见，一段代表一个逻辑模块。



页大小是**固定**的，分页是**一维**的，只需一个记忆符即可表示一个地址

段大小**不固定**，分段是**二维**的，需要段号和段内地址



**分段更容易实现信息的共享和保护**，比如一些纯代码可以共享，直接指向该段即可。同理，可分为可访问和不可访问段



分页**访存要两次**，第一次查页表，第二次访问目标单元。

分段**访存要两次**，第一次查段表，第二次访问目标单元。

两者都可以引入**快表**（直接保存实际的），那么都只需一次访存。

快表：是页表的缓存，缓存了虚拟地址到物理地址的映射

页表：页到物理地址的映射



![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024164516533-869573781.png)

补充：

分段存储：段内地址W字段溢出将产生越界中断。

分页存储：段内地址W字段溢出会自动加入到页号中。

#### 8、总结

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024163733207-1074596879.png)

### 段页式存储管理

第一次查段表，第二次查对应的页表，第三次查目标单元

#### 1、分页、分段的有缺点分析

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024164819264-302516041.png)

#### 2、基本思想

用户程序划分：按段式划分（对用户来讲，按段的逻辑关系进行划分；对系统讲，按页划分每一段）

逻辑地址：

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024164940232-1333874973.png)

 **内存划分：按页式存储管理方案**
 **内存分配：以页为单位进行分配**

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024165048537-307146941.png)

#### 3、逻辑地址结构

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024165237632-1280186867.png)

#### 4、段表页表

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024165517051-1418927958.png)

#### 5、地址转换

![img](https://img2018.cnblogs.com/blog/1358881/201910/1358881-20191024165601134-342443140.png)

#### 6、评价

**优点：**
保留了分段和请求分页存储管理的全部优点
提供了虚存空间，能更有效利用主存

**缺点：**
增加了硬件成本
系统复杂度较大

#### 7、总结

![img](javaNote.assets/1358881-20191024165652774-1987561570.png)

### 逻辑地址

![img](javaNote.assets/bc0aaaf379fc4bc8882efd94b9052b64.png)

逻辑地址，程序所使用的地址CPU分配给程序看到的内存单元，

**相对块号**。需要MMU从虚拟地址映射到物理地址中。

### 虚拟地址

逻辑地址通过段式内存管理映射的地址称为虚拟地址（线性地址）

### 物理地址

虚拟地址经过页式内存管理转换为物理地址

CPU外部地址总线上的寻址物理内存的地址，是地址变换的最终结果地址，实际磁盘或物理内存的地址



Linux操作系统本身的代码和应用程序面对都是虚拟地址，屏蔽了CPU逻辑地址的概念，段只被用于访问控制和内存保护

### 虚拟内存

虚拟内存：计算机所呈现的比实际内存大得多的容量。比如北京到上海只需3公里的铁轨，只要你操作得足够快，把后面的铁轨铺到火车前面。

这就是虚拟内存管理要完成的任务，为每个程序分配了64MB的虚拟内存空间，因此逻辑地址范围为0x0000000到0x4000000

#### **为什么要有虚拟内存**

- 进程要4G空间，但实际不会用到那么多

- **地址空间隔离。**用户直接访问物理内存，不安全，可能恶意破坏别的内存数据。

- **内存利用率低。**由于内存有限，一个程序空间不够，就要先释放部分空间才能运行，这样数据装入装出效率低下。另外，虚拟内存是连续的，不代表物理内存是连续的，意味着可以使用内存碎片

- **程序运行地址不确定。**因为内存随机分配，所以程序运行地址不确定。

- **屏蔽内存细节**，降低使用门槛。不同厂商内存结构不一致，直接使用比较复杂。

#### 分页

**局部性原理**，每次使用的数据都是相邻的，所以有了**分页**的概念，每次以页（4k）单位读取数据。

当程序执行到x页时，当发现空页面时，就发送了页错误（Page Fault）,操作系统就分配一个物理页面，再将物理页面和虚拟内存的虚拟页映射起来，然后把控制权交给进程。

#### TLB（Translation Lookaside Buffer）:页表缓存

本质是一块高速缓存，缓存虚拟地址和物理地址，如果虚拟地址有对应的物理地址，就叫命中，所以提高命中率可大大提高性能

### SWAP分区

linux叫swap分区，当物理内存不够的时候，先把一部分内存放到swap分区中，待内存空闲再继续执行，也叫交换分区。一般得自己创建swap分区。

window叫做虚拟内存，内存没有用完也会去使用，一般放在c盘

![image-20220406150155056](javaNote.assets/image-20220406150155056.png)

```
swap是什么
内存不足的时候，采用硬盘来虚拟出内存

添加swap
#dd if=/dev/zero of=/tmp/swapfile bs=1M count=4096
 	dd 用来建立空文件
	if=fileName 输入文件（源文件），/dev/zero是会一值输出0的文件
	of 输出文件
	bs 块的大小为多少字节
	count 指定多少块
	创建swap文件，大小1G，文件越大，创建时间越长，文件路径可自定义（/tmp/swap）

查看创建的swap文件大小
#du -h /tmp/swapfile

创建swap
#mkswap /tmp/swapfile # 格式化为内存交换分区格式
#swapon /tmp/swapfile # 将swap设备启动
此时使用命令 free -m就能发现有交换分区了，但是系统重启之后，swap分区又回变为0,因此需要编辑下面的文件

(出现swapon: /tmp/swapfile: insecure permissions 0644, 0600 suggested.)
#vi /etc/fstab 
/tmp/swap swap swap default 0 0
在文件末尾（最后一行）加上

#vi /etc/sysctl.conf 
vm.swappiness=15 表示15的时候使用虚拟内存

查看所有交换分区
#swapon -s

删除swap
#swapoff /tmp/swap
停止swap分区

#rm -rf /tmp/swap
删除swap分区文件

#vi /etc/fstab
去掉上面的那行
```

## Linux命令

### dmesg

display message：用于显示开机信息。（开机信息亦保存在 /var/log 目录中，名称为 dmesg 的文件里。）

###swapon -s

查看所有交换分区

### hdparm

显示与设定**硬盘的参数**，可检测，显示与设定IDE或SCSI硬盘的参数。

查看硬盘型号和硬盘序列号

```
hdparm -i /dev/sda
```

显示硬盘的相关设置：

```
# hdparm /dev/sda
 /dev/sda:
 IO_support = 0 (default 16-bit)
 readonly = 0 (off)
 readahead = 256 (on)
 geometry = 19929［柱面数］/255［磁头数］/63［扇区数］, sectors = 320173056［总扇区数］, start = 0［起始扇区数］
```

显示硬盘的柱面、磁头、扇区数

```
# hdparm -g /dev/sda
 /dev/sda:
 geometry = 19929［柱面数］/255［磁头数］/63［扇区数］, sectors = 320173056［总扇区数］, start = 0［起始扇区数］
```

评估硬盘的读取效率

```
 hdparm -t /dev/sda
 /dev/sda:
 Timing buffered disk reads: 166 MB in 3.03 seconds = 54.85 MB/sec
 [root@linuxso.com ~]# hdparm -t /dev/sda
 /dev/sda:
 Timing buffered disk reads: 160 MB in 3.01 seconds = 53.11 MB/sec
 [root@linuxso.com ~]# hdparm -t /dev/sda
 /dev/sda:
 Timing buffered disk reads: 166 MB in 3.00 seconds = 55.31 MB/sec
```

### fdisk

fdisk -l 查看所有分区

### ls

ls -al

-a 显示所有文件及目录

-l 除文件名称外，亦将文件型态、权限、拥有者、文件大小等资讯详细列出

![image-20220918111157325](javaNote.assets/image-20220918111157325.png)



从上面可以看到，每一行都有7列，分别是：

1. **第一列**共10位，第1位表示文档类型，`d`表示目录，`-`表示文件，`l`表示链接文件，`d`表示可随机存取的设备，如U盘等，`c`表示一次性读取设备，如鼠标、键盘等。后9位，依次对应三种身份所拥有的权限，身份顺序为：owner、group、others，权限顺序为：readable、writable、excutable。如：`-r-xr-x---`的含义为**当前文档是一个文件，拥有者可读、可执行，同一个群组下的用户，可读、可执行，其他人没有任何权限**。
2. **第二列**表示链接数，表示有多少个文件链接到inode号码。(硬链接才会增加，软链接是新增inode结点，只是数据文件执行同一个)
3. **第三列**表示拥有者
4. **第四列**表示所属群组
5. **第五列**表示文档容量大小，单位字节
6. **第六列**表示文档最后修改时间，注意不是文档的创建时间哦
7. **第七列**表示文档名称。以点(.)开头的是隐藏文档

### shell头

![image-20220903170611120](javaNote.assets/image-20220903170611120.png)

### 信号

**ctrl-c**：发送 SIGINT 信号**强行中断**当前程序
**ctrl-z**：发送SIGTSTP**转到后台挂起**

ctrl-\：发送 SIGQUIT 信号**退出**



**ctrl-d**：不是发送信号，而是表示一个特殊的二进制值，表示 EOF，**注销当前用户**，等价于**exit**和**logout**；



ctrl-s：**中断控制台输出**；
**ctrl-q**：恢复控制台输出；
**ctrl-l**：清屏

![image-20220903165721220](javaNote.assets/image-20220903165721220.png)

### 虚拟机克隆

```
接下来修改一下ip，以防网络冲突；
cd /etc/sysconfig/network-scripts/
vi ifcfg-ens33
service network restart 
```

### 用户

```
useradd ssh02
passwd ssh02
chown -R ssh02 /home/tomcat-9.0/logs

1.想创建的用户目录
mkdir /home
2.新建用户到指定的目录
useradd ssh02 -d /home/test
3.设置新用户密码
passwd ssh02
4. 将访问目录权限全部赋予用户
chown ssh02 /home
5.将上层目录设置为root所有
chown root /home/
6.赋予权限给上层目录
chmod 771 /home

su - user #切换用户
su -  # 切换管理员

useradd -d /home/hf hf
passwd hf #修改密码
userdel hf

# 查看所有用户（组）
cat /etc/passwd
cat /etc/group

sudo 采用管理员身份执行
-u username # 不加此参数代表以管理员身份运行，否则以username身份运行 

# 新增组
groupadd group-hf

# 查看用户所属组
groups username

# 添加用户到某个组
usermod -G group-hf hf
```

### unmask

$umask 0000 #临时修改

$vi /etc/profile #永久生效

$ umask 查看自己当前unmask情况文件权限

- 文件默认权限默认最大为`666`
- 目录默认权限默认最大为`777`
- 建立目录之后的权限为`777`减去`umask`的值。`777 - 022 = 755`

```
ipconfig	检测和设置本机的网络接口 ipconfig/all：显示当前TCP/IP网络中的所有配置信息
route	控制网络路由表。
traceroute	侦测主机到目的主机之前所经过的路由的命令
telnet	远程登陆服务的标准协议和主要方式，常用的远程控制Web服务器的方法。
ping	检查网络是否连通，可以很好地帮助我们分析和判定网络故障。
netstat	查看进程监听端口的情况
iptables	根据IP制定策略，也可以根据端口制定策略
```

### cron

```
五项
分钟(0-59) 小时(0-23) 月份第几天(1-31) 月份(1-12) 星期第几天(0-6)
```

### vim

https://blog.csdn.net/sunjinshengli/article/details/108558752

```
ctrl+a 光标移到最前面
ctrl_e 光标移到最后面

ctrl+u 光标处快速往前删除
ctrl+k 光标处快速往后删除

yy 	复制游标所在行整行
p    粘贴至游标后（下） 
dd    剪切游标所在行整行 
```

### alias

alias copy='cp'

alias [别名]=[指令名称]   设置别名

```
临时设置：
alias [别名]=[指令名称]   设置别名
# alias grep='grep --color=auto'			//只针对当前终端和当前用户生效

永久设置：
1）全局（针对所有用户生效）
vim /etc/bashrc
alias grep='grep --color=auto'
source /etc/bashrc

2）局部（针对具体的某个用户）
vim ~/.bashrc
alias grep='grep --color=auto'
source ~/.bashrc
```

### cp

```
cp
-r 目录递归复制
-i 交互的形式，重写会提示
-l 硬链接
-s 符号链接

如果dir2目录不存在，则可以直接使用
cp -r dir1 dir2

如果dir2目录已存在，则需要使用
cp -r dir1/. dir2
```

### ps命令

**ps -aux**

查看进程详细信息，包括用户，进程号，cpu，内存

```
[root@k8s-node1 shell_test]# ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.1  0.0  45048  3780 ?        Ss   Apr06  24:57 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
```

![image-20220420162820846](javaNote.assets/image-20220420162820846.png)

**ps -ef**

显示所有运行中的进程

![image-20220420162803302](javaNote.assets/image-20220420162803302.png)

字段含义如下：

```
ps   将某个进程显示出来
-A，-a 　显示所有程序。 
-f 　显示UID,PPIP,C与STIME栏位。 
grep命令是查找

中间的|是管道命令 将左侧的标准输入作为右侧的标准输入

UID PID PPID C STIME TTY TIME CMD
各相关信息的意义：
UID 程序被该 UID 所拥有
PID 就是这个程序的 ID 
PPID 则是其上级父程序的ID
C CPU 使用的资源百分比
STIME 系统启动时间
TTY 登入者的终端机位置
TIME 使用掉的 CPU 时间。
CMD 所下达的指令为何
```

### tar命令

```
tar -cf 打包
tar -zxf 对.gz解包 

-f 使用文件
-c create打包
-x extract解压缩
-z gzip
-v 显示处理的文件
-C dir 改变解压后存储的路径
```

### rpm

用法

```
rpm -i 需要安装的包文件名

举例如下：

rpm -i example.rpm 安装 example.rpm 包；

rpm -iv example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息；

rpm -ivh example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息及安装进度；
```

查看安装路径

```
rpm -ql softName
```

查看已安装软件

```
[root@jacky zookeeper]# rpm -qa | grep jdk

java-1.6.0-openjdk-1.6.0.0-1.66.1.13.0.el6.i686
java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.i686
```

卸载已安装软件

```
rpm -e --nodeps 要卸载的软件包

root@jacky zookeeper]# rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.66.1.13.0.el6.i686
```

### which locate find

which和locate基于**内建数据库**，效率高

find **磁盘**查找,指定目录查找文件

whereis 只能用于**程序名**的搜索，而且只搜索**二进制**文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s）

```
删除10天前的日志文件
find ./* -type f -mtime +10 -exec rm  {}  \;
```

### 软硬连接

```
硬链接：多了一个文件名对inode结点的链接
软连接：是新的文件，拥有独立的inode结点。指向同一个数据块。保存了文件的绝对路径。

软连接可对不存在的目录或文件建立连接，软连接链接计数i_link不会增加
```

软连接：有自己的inodes(索引结点),类似**快捷方式**，可跨文件系统，本质是用新inode链接名字，名字在链接到同一个文件

硬连接：指向同一个inodes，移动或删除原文件不会被破坏（相当于一个**备份**，同一文件以不同文件名的形式存在），不同文件名指向**同一个inode结点**，当然数据也是一样的。（**会增加链接数**）

可以看到软硬连接的inode都是393823，除了名字所有信息都是一样的。因为是同一个inodes本来就是同一个文件系统，所以**不能跨文件系统**，**不能链接目录**

![image-20220714220540108](javaNote.assets/image-20220714220540108.png)

```
ln -s 创建软连接
ln 硬连接
cp -s sourceFile s_link_sf 软连接
cp -l sourceFile h_link_sf 硬连接
```

### LVM

```
磁盘sda分为两个分区sda1和sda2
分区sda2是lvm
```

![image-20220828165255063](javaNote.assets/image-20220828165255063.png)

http://blog.chinaunix.net/uid-23511971-id-320264.html

一、LVM（Logical [Volume](https://so.csdn.net/so/search?q=Volume&spm=1001.2101.3001.7020) Manager逻辑卷管理）的概念：
  LVM是Linux系统对磁盘分区进行管理的一种方式，使用它可以让你更为灵活的管理你的磁盘。在了解LVM的概念之前我们应该先了解PV（physical volume,物理卷）、VG（volume group,卷组）和LV（logical volume,逻辑卷）。因为LVM就是由这三种元素组成的。下面我们来了解一下它们各自的概念：
\1. PV（physical volume,物理卷）：
  PV是VG的组成部分，它是由分区构成的，通常我们在有多块硬盘的环境中把一块硬盘格式化成一个主分区后，然后把这块硬盘做成PV，在只有一块硬盘的情况下我们就是把这块硬盘上的某一个分区做成PV。比如，公司里的服务器可能有多块硬盘，这个时候你可以把一块硬盘划一个主分区，然后再把它做成PV，但是就像这次我重做系统时候机子上就一块硬盘，我还得考虑引导分区和“/”根分区，所以我就把硬盘划了四个主分区，一个“/boot”分区、一个“/”分区，还有一个“swap”分区，最后当然就把剩下的分了一个主分区，把系统装好后我把最后一个主分区做成了一个PV，然后加入到VG里，又从VG里划分的LV，也就组成了LVM。
\2. VG（volume group,卷组）：
  VG就是卷组，它是由若干个PV组成的。也就是我们把上面那些硬盘分区，然后做成的PV。它就是由那些PV组成的。它的作用就是把PV集中到一块再进行划分。
\3. LV（logical volume,逻辑卷）：
  LV就是从VG里划分出来的卷，它可以在你所用的卷不够用的情况下增加其容量。它其实就像是Windows里的逻辑磁盘，不过Windows里的逻辑磁盘不能随心所欲的增加或减少磁盘的容量，而LV就可以。

### 目录结构

**/proc** 是虚拟文件系统，是系统内存的映射

### 磁盘分区

#### df -Th

查看磁盘**使用情况和挂载情况**。

```
-T 文件系统类型
```

![image-20220827221403889](javaNote.assets/image-20220827221403889.png)

#### fdisk -l 

**查看所有磁盘分区**（包括未格式化和未分区的）

![image-20220827221320867](javaNote.assets/image-20220827221320867.png)

#### lsblk 

查看**磁盘分区结构**

![image-20220827221301264](javaNote.assets/image-20220827221301264.png)

#### du  -sh /mydata/* 

查看具体**某个目录的占用空间**

```
-s 表示总的
```

![image-20220803215909810](javaNote.assets/image-20220803215909810.png)

#### LVM扩容

扩容成功链接：

镜像的所以不能直接在原来的扩容，得在新加磁盘然后加入vg中

https://www.cnblogs.com/hydd/p/12672797.html

```
fdisk /dev/sdb # 新建主分区
pvcreate /dev/sdb # 把新增磁盘分区设为物理卷pv
vgs # 查看已有的虚拟组vg
vgextend centos /dev/sdb # 将上面物理卷pv加到vg中
lventend -L +7G /dev/mapper/centos-root # 扩容逻辑卷lv
xfs_grows /dev/mapper/centos-root # xfs类型让系统读取，ext4用resize2fs命令
```

https://zhuanlan.zhihu.com/p/416624687

https://www.cnblogs.com/kevingrace/p/5825963.html

https://blog.csdn.net/lkforce/article/details/80917306

#### 格式与挂载

磁盘格式化（变成指定的文件系统）后才能进行挂载，挂载到某个目录，这个目录称为挂载点，挂载点是访问文件系统的入口。

一个目录最多只能挂载一个磁盘

```
mkfs.ext4 /dev/xvdc1
或# mkfs -t xfs /dev/xvdc1

mount /dev/xvdb1 /xfs #单独挂载到某个目录

umount /dev/xvdc1 #卸载某个分区
```

添加分区开机自动挂载
说明：/xfstest表示挂载位置，使用mount挂载后重启系统后会失效，需要添加开机自动挂载。

```
#echo '/dev/xvdb1 /xfstest xfs defaults 0 0' >> /etc/fstab
或者编辑/etc/fstab，在下面增加/dev/xvdb1 /xfstest xfs defaults 0 0

# mount -a		#挂载所有新分区

# cat /etc/fstab#查看写入分区信息
```

### vmstate

查看cpu内存负载

![image-20220719095112461](javaNote.assets/image-20220719095112461.png)

### top命令

查看操作系统信息，包括CPU和内存

![image-20220611124327971](javaNote.assets/image-20220611124327971.png)

### lsof

根据端口port查看进程

```
lsof -i:port
```

### netstat命令

netstat -anp # 查看网络连接状态

-a或all 显示所有连接中的socket
-n或numeric 直接使用IP地址，而不通过域名服务器
-p或programs 显示程序名称
-t或tcp 显示TCP传输协议的连线情况

#### 查看端口号被哪个进程占领

netstat -nap | grep 8080

### ifconfig命令

查看和配置网络接口

### free命令

查看内存

```
free -h(humanic)
```

### systemctl

```
systemctl status serviceName 查看服务的详细信息
```

### tail -f 

```
实时查看日志
```

-f 循环读取

-n<行数> 显示文件的尾部 n 行内容

### 系统服务

```
/usr/lib/systemd/system/docker.service
```

### awk

awk用来**提取列的主要工具**；

echo "aa bb cc" | awk -F '{print $1}' 

 输出aa，一行一行的读取指定的文件， 以空格作为分隔符，打印第一个字段



awk '{print $2}' $fileName :

一行一行的读取指定的文件， 以空格作为分隔符，打印第二个字段

### 统计IP次数最多的

netstat -ntu | tail -n +3|**awk** '{ print $5}' | **cut** -d : -f 1 | sort | uniq -c| **sort** -n -r | head -n 5
8 127.0.0.1
2 192.168.47.27




tail -n +3 :去掉上面用红色标明的两行。

awk '{ print $5}'：取数据的低5域（第5列），上面蓝色标明。

cut -d : -f 1 ：取蓝色部分前面的IP部分。

sort：对IP部分进行排序。

uniq -c：打印每一重复行出现的次数。（并去掉重复行）

sort -n -r：按照重复行出现的次序倒序排列。

head -n 5：取排在前5位的IP 

```
$ netstat -ntu
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 127.0.0.1:8152 127.0.0.1:4193 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4192 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4196 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4199 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4201 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4204 TIME_WAIT
tcp 0 0 127.0.0.1:8152 127.0.0.1:4207 TIME_WAIT
```

### 关机命令

重启：shutdown -r 、reboot、init 6 

关机：shutdown -h 、 halt、init 0

#### 一、Linux 的五个关机重启命令

　　1、shutdown

　　2、poweroff

　　3、init

　　4、reboot

　　5、halt

#### 二、具体说明

　　在linux下一些常用的关机/重启命令有shutdown、halt、reboot、及init，它们都可以达到重启系统的目的，但每个命令的内部工作过程是不同的。

##### 　　1. shutdown

　　shutdown命令安全地将系统关机。 有些用户会使用直接断掉电源的方式来关闭linux，这是十分危险的。因为linux与windows不同，其后台运行着许多进程，所以强制关机可能会导致进程的数据丢失﹐使系统处于不稳定的状态﹐甚至在有的系统中会损坏硬件设备。而在系统关机前使用shutdown命令﹐系统管理员会通知所有登录的用户系统将要关闭。并且login指令会被冻结﹐即新的用户不能再登录。直接关机或者延迟一定的时间才关机都是可能的﹐还可能重启。这是由所有进程〔process〕都会收到系统所送达的信号〔signal〕决定的。这让像vi之类的程序有时间储存目前正在编辑的文档﹐而像处理邮件〔mail〕和新闻〔news〕的程序则可以正常地离开等等。

　　shutdown执行它的工作是送信号〔signal〕给init程序﹐要求它改变runlevel。

　　Runlevel 0被用来停机〔halt〕﹐runlevel 6是用来重新激活〔reboot〕系统﹐而runlevel 1则是被用来让系统进入管理工作可以进行的状态﹔这是预设的﹐假定没有-h也没有-r参数给shutdown。要想了解在停机〔halt〕或者重新开机〔reboot〕过程中做了哪些动作﹐你可以在这个文件/etc/inittab里看到这些runlevels相关的资料。

```
shutdown 参数说明:

　　[-t] 在改变到其它runlevel之前﹐告诉init多久以后关机。

　　[-r] 重启计算器。

　　[-k] 并不真正关机﹐只是送警告信号给每位登录者〔login〕。

　　[-h] 关机后关闭电源〔halt〕。

　　[-c] cancel current process取消目前正在执行的关机程序。所以这个选项当然没有时间参数﹐但是可以输入一个用来解释的讯息﹐而这信息将会送到每位使用者。

　　[-f] 在重启计算器〔reboot〕时忽略fsck。

　　[-F] 在重启计算器〔reboot〕时强迫fsck。

　　[-time] 设定关机〔shutdown〕前的时间。

```

##### 　　2.halt----最简单的关机命令

　　其实halt就是调用shutdown -h。halt执行时﹐杀死应用进程﹐执行sync系统调用﹐文件系统写操作完成后就会停止内核。

　　参数说明:

　　[-n] 防止sync系统调用﹐它用在用fsck修补根分区之后﹐以阻止内核用老版本的超级块〔superblock〕覆盖修补过的超级块。

　　[-w] 并不是真正的重启或关机﹐只是写wtmp〔/var/log/wtmp〕纪录。

　　[-d] 不写wtmp纪录〔已包含在选项[-n]中〕。

　　[-f] 没有调用shutdown而强制关机或重启。

　　[-i] 关机〔或重启〕前﹐关掉所有的网络接口。

　　[-p] 该选项为缺省选项。就是关机时调用poweroff。

##### 　　3.reboot

　　reboot的工作过程差不多跟halt一样﹐不过它是引发主机重启﹐而halt是关机。它 的参数与halt相差不多。

##### 　　4.init

```
语法：init(选项)(参数)

-b：不执行相关脚本而直接进入单用户模式；
-s：切换到单用户模式。

0 停机（千万不能把initdefault 设置为0）
1 单用户模式
2 多用户，没有 NFS(和级别3相似，会停止部分服务)
3 完全多用户模式
4 没有用到
5 x11(Xwindow)
6 重新启动（千万不要把initdefault 设置为6）

```

### 后台运行命令

```
   1. command & ： 后台运行，你关掉终端会停止运行
   2. nohup command & ： 后台运行，你关掉终端也会继续运行
```

### 批量杀进程

```
kill -9 `ps -ef | grep redis | awk '{print $2}'`

-9（SIGKILL）
ctrl+C 终止进程 SIGINT
ctrl+Z 暂停线程 SIGSTP
```

### grep

全局正则表达式搜索

```
grep -w 单词精确匹配
```

### 标准输入输出

```
0 标准输入
1 标准输出
2 标准错误输出

&>a.txt 表示将标准输出和标准错误输出重定向到文件a.txt中

2>&1  意思就很明了了，就是讲执行linux命令时的错误信息也输出到屏幕上。

/dev/null 黑洞文件，表示删除
2>/dev/null 表示将标准错误输出不显示

>/proc/self/fd/0       //表示标准输入，即键盘输入

/dev/stdout    ----->/proc/self/fd/1　　　 　//表示标准输出，即显示屏，屏幕

/dev/stderr     ----> /proc/self/fd/2      //表示标准错误输出，有些脚本运行时会报错，就会输入到这。
```

### 管道与xargs

```
管道：标准输出转为标准输入
xrgs：标准输出转为命令行输入
```

```
cat /etc/passwd | grep root  等于  grep root /etc/passwd
管道命令（|）。管道命令的作用，是将左侧命令（cat /etc/passwd）的标准输出转换为标准输入，提供给右侧命令（grep root）作为参数。
```

但是，大多数命令都不接受标准输入作为参数，只能直接在命令行输入参数，这导致无法用管道命令传递参数。

```
$ echo "hello world" | echo
```

上面的代码不会有输出。因为管道右侧的`echo`不接受管道传来的标准输入作为参数。

#### `xargs`命令的作用，是将标准输入转为命令行参数。

```
$ echo "hello world" | xargs echo
hello world
```

### shell默认变量($0、$1..)

$@

![image-20220916221925325](javaNote.assets/image-20220916221925325.png)

```

$#：脚本参数个数
$0：脚本文件名

$@：$1 $2 $3(推荐)
$*："$1" "$2" "$3"
	
$?：显示上一条命令的返回码，如果为0则代表执行成功。	

$$：脚本当前进程ID号
$!：后台运行的最后一个进程号

结合if-else语句实现判断上一个命令是否执行成功。
-eq
等于
-ne	不等于
-gt
大于
-lt	小于
ge	大于等于
le	小于等于
```

## MySQL

### 数据源

原生态：JDBC
封装：dbcp,c3p0,druid

#### 一、hirake连接池

spring默认使用，比druid快

#### 二、druid连接池

对SQL语句进行监控、拦截，可视化界面

```
DataSource ds = DruidDataSourceFactory.createDataSource(pro);
```

#### 三、C3P0连接池

1. 导入 `c3p0-0.9.5.5.jar`和`mchange-commons-java-0.2.19.jar`两个包
2. 定义配置文件，将`c3p0-config.xml`文件放在src目录下
3. 创建数据库连接池对象`ComboPooledDataSource`

mybaties默认使用pooled数据库连接池，可选的有unpool和jndi

### 为什么推荐使用自增主键

  InnoDB中，表中的数据是直接存储在**主键聚簇索引**的叶子节点上的，每插入一条记录，其实都是**增加一个叶子结点**，如果主键是顺序的，只需要把新增的一条记录存储在上一条记录的后面。当页达到最大填充因子的时候，下一条记录就会写入新的页中，这种情况下，主键页就会近似于被顺序的记录填满。
  若表的主键不是顺序的id，而是无规律数据，比如字符串，InnoDB无法简单的把一行记录插入到索引的最后，而是**需要找一个合适的位置（已有数据的中间位置），甚至产生大量的页分裂并且移动大量数据**；在寻找合适位置进行插入时，目标页可能不在内存中，这就导致了**大量的随机IO操作**，影响插入效率；除此之外，大量的页分裂会导致大量的**内存碎片**。

### 数据库约束

非空约束（not null）

唯一约束（unique）

主键约束（primary key）

外键约束（foreign key）、

检查约束（check）<Oracle 数据库有 check 约束>

### 存储过程

存储过程**可以返回多个变量**，也可以没有返回值
存储过程可封装并隐藏复杂的商业逻辑，可以包括程序流、逻辑以及对数据库的查询，
存储过程主要是在服务器上执行，减少对客户机的压力

存储过程可以在三种环境下被调用：

1. command命令下，基本语法为：**exec** sp_name [参数名]；
2. SQL环境下，基本语法为：**call** sp_name [参数名]；
3. PL/SQL环境下，基本语法为：**begin** sp_name [参数名] end；

### count(*)和count(1)

#### 不同存储引擎的性能不一样

我们不知道，Mysql常见的存储引擎有两种，MyISAM和Innodb，

在这两种存储引擎下，MySQL对于使用count(*)返回结果的流程是不一样的。

- 在MyISAM引擎中，每张表的**总行数是存储在磁盘上**，所以当执行count(*)时，是直接从磁盘**O(1)**拿到这个值返回，能够快速返回。但要是在后面加了where查询条件时，统计总数也不是像想象中那么快了。
- 在Innodb引擎中，执行count(*)，需要**将数据一行一行地读，再统计总数。**



看到这里，不知道你有没有这样的疑问：

> 为什么Innodb引擎不像MyISAM引擎一样把表总记录存储起来呢？



这个问题问得好，回答这个问题前，我们先了解下MVCC，

#### **什么是MVCC**

全称：Multi-Version Concurrency Control 即多版本并发控制，MVCC 是一种并发控制的方法，一般在数据库管理系统中，实现对数据库的并发访问；在编程语言中实现事务内存。



MVCC 在 MySQL InnoDB 中的实现主要是为了提高数据库并发性能，用更好的方式去处理读-写冲突，做到即使有读写冲突时，也能做到不加锁，非阻塞并发读。

就是因为要实现多版本并发控制，所以才导致Innodb不能直接存储表总记录数。

因为每个事务获取到的一致性视图都是不一样的，所以返回的数据总记录也是不一致的。

举个例子说明下：

假如有一张用户表tb_user, 有三处正在查询用户的总数。

```
select count(*) from tb_user
```

![img](https://pic.rmb.bdstatic.com/bjh/news/327fc3cc24ab04d96159934ce31e0b79.jpeg?x-bce-process=image/watermark,bucket_baidu-rmb-video-cover-1,image_YmpoL25ld3MvNjUzZjZkMjRlMDJiNjdjZWU1NzEzODg0MDNhYTQ0YzQucG5n,type_RlpMYW5UaW5nSGVpU01HQg==,w_19,text_QOa0queUn-m5jw==,size_19,x_15,y_15,interval_2,color_FFFFFF,effect_softoutline,shc_000000,blr_2,align_1)





这时候每次查到的用户数总数可能不太一样。

这是因为每个用户**会根据read view存储的数据来判断哪些数据是自己可见的，哪些是不可见**的。

#### read view

当执行SQL语句查询时会产生一致性视图，即read-view，它是由查询的那一刻所有未提交事务ID组成的数组，和已经创建的最大事务ID组成的。



在这个数组中最小的事务ID被称之为min_id，

最大事务ID被称之为max_id，

而查询的数据结果就是根据read-view做对比从而得到快照。



于是就产生了以下的对比规则，这个规则就是使用当前的记录的trx_id跟read-view进行对比，规则如下：



- 如果落在trx_id<min_id，表示该版本是已经提交的事务生成的，由于事务已经提交所以数据是可见的
- 如果落在trx_id>max_id，表示该版本是由将来启动的事务生成的，是不可见的
- 如果落在trx_id 在min_id 和max_id 中间（min_id<=trx_id<=max_id）时

要是row的trx_id在数组中，表示该版本是由还没提交的事务生成的，不可见，但是当前自己的事务是可见的；

要是row的trx_id不在数组中，表明是提交的事务生成了该版本，是可见的。



读到这，相信你已经知道Innodb引擎为什么不像MyISAM引擎一样把表总记录存储起来了吧。因为 InnoDB 支持事务，MyISAM不支持事务。



在执行count(*)操作的时候还是做了优化的。

#### mysql对count(*)做了优化

自动找到最小的那一颗树进行比较。

InnoDB是索引组织表，主键索引树的叶子节点是数据，而普通索引树的叶子节点是主键值。所以，**普通索引树比主键索引树小很多**。对于count(*)这样的操作，遍历哪个索引树得到的结果逻辑上都是一样的。因此，MySQL优化器**会找到最小的那棵树来遍历**。



如果你使用过show table status 命令的话，就会发现这个命令的输出结果里面也有一个rows值用于显示这个表当前有多少行。



那么是不是这个rows值就能代替count(*)了吗？

其实不能，rows这个是从从采样估算得来的，因此它也是不是准确。不准确到什么程度，官方文档说是在40%到50%。所以show table status命令显示的行数rows是不能直接使用。



基于MySQL的Innodb存储引擎，统计表的总记录数下面这4种做法，哪种效率最高？

实践案例，准备了一张有 500W多条数据的表，表结构如下：



```
CREATE TABLE `tb_user` (`id` int(11) unsigned NOT NULL AUTO_INCREMENT,`user_id` int(11) DEFAULT NULL ,`user_name` varchar(100) DEFAULT NULL ,PRIMARY KEY (`id`) USING BTREE,UNIQUE KEY `userId` (`user_id`) USING BTREE) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4
```

可以看到，这张表有一个主键索引，用不同方式来查询该表用户记录总数

- count(主键id)

用select count(*) from tb_user 耗时0.739s

InnoDB引擎会遍历整张表，**把每一行的id值都取出来**，返回给server层。server层拿到id后，判断是不可能为空的，就按行累加。

- count(1)

用select count(1) from tb_user 耗时0.753s

同样遍历整张表，但**不取值**，server层对返回的每一行，放一个数字1进去，判断是不可能为空的，按行累加。

- count(字段)

用select count(user_name) from tb_user 耗时1.436s

分为两种情况，字段定义为not null和null

1. 为not null时：逐行从记录里面读出这个字段，判断不能为null，累加
2. 为 null时：执行时，判断到有可能是null，**还要把值取出来再判断一下，不是null才累加**



- count(*)



用select count(*) from tb_user 耗时0.739s

需要注意的是，并不是带了*就把所有值取出来，而是mysql做了专门的优化，count(*)肯定不是null，按行累加。

从上面的执行结果，得知count(字段)<count(主键id)<count(1)≈count(*)

#### 总结

基于MySQL的Innodb存储引擎，统计表的总记录数按照效率排序的话count(字段)<count(主键id)<count(1)≈count(*)

效率最高是count(*),并不是count(1)

所以建议**尽量使用count(*)**.

### mysql内部代码的优缺点

mysql内部代码有四种：存储过程，存储函数，事件，触发器。 

#### 一、存储过程&存储函数

##### 1、优点：

内部执行，离数据最近，另外在服务器上执行还可以**节省宽带和网络延迟**

**代码重用**，可以方便地统一业务规则，保证某些行为总是一致，也可以为应用提供一定的安全性。

简化代码的维护和版本更新。

帮助提升安全，提供更细颗粒度的权限控制。

缓存执行计划，如果反复调用可以降低消耗。

维护简单，没外部依赖更好在开发和数据库维护人员间分工。 

##### 2、缺点：

**有安全隐患**

mysql没有提供好的开发和调试工具，编写调试困难。

效率差，存储过程使用的函数有限，难以编写复杂的字符串维护功能，也难以实现太复杂的逻辑。

部署带来额外的复杂性。

带来额外的内部存储代码。

给服务器带来额外压力

mysql没有资源消耗控制进程，如果存储过程发生错误，可能直接把服务器拖死。

调试困难。  

#### 二、触发器

##### 1、优点：

减少客户端和服务端之间的通信

简化应用逻辑

提高性能

可用于自动更新反范式化数据或者汇总汇总表数据。 

##### 2、缺点：

功能有限。

对于每一个表的每一个时间，最多只能定义一个触发器。

Mysql只支持“基于行的触发”——所以说，触发器是针对一条记录的。而不是针对整个sql语句的，如果更变的数据集非常大的话，效率会很低。而且触发器会掩盖服务器背后的工种，影响潜在效率，对性能排查造成阻碍。

触发器问题难以排查，尤其是性能问题

触发器可能导致死锁和锁等待，如果触发器失败，sql执行也会失败。

触发器并不能保证更新原子性。

#### 三、事件

在Mysql内部实现通常把复杂代码封装成存储过程再通过call来调用事件在一个独立事件调度进程中被初始化，这个线程和处理链接的线程没有任何关系。不接受常熟也没有返回值。

用于定期维护任务。

### 日期加减

**1. addtime()**　　

为日期加上指定秒数

```
select addtime(now(),1); -- 加1秒
```

**2. adddate()**　　

有两种用法，第二个参数直接填数字的话是为日期加上指定天数，填interval的话是为日期加上指定的interval时间

```
select adddate(now(),1); -- 加1天``select adddate(now(), interval 1 day); -- 加1天``select adddate(now(), interval 1 hour); --加1小时``select adddate(now(), interval 1 minute); -- 加1分钟``select adddate(now(), interval 1 second); -- 加1秒``select adddate(now(), interval 1 microsecond); -- 加1毫秒``select adddate(now(), interval 1 week); -- 加1周``select adddate(now(), interval 1 month); -- 加1月``select adddate(now(), interval 1 quarter); -- 加1季``select adddate(now(), interval 1 year); -- 加1年
```

**4. subtime()**　　

为日期减去指定秒数

```
select subtime(now(), 1); -- 减1秒
```

**5. subdate()**　　

与adddate()函数用法一致，有两种用法，第二个参数直接填数字的话是为日期减去指定天数，填interval的话是为日期减去指定的interval时间

```
select subdate(now(),1); -- 减1天``select subdate(now(), interval 1 day); -- 减1天``select subdate(now(), interval 1 hour); --减1小时``select subdate(now(), interval 1 minute); -- 减1分钟``select subdate(now(), interval 1 second); -- 减1秒``select subdate(now(), interval 1 microsecond); -- 减1毫秒``select subdate(now(), interval 1 week); -- 减1周``select subdate(now(), interval 1 month); -- 减1月``select subdate(now(), interval 1 quarter); -- 减1季``select subdate(now(), interval 1 year); -- 减1年
```

### SQL子类

1. DDL（数据定义语言）
    DDL 主要是指如下的四种SQL 语句，以 CREATE、DROP、ALRET开头和 TRUNCATE TABLE 语句。这里主要说一下 TRUNCATE TABLE ，截断表的数据，也就是删除表中的数据，删除这些数据的时候，系统不做日志，因此无法恢复，删除的速度比较快；而DELETE 语句也是删除表中的记录，但它要写日志，删除的数据可以恢复，数据量大的时候删除比较慢。

2. DML（数据操纵语言）
    它们是SELECT、UPDATE、INSERT、DELETE，就象它的名字一样，这4条命令是用来对数据库里的数据进行操作的语言。

3. DQL（数据查询语言）
    例如：SELECT语句

4. TCL（事务处理语言）
    事物处理语言是指提交、回滚和保留点3句SQL，既是commit、rollback和savepoint。事务是指一系列的连续的不可分割的数据库操作，这些操作要么同时成功，要么同时失败。oracle 的默认事务模型是显式事务模型，即执行完DML后必须手动提交或回滚。

5. DCL（数据控制语言）
    是指授予权限和回收权限语句，既是grant、revoke、deny 等语句。

### MyCat

#### server.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mycat:server SYSTEM "server.dtd">
<mycat:server xmlns:mycat="http://io.mycat/">
	<system>
	<property name="nonePasswordLogin">0</property> <!-- 0为需要密码登陆、1为不需要密码登陆 ,默认为0，设置为1则需要指定默认账户-->
	<property name="useHandshakeV10">1</property>
	<property name="useSqlStat">0</property>  <!-- 1为开启实时统计、0为关闭 -->
	<property name="useGlobleTableCheck">0</property>  <!-- 1为开启全加班一致性检测、0为关闭 -->

		<property name="sequnceHandlerType">2</property>
	<property name="subqueryRelationshipCheck">false</property> <!-- 子查询中存在关联查询的情况下,检查关联字段中是否有分片字段 .默认 false -->
      <!--  <property name="useCompression">1</property>--> <!--1为开启mysql压缩协议-->
        <!--  <property name="fakeMySQLVersion">5.6.20</property>--> <!--设置模拟的MySQL版本号-->
	<!-- <property name="processorBufferChunk">40960</property> -->
	<!-- 
	<property name="processors">1</property> 
	<property name="processorExecutor">32</property> 
	 -->
        <!--默认为type 0: DirectByteBufferPool | type 1 ByteBufferArena | type 2 NettyBufferPool -->
		<property name="processorBufferPoolType">0</property>
		<!--默认是65535 64K 用于sql解析时最大文本长度 -->
		<!--<property name="maxStringLiteralLength">65535</property>-->
		<!--<property name="sequnceHandlerType">0</property>-->
		<!--<property name="backSocketNoDelay">1</property>-->
		<!--<property name="frontSocketNoDelay">1</property>-->
		<!--<property name="processorExecutor">16</property>-->
		<!--
			<property name="serverPort">8066</property> <property name="managerPort">9066</property> 
			<property name="idleTimeout">300000</property> <property name="bindIp">0.0.0.0</property> 
			<property name="frontWriteQueueSize">4096</property> <property name="processors">32</property> -->
		<!--分布式事务开关，0为不过滤分布式事务，1为过滤分布式事务（如果分布式事务内只涉及全局表，则不过滤），2为不过滤分布式事务,但是记录分布式事务日志-->
		<property name="handleDistributedTransactions">0</property>
		
			<!--
			off heap for merge/order/group/limit      1开启   0关闭
		-->
		<property name="useOffHeapForMerge">1</property>

		<!--
			单位为m
		-->
        <property name="memoryPageSize">64k</property>

		<!--
			单位为k
		-->
		<property name="spillsFileBufferSize">1k</property>

		<property name="useStreamOutput">0</property>

		<!--
			单位为m
		-->
		<property name="systemReserveMemorySize">384m</property>


		<!--是否采用zookeeper协调切换  -->
		<property name="useZKSwitch">false</property>

		<!-- XA Recovery Log日志路径 -->
		<!--<property name="XARecoveryLogBaseDir">./</property>-->

		<!-- XA Recovery Log日志名称 -->
		<!--<property name="XARecoveryLogBaseName">tmlog</property>-->
		<!--如果为 true的话 严格遵守隔离级别,不会在仅仅只有select语句的时候在事务中切换连接-->
		<property name="strictTxIsolation">false</property>
		
		<property name="useZKSwitch">true</property>
		
	</system>
	
	<!-- 全局SQL防火墙设置 -->
	<!--白名单可以使用通配符%或着*-->
	<!--例如<host host="127.0.0.*" user="root"/>-->
	<!--例如<host host="127.0.*" user="root"/>-->
	<!--例如<host host="127.*" user="root"/>-->
	<!--例如<host host="1*7.*" user="root"/>-->
	<!--这些配置情况下对于127.0.0.1都能以root账户登录-->
	<!--
	<firewall>
	   <whitehost>
	      <host host="1*7.0.0.*" user="root"/>
	   </whitehost>
       <blacklist check="false">
       </blacklist>
	</firewall>
	-->

	<user name="root" defaultAccount="true">
		<property name="password">123456</property>
		<property name="schemas">TESTDB</property>
		
		<!-- 表级 DML 权限设置 -->
		<!-- 		
		<privileges check="false">
			<schema name="TESTDB" dml="0110" >
				<table name="tb01" dml="0000"></table>
				<table name="tb02" dml="1111"></table>
			</schema>
		</privileges>		
		 -->
	</user>

	<user name="user">
		<property name="password">user</property>
		<property name="schemas">TESTDB</property>
		<property name="readOnly">true</property>
	</user>

</mycat:server>

```

#### schema.xml

```xml
<?xml version="1.0"?>
<!DOCTYPE mycat:schema SYSTEM "schema.dtd">
<mycat:schema xmlns:mycat="http://io.mycat/">

	<schema name="TESTDB" checkSQLschema="false" sqlMaxLimit="100">
		<!-- auto sharding by id (long) -->
		<table name="travelrecord" dataNode="dn1,dn2,dn3" rule="auto-sharding-long" />

		<!-- global table is auto cloned to all defined data nodes ,so can join
			with any table whose sharding node is in the same data node -->
		<table name="company" primaryKey="ID" type="global" dataNode="dn1,dn2,dn3" />
		<table name="goods" primaryKey="ID" type="global" dataNode="dn1,dn2" />
		<!-- random sharding using mod sharind rule -->
		<table name="hotnews" primaryKey="ID" autoIncrement="true" dataNode="dn1,dn2,dn3"
			   rule="mod-long" />
		<!-- <table name="dual" primaryKey="ID" dataNode="dnx,dnoracle2" type="global"
			needAddLimit="false"/> <table name="worker" primaryKey="ID" dataNode="jdbc_dn1,jdbc_dn2,jdbc_dn3"
			rule="mod-long" /> -->
		<table name="employee" primaryKey="ID" dataNode="dn1,dn2"
			   rule="sharding-by-intfile" />
		<table name="customer" primaryKey="ID" dataNode="dn1,dn2"
			   rule="sharding-by-intfile">
			<childTable name="orders" primaryKey="ID" joinKey="customer_id"
						parentKey="id">
				<childTable name="order_items" joinKey="order_id"
							parentKey="id" />
			</childTable>
			<childTable name="customer_addr" primaryKey="ID" joinKey="customer_id"
						parentKey="id" />
		</table>
		<!-- <table name="oc_call" primaryKey="ID" dataNode="dn1$0-743" rule="latest-month-calldate"
			/> -->
	</schema>
	<!-- <dataNode name="dn1$0-743" dataHost="localhost1" database="db$0-743"
		/> -->
	<dataNode name="dn1" dataHost="localhost1" database="db1" />
	<dataNode name="dn2" dataHost="localhost1" database="db2" />
	<dataNode name="dn3" dataHost="localhost1" database="db3" />
	<!--<dataNode name="dn4" dataHost="sequoiadb1" database="SAMPLE" />
	 <dataNode name="jdbc_dn1" dataHost="jdbchost" database="db1" />
	<dataNode	name="jdbc_dn2" dataHost="jdbchost" database="db2" />
	<dataNode name="jdbc_dn3" 	dataHost="jdbchost" database="db3" /> -->
	<dataHost name="localhost1" maxCon="1000" minCon="10" balance="0"
			  writeType="0" dbType="mysql" dbDriver="native" switchType="1"  slaveThreshold="100">
		<heartbeat>select user()</heartbeat>
		<!-- can have multi write hosts -->
		<writeHost host="hostM1" url="localhost:3306" user="root"
				   password="123456">
			<!-- can have multi read hosts -->
			<readHost host="hostS2" url="192.168.1.200:3306" user="root" password="xxx" />
		</writeHost>
		<writeHost host="hostS1" url="localhost:3316" user="root"
				   password="123456" />
		<!-- <writeHost host="hostM2" url="localhost:3316" user="root" password="123456"/> -->
	</dataHost>
	<!--
		<dataHost name="sequoiadb1" maxCon="1000" minCon="1" balance="0" dbType="sequoiadb" dbDriver="jdbc">
		<heartbeat> 		</heartbeat>
		 <writeHost host="hostM1" url="sequoiadb://1426587161.dbaas.sequoialab.net:11920/SAMPLE" user="jifeng" 	password="jifeng"></writeHost>
		 </dataHost>

	  <dataHost name="oracle1" maxCon="1000" minCon="1" balance="0" writeType="0" 	dbType="oracle" dbDriver="jdbc"> <heartbeat>select 1 from dual</heartbeat>
		<connectionInitSql>alter session set nls_date_format='yyyy-mm-dd hh24:mi:ss'</connectionInitSql>
		<writeHost host="hostM1" url="jdbc:oracle:thin:@127.0.0.1:1521:nange" user="base" 	password="123456" > </writeHost> </dataHost>

		<dataHost name="jdbchost" maxCon="1000" 	minCon="1" balance="0" writeType="0" dbType="mongodb" dbDriver="jdbc">
		<heartbeat>select 	user()</heartbeat>
		<writeHost host="hostM" url="mongodb://192.168.0.99/test" user="admin" password="123456" ></writeHost> </dataHost>

		<dataHost name="sparksql" maxCon="1000" minCon="1" balance="0" dbType="spark" dbDriver="jdbc">
		<heartbeat> </heartbeat>
		 <writeHost host="hostM1" url="jdbc:hive2://feng01:10000" user="jifeng" 	password="jifeng"></writeHost> </dataHost> -->

	<!-- <dataHost name="jdbchost" maxCon="1000" minCon="10" balance="0" dbType="mysql"
		dbDriver="jdbc"> <heartbeat>select user()</heartbeat> <writeHost host="hostM1"
		url="jdbc:mysql://localhost:3306" user="root" password="123456"> </writeHost>
		</dataHost> -->
</mycat:schema>
```

#### rule.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mycat:rule SYSTEM "rule.dtd">
<mycat:rule xmlns:mycat="http://io.mycat/">
	<tableRule name="rule1">
		<rule>
			<columns>id</columns>
			<algorithm>func1</algorithm>
		</rule>
	</tableRule>

	<tableRule name="rule2">
		<rule>
			<columns>user_id</columns>
			<algorithm>func1</algorithm>
		</rule>
	</tableRule>

	<tableRule name="sharding-by-intfile">
		<rule>
			<columns>sharding_id</columns>
			<algorithm>hash-int</algorithm>
		</rule>
	</tableRule>
	<tableRule name="auto-sharding-long">
		<rule>
			<columns>id</columns>
			<algorithm>rang-long</algorithm>
		</rule>
	</tableRule>
	<tableRule name="mod-long">
		<rule>
			<columns>id</columns>
			<algorithm>mod-long</algorithm>
		</rule>
	</tableRule>
	<tableRule name="sharding-by-murmur">
		<rule>
			<columns>id</columns>
			<algorithm>murmur</algorithm>
		</rule>
	</tableRule>
	<tableRule name="crc32slot">
		<rule>
			<columns>id</columns>
			<algorithm>crc32slot</algorithm>
		</rule>
	</tableRule>
	<tableRule name="sharding-by-month">
		<rule>
			<columns>create_time</columns>
			<algorithm>partbymonth</algorithm>
		</rule>
	</tableRule>
	<tableRule name="latest-month-calldate">
		<rule>
			<columns>calldate</columns>
			<algorithm>latestMonth</algorithm>
		</rule>
	</tableRule>
	
	<tableRule name="auto-sharding-rang-mod">
		<rule>
			<columns>id</columns>
			<algorithm>rang-mod</algorithm>
		</rule>
	</tableRule>
	
	<tableRule name="jch">
		<rule>
			<columns>id</columns>
			<algorithm>jump-consistent-hash</algorithm>
		</rule>
	</tableRule>

	<function name="murmur"
		class="io.mycat.route.function.PartitionByMurmurHash">
		<property name="seed">0</property><!-- 默认是0 -->
		<property name="count">2</property><!-- 要分片的数据库节点数量，必须指定，否则没法分片 -->
		<property name="virtualBucketTimes">160</property><!-- 一个实际的数据库节点被映射为这么多虚拟节点，默认是160倍，也就是虚拟节点数是物理节点数的160倍 -->
		<!-- <property name="weightMapFile">weightMapFile</property> 节点的权重，没有指定权重的节点默认是1。以properties文件的格式填写，以从0开始到count-1的整数值也就是节点索引为key，以节点权重值为值。所有权重值必须是正整数，否则以1代替 -->
		<!-- <property name="bucketMapPath">/etc/mycat/bucketMapPath</property> 
			用于测试时观察各物理节点与虚拟节点的分布情况，如果指定了这个属性，会把虚拟节点的murmur hash值与物理节点的映射按行输出到这个文件，没有默认值，如果不指定，就不会输出任何东西 -->
	</function>

	<function name="crc32slot"
			  class="io.mycat.route.function.PartitionByCRC32PreSlot">
	</function>
	<function name="hash-int"
		class="io.mycat.route.function.PartitionByFileMap">
		<property name="mapFile">partition-hash-int.txt</property>
	</function>
	<function name="rang-long"
		class="io.mycat.route.function.AutoPartitionByLong">
		<property name="mapFile">autopartition-long.txt</property>
	</function>
	<function name="mod-long" class="io.mycat.route.function.PartitionByMod">
		<!-- how many data nodes -->
		<property name="count">3</property>
	</function>

	<function name="func1" class="io.mycat.route.function.PartitionByLong">
		<property name="partitionCount">8</property>
		<property name="partitionLength">128</property>
	</function>
	<function name="latestMonth"
		class="io.mycat.route.function.LatestMonthPartion">
		<property name="splitOneDay">24</property>
	</function>
	<function name="partbymonth"
		class="io.mycat.route.function.PartitionByMonth">
		<property name="dateFormat">yyyy-MM-dd</property>
		<property name="sBeginDate">2015-01-01</property>
	</function>
	
	<function name="rang-mod" class="io.mycat.route.function.PartitionByRangeMod">
        	<property name="mapFile">partition-range-mod.txt</property>
	</function>
	
	<function name="jump-consistent-hash" class="io.mycat.route.function.PartitionByJumpConsistentHash">
		<property name="totalBuckets">3</property>
	</function>
</mycat:rule>

```



### 排序函数

SQL中有三种排序函数
1、row_number() over(order by 列名)
2、rank() over(order by 列名)
3、dense_rank() over(order by 列名)

row_number():**不考虑数据的重复性**，按照顺序一次打上标号
如：1 2 3 4

rank():是**跳跃排序**
如：1 2 2 4,会跳过3

dense_rank():是**连续排序**，考虑数据的重复性
如：1 2 2 3 序号连续



```
#  1 2 3 4 不在乎相等的情况一直排
select  row_number() over (order by decimal_test) ,t1.* from t1;

# 1 2 2 4 跳跃
select  rank() over (order by decimal_test),t1.* from t1;

# 1 2 2 3 不跳跃
select  dense_rank() over (order by decimal_test),t1.* from t1;

# 现要查询排名在20之后的学生信息并加入排名s_rank（不包括第20名，分数相同则并列排名，排名不间断）
select * from (select *,dense_rank()  over (order by decimal_test) r from t1) d_rank where d_rank.r>2;
```



### SQL执行顺序 

[博客](https://blog.csdn.net/u014044812/article/details/51004754/)

```
FROM WHERE GROUP BY HAVING SELECT ORDER BY
```

```
FROM子句->WHERE子句->GROUP BY子句->HAVING子句->SELECT子句->ORDER BY子句->LIMIT子句->最终结果 
```

### in&exist

or可以使用union代替。

in 一般可以用**exists**去优化或者使用**连接**去优化

in子查询一般是使用memory引擎（hash索引）建立了一个临时表，但结果集不要太多，否则会变成基于磁盘的存储引擎（B+）。

```
in子查询里面一定得是小表，效率比exist高，因为使用in外表是大表可以用到索引，in()里面只执行一次，先执行子查询放到临时表中，再去查询外表和内表进行匹配。

假设子查询B表是小表，效率高
select * from A where cc in (select cc from B) 用到了A表上cc列的索引；

select * from A where exists(select cc from B where cc=A.cc) 效率低，大表A是全表扫描，只用到了小表B表上cc列的索引。 

not in和not exists比较，not exists效率一定比not in高，因为not in都是全表扫描，not exists可能用到索引
```

### 数据类型

> mysql数据类型有：BOOL、TINY INT、INT、BIG INT、FLOAT、DOUBLE、DECIMAL、CHAR、VARCHAR、TINY TEXT、TEXT、Date、DateTime、TimeStamp、Year等等。

![img](javaNote.assets/5f70549b1d24a291.jpg)

#### 一、MySQL的数据类型

主要包括以下五大类：

整数类型：BIT、BOOL、TINY INT、SMALL INT、MEDIUM INT、 INT、 BIG INT

浮点数类型：FLOAT、DOUBLE、DECIMAL

字符串类型：CHAR、VARCHAR、TINY TEXT、TEXT、MEDIUM TEXT、LONGTEXT、TINY BLOB、BLOB、MEDIUM BLOB、LONG BLOB

日期类型：Date、DateTime、TimeStamp、Time、Year

其他数据类型：BINARY、VARBINARY、ENUM、SET、Geometry、Point、MultiPoint、LineString、MultiLineString、Polygon、GeometryCollection等

**1、整型**

| MySQL数据类型 | 含义（有符号）                       |
| ------------- | ------------------------------------ |
| tinyint(m)    | 1个字节 范围(-128~127)               |
| smallint(m)   | 2个字节 范围(-32768~32767)           |
| mediumint(m)  | 3个字节 范围(-8388608~8388607)       |
| int(m)        | 4个字节 范围(-2147483648~2147483647) |
| bigint(m)     | 8个字节 范围(+-9.22*10的18次方)      |

取值范围如果加了unsigned，则最大值翻倍，如tinyint unsigned的取值范围为(0~256)。

int(m)里的m是表示SELECT查询结果集中的显示宽度，并不影响实际的取值范围，没有影响到显示的宽度，不知道这个m有什么用。

**2、浮点型(float和double)**

| MySQL数据类型 | 含义                                          |
| ------------- | --------------------------------------------- |
| float(m,d)    | 单精度浮点型 8位精度(4字节) m总个数，d小数位  |
| double(m,d)   | 双精度浮点型 16位精度(8字节) m总个数，d小数位 |

设一个字段定义为float(6,3)，如果插入一个数123.45678,实际数据库里存的是123.457，但总个数还以实际为准，即6位。整数部分最大是3位，如果插入数12.123456，存储的是12.1234，如果插入12.12，存储的是12.1200.

**3、定点数**

浮点型在数据库中存放的是近似值，而定点类型在数据库中存放的是精确值。

decimal(m,d) 参数m<65 是总个数，d<30且 d<m 是小数位。

**4、字符串(char,varchar,_text)**

| MySQL数据类型 | 含义                            |
| ------------- | ------------------------------- |
| char(n)       | 固定长度，最多255个字符         |
| varchar(n)    | 固定长度，最多65535个字符       |
| tinytext      | 可变长度，最多255个字符         |
| text          | 可变长度，最多65535个字符       |
| mediumtext    | 可变长度，最多2的24次方-1个字符 |
| longtext      | 可变长度，最多2的32次方-1个字符 |

char和varchar：

1.char(n) 若存入字符数小于n，则以**空格补于其后**，查询之时再将空格去掉。所以**char类型存储的字符串末尾不能有空格**，varchar不限于此。

2.char(n) 固定长度，char(4)不管是存入几个字符，都将占用4个字节，varchar是存入的实际字符数+1个字节（n<=255）或2个字节(n>255)，

所以char(4),存入3个字符将占用4个字节。

3.char类型的**字符串检索速度要比varchar类型的快**。



varchar和text：

1.varchar可指定n，text不能指定，内部存储varchar是存入的实际字符数+1个字节（n<=255）或2个字节(n>255)，text是实际字符数+2个字

节。

2.text类型不能有默认值。

3.varchar可直接创建索引，text创建索引要指定前多少个字符。varchar查询速度快于text,在都创建索引的情况下，text的索引似乎不起作用。

**5.二进制数据(_Blob)**

1._BLOB和_text存储方式不同，_TEXT以文本方式存储，英文存储区分大小写，而_Blob是以二进制方式存储，不分大小写。

2._BLOB存储的数据只能整体读出。

3._TEXT可以指定字符集，_BLO不用指定字符集。

**6.日期时间类型**

| MySQL数据类型 | 含义                          |
| ------------- | ----------------------------- |
| date          | 日期 '2008-12-2'              |
| time          | 时间 '12:25:36'               |
| datetime      | 日期时间 '2008-12-2 22:06:44' |
| timestamp     | 自动存储记录修改时间          |

若定义一个字段为timestamp，这个字段里的时间数据会随其他字段修改的时候自动刷新，所以这个数据类型的字段可以存放这条记录最后被修改的时间。

数据类型的属性

| MySQL关键字        | 含义                     |
| ------------------ | ------------------------ |
| NULL               | 数据列可包含NULL值       |
| NOT NULL           | 数据列不允许包含NULL值   |
| DEFAULT            | 默认值                   |
| PRIMARY KEY        | 主键                     |
| AUTO_INCREMENT     | 自动递增，适用于整数类型 |
| UNSIGNED           | 无符号                   |
| CHARACTER SET name | 指定一个字符集           |

#### 二、MYSQL数据类型的长度和范围

各数据类型及字节长度一览表：

| 数据类型           | 字节长度 | 范围或用法                                                   |
| ------------------ | -------- | ------------------------------------------------------------ |
| Bit                | 1        | 无符号[0,255]，有符号[-128,127]，天缘博客备注：BIT和BOOL布尔型都占用1字节 |
| TinyInt            | 1        | 整数[0,255]                                                  |
| SmallInt           | 2        | 无符号[0,65535]，有符号[-32768,32767]                        |
| MediumInt          | 3        | 无符号[0,2^24-1]，有符号[-2^23,2^23-1]]                      |
| Int                | 4        | 无符号[0,2^32-1]，有符号[-2^31,2^31-1]                       |
| BigInt             | 8        | 无符号[0,2^64-1]，有符号[-2^63 ,2^63 -1]                     |
| Float(M,D)         | 4        | 单精度浮点数。天缘博客提醒这里的D是精度，如果D<=24则为默认的FLOAT，如果D>24则会自动被转换为DOUBLE型。 |
| Double(M,D)        | 8        | 双精度浮点。                                                 |
| Decimal(M,D)       | M+1或M+2 | 未打包的浮点数，用法类似于FLOAT和DOUBLE，天缘博客提醒您如果在ASP中使用到Decimal数据类型，直接从数据库读出来的Decimal可能需要先转换成Float或Double类型后再进行运算。 |
| Date               | 3        | 以YYYY-MM-DD的格式显示，比如：2009-07-19                     |
| Date Time          | 8        | 以YYYY-MM-DD HH:MM:SS的格式显示，比如：2009-07-19 11：22：30 |
| TimeStamp          | 4        | 以YYYY-MM-DD的格式显示，比如：2009-07-19                     |
| Time               | 3        | 以HH:MM:SS的格式显示。比如：11：22：30                       |
| Year               | 1        | 以YYYY的格式显示。比如：2009                                 |
| Char(M)            | M        | 定长字符串。                                                 |
| VarChar(M)         | M        | 变长字符串，要求M<=255                                       |
| Binary(M)          | M        | 类似Char的二进制存储，特点是插入定长不足补0                  |
| VarBinary(M)       | M        | 类似VarChar的变长二进制存储，特点是定长不补0                 |
| Tiny Text          | Max:255  | 大小写不敏感                                                 |
| Text               | Max:64K  | 大小写不敏感                                                 |
| Medium Text        | Max:16M  | 大小写不敏感                                                 |
| Long Text          | Max:4G   | 大小写不敏感                                                 |
| TinyBlob           | Max:255  | 大小写敏感                                                   |
| Blob               | Max:64K  | 大小写敏感                                                   |
| MediumBlob         | Max:16M  | 大小写敏感                                                   |
| LongBlob           | Max:4G   | 大小写敏感                                                   |
| Enum               | 1或2     | 最大可达65535个不同的枚举值                                  |
| Set                | 可达8    | 最大可达64个不同的值                                         |
| Geometry           |          |                                                              |
| Point              |          |                                                              |
| LineString         |          |                                                              |
| Polygon            |          |                                                              |
| MultiPoint         |          |                                                              |
| MultiLineString    |          |                                                              |
| MultiPolygon       |          |                                                              |
| GeometryCollection |          |                                                              |

#### 三、使用建议

1、在指定数据类型的时候一般是**采用从小原则**，比如能用TINY INT的最好就不用INT，能用FLOAT类型的就不用DOUBLE类型，这样会对MYSQL在运行效率上提高很大，尤其是大数据量测试条件下。

2、不需要把数据表设计的太过复杂，功能模块上区分或许对于后期的维护更为方便，慎重出现大杂烩数据表

3、数据表和字段的起名字也是一门学问

4、设计数据表结构之前请先想象一下是你的房间，或许结果会更加合理、高效

5、数据库的最后设计结果一定是效率和可扩展性的折中，偏向任何一方都是欠妥的

#### 选择数据类型的基本原则

前提：使用适合存储引擎。

选择原则：根据选定的存储引擎，确定如何选择合适的数据类型。

下面的选择方法按存储引擎分类：

- MyISAM 数据存储引擎和数据列：MyISAM数据表，最好使用固定长度(CHAR)的数据列代替可变长度(VARCHAR)的数据列。
- MEMORY存储引擎和数据列：MEMORY数据表目前都使用固定长度的数据行存储，因此无论使用CHAR或VARCHAR列都没有关系。两者都是作为CHAR类型处理的。
- InnoDB 存储引擎和数据列：建议使用 VARCHAR类型。

对于**InnoDB数据表，内部的行存储格式没有区分固定长度和可变长度列**（所有数据行都使用指向数据列值的头指针），因此在本质上，使用固定长度的CHAR列不一定比使用可变长度VARCHAR列简单。因而，**主要的性能因素是数据行使用的存储总量**。由于CHAR平均占用的空间多于VARCHAR，因 此**使用VARCHAR来最小化需要处理的数据行的存储总量和磁盘I/O是比较好的**。

下面说一下固定长度数据列与可变长度的数据列。

#### text和blob

在使用text和blob字段类型时要注意以下几点，以便更好的发挥数据库的性能。

①BLOB和TEXT值也会引起自己的一些问题，特别是执行了大量的删除或更新操作的时候。删除这种值会在数据表中留下很大的"空洞"，以后填入这些"空洞"的记录可能长度不同,为了提高性能,建议定期使用 OPTIMIZE TABLE 功能对这类表进行碎片整理.

②使用合成的（synthetic）索引。合成的索引列在某些时候是有用的。一种办法是根据其它的列的内容建立一个散列值，并把这个值存储在单独的数据列中。接下来你就可以通过检索散列值找到数据行了。但是，我们要注意这种技术只能用于精确匹配的查询（散列值对于类似<或>=等范围搜索操作符 是没有用处的）。我们可以使用MD5()函数生成散列值，也可以使用SHA1()或CRC32()，或者使用自己的应用程序逻辑来计算散列值。请记住数值型散列值可以很高效率地存储。同样，如果散列算法生成的字符串带有尾部空格，就不要把它们存储在CHAR或VARCHAR列中，它们会受到尾部空格去除的影响。

合成的散列索引对于那些BLOB或TEXT数据列特别有用。用散列标识符值查找的速度比搜索BLOB列本身的速度快很多。

③在不必要的时候避免检索大型的BLOB或TEXT值。例如，SELECT *查询就不是很好的想法，除非你能够确定作为约束条件的WHERE子句只会找到所需要的数据行。否则，你可能毫无目的地在网络上传输大量的值。这也是 BLOB或TEXT标识符信息存储在合成的索引列中对我们有所帮助的例子。你可以搜索索引列，决定那些需要的数据行，然后从合格的数据行中检索BLOB或 TEXT值。

④把BLOB或TEXT列分离到单独的表中。在某些环境中，如果把这些数据列移动到第二张数据表中，可以让你把原数据表中 的数据列转换为固定长度的数据行格式，那么它就是有意义的。这会减少主表中的碎片，使你得到固定长度数据行的性能优势。它还使你在主数据表上运行 SELECT *查询的时候不会通过网络传输大量的BLOB或TEXT值。

#### 浮点数与定点数

为了能够引起大家的重视，在介绍浮点数与定点数以前先让大家看一个例子：

mysql> CREATE TABLE test (c1 float(10,2),c2 decimal(10,2));

``Query OK, 0 rows affected (0.29 sec)``

mysql> insert into test values(**131072.32,131072.32**);

``Query OK, 1 row affected (0.07 sec)``

mysql> select * from test;

``+-----------+-----------+``| c1    | c2    |``+-----------+-----------+``| **131072.31 | 131072.32** |``+-----------+-----------+``1 row in set (0.00 sec)

从上面的例子中我们看到c1列的值由131072.32变成了131072.31，这就是**浮点数的不精确性造成**的。

在mysql中float、double（或real）是浮点数，**decimal（或numberic）是定点数**。

浮点数相对于定点数的优点是在长度一定的情况下，浮点数能够表示更大的数据范围；它的缺点是会引起精度问题。在今后关于浮点数和定点数的应用中，大家要记住以下几点：

1. 浮点数存在误差问题；
2. 对货币等对精度敏感的数据，应该用定点数表示或存储；
3. 编程中，如果用到浮点数，要特别注意误差问题，并尽量避免做浮点数比较；
4. 要注意浮点数中一些特殊值的处理。



- 

```
int(11) 不影响实际存储的范围，实际还是用4个字节去存储
只有一个字段设置了无符号和填充0属性，长度不够才会填充0，长度超过11也是失效的

decimal(10,3)表示共有7位整数3位小数，此例的精确度为10位
```

![image-20220707170611313](javaNote.assets/image-20220707170611313.png)

### char与varchar

#### 区别

varchar是变长字段，需要使用**一个或两个字节存储长度**（当允许存储的最大字节数MW（字符长度*每个字符需要的字节）大于255字节且真实字节数超过127字节时使用2字节，否则使用1字节），所以varchar也要按需分配

varchar会有**内存碎片**问题（比如把200长度**更新**为50），如果一个行占用的空间增长，并且在页内没有更多的空间可以存储，在这种情况下InnoDB需要分裂页来使行可以放进页内，这样会增加碎片。内存碎片容易造成**空间浪费**和**磁盘IO读写性能下降**，因为数据更加随机分散。

char的检索效率会更高

char尾部空格不会存储，不足长度会空格填充，检索的时候会调用trim删除尾部的空格

varchar尾部会存储空格，不足不会补空格



下面的表显示了将各种字符串值保存到CHAR(4)和VARCHAR(4)列后的结果，说明了CHAR和VARCHAR之间的差别：

| 值         | CHAR(4) | 存储需求 | VARCHAR(4) | 存储需求 |
| ---------- | ------- | -------- | ---------- | -------- |
| ''         | ' '     | 4个字节  | ''         | 1个字节  |
| 'ab'       | 'ab '   | 4个字节  | 'ab '      | 3个字节  |
| 'abcd'     | 'abcd'  | 4个字节  | 'abcd'     | 5个字节  |
| 'abcdefgh' | 'abcd'  | 4个字节  | 'abcd'     | 5个字节  |

请注意上表中最后一行的值只适用*不使用严格模式*时；如果MySQL运行在严格模式，超过列长度不的值不保存，并且会出现错误。

从CHAR(4)和VARCHAR(4)列检索的值并不总是相同，因为**检索时从CHAR列删除了尾部的空格**。通过下面的例子说明该差别：

mysql> CREATE TABLE vc (v VARCHAR(4), c CHAR(4));

mysql> INSERT INTO vc VALUES (``'ab '``, ``'ab '``);

mysql> SELECT CONCAT(v, ``'+'``), CONCAT(c, ``'+'``) FROM vc;

![image-20220917103420225](javaNote.assets/image-20220917103420225.png)



#### 适用场景

**CHAR适合存储很短的字符串，或者所有值都接近同一个长度**。例如，CHAR非常适合存储密码的MD5值，因为这是一个定长的值。对于**经常变更的数据**，CHAR也比VARCHAR更好，因为**定长的CHAR类型不容易产生碎片**。对于非常短的列，CHAR比VARCHAR在存储空间上也更有效率。例如用CHAR(1)来存储只有Y和N的值，如果采用单字节字符集只需要一个字节，但是VARCHAR(1)却需要两个字节，因为还有一个记录长度的额外字节。



VARCHAR适合**字符串很长或者所要存储的字符串长短不一，差别很大**；字符串列的**最大长度比平均长度大得多**；**列的更新很少，所以碎片不是问题。**

### Innodb行格式

**默认使用Dynamic**，类似于Compact，只不过**溢出列**有点不同：Compact会只前768字节和指向其他页的地址，

而Dynamic把所有的数据都存到移除页中；

Compact会把变长字段如varchar类型会加入到**变长字段列表**，并且有**null值列表**（使用位标识null值）

Compact、Redundant、Dynamic和Compressed

### 常见sql

```
# 表复制，MySQL仅支持:
create table t3 select * from t2;

不支持select * into new_table from old_table


select id into @id from t2 where id=1;
select @id;

# 建表语句
create table if not exists test.user
(
	id int auto_increment
		primary key,
	username varchar(56) not null,
	password varchar(20) charset latin1 null,
	birthday datetime null,
	score decimal null,
	index idx_name(username),
	unique key uni_key(username),
	foreign key(username) references sys_user(username)
)engine InnoDb,auto_increment=1,charset=utf8;


# 查询选修了所有课程的学生学号和所属部门
# 等价于查询不存在一门课这个学生没选
select s.stu_name,s.stu_department from tb_student s
where not exists (
    select 1 from tb_course c # true表示有一门课该学生没有选
    where not exists(
        select 1 from tb_score where course_id=c.course_id and stu_id=s.stu_id
        )
    )
    
    
# 查询“001”课程比“002”课程成绩高的所有学生的学号;
select * from tb_student s
where exists(
    select 1 from tb_score sc1 where s.stu_id=sc1.stu_id and sc1.course_id=1 and exists(
        select 1 from tb_score sc2 where s.stu_id=sc2.stu_id and sc2.course_id=2 and sc1.score<sc2.score
        )
          );

select a.stu_id from (select * from tb_score s1 where s1.course_id=1) a ,(select * from tb_score s2 where s2.course_id=2) b
where a.stu_id=b.stu_id and a.score<b.score;

# 查询没学过“叶平”老师课的同学的学号、姓名
select * from tb_student s where exists(
    select 1 from tb_course c where c.course_id=1 and not exists( # 选择课程2并且该学生没有选
        select 1 from tb_score sc where sc.course_id=c.course_id and sc.stu_id=s.stu_id
        )
    );
select * from tb_student s where s.stu_id not in (
    select distinct sc.stu_id from tb_course c,tb_score sc where c.course_id=1 and c.course_id=sc.course_id
    );
    
# 查询学过“叶平”老师所教的所有课的同学的学号、姓名;=》不存在一门叶老师的课该学生没有学过
select * from tb_student s where not exists(
    select 1 from tb_course c where c.tea_id=1 and not exists( # 找出叶老师的课并且不存在改选手没选过
        select 1 from tb_score sc where c.course_id=sc.course_id and sc.stu_id=s.stu_id
        ));

select * from tb_student s where s.stu_id in (
    select sc.stu_id from tb_score sc ,tb_course c where sc.course_id=c.course_id and c.tea_id=1 group by sc.stu_id
    having count(*) =(select count(*) from tb_course where tea_id=1)
    );
```

### 复制原理

```
1.主库数据发生改变时使用binlog dump线程写进bin_log
2.从库定期探测主库的bin_log发生变化后
启动IO线程读取主库的binlog,写到relay log中继日志中
再用SQL thread重放binlog同步数据。
```

![bd539a8d61949790cd99aa07953b452.png](javaNote.assets/1604029983639444.png)

### 读写分离

核心：重写AbstractRoutingDataSource的获取key的determineCurrentLookupKey方法

AbstractRoutingDataSource中调用determineTargetDataSource()获取数据源，它又是调用determineCurrentLookupKey()得到数据源的key。那么我们只需重写determineCurrentLookupKey()方法即可

```java
// AbstractRoutingDataSource#determineTargetDataSource()

protected DataSource determineTargetDataSource() {
   Assert.notNull(this.resolvedDataSources, "DataSource router not initialized");
   Object lookupKey = determineCurrentLookupKey();
   DataSource dataSource = this.resolvedDataSources.get(lookupKey);
   if (dataSource == null && (this.lenientFallback || lookupKey == null)) {
      dataSource = this.resolvedDefaultDataSource;
   }
   if (dataSource == null) {
      throw new IllegalStateException("Cannot determine target DataSource for lookup key [" + lookupKey + "]");
   }
   return dataSource;
}
```

于是继承AbstractRoutingDataSource重写获取key的方法determineCurrentLookupKey()

```java
    // 重写获取key方法determineCurrentLookupKey
    @Override
    protected Object determineCurrentLookupKey() {
        DataSourceTypeEnum databaseType = DataSourceContextHolder.getDatabaseType();
        int i;
        List<Map<String, String>> mastersources = dataSourceProperties.getMastersources();
        List<Map<String, String>> slavesources = dataSourceProperties.getSlavesources();
        if(databaseType.equals(DataSourceTypeEnum.DATA_SOURCE_MASTER))
            // 随机获取主数据源
            i= ThreadLocalRandom.current().nextInt(mastersources.size())%mastersources.size();
        else
            i= ThreadLocalRandom.current().nextInt(slavesources.size())%slavesources.size();
        return databaseType.getName()+i; //
    }
```

aop拦截dao层的方法,动态切换数据源

```java
@Aspect
@Slf4j
public class DataSourceAspect {
    private static final String[] queryStrs={"query","select","get"};

    @Pointcut("execution(* com.hu.health.member.dao.*.*(..))")
    public void executeSql(){}

    @Before("executeSql()")
    public void doBefore(JoinPoint joinPoint){
        MethodSignature methodSignature = (MethodSignature) joinPoint.getSignature();
        String mName = methodSignature.getMethod().getName();
        log.info("拦截的sql方法：{}",mName);
        DataSourceContextHolder.setDatabaseType(DataSourceTypeEnum.DATA_SOURCE_MASTER); // 默认master
        for (String queryStr : queryStrs) {
            if(mName.startsWith(queryStr)){
                log.info("查询语句，设置数据源为slave");
                DataSourceContextHolder.setDatabaseType(DataSourceTypeEnum.DATA_SOURCE_SLAVE);
                break;
            }
        }
        log.info("当前数据源是：{}",DataSourceContextHolder.getDatabaseType().getName());
    }
}
```



```
  # 配置读写分离主从数据源
  mastersources:
    -  driverClassName: com.mysql.cj.jdbc.Driver
       url: jdbc:mysql://114.132.44.209:3306/health_ums?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=Asia/Shanghai
       username: root
       password: root
       type: com.alibaba.druid.pool.DruidDataSource

  slavesources:
    - driverClassName: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://114.132.44.209:3307/health_ums?useUnicode=true&characterEncoding=UTF-8&useSSL=false&serverTimezone=Asia/Shanghai
      username: root
      password: root
      type: com.alibaba.druid.pool.DruidDataSource
```



### 视图

视图不能检索，因为没有主键和索引，也没有关联的触发器、默认值等，本质只是一张查看和存放的表，另外只保存视图的定义规则

### 索引下推

https://blog.csdn.net/qq_32979219/article/details/122791064

```
减少回表次数
idx(name,age)
比如select * from t where name='tt%' and age=10
不会用到age索引，开启索引下推后，在二级索引查询到满足tt%的时候，不会直接去聚簇索引查找，而是先判断age是否满足，满足了再回表。

总结：不会减少二级索引扫描的行，但能减少回表的次数，提前过滤不满足另一个索引的记录
```

### 适合建立索引？

答：1.为经常出现order by 、group by、distinct后的字段添加索引

2、在union等集合操作的结果集字段上建立索引

3、经常做查询的字段建立索引

4、经常用在表连接上的字段建立索引

### sql优化步骤

show status like '%%'; # 查看各种统计信息，慢查询，连接数，增删改查次数
show processlist; # 查看当前执行sql的锁等待状态等

explain sql; # 查看执行计划

show profiles ; # 查看执行耗时
show profile cpu for query 29; # 查看cpu损耗

trace; # 分析优化器执行计划



![image-20220616094435687](javaNote.assets/image-20220616094435687.png)

![image-20220616094546403](javaNote.assets/image-20220616094546403.png)

###  索引种类

主键索引

唯一索引

普通索引

联合索引

前缀索引 指定长度 一些地名相同既可以

innodb 主键索引：指向数据行 二级索引指向主键值

isam 没区别

### 索引失效

**运算** 

**通配符** 

**跳过联合索引（最左匹配原则）** 

**范围查询** **、**

**字符串得加‘’（）因为会自动类型转换，索引失效**

**使用覆盖索引**

**Or** **也会失效**

**In****走索引** **not in****不走索引** 

 使用join代替子查询，因为子查询会建立临时表

**Order by****使用有序字段，不然会****filesort** **尽量使用主键返回数据**  

**Group by****默认会排序，可使用** **order by null**

**Join****替代子查询**

### 事务实现原理

#### 一、ACID如何实现

·    事务的原子性是通过 undo log 来实现的 回滚日志

·    事务的持久性性是通过 redo log 来实现的

·    事务的隔离性是通过 (读写锁+MVCC)来实现的

·    而事务的终极大 boss 一致性是通过原子性，持久性，隔离性来实现的！！！

#### 二、隔离级别

##### 1、读未提交

可以读取到未提交的数据，会出现脏读问题

##### 2、读已提交

只能读取到已提交的数据，但是由于是当前读（每次**生成新的ReadView**）,所以产生不可重复读

##### 3、可重复读

**只生成一次ReadView**，所有可重复读。但是会有幻读问题，可通过next-key锁解决

##### 4、串行化

#### 三、MVCC（实现隔离级别）

##### 1、readView一致性视图

当前活跃事务列表（m_ids），最小事务id（max_tx_id），最大事务id（min_tx_id）

##### 2、版本链roll_pointer

聚簇索引两个隐藏列：最新的事务id（tx_id）和回滚日志版本指针（roll_pointer）

##### 3、MVCC如何工作（如何判断是否可读？）

如果tx_id小于min_tx_id，那么说明已提交了，那么可读

如果tx_id大于等于max_tx_id，说明事务是创建当前ReadView之后才生成的，那么对当前事务不可见

如果tx_id在min_tx_id和max_tx_id之间，需要判断是否在ReadView中活跃事务列表m_ids中，如果是，说明依然活跃，那么对当前不可见，否则，对当前事务可见。



如果当前版本不可读，那么会沿着回滚指针往前找旧的版本，知道对当前可读。



对于读已提交来说，由于每次都是生成新的一致性视图，所以事务提交后从活跃事务列表m_ids中移除了事务，对当前可读，导致出现了不可重读问题。

对于可重复读来说，只生成一次一致性视图，所以活跃事务列表m_ids不会改变，所以可以重复读

#### undo_log(回滚日志)

原子性，回滚到原来的样子

增删改记录对应的undo_log，undo log 会写入 Buffer Pool 中的 Undo 页面

#### redo_log(重做日志)

崩溃恢复，保证事务做的修改和undo_log做的修改不丢失

循环写（到检查点的时候就要阻塞刷盘了）

在内存修改该 Undo 页面后，需要记录对应的 redo log。

buffer pool修改的时候也要记录redo_log

刷盘策略，为减少IO操作，不会立即刷盘，有后台线程在合适的时间写入磁盘



> 事务没提交的时候，redo log 会被持久化到磁盘吗？

**会的。**

事务执行中间过程的 redo log 也是直接写在 redo log buffer 中的，这些缓存在 redo log buffer 里的 redo log 也会被「后台线程」每隔一秒一起持久化到磁盘。

也就是说，事务没提交的时候，redo log 也是可能被持久化到磁盘的。

有的同学可能会问，如果 mysql 崩溃了，还没提交事务的 redo log 已经被持久化磁盘了，mysql 重启后，数据不就不一致了？

放心，这种情况 mysql 重启会进行回滚操作，因为事务没提交的时候，binlog 是还没持久化到磁盘的。

所以， redo log 可以在事务没提交之前持久化到磁盘，但是 binlog 必须在事务提交之后，才可以持久化到磁盘。

保存在`ib_logfile`中

[博客](https://www.cnblogs.com/qianyuliang/p/9916372.html)

#### bin_log

追加写

记录更新完后，记录bin_log

statement

row

mix

### 常用命令

```
查看你mysql版本
select version();

查看表的统计信息
show table status like 'table_name' \G
```

### InnoDB和MyISAM区别

innodb支持事务，外键，行锁。

**MyISAM插入查询比较快**。

为什么插入快，因为索引和数据是分开的，因此只需要维护B树索引，数据直接按顺序插入即可；

为什么查询快，同样是因为索引和数据是分开的，因此索引存放的就是数据的地址，而InnoDB还得从聚簇索引找。

### B+树

https://mp.weixin.qq.com/s/A5gNVXMNE-iIlY3oofXtLw

首先就是B树非叶子结点存数据，那么相同数据量的情况下自然高度变高。高端变高，对应就是**磁盘IO**提高。因此，B+树能更加矮胖。

另外，B+树支持范围查询，数据全部存放在叶子节点

B树非叶子结点存放数据，平均查找速度快，但是返回数据有限，相同数据量情况下，磁盘IO性能更低。

1). n叉B+Tree最多含有n个key，而BTree最多含有n-1个key。

2). B+Tree的叶子节点保存所有的key信息，依key大小顺序排列。

 

3). 所有的非叶子节点都可以看作是key的索引部分。

所以查询效率稳定

 

```
聚簇索引：主键缺省使用它 主键所在的索引为ClusterIndex(聚簇索引)
一个表只能有一个主键，所以只能有一个聚簇索引，如果表没有定义主键，则选择第一个非NULL唯一索引作为聚簇索引，如果还没有则生成一个隐藏id列作为聚簇索引。
 
```

\1. 聚集索引。表数据按照索引的顺序来存储的，也就是说索引项的顺序与表中记录的物理顺序一致。对于聚集索引，叶子结点即存储了真实的数据行，不再有另外单独的数据页。 在一张表上最多只能创建一个聚集索引，因为真实数据的物理顺序只能有一种。

叶子结点存放数据的 并且表的物理结构跟索引一样

红黑树的特性：根节点为黑色，红色节点的叶子结点一定是黑色，每一条路径黑色结点数目一样，叶子结点（nil）一定是黑色

### 三种锁级别

**表级锁**：开销小，加锁快；**不会出现死锁**；锁定粒度大，发生锁冲突的概率最高,并发度最低。

行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低,并发度也最高。

页面锁：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般。

### 一、行级锁

**InnoDB的行级锁定的两种类型**：共享锁和排他锁，而在锁定机制的实现过程当中为了让行级锁定和表级锁定共存，InnoDB也一样使用了意向锁（表级锁定）的概念，也就有了意向共享锁和意向排他锁这两种。

#### **1、行级锁的加锁：**

**隐式加锁：**

- InnoDB自动加意向锁。
- 对于UPDATE、DELETE和INSERT语句，InnoDB会自动给涉及数据集加排他锁（X)；
- 对于普通SELECT语句，InnoDB不会加任何锁；

**显示加锁：**

- 共享锁（S）：SELECT * FROM table_name WHERE ... **LOCK IN SHARE MODE**
- 排他锁（X) ：SELECT * FROM table_name WHERE ... **FOR UPDATE**

#### 2、三种行级锁

- Next-Key Lock：Record Lock + Gap Lock 的组合，锁定一个范围，并且锁定记录本身。
- Gap Lock，间隙锁，锁定一个范围，但是不包含记录本身；

- Record Lock，记录锁，也就是仅仅把一条记录锁上；

#### **间隙锁（Next-Key锁）**

**间隙锁定义：**

nnodb的锁定规则是经过在指向数据记录的第一个索引键以前和最后一个索引键以后的空域空间上标记锁定信息而实现的。 Innodb的这种锁定实现方式被称为“ NEXT-KEY locking” （间隙锁），由于Query执行过程当中经过范围查找的话，它会锁定整个范围内全部的索引键值，即便这个键值并不存在。

例：假如emp表中只有101条记录，其empid的值分别是 1,2,…,100,101，下面的SQL：

```
mysql> select * from emp where empid > 100 for update;
```


是一个范围条件的检索，InnoDB不只会对符合条件的empid值为101的记录加锁，也会对empid大于101（这些记录并不存在）的“间隙”加锁。

**间隙锁的缺点：**

- 间隙锁有一个比较致命的弱点，就是当锁定一个范围键值以后，即便某些不存在的键值也会被无辜的锁定，而形成在**锁定的时候没法插入锁定键值范围内的任何数据**。在某些场景下这可能会对性能形成很大的危害
- 当Query**没法利用索引**的时候， Innodb会放弃使用行级别锁定而**改用表级别的锁定**，形成并发性能的下降；
- 当Quuery使用的索引并不包含全部过滤条件的时候，数据检索使用到的索引键所指向的数据可能有部分并不属于该Query的结果集的行列，可是也会被锁定，由于间隙锁锁定的是一个范围，而不是具体的索引键；
- 当Query在使用索引定位数据的时候，若是使用的索引键同样但访问的数据行不一样的时候（索引只是过滤条件的一部分），同样会被锁定

**间隙锁的做用：**

- **防止幻读**，以知足相关隔离级别的要求。
- 为了数据恢复和复制的需要。

**注意**

- 在实际应用开发中，尤为是并发插入比较多的应用，咱们要尽可能优化业务逻辑，**尽可能使用相等条件来访问更新数据，避免使用范围条件**。
- InnoDB除了经过范围条件加锁时使用间隙锁外，若是**使用相等条件请求给一个不存在的记录加锁，InnoDB也会使用间隙锁**。

#### 3、加锁规则

唯一索引等值查询：

- 当查询的记录是存在的，next-key lock 会退化成「**记录锁**」。
- 当查询的记录是不存在的，next-key lock 会退化成「**间隙锁**」。

非唯一索引等值查询：

- 当查询的记录存在时，会加 **next-key lock** 。
- 当查询的记录不存在时，next-key lock会退化为**间隙锁**

非唯一索引和主键索引的范围查询的加锁规则不同之处在于：

- 唯一索引在满足一些条件的时候，next-key lock 退化为**间隙锁和记录锁**。
- 非唯一索引范围查询，next-key lock **不会退化为**间隙锁和记录锁。

#### 4、兼容性及注意事项

![img](javaNote.assets/7bd6a597317e402d90578559456486a8.png)

InnoDB行锁是经过给索引上的索引项加锁来实现的。因此，只有经过索引条件检索数据，InnoDB才使用行级锁，不然，InnoDB将使用表锁。其余注意事项：

- 在**不经过索引**条件查询的时候，InnoDB使用的是**表锁**，而不是行锁。 
- 因为MySQL的行锁是针对索引加的锁，不是针对记录加的锁，因此即便是访问不一样行的记录，若是使用了相同的索引键，也是会出现锁冲突的。
- 当表有多个索引的时候，不一样的事务可使用不一样的索引锁定不一样的行，另外，不管是使用主键索引、惟一索引或普通索引，InnoDB都会使用行锁来对数据加锁。
- 即使在条件中使用了索引字段，但具体是否使用索引来检索数据是由MySQL经过判断不一样执行计划的代价来决定的，若是MySQL认为全表扫描效率更高，好比对一些很小的表，它就不会使用索引，这种状况下InnoDB将使用表锁，而不是行锁。所以，在分析锁冲突时，别忘了检查SQL的执行计划，以确认是否真正使用了索引。

https://blog.csdn.net/zy103118/article/details/124823532

https://xiaolincoding.com/mysql/lock/how_to_lock.html#%E5%94%AF%E4%B8%80%E7%B4%A2%E5%BC%95%E8%8C%83%E5%9B%B4%E6%9F%A5%E8%AF%A2

### 二、表级锁

#### **1、InnoDB如何加表锁：**

在用 **LOCK TABLES**对InnoDB表加锁时要注意，要将AUTOCOMMIT设为0，不然MySQL不会给表加锁；事务结束前，不要用UNLOCK TABLES释放表锁，由于UNLOCK TABLES会隐含地提交事务；COMMIT或ROLLBACK并不能释放用LOCK TABLES加的表级锁，必须用UNLOCK TABLES释放表锁。

```
SET AUTOCOMMIT=0;
LOCK TABLES t1 WRITE, t2 READ, ...;
[do something with tables t1 and t2 here];
COMMIT;
UNLOCK TABLES;
```

#### 2、四种表级锁

- 表锁；

```sql
//表级别的共享锁，也就是读锁；
lock tables t_student read;

//表级别的独占锁，也就是写锁；
lock tables t_stuent write;
```

- 意向锁；
- 元数据锁（MDL）;
- AUTO-INC 锁；

![img](javaNote.assets/f6dae7c2ecd24c0e9074d18d44913e10.png)

### 三、页面锁

### 数据库死锁

超时、事务回滚、死锁检测

#### 1、死锁解决

1、设置**锁超时**时间（innodb_lock_wait_timeout）

2、**回滚小事务**（通过show processlist或show engine innodb status;进行查看）

3、默认有有**死锁检测**（innodb_deadlock_detect)

#### 2、死锁避免

1、按**相同顺序加锁**

2、使用**表级锁**避免死锁

3、一次**申请所有资源**

4、采用读已提交

![image-20220911214158999](javaNote.assets/image-20220911214158999.png)

![image-20220717150243241](javaNote.assets/image-20220717150243241.png)

![image-20220717150226615](javaNote.assets/image-20220717150226615.png)

查看死锁

```
set global innodb_status_output_locks=on;
show engine innodb status;
```

```
------------------------
LATEST DETECTED DEADLOCK 检测到死锁
------------------------
2022-07-17 07:01:52 140343824779008
*** (1) TRANSACTION:
TRANSACTION 47400, ACTIVE 13 sec starting index read
mysql tables in use 1, locked 1
LOCK WAIT 3 lock struct(s), heap size 1128, 2 row lock(s)
MySQL thread id 140915, OS thread handle 140343238305536, query id 35590030 27.47.107.87 root statistics
/* ApplicationName=DataGrip 2020.1 */
select * from community_question where id=54 for update 找到执行的语句

当前事务拥有的锁 space id 864 page no 4 n bits 72
*** (1) HOLDS THE LOCK(S):
RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47400 lock_mode X locks rec but not gap
Record lock, heap no 2 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000034; asc        4;;
 1: len 6; hex 00000000b366; asc      f;;
 2: len 7; hex 01000000a52828; asc      ((;;
 3: len 4; hex 32333132; asc 2312;;
 4: len 6; hex 736164617364; asc sadasd;;
 5: len 4; hex 62581c3f; asc bX ?;;
 6: len 4; hex 625c2bda; asc b\+ ;;
 7: len 8; hex 8000000000000000; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 0; hex ; asc ;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000000; asc         ;;
 14: len 0; hex ; asc ;;
 15: len 0; hex ; asc ;;
 16: len 0; hex ; asc ;;
 17: SQL NULL;

等待获取的锁，space id 864 page no 4 n bits 72
*** (1) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47400 lock_mode X locks rec but not gap waiting
Record lock, heap no 3 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000036; asc        6;;
 1: len 6; hex 00000000b3f0; asc       ;;
 2: len 7; hex 81000001350110; asc     5  ;;
 3: len 12; hex e68891e698afe6a087e9a298; asc             ;;
 4: len 18; hex e58685e5aeb9e58685e5aeb9e58685e5aeb9; asc                   ;;
 5: len 4; hex 625e849e; asc b^  ;;
 6: len 4; hex 625e849e; asc b^  ;;
 7: len 8; hex 8000000000000002; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 9; hex 6a6176613b7068703b; asc java;php;;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000001; asc         ;;
 14: len 22; hex 687474703a612e6a70673b687474703a622e6a70673b; asc http:a.jpg;http:b.jpg;;;
 15: len 9; hex e7bc96e7a88be58cba; asc          ;;
 16: len 4; hex 6d6f6f6e; asc moon;;
 17: len 4; hex 80000000; asc     ;;


*** (2) TRANSACTION:
TRANSACTION 47399, ACTIVE 18 sec starting index read
mysql tables in use 1, locked 1
LOCK WAIT 3 lock struct(s), heap size 1128, 2 row lock(s)
MySQL thread id 140916, OS thread handle 140341719037696, query id 35590060 27.47.107.87 root statistics
/* ApplicationName=DataGrip 2020.1 */ select * from community_question where id=52 for update

拥有的锁 space id 864 page no 4 n bits 72
*** (2) HOLDS THE LOCK(S):
RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47399 lock_mode X locks rec but not gap
Record lock, heap no 3 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000036; asc        6;;
 1: len 6; hex 00000000b3f0; asc       ;;
 2: len 7; hex 81000001350110; asc     5  ;;
 3: len 12; hex e68891e698afe6a087e9a298; asc             ;;
 4: len 18; hex e58685e5aeb9e58685e5aeb9e58685e5aeb9; asc                   ;;
 5: len 4; hex 625e849e; asc b^  ;;
 6: len 4; hex 625e849e; asc b^  ;;
 7: len 8; hex 8000000000000002; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 9; hex 6a6176613b7068703b; asc java;php;;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000001; asc         ;;
 14: len 22; hex 687474703a612e6a70673b687474703a622e6a70673b; asc http:a.jpg;http:b.jpg;;;
 15: len 9; hex e7bc96e7a88be58cba; asc          ;;
 16: len 4; hex 6d6f6f6e; asc moon;;
 17: len 4; hex 80000000; asc     ;;

等待的锁 space id 864 page no 4 n bits 72
*** (2) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47399 lock_mode X locks rec but not gap waiting
Record lock, heap no 2 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000034; asc        4;;
 1: len 6; hex 00000000b366; asc      f;;
 2: len 7; hex 01000000a52828; asc      ((;;
 3: len 4; hex 32333132; asc 2312;;
 4: len 6; hex 736164617364; asc sadasd;;
 5: len 4; hex 62581c3f; asc bX ?;;
 6: len 4; hex 625c2bda; asc b\+ ;;
 7: len 8; hex 8000000000000000; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 0; hex ; asc ;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000000; asc         ;;
 14: len 0; hex ; asc ;;
 15: len 0; hex ; asc ;;
 16: len 0; hex ; asc ;;
 17: SQL NULL;

这里采用回滚事务2解决死锁
*** WE ROLL BACK TRANSACTION (2)
------------
TRANSACTIONS
------------
Trx id counter 47401
Purge done for trx's n:o < 47377 undo n:o < 0 state: running but idle
History list length 0
LIST OF TRANSACTIONS FOR EACH SESSION:
---TRANSACTION 421819211000184, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819210999376, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819210997760, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819211001800, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819210998568, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819211003416, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819211000992, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819210996144, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 421819210995336, not started
0 lock struct(s), heap size 1128, 0 row lock(s)
---TRANSACTION 47400, ACTIVE 130 sec
3 lock struct(s), heap size 1128, 2 row lock(s)
MySQL thread id 140915, OS thread handle 140343238305536, query id 35590068 27.47.107.87 root
TABLE LOCK table `health_community`.`community_question` trx id 47400 lock mode IX
RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47400 lock_mode X locks rec but not gap
Record lock, heap no 2 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000034; asc        4;;
 1: len 6; hex 00000000b366; asc      f;;
 2: len 7; hex 01000000a52828; asc      ((;;
 3: len 4; hex 32333132; asc 2312;;
 4: len 6; hex 736164617364; asc sadasd;;
 5: len 4; hex 62581c3f; asc bX ?;;
 6: len 4; hex 625c2bda; asc b\+ ;;
 7: len 8; hex 8000000000000000; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 0; hex ; asc ;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000000; asc         ;;
 14: len 0; hex ; asc ;;
 15: len 0; hex ; asc ;;
 16: len 0; hex ; asc ;;
 17: SQL NULL;

RECORD LOCKS space id 864 page no 4 n bits 72 index PRIMARY of table `health_community`.`community_question` trx id 47400 lock_mode X locks rec but not gap
Record lock, heap no 3 PHYSICAL RECORD: n_fields 18; compact format; info bits 0
 0: len 8; hex 8000000000000036; asc        6;;
 1: len 6; hex 00000000b3f0; asc       ;;
 2: len 7; hex 81000001350110; asc     5  ;;
 3: len 12; hex e68891e698afe6a087e9a298; asc             ;;
 4: len 18; hex e58685e5aeb9e58685e5aeb9e58685e5aeb9; asc                   ;;
 5: len 4; hex 625e849e; asc b^  ;;
 6: len 4; hex 625e849e; asc b^  ;;
 7: len 8; hex 8000000000000002; asc         ;;
 8: len 4; hex 80000000; asc     ;;
 9: len 4; hex 80000000; asc     ;;
 10: len 4; hex 80000000; asc     ;;
 11: len 9; hex 6a6176613b7068703b; asc java;php;;;
 12: len 4; hex 80000000; asc     ;;
 13: len 8; hex 8000000000000001; asc         ;;
 14: len 22; hex 687474703a612e6a70673b687474703a622e6a70673b; asc http:a.jpg;http:b.jpg;;;
 15: len 9; hex e7bc96e7a88be58cba; asc          ;;
 16: len 4; hex 6d6f6f6e; asc moon;;
 17: len 4; hex 80000000; asc     ;;

```

### key和index

```
key可以约束数据完整性，也可以起索引的作用，MySQL建key会自动建索引。

primary key
unique key
forign key
mul key 普通key,等价普通索引


主键索引
唯一索引 一般使用unique key创建
普通索引
```

### 存储引擎

#### innodb

**事务、外键、行锁**

支持分布式事务和安全点（安全点是指事务的部分回滚）

聚簇索引

#### myisam

**非事务**主要存储引擎，查询和插入效率高，占用空间和内存少

#### memory

读写快，数据易丢失

### RESTRICT&CASCADE

```
RESTRICT表示表的删除是有条件限制的，要删除的基本表不能被其他表的约束所引用，不能有视图，不能有触发器，不能有存储过程或函数等。如果存在这些依赖该表的对象，则表不能被删除

CASCADE表示表的删除没有限制条件，在删除基本表的同时，相关的依赖对象（如视图）都将被删除。
```

### truncate&delete&drop

1、相同点;都是只删数据不删表结构
2、不同点

- truncate和drop一样是**DDL**,删除立即生效，元数据不会放到rollback segment中，不能回滚和触发trigger;
- truncate通过**释放数据页来删除数据**，并在事务日志页标记页的释放，使用事务资源少；delete每删除一行就写入事务日志
- truncate**存在外键删除失败**，无论这个外键是否存在；
- truncate只能删除全部数据；
- truncate自增值重置为0，删除返回值也是0

### 关系代数

![在这里插入图片描述](javaNote.assets/2021042713292577.png)



#### 选取Selection

![在这里插入图片描述](javaNote.assets/20210427133725889.png)



#### 投影Projection

![在这里插入图片描述](javaNote.assets/20210427133951280.png)

#### θ连接θJoin

自然连接要求相同属性值的属性名相同，即是去除了重复列的等值连接

![在这里插入图片描述](javaNote.assets/20210427134404575.png)

![在这里插入图片描述](javaNote.assets/2021042713443119.png)

![在这里插入图片描述](javaNote.assets/20210427134513780.png)

![在这里插入图片描述](javaNote.assets/20210427134545302.png)



#### 除法Division

![在这里插入图片描述](javaNote.assets/20210427134839698.png)

### 三大范式

1.列不可再分
2.唯一标识一行，消除部份依赖，满足**完全依赖**
3.消除传递依赖，非主属性**只能依赖主属性**，可设置外键解决

### 索引失效

对索引计算，索引会失效，因为索引计算就跟原来的排序规则不一样了

```
select 1='1'  1
select 0='a'  1  转为整形再比较，非数字字符自动转为0，数字字符转为对应的数字

t1{
	a int,
	e char
}
select * from t1 where a=1   走索引
select * from t1 where a='1' 走索引,因为‘1'自动转为1，且不是字段a去运算

select * from t1 where e=1   不走索引，字段e被计算（那么就跟原来排序规则不一样了），统一e转为数字再比较
select * from t1 where e=‘1’ 走索引，因为本来就是字符，不用计算
```

### 数据库字符集和排序规则

```
alter database health_community charset =utf8 collate=utf8_general_ci;
```

utfmb4默认排序规则utf8mb4_0900_ai_ci

![image-20220413203933782](javaNote.assets/image-20220413203933782.png)

查看字符集

```
SHOW VARIABLES LIKE 'character%';
SHOW VARIABLES LIKE 'collation_%';
```

### 主从复制、读写分离

#### Slave_SQL_Running stop

```
Slave SQL for channel '': Worker 1 failed executing transaction 'ANONYMOUS' at master log master-bin.000007, end_log_pos 510; Could not execute Delete_rows event on table health_community.community_area; Can't find record in 'community_area', Error_code: 1032; handler error HA_ERR_KEY_NOT_FOUND; the event's master log FIRST, end_log_pos 510, Error_code: MY-001032

当主从数据不一致的时候，比如主有一行数据a,但从没有数据a,当主删除a的时候，从就会报数据不一致，并停止从库协调器和工作进程运行
The slave coordinator and worker threads are stopped, possibly leaving data in inconsistent state. A restart should restore consistency automatically, although using non-transactional storage for data or info tables or DDL queries could lead to problems. In such cases you have to examine your data (see documentation for details). Error_code: MY-001756

```

#### 主从不一致解决方案

[博客](https://baijiahao.baidu.com/s?id=1711660568537406582&wfr=spider&for=pc)

设置为只读状态，备份数据库，导入从库，然后再重新开启主从同步+

```
1.先进入主库，进行锁表，防止数据写入

mysql> flush tables with readlock;注意：该处是锁定为只读状态，语句不区分大小写

2.进行数据备份

#把数据备份到mysql.bak.sql文件

mysqldump -uroot -p -hlocalhost > mysql.bak.sql这里注意一点：数据库备份一定要定期进行，可以用shell脚本或者python脚本，都比较方便，确保数据万无一失。

3.查看master 状态

mysql> showmasterstatus;+-------------------+----------+--------------+-------------------------------+| File | Position | Binlog_Do_DB | Binlog_Ignore_DB |+-------------------+----------+--------------+-------------------------------+| mysqld-bin.000001 | 3260 | | mysql,test,information_schema |+-------------------+----------+--------------+-------------------------------+1 row in set (0.00 sec)4.把mysql备份文件传到从库机器，进行数据恢复

scp mysql.bak.sql root@192.168.128.101:/tmp/5.停止从库的状态

mysql> stopslave;

6.然后到从库执行mysql命令，导入数据备份

mysql> source /tmp/mysql.bak.sql

7.设置从库同步，注意该处的同步点，就是主库show master status信息里的| File| Position两项

changemasterto master_host = '192.168.128.100', master_user = 'rsync', master_port=3306, master_password='', master_log_file = 'mysqld-bin.000001', master_log_pos=3260;8.重新开启从同步

mysql> startslave;
9.查看同步状态

mysql> showslavestatus\G Slave_IO_Running: YesSlave_SQL_Running: Yes10.回到主库并执行如下命令解除表锁定。

UNLOCKTABLES
```

#### 读写分离

1. 中间件：amoeba，MySQL-Proxy

2. 应用程序路由

[代码实现](https://www.cnblogs.com/wollow/p/10839890.html)

![img](javaNote.assets/15299539-cefd7cd3f750b59c.jpg)

#### 授权命令

```
select * from user;

update user set host = '%' where user = 'root' and host='localhost';

GRANT ALL ON *.* TO 'root'@'%' 
flush privileges;    
```

#### [Entrypoint]: Switching to dedicated user 'mysql

```
指定新的挂载目录运行正常, 搜遍全网都没有找到答案

解决办法:
删除以下文件(建议删除前备份):

data/ib_logfile0
data/ib_logfile1
...
1
2
3
重新启动就可以了

原因
主要是因为我修改了虚拟机的内存分配, 导致mysql 8写日志的大小计算出了问题.
删除文件让mysql重新生成OK, 或者可以把虚拟机设置为原来分配的内存大小
```

![image-20220401184757175](javaNote.assets/image-20220401184757175.png)

### 命令

```
docker run -itd --name  mysql5.7-master -p 3307:3306 \
 -v /opt/module/mysql/master/conf:/etc/mysql/conf.d \
 -v /opt/module/mysql/master/data:/var/lib/mysql \
 -v /opt/module/mysql/master/logs:/var/log/mysql \
 -e MYSQL_ROOT_PASSWORD=root \
 mysql:5.7
 
 docker run -itd --name  mysql5.7-slave -p 3308:3306 \
 -v /opt/module/mysql/slave/conf:/etc/mysql/conf.d \
 -v /opt/module/mysql/slave/data:/var/lib/mysql \
 -v /opt/module/mysql/slave/logs:/var/log/mysql \
 -e MYSQL_ROOT_PASSWORD=root \
 mysql:5.7
 
  docker run -itd --name  mysql5.7-3309 -p 3309:3306 \
 -v /opt/module/mysql/slave2/conf:/etc/mysql/conf.d \
 -v /opt/module/mysql/slave2/data:/var/lib/mysql \
 -v /opt/module/mysql/slave2/logs:/var/log/mysql \
 -e MYSQL_ROOT_PASSWORD=root \
 mysql:5.7
```



```
version: '2.2'
services:
    mysql-new:
        container_name: docker_tool_mysql
        cpus: "2"
        mem_limit: "3G"
        environment:
            MYSQL_ROOT_PASSWORD: "root"
        image: "docker.io/mysql:8.0.28"
        restart: always
        volumes:
            - "/mydata/mysql/data:/var/lib/mysql"
            - "/mydata/mysql/config/my.cnf:/etc/mysql/my.cnf"
            - "/mydata/mysql/init:/docker-entrypoint-initdb.d/"
            - "/mydata/mysql/mysql-files:/var/lib/mysql-files/
        ports:
            - "3306:3306"
```

#### 配置文件

```
[client] 
default-character-set=utf8 

[mysql] 
default-character-set=utf8 

[mysqld] 
init_connect='SET collation_connection = utf8_general_ci' 
init_connect='SET NAMES utf8' 
character-set-server=utf8 
collation-server=utf8_general_ci
skip-character-set-client-handshake 
skip-name-resolve
# 配置主从复制
server-id=11
log_bin=master-bin
log_bin_index=master-bin.index 
# 防止statement模式数据不一致问题（随机数，now()）
binlog_format=row
binlog-ignore-db=mysql
#备注：
#server-id 服务器唯一标识。
#log_bin 启动MySQL二进制日志，即数据同步语句，从数据库会一条一条的执行这些语句。
#binlog_do_db 指定记录二进制日志的数据库，即需要复制的数据库名，如果复制多个数据库，重复设置这个选项即可。
#binlog_ignore_db 指定不记录二进制日志的数据库，即不需要复制的数据库名，如果有多个数据库，重复设置这个选项即可。
#其中需要注意的是，binlog_do_db和binlog_ignore_db为互斥选项，一般只需要一个即可。

max_connections=400
max_user_connections=700
wait_timeout=400
```

#### 开机自启动

```
让MySQL数据库随系统的开机而启动：chkconfig mysqld on

关闭MySQL的开机自启动：chkconfig mysqld off
```

#### 安装

- [安装MySql5.7](https://www.jianshu.com/p/19291fb17b99)
- [彻底删除mysql](https://www.cnblogs.com/Can-daydayup/p/10873948.html)
- [有道云笔记](http://note.youdao.com/noteshare?id=7e33e28807934dc31985f3226e119ced&sub=8A1383DDFDDA4842BB01E516A7B5DAD8)
- [参考博客](https://www.cnblogs.com/Can-daydayup/p/10877500.html)

1. 查看mysql状态

   ```bash
   systemctl status mysqld
   ```

2. 配置允许远程连接

   ```bash
   1、改表法
   update user set host = '%' where user = 'root';
   select host, user from user;
   
   2、授权法
   grant 权限 on 数据库名.表名 to 用户@登录主机 identified by "用户密码";
   GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
   FLUSH PRIVILEGES;
   ```


3. Xshell登录mysql

   ```
   mysql -uroot -h127.0.0.1 -p
   ```

4. 启动

   ```
   servcie mysqld restart
   ```

5. 查看版本信息

   ```
   status
   SELECT VERSION();//5.7.26
   ```


6. 建库

   ```
   CREATE DATABASE test2 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci
   ```

   

#### 远程连接

- mysql和ssh配合连接
- 注：我的sql主机地址填127.0.0.1
- [原文链接](https://blog.csdn.net/benben1580/article/details/79334523)

#### Sqlyog创建存储过程

记：SQLyog中的Query编辑器下，分号分隔符是通知mysql客户端已经输入完成的符号，而存储过程中有很多分号，所以一运行就报错。

解决办法：找到数据库中Stored Proces然后右击选择创建存储过程

#### length与char_length

```
char_length(str)

	计算单位：字符

	不管汉字还是数字或者是字母都算是一个字符

length(str)

	计算单位：字节

	utf8编码：一个汉字三个字节，一个数字或字母一个字节。

	gbk编码：一个汉字两个字节，一个数字或字母一个字节。
```

#### varchar（）类型

```
MySQL5.0.3版本之后

varchar(char_length)：按字符算

数据类型大小：0--65535字节，但最多占65532字节(其中需要用两个字节存放长度，小于255字节用1个字节存放长度)

详解：varchar(20)表示字符数，不管什么编码，不管是英文还是中文都可以存放20个。
```

##### 查看一个表是某个表的外键

```
SELECT TABLE_NAME,COLUMN_NAME,CONSTRAINT_NAME, REFERENCED_TABLE_NAME,REFERENCED_COLUMN_NAME FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE REFERENCED_TABLE_NAME = '表名';
```

#### Server returns invalid timezone. 

Go to 'Advanced' tab and set 'serverTimezone' property

```
# 原因：没设置时区
show variables like'%time_zone'; # 显示 SYSTEM 就是没有设置时区
set global time_zone = '+8:00';
```

#### [mysql-建表、添加字段、修改字段、添加索引SQL语句写法](https://www.cnblogs.com/f-rt/p/11141421.html)

#### mysql与TIMESTAMP（时间戳）

[博客](https://www.jb51.net/article/51794.htm)

1. 在创建新记录和修改现有记录的时候都对这个数据列刷新

```sql
TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
```

2. 在创建新记录的时候把这个字段设置为当前时间，但以后修改时，不再刷新它

```sql
TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

3. 异同

```
相同点：
1.可自动更新和初始化，默认显示格式相同YYYY-MM-dd HH:mm:ss

不同点：
2. timestamp的时间范围是：‘1970-01-01 00:00:01' UTC to ‘2038-01-19 03:14:07' UTC ，自动时区转化，实际存储毫秒数，4字节存储
3. datetime的时间范围：‘1000-01-01 00:00:00' to ‘9999-12-31 23:59:59' ，不支持时区，8字节存储
```

#### err_log、bin_log、slow_log

error_log

`记录db启动，运行，停止时间严重错误`

bin_log

```
DDL 操作表结构，字段的语句。
DCL 权限等一些控制语句。
DML 操作表的语句（insert,update,delete），并且是已经提交的，未提交的不会记录
```

slow_log

`记录慢SQL语句的日志,定位低效SQL语句的工具日志，默认不开启`

#### docker命令

![image-20220114195621548](javaNote.assets/image-20220114195621548.png)

#### 自增id

```
innodb
5.7:最大值保存到内存中，不重启不会弥补空闲
重启会重新找到最大的加一
8.0：写入 redo log，保存到引擎专用的系统表中。
重启后找redo日志和当前表数值中的最小值
```

#### mySql中Truncate的用法

[博客](https://blog.csdn.net/sun_shang/article/details/78064190)

区别

```
truncate:删除表的数据不会在事务日志中记录，是释放数据页来删除数据，并只会在事务日志中记录数据页；所以ROLLBACK语句不会撤销
用TRUNCATE TABLE删除数据的表上增加数据时，要使用UPDATE STATISTICS来维护索引信息。

```

## Redis

### [SCAN](http://www.redis.cn/commands/scan.html) 

[SCAN](http://www.redis.cn/commands/scan.html) 命令及其相关的 [SSCAN](http://www.redis.cn/commands/sscan.html), [HSCAN](http://www.redis.cn/commands/hscan.html) 和 [ZSCAN](http://www.redis.cn/commands/zscan.html) 命令都用于增量迭代一个集合元素。

- [SCAN](http://www.redis.cn/commands/scan.html) 命令用于迭代当前数据库中的key集合。
- [SSCAN](http://www.redis.cn/commands/sscan.html) 命令用于迭代SET集合中的元素。
- [HSCAN](http://www.redis.cn/commands/hscan.html) 命令用于迭代Hash类型中的键值对。
- [ZSCAN](http://www.redis.cn/commands/zscan.html) 命令用于迭代SortSet集合中的元素和元素对应的分值

### 高可用

#### 主从复制

```
Slave启动成功连接到master后会发送一个sync命令

Master接到命令启动后台的存盘进程，同时收集所有接收到的用于修改数据集命令， 在后台进程执行完毕之后，master将传送整个数据文件到slave,以完成一次完全同步

全量复制：而slave服务在接收到数据库文件数据后，将其存盘并加载到内存中。

增量复制：Master继续将新的所有收集到的修改命令依次传给slave,完成同步

但是只要是重新连接master,一次完全同步（全量复制)将被自动执行
```

命令: slaveof host port

#### 哨兵

https://blog.csdn.net/zhanghuiqi205/article/details/112169486

##### 配置

```
sentinel monitor mymaster 192.168.14.101 6379 2 # 投票master宕机的数量
```

##### **工作原理**

一、三个定时任务

```
1、每个sentinel对master和slave执行info命令，第一个是用来发现slave节点，第二个是确定主从关系
2、每个sentinel通过master的channel发布订阅交换节点信息和自身信息，判断主管下线还是客观下线
3、每个sentinel对其他sentinel和redis执行ping命令，用于心跳检测，作为存活的依据
```

二、主管下线和客观下线

```
主观下线：当前sentinel实例认为master服务不可用
客观下线：多个sentinel实例认为master服务不可用，此时master变为主观下线状态
```

三、故障转移

故障转移是由 sentinel 领导者节点来完成的(只需要一个sentinel节点),关于 sentinel 领导者节点的选取也是每个 sentinel 向其他 sentinel 节点发送我要成为领导者的命令,超过半数sentinel 节点同意,并且也大于quorum ,那么他将成为领导者,如果有多个sentinel都成为了领导者,则会过段时间在进行选举

故障转移步骤

```
1、从slave结点选出合适的结点作为master节点
	slave-priority越小优先级越高
	复制偏移量offset越大优先级越高（数据越完整）
	runId最小的slave结点（启动越早）
2、对上面选出来的执行slaveof of no one
3、像剩余结点发送命令，让他们成为新master的slave结点
4、更新原来的master节点配置为slave节点，重新恢复去复制新master的节点信息
```

##### 优缺点

```
优点：主从复制的加强版，自动主从切换
缺点：在线扩容比较麻烦；只有主节点提供服务，不太支持高并发
```

##### 总结

```
sentinel集群是独立的线程，能够监控redis集群，发现master宕机后自动切换。
```

#### 集群

https://blog.csdn.net/xueguchen/article/details/109847085

原理简介

```
将所有数据分为16384个槽位slots,每个节点负责一部分槽位。槽位的信息存储于每个节点中。

使用crc16算法进行hash并对16384取模得到具体槽位，客户端发送请求后可以缓存槽位信息。

当节点发现槽位信息不归自己管理时，会发送跳转指令携带目标操作的节点地址，客户端跳转到正确的节点进行操作，并更新本地的槽位映射表。

集群节点采用gossip协议进行通信
goosip协议包含多种消息，包括ping,pong,meet,fail等
优点在于元数据的更新比较分散，不是集中在一个地方，陆陆续续打到所有节点上，减少网络负担。（每次选择最久没通信的节点，携带少量的其他信息，因此有一定的交互延迟）
meet:发送meet给新加入的节点，让新节点加入集群
ping:互相ping交换自己的状态和维护的集群状态
pong:对ping和meet消息的返回，包含自己的状态和信息，也可用于广播和更新
fail:某节点发现其他节点宕机后，发送fail通知其他节点
```

JedisCluster客户端

初始化的时候，随机选择一个node,初始化hashslot映射表，同时为每个节点创建一个JedisPolol连接池。每次基于JedisCluster操作，现在本地计算key的hashSlot并找到对应的节点。

### 缓存异常

缓存雪崩：缓存数据同时过期。设置不同的过期时间或加锁排队；预热；发送消息队列给后台进行续命

缓存击穿：单点key失效导致大量请求同时进来：加锁；定时任务续命

缓存穿透：查询不存在的数据：采用布隆过滤器（bitMap映射所有的数据，过滤掉不存在的请求）；存储null值

###  数据结构

（1）String :简单动态字符串 len(已使用) free（剩余）

（2）List: 快速链表（quickList）：链表+压缩列表 

压缩列表：（总字节数 偏移量 节点个数）  

每个结点：前一个结点长度（导致连锁更新） 数据类型 真正的值

Set :hash表+整数集合（元素全部为整数）

Zset 指向zset数据结构，使用跳表+字典

因此跳表支持范围查询，字典支持o(1)获取权值

Hash表就是：entry数组（哈希到数组上）

Entry结点key v(union结构体，因此int16 int 32所以节省内存)

Rehash 1

###  事务

Redis事务 multi discard exec 

组队过程中有error则会组队失败，若没有问题，最终执行的会有失败也有成功

### 集群脚本

```
#!/bin/bash
array=( 6379 6380 6381 6389 6390 6391 )
for e in ${array[@]}
do
        #echo $e 
        rm "dump"$e".rdb"
        rm "nodes-"$e".conf"
        `redis-server $e".conf"`
done
redis-cli --cluster create --cluster-replicas 1 192.168.42.100:6379 192.168.42.100:6380 192.168.42.100:6381 192.168.42.100:6389 192.168.42.100:6390 192.168.42.100:6391
```

![image-20220514145004953](javaNote.assets/image-20220514145004953.png)

### 双写不一致

分布式锁

读写锁

乐观锁

内存队列：同个key的操作放到一个对列中串行执行

#### ![image-20220514145704064](javaNote.assets/image-20220514145704064.png)主从复制锁失效

从结点没同步，分布式锁失效怎么办？（因为redis是AP,主节点设置成功了马上返回）

```
redlock 半数成功才算成功
```

![image-20220514144425775](javaNote.assets/image-20220514144425775.png)

**分布锁性能问题怎么办？**

参考concurrentHashMap分段锁，减少锁的粒度

![image-20220514144823706](javaNote.assets/image-20220514144823706.png)

#### 默认配置文件

```
bind 127.0.0.1
protected-mode yes
port 6379
tcp-backlog 511
timeout 0
tcp-keepalive 300
daemonize yes
supervised no
pidfile /var/run/redis_6379.pid
loglevel notice
logfile ""
databases 16
always-show-logo yes
save 900 1
save 300 10
save 60 10000
stop-writes-on-bgsave-error yes
rdbcompression yes
rdbchecksum yes
dbfilename dump.rdb
rdb-del-sync-files no
dir ./
replica-serve-stale-data yes
replica-read-only yes
repl-diskless-sync no
repl-diskless-sync-delay 5
repl-diskless-load disabled
repl-disable-tcp-nodelay no
replica-priority 100
acllog-max-len 128
lazyfree-lazy-eviction no
lazyfree-lazy-expire no
lazyfree-lazy-server-del no
replica-lazy-flush no
lazyfree-lazy-user-del no
oom-score-adj no
oom-score-adj-values 0 200 800
appendonly no
appendfilename "appendonly.aof"
appendfsync everysec
no-appendfsync-on-rewrite no
auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb
aof-load-truncated yes
aof-use-rdb-preamble yes
lua-time-limit 5000
slowlog-log-slower-than 10000
slowlog-max-len 128
latency-monitor-threshold 0
notify-keyspace-events ""
hash-max-ziplist-entries 512
hash-max-ziplist-value 64
list-max-ziplist-size -2
list-compress-depth 0
set-max-intset-entries 512
zset-max-ziplist-entries 128
zset-max-ziplist-value 64
hll-sparse-max-bytes 3000
stream-node-max-bytes 4096
stream-node-max-entries 100
activerehashing yes
client-output-buffer-limit normal 0 0 0
client-output-buffer-limit replica 256mb 64mb 60
client-output-buffer-limit pubsub 32mb 8mb 60
hz 10
dynamic-hz yes
aof-rewrite-incremental-fsync yes
rdb-save-incremental-fsync yes
jemalloc-bg-thread yes
```



#### 热点key问题

热卖商品集中到一个分片上，超过但server极限，崩了，进而数据库也崩了。

![面试官：先说说如何发现 Redis 热点 Key，解决方案有哪些？](javaNote.assets/format,png.png)

[面试题](https://blog.51cto.com/lxw1844912514/2942444)

#### redis提供6种数据淘汰策略

redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。

1. volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选**最近最少使用**的数据淘汰

2. volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选**将要过期**的数据淘汰
3. volatile-random：从已设置过期时间的数据集（server.db[i].expires）中**任意选择数据**淘汰
4. allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
5. allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
6. no-enviction（驱逐）：禁止驱逐数据

#### dockercompose.yml

```
version: '3'
services:
  redis:
    image: redis:6.2.6-alpine
    container_name: redis-my
    privileged: true
    volumes:
      - ./data:/data
      - ./conf/redis.conf:/usr/local/etc/redis/redis.conf
    ports:
      - 6379:6379
    #command: redis-server /usr/local/etc/redis/redis.conf
```

#### broken pipe

错误原因：拿到了一个无效的连接

#### 远程连接redis

1. 开放防火墙和安全组6379

2. 修改 reids.conf 配置文件

   ```txt
   1.注释掉绑定ip bind 127.0.0.1   #不注释的话就是默认只允许本地访问
   2.将保护模式改成no    protected-mode no
   3.通过requirepass 设置密码
   ```

## 网络

### 六种基本的网络拓扑结构

![img](javaNote.assets/v2-7815013b9b6381e1ee119bc948db75a8_720w.jpg)

由n个节点构成的星型拓扑结构的网络中，共有 n 个直接连接。
由n个节点构成的环状拓扑结构的网络中，共有 1 个直接的连接，
由n个节点构成的完全型网状结构的网络中，共有 n*(n-1) 个直接的连接。

#### 1、星型拓扑 n-1

n-1 个直接连接

![img](javaNote.assets/v2-c70b1fb3af666e40bf729b4999d1f64d_720w.png)

星型拓扑结构是一个中心，多个分节点。多节点与中央节点通过点到点的方式连接。中央节点执行集中式控制策略，因此中央节点相当复杂，负担比其他各节点重的多。

优点：结构简单，连接方便，管理和维护都相对容易，而且扩展性强。网络延迟时间较小，传输误差低。中心无故障，一般网络没问题。

缺点：中心故障，网络就出问题，同时共享能力差，通信线路利用率不高。

#### 2、环形拓扑 n

n 个直接连接

![img](javaNote.assets/v2-11d24184b0e3dfa6ed1b99146b4c00d6_720w.png)

环形拓扑结构是节点形成一个闭合环。环形网中各节点通过环路接口连在一条首尾相连的闭合环形通信线路中，环上任何节点均可请求发送信息。传输媒体从一个端用户到另一个端用户，直到将所有的端用户连成环型。数据在环路中沿着一个方向在各个节点间传输，信息从一个节点传到另一个节点。

这种结构显而易见消除了端用户通信时对中心系统的依赖性。每个端用户都与两个相临的端用户相连，因而存在着点到点链路，但总是以单向[方式](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E6%96%B9%E5%BC%8F)操作，于是便有上游端用户和下游端用户之称。

优点：信息流在网中是沿着固定方向流动的，两个节点仅有一条道路，简化了路径选择的控制；环路上各节点都是自举控制，控制软件简单。

缺点：信息源在环路中是串行地穿过各个节点，当环中节点过多时，势必影响信息传输速率，使网络的响应时间延长；环路是封闭的，不便于扩充；可靠性低，一个节点故障，将会造成全网瘫痪；维护难，对分支节点故障定位较难。

#### 3、总线型拓扑

![img](javaNote.assets/v2-c04742a365d294fdf8c094f0d8b0596d_720w.png)

总线拓扑结构所有设备连接到一条连接介质上。由一条高速公用总线连接若干个节点所形成的网络即为总线形网络，每个节点上的网络接口板硬件均具有收、发功能，接收器负责接收总线上的串行信息并转换成并行信息送到PC工作站；发送器是将并行信息转换成串行信息后广播发送到总线上，总线上发送信息的目的地址与某节点的接口地址相符合时，该节点的接收器便接收信息。由于各个节点之间通过电缆直接连接，所以总线型拓扑结构中所需要的电缆长度是最小的，但总线只有一定的负载能力，因此总线长度又有一定限制，一条总线只能连接一定数量的节点。

优点：总线结构所需要的电缆数量少，线缆长度短，易于布线和维护。多个节点共用一条传输信道，信道利用率高。

缺点：总线形网常因**一个节点出现故障**（如结头接触不良等）而导致整个网络不通，因此**可靠性不高**。

#### 4、树形拓扑

![img](javaNote.assets/v2-f06f1d8a7898fed878535366c9a3e68b_720w.png)

树形拓扑从总线拓扑演变而来,形状像一棵倒置的树,顶端是树根,树根以下带分支,每个分支还可再带子分支，树根接收各站点发送的数据,然后再广播发送到全网。我国**电话网络即采用树形结构**。

优点：结构比较简单，成本低。在网络中，任意两个节点之间不产生回路，每个链路都支持双向传输。网络中节点扩充方便灵活，寻找链路路经比较方便。

缺点：在这种网络系统中，除叶节点及其相连的链路外，任何一个节点或链路产生的故障都会影响整个网络。

#### 5、网状拓扑 n(n-1)

![img](javaNote.assets/v2-afeeef3ae7ed99ed354b6d16a913235d_720w.png)

主要指各节点通过传输线互联连接起来，并且每一个节点至少与其他两个节点相连。网状拓扑结构具有较高的可靠性，但其结构复杂，实现起来费用较高，不易管理和维护，不常用于局域网。

优点：网络可靠性高，一般通信子网任意两个节点交换机之间，存在着两条或两条以上的通信路径。可扩充性好，网络可建成各种形状，采用多种通信信道，多种传输速率。

缺点：网络结构复杂，成本高，不易维护。

#### 6、混合型拓扑

![img](javaNote.assets/v2-fb9e6442d8e24577eeac8a826c1bf7dd_720w.jpg)

将两种或几种网络拓扑结构混合起来构成的一种网络拓扑结构称为混合型拓扑结构（也有的称之为杂合型结构）。

### 协商缓存和强制缓存

#### 强制缓存

Cache-controller(优先级更高)，相对时间

Expires，绝对时间

强缓存指的是**只要浏览器判断缓存没有过期**，则直接使用浏览器的本地缓存，决定是否使用缓存的主动性在于浏览器这边。

如下图中，返回的是 200 状态码，但在 size 项中标识的是 from disk cache，就是使用了强制缓存。

![img](javaNote.assets/1cb6bc37597e4af8adfef412bfc57a42.png)

#### 协商缓存

Last-Modify 最新修改时间

Etag 资源唯一标识

某些请求的响应码是 `304`，这个是告诉浏览器可以使用本地缓存的资源

第一种：请求头部中的 `If-Modified-Since` 字段与响应头部中的 `Last-Modified` 字段实现

第二种：请求头部中的 `If-None-Match` 字段与响应头部中的 `ETag` 字段

### HTTP2

1、头部压缩

采用hpack算法，具体包括如下

静态编码表：用123替换原来常用header字段,比如method,path

动态编码表：自定义编码表双方进行维护

客户端和服务端动态动态维护字典，用长度较短的索引表示重复字符串，再用哈夫曼算法进行数据压缩

2、二进制帧

将HTTP的文本格式改为二进制数据，极大提高传递效率

帧的结构

首部有长度，标志位（数据结束标志，流的遇险记），流标识符，负载就是实际传输的数据，是经哈夫曼编码的HTTP头部和包体

帧类型

![img](javaNote.assets/帧类型.png)

数据帧就是http头部，包体和流的优先级

控制帧就是心跳，流量控制，流终止等

3、并发传输

HTTP1.1基于请求响应模式，完成一个事务（一次请求响应）才能进行下一个事务，有**队头阻塞**问题，管道只能解决请求的对头阻塞，无法解决响应的队尾阻塞，浏览器默认没有开启

**流**是一个逻辑概念，流包含一个或多个**消息**（对应HTTP请求或响应），一个消息可由一个或多个**帧**组成

多个流复用一个TCP连接，不同流对应的帧可以乱序传输，同个流的帧一定要按序传输

![img](javaNote.assets/stream.png)

4、服务器主动推送资源

### TCP和UDP绑同个端口

https://mp.weixin.qq.com/s/3fMZN_LidCi5fiD16nNWWA

TCP和UDP是**可以同时绑定一个端口**的，只要四元组不同就可以

四元组：源IP,源端口，目标IP,目标端口

可同个reuse参数复用time_wait状态的连接

### DDOS

- **限制半连接队列大小**。多的会丢弃

- SYN-ACK的**重试次数减少**。减少服务端的超时重传



当大量syn请求包发送给服务端的时候，需要设置合理的最大并发半开连接数。一旦超过相应的最大限制，系统就会认为自己收到了syn flood攻击，进入防范模式中。SYN Timeout时间被减短，SYN-ACK的重试次数减少，系统也会自动对缓冲区中的报文进行延时，避免对TCP/IP堆栈造成过大的冲击，力图将攻击危害减到最低。


攻击客户端通过发包器，在短时间内伪造大量不存在的IP地址，向服务器不断地发送SYN包，服务器回复确认包SYN/ACK，并等待客户的确认，由于源地址是不存在的，服务器需要不断的重发SYN/ACK直至超时，这些伪造的SYN包将长时间占用未连接队列，正常的SYN请求被丢弃，目标系统运行缓慢，严重者引起网络堵塞甚至系统瘫痪。

SYN攻击是一个典型的DDOS攻击。检测SYN攻击非常的方便，当你在服务器上看到大量的半连接状态时，特别是源IP地址是随机的，基本上可以断定这是一次SYN攻击。



### RST

TCP的异常终止,一种能够释放TCP连接的机制

```
四种情况会发送RST包：
1、端口未打开
2、请求超时
3、提前关闭
4、在一个已关闭的socket上收到数据
```

### TCP保证可靠传输

#### 校验和

如果接收方比对校验和与发送方不一致，那么数据一定传输有误。但是如果接收方比对校验和与发送方一致，**数据不一定传输成功。**

#### 序列号和确认应答机制

每次收到数据都要进行确认应答，也就是发送ACK报文。这个ACK报文中有对应的确认号，告诉对方期望下次从哪开始发。

数据可通过序列号进行排序，也可去除掉重复序列号的数据。

#### 超时重传

没有收到ACK报文就对刚才的数据进行重新发送

#### 连接管理

三次握手和三次挥手

#### 流量控制

根据窗口大小（接收端的数据缓冲区的大小）改变自己的发送数据速度。

如果窗口为0，停止发送。并定期发送探测数据段（防止接受端告知窗口大小的数据包丢失导致死锁），让接受端告诉自己窗口大小。

#### 拥塞控制

由于不知道网络的情况，一开始就发送大量数据容易导致拥堵，所以引入**慢启动**机制，先发少量数据进行探路。这时候就有**拥塞窗口**的概念，每次收到ACK应答，就指数增长。超过一定阈值后，就线性增长。遇到网络阻塞，就减半。

### 输入URL发生的事

#### 整体组件图

![image-20220521155215885](javaNote.assets/image-20220521155215885.png)



#### DNS查询过程

![image-20220521155359027](javaNote.assets/image-20220521155359027.png)

**DNS记录类型**

![image-20220521155737504](javaNote.assets/image-20220521155737504.png)

**对称加密和非对称加密**

![image-20220521155820739](javaNote.assets/image-20220521155820739.png)



#### 四层负载均衡

vip的概念：也可以保护后端真正的服务器

![image-20220521155907286](javaNote.assets/image-20220521155907286.png)



**调度算法**

![image-20220521155952744](javaNote.assets/image-20220521155952744.png)



**四层负载均衡特点**

![image-20220521160015584](javaNote.assets/image-20220521160015584.png)



#### 七层负载均衡

![image-20220521160037583](javaNote.assets/image-20220521160037583.png)

### CRC

循环冗余校验

生成多项为;G(X)=X^4+X+1.则信息为1101011111的CRC码为（）

```
阶为4，左移4位，按位异或
```

![img](javaNote.assets/969156946_1581908541437_131FA92C75D60B62AFCDCCF2872A039F.jpeg)

### 各层概述

![img](javaNote.assets/3E592997AC0FA3E33F6F75D2B62FF631.png)

![img](javaNote.assets/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6YWS5YmR5LuZYWJj,size_20,color_FFFFFF,t_70,g_se,x_16.png)

![img](javaNote.assets/webp.webp)

#### 应用层

为操作系统或网络应用程序提供访问网络服务的接口，数据传输基本单位报文。

应用网关：应用层的协议转换。例如一个主机ISO电子邮件标准，另一个主机执行的是Internet电子邮件标准，如果这两个主机需要交换电子邮件，那么必须经过一个电子邮件网关进行协议转换。

#### 传输层

将上层数据分段并提供端到端的、可靠或不可靠的传输及端到端的差错控制和流量控制，提供建立、维护和取消连接的功能

网关：协议转换器，充当转换翻译的重任，如果两个网络的通信协议、数据格式或语言不同时，网关会对信息重新打包，以适应目标系统的需求。默认在网络层以上实现网络互联（可用于局域网或广域网）

传输网关：在**两个网络之间建立传输连接**，不同网络的主机之间可跨越多个网络的、级联的、**点对点**的传输连接

#### 网络层

IP寻址和路由选择、分组传输、控制子网运行。

向上提供无连接的、**最大努力的交付**的数据包服务（IP数据报）

**IP地址**有什么用：IP地址通过ARP协议转为MAC地址，最终按照硬件地址找到主机的，那为什么不直接使用MAC地址，主要是**屏蔽**下层异构网络

**IP分组转发算法**

(1)在数据报首部提取目标IP地址D，得出网络地址N.

(2)如果是本网络直接交付（封装成MAC帧）,或根据路由表传给下一跳路由器，或交给默认路由器

**ARP地址解析协议**

保存**IP地址**到**硬件地址**的映射表，并且会动态更新，ARP高速缓存表初始化的时候采用广播的方式

**路由选择协议**

路由选择分为内部网关协议（自治系统AS）和外部网关协议，内部网关协议有RIP和OSPF协议，外部网关协议有BGP协议。

RIP协议（适合小网络）：路由信息协议，基于距离向量，最短跳数16视为不可达，比如（1，3，R）表示到达网络1的跳数为3，下一个路由是R.好消息传得快，坏消息传得慢。

OSPF协议（适合大网络）：开放最短路径优先协议，基于**Dijkstra的最短路径**算法，坏消息能够快速收敛。划分为小的区域进行洪泛，直接使用IP数据包传送。

BGP协议：边界网关协议，域间路由协议，互联网的规模很大，自治系统之间的路由选择非常困难。另外一些数据报为了安全不能通过国外的网络。基于路径向量选择协议，每个自治系统之间保证要有一个BGP代言人。

路由器：连接多个逻辑分开的网络，根据IP地址区分不同的网络，实现网路的互连和隔离，把IP报文传送到正确的网络。

#### 链路层

帧的开始和结束、透明传输、差错校验

网桥：连接两个局域网，根据MAC地址转发帧

交换机：更多端口的网桥，根据帧的目标MAC地址对照MAC地址表决定由哪个端口转发，不在表中则向所有端口转发，及洪泛

#### 物理层

接口标准、如何更快的传输数据

中继器：放大信号

集线器：多个端口的集线器

### DNS域名解析

主要是使用UDP协议,默认端口53

主DNS服务器和辅助DNS服务器之间使用TCP协议，

1. 辅域名服务器会定时（一般时3小时）向主域名服务器进行查询以便了解数据是否有变动。如有变动，则会执行一次区域传送，进行数据同步。区域传送将使用TCP而不是UDP，因为数据同步传送的数据量比一个请求和应答的数据量要多得多。 
2. TCP是一种可靠的连接，保证了数据的准确性。 

浏览器首先看一下自己的缓存里有没有，如果没有就向操作系统的缓存要，还没有就检查本机域名解析文件 `hosts`，如果还是没有，就会 DNS 服务器进行查询，查询的过程如下：

1. 客户端首先会发出一个 DNS 请求，问 www.server.com 的 IP 是啥，并发给本地 DNS 服务器（也就是客户端的 TCP/IP 设置中填写的 DNS 服务器地址）。
2. 本地域名服务器收到客户端的请求后，如果缓存里的表格能找到 www.server.com，则它直接返回 IP 地址。如果没有，本地 DNS 会去问它的根域名服务器：“老大， 能告诉我 www.server.com 的 IP 地址吗？” 根域名服务器是最高层次的，它不直接用于域名解析，但能指明一条道路。
3. 根 DNS 收到来自本地 DNS 的请求后，发现后置是 .com，说：“www.server.com 这个域名归 .com 区域管理”，我给你 .com 顶级域名服务器地址给你，你去问问它吧。”
4. 本地 DNS 收到顶级域名服务器的地址后，发起请求问“老二， 你能告诉我 www.server.com 的 IP 地址吗？”
5. 顶级域名服务器说：“我给你负责 www.server.com 区域的权威 DNS 服务器的地址，你去问它应该能问到”。
6. 本地 DNS 于是转向问权威 DNS 服务器：“老三，www.server.com对应的IP是啥呀？” server.com 的权威 DNS 服务器，它是域名解析结果的原出处。为啥叫权威呢？就是我的域名我做主。
7. 权威 DNS 服务器查询后将对应的 IP 地址 X.X.X.X 告诉本地 DNS。
8. 本地 DNS 再将 IP 地址返回客户端，客户端和目标建立连接。

![域名解析的工作流程](javaNote.assets/33.jpg)

### Ping命令

应用可能用到**DNS**，域名解析服务
网络层**ICMP**协议和**ARP**地址解析协议

### NAT协议

```
将内部网络的私有IP地址翻译成全球唯一的公网IP地址，使内部网络可以连接到互联网上

SNAT:内部地址要访问公网上的服务时，内部地址会主动发起连接，将内部地址转换成公有ip。网关这个地址转换称为SNAT.
DNAT:当内部需要对外提供服务时，外部发起主动连接，路由器或着***的网关接收到这个连接，然后把连接转换到内部，此过程是由带公有ip的网关代替内部服务来接收外部的连接，然后在内部做地址转换，此转换称为DNAT
```

### DHCP协议

动态主机配置协议，局域网网络协议，可自动分配IP地址

### RARP协议

运行局域网的物理机器从网关服务器的ARP表或缓存上请求其IP地址

### 滑动窗口协议

![image-20220911104809067](javaNote.assets/image-20220911104809067.png)

停止等待、退后N帧，选择重传

因此TCP有队头阻塞问题

https://blog.csdn.net/qq_47529104/article/details/123362159

![这里写图片描述](javaNote.assets/20160418155442777.png)

1.发送端和接收端分别设定发送窗口和接收窗口。
2.三次握手的时候，客户端把自己的缓冲区大小也就是窗口大小发送给服务器，服务器回应是也将窗口大小发送给客户端，服务器客户端都知道了彼此的窗口大小。
3.比如主机A的发送窗口大小为5，主机A可以向主机B发送5个单元，如果B缓冲区满了，A就要等待B确认才能继续发送数据。
4.如果缓冲区中有1个报文被进程读取，主机B就会回复ACK给主机A，接收窗口向前滑动，报文中窗口大小为1，就说明A还可以发送1个单元的数据，发送窗口向前滑动，之后等待主机B的确认报文。
只有接收窗口向前滑动并发送了确认时，发送窗口才能向前滑动。

[博客](https://blog.csdn.net/qq_34501940/article/details/51180268)

**停止等待协议**

- 一个好了才能发送下一个，降低信号的利用率

- 发送窗口=1，接受窗口=1

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATWxsbGxr,size_20,color_FFFFFF,t_70,g_se,x_16.png)

**退后N帧协议**

- 一个接受不到，改帧以后都重传，网络不好的时候会造成大量浪费带宽

- 发送>1,接收=1

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATWxsbGxr,size_20,color_FFFFFF,t_70,g_se,x_16-16583942520383.png)

**选择重传**协议

- 一个帧坏了，后面的还会缓存起来，只重传丢失的那一个，会浪费缓存

- 发送>1,接收>1

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATWxsbGxr,size_20,color_FFFFFF,t_70,g_se,x_16-16583942635955.png)

### TCP和HTTP的联系和区别

TCP是传输层的协议，HTTP是应用层协议，HTTP基于TCP协议。HTTP协议只关心约定协议内容，只关心让对方能懂。TCP有发送确认机制，只关心点对点传输，保证消息可靠传输。具体有三次握手，四次挥手机制

### TCP如何保证可靠传输

检验和

连接管理

序列号

确认应答机制

超时重传

流量控制

拥塞控制：慢开始，拥塞避免，快重传，快恢复

```
1、慢开始：少量数据进行试探
2、拥塞避免：指数增长，达到阈值后，加法增长
个别报文段在网络中丢失，但实际网络并未丢失。为避免发送方得不到确认产生超时，误以为发生拥塞于是进行慢开始，导致降低网络的传输效率。
3、快重传：当发送方收到重复的M2确认会快速重传M3
4、快恢复：不采用慢开始，而只将门限值设为拥塞窗口减半，并把拥塞窗口设为门限值
```

### unix五种IO模型

IO分为两个阶段：数据准备和数据拷贝

数据准备：设备到内核

数据拷贝：内核拷贝到用户空间

https://blog.csdn.net/qq_35361244/article/details/109251983

```
阻塞io：数据准备和数据拷贝阶段都阻塞

非阻塞io：数据准备阶段不阻塞，轮询数据是否准备好，耗cpu

多路复用io：适合多连接，只用一个线程在select轮询内核socket状态，

信号io:发送io请求就到socker注册一个信号，内核数据报准备好发送信号通知用户线程

异步io：数据主备和数据复制都交给内核完成，真正非阻塞
```

#### 1、阻塞式I/O

等待数据和拷贝数据都等待

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzYxMjQ0,size_16,color_FFFFFF,t_70#pic_center.png)

#### 2、非阻塞式I/O

不断**系统调用**询问数据是否准备好，即在数据准备阶段不会阻塞

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzYxMjQ0,size_16,color_FFFFFF,t_70#pic_center-16510400903116.png)

#### 3、I/O复用

[select,poll,epoll](https://blog.csdn.net/wteruiycbqqvwt/article/details/90299610)

##### select/poll

需要进行 **2 次「遍历」文件描述符集合**，一次是在内核态里，一个次是在用户态里 ，而且还会发生 **2 次「拷贝」文件描述符集合**，先从用户空间传入内核空间，由内核修改后，再传出到用户空间中

O(n) 遍历,BitsMap存储,
poll采用链表，因此无连接数限制

##### epoll

维护了红黑树，时间驱动机制，通过回调加入到就绪列表中，返回就绪的socket列表

*第一点*，epoll 在内核里使用**红黑树来跟踪进程所有待检测的文件描述字**，把需要监控的 socket 通过 `epoll_ctl()` 函数加入内核中的红黑树里，红黑树是个高效的数据结构，增删改一般时间复杂度是 `O(logn)`。而 select/poll 内核里没有类似 epoll 红黑树这种保存所有待检测的 socket 的数据结构，所以 select/poll 每次操作时都传入整个 socket 集合给内核，而 epoll 因为在内核维护了红黑树，可以保存所有待检测的 socket ，所以只需要传入一个待检测的 socket，减少了内核和用户空间大量的数据拷贝和内存分配。

*第二点*， epoll 使用**事件驱动**的机制，内核里**维护了一个链表来记录就绪事件**，当某个 socket 有事件发生时，通过**回调函数**内核会将其加入到这个就绪事件列表中，当用户调用 `epoll_wait()` 函数时，只会返回有事件发生的文件描述符的个数，不需要像 select/poll 那样轮询扫描整个 socket 集合，大大提高了检测的效率。

O(1) 事件驱动IO

![img](javaNote.assets/epoll.png)

epoll 的方式即使监听的 Socket 数量越多的时候，效率不会大幅度降低，能够同时监听的 Socket 的数目也非常的多了，上限就为系统定义的进程打开的最大文件描述符个数。



**边缘触发和水平触发**

边缘触发（效率更高）：只触发一次，一般配合nio使用

水平触发：不断从epoll_wait 中苏醒，直到内核缓冲区数据读完

- 使用边缘触发模式时，当被监控的 Socket 描述符上有可读事件发生时，**服务器端只会从 epoll_wait 中苏醒一次**，即使进程没有调用 read 函数从内核读取数据，也依然只苏醒一次，因此我们程序要保证一次性将内核缓冲区的数据读取完；
- 使用水平触发模式时，当被监控的 Socket 上有可读事件发生时，**服务器端不断地从 epoll_wait 中苏醒，直到内核缓冲区数据被 read 函数读完才结束**，目的是告诉我们有数据需要读取；

**select**阻塞调用线程，直到一个或多个数据包准备就绪，然后系统调用（**recvfrom**）拷贝数据

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzYxMjQ0,size_16,color_FFFFFF,t_70#pic_center-16510403144768.png)

#### 4、信号驱动I/O

调用**sigio**函数，不阻塞执行其它任务，内核数据包准备就绪发送就绪信号，进程收到通知后调用**recvfrom**函数，拷贝数据到缓冲区

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201024104641126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzYxMjQ0,size_16,color_FFFFFF,t_70#pic_center)

#### 5、异步I/O

不阻塞，并且所有任务都交给内核处理（数据准备和数据拷贝），全部准备好了再通知线程处理数据报，真正做到非阻塞。

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzYxMjQ0,size_16,color_FFFFFF,t_70#pic_center-165104086875711.png)

下面这张图，总结了以上几种 I/O 模型：

![img](javaNote.assets/同步VS异步IO.png)

在前面我们知道了，I/O 是分为两个过程的：

1. 数据准备的过程
2. 数据从内核空间拷贝到用户进程缓冲区的过程

阻塞 I/O 会阻塞在「过程 1 」和「过程 2」，而非阻塞 I/O 和基于非阻塞 I/O 的多路复用只会阻塞在「过程 2」，所以这三个都可以认为是同步 I/O。

异步 I/O 则不同，「过程 1 」和「过程 2 」都不会阻塞。

### STOMP协议

```java
package com.wzh.demo.websocket.config;

import com.wzh.demo.websocket.handler.MyPrincipalHandshakeHandler;
import com.wzh.demo.websocket.interceptor.WebSocketChannelInterceptor;
import com.wzh.demo.websocket.interceptor.WebSocketHandshakeInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.messaging.converter.MessageConverter;
import org.springframework.messaging.handler.invocation.HandlerMethodArgumentResolver;
import org.springframework.messaging.handler.invocation.HandlerMethodReturnValueHandler;
import org.springframework.messaging.simp.config.ChannelRegistration;
import org.springframework.messaging.simp.config.MessageBrokerRegistry;
import org.springframework.scheduling.concurrent.DefaultManagedTaskScheduler;
import org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler;
import org.springframework.util.AntPathMatcher;
import org.springframework.web.socket.config.annotation.EnableWebSocketMessageBroker;
import org.springframework.web.socket.config.annotation.StompEndpointRegistry;
import org.springframework.web.socket.config.annotation.WebSocketMessageBrokerConfigurer;
import org.springframework.web.socket.config.annotation.WebSocketTransportRegistration;

import java.util.List;

/**
 * <配置基于STOMP的websocket>
 * <功能详细描述>
 * @author wzh
 * @version 2018-08-12 18:38
 * @see [相关类/方法] (可选)
 **/
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketStompConfig implements WebSocketMessageBrokerConfigurer {

    /**
     * 添加这个Endpoint，这样在网页中就可以通过websocket连接上服务,
     * 也就是我们配置websocket的服务地址,并且可以指定是否使用socketjs
     * 
     * @param registry
     */
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry)
    {
        
        /*
         * 1. 将 /serviceName/stomp/websocketJs路径注册为STOMP的端点，
         *    用户连接了这个端点后就可以进行websocket通讯，支持socketJs
         * 2. setAllowedOrigins("*")表示可以跨域
         * 3. withSockJS()表示支持socktJS访问
         * 4. addInterceptors 添加自定义拦截器，这个拦截器是上一个demo自己定义的获取httpsession的拦截器
         * 5. addInterceptors 添加拦截处理，这里MyPrincipalHandshakeHandler 封装的认证用户信息
         */
        registry.addEndpoint("/stomp/websocketJS")
                //.setAllowedOrigins("*")
                .addInterceptors(new WebSocketHandshakeInterceptor())
                .setHandshakeHandler(new MyPrincipalHandshakeHandler())
                .withSockJS()

        ;

        /*
         * 看了下源码，它的实现类是WebMvcStompEndpointRegistry ，
         * addEndpoint是添加到WebMvcStompWebSocketEndpointRegistration的集合中，
         * 所以可以添加多个端点
         */
        registry.addEndpoint("/stomp/websocket");
    }

    /**
     * 配置消息代理
     * @param registry
     */
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry)
    {
        /*
         *  enableStompBrokerRelay 配置外部的STOMP服务，需要安装额外的支持 比如rabbitmq或activemq
         * 1. 配置代理域，可以配置多个，此段代码配置代理目的地的前缀为 /topicTest 或者 /userTest
         *    我们就可以在配置的域上向客户端推送消息
         * 3. 可以通过 setRelayHost 配置代理监听的host,默认为localhost
         * 4. 可以通过 setRelayPort 配置代理监听的端口，默认为61613
         * 5. 可以通过 setClientLogin 和 setClientPasscode 配置账号和密码
         * 6. setxxx这种设置方法是可选的，根据业务需要自行配置，也可以使用默认配置
         */
        //registry.enableStompBrokerRelay("/topicTest","/userTest")
                //.setRelayHost("rabbit.someotherserver")
                //.setRelayPort(62623);
                //.setClientLogin("userName")
                //.setClientPasscode("password")
                //;

        // 自定义调度器，用于控制心跳线程
        ThreadPoolTaskScheduler taskScheduler = new ThreadPoolTaskScheduler();
        // 线程池线程数，心跳连接开线程
        taskScheduler.setPoolSize(1);
        // 线程名前缀
        taskScheduler.setThreadNamePrefix("websocket-heartbeat-thread-");
        // 初始化
        taskScheduler.initialize();

        /*
         * spring 内置broker对象
         * 1. 配置代理域，可以配置多个，此段代码配置代理目的地的前缀为 /topicTest 或者 /userTest
         *    我们就可以在配置的域上向客户端推送消息
         * 2，进行心跳设置，第一值表示server最小能保证发的心跳间隔毫秒数, 第二个值代码server希望client发的心跳间隔毫秒数
         * 3. 可以配置心跳线程调度器 setHeartbeatValue这个不能单独设置，不然不起作用，要配合setTaskScheduler才可以生效
         *    调度器我们可以自己写一个，也可以自己使用默认的调度器 new DefaultManagedTaskScheduler()
         */
        registry.enableSimpleBroker("/topicTest","/userTest")
                .setHeartbeatValue(new long[]{10000,10000})
                .setTaskScheduler(taskScheduler);
        /*
         *  "/app" 为配置应用服务器的地址前缀，表示所有以/app 开头的客户端消息或请求
         *  都会路由到带有@MessageMapping 注解的方法中
         */
        registry.setApplicationDestinationPrefixes("/app");

        /*
         *  1. 配置一对一消息前缀， 客户端接收一对一消息需要配置的前缀 如“'/user/'+userid + '/message'”，
         *     是客户端订阅一对一消息的地址 stompClient.subscribe js方法调用的地址
         *  2. 使用@SendToUser发送私信的规则不是这个参数设定，在框架内部是用UserDestinationMessageHandler处理，
         *     而不是而不是 AnnotationMethodMessageHandler 或  SimpleBrokerMessageHandler
         *     or StompBrokerRelayMessageHandler，是在@SendToUser的URL前加“user+sessionId"组成
         */
        registry.setUserDestinationPrefix("/user");

        /*
         * 自定义路径分割符
         * 注释掉的这段代码添加的分割符为. 分割是类级别的@messageMapping和方法级别的@messageMapping的路径
         * 例如类注解路径为 “topic”,方法注解路径为“hello”，那么客户端JS stompClient.send 方法调用的路径为“/app/topic.hello”
         * 注释掉此段代码后，类注解路径“/topic”,方法注解路径“/hello”,JS调用的路径为“/app/topic/hello”
         */
        //registry.setPathMatcher(new AntPathMatcher("."));

    }

    /**
     * 配置发送与接收的消息参数，可以指定消息字节大小，缓存大小，发送超时时间
     * @param registration
     */
    @Override
    public void configureWebSocketTransport(WebSocketTransportRegistration registration) {
        /*
         * 1. setMessageSizeLimit 设置消息缓存的字节数大小 字节
         * 2. setSendBufferSizeLimit 设置websocket会话时，缓存的大小 字节
         * 3. setSendTimeLimit 设置消息发送会话超时时间，毫秒
         */
        registration.setMessageSizeLimit(10240)
                    .setSendBufferSizeLimit(10240)
                    .setSendTimeLimit(10000);
    }

    /**
     * 设置输入消息通道的线程数，默认线程为1，可以自己自定义线程数，最大线程数，线程存活时间
     * @param registration
     */
    @Override
    public void configureClientInboundChannel(ChannelRegistration registration) {

        /*
         * 配置消息线程池
         * 1. corePoolSize 配置核心线程池，当线程数小于此配置时，不管线程中有无空闲的线程，都会产生新线程处理任务
         * 2. maxPoolSize 配置线程池最大数，当线程池数等于此配置时，不会产生新线程
         * 3. keepAliveSeconds 线程池维护线程所允许的空闲时间，单位秒
         */
        registration.taskExecutor().corePoolSize(10)
                    .maxPoolSize(20)
                    .keepAliveSeconds(60);
        /*
         * 添加stomp自定义拦截器，可以根据业务做一些处理
         * springframework 4.3.12 之后版本此方法废弃，代替方法 interceptors(ChannelInterceptor... interceptors)
         * 消息拦截器，实现ChannelInterceptor接口
         */
        registration.setInterceptors(webSocketChannelInterceptor());
    }

    /**
     *设置输出消息通道的线程数，默认线程为1，可以自己自定义线程数，最大线程数，线程存活时间
     * @param registration
     */
    @Override
    public void configureClientOutboundChannel(ChannelRegistration registration) {
        registration.taskExecutor().corePoolSize(10)
                    .maxPoolSize(20)
                    .keepAliveSeconds(60);
        //registration.setInterceptors(new WebSocketChannelInterceptor());
    }

    /**
     * 添加自定义的消息转换器，spring 提供多种默认的消息转换器，
     * 返回false,不会添加消息转换器，返回true，会添加默认的消息转换器，当然也可以把自己写的消息转换器添加到转换链中
     * @param list
     * @return
     */
    @Override
    public boolean configureMessageConverters(List<MessageConverter> list) {
        return true;
    }

    /**
     * 自定义控制器方法的参数类型，有兴趣可以百度google HandlerMethodArgumentResolver这个的用法
     * @param list
     */
    @Override
    public void addArgumentResolvers(List<HandlerMethodArgumentResolver> list) {

    }

    /**
     * 自定义控制器方法返回值类型，有兴趣可以百度google HandlerMethodReturnValueHandler这个的用法
     * @param list
     */
    @Override
    public void addReturnValueHandlers(List<HandlerMethodReturnValueHandler> list) {

    }

    /**
     * 拦截器加入 spring ioc容器
     * @return
     */
    @Bean
    public WebSocketChannelInterceptor webSocketChannelInterceptor()
    {
        return new WebSocketChannelInterceptor();
    }

}


```



### HTTP常见方法和状态码

#### 5个常用Method

get 从服务器端获取资源

put 提交资源

post 更新资源

delete 删除资源

connect 建立tunnel隧道

#### **状态码分类表**

​          类别                    								原因短句

1xx	Informational（信息性状态码）	接受的请求正在处理
2xx	Success（成功状态码）	  			请求正常处理完毕
3xx	Redirection（重定向）					需要进行附加操作以完成请求
4xx	Client error（客户端错误）			客户端请求出错，服务器无法处理请求
5xx	Server Error（服务器错误）			服务器处理请求出错

#### **各类别常见状态码：**

```
301 永久重定向
302 临时重定向
304 not modify未修改


2xx （3种）

200 OK：表示从客户端发送给服务器的请求被正常处理并返回；

204 No Content：表示客户端发送给客户端的请求得到了成功处理，但在返回的响应报文中不含实体的主体部分（没有资源可以返回）；

206 Patial Content：表示客户端进行了范围请求，并且服务器成功执行了这部分的GET请求，响应报文中包含由Content-Range指定范围的实体内容。

3xx （5种）

301 Moved Permanently：永久性重定向，表示请求的资源被分配了新的URL，之后应使用更改的URL；

302 Found：临时性重定向，表示请求的资源被分配了新的URL，希望本次访问使用新的URL；

       301与302的区别：前者是永久移动，后者是临时移动（之后可能还会更改URL）

303 See Other：表示请求的资源被分配了新的URL，应使用GET方法定向获取请求的资源；

      302与303的区别：后者明确表示客户端应当采用GET方式获取资源

304 Not Modified：表示客户端发送附带条件（是指采用GET方法的请求报文中包含if-Match、If-Modified-Since、If-None-Match、If-Range、If-Unmodified-Since中任一首部）的请求时，服务器端允许访问资源，但是请求为满足条件的情况下返回改状态码；

307 Temporary Redirect：临时重定向，与303有着相同的含义，307会遵照浏览器标准不会从POST变成GET；（不同浏览器可能会出现不同的情况）；

4xx （4种）

400 Bad Request：表示请求报文中存在语法错误；

401 Unauthorized：未经许可，需要通过HTTP认证；

403 Forbidden：服务器拒绝该次访问（访问权限出现问题）

404 Not Found：表示服务器上无法找到请求的资源，除此之外，也可以在服务器拒绝请求但不想给拒绝原因时使用；
405 请求方式不对

5xx （2种）

500 Inter Server Error：表示服务器在执行请求时发生了错误，也有可能是web应用存在的bug或某些临时的错误时；

503 Server Unavailable：表示服务器暂时处于超负载或正在进行停机维护，无法处理请求；
```

### Https

用非对称加密的方式协商对称密匙

![img](javaNote.assets/458D639F0DE2FDB51585834A999C051C.png)

#### http&https区别

https是http加上ssl的应用层协议。在http的基础上增加了安全性和可靠性。

端口的不同：http默认是80端口， https默认是443端口

安全性：http是明文传输，https是密文传输。

认证：http没有认证，https是先进行TCP连接，再进行SSL层的握手，在这个过程中需要认证。

成本上：https的证书需要成本，同时加密和解密时对CPU和内存开销增加。

#### 一、四次握手过程

https通信时，首先建立ssl层的连接，客户端将ssl版本号和加密组件发到客户端，客户端收到后对ssl版本号和加密组件进行匹配，同时将CA证书及密钥发送到客户端。客户端对证书进行验证，验证通过后使用非对称加密对数据通信时的密钥进行协商。协商后得到一致的获得一致的对称加密密钥。然后使用对称加密算法进行

1、客户端发送TLS版本，client随机数和支持的密码套件列表（密匙交换算法--签名算法--对称加密算法--摘要算法）

2、服务端发送TLS版本，server随机数，选择的密码套件和数字证书

3、验证证书的安全性并得到服务器RSA公匙，生称新的新的随机数（pre-master）并用RSA公匙加密发给服务端。服务收到后用RSA解密得到pre-master。

至此双方都共享了三个随机数：客户端随机数，服务端随机数，pre-master，用于生成会话密匙，他就是对称密匙。

然后客户端就把之前发送的所有数据做个摘要，使用会话密匙加密让服务器验证一下消息是否又被篡改。

4、服务器也是同样的操作，双方都验证加密和解密没问题，握手正式完成



TLS四次握手过程

![img](javaNote.assets/B7268EF66524898CEF0E068EA5F1BA26.gif)

#### 二、数字证书签发和验证流程

CA 签发证书的过程，如上图左边部分：

- 首先 CA 会把持有者的公钥、用途、颁发者、有效时间等信息打成一个包，然后对这些信息进行 Hash 计算，得到一个 Hash 值；
- 然后 CA 会使用自己的私钥将该 Hash 值加密，生成 Certificate Signature，也就是 CA 对证书做了签名；
- 最后将 Certificate Signature 添加在文件证书上，形成数字证书；

客户端校验服务端的数字证书的过程，如上图右边部分：

- 首先客户端会使用同样的 Hash 算法获取该证书的 Hash 值 H1；
- 通常浏览器和操作系统中集成了 CA 的公钥信息，浏览器收到证书后可以使用 CA 的公钥解密 Certificate Signature 内容，得到一个 Hash 值 H2 ；
- 最后比较 H1 和 H2，如果值相同，则为可信赖的证书，否则则认为证书不可信。

![img](javaNote.assets/证书的校验.png)

#### 证书链

证书信任链

开始客户端只信任根证书 GlobalSign Root CA 证书的，然后 “GlobalSign Root CA” 证书信任 “GlobalSign Organization Validation CA - SHA256 - G2” 证书，而 “GlobalSign Organization Validation CA - SHA256 - G2” 证书又信任 baidu.com 证书，于是客户端也信任 baidu.com 证书。

![img](javaNote.assets/用户信任.png)

### RSA的公钥、私钥

采用单钥[密码系统](https://baike.baidu.com/item/密码系统)的加密方法，同一个[密钥](https://baike.baidu.com/item/密钥)可以同时用作信息的加密和解密，这种加密方法称为对称加密，也称为单[密钥加密](https://baike.baidu.com/item/密钥加密)。

与对称加密[算法](https://baike.baidu.com/item/算法)不同，[非对称加密算法](https://baike.baidu.com/item/非对称加密算法)需要两个[密钥](https://baike.baidu.com/item/密钥)：[公开密钥](https://baike.baidu.com/item/公开密钥)（publickey）和私有密钥（privatekey）。[公开密钥](https://baike.baidu.com/item/公开密钥)与私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。因为加密和解密使用的是两个不同的[密钥](https://baike.baidu.com/item/密钥)，所以这种算法叫作[非对称加密算法](https://baike.baidu.com/item/非对称加密算法)。

一、举个例子

1、发消息

  用对方的公钥给对方发消息

![img](https:////upload-images.jianshu.io/upload_images/5192115-dfd9bdfcd51d377b.png?imageMogr2/auto-orient/strip|imageView2/2/w/647/format/webp)

2、发公告

 发公告的时候，用自己的私钥形成签名！

![img](https:////upload-images.jianshu.io/upload_images/5192115-3ee4f762e9878eee.png?imageMogr2/auto-orient/strip|imageView2/2/w/672/format/webp)

#### 二、加密和签名

RSA的公钥、私钥是互相对应的，RSA会生成两个密钥，你可以把任何一个用于公钥，然后另一个就是你必须保护好的私钥了。

RSA的公钥、私钥都可以加密，也都可以解密。

其中：

用公钥加密需要私钥解密，称为“加密”。由于私钥是不公开的，确保了内容的保密，没有私钥无法获得内容；

用私钥加密需要公钥解密，称为“签名”。由于公钥是公开的，任何人都可以解密内容，但只能用发布者的公钥解密，验证了内容是该发布者发出的。

所以：

如果用于加密解密，那就是用公钥加密私钥解密（仅你可读但别人不可读，任何人都可写）

如果用于证书验证，那就是用私钥加密公钥解密（仅你可写但别人不可写，任何人都可读）

#### 三、认证过程

![img](https:////upload-images.jianshu.io/upload_images/5192115-35fbd540dd37f0f4.png?imageMogr2/auto-orient/strip|imageView2/2/w/671/format/webp)

#### jwt的签名算法有三种：

- HMAC【哈希消息验证码(对称)】：HS256/HS384/HS512
- RSASSA【RSA签名算法(非对称)】（RS256/RS384/RS512）
- ECDSA【椭圆曲线数据签名算法(非对称)】（ES256/ES384/ES512）

### TCP三次握手和四次挥手

TCP三次握手**TCP运输连接有三个阶段：连接建立、数据传送、连接释放**

TCP连接过程通常叫做**握手**，握手需要客户端和服务器端交换三个报文，如下图所示

之所以需要三次握手是因为TCP是可靠传输，三次能够刚好可靠又不多余

TCP三次握手与Socket的连接过程是相关联对应的，Socket就是对于TCP/IP的封装么

客户端有CLOSED、SYN-SEND、ESTABLISHED三种状态

客户端有CLOSED、LISTEN、SYN-RCVD、ESTABLISHED四种状态

服务器会首先创建连接，并且进入监听等待阶段，等待客户端的请求

当需要发送请求时，浏览器客户端主动打开连接，然后服务器被动打开连接![img](javaNote.assets/8309948_1566974042905_FC5D1E4A8542CB51426DC924E8578CD5.png)

#### 连接过程

#### TCP三次握手

客户端在需要时，向服务器发起请求连接报文，发出后状态从CLOSED转换为SYN-SEND 同步-已发送状态

服务器一直处于LISTEN状态，接收到请求后，对客户端的请求进行回应，转换为SYN-RCVD，同步-已收到状态

客户端收到服务器的回应后，状态转换为ESTABLISHED，并且再次向服务器发送确认

服务器收到客户端的确认之后，服务器也转换为ESTABLISHED状态，完成了连接

**发出消息或者收到消息后状态才会进行切换**

客户端与服务器的握手是一个往复确认的过程

客户端：发出确认请求，SYN=1，seq=x，你听得到么，我想建立连接（SYN=1），我的序号是x（seq=x）

服务器：对请求进行确认，也就是回应，我听到了（ACK=1，ack=x+1），你听得到么（SYN=1），我的序号是y（seq=y）

客户端：对服务器的回应进行确认，我听到了（ACK=1，ack=y+1），我的序号是x+1

IP数据报经过运输层需要分段发送，所以在TCP的处理过程中，有**序号**的概念

比如客户端说我要从666号开始，发送100个数据，服务器说，我是从888号开始回应的

上面的seq=x 和 seq=y  seq=x+1（上一个seq=x，下一个自然就是seq=x+1了）都是各自的序号**握手的过程就是SYN seq  ACK ack的来回确认**

SYN ACK是头部的字段，可以理解为标志位，协议中有对他们的值有具体的规定

ack就是确认号，确认号是期望收到的对方的下一个报文段的第一个数据字节的序号，也就是收到的序号+1

否则随便一个，怎么对得上号

#### 为什么要三次握手？

如果不是三次握手，只有两次

如果客户端发出请求连接时，报文延时了，于是客户端重新发送了一次连接请求消息

后来收到了确认，建立了连接，然后完成了数据传输，关闭了连接

此时，服务器收到了那个迟到的请求消息，此时他应该是个废物了

但是如果只有两次握手，服务器收到请求就响应建立了连接了

但是如果是三次，客户端不会再次确认，服务器也就随后知道了这消息有问题，不会建立连接

#### TCP四次挥手

连接建立以后就可以进行数据通信传输了

通信结束后，需要断开连接，断开连接需要四次交互，常被称为**四次挥手**

**最初状态均为ESTABLISHED**，客户端与服务器相互进行数据传送

下图假设客户端无数据发送，请求断开连接![img](javaNote.assets/8309948_1566974066111_035082E832E529B2DFF7F11FE4D076A4.png)

断开过程客户端无数据发送时，请求关闭连接，我好了，我想断开连接了（FIN=1）我的序号是u（u就是之前传送过的所有数据的最后一个字节的序号+1）

此时客户端转变为FIN-WAIT-1状态

服务器收到客户端的消息后，告诉客户端“好的，我知道了”（ACK=1，ack=u+1），这条消息的序号是v（seq=v ，这是服务器发送消息的序号)

此时服务器的状态就转换为了CLOSE-WAIT状态

此时，客户端通往服务器的路就断开了，客户端不能向服务器发送数据但是服务器仍旧可以向客户端发送数据，现在是“半关闭”的状态

当客户端收到来自服务器的确认之后，进入FIN-WAIT-2状态，等待服务器那边说断开连接，等待中。。。。。

当服务器所有的数据也都完全发送完成了之后，服务器才开始主动告知客户端断开连接（FIN=1，seq=w）

这中间服务器可能又继续发送了一些数据，可能是v+1 也可能发送了更多，所以设置为w

并且再次发送确认信息（ACK=1，ack=u+1，因为客户端已经不能发送数据了，服务器期望收到的序号永远都是最后一个序号+1，也就是u+1）

这时，服务器就进入了LAST-ACK状态，最后确认状态

客户端收到了服务器的断开连接请求后，也需要给出确认响应（ACK=1，ack=w+1，seq=u+1），然后进入TIME-WAIT状态

等待两个MSL后，进入关闭状态

MSL 是Maximum Segment Lifetime英文的缩写“报文最大生存时间”，他是任何报文在网络上存在的最长时间，超过这个时间报文将被丢弃。服务器最终收到来自客户端的确认信息后，关闭，进入CLOSED状态

**四次挥手也是一个互相确认的过程，你说不玩了，别人答应了，还要等别人都搞好了再告诉你可以走了，你才能走**

客户端：我不想玩了

服务器：好的我知道了

服务器：你可以走了

客户端：好的我走了

就如同在网吧上网，你点击下机之后，再去网管那边结账

结账清楚了之后才彻底结束，而不是你说走就走了，难道你办会员卡了么

这个过程很好理解，**客户端发出请求后，并不意味着服务器都已经完成响应****所以当客户端请求断开时，并不能立即断开，还需要等待服务器那边处理妥当，再来通知你的确是可以断开了

消息发出来谁知道别人收没收到，所以还需要一个确认

### TIME_WAIT

#### 为什么等待2MSL

msl:（报文最大存活时间）

1. 服务器等待ACK时间+超时重传时间就是2MSL，确保服务器接收ACK报文并正常关闭，**释放资源**。

2. 避免历史连接中的数据**被客户端**相同的四元组接收。服务端以相同的四元组重新打开了新连接，前面被延迟的 `SEQ = 301` 这时抵达了客户端，而且该数据报文的序列号刚好在客户端接收窗口内，因此客户端会正常接收这个数据报文，但是这个数据报文是上一个连接残留下来的，这样就产生数据错乱等严重的问题

#### TIME_WAIT 危害

- 第一是占用**系统资源，比如文件描述符**、内存资源、CPU 资源、线程资源等；
- 第二是**占用端口资源**，端口资源也是有限的，一般可以开启的端口为 `32768～61000`，也可以通过 `net.ipv4.ip_local_port_range`参数指定范围。

#### 优化

- 打开 net.ipv4.tcp_tw_reuse 和 net.ipv4.tcp_timestamps 选项；**重用tw状态的socket**
- net.ipv4.tcp_max_tw_buckets.过这个值时，系统就会将后面的 TIME_WAIT 连接状态**重置**
- 程序中使用 SO_LINGER ，应用强制使用 RST 关闭。**直接关闭**

### ip地址划分

主机数要减去全0和全1，**全0代表一个网段**，**全1表示广播地址**

**127是环路地址**

```
3、公有地址（Public address）

由Inter NIC（Internet Network Information Center 因特网信息中心）负责。这些IP地址分配给注册并向Inter NIC提出申请的组织机构。通过它直接访问因特网。

 

4、私有地址（Private address）

属于非注册地址，专门为组织机构内部使用。以下为留用的私有地址：
       A类 10.0.0.0--10.255.255.255         (10.0.0.0/8)
       B类 172.16.0.0--172.31.255.255      (172.16.0.0/12)
       C类 192.168.0.0--192.168.255.255  (192.168.0.0/16)

我们平时说的局域网地址一般都是在留用的私有地址的范围内，这些地址为非注册IP。局域网和外网交互是通过互联网运营商分配给我们的动态IP（该IP为公有IP地址）。一般一个局域网分配一个公有IP，局域网内的所有主机通过路由器（或其他设备）上的一种映射机制访问外网。
```

#### 子网划分

子网号**不能是另一个子网的前缀**，不然路由器转发的时候就不能区分去哪个子网了。

可以采用**哈夫曼编码**，划分5个子网号的哈夫曼树如下：

```
0
10
110
1110
1111
```

所以至少需要4位存储保留子网号，所以主机数为2^8-2=254，即IP地址数为254

![image-20220910154143478](javaNote.assets/image-20220910154143478.png)

![image-20220916195347877](javaNote.assets/image-20220916195347877.png)

### 网卡（网络设配器）

```
链路层电脑接入局域网的设备
```

网卡**属于OSI的物理层与链路层**，它工作在物理层和数据链路层的MAC子层。

网卡，即网络接口控制器，又称网络接口控制器，**网络适配器**，网卡，或局域网接收器，是一块被设计用来允许**计算机在计算机网络上进行通讯的计算机硬件**；**计算机与外界局域网的连接是通过网卡进行的**。由于其拥有MAC地址，因此属于OSI模型的第1层（物理层）；它使得用户可以通过电缆或无线相互连接。

**网卡主要功能：**

1、实现与主机总线的通讯连接，解释并执行主机的控制命令。

2、实现数据链路层的功能。

3、实现物理层的功能 网卡简称网络接口卡 ，是计算机局域网中重要的连接设备之一，**计算机通过网卡接入网络**。

### 粘包

tcp为了提高效率，每次都要等足够长的数据才进行发送

```
A:固定长度；
B：分隔符
D:添加长度信息。
```

### IPv6

128位、**取消了分片/重新组装相关字段**

- IPv6 可自动配置，即使没有 DHCP 服务器也可以实现自动分配IP地址，真是**便捷到即插即用**啊。
- IPv6 包头包首部长度采用固定的值 `40` 字节，去掉了包头校验和，简化了首部结构，减轻了路由器负荷，大大**提高了传输的性能**。
- IPv6 有应对伪造 IP 地址的网络安全功能以及防止线路窃听的功能，大大**提升了安全性**。

## 算法和数据结构

### 分布式唯一ID

#### 一、分布式唯一ID的需求产生的背景

在分布式集群环境环境中，大量的业务场景需要使用到唯一ID的情况，如用户需要唯一身份标识、商品需要唯一标识、消息需要唯一标识、事件需要唯一标识等，都需要全局唯一ID，尤其是复杂的分布式业务场景中全局唯一ID更为重要那么，分布式唯一ID有哪些特性或要求呢？

① 唯一性：生成的ID全局唯一，在特定范围内冲突概率极小。
② 有序性：生成的ID按某种规则有序，便于数据库插入及排序。
③ 可用性：可保证高并发下的可用性, 确保任何时候都能正确的生成ID。
④ 自主性：分布式环境下不依赖中心认证即可自行生成ID。
⑤ 安全性：不暴露系统和业务的信息, 如：订单数,用户数等。

#### 二、常见的分布式唯一ID解决方案

总的来说，大概有三大类方法，分别是：
数据库自增ID、
UUID生成、
redis生成、
snowflake雪花算法。

#### 1、【数据库自增长ID】

【优缺点】
优点： 非常简单，有序递增，方便分页和排序；
缺点： 分库分表后，同一数据表的自增ID容易重复，无法直接使用(可以设置步长，但局限性很明显)；性能吞吐量整个较低；ID号码不够随机，能够泄露发号数量的信息，不太安全。

【使用场景】
单数据库实例的表ID(包含主从同步场景)，部分按天计数的流水号等；分库分表场景、全系统唯一性ID场景不适用

#### 2、UUID生成

【生成原理】
UUID生成id需要用到**以太网卡地址**、**纳秒级时间**、芯片ID码和许多可能的数字。其生成的id由当前日期和时间(UUID的第一个部分与时间有关，如果你在生成一个UUID之后，过几秒又生成一个UUID，则第一个部分不同，其余相同)，时钟序列，全局唯一的IEEE机器识别号。

【优缺点】
优点： 不依赖任何数据源，自行计算，没有网络ID，速度超快，并且全球唯一；
缺点： 没有顺序性，并且比较长(128bit)，作为数据库主键、索引会导致索引效率下降，空间占用较多。

【使用场景】
只要对存储空间没有苛刻要求的都能够适用，比如各种链路追踪、日志存储等。

#### 3、redis生成id

【生成原理】
依赖redis的数据源，通过**redis的incr/incrby自增原子操作**命令，能保证生成id肯定是唯一有序的，本质生成方式与数据库一致。

【优缺点】
优点： 整体吞吐量比数据库要高；
缺点：Redis是基于内存的数据库，其实例或集群宕机后，找回最新的ID值有点困难。由于使用自增，对外容易暴露业务数据总量

【应用场景】
比较适合计数场景，如用户访问量，订单流水号(日期+流水号)等。

#### 4、雪花算法snowflake

【实现原理】
属于半依赖数据源方式，原理是使用**Long类型**(64位)，按照一定的规则进行填充：**时间(毫秒级)+集群ID+机器ID+序列号**，每部分占用的位数可以根据实际需要分配，其中集群ID和机器ID这两部分，在实际应用场景中要依赖外部参数配置或数据库记录。

【优缺点】
优点： 高性能、低延迟、去中心化、按时间有序；
缺点： 要求机器时钟同步(到秒级即可)，即时间回拨 会导致id重复。

【使用场景】
分布式应用环境的数据主键，大多数使用雪花算法来实现分布式id。

【如何解决时间回拨问题】
时间回拨是指，当机器出现问题,时间可能回到之前,此时雪花算法生成的id可能与之前的id值相同，从而导致id重复
【解决方式】
1、系统抛出异常，运维来手动调整时间；
2、延迟等待，对于偶然性的时间回拨，也许是机器出现了一次小故障，频繁出现的概率并不大，所以对于这种情况没必要中断业务，可以采用阻塞线程5ms，再获取时间，对比看时间是否比上一次请求的时间大，如果大了,说明恢复正常了,则不用管；如果还小,说明真出问题了,则抛出异常,呼唤程序员处理
3、备用机方式来解决，当前机器出现问题，迅速换一台机器，通过高可用解决

### 加密算法

![image-20220911110949448](javaNote.assets/image-20220911110949448.png)

1.RSA：是一个支持变长密钥的公共密钥算法，需要加密的文件块的长度也是可变的，**非对称**算法； 

  2.RC2和RC4：**对称**算法，用变长密钥对大量数据进行加密，比 DES 快； 

  3.DES（Data Encryption Standard）：**对称**算法，数据加密标准，速度较快，适用于加密大量数据的场合； 

  

MD5 由于是**单向不可逆的**，所以**不可以解密**，不能用来对文本进行加密，可以用来签名，校验数据的完整性

### 顺序表插入删除移动次数

插入移动次数：n / 2

![\sum_{i=0}^{n+1} \frac{1}{n+1}(n-i)=\frac{1}{n+1} \sum_{i=0}^{n+1}(n-i)=\frac{1}{n+1} \frac{n(n+1)}{2}=\frac{n}{2}](javaNote.assets/frac{n}{2}.gif)

删除：(n-1) / 2

![\sum_{i=0}^{n} p_{0}(n-i)=\sum_{i=0}^{n} \frac{1}{n}(n-i)=\frac{1}{n} \sum_{i=0}^{n}(n-i)=\frac{1}{n} \frac{n(n-1)}{2}=\frac{n-1}{2}](javaNote.assets/frac{n-1}{2}.gif)

![image-20220904173720513](javaNote.assets/image-20220904173720513.png)

### 广义表

#### 广义表的长度

指广义表中所包含的数据元素的个数

例如，在广义表 {a,{b,c,d}} 中，它包含一个原子和一个子表，因此该广义表的长度为 2，深度为2。
再比如，广义表 {{a,b,c}} 中只有一个子表 {a,b,c}，因此它的长度为 1，深度为2。

#### 广义表的深度

可以通过观察该表中所包含括号的层数间接得到。这里需要注意，数左括号（或右括号）时同一层次的多个括号只计算一次

比如：广义表 {{1,2},{3,{4,5}}} 中，子表 {1,2} 和 {3,{4,5}} 位于同层，此广义表中包含 3 层括号，因此长度为，2深度为 3。

E((a,(a,b),((a,b),c)))长度为1，深度为4

![image-20220903172328335](javaNote.assets/image-20220903172328335.png)

### 算法的基本要素

一是**对数据对象的运算和操作**

二是算法的**控制结构**

![image-20220903171857564](javaNote.assets/image-20220903171857564.png)

### 活结点

活结点：能够扩展子节点的节点

![image-20220903171806688](javaNote.assets/image-20220903171806688.png)

### hash冲突

常用处理冲突的思路：

- 换个位置: `开放地址法`
- 同一位置的冲突对象组织在一起:`链地址法`

一旦产生了冲突（该地址已有其它元素），就按某种规则去寻找另一空地址

若发生了第 i 次冲突，试探的下一个地址将增加di，基本公式是：
hi(key) = (h(key)+di) mod TableSize ( 1≤ i < TableSize )
di 决定了不同的解决冲突方案：线性探测、平方探测、双散列。
线性探测：di = i
平方探测：di = ± i2( +12, -12, +22, -22……)
双散列：di = i * h2(key)

### 算法设计的四个要求

1、可读性

2、正确性

3、健壮性

4、时间和空间效率

### 进制转换

#### 1.十进制转换为其他进制：短除法

520=0X208 (2×16×16+8=520)

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6L-95qKm5LmL,size_20,color_FFFFFF,t_70,g_se,x_16.png)

#### 2.其他进制转换为十进制：位权计算

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6L-95qKm5LmL,size_20,color_FFFFFF,t_70,g_se,x_16-16621894680792.png)

 如：

​	二进制  1001 0011      其十进制为：1×2^7+1×2^4+1×2^1+1×2^0=147

​    八进制  1010               其十进制为：1×8^3+1×8^1=520

#### 3.二进制、八进制、十六进制的相互转换：拆位

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6L-95qKm5LmL,size_20,color_FFFFFF,t_70,g_se,x_16-16621894842934.png)

#### 5、十进制小数转二进制

同样按权展开，得B=a(2^-1)+b(2^-2)。因为小数部分的**位权是负次幂，所以我们只能乘2**，得2B=a+b（2^-1)。注意a变成了整数部分，我们取整数正好是取到了a，剩下的小数部分也如此。

![img](javaNote.assets/472309f7905298221d54ce53daca7bcb0a46d43f.png)

### 循环队列

#### 1、初始化

![img](javaNote.assets/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5LiD5LujMzY1,size_20,color_FFFFFF,t_70,g_se,x_16.png)

#### 2、判空

Q.front == Q.rear

#### 3、获取元素个数

(Q.rear - Q.front + MaxSize) % MaxSize

#### 4、入队

Q.base[Q.rear]=e; 将元素e放入Q.rear指向的空间

Q.rear=(Q.rear+1)%Maxsize rear指针向后移动一个单位

#### 5、出队

e=Q.base[Q.front];

Q.front=[Q.front+1]%Maxsize

#### 6、获取队头元素

Q.**base**[Q.front]

#### 7、获取队尾元素

Q.**base**[Q.rear - 1] 注意rear指向空，前一位才是队尾元素

### 二次散列

![img](javaNote.assets/v2-0c6329aaa5c5f5b2fefaaefe70b1b9de_b.jpg)

![image-20220716105513250](javaNote.assets/image-20220716105513250.png)

![img](javaNote.assets/F3CCDD27D2000E3F9255A7E3E2C48800.jpeg)

### 唯一确定一颗二叉树

一定要有**中序**才能唯一确定一颗二叉树

- 先序和后续只能确定根节点，再从中序分割出左右子树

- 根据根节点把中序遍历分为左右子树。

### 二叉树度和节点数

```
n2=n0-1 度为2的结点比叶子结点少一个
```

```
结论：二叉树中度数为2的节点数量比叶子节点少一个

证明：设0度节点（叶子节点）、一度节点、二度节点数量分别为n0,n1,n2

那么总的点数为n=n0+n1+n2。

而边的数量为m=n-1（树的性质）

同时又有m=2*n2+1*n1+0*n0

所以 n0+n1+n2-1=m=2n2+n1

所以 n2=n0-1
```



### 时间复杂度

```
log4n=log2^2n=0.5log2n
```

![image-20220726163335340](javaNote.assets/image-20220726163335340.png)

```java
下面两种道理都是一样的

//时间复杂度为 2^n
    
func(int n){
	if(n==1){
		return;
	}
	return n*func（n-1）（n-2）;
}


//时间复杂度：2^n
func(int n){
    if(n==1){
        return;
    }
    return f(n-1)+(n-2);
}

f(6)=        f(5)         +           f(4)
        f(4)        f(3)         f(3)       f(2)
   f(3)     (2)   f(2) f(1)   f(2)   f(1)
 f(2)(1)   f(1)
```

### 八大排序

**直接插入排序和冒泡排序的最好情况都是O(n)**

稳定性：跳跃的一定是不稳定的
希尔排序就是插入排序的升级版，不稳定的，复杂度最差最坏都是O(nlog2n)
归并排序：O(nlog2n),稳定

归并需要的O(n)的空间，快排需要O(nlogn)的空间



**直接插入排序**（稳定）：从第二位开始遍历，如果小于前一位，就找到往前找插入到最合适的位置。O(n^2)。稳定

**希尔排序**（不稳定）：插入排序的升级版，对一个增量进行插入排序，增量不断减小至1。O(nlogn)。会跳跃，不稳定

**冒泡排序**（稳定）：O(n^2)  左右交换，稳定

**快速排序**（不稳定）：O(nlogn)会跳跃，不稳定

**直接选择排序**：每次找到最小的，和开头进行跨域交换，所以不稳定。O(n^2)。不稳定，比如7，7，2，7和2交换之后就不稳定了

**堆排序**（不稳定）：O(nlogn) 会跳跃，不稳定

**归并排序**（稳定）：二路归并排序，倒满二叉树，子序列有序，再进行合并。O(nlogn) 稳定

**基数排序**（稳定）：O(d(n+r))。个位，十位逐个比较，稳定

![这里写图片描述](javaNote.assets/20180114193248117.png)

### 补码

符号位不变，各位取反，末位加一

```
负数的补码是将其原码除符号位之外的各位求反之后在末位再加1。
[-3]补=[10000011]补=11111101
```

### 强连通图

每一对顶点之间都存在路径

n个顶点的有向强连通图：至少有n条边（形成环），最多有n(n-1)条边

n个顶点的无向强连通图：至少有n-1条边（一条直线），最多有n(n-1)/2条边

### 点积

![image-20220911112833002](javaNote.assets/image-20220911112833002.png)

大于0，说明是锐角

小于0，说明是钝角

等于0，说明是直角

### 向量

AB+BC=AC

AB-AC=CB

### 排列组合

【1】、10个相同的糖果，分给3个孩子A、B、C，每个孩子至少一个，有多少种不同的分法？C（9，2）=36

【2】、10个相同的糖果，分给3个孩子A、B、C，有多少种不同的分法？C（12，2）=66

【3】、10个相同的糖果，分给3个孩子A、B、C，每个孩子至少2个，有多少种不同的分法？C（6，2）=15

【4】、10个相同的糖果，分给3个孩子A、B、C，A至少一个，B至少2个，C可以没有，有多少种不同的分法？C（9，2）=36

【答案】

【1】第一题是最为典型的插板法的题目。10个糖果排成一排，共形成9个空，我从这9个空里选两个，插入隔板，便把这10个糖果分成了三份，每份起码有一个，这样的话，方法数就是**C（9，2）=36**。

【2】、与第一题不同，这里没有限制孩子获得的数量，意味着有些孩子可以分到0个。那么这时候就不能直接用插板法了，必须转化成每个孩子至少得到1个。怎么转化呢？

很简单，分这10个糖果之前就**给每个小朋友1个糖果**，这样就保证分的时候每个小朋友至少分一个了，就可以用插板法了，只不过这时的题就变成了“10+3=13个相同的糖果，分给3个孩子A、B、C，每个孩子至少一个，有多少种不同的分法？”.

13个糖果12个空，分成三组插两块板，方法数就是**C（12，2）=66**。

【3】.不能直接插板，需要先将至少2个转化成至少1个，咋转化？**先给每人1个**，剩下的至少每人一个就搞定啦！题目变为“10-1×3=7个相同的糖果，分给3个孩子A、B、C，每个孩子至少一个，有多少种不同的分法？”

7个糖果6个空，分成三组插两块板，方法数就是C（6，2）=15。

【4】此题综合了这几类题型，还是转化：A满足不用管；**B至少2个，需要先分掉1个**；**C可以不分，那就借一个给他**。 10-1+1=10，题目变成第一小题了，答案还是36.

![image-20220911111609106](javaNote.assets/image-20220911111609106.png)

[文章](https://zhuanlan.zhihu.com/p/41855459)

#### 排列

从n个不同元素中取出m个元素的所有排列的个数，记作 A（n，m）

![img](javaNote.assets/241f95cad1c8a7863d7dc9727709c93d70cf5073.png)

#### 组合

从n个不同中取出m个元素的所有组合个数，记作 C（n，m）

![img](javaNote.assets/023b5bb5c9ea15cea4b86375a6003af33a87b27c.png)

### 等差和等比数列

等差数列：sn=(n(1+n))/2

等比数列：sn=(a1(1-q^n))/(1-q)

![img](javaNote.assets/d439b6003af33a8789221a65cd37d3315243b5f2.jpeg)

### 二叉搜索树

中序的前驱后继结点

### 最小生成树

最小生成树的**代价唯一**的，但**生成树不唯一**，比如每一条边都一样的生成树。

所有权值最小的边**不一定**会出现在所有的最小生成树中。

使用普里姆(Prim)算法从不同顶点开始得到的最小生成树不一定相同，比如每一条边都一样的生成树。

使用普里姆算法和克鲁斯卡尔(Kruskal)算法得到的最小生成树**可能相同**

![image-20220910151336530](javaNote.assets/image-20220910151336530.png)

#### prim（普里姆）算法

O(n^2) 

每次维护一个联通集（已形成的生成树），不断**加入距生成树最近的顶点**。

针对顶点进行，所以**边多**比较适合。

```
    int buildMinSpan_tree(int[][] dist, int n) {
        // 开始构造最小生成树
        int ans=0;
        int[] lowCost=new int[n], // 距联通集中的最短距离
                vertex=new int[n]; // 距联通集的最短距离对应的顶点

        // 首先把0加入联通集中（最小生成树从哪一个顶点开始结果是一样的）
        lowCost[0]=0;
        vertex[0]=0;
        for (int i = 1; i < n; i++) {
            lowCost[i]=dist[0][i]; // 初始化结点到联通集的距离为到顶点0的距离（lowCost=0表示已加入联通集）
            vertex[i]=0; // 相关顶点左边也为0
        }

        for (int i = 1; i < n; i++) {
            // 找到距离联通集最近的结点
            int k=-1,minValue=Integer.MAX_VALUE;
            // 遍历distance,找到最近的结点
            for (int j = 1; j < n; j++) {
                if(lowCost[j]!=0&&lowCost[j]<minValue){ // 未加入联通集，得到距离当前联通集最近的顶点
                    k=j; // 记录新加入的下标
                    minValue=lowCost[j]; // 更新最小值
                }
            }

            ans+=lowCost[k]; // 累计生成树的花费
            lowCost[k]=0; // 加入联通集

            // 更新distance数组，即到联通集的最短距离
            for (int j = 1; j < n; j++) {
                if(dist[k][j]<lowCost[j]){
                    // 新加入的顶点更近
                    vertex[j]=k;
                    lowCost[j]=dist[k][j];
                }
            }
        }
        return ans;
    }
```

[leetcode 1584. 连接所有点的最小费用](https://leetcode.cn/problems/min-cost-to-connect-all-points/)

[个人题解地址](https://leetcode.cn/problems/min-cost-to-connect-all-points/solution/primsuan-fa-by-moon-iw-dyi7/)

算法思想：
先找一个结点，之后不断加入距离联通集最近的顶点，同时更新顶点到联通集的最短距离。
Prim算法是针对顶点进行，所以边多的情况比较适合。


/**
 * 最小生成树之Prim算法
 * 使用数组lowCost表示距联通集中的最短距离，初始为到顶点0的距离；之后每加入一个顶点，更新数组
 * 使用数组vertex距联通集的最短距离对应的顶点存储距离已有生成树中距离
 * 时间：O（n^2）
 * 空间：O(n) 存储 距联通集中的最短距离 和 距联通集的最短距离对应的顶点
 */

参考：大话数据结构

#### Kruskal（克鲁斯卡尔）算法

O(eloge) 根据边决定

**贪心算法**：每次把最短的边连起来

eloge边先**排好序**，每次把边连起来，同时**保证不形成环**就连起来。

针对边排序，所以**边少比较适合**。

### 单源最短路径

#### Dijkstra（迪杰斯特拉）

每次找到距离源点的最近结点，如果未加入的节点能通过新加入的节点更短的到达源节点，那么更新v0到该结点的最短路径，O(n2)

#### Floyd（弗洛伊德算法）

如果有一个点k让i，j的距离更短，更新i，j的距离

三重循环，每次修改得到更小的前驱结点，O(n3)。

### 哈夫曼树

可用于**子网划分**

带权最短路径WPL最小的二叉树，**权重越大的让他路径越短**

![image-20220512123555113](javaNote.assets/image-20220512123555113.png)

![image-20220716111655748](javaNote.assets/image-20220716111655748.png)

![img](javaNote.assets/7DAF6B9D2D174403916910ECA02BE658.jpeg)

### 红黑树

**B+树**插入操作的平均时间复杂度为O(logn)，最坏时间复杂度为**O(n)**
**Hash表**插入操作的平均时间复杂度为O(1)，最坏时间复杂度为O(n)
**排序链表**插入操作的平均和最坏时间复杂度为O(n)
**红黑树**插入操作的平均和最坏时间复杂度为**O(logn)**

![image-20220904221704838](javaNote.assets/image-20220904221704838.png)

解决**BST**倾斜问题，会退化成链表。二叉查找树增删查改的时间复杂度为O(logN)（其中N为节点数），最坏的情况下为O(N)

于是平衡二叉查找树(**Balanced BST**)产生了，平衡树在插入和删除的时候，会通过旋转操作将高度保持在logN。

其中两款具有代表性的平衡树分别为**AVL树和红黑树**。AVL树由于实现比较复杂，而且**插入和删除性能差**，在实际环境下的应用不如红黑树。

红黑树（Red-Black Tree，以下简称RBTree）的实际应用非常广泛，比如Linux内核中的完全公平调度器、高精度计时器、ext3文件系统等等，各种语言的函数库如Java的TreeMap和TreeSet，C++ STL的map、multimap、multiset等。

#### 时间复杂度

整个红黑树的查找，插入和删除都是O(logN)，因为**高度就是logn**,查找从根到叶，走过的路径是树的高度，删除和插入操作是从叶到根的，所以经过的路径都是logN。

https://blog.csdn.net/u014454538/article/details/120120216

```
1、头尾（nil）都是黑结点
2、从叶子结点到根节点黑色结点数目是一样的
3、不能有两个连续的红节点
```

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQ0NTQ1Mzg=,size_16,color_FFFFFF,t_70.png)

通过这些规则，保证红黑树的自平衡

#### 查询效率这么高，mysql为什么不用？

主要是**红黑树的高度会比较高**，磁盘io太大

#### HashMap为什么用红黑树而不用B树？

**数据都会“挤在”一个结点里面**，这个时候遍历效率就退化成了链表。

B/B+树多用于外存上时，B/B+也被成为一个磁盘友好的数据结构。

HashMap本来是数组+链表的形式，链表由于其查找慢的特点，所以需要被查找效率更高的树结构来替换。如果用B/B+树的话，在数据量不是很多的情况下，**数据都会“挤在”一个结点里面**，这个时候遍历效率就退化成了链表。

### B&B+树

B树不支持顺序查找，**B+树支持顺序查找**
B树和B+树**都支持随机查找**，都可做文件的索引结构，平衡多叉树

#### 二叉排序树

#### `可能退化成链表`

#### 平衡二叉树(AVL)

#### `每个结点的左右子树高度差至多等于一`

### 最大公约数

```
m*n=最大公约数*最小公倍数

辗转相除法或辗转相减法
```

```java
    // 辗转相除法递归
    public int gcd1(int m,int n){
        while (n!=0){
            int remainder=m%n;
            m=n;
            n=remainder;
        }
        return m;
    }
    // 辗转相除法迭代
    public int gcd2(int m,int n){
        if(n==0)
            return m;
        return gcd2(n,m%n);
    }

    // 辗转相减法
    public int gcd3(int m,int n){
        while(m!=n){
            if(m>n){
                m=m-n;
            }
            else{
                n=n-m;
            }
        }
	    return m;
    }
```

### 快排:会退化成O(n2)

[博客园](https://www.cnblogs.com/MOBIN/p/4681369.html)

```java

    public static void quickSort(int arr[],int _left,int _right){
        int left = _left;
        int right = _right;
        int temp = 0;
        if(left <= right){   //待排序的元素至少有两个的情况
            temp = arr[left];  //待排序的第一个元素作为基准元素
            while(left != right){   //从左右两边交替扫描，直到left = right
                while(right > left && arr[right] >= temp)  
                     right --;        //从右往左扫描，找到第一个比基准元素小的元素
                  arr[left] = arr[right];  //找到这种元素arr[right]后与arr[left]交换
                while(left < right && arr[left] <= temp)
                     left ++;         //从左往右扫描，找到第一个比基准元素大的元素
                  arr[right] = arr[left];  //找到这种元素arr[left]后，与arr[right]交换
            }
            arr[right] = temp;    //基准元素归位
            quickSort(arr,_left,left-1);  //对基准元素左边的元素进行递归排序
            quickSort(arr, right+1,_right);  //对基准元素右边的进行递归排序
        }        
    }
```

### 堆排序`len/2+1为最后一个非叶子结点`

[博客园](https://www.cnblogs.com/chengxiao/p/6129630.html)

```java
package sortdemo;

import java.util.Arrays;

/**
 * Created by chengxiao on 2016/12/17.
 * 堆排序demo
 */
public class HeapSort {
    public static void main(String []args){
        int []arr = {9,8,7,6,5,4,3,2,1};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }
    public static void sort(int []arr){
        //1.构建大顶堆
        for(int i=arr.length/2-1;i>=0;i--){
            //从第一个非叶子结点从下至上，从右至左调整结构
            adjustHeap(arr,i,arr.length);
        }
        //2.调整堆结构+交换堆顶元素与末尾元素
        for(int j=arr.length-1;j>0;j--){
            swap(arr,0,j);//将堆顶元素与末尾元素进行交换
            adjustHeap(arr,0,j);//重新对堆进行调整
        }

    }

    /**
     * 调整大顶堆（仅是调整过程，建立在大顶堆已构建的基础上）
     * @param arr
     * @param i
     * @param length
     */
    public static void adjustHeap(int []arr,int i,int length){
        int temp = arr[i];//先取出当前元素i
        for(int k=i*2+1;k<length;k=k*2+1){//从i结点的左子结点开始，也就是2i+1处开始
            if(k+1<length && arr[k]<arr[k+1]){//如果左子结点小于右子结点，k指向右子结点
                k++;
            }
            if(arr[k] >temp){//如果子节点大于父节点，将子节点值赋给父节点（不用进行交换）
                arr[i] = arr[k];
                i = k;
            }else{
                break;
            }
        }
        arr[i] = temp;//将temp值放到最终的位置
    }

    /**
     * 交换元素
     * @param arr
     * @param a
     * @param b
     */
    public static void swap(int []arr,int a ,int b){
        int temp=arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
```

##### 设一课完全二叉树共有999个结点，则在该二叉树中的叶节点个数是？

```
最后一个结点999/2=499为它的父节点，说明它499之后都是叶子节点，所以999-499=500
```

##### 给定一个由若干 0 和 1 组成的数组 A，我们最多可以将 K 个值从 0 变成 1 ，返回仅包含 1 的最长（连续）子数组的长度

```
    public static int GetMaxConsecutiveOnes(int[] arr, int k) {
        // 判断数组长度是否小于等于将0变为1的长度  若是 则最长连续为数组的长度
        if (arr.length <= k) {
            return arr.length;
        }
        int i = 0;
        // 存储最长连续子数组的长度
        int max = 0;
        // 从索引为0的数组下标开始循环    直到索引大于数组长度减去k的长度
        while (i < arr.length - k) {
            // 定义将0变为1的次数
            int count = 0;
            // 从索引为i处开始循环对比
            int j = i;
            for (; j < arr.length; j++) {
                // 如果索引位置处的值不为1   则将count++  意思为将0变成1了
                if (arr[j] != 1) {
                    count++;
                }
                // 如果将0变为1的次数 大于最初定义的k次数 则将长度和最大值对比  保留最长的长度
                if (count > k) {
                    max = max > j - i ? max : j - i;
                    break;
                }
            }
            // 如果循环完毕最终长度和数组长度相同  则再将长度和最大值对比  保留最长的长度
            if (j==arr.length){
                max = max > j - i ? max : j - i;
            }
            i++;
        }
        return max;

    }
    
    
    
```

## MongoDB

支持副本集部署

数据记录的格式是json，数据存放格式是BSON

![img](javaNote.assets/Center.png)

## 分布式算法

### paxos算法

分布式共识算法

### raft算法

分布式共识算法

复制日志来实现多副本状态机

动图：https://thesecretlivesofdata.com/raft/

https://blog.csdn.net/daaikuaichuan/article/details/98627822

#### 1、Raft分为哪几个部分？

  **主要是分为leader选举、日志复制、日志压缩、成员变更等**。

#### 2、Raft中任何节点都可以发起选举吗？

  Raft发起选举的情况有如下几种：

- 刚启动时，所有节点都是follower，这个时候发起选举，选出一个leader；
- 当leader挂掉后，**时钟最先跑完的follower发起重新选举操作**，选出一个新的leader。
- 成员变更的时候会发起选举操作。

#### 3、Raft中选举中给候选人投票的前提？

  **Raft确保新当选的Leader包含所有已提交（集群中大多数成员中已提交）的日志条目**。这个保证是在RequestVoteRPC阶段做的，candidate在发送RequestVoteRPC时，会带上自己的**last log entry的term_id和index**，follower在接收到RequestVoteRPC消息时，**如果发现自己的日志比RPC中的更新，就拒绝投票**。日志比较的原则是，如果本地的最后一条log entry的term id更大，则更新，如果term id一样大，则日志更多的更大(index更大)。

#### 4、Raft网络分区下的数据一致性怎么解决？

  发生了网络分区或者网络通信故障，**使得Leader不能访问大多数Follwer了，那么Leader只能正常更新它能访问的那些Follower，而大多数的Follower因为没有了Leader，他们重新选出一个Leader**，然后这个 Leader来接受客户端的请求，如果客户端要求其添加新的日志，这个新的Leader会通知大多数Follower。**如果这时网络故障修复 了，那么原先的Leader就变成Follower，在失联阶段这个老Leader的任何更新都不能算commit，都回滚，接受新的Leader的新的更新（递减查询匹配日志）**。
![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RhYWlrdWFpY2h1YW4=,size_16,color_FFFFFF,t_70.png)

#### 5、Raft数据一致性如何实现？

  **主要是通过日志复制实现数据一致性，leader将请求指令作为一条新的日志条目添加到日志中，然后发起RPC 给所有的follower，进行日志复制，进而同步数据**。

#### 6、Raft的日志有什么特点？

  **日志由有序编号（log index）的日志条目组成，每个日志条目包含它被创建时的任期号（term）和用于状态机执行的命令**。

#### 7、Raft和Paxos的区别和优缺点？

- Raft的leader有限制，**拥有最新日志的节点才能成为leader**，multi-paxos中对成为Leader的限制比较低，**任何节点都可以成为leader**。
- **Raft中Leader在每一个任期都有Term**号。

#### 8、Raft prevote机制？

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RhYWlrdWFpY2h1YW4=,size_16,color_FFFFFF,t_70-165901476718721.png)
  **Prevote（预投票）是一个类似于两阶段提交的协议**，**第一阶段先征求其他节点是否同意选举，如果同意选举则发起真正的选举操作，否则降为Follower角色**。这样就**避免了网络分区节点重新加入集群，触发不必要的选举操作**。

#### 9、Raft里面怎么保证数据被commit，leader宕机了会怎样，之前的没提交的数据会怎样？

  **leader会通过RPC向follower发出日志复制，等待所有的follower复制完成，这个过程是阻塞的**。

  **老的leader里面没提交的数据会回滚，然后同步新leader的数据**。

#### 10、Raft日志压缩是怎么实现的？增加或删除节点呢？？

  在实际的系统中，**不能让日志无限增长**，否则**系统重启时需要花很长的时间进行回放**，从而影响可用性。**Raft采用对整个系统进行snapshot来解决，snapshot之前的日志都可以丢弃（以前的数据已经落盘了）**。

  **snapshot里面主要记录的是日志元数据，即最后一条已提交的 log entry的 log index和term**。

#### 11、Raft里面的lease机制是什么，有什么作用？

  **租约机制确保了一个时刻最多只有一个leader，避免只使用心跳机制产生双主的问题**。**中心思想是每次租约时长内只有一个节点获得租约、到期后必须重新颁发租约**。
![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RhYWlrdWFpY2h1YW4=,size_16,color_FFFFFF,t_70-165901476718722.png)

#### 12、Raft协议的leader选举，正常情况下，网络抖动造成follower发起leader选举，且该follower的Term比现有leader高，集群中所有结点的日志信息当前一致，这种情况下会选举成功吗？

  **参考网络分区的情况**。

## SringCloud

### setinel

Sentinel实现**限流、隔离、降级、熔断**等功能，本质要做的就是两件事情：

- 统计数据：统计某个资源的访问数据（QPS、RT等信息）
- 规则判断：判断限流规则、隔离规则、降级规则、熔断规则是否满足

总体基于责任链模式，每个链路节点抽象成××slot，一些slot进行数据统计，一些进行规则判断等，然后基于各种限流算法实现对应的限流规则等。主要组件有ProcessorSLotChain处理器链，链路节点Node，资源Entry，上下文Context等

![image-20220728225713168](javaNote.assets/image-20220728225713168.png)

#### 一、限流算法

1、滑动时间窗口计数器算法

限流中的快速失败、warm up、QPS计数

![image-20220728224618315](javaNote.assets/image-20220728224618315.png)

2、令牌桶算法

参数限流

![image-20220728224633144](javaNote.assets/image-20220728224633144.png)

3、漏桶算法

排队等待效

![image-20220728224642849](javaNote.assets/image-20220728224642849.png)

![image-20220728224901130](javaNote.assets/image-20220728224901130.png)

#### 二、概念组件

#### ProcessorSlotChain

setinel的核心骨架是`ProcessorSlotChain`**处理器槽链**，基于**责任链模式**，将不同的功能（限流、降级、系统保护）封装为一个个的Slot，请求进入后逐个执行即可

![image-20220728220641635](javaNote.assets/image-20220728220641635.png)

责任链中的Slot也分为两大类：

- 统计数据构建部分（statistic）
  - NodeSelectorSlot：负责构建簇点链路中的节点（DefaultNode），将这些节点形成链路树
  - ClusterBuilderSlot：负责构建某个资源的ClusterNode，ClusterNode可以保存资源的运行信息（响应时间、QPS、block 数目、线程数、异常数等）以及来源信息（origin名称）
  - StatisticSlot：负责统计实时调用数据，包括运行信息、来源信息等
- 规则判断部分（rule checking）
  - AuthoritySlot：负责授权规则（来源控制）
  - SystemSlot：负责系统保护规则
  - ParamFlowSlot：负责热点参数限流规则
  - FlowSlot：负责限流规则
  - DegradeSlot：负责降级规则

#### Node

链路节点

Sentinel中的簇点链路是由一个个的Node组成的，Node是一个接口，包括下面的实现：

![image-20210925103029924](javaNote.assets/image-20210925103029924.png)

所有的节点都可以记录对资源的访问统计数据，所以都是StatisticNode的子类。

按照作用分为两类Node：

- DefaultNode：代表链路树中的每一个资源，一个资源出现在不同链路中时，会创建不同的DefaultNode节点。而树的入口节点叫EntranceNode，是一种特殊的DefaultNode
- ClusterNode：代表资源，一个资源不管出现在多少链路中，只会有一个ClusterNode。记录的是当前资源被访问的所有统计数据之和。



DefaultNode记录的是资源在当前链路中的访问数据，用来实现基于链路模式的限流规则。ClusterNode记录的是资源在所有链路中的访问数据，实现默认模式、关联模式的限流规则。



例如：我们在一个SpringMVC项目中，有两个业务：

- 业务1：controller中的资源`/order/query`访问了service中的资源`/goods`
- 业务2：controller中的资源`/order/save`访问了service中的资源`/goods`

创建的链路图如下：

![image-20210925104726158](javaNote.assets/image-20210925104726158.png)

#### Entry

基于**AOP**思想，对资源标记的方法环绕增强，完成对**资源**Entry的创建

![image-20220728221012195](javaNote.assets/image-20220728221012195.png)

```java
@Aspect
public class SentinelResourceAspect extends AbstractSentinelAspectSupport {
	// 切点是添加了 @SentinelResource注解的类
    @Pointcut("@annotation(com.alibaba.csp.sentinel.annotation.SentinelResource)")
    public void sentinelResourceAnnotationPointcut() {
    }
	
    // 环绕增强
    @Around("sentinelResourceAnnotationPointcut()")
    public Object invokeResourceWithSentinel(ProceedingJoinPoint pjp) throws Throwable {
        // 获取受保护的方法
        Method originMethod = resolveMethod(pjp);
		// 获取 @SentinelResource注解
        SentinelResource annotation = originMethod.getAnnotation(SentinelResource.class);
        if (annotation == null) {
            // Should not go through here.
            throw new IllegalStateException("Wrong state for SentinelResource annotation");
        }
        // 获取注解上的资源名称
        String resourceName = getResourceName(annotation.value(), originMethod);
        EntryType entryType = annotation.entryType();
        int resourceType = annotation.resourceType();
        Entry entry = null;
        try {
            // 创建资源 Entry
            entry = SphU.entry(resourceName, resourceType, entryType, pjp.getArgs());
            // 执行受保护的方法
            Object result = pjp.proceed();
            return result;
        } catch (BlockException ex) {
            return handleBlockException(pjp, annotation, ex);
        } catch (Throwable ex) {
            Class<? extends Throwable>[] exceptionsToIgnore = annotation.exceptionsToIgnore();
            // The ignore list will be checked first.
            if (exceptionsToIgnore.length > 0 && exceptionBelongsTo(ex, exceptionsToIgnore)) {
                throw ex;
            }
            if (exceptionBelongsTo(ex, annotation.exceptionsToTrace())) {
                traceException(ex);
                return handleFallback(pjp, annotation, ex);
            }

            // No fallback function can handle the exception, so throw it out.
            throw ex;
        } finally {
            if (entry != null) {
                entry.exit(1, pjp.getArgs());
            }
        }
    }
}
```

#### Context

什么是Context呢？

- Context 代表调用链路上下文，贯穿一次调用链路中的所有资源（ `Entry`），基于ThreadLocal。
- Context 维持着入口节点（`entranceNode`）、本次调用链路的 curNode（当前资源节点）、调用来源（`origin`）等信息。
- 后续的Slot都可以通过Context拿到DefaultNode或者ClusterNode，从而获取统计数据，完成规则判断
- Context初始化的过程中，会创建EntranceNode，contextName就是EntranceNode的名称

对应的API如下：

```java
// 创建context，包含两个参数：context名称、 来源名称
ContextUtil.enter("contextName", "originName");
```



在`AbstractSentinelInterceptor`中初始化

`HandlerInterceptor`拦截器会拦截一切进入controller的方法，执行`preHandle`前置拦截方法，而Context的初始化就是在这里完成的。

```java
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
    throws Exception {
    try {
        // 获取资源名称，一般是controller方法的@RequestMapping路径，例如/order/{orderId}
        String resourceName = getResourceName(request);
        if (StringUtil.isEmpty(resourceName)) {
            return true;
        }
        // 从request中获取请求来源，将来做 授权规则 判断时会用
        String origin = parseOrigin(request);
        
        // 获取 contextName，默认是sentinel_spring_web_context
        String contextName = getContextName(request);
        // 创建 Context
        ContextUtil.enter(contextName, origin);
        // 创建资源，名称就是当前请求的controller方法的映射路径
        Entry entry = SphU.entry(resourceName, ResourceTypeConstants.COMMON_WEB, EntryType.IN);
        request.setAttribute(baseWebMvcConfig.getRequestAttributeName(), entry);
        return true;
    } catch (BlockException e) {
        try {
            handleBlockException(request, response, e);
        } finally {
            ContextUtil.exit();
        }
        return false;
    }
}
```

#### ProcessorSlotChain执行流程

##### StatisticSlot

StatisticSlot负责统计实时调用数据，包括运行信息（访问次数、线程数）、来源信息等。

StatisticSlot是实现限流的关键，其中基于**滑动时间窗口算法**维护了计数器，统计进入某个资源的请求次数。

核心代码：

```java
@Override
public void entry(Context context, ResourceWrapper resourceWrapper, DefaultNode node, 
                  int count, boolean prioritized, Object... args) throws Throwable {
    try {
        // 放行到下一个 slot，做限流、降级等判断
        fireEntry(context, resourceWrapper, node, count, prioritized, args);

        // 请求通过了, 线程计数器 +1 ，用作线程隔离
        node.increaseThreadNum();
        // 请求计数器 +1 用作限流
        node.addPassRequest(count);

        if (context.getCurEntry().getOriginNode() != null) {
            // 如果有 origin，来源计数器也都要 +1
            context.getCurEntry().getOriginNode().increaseThreadNum();
            context.getCurEntry().getOriginNode().addPassRequest(count);
        }

        if (resourceWrapper.getEntryType() == EntryType.IN) {
            // 如果是入口资源，还要给全局计数器 +1.
            Constants.ENTRY_NODE.increaseThreadNum();
            Constants.ENTRY_NODE.addPassRequest(count);
        }

        // 请求通过后的回调.
        for (ProcessorSlotEntryCallback<DefaultNode> handler : StatisticSlotCallbackRegistry.getEntryCallbacks()) {
            handler.onPass(context, resourceWrapper, node, count, args);
        }
    } catch (Throwable e) {
        // 各种异常处理就省略了。。。
        context.getCurEntry().setError(e);

        throw e;
    }
}
```



另外，需要注意的是，所有的计数+1动作都包括两部分，以` node.addPassRequest(count);`为例：

```java
@Override
public void addPassRequest(int count) {
    // DefaultNode的计数器，代表当前链路的 计数器
    super.addPassRequest(count);
    // ClusterNode计数器，代表当前资源的 总计数器
    this.clusterNode.addPassRequest(count);
}
```

具体计数方式，我们后续再看。

接下来，进入规则校验的相关slot了，依次是：

- AuthoritySlot：负责授权规则（来源控制）
- SystemSlot：负责系统保护规则
- ParamFlowSlot：负责热点参数限流规则
- FlowSlot：负责限流规则
- DegradeSlot：负责降级规则

AuthoritySlot

## 设计模式

### 高内聚低耦合

耦合： 模块与模块之间的联系。

内聚：一般指（东西聚集在一起）形成一个模块，例如方法，变量，对象，或者是功能模块。

高内聚：尽可能的让一个**模块内部的代码相关程度高，相互联系的紧密**。模块内部的代码，**相互之间的联系越强，内聚就越高， 模块的独立性就越好**。 一个模块应该尽量去独立的完成一个功能！如果必须写另外的功能，建议拆分成多个模块，低内聚的代码，不好维护，代码也不够健壮。

低耦合：尽可能的**将每一个功能通过模块单独写出去 ，然后通过指定的接口来相互联系**，模块与模块之间的关系越是紧密，独立性就越不好，改变一个模块可能会影响其他的模块。

### 七大原则

https://zhuanlan.zhihu.com/p/58092071

理解面向对象六大原则，并运用设计模式进行系统设计实现

#### 1、 迪米特法则

**最少知道法则**，类的内部如何实现、如何复杂都与调用者或者依赖，只需要我知道调用的方法就行。例如**外观模式**，对外暴露统一的接口。

#### 2、 单一职责原则

一个类只负责一个功能领域中的相应职责。

功能简单，提高可读性和维护性，降低修改带来的风险

#### 3、 接口隔离原则

使用多个专门地接口，而不是使用单一的总接口导致依赖他不需要的接口

#### 4、 开闭原则

对扩展开发，对修改关闭，通过继承来增加新的类

#### 5、 里氏替换原则

所有引用基类（父类）的地方都能**透明地使用子类对象**。

替换子类系统正常工作。

#### 6、 依赖倒置原则

面向接口编程，细节依赖抽象，高层模块不依赖底层模块

#### 7、合成复用原则

尽量使用合成聚合的方式，而不是使用继承

### 三种类型

#### 1、创建型5

单例模式，工厂模式，原型模式、建造者模式、抽象工厂模式

#### 2、结构型7

适配器模式、桥接模式、**装饰模式**、组合模式、外观模式、享元模式、**代理模式**。

#### 3、行为型11

模版方法模式、命令模式、访问者模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式（Interpreter模式）、状态模式、策略模式、责任链模式

![image-20220727210958948](javaNote.assets/image-20220727210958948.png)

1.适配器模式 Adapter
  适配器模式是将一个类的接口转换成客户希望的另外一个接口。适配器模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。
  两个成熟的类需要通信，但是接口不同，由于开闭原则，我们不能去修改这两个类的接口，所以就需要一个适配器来完成衔接过程。

2.桥接模式 Bridge
  桥接模式将**抽象部分与它的实现部分分离**，是它们都可以独立地变化。它很好的支持了开闭原则和组合锯和复用原则。实现系统可能有多角度分类，每一种分类都有可能变化，那么就把这些多角度分离出来让他们独立变化，减少他们之间的耦合。

3.组合模式 Composite
  组合模式将对象组合成**树形结构**以表示部分-整体的层次结构，组合模式使得用户对单个对象和组合对象的使用具有一致性。

4.装饰模式 Decorator
装饰模式**动态地给一个对象添加一些额外的职责**，就增加功能来说，它比生成子类更灵活。也可以这样说，装饰模式把复杂类中的核心职责和装饰功能区分开了，这样既简化了复杂类，有去除了相关类中重复的装饰逻辑。 装饰模式没有通过继承原有类来扩展功能，但却达到了一样的目的，而且比继承更加灵活，所以可以说装饰模式是继承关系的一种替代方案。

5.外观模式 Facade
 外观模式为子系统中的一组接口**提供了统一的界面**，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。

外观模式中，客户对各个具体的子系统是不了解的，所以对这些子系统进行了封装，对外只提供了用户所明白的单一而简单的接口，用户直接使用这个接口就可以完成操作，而不用去理睬具体的过程，而且子系统的变化不会影响到用户，这样就做到了信息隐蔽。

6.享元模式 Flyweight
 享元模式为运用共享技术有效的支持大量细粒度的对象。因为它可以通过共享大幅度地减少单个实例的数目，避免了大量非常相似类的开销。大量应用于**各种池化技术**。

  享元模式是一个类别的多个对象共享这个类别的一个对象，而不是各自再实例化各自的对象。这样就达到了节省内存的目的。

7.代理模式 proxy

为其他对象提供一种，并由***对象控制对原对象的引用，以间接控制对原对象的访问。

### 依赖关系：

表现为函数中的参数，使用到其他类的方法，即依赖到其他类的定义。

具体可为：局部变量、方法的形参、静态方法的调用

```
class Driver {  
    //使用形参方式发生依赖关系  
    public void drive1(Car car){  
        car.run();  
    }  
    //使用局部变量发生依赖关系  
    public void drive2(){  
        Car car = new Car();  
        car.run();  
    }  
    //使用静态变量发生依赖关系  
    public void drive3(){  
        Car.run();  
    }  
}
```

关联关系（特殊的依赖关系）：是类的成员变量（has a）

比如人拥有身份证，身份证对应一个人

```
class Driver {  
    //使用成员变量形式实现关联  
    Car mycar=new Car();
}
```

聚合关系（较强的关联关系）：是类的成员变量，创建的时候可以不传入对象，通过setter传入对象

车由车轮组成，车没了，车轮可以单独存在

```
class Driver {  
	// 生命周期不一致
    Car mycar;  
    // setter方法中传入对象，实现聚合
    public void setCar(Car car){  
    	mycar = car;  
	}
}
```

组合关系（更强的关联关系）：是类的成员变量，通过构造传入对象，一起创建（生命周期一致）

人由头和驱干组成，人没了，头和驱干不存在

```
class Driver {  
	// 生命周期一致
    Car mycar;  
    // 构造方法中传入对象，实现组合
    public Driver(Car car){  
    	mycar = car;  
	}
}
```

has

dependency 依赖（ operation(a : A)       ）

aggregation  聚合（ a : A      setA(a : A)   ）

composite    组合（ a : A =new A ()          ）

尽量不用继承 is

![image-20211105110008109](javaNote.assets/image-20211105110008109.png)

![image-20211105111426234](javaNote.assets/image-20211105111426234.png)

##### 依赖（虚实线箭头）

![image-20211105195653326](javaNote.assets/image-20211105195653326.png)

##### 关联（实线箭头）

![2b0e58921503e32f3712e8311c1cf32](javaNote.assets/2b0e58921503e32f3712e8311c1cf32.png)

##### 聚合（整体和部分可分割）

![image-20211105194132626](javaNote.assets/image-20211105194132626.png)

##### 组合（不可分割）

![c2126cd4dc914f5dbba39b25be924fb](javaNote.assets/c2126cd4dc914f5dbba39b25be924fb.png)

迭代器

![image-20211127112616051](javaNote.assets/image-20211127112616051.png)

![image-20211127112809832](javaNote.assets/image-20211127112809832.png)

解释器：解析表达式，对于+-*使用不同的解释器

![image-20211127221150428](javaNote.assets/image-20211127221150428.png)

![image-20211127222328220](javaNote.assets/image-20211127222328220.png)

![image-20211127222841454](javaNote.assets/image-20211127222841454.png)

就是根据不同的需要，返回不同的解释器

![image-20211127222821309](javaNote.assets/image-20211127222821309.png)

![image-20211127223027855](javaNote.assets/image-20211127223027855.png)

## git

### rebase和merge区别

merge

只需解决一次冲突，产生一次合并冲突

![image-20210531151838328.png](javaNote.assets/e587fb1eba2a807440992fb0dd408aac.png)



rebase

你的提交记录更加清晰可读,rebase 翻译为变基，他的作用和 merge 很相似，用于把一个分支的修改合并到当前分支上。让master集成变支变基到当前分支上。

![WechatIMG2.png](javaNote.assets/3c4b8271175be2e7475db07b5de80533.png)

![img](javaNote.assets/1591949646655753.png)

```
特别注意，只能在自己使用的 feature 分支上进行 rebase 操作，不允许在集成分支上进行 rebase，因为这种操作会修改集成分支的历史记录。
```

### 添加两个远程仓库

```
同步方式
命令方式同步
先删除已关联的名为origin的远程库：

git remote rm origin
然后，再关联GitHub的远程库：

git remote add github git@github.com:chloneda/demo.git
接着，再关联码云的远程库：

git remote add gitee git@gitee.com:chloneda/demo.git

提交到github
git push github master
提交到码云
git push gitee master

箭头打不开
删除子文件夹里面的.git文件
执行git rm --cached [文件夹名]
```

### 标签管理和分支管理

```
git branch -r # 查看远程分支


1、打标签
$ git tag v1.0 (默认最新commit上)
3、创建带有说明的标签，其中-a指定标签名，-m指定说明的文字
$ git tag -a 标签名 -m '说明文字'

git tag 命令查看所有的标签

历史提交打标签
$ git tag v0.9 xxxxxxx # xxxxxxx表示刚才提交的commit id

2、查看标签信息
$ git show tagname # tagname表示标签的名字 例如：v0.9、v1.0



给历史提交打带有说明的标签
$ git tag -a 标签名 -m '说明文字' commitId # xxxxxxx表示需要打标签的
注意：标签总是和某个commit挂钩，如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签

4、删除tag

$ git tag -d v0.9
因为创建的标签都只存储在本地，不会自动推送到远程；所以，打错的标签可以在本地安全删除

5、推送标签至远程
$ git push origin v1.0 # 推送单个标签至远程
$ git push origin --tags # 一次性推送全部尚未推送到远程的本地标签

6、删除远程的标签
需要先从本次删除，删除本地的标签

$ git tag -d v1.0
然后从远程删除，删除命令也是push，格式如下

$ git push origin :refs/tags/v1.0

```

### 常用代码

```bash
#用于输出git提交日志 
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'

git config --global user.name “xxx”
git config --global user.email xxx@qq.com

查看配置信息
git config --global user.name
git config --global user.email

cd existing_git_repo
git remote rm origin
git remote add origin https://gitee.com/xxx/xxx.git

git add .
git commit -m “init my project”
git push --set-upstream origin master(重点)

#查看我的公匙
cd ~/.ssh
cat id_rsa.pub

#清除缓存（更新gitignore）
git rm -r --cached .

#查看本地分支
git branch

#查看远程分支
git branch -r

#切换分支
git checkout 分支名称

#创建新分支
git branch 新分支名称


#指定远程分支，和本地分支
git pull origin 远程分支名称:本地分支名称

```

**工作原理**

![image-20210910170432955](javaNote.assets/image-20210910170432955.png)

![image-20210910170800923](javaNote.assets/image-20210910170800923.png)

```bash
#用于输出git提交日志 
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
```

![image-20210910225804971](javaNote.assets/image-20210910225804971.png)

![image-20210910225843865](javaNote.assets/image-20210910225843865.png)

## HU

### 项目深挖

![image-20220414224059381](javaNote.assets/image-20220414224059381.png)

一、基于**Redis**实现社区模块的点赞评论功能，使用**Quartz**定时任务将缓存数据更新到MySQl 



贴子和评论都是下面这个套路：

1、list:area:id 最新的帖子，使用阻塞队列判断是否需要移除老的评论

2、zset:areaId 时间戳作为初始分值，点赞评论浏览增加权值

同时数据库持久化点赞和评论记录，评论会额外插入list中



点赞评论如何记录是谁，如何实时显示帖子的点赞和评论？

set保存点赞的人，防止重复点赞，后面拼接时间戳；点赞评论计数采用hash字段进行增加

评论数据使用list存起来



3、hash:area id:entity

使用list存最新的帖子，使用zset去维护帖子的热度，hash存实体。



如何保证热点数据？

使用阻塞队列异步删除数据，如果超过容量，删除后面的

同时每次访问会将**过期时间续命**



使用**Quartz**更新哪些数据到MySQl中 ？

帖子实体、点赞数据

评论是直接落库的，同时会存进list中



### 读写分离

```
1、AOP拦截dao层的方法，把读写类型存到threadLoacl中
2、继承AbstractRoutingDataSource，重写determineCurrentLookupKey动态切换数据源，通过threadLoacl获取需要的数据源
```

### es和mysql数据一致性

上面两种方案中都存在硬编码问题，也就是有任何对mysq进行增删改查的地方要么植入ES代码，要么替换为MQ代码，代码的侵入性太强。

如果对实时性要求不高的情况下，可以考虑用定时器来处理，具体步骤如下：

数据库的相关表中增加一个字段为timestamp的字段，任何crud操作都会导致该字段的时间发生变化；原来程序中的CURD操作不做任何变化；增加一个定时器程序（京东内部叫Worker），让该程序按一定的时间周期扫描指定的表，把该时间段内发生变化的数据提取出来；逐条写入到ES中。入下图所示

优点：

不改变原来代码，没有侵入性、没有硬编码；

没有业务强耦合；不改变原来程序的性能；

Worker代码编写简单不需要考虑增删改查。

缺点：

时效性较差，由于定时器工作周期不可能设在秒级，所以实时性没有上面2中好；

对数据库有一定的轮询压力，一种改进方法是将轮询放到压力不大的从库上。

### elk

日志整合es

https://www.cnblogs.com/kebibuluan/p/15933706.html

```

```

启动命令

```
D:/my-log/logstash-7.3.0/bin/logstash.bat -f ./config/my-log.conf

D:/app/logstash-7.3.0/bin/logstash.bat -f D:\app\logstash-7.3.0\config\kafka.conf
```



收集kafka中的日志

```
# Sample Logstash configuration for creating a simple
# Beats -> Logstash -> Elasticsearch pipeline.

input {
	kafka{
		bootstrap_servers =>["192.168.42.100:9092"]	
		group_id => "logstash_group"
		auto_offset_reset => "latest"
		consumer_threads => 5
		decorate_events => true # 记录kafka主题分区偏移量元信息
		topics => ["first"]
		type => "default"
		codec => json
	}
}

filter {
	   
}

# 输出信息到 es
output {
	elasticsearch {
		hosts => "192.168.42.100:9200"
		index => "job_kafka_%{+YYYY-MM-dd}"
		retry_on_conflict => 5
		document_id => "%{[@metadata][kafka][topic]}-%{[@metadata][kafka][partition]}-%{[@metadata][kafka][offset]}" #指定document_id，去重目的
		codec => plain { charset => "UTF-8" }
	}
}

```



收集文件my-log日志

```
# Sample Logstash configuration for creating a simple
# Beats -> Logstash -> Elasticsearch pipeline.

input {
  file {
    path => ["D:/my-log/*"]
  }
}

filter {
  grok {
    match => { "message" => "%{TIMESTAMP_ISO8601:datetime} (?<thread>(\[.*\])) %{DATA:level} %{DATA:class} - %{GREEDYDATA:message}" }
  }
mutate{
	gsub => ["thread","["",""],
	gsub => ["thread","]"",""]
}
}

# 输出信息到 es
output {
    if "_grokparsefailure" not in [tags]{ # grok匹配成功存es的info-表
        elasticsearch { 
            hosts => ["192.168.42.100:9200"] #配置Es地址
           index => "logstash-%{+YYYY.MM.dd}"        #配置es索引(表名)
        }
    } else { # grok匹配失败存es的error-表
        elasticsearch { 
            # host（同message配置）：string or array
            hosts => ["192.168.42.100:9200"] #配置Es地址
            index => "error-%{+YYYY.MM.dd}" #配置es索引(表名)
        }
    }
}

```



### es

1.综合社区帖子的热度和用户历史浏览搜索数据

1.1帖子的热度

点赞量和浏览量脚本算分

1.2用户历史浏览搜索数据：

存储帖子的tag字段和对应的区areaname

作为算分函数functions的过滤条件

```json
GET /question/_search
{
  "query": {
    "function_score": {
      "query": {
        "bool": {
          "should": [
            {
              "match": {
                "all": "区"
              }
            }
          ]
        }
      },
      "functions": [
        {
          "script_score": {
            "script": "_score + doc['likeCount'].value*10+doc['viewCount'].value"
          }
        },
        {
          "filter": {
            "term": {
              "areaName": "钓鱼区"
            }
          },
          "weight": 10
        },
        {
          "filter": {
            "terms": {
              "tag": [
                "c++;c"
              ]
            }
          },
          "weight": 10
        }
      ],
      "boost_mode": "avg"
    }
  },
  "from": 0,
  "size": 20, 
  "highlight": {
    "fields": [
      {
        "areaName": {
          "require_field_match": "false"
        }
      },
      {
        "title": {
          "require_field_match": "false"
        }
      },
      {
        "tag": {
          "require_field_match": "false"
        }
      },
      {
        "areaName": {
          "require_field_match": "false"
        }
      }
    ]
  }
}
```



```json
PUT /question
{
  "settings": {
    "analysis": {
      "analyzer": {
        "text_analyzer":{
          "tokenizer":"ik_max_word",
          "filter":"py"
        },
        "completion_anylyzer":{
          "tokenizer":"keyword",
          "filter":"py"
        }
      },
      "filter": {
        "py":{
          "type":"pinyin",
          "keep_full_pinyin": false,
          "keep_joined_full_pinyin": true,
          "keep_original": true,
          "limit_first_letter_length": 16,
          "remove_duplicated_term": true,
          "none_chinese_pinyin_tokenize": false
        }
      }
    }
  }, 
  "mappings": {
    "properties": {
      "id": {
        "type": "long"
      },
      "title": {
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart", 
        "copy_to": "all"
      },
      "description": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "createTime": {
        "type": "date"
      },
      "modifiedTime": {
        "type": "date"
      },
      "creatorId": {
        "type": "keyword"
      },
      "creatorName": {
        "type": "text",
        "analyzer": "text_analyzer"
      },
      "commentCount": {
        "type": "long"
      },
      "viewCount": {
        "type": "long"
      },
      "likeCount": {
        "type": "long"
      },
      "tag": {
        "type": "keyword",
        "copy_to": "all"
      },
      "sticky": {
        "type": "long"
      },
      "areaId": {
        "type": "long"
      },
      "areaName": {
        "type": "keyword",
        "copy_to": "all"
      },
      "img": {
        "type": "keyword"
      },
      "all":{
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart"
      },
      "suggestion":{
        "type": "completion",
        "analyzer": "completion_anylyzer"
      }
    }
  }
}
```



由于项目的功能模块众多，我们采用了微服务架构，有效的拆分了应用，实现敏捷开发和部署，各模块架构如下图。同时，采用Docker容器化部署个微服务应用，并使用Jenkins工具进行持续集成。

​                               

在项目的多个模块中，比如养聊站模块，由于帖子数量庞大，在分布式的场景下，采用普通的SQL检索遇到了很大的性能瓶颈。于是，我们引入了开源的分布式搜索引擎ElasticSearch，通过构建特定的索引，将MySQL中的数据批量导入ElasticSearch中，对外提供统一的全文检索服务，解决了系统海量数据的全文检索难点。

为缓解数据库的压力，在饮食运动养聊模块的数据读写都使用Redis作为缓存中间件，提高了系统的性能。同时，为解决高可用和海量数据读写问题，搭建了Redis的分片集群。

版本选择：

```
canal服务器·使用的是canal1.1.5

canal-adapter-1.1.6 es适配器
```

canal采用tcp模式，同时配备两个instance实例（example,rabbitmq），example实例负责同步es,rabbitmq实例同步redis缓存。

另外只同步health_community的中的community_question到es中

### 点赞评论模块

1、用户点赞

参数：用户id+帖子id

数据库实体：点赞记录表，帖子表点赞数增加

redis设计：hash存储questionLike，key(questionId::userId) value(1:tiemstamp)

2、用户评论：

参数：父评论id,帖子id,评论人id

数据库实体：评论表，帖子表评论数增加

redis设计：hash存储questionComment, key(questionId:userId:parentUserId:tiemStamp) value(comment)



用户评论->异步通知文章评论数加一-》持久化到数据库中

获取文章列表是用了缓存的，开启定时器，定期扫描去删除缓存

### canal订阅过滤规则

```
* a. 如果本次订阅中filter信息为空，则直接使用canal server服务端配置的filter信息
* b. 如果本次订阅中filter信息不为空，目前会直接替换canal server服务端配置的filter信息，以本次提交的为准
```

全库全表	

```
connector.subscribe(".*\\..*")
```

指定库全表	

```
connector.subscribe("test\\..*")
```

单表

```
connector.subscribe("test.user")
```

多规则组合使用

```
connector.subscribe("test\\..*,test2.user1,test3.user2")
```

### cannal server instance client概念

server-server 对应JVM,instance就是真正的数据队列，instance承载着EventParser(解析binlog),EventSink(过滤路由加工),EventStore（时间存储）

### canal高可用HA设计

通过多实例，创建成功就是对应的canal instance,失败就是standby备用状态。当实例消息，zookeeper会重新创建实例

1. canal server要启动某个canal instance时都先向zookeeper进行一次尝试启动判断 (实现：创建EPHEMERAL节点，谁创建成功就允许谁启动)
2. 创建zookeeper节点成功后，对应的canal server就启动对应的canal instance，没有创建成功的canal instance就会处于standby状态
3. 一旦zookeeper发现canal server A创建的节点消失后，立即通知其他的canal server再次进行步骤1的操作，重新选出一个canal server启动instance.
4. canal client每次进行connect时，会首先向zookeeper询问当前是谁启动了canal instance，然后和其建立链接，一旦链接不可用，会重新尝试connect.

Canal Client的方式和canal server方式类似，也是利用zookeeper的抢占EPHEMERAL节点的方式进行控制.

### canal实例只能被消费一次

一个canal实例（比如example）只能被消费一次

### canal执行流程

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2MDc5OTEy,size_16,color_FFFFFF,t_70.png)

### 认证逻辑

使用JWT+HMAC签名（哈希消息验证码(对称)）

对用户id和nickname进行加密，放入负载中，并签名

```java
/**
 * jwt使用rsa非对称加解密工具类
 */
public class JwtRsaUtil {
    private static final String SECRET="sdfdsfs"; // 密匙
    public static String generateJwtTokenHMAC(PayLoad userInfoPayLoad) throws UnsupportedEncodingException {
        Assert.notNull(userInfoPayLoad,"userInfoPayLoad不能为空");
        return  JWT.create()
                    .withIssuer("HU")
                    .withClaim("userInfo", JSON.toJSONString(userInfoPayLoad))
                    .sign(Algorithm.HMAC256(SECRET));
    }

    public static PayLoad getInfoFromToken(String token) throws NoSuchAlgorithmException, UnsupportedEncodingException {
        JWTVerifier verifier = JWT.require(Algorithm.HMAC256(SECRET))
                .withIssuer("HU")
                .build();
        DecodedJWT jwt = verifier.verify(token);
        Claim claim = jwt.getClaim("userInfo");
        String payload = claim.asString();
        PayLoad payLoad = JSON.parseObject(payload, PayLoad.class);
        return payLoad;
    }
}
```

### node版本

![image-20220624195541901](javaNote.assets/image-20220624195541901.png)

### 使用到的设计模式

### 哪里用到redis

##### 运动模块：运动运动小贴士

存储：hash  health:sport:type  id   typeEntity

并使用到了分布式锁

```java
public static final String SPORT_TYPE="health:sport:type";

    public static  final String TYPE_LOCK="lock:health:sport:type";

    /**
     * 获取运动小贴士，数据读多写少
     * 对象采用hash结构 health:sport:type  id   typeEntity
     * @param params
     * @return
     */
    @Override
    public PageUtils queryPage(Map<String, Object> params) {
        List<TypeEntity> entities= getRedis(params);
        if(entities==null){
            // 采用分布式锁，解决缓存击穿问题
            RLock lock = redissonClient.getLock(TYPE_LOCK);
            lock.lock(); // 休眠阻塞
            entities=getRedis(params); // 双检，别的线程可能已经获取到数据了
            if(entities==null){
                IPage<TypeEntity> page = this.page(
                        new Query<TypeEntity>().getPage(params),
                        new QueryWrapper<TypeEntity>()
                );
                entities=page.getRecords();
                saveToRedis(page); // 保存到缓存中
            }
            lock.unlock(); // 记得解锁
        }
        return new PageUtils(new Page<TypeEntity>(1,entities.size(),entities.size()).setRecords(entities));
    }

    private List<TypeEntity> getRedis(Map<String, Object> params) {
        BoundHashOperations<String, String, String> hashOps = redisTemplate.boundHashOps(SPORT_TYPE);
        List<String> values = hashOps.values();
        List<TypeEntity> entities=null;
        if(values!=null&&!values.isEmpty()){
            entities=values.stream().map(v-> JSON.parseObject(v,TypeEntity.class)).collect(Collectors.toList());
        }
        return entities;
    }


    private void saveToRedis(IPage<TypeEntity> page) {
        BoundHashOperations<String, String, String> hashOps = redisTemplate.boundHashOps(SPORT_TYPE);
        List<TypeEntity> entities = page.getRecords();
        for (TypeEntity entity : entities) {
            hashOps.put(entity.getId().toString(), JSON.toJSONString(entity));
        } // 这里不设置过期时间，因为每个人都要访问，且数据量不大
    }
```

## 大就业

### swagger

springboot 2.6.5 ✚ swagger 3.0.0配置属下

```
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.6.5</version>
</parent>
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-boot-starter</artifactId>
	<version>3.0.0</version>
</dependency>

```

application.yml 或applicaiton.properties 中添 必须 加如下配置

```
spring:
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher
```

只需要在启动类上加 `@EnableSwagger2` 注解即可
访问地址：http://127.0.0.1:88/swagger-ui/index.html

注解说明

```
@Api : 用在类上，说明该类的主要作用。

@ApiOperation：用在方法上，给API增加方法说明。

@ApiImplicitParams : 用在方法上，包含一组参数说明。

@ApiImplicitParam：用来注解来给方法入参增加说明。

@ApiResponses：用于表示一组响应。

@ApiResponse：用在@ApiResponses中，一般用于表达一个错误的响应信息

@ApiModel：用在返回对象类上，描述一个Model的信息（一般用在请求参数无法使用@ApiImplicitParam注解进行描述的时候）

@ApiModelProperty：描述一个model的属性
————————————————
版权声明：本文为CSDN博主「被子里」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/jjs15259655776/article/details/107753312
```



### 项目介绍

#### 1、如何缓存热点职位

hash结构存储职位所有信息

zset结构保存职位的热度

定期将zset中低热度的内容从hash中清除掉

使用淘汰策略，lru清除冷门数据

#### 2、热点职位

ZSet：job:hot     key(jobId)   score(时间戳+点击量)

Hash：job:entity    key(jobId)   value(jobEntity)



用户行为：浏览职位，投递职位

kafka对应三个话题：job-browse   job-delivery

每种都会增加职位的热度：一小时毫秒数，2小时



**如果一个用户点赞，那么****5****分钟内就不能在点赞了**

**新发布的职位也会缓存，****zset—****当前时间戳**

**Hset: jobId : jobEntity**

**Zset: jobId: timestamp+click** **以时间戳****+****浏览次数（每次加三分钟对应的秒数）**

#### 3、SpringSecurity逻辑

（1）重写 UsernamePasswordAuthenticationFilter的认证成功方法，生成token并把权限列表保存在redis;另外这里也可以自定义登录路径。

（2）重写BasicAuthenticationFilter的doFilterInternal授权方法，改为从根据token从redis中获取；

（3）在WebSecurityConfigurerAdapter添加自定义的过滤器；另外使用自定义的userDetailsService和PasswordEncoder

 

登录逻辑，先到health-acl进行登录服务，获取token（里面包含用户名，10分钟）

以后访问各个微服务，都要header都要携带token，不然访问失败

原理：在BasicAuthenticationFilter的doFilterInternal中，会根据token到redsis中获取权限列表，获取成功，放入到security上下文中

SecurityContextHolder.*getContext*().setAuthentication(authRequest)

#### 用户登录流程

调用接口

请求参数

后端逻辑：

（1）远程调用acl服务保存当前当前用户到acl-user（账号密码都是openid）,同时授予默认权限

（2）使用openId进行登录，同时返回token

返回当前用户

权限控制逻辑

（1）不登录也可以访问

（2）没有标注@PreAuth

需要先登录，但可以没有权限

（3）标注@PreAuth

要登录，并且有相应的权限

#### 接口幂等性

基于token机制+redis解决了页面重复提交问题

首先申请token，并把token存到redis中，页面请求的时候把在header中携带token,如果token存在则成功。然后先删除token，再保存数据。

先删Token还是先保存数据：采用先删token

如果保存数据失败，重新保存的时候只需要请求token即可

如果采用先保存数据，如果数据保存成功，删token删失败，那么还是会导致数据重复提交。

#### 聊天逻辑

再app.js中连接socket

message页面，订阅私人频道和公共频道

dialog页面：订阅私人频道，如果私人频道有消息且是当前对面，则队列增加消息。

在消息中在异步持久化

#### 用户信息解密

![img](javaNote.assets/531019-20161127000049065-2021089005.jpg)

### dubbo依赖

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

<!--    <parent>-->
<!--        <groupId>org.apache.dubbo.samples</groupId>-->
<!--        <artifactId>dubbo-spring-boot-service-introspection-zookeeper-samples</artifactId>-->
<!--        <version>2.7.10-SNAPSHOT</version>-->
<!--        <relativePath>../pom.xml</relativePath>-->
<!--    </parent>-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>2.3.0.RELEASE</version>
    </parent>

    <properties>
        <mybatisplus.version>3.3.1</mybatisplus.version>
    </properties>

    <groupId>com.lhf.dajiuye</groupId>
    <artifactId>dajiuye-job-service</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>dajiuye-job-service</name>
    <description>Demo project for Spring Boot</description>
    <dependencies>
        <!-- Spring Boot dependencies -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <dependency>
            <groupId>org.apache.dubbo</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>2.7.8</version>
        </dependency>

        <!-- Apache Zookeeper -->
        <dependency>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
            <version>3.4.8</version>
            <exclusions>
                <exclusion>
                    <groupId>org.slf4j</groupId>
                    <artifactId>slf4j-log4j12</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-x-discovery</artifactId>
            <version>4.3.0</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.53</version>
        </dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.3.7.RELEASE</version>
                <configuration>
                    <mainClass>com.lhf.dajiuye.job.service.DajiuyeJobServiceApplication</mainClass>
                </configuration>
                <executions>
                    <execution>
                        <id>repackage</id>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>

```



### app.js生命周期

```
　onLaunch 生命周期函数–监听小程序初始化 
　　当小程序初始化完成时，会触发 onLaunch（全局只触发一次）。

　　onShow  生命周期函数–监听小程序显示
　　当小程序启动，或从后台进入前台显示，会触发 onShow

　　onHide 生命周期函数–监听小程序隐藏
　　当小程序从前台进入后台，会触发 onHide

　　onError 错误监听函数
　　当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息
```

### 原生websocket

```
import {
    request
} from "../../requests/index.js";
Page({

    /**
     * 页面的初始数据
     */
    data: {
        userInfo: {},
        allMessage: [],
        isDisConnection:false//是否是手动断开锻炼
    },

    /**
     * 生命周期函数--监听页面加载
     */
    onLoad: function (options) {
        // this.startSetInter()
    },

    /**
     * 生命周期函数--监听页面显示
     */
    onShow: function () {
        const socketUrl = 'ws://127.0.0.1:9977/message-server/webSocketOneToOne/0/2'
        var that=this
        wx.connectSocket({
            url: socketUrl,
            success: function () {
                console.log('websocket连接成功~')
                wx.onSocketMessage((res) => {
                    //接收到消息
                    console.log("接收到消息" + JSON.stringify(res));
                })
                wx.onSocketOpen(() => {
                    console.log('WebSocket连接打开')
                    that.sendmsg()
                })
                wx.onSocketError((res) => {
                    console.log('WebSocket连接打开失败')
                    that.reconnect()
                })
                wx.onSocketClose((res) => {
                    console.log('WebSocket 已关闭！');
                    socketOpen = false;
                    if (that.data.isDisConnection) {
                        that.reconnect()
                    }
                })
            },
            fail: function () {
                console.log('websocket连接失败~')
            }
        })


        const userInfo = wx.getStorageSync('userInfo')
        if (!userInfo) {
            wx.switchTab({
                url: '../user/index', //注意switchTab只能跳转到带有tab的页面，不能跳转到不带tab的页面
            })
            wx.showToast({
                title: '请先登录',
                icon: 'none',
                image: '',
                duration: 1000,
                mask: false,
            });
            return;
        }
        this.setData({
            userInfo
        })
        this.setAllMessage(userInfo.openId)
    },

     /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {
    this.setData({
      isDisConnection:true
    })
    wx.closeSocket()
  },

    sendmsg(){
        console.log("准备发送消息")
        var message = {
            "msgContent": "asda",
            "targetId":"asdada"
          }
        wx.sendSocketMessage({
            data: JSON.stringify(message),
            success(res) {
              console.log("发送消息成功")
            },
            fail: function (e) {
                console.log(e)
                console.log("发送失败")
              }
          })
    },

    startSetInter: function () {
        var that = this;
        //将计时器赋值给setInter
        that.data.setInter = setInterval(
            function () {
                that.setAllMessage(that.data.userInfo.openId)
            }, 30000);
    },
    endSetInter: function () {
        var that = this;
        //清除计时器  即清除setInter
        clearInterval(that.data.setInter)
    },
    async setAllMessage(openId) {
        var that = this
        const result = await request({
            url: "/own/user/getAllMessage",
            data: {
                openId
            }
        });
        that.setData({
            allMessage: result
        })
    },
    setList(e) {
        console.log("hahah")
        console.log(e)
        wx.setStorageSync('msgs', this.data.allMessage[e.currentTarget.dataset.msgs])
        wx.navigateTo({ //---wx.  传当前页面的数据到另外一个页面！！！
            url: "/pages/dialog/index"
        })
    }
})
```

### 业务设计

#### 1、首页就是工作匹配，填好简历一键为你匹配职业；

#### 2、中间就是工作区，并加多一些筛选。

#### 3、我的 就基本没有变

#### 4、校招区 连list,list里面放校招图片，有筛选功能（右边弹出，有地区、字母排序），有搜索功能

#### 5、刷题区

### 小程序知识点

#### for循环

-    ```html
     微信小程序的for循环的选项是item,下标是index。
     <view wx:for="{{arr}}">
        <text>{{index}}--- {{item}}</text>
     </view>
     也可以指定遍历选项和下标的别名，
     指定遍历选项的别名：wx:for-item="xxx"　
     指定遍历下标的别名 ：wx:for-index="yyy"
     <!-- 给遍历的item指定别名，给遍历的下标指定别名 -->
     <view wx:for="{{arr}}" wx:for-item="testItem" wx:for-index="i">
       <text>{{testItem}} === {{i}}</text>
     </view>
     
     ```

#### 元素隐藏

- ```html
  wx:if="{{schoolObj.schImg3!==''}}"
  hidden="{{}}"
  style="display:none"
  style="opacity:{{opacity}}"
  ```

#### 两个页面间传递参数

- ```js
  //这里假设要把一个名为ob的对象进行传输
  	var str= JSON.stringify(ob);
     wx.navigateTo({
       url: '../要传递的页面/要传递的页面?str=' + str
     })
  ```

- ```js
  onLoad: function (options) {
      //将第一个页面中传过来的数据解析成对象放到onedata中
      var onedata = JSON.parse(options.str)
      //console.log(onedata)
      //之后进行使用即可
    }
  ```


#### 小程序调用组件的方法

- 假如我们已经有了一个自定义组件toast
  
  ![img](javaNote.assets/70.png)
  
  组件里面有个方法控制toast的显示
  
  ![img](javaNote.assets/70.png)
  
  假如我要在登录界面引用toast，那如何调用自定义组件的方法控制toast显示？
  
  1.首先在登录的json页面引用组件
  
  ![img](javaNote.assets/70.png)
  
  2.在登录的wxml页面引用组件（一定要设置id），这一步的<toast>标签名就是上一步引入组件时的key名，两者要保持一致
  
  ![img](javaNote.assets/70.png)
  
  3.在登录页的js页面的生命周期中获取组件（图中的传入的参数就是第2步设置的组件id）
  
  ![img](javaNote.assets/70.png)
  
  4.用(this.toast.方法名)即可调用自定义组件的方法
  
  ![img](javaNote.assets/70.png)
  
  5.参照以上方法基本上是能够调用的，如果调用过程中selectComponent返回null，你可以看看我的这篇文章，对这个问题进行了一些分析

#### 字符串

```
比较大小
str1.localeCompare(str2)
```



### 接口api

#### 1、轮播图

**简要描述**

- 轮播图

**请求URL**：

- ```
  http://localhost:8080/home/swiperdata
  ```

**请求方式：**

- GET

**请求头参数**：

**请求体参数**：

**返回示例：**

```json
{
    "message": [{
            "open_type": "navigate",
            "navigator_url": "/pages/goods_detail/main?goods_id=129",
            "goods_id": 129,
            "image_src": "https://img.coolcr.cn/2021/08/30/5a7136e08e6b7.jpg"
        },
        {
            "open_type": "navigate",
            "navigator_url": "/pages/goods_detail/main?goods_id=395",
            "goods_id": 395,
            "image_src": "https://img.coolcr.cn/2021/08/30/a1791fbe530e2.jpg"
        },
        {
            "open_type": "",
            "navigator_url": "",
            "goods_id": 0,
            "image_src": "https://img.coolcr.cn/2021/08/30/f0b258bd5c4ab.jpg"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

#### 2、分类导航图

**简要描述**

- 分类导航图

**请求URL**：

- ```
  http://localhost:8080/home/catitems
  ```

**请求方式：**

- GET

**请求头参数**：

**请求体参数**：

**返回示例：**

```json
{
    "message": [{
            "open_type": "switchTab",
            "navigator_url": "/pages/category/main",
            "name": "校招",
            "image_src": "https://img.coolcr.cn/2021/08/30/8b059d980545e.png"
        },
        {
            "open_type": "switchTab",
            "navigator_url": "/pages/category/main",
            "name": "实习",
            "image_src": "https://img.coolcr.cn/2021/08/30/8b059d980545e.png"
        },
        {
            "open_type": "switchTab",
            "navigator_url": "/pages/category/main",
            "name": "分类",
            "image_src": "https://img.coolcr.cn/2021/08/30/8b059d980545e.png"
        },
        {
            "open_type": "switchTab",
            "navigator_url": "/pages/category/main",
            "name": "定制",
            "image_src": "https://img.coolcr.cn/2021/08/30/8b059d980545e.png"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

#### 3、职位信息列表

**简要描述**

- 职位信息列表

**请求URL**：

- ```
  http://localhost:8080/home/jobdata
  ```

**请求方式：**

- GET

**请求头参数**：

**请求体参数**：

**返回示例：**

```json
{
    "message": [
        {
            "jobCreateTime": "2019/7/2",
            "jobAuthor": "",
            "jobComId": "jakd1a_asd",
            "jobField2": "短视频",
            "jobField1": "直播",
            "jobUpdateTime": "2019/2/3",
            "jobEdu": "本科",
            "jobPriority": "1",
            "jobName": "java开发工程师",
            "jobRequire1": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobSalary": "20k/月",
            "jobRequire2": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobRequire3": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobRequire4": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobComFinancing": "",
            "jobAge": "应届生",
            "jobImg": "http://asdkak.cja.com",
            "jobPlace": "广州深圳",
            "jobId": "asdadad",
            "schStat": "",
            "internshipTime": "5天/周",
            "schViewCnt": "",
            "jobComName": "",
            "jobDesc1": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc3": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc2": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc4": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；"
        },
        {
            "jobCreateTime": "2019/7/2",
            "jobAuthor": "",
            "jobComId": "jakd1a_asd",
            "jobField2": "短视频",
            "jobField1": "直播",
            "jobUpdateTime": "2019/2/3",
            "jobEdu": "本科",
            "jobPriority": "1",
            "jobName": "java开发工程师",
            "jobRequire1": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobSalary": "20k/月",
            "jobRequire2": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobRequire3": "",
            "jobRequire4": "掌握WEB后端开发技术: 协议、架构、存储、缓存、安全等；",
            "jobComFinancing": "",
            "jobAge": "应届生",
            "jobImg": "http://asdkak.cja.com",
            "jobPlace": "广州深圳",
            "jobId": "asdasdaasd",
            "schStat": "",
            "internshipTime": "5天/周",
            "schViewCnt": "",
            "jobComName": "",
            "jobDesc1": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc3": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc2": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；",
            "jobDesc4": "参与公司企业级产品后端的研发，确保系统的安全、高可用性和可靠性；"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

## 面试笔试

输入n,x求1，2，3..n中x出现的次数

### 自我介绍

面试官你好，我叫林涣锋，我来自东莞理工学院软件工程卓越计划班，我应聘的是贵公司的Java开发岗位

大学期间，我**参与开发了许多java相关的项目**，在其中主要负责项目的核心技术开发和系统架构，积累一定的项目实战开发能力，对项目的使用到的技术框架的有一定了解。

另外，我也多次参加计算机设计大赛，蓝桥杯算法竞赛等专业竞赛，积累了竞赛方面的相关经验。

在课内方面，我的计算机专业成绩优异，有获得奖学金

大学实践方面，我担任了校审计处学生助理，社会实践分队负责人，班级团支书等。

这就是我的自我介绍，感谢面试官。



自我介绍半分钟到一分钟

1.面试官懒得看简历，自己提炼特长

和职位匹配的经历

为什么你能胜任

求职动机

3个优势和亮点

例子：面试官你好，我叫林涣锋，来自东莞理工学院网络空间安全学院，华为一直是受人尊敬的公司，我这次应聘的职位是java后端开发的工作，从事后端开发的工作一直是我的梦想，为此，我大学期间很早就在结合岗位的要求做准备，包括对各种协议的熟悉，常见算法的实践等，在研究生两年的时间，我也重点选择了网络相关的课题进行研究，希望能加入公司，从事相关后端开发的工作，谢谢

我也一直在学习相关的

课代表来了（自己是在跟人打交道）
1、我是谁
2、亮点 有事实支撑的技能
3、亮点 你对工作的热情
4、亮点 为什么想要这份工作
5、自己适合这份工作的原因

扬长弊端

简历的中心思想和提纲

### 保融面试

1、如果用户下载的内容很大，超过内存怎么办

2、线程安全的对象

3、decimal原理

### 菜鸟面试

自我介绍，项目

为什么设计这个项目

怎么设计这个数据库，表怎么设计，主要表是什么

数据库存储引擎，innodb

索引B+的了解

Mysql的隔离级别

B+ 磁盘最小单位，对应表数据什么

Redis的使用场景

项目中哪些使用到redis了，怎么使用的

Redis宕机了怎么办

Rdb的了解

数据丢失怎么办

aof一定是100%数据不丢失吗

为什么一定要用redis

数据结构这方面的了解，根据时间复杂度对排序进行分类

问下图，如何生成最短路径

线程的整个生命周期，线程创建过程

Waiting time_waiting区别

反问：校招最考察什么

 

建议：打好基础，比如数据结构基础（图），redis，不一定要知识点有多广；数据库怎么设计之类的，有项目更好

其他：环境声音比较吵听不太清楚

**数据页中的记录按照「主键」顺序组成单向链表**

### 网易笔试题

\1.   进程调度算法

\2.   讲一讲你熟悉的一种设计模式

\3.   TCP三次握手种，Time_wait和close_wait的wait分别代表什么

Close_wait：服务端通知高层应用进程客户端要释放了，等待高层服务器关闭花费的时间，还没发完的数据在这段时间赶紧发

Time_wait：客户端等待，以确保服务器收到ACK真正关闭连接

\4.   删除倒数第n个结点

\5.   整数反转：123-》321

\6.   找出每个部门中工资最高的部门名称，员工名字，薪资

\7.   操作系统

\8.   时间片是1，一个进程有100个线程，那么该进程获取到的时间片为多少1

\9.   有静态代码块，有父类，然后调用子类方法，哪些代码块会执行

\10. 死锁的线程n,资源x,至少多少不会死锁

\11. 掩码为255.255.255.0有多少台主机

\1. 挖实习和项目
2.Java垃圾回收啥时候失败
3.Arrays.sort针对快排做了哪些优化
4.MySQL怎么看性能，怎么优化
5.ArrayList扩容机制
6.垃圾回收算法
7.项目代码里用的哪种垃圾回收算法
8.项目有没有用加密，怎么避免外网入侵
9.玩没玩过游戏
10.业务介绍和反问

## 错题集

### 磁盘启动

磁盘虽然是共享设备，但是对它进行**读写**操作的话必须先根据信息在磁盘上的指定位置，即**把磁盘移动到指定的柱面**，再等待指定的扇区旋转到磁头位置下。当**磁头在进行读写操作时不能随意地改变磁头的位置，否则会造成错误**。所以，磁盘虽是共享型设备，但任何时刻最多只能允许一个作业进行读写操作

![image-20220917145614166](javaNote.assets/image-20220917145614166.png)

### 导致创建新进程

引起创建进程的事件：

1、**用户登录**

2、作业调度

3、提供服务（用户程序提出请求）

4、应用请求（基于应用进程的需求）

![image-20220916215854033](javaNote.assets/image-20220916215854033.png)

### 内存管理-程序的链接和装入

一个进程在**被换出**之前所在的内存位置与后来被从外存重新调入内存时所在的内存位置不同

在这种情况下，**地址映射必须延迟到进程执行时再进行**，把这种装入方式称为**动态运行时装入（动态重定位)**。

动态重定位是在程序执行时对其发出的地址逐条进行翻译。因此，不论程序是否改变存放位置，只需要对翻译机制进行更新即可正确执行。

要保证一个程序在主存中被改变了存放位置后仍能正确执行，则对主存空间应采用（）

![image-20220916215042819](javaNote.assets/image-20220916215042819.png)

### 最大回文字串

![image-20220912153426646](javaNote.assets/image-20220912153426646.png)

### 线性函数

![img](javaNote.assets/d89a3c99a900823bc436ae4749ad2d1f.jpeg)

![image-20220912152831245](javaNote.assets/image-20220912152831245.png)

### 二维数组

![image-20220912114617971](javaNote.assets/image-20220912114617971.png)

### 操作系统-内存管理

[操作系统题库解析](https://www.doc88.com/p-1416198931851.html)

#### 改进CPU的利用率

![image-20220918105019220](javaNote.assets/image-20220918105019220.png)

![image-20220918105059604](javaNote.assets/image-20220918105059604.png)

#### 需要增加并发进程数的是

CPU利用率为13%，磁盘利用率为97%。时间都花在页面交换了，CPU使用率低，应增大内存或减少多道程序的度数（个数），度数少了每个分到的内存自然就多了。

CPU利用率为87%，磁盘利用率为3%。CPU一直在运行，很少的进程进行换入换出。系统正常。

CPU利用率3%，磁盘利用率3%。CPU利用率较低，且缺页现象不明显，可增加并发进程数，提高CPU利用率

![image-20220918104932591](javaNote.assets/image-20220918104932591.png)

![image-20220911221749497](javaNote.assets/image-20220911221749497.png)

### 定时器

![image-20220911202916304](javaNote.assets/image-20220911202916304.png)

### 优化道具购买

![image-20220911202846536](javaNote.assets/image-20220911202846536.png)

### 求阵型半径

![image-20220911202713431](javaNote.assets/image-20220911202713431.png)

### 唯一id生成

![image-20220911202637466](javaNote.assets/image-20220911202637466.png)

### 获取99%响应时间

![image-20220911202804632](javaNote.assets/image-20220911202804632.png)

### 概率

#### 小组赛

单循环赛：
单循环赛，是所有参加比赛的队均能相遇一次，最后按各队在全部比赛中的积分、得失分率排列名次。如果参赛队不多，而且时间和场地都有保证，通常都采用这种竞赛方法。
分析：
假设得分1分，那么你只能平一场和你打平得那一队也是平其他都输了，你们两队就都出局，
假设得分2的话那么其他和你打得两只队伍也是平那么它们都是1，然后和其他打输了，那两只队伍就只有1就被淘汰了。自己就出了

所以选择2分

![image-20220911110521043](javaNote.assets/image-20220911110521043.png)

### C&C++

#### char a[10],*p;p=a="china"错在哪了？

*符号，在定义的语句中，表示**声明了一个指针的类型**；
*符号，在赋值语句中，表示一个运算，**取这个变量的指向内容**

&就是取地址符

**p=a是对的**！也可以写成**p=&a[0]**
p是指针，指向一个地址，**数组名就是它的第一个元素的地址**。

a="china"把字符串赋值给一个地址，显然是**不对**的！
可以这样char
**a[10]="china",或是*p="china"**

#### 题目2

![image-20220911103212305](javaNote.assets/image-20220911103212305.png)

char a[]="abcdefg" ; 定义字符数组a，并将字符串abcdefg存储到该数组中，数组没有给定宽度，其宽度为abcdefg的长度+\0，即7+1=8.
可通过printf("%d", sizeof(a) ) ; 来输出其宽度。

A中a[10]已经声明了长度位10，后面a[]长度不能再变化了

#### 内存分几个区

![image-20220911103708900](javaNote.assets/image-20220911103708900.png)

内存到底分几个区？

1、栈区（stack）— 由编译器自动分配释放 ，存放函数的参数值，局部变量的值等。

2、堆区（heap） — 一般由程序员分配释放， 若程序员不释放，程序结束时可能由os回收 。注意它与数据结构中的堆是两回事，分配方式倒是类似于链表。

3、全局区（静态区）（static）—**全局变量和静态变量**的存储是放在一块的，初始化的全局变量和静态变量在一块区域， 未初始化的全局变量和未初始化的静态变量在相邻的另一块区域。程序结束后有系统释放。

4、文字常量区 — 常量字符串就是放在这里的。 程序结束后由系统释放。

5、程序代码区 — 存放函数体的二进制代码。

#### sizeof

[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)是连续的字符序列，最后以空字符'\0'作为终止符。一个字符串的长度指所有字符的数量，但**不包括终止符**。

char str1[30] = "Let's go"; // 字符串长度：8；数组长度：30

**在32位系统上，对任意指针求sizeof，得到的结果都是4**

**在64位系统上，对任意指针求sizeof，得到的结果都是8**

![image-20220911110335295](javaNote.assets/image-20220911110335295.png)

### 数据结构时间复杂度

![image-20220910170124402](javaNote.assets/image-20220910170124402.png)

### 进程内存空间

函数参数，局部变量自动分配在栈上。

栈上的内存随着方法出栈内存就释放了，不会造成泄露

![image-20220908220759844](javaNote.assets/image-20220908220759844.png)

### unicode

![image-20220907230513829](javaNote.assets/image-20220907230513829.png)

### 改善磁盘设备的IO性能

```
重排IO请求次序
预读和滞后写
优化文件物理块的分布
```

![image-20220907225901136](javaNote.assets/image-20220907225901136.png)

### linux文件权限

![image-20220905215738429](javaNote.assets/image-20220905215738429.png)

### extend&super

```
/**
 * List<? super A>： A和A的父类
 * List<? extends A>： A和A的子类对象
 */
```

![image-20220905212531645](javaNote.assets/image-20220905212531645.png)

### 常用函数式接口

- Supplier
- Comsumer
- Predicate
- Function

### 基本数据类型

![image-20220904222218770](javaNote.assets/image-20220904222218770.png)

### JUC工具类

![image-20220903173208382](javaNote.assets/image-20220903173208382.png)

### 字符匹配复杂度

![image-20220903172030469](javaNote.assets/image-20220903172030469.png)

### 线性链表

![image-20220903172007865](javaNote.assets/image-20220903172007865.png)

### RestFul&RPC

1、RESTful是一种软件**约束风格**，用于约束客户端和服务器交互，满足这些约束条件和原则的应用程序或设计就是 RESTful。比如HTTP协议使用同一个URL地址，通过GET，POST，PUT，DELETE等方式实现查询、提交、删除数据。

2、RPC是远程过程**调用模型**，是用于解决分布式系统服务间调用的一种方式。RPC采用客户端与服务端模式，双方通过约定的接口（常见为通过IDL定义或者是代码定义）以类似本地方法调用的方式来进行交互，客户端根据约定传输调用函数+参数给服务端（一般是网络传输TCP/UDP），服务端处理完按照约定将返回值返回给客户端。

可分为两大部分RPC +服务治理
RPC部分 = IDL  +客户端/服务端实现层 +协议层 +数据传输层
服务治理 =服务管理（注册中心） +服务监控 +服务容灾 +服务鉴权

### Service Mesh

Service Mesh为了**解决传统微服务框架"胖客户端"**方式，引入的如下问题：
与业务无关的服务治理逻辑与业务代码强耦合，框架、SDK的升级与业务代码强绑定，多语言的胖客户端支持起来性价比极低。

Service Mesh又译作“**服务网格**”，作为**服务间通信的基础设施层**， 作为下一代微服务技术。负责服务之间的网络调用、限流、熔断和监控，对于编写应用程序来说一般无须关心这一层。

微服务 (Microservices) 是一种软件架构风格，它是以专注于单一责任与功能的小型功能区块 (Small Building Blocks) 为基础，利用模块化的方式组合出复杂的大型应用程序，各功能区块使用与***语言无关\*** (Language-Independent/Language agnostic) 的 API 集相互通信。

![image-20220827132204615](javaNote.assets/image-20220827132204615.png)

### spring

![image-20220823172923728](javaNote.assets/image-20220823172923728.png)

### 二叉树

![image-20220823105842021](javaNote.assets/image-20220823105842021.png)

解法一：

（１）二叉树性质

２、总结点数＝各结点度之和＋１（ｎ＝ｎ0＊0＋ｎ1＊1＋ｎ2＊2＋１）

３、叶子节点数＝度为２的结点数＋１（ｎ0＝ｎ2＋1）

已知该完全二叉树叶子节点数为124，即可得完全二叉树ｎ2＝ｎ0－１＝123

（2）完全二叉树性质

１、完全二叉树，度为１的结点数不是0就是1

２、深度为ｈ的完全二叉树，１～h－１层必定是满的，且第ｈ层结点集中在左侧

完全二叉树最多结点数ｎ＝ｎ0＋ｎ1＋ｎ2＝124＋１＋123＝248

解法二：

（１）完全二叉树叶子节点数为124个，即可推导出最底层深度为8，且第8层最多可有128个叶子节点（128－124＝4，即最右侧分布4个节点）

（２）此时有两种情况，第一种。上一层最右侧的4个节点都是叶子节点，第二种，最右侧3个叶子节点＋其中一个靠左的叶子节点存在一个左节点

（３）显然第二种情况节点数是最多的，１～７层共127个节点、第8层有121个叶子节点，共127＋121＝248

### 双向链表

![image-20220823102532982](javaNote.assets/image-20220823102532982.png)

### 地址

![image-20220823102309228](javaNote.assets/image-20220823102309228.png)

### 编译

java程序编译后结果不一定只有一个

![image-20220820211633278](javaNote.assets/image-20220820211633278.png)

```
22.下列说法中，不正确的是_B。

A．一个java源程序经过编译后，得到的文件的扩展名一定是.class
B．一个java源程序编译通过后，得到的结果文件数也只有一个
C．一个java源程序只能有一个public class类定义，且源文件的名字与public class的类名相同，扩展名必须是.java
D．一个java源程序可以包含多个class类

答案：B
难度等级：简单
解析：
一般情况下一个Java文件代表一个类，在编译时会产生一个字节码.class文件。
但是在Java中 一个源文件中可以包含多个类，但是只能有一个public类，其他的都成为内部类，这时编译时会生成多个字节码文件。一个是那个public类也是该源文件名对应的.class 另一个就是public类名$内部类名.class
```

![image-20220820211411949](javaNote.assets/image-20220820211411949.png)

### 类成员

静态的才属于类成员

![image-20220820183143933](javaNote.assets/image-20220820183143933.png)

### 概率题

![image-20220818182336023](javaNote.assets/image-20220818182336023.png)

![image-20220805160039622](javaNote.assets/image-20220805160039622.png)

### 海量数据

[海量数据](https://www.nowcoder.com/jump/super-jump/word?word=海量数据)中找出重复次数最多的一个/前N个数据，我们的解决方法是： **分而治之/Hash映射 + HashMap/前缀树统计频率 + 堆/快速/归并[排序](https://www.nowcoder.com/jump/super-jump/word?word=排序)**

#### 一、海量日志数据，提取出某日访问[百度]()次数最多的IP。 

1、通过hash算法%1000把每个ip分到小文件中（同个ip一定会分到同个文件）

2、找出每个文件次数最多的ip（hash/堆）

3、对这1000个再进行堆排序

 假设内存无穷大，我们可以用常规的HashMap(ip，value)来统计ip出现的频率，统计完后利用[排序]()[算法]()得到次数最多的IP，这里的[排序]()[算法]()一般是堆[排序]()或快速[排序]()。 

 但考虑实际情况，我们的内存是有限的，所以无法将海量日志数据一次性塞进内存里，那应该如何处理呢？很简单**，分而治之**！即将这些IP数据**通过Hash映射[算法]()划分为多个小文件**，比如模1000，把整个大文件映射为1000个小文件，再找**出每个小文件中出现频率最大的IP**，最后在这1000个最大的IP中，找出那个频率最大的IP，即为所求（是不是很像Map Reduce的思想？）。 

 这里鬼仔再多说一句：Hash取模是一种等价映射[算法]()，不会存在同一个元素分散到不同小文件中的情况，这保证了我们分别在小文件统计IP出现频率的正确性。我们对IP进行模1000的时候，**相同的IP在Hash取模后，只可能落在同一个小文件中，不可能被分散的**。因为如果两个IP相等，那么经过Hash(IP)之后的哈希值是相同的，将此哈希值取模（如模1000），必定仍然相等。 

 总结一下，该类题型的解决方法分三步走： 

1.  分而治之、hash映射； 
2.  HashMap（或前缀树）统计频率； 
3.  应用[排序]()[算法]()（堆[排序]()或快速[排序]()）。 

 如果将题目改为：海量日志数据，提取出某日访问[百度]()次数最多的前N个IP。牛油们知道怎么处理吗？把答案写在评论区吧～ 

####  二、搜索引擎会通过日志文件把用户每次检索使用的所有查询串都记录下来，每个查询长度不超过 255 字节。假设目前有一千万个记录（这些查询串的重复度比较高，虽然总数是1千万，但如果除去重复后，不超过3百万个。一个查询串的重复度越高，说明查询它的用户越多，也就是越热门），请你统计最热门的10个查询串，要求使用的内存不能超过1G。 

 我们首先分析题意：一千万个记录，除去重复后，实际上只有300万个不同的记录，每个记录假定为最大长度255Byte，则最多占用内存为：3M*1K/4=0.75G<1G，完全可以将所以查询记录存放在内存中进行处理。相较于第一道题目，这题还更简单了，直接HashMap（或前缀树）+堆[排序]()即可。 

 具体做法如下： 

1.  遍历一遍左右的Query串，利用HashMap（或前缀树）统计频率，时间复杂度为O(N)，N=1000万； 
2.  建立并维护一个大小为10的最小堆，然后遍历300万Query的频率，分别和根元素（最小值）进行对比，最后找到Top K，时间复杂度为N‘logK，N‘=300万，K=10。 

####  三、有一个1G大小的一个文件，里面每一行是一个词，词的大小不超过16字节，内存限制大小是1M。返回频数最高的100个词。 

 经过前两道题的训练，第三道题相信大家已经游刃有余了，这类题型都有相同的特点：文件size很大，内存有限，解决方法还是经典三步走：分而治之 + hash统计 + 堆/快速[排序]()。 

 具体做法如下： 

1.  分而治之、hash映射：遍历一遍文件，对于每个词x，取hash(x)并模5000，这样可以将文件里的所有词分别存到5000个小文件中，如果哈希函数设计得合理的话，每个文件大概是200k左右。就算其中有些文件超过了1M大小，还可以按照同样的方法继续往下分，直到分解得到的小文件的大小都不超过1M； 
2.  HashMap（或前缀树）统计频率：对于每个小文件，利用HashMap（或前缀树）统计词频； 
3.  堆[排序]()：构建最小堆，堆的大小为100，找到频率最高的100个词。 

####  四、给定a、b两个文件，各存放50亿个url，每个url各占64字节，内存限制是4G，让你找出a、b文件共同的url？ 

 每个url是64字节，50亿*64=5G×64=320G，内存限制为4G，所以不能直接放入内存中。怎么办？分而治之！ 

 具体做法如下： 

1.  遍历文件a中的url，对url进行hash(url)%1000，将50亿的url分到1000个文件中存储（a0，a1，a2.......），每个文件大约300多M，对文件b进行同样的操作，因为**hash函数相同，所以相同的url必然会落到对应的文件中**，比如文件a中的url1与文件b中的url2相同，那么它们经过hash(url)%1000也是相同的。即url1落入第n个文件中，url2也会落入到第n个文件中。 
2.  遍历a0中的url，存入HashSet中，同时遍历b0中的url，查看是否在HashSet中存在，如果存在则保存到单独的文件中。然后以此遍历剩余的小文件即可。 

 小结 

  讲完了这四道例题，我们再来总结一下，这几道题都有一个共性， **那就是要求在[海量数据]()中找出重复次数最多的一个/前N个数据**，我们的解决方法也很朴实： **分而治之/Hash映射 + HashMap/前缀树统计频率 + 堆/快速/归并[排序]()**，具体来说就是先做hash，然后求模映射为小文件，求出每个小文件中重复次数最多的一个，并记录重复次数，最后利用堆这个数据结构高效地取出前N个出现次数最多的数据。

### 计算题

![image-20220808211943578](javaNote.assets/image-20220808211943578.png)

![image-20220808211800882](javaNote.assets/image-20220808211800882.png)

![image-20220808211709231](javaNote.assets/image-20220808211709231.png)

![image-20220808211636249](javaNote.assets/image-20220808211636249.png)

![image-20220808211606654](javaNote.assets/image-20220808211606654.png)

![image-20220808211522890](javaNote.assets/image-20220808211522890.png)

![image-20220808211422514](javaNote.assets/image-20220808211422514.png)

![image-20220808211349049](javaNote.assets/image-20220808211349049.png)

![image-20220808211249411](javaNote.assets/image-20220808211249411.png)

![image-20220808211026295](javaNote.assets/image-20220808211026295.png)

![image-20220808210655898](javaNote.assets/image-20220808210655898.png)

![image-20220805142806340](javaNote.assets/image-20220805142806340.png)

![image-20220805142757661](javaNote.assets/image-20220805142757661.png)

![image-20220805141313413](javaNote.assets/image-20220805141313413.png)

### 分段机制

![image-20220804221551892](javaNote.assets/image-20220804221551892.png)

### 引起进程调度

只要是就绪状态就可能发生进程调度



**进程调度的定义**：进程调度的主要功能是按照一定的策略**选择—个处于就绪状态的进程，使其获得处理机执行**；

然后找是不是就绪状态即可

C不是就绪状态，所以C；



就绪状态 >>> 运行状态 (这个过程会出现任务调度)

A. 当任务完成之后，就会从从运行状态转换为就绪状态。

B.当进程访问临界区时，其他进程加锁，那么他就处于就绪状态,当其他程序释放所之后，他就会进入运行状态

C.当一个进程执行了一条转移指令后，这里我们举例：中断就是一个转移指令，当我们产生中断时程序会从运行状态变为阻塞状态，并不会引起任务调度

D.当我们创建一个新的进程时，新的进程处于就绪状态

![image-20220804220621840](javaNote.assets/image-20220804220621840.png)

![image-20220804221105424](javaNote.assets/image-20220804221105424.png)

### 不可重复读和幻读

不可重复读

在一个事务内**多次读取同一个数据，如果出现前后两次读到的数据不一样**的情况，就意味着发生了「不可重复读」现象。

幻读

在一个事务内多次查询某个**符合查询条件**的「记录数量」，如果出现前后两次查询到的记录数量不一样的情况，就意味着发生了「幻读」现象。

![image-20220727215714721](javaNote.assets/image-20220727215714721.png)

### 出栈顺序

![image-20220727215511652](javaNote.assets/image-20220727215511652.png)

### 快排

没经过一躺排序，会有一个元素的位置被确定，当然大于左边小于右边

![image-20220727215109026](javaNote.assets/image-20220727215109026.png)

### 编码表

```
EF BF BD EF BF BD
对应的2进制编码是(这里我们分成了两段,取其中一段进行分析)
EF BF BD :11101111 10111111 10111101
                  ↑↑↑↑         ↑↑             ↑↑
根据图可知是第三种情况去掉前缀(上面箭头的指的地方就是前缀)后是：
1111 1111 1111 1101
 转成十六进制即是 FFFD
第二段相同的同理
```

![image-20220727204826701](javaNote.assets/image-20220727204826701.png)

### 缺页中断

注意是FIFO，不是LRU

缺页中断，看清题目，刚开始的三个页应该也需要算进去。如果是页面置换的次数就不用算前面三个页。

![image-20220726095758998](javaNote.assets/image-20220726095758998.png)

![image-20220726095747779](javaNote.assets/image-20220726095747779.png)

### 并发作业时间计算

计算的时候可以输入，输出的时候可以计算，所以最后应该是2+3+4+4+4=17

![img](javaNote.assets/873BD1D3B29C7117FB7014BCBD9D1114.png)

![image-20220726094848711](javaNote.assets/image-20220726094848711.png)

### Integer不可变类

```
Integer和String一样是final修饰的最终类，因此也是不可变性
```

![image-20220722102744597](javaNote.assets/image-20220722102744597.png)

### mount

-r: 将文件系统作为**只读文件**系统进行**安装**，而不考虑它先前在 /etc/file systems 文件中指定的内容或者先前的任何命令行选项。
ro : 将**已安装**的文件指定为**只读文件**，而不考虑它先前在 /etc/file systems 文件中指定的选项或者先前的任何命令行选项。缺省值是 rw。

![image-20220721174702441](javaNote.assets/image-20220721174702441.png)

### 值&引用类型

```
实例是针对于对象的概念，当类实例化为对象的时候，这个时候可以称为是类的一个实例。
封装的概念也是针对类而言的，值类型数据不存在封装概念。
值类型变量可以作为成员变量存储在堆里，例如一个Class A中包含一个int value，那么value是作为成员变量存储在堆中的。
```

![img](javaNote.assets/243827773_1597801988854_CDC679BEBBE282E170AB6FE0DCA8445E.jpeg)

![image-20220720225827802](javaNote.assets/image-20220720225827802.png)

### 增量模型

```
增量模型是把待开发的软件系统模块化，将每个模块作为一个增量组件，从而分批次地分析、设计、编码和测试这些增量组件。运用增量模型的软件开发过程是递增式的过程。

相对于瀑布模型而言，采用增量模型进行开发，开发人员不需要一次性地把整个软件产品提交给用户，而是可以分批次进行提交。
```

![image-20220720225434257](javaNote.assets/image-20220720225434257.png)

### 砝码称重

```
9个分为3个，那边轻就在哪边，不然就在第三组。
```

![image-20220716173432878](javaNote.assets/image-20220716173432878.png)

### Java基础

```
x++ +先计算+
```

![image-20220715223234774](javaNote.assets/image-20220715223234774.png)

```
byte b1=1,b2=2,b3,b6; 
final byte b4=4,b5=6; 
b6=b4+b5; 
b3=(b1+b2); 
System.out.println(b3+b6);

被final修饰的变量是常量，这里的b6=b4+b5可以看成是b6=10；在编译时就已经变为b6=10了

而b1和b2是byte类型，java中进行计算时候将他们提升为int类型，再进行计算，b1+b2计算后已经是int类型，赋值给b3，b3是byte类型，类型不匹配，编译不会通过，需要进行强制转换。

Java中的byte，short，char进行计算时都会提升为int类型。

```

![image-20220713091915706](javaNote.assets/image-20220713091915706.png)

### 数据库

![image-20220707170956420](javaNote.assets/image-20220707170956420.png)

![image-20220707170937656](javaNote.assets/image-20220707170937656.png)



题目是小于连接，答案×表示笛卡尔积，对应的属性位置为1，4

![image-20220707164346480](javaNote.assets/image-20220707164346480.png)

### pctfree&pctused

![image-20220707112841396](javaNote.assets/image-20220707112841396.png)

```
pctfree:当空闲空间占比低于pctfree，就会把当前块移除空闲链表freelist，可以被insert
pctused:当使用率小于pctused会重新加入空闲链表。

pctfree默认是10，pctused默认是40，且规定pctfree+pctused < 90
此道题A、D大于90排除，又因为字段中有大量空值，为保证后续空间有足够空间更新，需要增大空闲比率，所以选B
```

### 二分查找

最差O(n)

### 时间片轮转

```
先来先服务算法, 有利于CPU密集型作业, 不利于IO密集型作业
因为CPU密集型说明会长时间占用CPU，进程IO中断让出CPU,排到队尾，那么就得等很长时间才能被重新调度



时间片轮转算法, 有利于cpu密集型作业, 不利于io密集型作业
```

### 时间复杂度递推方程

设某算法的时间复杂度函数的递推方程是 T(n) = T(n - 1) + n（n 为正整数）及 T(0) = 1，则该算法的时间复杂度为n^2

```
T(n-1)+n=T(n-2)+n-1+n=T(n-3)+n-2+n-1+n=(1+n)n/2=n^2
```

### HTTP报文

HTTP响应报文由三部分组成，
响应行：由报文协议及版本、状态码及描述组成。
响应头：和请求头一样，由属性组成。
响应体：是服务器返回给客户端的文本信息。

### 两个栈模拟队列

用俩个栈模拟实现一个队列，如果栈的容量分别是O和P(O>P),那么模拟实现的队列最大容量是多少？

**2p+1**，O中还可一个存一个，即可满足先进先出的特点

选取较大O作为缓冲区，先入栈p个元素，再全部出栈到p中，再把O入栈p+1个元素。

此时就得p先出栈，再把O中p个元素放到p中，然后O先出栈，再p出栈

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NDUzE5OTQxMQ==,size_16,color_FFFFFF,t_70.png)

![在这里插入图片描述](javaNote.assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1NDUzE5OTQxMQ==,size_16,color_FFFFFF,t_70-165796369442714.png)

https://blog.csdn.net/SCS199411/article/details/91443928

### 笔试题

java的继承，构造方法谁先执行，初始化

bufferReader继承自谁

0xf00和0x111之类相加减

从高度a下落，每次回到前一次的一半，问第b次到地面走了多少米

无序数组，三数之和等于0

一定要有构造方法嘛，普通方法可以跟类重名吗

#### 网站运营商广告

DNS劫持或HTTP劫持
DNS劫持:访问马化腾的网站，返回了运营商的中间服务器IP。访问该ip一致性**返回302**临时重定向，跳转至预处理的网页，在这个网页上再打开原网页的内容
HTTP劫持：一种是类似DNS的302，一种是js插入广告

实例方法调超类

![image-20220425113832022](javaNote.assets/image-20220425113832022.png)

### 精度转换

int x=1;float y=2; 求x/y 自动转为精度高的

```
int x=1;
float y=2;
System.out.println(x/y); // 0.5
```

## Nginx

#### 简介

![image-20220521161703247](javaNote.assets/image-20220521161703247.png)

#### 反向代理

![image-20220521161921323](javaNote.assets/image-20220521161921323.png)



#### 简单调优



![image-20220521161944254](javaNote.assets/image-20220521161944254.png)



**内核网络参数**

![image-20220521162240725](javaNote.assets/image-20220521162240725.png)



**提升网络效率**

![image-20220521162254181](javaNote.assets/image-20220521162254181.png)

```
server
{
    listen 80;
    server_name 47.106.21.242;

    include enable-php-56.conf;
    
    include 		/www/server/panel/vhost/rewrite/47.106.21.242.conf;

    location / {
    	    index  index.html;
    		alias /www/wwwroot/http;
    }
    access_log  /www/wwwlogs/47.106.21.242.log;
    error_log  /www/wwwlogs/47.106.21.242.error.log;
}
```

#### dockercompose

```
version: '3.1'
services:
    nginx:
        image: nginx:1.21.6-alpine     # 镜像名称
        container_name: nginx     # 容器名字
        restart: always     # 开机自动重启
        ports:     # 端口号绑定（宿主机:容器内）
            - '80:80'
            - '443:443'
        volumes:      # 目录映射（宿主机:容器内）
            - ./conf/nginx.conf:/etc/nginx/nginx.conf
            - ./conf.d:/etc/nginx/conf.d
            - ./html:/usr/share/nginx/html
            - ./ssl:/etc/ssl
```

#### default.conf

```
server {                                                                                                                                                                                                         
    listen       80;                                                                                                                                                                                             
    listen  [::]:80;                                                                                                                                                                          
    #access_log  /var/log/nginx/host.access.log  main;                                                                                                                                                           
    location / {                                                                                 
        root   /usr/share/nginx/html;                                                                       
        index  index.html index.htm;                                                                                                                                                                             
    }                                                                                                   
    #error_page  404              /404.html;                                                                            
    # redirect server error pages to the static page /50x.html                                                                                             
    error_page   500 502 503 504  /50x.html;                                                                                                                                                                     
    location = /50x.html {                                                                              
        root   /usr/share/nginx/html; 
    }                                                                                               
    # proxy the PHP scripts to Apache listening on 127.0.0.1:80                                                                                                 
    #location ~ \.php$ {                                                                      
    #    proxy_pass   http://127.0.0.1;  
    #}                                                                                              
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000                                                                           
    #location ~ \.php$ {                                                                                    
    #    root           html;                                                                               
    #    fastcgi_pass   127.0.0.1:9000;               
    #    fastcgi_index  index.php;                                                                        
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;     
    #    include        fastcgi_params;      
    #}                                                                                
    # deny access to .htaccess files, if Apache's document root    
    # concurs with nginx's one                                                                             
    #location ~ /\.ht {     
    #    deny  all;                                                                                     
    #}           
}
```

#### nginx.conf

```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024; 
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}

```

#### 配置文件

```
events{
	accept_mutex on; # 惊群
	multi_accept on; 
	worker_commections 1024; # 单个worker的最大连接数
	use epoll;
}
```





#### 浏览器的缓存

![image-20211211200057006](javaNote.assets/image-20211211200057006.png)

### Kafka



## RabbitMQ

### 如何保证消息可靠性

- 生产者确认机制confirmCallback（通过confirm回调的result判断结果）和returnCallBack（消息到达队列失败触发的回调）
- 生产者事务
- 消息持久化
- 消费者确认
- 失败重试

#### 1、生产者确认

confirmCallback和returnCallback

生产者将[信道](https://so.csdn.net/so/search?q=信道&spm=1001.2101.3001.7020)设置成`confirm`模式，一旦信道进入`confirm`模式，所有在该信道上面发布的消息都会被指派一个唯一的id(从1开始)，一旦消息被投递到匹配的队列之后，rabbitmq就会发送一个确认(`Basic.Ack`)和`deliverTag`(消息id)给生产者。

如果消息和队列是持久化的那么消息会在持久化之后被发出。rabbitmq除了回传`deliverTag`之外，还有`multiple`参数，表示到这个序号之前所有的消息都得到了处理。所有的消息只会被`Ack`或`Nack`一次，不会出现既被`Ack`又被`Nack`

消息没没有到达交换机，通过**confirmCallback**的result获取，Nack表现没有正常到达队列

```java
		// 1.准备消息
        String message = "hello, spring amqp!";
        // 2.准备CorrelationData
        // 2.1.消息ID
        CorrelationData correlationData = new CorrelationData(UUID.randomUUID().toString());
        // 2.2.准备ConfirmCallback
        correlationData.getFuture().addCallback(result -> {
            // 判断结果
            if (result.isAck()) {
                // ACK
                log.debug("消息成功投递到交换机！消息ID: {}", correlationData.getId());
            } else {
                // NACK
                log.error("消息投递到交换机失败！消息ID：{}", correlationData.getId());
                // 重发消息
            }
        }, ex -> {
            // 记录日志
            log.error("消息发送失败！", ex);
            // 重发消息
        });
        // 3.发送消息
        rabbitTemplate.convertAndSend("amq.topic", "a.simple.test", message, correlationData);
```

消息到达交换机但**没到达队列**，触发**returnCallback**

```java
        // 配置ReturnCallback,消息到达队列失败触发
        rabbitTemplate.setReturnCallback((message, replyCode, replyText, exchange, routingKey) -> {
            // 判断是否是延迟消息
            Integer receivedDelay = message.getMessageProperties().getReceivedDelay();
            if (receivedDelay != null && receivedDelay > 0) {
                // 是一个延迟消息，忽略这个错误提示
                return;
            }
            // 记录日志
            log.error("消息发送到队列失败，响应码：{}, 失败原因：{}, 交换机: {}, 路由key：{}, 消息: {}",
                     replyCode, replyText, exchange, routingKey, message.toString());
            // 如果有需要的话，重发消息
        });
```

#### 2、事务机制

rabbitmq与事务相关的方法:

- `channel.txSelect()`: 将当前信道设置成事务模式
- `channel.txCommit()`: 用于提交事务
- `channel.txRollback()`: 用于回滚事务

**通过事务实现机制，只有消息成功被rabbitmq服务器接收，事务才能提交成功，否则便可在捕获异常之后进行回滚，然后进行消息重发，但是事务非常影响rabbitmq的性能。还有就是事务机制是阻塞的过程，只有等待服务器回应之后才会处理下一条消息**

示例：

```java
public class TransactionSender {


    private static final String ex_name = "ex_tx";
    private static final String q_name = "q_tx";
    private static final String rt_name = "rt_tx";

    public static void main(String[] args) throws IOException, TimeoutException {

        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();

        channel.exchangeDeclare(ex_name, BuiltinExchangeType.DIRECT);
        channel.queueDeclare(q_name, false, false, false, null);
        channel.queueBind(q_name, ex_name, rt_name);

        channel.txSelect();
        try {
            channel.basicPublish(ex_name, rt_name, null, "hello".getBytes());
            //显示抛出RuntimeException
            int a = 1/0;
            channel.txCommit();
        } catch (IOException e) {
            e.printStackTrace();
            channel.txRollback();
        }
    }
}
```

#### 3、持久化

交换机持久化、队列持久化、消息持久化

#### 4、消费者确认机制

消费者设置手动提交或自动提交

RabbitMQ支持消费者确认机制，即：消费者处理消息后可以向MQ发送ack回执，**MQ收到ack回执后才会删除该消息**。而SpringAMQP则允许配置三种确认模式：

- manual：手动ack，需要在业务代码结束后，调用api发送ack。

- auto：自动ack，**由spring监测listener代码是否出现异常，没有异常则返回ack**；抛出异常则返回nack

- none：关闭ack，MQ假定消费者获取消息后会成功处理，因此消息投递后立即被删除

#### 5、失败重试机制

当消费者出现异常后，消息会不断requeue（重新入队）到队列，再重新发送给消费者，然后再次异常，再次requeue，无限循环，导致mq的消息处理飙升，带来不必要的压力

MessageRecoverer，重试耗尽后，将**失败消息投递到指定的交换机**，由人工进行处理

```
@Bean
public MessageRecoverer republishMessageRecoverer(RabbitTemplate rabbitTemplate){
	return new RepublishMessageRecoverer(rabbitTemplate, "error.direct", "error");
}
```

### 死信交换机

#### 1、什么样的消息会成为死信？

- 消息被消费者reject或者返回nack

- 消息超时未消费

- 队列满了

#### 2、如何给队列绑定死信交换机？

- 给队列设置dead-letter-exchange属性，指定一个交换机

- 给队列设置dead-letter-routing-key属性，设置死信交换机与死信队列的RoutingKey

#### 3、如何实现发送一个消息20秒后消费者才收到消息？

- 给消息的目标队列指定死信交换机

- 消费者监听与死信交换机绑定的队列

- 发送消息时给消息设置ttl为20秒

### 延迟队列

利用TTL结合死信交换机，我们实现了消息发出后，消费者延迟收到消息的效果。这种消息模式就称为延迟队列（Delay Queue）模式。

因为延迟队列的需求非常多，所以RabbitMQ的官方也推出了一个插件，原生支持延迟队列效果。



延迟队列插件的使用步骤包括哪些？

- 声明一个交换机，添加delayed属性为true

- 发送消息时，添加x-delay头，值为超时时间

### 惰性队列

#### 消息堆积问题

- 增加**更多消费者**，提高消费速度

- 在消费者内**开启线程池**加快消息处理速度

- **扩大队列容积**，提高堆积上限

#### 惰性队列

指定x-queue-mode属性为lazy即可

- 接收到消息后**直接存入磁盘**而非内存

- 消费者要**消费消息时才会从磁盘中读取**并加载到内存

- 支持数百万条的消息存储

优点：

- 基于磁盘存储，消息上限高

- 没有间歇性的page-out，性能比较稳定

缺点：

- 基于磁盘存储，消息时效性会降低

- 性能受限于磁盘的IO

### MQ集群

#### 两种模式

- 普通模式：普通模式集群**不进行数据同步**，只会进行元数据信息（交换器、队列、绑定关系、vhost元数据）的同步。例如我们有2个MQ：mq1，和mq2，如果你的消息在mq1，而你连接到了mq2，那么mq2会去mq1拉取消息，然后返回给你。如果mq1宕机，**消息就会丢失**。
- 镜像模式：与普通模式不同，**队列会在各个mq的镜像节点之间同步**，因此你连接到任何一个镜像节点，均可获取到消息。而且如果一个节点宕机，并**不会导致数据丢失**。不过，这种方式增加了数据同步的带宽消耗。

#### 获取cookie

RabbitMQ底层依赖于Erlang，而Erlang虚拟机就是一个面向分布式的语言，默认就支持集群模式。集群模式中的每个RabbitMQ 节点使**用 cookie 来确定它们是否被允许相互通信**。

要使两个节点能够通信，它们必须具有相同的共享秘密，称为**Erlang cookie**。cookie 只是一串最多 255 个字符的字母数字字符。

每个集群节点必须具有**相同的 cookie**。实例之间也需要它来相互通信。

#### 镜像模式

- 镜像队列结构是一主多从（从就是镜像）
- 所有操作都是主节点完成，然后同步给镜像节点
- 主宕机后，镜像节点会替代成新的主（如果在主从同步完成前，主就已经宕机，可能出现数据丢失）
- 不具备负载均衡功能，因为所有操作都会有主节点完成（但是不同队列，其主节点可以不同，可以利用这个提高吞吐量）

镜像队列是基于普通的集群模式的

2.1. 镜像队列的结构
镜像队列基本上就是一个特殊的BackingQueue，它内部包裹了一个普通的BackingQueue做本地消息持久化处理，在此基础上增加了将消息和ack复制到所有镜像的功能。所有对mirror_queue_master的操作，会通过**可靠组播GM的方式同步到各slave节点**。GM负责消息的广播，mirror_queue_slave负责回调处理，而master上的回调处理是由coordinator负责完成。mirror_queue_slave中包含了普通的BackingQueue进行消息的存储，master节点中BackingQueue包含在mirror_queue_master中由AMQQueue进行调用。

消息的发布（除了Basic.Publish之外）与消费都是通过master节点完成。master节点对消息进行处理的同时将消息的处理动作通过GM广播给所有的slave节点，slave节点的GM收到消息后，通过回调交由mirror_queue_slave进行实际的处理。

对于Basic.Publish，消息同时发送到master和所有slave上，如果此时master宕掉了，消息还发送slave上，这样当slave提升为master的时候消息也不会丢失。

2.2. GM（Guarenteed Multicast）
GM模块实现的一种**可靠的组播通讯协议**，该协议能够保证组播**消息的原子性**，即保证组中活着的节点要么都收到消息要么都收不到。

它的实现大致如下：

将所有的节点形成一个循环链表，每个节点都会监控位于自己左右两边的节点，当有节点新增时，相邻的节点保证当前广播的消息会复制到新的节点上；当有节点失效时，相邻的节点会接管保证本次广播的消息会复制到所有的节点。在master节点和slave节点上的这些gm形成一个group，group（gm_group）的信息会记录在mnesia中。不同的镜像队列形成不同的group。消息从master节点对于的gm发出后，顺着链表依次传送到所有的节点，由于所有节点组成一个循环链表，master节点对应的gm最终会收到自己发送的消息，这个时候master节点就知道消息已经复制到所有的slave节点了。

### RabbitMQ 消息怎么传输？

由于 TCP 链接的创建和销毁开销较大，且并发数受系统资源限制，会造成性能瓶颈，所以 RabbitMQ **使用信道**的方式来传输数据。

信道（Channel）是生产者、消费者与 RabbitMQ 通信的渠道，信道是**建立在 TCP 链接上的虚拟链接**，且每条 TCP 链接上的信道数量没有限制。就是说 RabbitMQ 在一条 TCP 链接上建立成百上千个信道来达到多个线程处理，这个 **TCP 被多个线程共享**，每个**信道在 RabbitMQ 都有唯一的 ID，保证了信道私有性**，每个信道对应一个线程使用

### docker-compose.yml

```
version: '3'
services:
  rabbitmq:
    image: rabbitmq:3.8.3-management
    container_name: rabbitmq
    restart: always
    hostname: myRabbitmq
    ports:
      - 15672:15672
      - 5672:5672
    volumes:
      - ./data:/var/lib/rabbitmq
    environment:
      - RABBITMQ_DEFAULT_USER=root
      - RABBITMQ_DEFAULT_PASS=root
```

RabbitListener和Rabbithandler的注意

传对象的时候，注意全类名要一致，不然数据转换异常

## Dubbo

#### 设计模式

```
装饰者模式

```

![image-20220710131429724](javaNote.assets/image-20220710131429724.png)

![image-20220710131441928](javaNote.assets/image-20220710131441928.png)

模板方法

![image-20220710220956303](javaNote.assets/image-20220710220956303.png)

#### spring报错

```
org.springframework.beans.factory.BeanCurrentlyInCreationException: Error creating bean with name 'referenceBean': Requested bean is currently in creation: Is there an unresolvable circular reference?
```

![image-20220709163308148](javaNote.assets/image-20220709163308148.png)

**报错分析：**

当ReferenceBean的setApplicationContext方法被调用时，其本身生命周期肯定还未结束，此时再调用applicationContext.getBean(beanDefinitionName)获取本身的时候就报错了，因为本身还处在bean生命周期，即还没创建成功

具体在下面的时候抛出异常，获取不到singleton实例

![image-20220709164107685](javaNote.assets/image-20220709164107685.png)

**解决方案：**

代码逻辑延后到了afterSingletonsInstantiated中执行

#### 心跳机制和超时重连

```
超时后服务端主动断开客户端(或者客户端链接不上服务端的时候)，会触发客户端的的

channelInactive 所以我们需要在这个地方实现的我们的重连
```

#### 序列化方式：

基于SPI机制，支持两种序列化方式，prostuff和hessian

SPI优势：面向接口编程，实现解耦，可配置切换序列化方式。不用硬编码导入实现类。

缺点：遍历的方式获取，个人优化：通过map和枚举，O(1)获取对应的实例

[官网框架设计概览](https://dubbo.apache.org/zh/docs/v2.7/dev/design/)

#### Hessian反序列化

Caused by: com.alibaba.com.caucho.hessian.io.HessianProtocolException: ClasA could not be instantiated
at com.alibaba.com.caucho.hessian.io.JavaDeserializer.instantiate(JavaDeserializer.java:317)

```
dubbo 使用Hessian反序列化的时候可能要使用到无参构造，不然报空指针异常，所以序列化对象最好有一个无参构造
```

#### 领域模型

Protocol 是服务域，它是 Invoker 暴露和引用的主功能入口，它负责 Invoker 的生命周期管理。

Invoker 是实体域，它是 Dubbo 的核心模型，其它模型都向它靠扰，或转换成它，它代表一个可执行体，可向它发起 invoke 调用，它有可能是一个本地的实现，也可能是一个远程的实现，也可能一个集群实现。

Invocation 是会话域，它持有调用过程中的变量，比如方法名，参数等。

#### 负载均衡策略

```
随机
轮询
最少活跃数
一致性哈希
最短响应时间
```

![image-20220710105008646](javaNote.assets/image-20220710105008646.png)

#### 整体设计图

![/dev-guide/images/dubbo-framework.jpg](javaNote.assets/dubbo-framework.jpg)

#### 各层说明

- **config 配置层**：对外配置接口，以 `ServiceConfig`, `ReferenceConfig` 为中心，可以直接初始化配置类，也可以通过 spring 解析配置生成配置类
- **proxy 服务代理层**：服务接口透明代理，生成服务的客户端 Stub 和服务器端 Skeleton, 以 `ServiceProxy` 为中心，扩展接口为 `ProxyFactory`
- **registry 注册中心层**：封装服务地址的注册与发现，以服务 URL 为中心，扩展接口为 `RegistryFactory`, `Registry`, `RegistryService`
- **cluster 路由层**：封装多个提供者的路由及负载均衡，并桥接注册中心，以 `Invoker` 为中心，扩展接口为 `Cluster`, `Directory`, `Router`, `LoadBalance`
- **monitor 监控层**：RPC 调用次数和调用时间监控，以 `Statistics` 为中心，扩展接口为 `MonitorFactory`, `Monitor`, `MonitorService`
- **protocol 远程调用层**：封装 RPC 调用，以 `Invocation`, `Result` 为中心，扩展接口为 `Protocol`, `Invoker`, `Exporter`
- **exchange 信息交换层**：封装请求响应模式，同步转异步，以 `Request`, `Response` 为中心，扩展接口为 `Exchanger`, `ExchangeChannel`, `ExchangeClient`, `ExchangeServer`
- **transport 网络传输层**：抽象 mina 和 netty 为统一接口，以 `Message` 为中心，扩展接口为 `Channel`, `Transporter`, `Client`, `Server`, `Codec`
- **serialize 数据序列化层**：可复用的一些工具，扩展接口为 `Serialization`, `ObjectInput`, `ObjectOutput`, `ThreadPool`

#### 关系说明

```
Remoting是Dubbo协议的实现，又分为Exchange信息交换层和Transport网络传输层。Transport层只负责单项消息传输，是对Netty的封装，Exchange层建立在Transport层之上，封装了请求和响应。
```

**RegistryProtocol#doLocalExport(Invoker<T> invoker,URL providerUrl)**

```java
    private <T> Exporter doLocalExport(Invoker<T> invoker,URL providerUrl) {
        DubboProtocol dubboProtocol = new DubboProtocol();
        return dubboProtocol.export(invoker);
    }
```

**DubboProtocol#export(Invoker<T> invoker)**

```java
    public <T> Exporter<T> export(Invoker<T> invoker) {
        URL url = invoker.getUrl();
        // 服务key
        String key = serviceKey(url);

        openServer(url); // 开启netty服务

        return super.export(invoker);
    }
    // 创建ExchangeServer
    private void openServer(URL url) {
        //TODO 先从缓存获取
        createServer(url);
    }

    /**
     * 得到交换层的ExchangeServer对象
     * @param url
     * @return
     */
    private ExchangeServer createServer(URL url) {
        ExchangeServer server= Exchangers.bind(url,requestHandler);
        return server;
    }
```

**Exchangers.bind(url,requestHandler)本质是HeaderExchanger.bind(url,handler)**

```java
    public ExchangeServer bind(URL url, ExchangeHandler handler) {
        return new HeaderExchangeServer(Transporters.bind(url,handler));
    }
```

Transporters.bind(url,handler))本质是

NettyTransporter.bind(url,handler)

```java
    public RemotingServer bind(URL url, ChannelHandler handler) {
        return new NettyServer(url,handler);
    }
```

靠invoker传来传去

```java
// 本地暴露接口，通过DubboProtocol暴露接口，最终会去调用RegistryProtocol#export    
@SuppressWarnings({"unchecked", "rawtypes"})
    private void doExportUrl(URL url, boolean withMetaData) {
        Invoker<?> invoker = proxyFactory.getInvoker(ref, (Class) interfaceClass, url);
        if (withMetaData) {
            invoker = new DelegateProviderMetaDataInvoker(invoker, this);
        }
        Exporter<?> exporter = protocolSPI.export(invoker);
        exporters.add(exporter);
    }

// DubboProtocol暴露服务
    @Override
    public <T> Exporter<T> export(Invoker<T> invoker) throws RpcException {
        checkDestroyed();
        URL url = invoker.getUrl();

        // export service.
        String key = serviceKey(url);
        DubboExporter<T> exporter = new DubboExporter<T>(invoker, key, exporterMap);

        //export a stub service for dispatching event
        Boolean isStubSupportEvent = url.getParameter(STUB_EVENT_KEY, DEFAULT_STUB_EVENT);
        Boolean isCallbackservice = url.getParameter(IS_CALLBACK_SERVICE, false);
        if (isStubSupportEvent && !isCallbackservice) {
            String stubServiceMethods = url.getParameter(STUB_EVENT_METHODS_KEY);
            if (stubServiceMethods == null || stubServiceMethods.length() == 0) {
                if (logger.isWarnEnabled()) {
                    logger.warn(new IllegalStateException("consumer [" + url.getParameter(INTERFACE_KEY) +
                            "], has set stubproxy support event ,but no stub methods founded."));
                }

            }
        }

        openServer(url);
        optimizeSerialization(url);

        return exporter;
    }
```

```
RegistryConfig转换成URL
```

ServiceConfig进行服务的暴露

```
    private void doExportUrl(URL url, boolean withMetaData) {
        Invoker<?> invoker = proxyFactory.getInvoker(ref, (Class) interfaceClass, url);
        if (withMetaData) {
            invoker = new DelegateProviderMetaDataInvoker(invoker, this);
        }
        Exporter<?> exporter = protocolSPI.export(invoker);
        exporters.add(exporter);
    }
```

```
    /**
     * always export injvm
     */
    private void exportLocal(URL url) {
        URL local = URLBuilder.from(url)
                .setProtocol(LOCAL_PROTOCOL)
                .setHost(LOCALHOST_VALUE)
                .setPort(0)
                .build();
        local = local.setScopeModel(getScopeModel())
            .setServiceModel(providerModel);
        doExportUrl(local, false);
        logger.info("Export dubbo service " + interfaceClass.getName() + " to local registry url : " + local);
    }
```

RegistryProtocol#export(Invoker)

```
    /**
     * RegistryProtocol进行服务暴露，传入一个invoker对象，Invoker就是一个中间人，
     * 最终也会委托给DubboRegistry进行服务注册
     * 将invoker进一步封装，然后交给不同协议的Registry去注册服务
     * @param originInvoker
     * @param <T>
     * @return
     * @throws RpcException
     */
    @Override
    public <T> Exporter<T> export(final Invoker<T> originInvoker) throws RpcException {
        // zookeeper注册中心的url
        // zookeeper://192.168.42.101:2181/org.apache.dubbo.registry.RegistryService?application=dajiuye-swipper-service&dubbo=2.0.2&export=dubbo%3A%2F%2F10.63.138.191%3A7072%2Fcom.lhf.dajiuye.api.service.swipper.SchoolService%3Fanyhost%3Dtrue%26application%3Ddajiuye-swipper-service%26bind.ip%3D10.63.138.191%26bind.port%3D7072%26deprecated%3Dfalse%26dubbo%
        URL registryUrl = getRegistryUrl(originInvoker);
        // url to export locally 服务本地暴露的url
        // dubbo://10.63.138.191:7072/com.lhf.dajiuye.api.service.swipper.SchoolService?anyhost=true&application=da
        URL providerUrl = getProviderUrl(originInvoker);

        // Subscribe the override data
        // FIXME When the provider subscribes, it will affect the scene : a certain JVM exposes the service and call
        //  the same service. Because the subscribed is cached key with the name of the service, it causes the
        //  subscription information to cover.
        final URL overrideSubscribeUrl = getSubscribedOverrideUrl(providerUrl);
        final OverrideListener overrideSubscribeListener = new OverrideListener(overrideSubscribeUrl, originInvoker);
        Map<URL, NotifyListener> overrideListeners = getProviderConfigurationListener(providerUrl).getOverrideListeners();
        overrideListeners.put(registryUrl, overrideSubscribeListener);
        // 根据配置信息对原来服务暴露的url进行重写
        providerUrl = overrideUrlWithConfig(providerUrl, overrideSubscribeListener);
        //export invoker 交给DubboProtocol协议进行服务暴露，比如创建NettyServer监听端口和保存服务实例
        final ExporterChangeableWrapper<T> exporter = doLocalExport(originInvoker, providerUrl);

        // url to registry 获取ZookeeperRegistry注册中心对象（与注册中心创建TCP连接）
        final Registry registry = getRegistry(registryUrl);
        // 服务注册的url
        // dubbo://10.63.138.191:7072/com.lhf.dajiuye.api.service.swipper.SchoolService?anyhost=true&application=dajiuye-swipper-service&deprecated=false&dubbo=2.0.2&dynamic=true&generic=false&interface=com.lhf.dajiuye.api.service.swipper.SchoolService
        final URL registeredProviderUrl = getUrlToRegistry(providerUrl, registryUrl);

        // decide if we need to delay publish (provider itself and registry should both need to register)
        boolean register = providerUrl.getParameter(REGISTER_KEY, true) && registryUrl.getParameter(REGISTER_KEY, true);
        if (register) {
            // 服务注册
            register(registry, registeredProviderUrl);
        }

        // register stated url on provider model
        registerStatedUrl(registryUrl, registeredProviderUrl, register);


        exporter.setRegisterUrl(registeredProviderUrl);
        exporter.setSubscribeUrl(overrideSubscribeUrl);

        if (!registry.isServiceDiscovery()) {
            // Deprecated! Subscribe to override rules in 2.6.x or before.
            registry.subscribe(overrideSubscribeUrl, overrideSubscribeListener);
        }

        notifyExport(exporter);
        //Ensure that a new exporter instance is returned every time export
        return new DestroyableExporter<>(exporter);
    }
```

最终调用DubboProtocol#export进行服务暴露

通过这个ExchangeHandler进行层与层的通信

![image-20220511103702996](javaNote.assets/image-20220511103702996.png)

#### Dubbo Channel和Netty Channel如何建立联系

![image-20220511112813231](javaNote.assets/image-20220511112813231.png)

## VUE

### elementUI

```
element-plus不适配vue3，官方已将vue3版本的更新为element-plus

npm install element-plus --save

引入
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
```



## Docker

### 原理

![image-20220831221934086](javaNote.assets/image-20220831221934086.png)

内核与硬件交互，提供操作硬件的指令

系统应用封装内核指令为函数，便于程序员调用

用户程序基于系统函数库实现功能

Ubuntu和CentOS都是基于Linux内核，只是系统应用不同，提供的函数库有差异

Docker将用户程序和系统应用（ubuntu或centos）一起打包，基于操作系统的内核就可以运行，屏蔽了系统应用函数库依赖等问题。

### 架构

![image-20220831222256618](javaNote.assets/image-20220831222256618.png)

### 容器操作

docker exec -it CONTAINER bash # 以终端交互的模式

docker run -p 端口映射 -e 环境变量 -d 后台运行

docker start&restart

docker ps [-a] 查看容器（所有）

docker logs -f 查看日志

docker rm 删除容器

docker inspect container_id | grep # 查看容器详细信息

![image-20220114205238651](javaNote.assets/image-20220114205238651.png)

### 数据卷操作

```
docker volumn create&inspect&ls&prune&rm
```

![image-20220831223718787](javaNote.assets/image-20220831223718787.png)

### 镜像操作

docker save保存镜像为压缩包

docker load加载压缩包为镜像

docker pull和docker push为镜像推送和镜像拉取

docker images 查看镜像

docker rmi删除镜像

通过使用docker build和Dockerfile构建镜像

![image-20220831222403609](javaNote.assets/image-20220831222403609.png)

### 批量删除容器或镜像

```
sudo docker ps -a | grep Exited | awk '{print $1}' | xargs sudo docker rm 删除异常停止的docker容器

sudo docker images | grep '<none>' | awk '{print $3}'| xargs sudo docker rmi -f 删除名称或标签为none的镜像
```

### docker-compose

```
docker-compose 

-f：指定使用的compose模板文件，默认为当前目录下的docker-compose.yaml文件，可以多次指定。

-p：指定项目的名称，默认将使用所在目录名称作为项目名。

–verbose：输出更多调试信息。

-v：打印版本信息并退出



build 构建（重新构建）项目中的服务容器

config 检测compose文件的错误

up 启动服务

down 停止容器

images 列出项目中所包含的镜像

logs 查看服务容器的日志

kill 发送 SIGKILL 信号来强制停止服务容器

port 查看某个容器端口所映射的公共端口

ps 列出项目中目前的所有容器

restart 重启项目中的服务

rm 删除所有停止状态的服务容器

run 在指定服务上运行一个命令

scale 设置指定服务运行的容器个数

stop 停止处于运行状态的容器

start 启动被stop的服务容器

top 查看各个服务容器内运行的进程

pause 暂停一个服务容器

unpause 恢复处于暂停状态中的服务
```



### 蓝绿发布：蓝绿一个好一个坏，切换

金丝雀发布：一个一个替换

### Harbor位置

```
/opt/harbor
```

### 启动命令

```
docker 启动命令
sudo systemctl start docker
 
docker 重启命令
systemctl restart docker

docker 查看状态命令
systemctl status docker
```

### 开机自启动

```
docker update name --restart
	no -  容器退出时，不重启容器；

    on-failure - 只有在非0状态退出时才从新启动容器；

    always - 无论退出状态是如何，都重启容器；
```

### docker 镜像启动成功但是无法访问

解决办法：

`vi /etc/sysctl.conf或者vi /usr/lib/sysctl.d/00-system.conf`

添加如下代码：
`net.ipv4.ip_forward=1`

重启network服务

`systemctl restart network`

查看是否修改成功

`sysctl net.ipv4.ip_forward`
如果返回为“net.ipv4.ip_forward = 1”则表示成功了

## k8s

master默认有污点不能部署:强制措施：

```
kubectl taint nodes --all node-role.kubernetes.io/master-
```

卸载看s集群

```
kubeadm reset -f
modprobe -r ipip
lsmod
rm -rf ~/.kube/
rm -rf /etc/kubernetes/
rm -rf /etc/systemd/system/kubelet.service.d
rm -rf /etc/systemd/system/kubelet.service
rm -rf /usr/bin/kube*
rm -rf /etc/cni
rm -rf /opt/cni
rm -rf /var/lib/etcd
rm -rf /var/etcd
yum clean all
yum remove kube*
```

## jenkins

war包启动命令（采用）

```
nohup java -jar jenkins.war &
```

rpm方式安装

```
wget https://pkg.jenkins.io/redhat-stable/jenkins-2.121.2-1.1.noarch.rpm

rpm -ivh jenkins-2.121.2-1.1.noarch.rpm
```

docker运行命令

```
docker run -d --name jenkins_v2 -p 8680:8080 -p 56000:50000 -v jenkins_data:/var/jenkins_home jenkins/jenkins
```

修改插件地址

```

cd /var/lib/jenkins/updates/

sed -i 's#http:\/\/updates.jekins-ci.org\/download#https:\/\/mirrors.tuna.tsinghua.edu.cn\/jenkins#g' default.json && sed -i '#/http:\/\/www.google.com#https:\/\/www.baidu.com#g' default.json
```

## es

### 知识点

在在es6中**_all**被禁止了，使用copy_to代替

PUT my_index
{
  "mappings": {
    "properties": {
      "first_name": {
        "type": "text",
        "copy_to": "full_name" 
      },
      "last_name": {
        "type": "text",
        "copy_to": "full_name" 
      },
      "full_name": {
        "type": "text",
        "store": true
      }
    }
  }
}

store:true 那么就可以把full_name也查出来

### 单节点es备份

```
# 查询所有
GET _search
{
  "query": {
    "match_all": {}
  }
}

DELETE /hot

PUT /hot
{
  "mappings": {
    "properties": {
      "hotWord":{
        "type": "keyword"
      }
    }
  }
}

# 测试补全
PUT test
{
  "mappings":{
    "properties":{
      "title":{
        "type":"completion"
      }
    }
  }
}

GET /question

GET /question/_search
{
  "query": {"match_all": {}}
}

POST /test/_doc
{
  "title":["Sony","dsadasda"]
}


GET /question/_search
{
  "suggest": {
    "title_suggest": {
      "text": "java;php;",
      "completion": {
        "field": "suggestion",
        "skip_duplicates":true,
        "size":10
      }
    }
  }
}

GET /question/_search
{
  "query": {"match_all": {}}
}

DELETE /question

PUT /question
{
  "settings": {
    "analysis": {
      "analyzer": {
        "text_analyzer":{
          "tokenizer":"ik_max_word",
          "filter":"py"
        },
        "completion_anylyzer":{
          "tokenizer":"keyword",
          "filter":"py"
        }
      },
      "filter": {
        "py":{
          "type":"pinyin",
          "keep_full_pinyin": false,
          "keep_joined_full_pinyin": true,
          "keep_original": true,
          "limit_first_letter_length": 16,
          "remove_duplicated_term": true,
          "none_chinese_pinyin_tokenize": false
        }
      }
    }
  }, 
  "mappings": {
    "properties": {
      "id": {
        "type": "long"
      },
      "title": {
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart", 
        "copy_to": "all"
      },
      "description": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "createTime": {
        "type": "date"
      },
      "modifiedTime": {
        "type": "date"
      },
      "creatorId": {
        "type": "keyword"
      },
      "creatorName": {
        "type": "text",
        "analyzer": "ik_smart"
      },
      "commentCount": {
        "type": "long"
      },
      "viewCount": {
        "type": "long"
      },
      "likeCount": {
        "type": "long"
      },
      "tag": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "sticky": {
        "type": "long"
      },
      "areaId": {
        "type": "long"
      },
      "areaName": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "img": {
        "type": "keyword"
      },
      "all":{
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart"
      },
      "suggestion":{
        "type": "completion",
        "analyzer": "completion_anylyzer"
      }
    }
  }
}


# 测试拼音分词器


# 老的question映射
PUT /question
{
  "question" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "all" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        },
        "areaId" : {
          "type" : "long"
        },
        "areaName" : {
          "type" : "text",
          "copy_to" : [
            "all"
          ],
          "analyzer" : "ik_smart"
        },
        "commentCount" : {
          "type" : "long"
        },
        "createTime" : {
          "type" : "date"
        },
        "creatorId" : {
          "type" : "keyword"
        },
        "creatorName" : {
          "type" : "text",
          "analyzer" : "ik_smart"
        },
        "description" : {
          "type" : "text",
          "copy_to" : [
            "all"
          ],
          "analyzer" : "ik_smart"
        },
        "id" : {
          "type" : "long"
        },
        "img" : {
          "type" : "keyword"
        },
        "likeCount" : {
          "type" : "long"
        },
        "modifiedTime" : {
          "type" : "date"
        },
        "sticky" : {
          "type" : "long"
        },
        "suggestion" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        },
        "tag" : {
          "type" : "text",
          "copy_to" : [
            "all"
          ],
          "analyzer" : "ik_smart"
        },
        "title" : {
          "type" : "text",
          "copy_to" : [
            "all"
          ],
          "analyzer" : "ik_smart"
        },
        "viewCount" : {
          "type" : "long"
        }
      }
    },
    "settings" : {
      "index" : {
        "routing" : {
          "allocation" : {
            "include" : {
              "_tier_preference" : "data_content"
            }
          }
        },
        "number_of_shards" : "1",
        "provided_name" : "question",
        "creation_date" : "1648203917549",
        "number_of_replicas" : "1",
        "uuid" : "tLMZaYGNRCGZqkIeHM8_tw",
        "version" : {
          "created" : "7120199"
        }
      }
    }
  }
}               
```

### HU帖子Mapping

hot

```
PUT /hot
{
  "mappings": {
    "properties": {
      "hotWord":{
        "type": "keyword"
      }
    }
  }
}
```

question

```
PUT /question
{
  "settings": {
    "analysis": {
      "analyzer": {
        "text_analyzer":{
          "tokenizer":"ik_max_word",
          "filter":"py"
        },
        "completion_anylyzer":{
          "tokenizer":"keyword",
          "filter":"py"
        }
      },
      "filter": {
        "py":{
          "type":"pinyin",
          "keep_full_pinyin": false,
          "keep_joined_full_pinyin": true,
          "keep_original": true,
          "limit_first_letter_length": 16,
          "remove_duplicated_term": true,
          "none_chinese_pinyin_tokenize": false
        }
      }
    }
  }, 
  "mappings": {
    "properties": {
      "id": {
        "type": "long"
      },
      "title": {
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart", 
        "copy_to": "all"
      },
      "description": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "createTime": {
        "type": "date"
      },
      "modifiedTime": {
        "type": "date"
      },
      "creatorId": {
        "type": "keyword"
      },
      "creatorName": {
        "type": "text",
        "analyzer": "ik_smart"
      },
      "commentCount": {
        "type": "long"
      },
      "viewCount": {
        "type": "long"
      },
      "likeCount": {
        "type": "long"
      },
      "tag": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "sticky": {
        "type": "long"
      },
      "areaId": {
        "type": "long"
      },
      "areaName": {
        "type": "text",
        "analyzer": "ik_smart",
        "copy_to": "all"
      },
      "img": {
        "type": "keyword"
      },
      "all":{
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart"
      },
      "suggestion":{
        "type": "completion",
        "analyzer": "completion_anylyzer"
      }
    }
  }
}
```



### 常见DSL语句

```json
GET _search
{
  "query": {
    "match_all": {}
  }
}

GET /_analyze
{
  "analyzer": "ik_max_word",
  "text": "黑马程序员"
}

GET /_analyze
{
  "analyzer": "ik_max_word",
  "text": "传智播客Java就业超过90%,奥力给！"
}

GET /_analyze
{
  "analyzer": "ik_smart",
  "text": "传智播客Java就业超过90%,奥力给！"
}

GET /_analyze
{
  "analyzer": "ik_max_word",
  "text": "传智播客Java就业率超过95%,习大大都点赞,奥力给！"
}

PUT /heima
{
  "mappings": {
    "properties": {
      "age": {
        "type": "keyword"
      },
      "weight": {
        "type": "float"
      },
      "isMarried": {
        "type": "boolean"
      },
      "info": {
        "type": "text",
        "analyzer": "ik_smart"
      },
      "email": {
        "type": "keyword",
        "index": false
      },
      "score": {
        "type": "float"
      },
      "name": {
        "properties": {
          "firstName": {
            "type": "keyword"
          },
          "lastName": {
            "type": "keyword"
          }
        }
      }
    }
  }
}


GET /heima

# 新增数据
POST /heima/_doc/1
{
  "age":"21",
  "weight":52.1,
  "isMarried":false,
  "info":"黑马程序员Java讲师",
    "email":"zy@itcast.cn",
    "score":[99.1, 99.5, 98.9],
    "name":{
      "firstName":"云",
      "lastName":"赵"
      
    }
}


# 可新增字段，但那不可以修改
PUT /heima/_mapping
{
  "properties":{
    "age":{
      "type":"integer"
    }
  }
}

# 查询文档
GET /hotel/_doc/434082

# 删除文档
DELETE /hotel/_doc/61083

# 增量修改
POST /heima/_update/1
{
  "doc":{
    "info":"py数分"
  }
}

# 黑马旅游索引库
PUT /hotel
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "name":{
        "type": "text",
        "analyzer": "ik_max_word",
        "copy_to": "all"
      },
      "address":{
        "type": "keyword",
        "index": false
      },
      "price":{
        "type": "integer"
      },
      "score":{
        "type": "integer"
      },
      "brand":{
        "type": "keyword",
        "copy_to": "all"
      },
      "city":{
        "type": "keyword",
        "copy_to": "all"
      },
      "starName":{
        "type": "keyword"
      },
      "business":{
        "type": "keyword"
      },
      "location":{
        "type": "geo_point"
      },
      "pic":{
        "type": "keyword",
        "index": false
      },
      "all":{
        "type": "text",
        "analyzer": "ik_max_word"
      }
    }
  }
}

# day2

# 查询所有
GET /hotel/_search
{
  "query": {
    "match_all": {}
  }
}

# match查询
GET /hotel/_search
{
  "query": {
    "match": {
      "all": "外滩如家"
    }
  }
}

# multi_match查询
GET /hotel/_search
{
  "query": {
    "multi_match": {
      "query": "外滩如家",
      "fields": ["brand","name","business"]
    }
  }
}

# term查询，精确匹配
GET /hotel/_search
{
  "query": {
    "term": {
      "city": {
        "value": "杭州上海"
      }
    }
  }
}

# range查询
GET /hotel/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 1000,
        "lte": 3000
      }
    }
  }
}

# distance查询
GET /hotel/_search
{
  "query": {
    "geo_distance":{
      "distance":"2km",
      "location":"31.21,121.5"
    }
  }
}

# function score 查询
GET /hotel/_search
{
  "query": {
    "function_score": {
      "query": {
        "match": {
          "all": "外滩"
        }
      }
    }
  }
}

# function score 查询
GET /hotel/_search
{
  "query": {
    "function_score": {
      "query": {
        "match": {
          "all": "外滩"
        }
      },
      "functions": [
        {
          "filter": {
            "term": {
              "brand": "如家"
            }
          },
          "weight": 10
        }
      ],
      "boost_mode": "multiply"
    }
  }
}

# bool查询
GET /hotel/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "name": {
              "value": "如家"
            }
          }
        }
      ],
      "must_not": [
        {
          "range": {
            "FIELD": {
              "gt": 400
            }
          }
        }
      ],
      "filter": [
        {
          "geo_distance": {
            "distance": "100km",
            "location": {
              "lat": 32.21,
              "lon": 121.5
            }
          }
        }
      ]
    }
  }
}

# 普通字段排序
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "score": "desc"
    },
    {
      "price": "asc"
    }
  ]
}

# 地理坐标排序
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "_geo_distance": {
        "location": {
          "lat": 31.03,
          "lon": 121.61
        },
        "order": "asc",
        "unit": "km"
      }
    }
  ]
}

# 分页
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "from": 10,
  "size": 3,
  "sort": [
    {
      "price": {
        "order": "asc"
      }
    }
  ]
}

# 高亮查询
GET /hotel/_search
{
  "query": {
    "match": {
      "name": "如家"
    }
  },
  "from": 0,
  "size": 20,
  "sort": [
    {
      "price": "asc"
    },
    {
      "_geo_distance": {
        "location":"31.040699,121.618075",
        "order": "asc",
        "unit": "km"
      }
    }
  ],
  "highlight": {
    "fields": {
      "name": {
        "pre_tags": "<em>",
        "post_tags": "</em>"
      }
    }
  }
}

# 434082
# 添加广告标记
POST /hotel/_update/434082
{
  "doc": {
    "isAD":true
  }
}

# bucket聚合，即分组
GET /hotel/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 100,
        "lte": 202
      }
    }
  }, 
  "size": 20,
  "aggs": {
    "brandAgg": {
      "terms": {
        "field": "brand",
        "order": {
          "_count": "asc"
        }, 
        "size": 20
      }
    }
  }
}

# 度量聚合
GET /hotel/_search
{
  "size": 0,
  "aggs": {
    "brandAgg": {
      "terms": {
        "field": "brand",
        "size": 10,
        "order": {
          "scoreAgg.avg": "desc"
        }
      },
      "aggs": {
        "scoreAgg": {
          "stats": {
            "field": "score"
          }
        }
      }
    }
  }
}

# 查询索引mapping
GET /hotel

# 自定义分词器
PUT /test
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_analyzer":{
          "tokenizer":"ik_max_word",
          "filter":"py"
        }
      },
      "filter": {
        "py":{
          "type":"pinyin",
          "keep_full_pinyin":false,
          "keep_joined_full_pinyin":true,
          "keep_original":true,
          "limit_first_letter_length":16,
          "remove_duplicated_term":true,
          "none_chinese_pinyin_tokenize":false
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "title":{
        "type": "completion",
        "analyzer": "my_analyzer",
        "search_analyzer": "ik_smart"
      }
    }
  }
}

# 删除索引库
DELETE /hotel

# 测试自定义分词器
POST /test/_analyze
{
  "text": "如家酒店还不错",
  "analyzer": "my_analyzer"
}

# 创建索引库
PUT test
{
  "mappings": {
    "properties": {
      "title":{
        "type": "completion"
      }
    }
  }
}

# 插入文档
POST test/_doc
{
  "title":["sony","WH-1000XM3"]
}

POST test/_doc
{
  "title":["SK-II","PITERA"]
}

POST test/_doc
{
  "title":["Nintendo","switch"]
}

# 自动补全查询
GET /test/_search
{
  "suggest": {
    "title_suggest": {
      "text": "s",
      "completion":{
        "field":"title",
        "skip_duplicates":true,
        "size":10
      }
    }
  }
}

# 修改酒店映射结构，实现自动补全
PUT /hotel
{
  "settings": {
    "analysis": {
      "analyzer": {
        "text_analyzer":{
          "tokenizer":"ik_max_word",
          "filter":"py"
        },
        "completion_analyzer":{
          "tokenizer":"keyword",
          "filter":"py"
        }
      },
      "filter": {
        "py":{
          "type":"pinyin",
          "keep_full_pinyin":false,
          "keep_joined_full_pinyin": true,
          "keep_original":true,
          "limit_first_letter_length":16,
          "remove_duplicated_term":true,
          "none_chinese_pinyin_tokenize":false
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "id":{
        "type": "keyword"
      },
      "name":{
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart",
        "copy_to": "all"
      },
      "address":{
        "type": "keyword",
        "index": false
      },
      "price":{
        "type": "integer"
      },
      "score":{
        "type": "integer"
      },
      "brand":{
        "type": "keyword"
      },
      "city":{
        "type": "keyword"
      },
      "starName":{
        "type": "keyword"
      },
      "business":{
        "type": "keyword",
        "copy_to": "all"
      },
      "location":{
        "type": "geo_point"
      },
      "pic":{
        "type": "keyword",
        "index": false
      },
      "all":{
        "type": "text",
        "analyzer": "text_analyzer",
        "search_analyzer": "ik_smart"
      },
      "suggestion":{
        "type": "completion",
        "analyzer": "completion_analyzer"
      }
    }
  }
}

# 酒店自动补全测试
GET /hotel/_search
{
  "suggest": {
    "YOUR_SUGGESTION": {
      "text": "hs",
      "completion":{
        "field":"suggestion",
        "skip_duplicates":true,
        "size":10
      }
    }
  }
}


```
