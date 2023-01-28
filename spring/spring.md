# spring

## 一.概念

简化开发: Spring框架中提供了两个大的核心技术，分别是:

* ==IOC==
* ==AOP==
  * ==事务处理==

Spring的学习主要包含四部分内容，分别是:

* ==Spring的IOC/DI==
* ==Spring的AOP==
* ==AOP的具体应用,事务管理==
* ==IOC/DI的具体应用,整合Mybatis==

### 1.IOC、IOC容器、Bean、DI

**==IOC（Inversion of Control）控制反转==**

使用对象时，由主动new产生对象转换为由==外部==提供对象，此过程中对象创建控制权由程序转移到外部，此思想称为控制反转。

**此处外部即IOC容器**

**被创建或被管理的对象在IOC容器中统称为==Bean==**

因为service运行需要依赖dao对象、IOC容器中虽然有service和dao对象、但是service对象和dao对象没有任何关系、需要把dao对象交给service,也就是说要绑定service和dao对象之间的关系

像这种在容器中建立对象与对象之间的绑定关系就要用到DI

**==DI（Dependency Injection）依赖注入==**

## 二.依赖注入示例

![Snipaste_2023-01-11_13-42-43](images\Snipaste_2023-01-11_13-42-43.png)

一个空的maven工程、引入依赖

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.3</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

编写类与接口

![Snipaste_2023-01-11_14-24-38](images\Snipaste_2023-01-11_14-24-38.png)

```java
public class BookServiceImpl implements BookService {
    private BookDao bookDao;
    @Override
    public void baoCun() {
        System.out.println("bookServiceImplBaoCun...");
        bookDao.save();
    }

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
}
```

注意要写set方法

resources下添加spring配置文件applicationContext.xml，并完成bean的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">


    <!--bean标签标示配置bean
    id属性标示给bean起名字
    class属性表示给bean定义类型
-->
    <bean id="bookDao" class="org.gzy.dao.impl.BookDaoImpl"/>

    <bean id="bookService" class="org.gzy.service.impl.BookServiceImpl">
        <!--配置server与dao的关系-->
        <!--property标签表示配置当前bean的属性
              name属性表示配置哪一个具体的属性
              ref属性表示参照哪一个bean
      -->
        <property name="bookDao" ref="bookDao"/>
    </bean>

</beans>
```

```java
@Test
public void mt(){
    ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
    BookService bookService = (BookService) ctx.getBean("bookService");

    bookService.baoCun();
}
```

**Spring底层使用的是类的无参构造方法来创建bean的、并且私有无参构造器依然可以创建、利用反射。**

## 三.一些属性介绍

### 1.scope

  <!--scope：为bean设置作用范围，可选值为单例singloton，非单例prototype-->

### 2.name

   <!--name:为bean指定别名，别名可以有多个，使用逗号，分号，空格进行分隔-->

<property>标签内的name属性指的是外层bookService的一个成员变量

```xml
<bean id="bookService" name="service service4 bookEbi" class="com.itheima.service.impl.BookServiceImpl">
    <property name="bookDao" ref="bookDao"/>
</bean>
```

 //此处根据bean标签的id属性和name属性的任意一个值来获取bean对象
   BookService bookService = (BookService) ctx.getBean("service4");

ref的属性值也可以是另一个bean的name值、但一般还是用id

获取bean无论是通过id还是name获取，如果无法获取到，将抛出异常==NoSuchBeanDefinitionException==

### 3.init-method&destroy-method

去看bean生命周期一节第五章

## 四.bean实例化

### 1.构造方法实例化

```xml
<bean id="bookDao" class="org.gzy.dao.impl.BookDaoImpl"/>
```

```java
BookDao bookDao = (BookDao) ctx.getBean("bookDao");
```

实验尝试操作BookDaoImpl的构造器来观察

**Spring底层使用的是类的无参构造方法来创建bean的、并且私有无参构造器依然可以创建、利用反射。**

### 2.静态工厂实例化

```java
//静态工厂创建对象
public class OrderDaoFactory {
    public static OrderDao getOrderDao(){
        return new OrderDaoImpl();
    }
}
```

```xml
<bean id="orderDao" class="com.itheima.factory.OrderDaoFactory" factory-method="getOrderDao"/>
```

在工厂的静态方法中，我们除了new对象还可以做其他的一些业务操作

### 3.实例工厂实例化

```java
public class UserDaoFactory {
    public UserDao getUserDao(){
        return new UserDaoImpl();
    }
}
```

```xml
<bean id="userFactory" class="com.itheima.factory.UserDaoFactory"/>
<bean id="userDao" factory-method="getUserDao" factory-bean="userFactory"/>
```

先把实例工厂配置成了一个bean了

### 4.FactoryBean的使用

这种方式在Spring去整合其他框架的时候会被用到，所以这种方式需要大家理解掌握。

具体的使用步骤为:

(1)创建一个UserDaoFactoryBean的类，实现FactoryBean接口，重写接口的方法

```java
public class UserDaoFactoryBean implements FactoryBean<UserDao> {
    //代替原始实例工厂中创建对象的方法
    public UserDao getObject() throws Exception {
        return new UserDaoImpl();
    }
    //返回所创建类的Class对象
    public Class<?> getObjectType() {
        return UserDao.class;
    }
}
```

(2)在Spring的配置文件中进行配置

```xml
<bean id="userDao" class="com.itheima.factory.UserDaoFactoryBean"/>
```



查看源码会发现，FactoryBean接口其实会有三个方法，分别是:

```java
T getObject() throws Exception;

Class<?> getObjectType();

default boolean isSingleton() {
		return true;
}
```

## 五.bean的生命周期

步骤1:添加初始化和销毁方法

针对这两个阶段，我们在BooDaoImpl类中分别添加两个方法，==方法名任意==

```java
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    //表示bean初始化对应的操作
    public void init(){
        System.out.println("init...");
    }
    //表示bean销毁前对应的操作
    public void destory(){
        System.out.println("destory...");
    }
}
```

步骤2:配置生命周期

在配置文件添加配置，如下:

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl" init-method="init" destroy-method="destory"/>
```

步骤3:运行程序init方法执行了，但是destroy方法却未执行，这是为什么呢?

* Spring的IOC容器是运行在JVM中
* 运行main方法后,JVM启动,Spring加载配置文件生成IOC容器,从容器获取bean对象，然后调方法执行
* main方法执行完后，JVM退出，这个时候IOC容器中的bean还没有来得及销毁就已经结束了
* 所以没有调用对应的destroy方法

知道了出现问题的原因，具体该如何解决呢?

1.close关闭容器

* ApplicationContext中没有close方法

* 需要将ApplicationContext更换成ClassPathXmlApplicationContext

  ```java
  ClassPathXmlApplicationContext ctx = new 
      ClassPathXmlApplicationContext("applicationContext.xml");
  ```

* 调用ctx的close()方法

  ```
  ctx.close();
  ```

* 运行程序，就能执行destroy方法的内容


2.

* 在容器未关闭之前，提前设置好回调函数，让JVM在退出之前回调此函数来关闭容器

* 调用ctx的registerShutdownHook()方法

  ```
  ctx.registerShutdownHook();
  ```

  **注意:**registerShutdownHook在ApplicationContext中也没有



相同点:这两种都能用来关闭容器

不同点:close()是在调用的时候关闭，registerShutdownHook()是在JVM退出前调用关闭。



3.分析上面的实现过程，会发现添加初始化和销毁方法，即需要编码也需要配置，实现起来步骤比较多也比较乱。

Spring提供了两个接口来完成生命周期的控制，好处是可以不用再进行配置`init-method`和`destroy-method`

接下来在BookServiceImpl完成这两个接口的使用:

修改BookServiceImpl类，添加两个接口`InitializingBean`， `DisposableBean`并实现接口中的两个方法`afterPropertiesSet`和`destroy`

```java
public class BookServiceImpl implements BookService, InitializingBean, DisposableBean {
    private BookDao bookDao;
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
    public void save() {
        System.out.println("book service save ...");
        bookDao.save(); 
    }
    public void destroy() throws Exception {
        System.out.println("service destroy");
    }
    public void afterPropertiesSet() throws Exception {
        System.out.println("service init");
    }
}
```

重新运行AppForLifeCycle类，

## 六.DI依赖注入

### 1.setter注入

声明成员变量、写上set方法

 private BookDao bookDao;

private int age；

都可以算成员变量、引用类型、简单类型

引用类型

```xml
  <bean id="bookService" class="org.gzy.service.impl.BookServiceImpl">
      <property name="bookDao" ref="bookDao"/>
  </bean>
```

简单类型

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
 	<property name="age" value="10"/>
</bean>
```

### 2.构造器注入

去掉set方法、添加构造器

```java
public class BookServiceImpl implements BookService {
    private  BookDao bookDao;
    private  int i;

    public BookServiceImpl(BookDao bookDao, int i) {
        this.bookDao = bookDao;
        this.i = i;
    }

    @Override
    public void baoCun() {
        System.out.println("bookServiceImplBaoCun...");
        bookDao.save();
    }

}
```

```xml
    <bean id="bookDao" class="org.gzy.dao.impl.BookDaoImpl"/>

    <bean id="bookService" class="org.gzy.service.impl.BookServiceImpl">
<!--        <property name="bookDao" ref="bookDao"/>-->
        <constructor-arg name="bookDao" ref="bookDao"/>
        <constructor-arg name="i" value="2"/>
    </bean>
```



### 其它type/index

方式一:删除name属性，添加type属性，按照类型注入

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg type="int" value="10"/>
    <constructor-arg type="java.lang.String" value="mysql"/>
</bean>
```

* 这种方式可以解决构造函数形参名发生变化带来的耦合问题
* 但是如果构造方法参数中有类型相同的参数，这种方式就不太好实现了

方式二:删除type属性，添加index属性，按照索引下标注入，下标从0开始

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg index="1" value="100"/>
    <constructor-arg index="0" value="mysql"/>
</bean>
```

* 这种方式可以解决参数类型重复问题
* 但是如果构造方法参数顺序发生变化后，这种方式又带来了耦合问题

介绍完两种参数的注入方式，具体我们该如何选择呢?

1. 强制依赖使用构造器进行，使用setter注入有概率不进行注入导致null对象出现
   * 强制依赖指对象在创建的过程中必须要注入指定的参数
2. 可选依赖使用setter注入进行，灵活性强
   * 可选依赖指对象在创建过程中注入的参数可有可无
3. Spring框架倡导使用构造器，第三方框架内部大多数采用构造器注入的形式进行数据初始化，相对严谨
4. 如果有必要可以两者同时使用，使用构造器注入完成强制依赖的注入，使用setter注入完成可选依赖的注入
5. 实际开发过程中还要根据实际情况分析，如果受控对象没有提供setter方法就必须使用构造器注入
6. **==自己开发的模块推荐使用setter注入==**

## 七.自动配置/自动装配

**IoC容器根据bean所依赖的资源在容器中自动查找并注入到bean中的过程称为自动装配**

#### 自动装配方式有哪些?

* ==按类型（常用）==
* 按名称
* 按构造方法
* 不启用自动装配

```xml
<bean class="com.itheima.dao.impl.BookDaoImpl"/>
<!--autowire属性：开启自动装配，通常使用按类型装配-->
<bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byType"/>
```

* 需要注入属性的类中对应属性的setter方法不能省略
* 被注入的对象必须要被Spring的IOC容器管理
* 按照类型在Spring的IOC容器中如果找到多个对象，会报`NoUniqueBeanDefinitionException`

```xml
<bean class="com.itheima.dao.impl.BookDaoImpl"/>
<!--autowire属性：开启自动装配，通常使用按类型装配-->
<bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byName"/>
```

* * bookDao是private修饰的，外部类无法直接方法
  * 外部类只能通过属性的set方法进行访问
  * 对外部类来说，setBookDao方法名，去掉set后首字母小写是其属性名
    * 为什么是去掉set首字母小写?
    * 这个规则是set方法生成的默认规则，set方法的生成是把属性名首字母大写前面加set形成的方法名
  * **所以按照名称注入，其实是和对应的set方法有关**，但是如果按照标准起名称，属性名和set对应的名是一致的

* 如果按照名称去找对应的bean对象，找不到则注入Null

* 当某一个类型在IOC容器中有多个对象，按照名称注入只找其指定名称对应的bean对象，不会报错

### 总结

两种方式介绍完后，以后用的更多的是==按照类型==注入。

最后对于依赖注入，需要注意一些其他的配置特征:

1. 自动装配用于引用类型依赖注入，不能对简单类型进行操作
2. 使用按类型装配时（byType）必须保障容器中相同类型的bean唯一，推荐使用
3. 使用按名称装配时（byName）必须保障容器中具有指定名称的bean，因变量名与配置耦合，不推荐使用
4. 自动装配优先级低于setter注入与构造器注入，同时出现时自动装配配置失效



## 九.总结

理解思想、可能全部用不到

@Autowired

@Value

## 十.核心容器

![1629984980781](images\1629984980781.png)

BeanFactory是延迟加载，只有在获取bean对象的时候才会去创建

需要知晓容器的最上级的父接口为 BeanFactory即可

# spring_注解开发



**Springboot不用写@ComponentScan。要求各bean在springboot主类所在包、或主类所在包的子包**

**==注意:@Component注解不可以添加在接口上，因为接口是无法创建对象的。==**



## 一.@Component

为了让Spring框架能够扫描到写在类上的注解，需要在配置文件上进行包扫描

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    
    <context:component-scan base-package="org.gzy"/>

</beans>
```

在BookDaoImpl类上添加`@Component`注解

```java
@Component("bookDao")
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ..." );
    }
}
```

**==注意:@Component注解不可以添加在接口上，因为接口是无法创建对象的。==**

测试

```java
public static void main(String[] args) {
    ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
    BookDao bookDao = (BookDao) ctx.getBean("bookDao");
    bookDao.save();
}
```



@Component注解如果不起名称、可以按照类型来获取bean对象

BookService bookService = ctx.getBean(BookService.class);

@Component注解如果不起名称、会有一个默认值就是`当前类名首字母小写`，所以也可以按照名称获取

BookService bookService = (BookService)ctx.getBean("bookServiceImpl");

### 1.衍生三个注解

对于@Component注解，还衍生出了其他三个注解`@Controller`、`@Service`、`@Repository`

## 二.纯注解开发@Configuration

### 1.使用配置类代替applicationcontext.xml文件

新建类、

类上添加`@Configuration`注解，将其标识为一个配置类,替换`applicationContext.xml`

在配置类上添加包扫描注解`@ComponentScan`替换`<context:component-scan base-package=""/>`

```java
@Configuration
@ComponentScan("com.itheima")
public class SpringConfig {
}
```

运行

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
    BookDao bookDao = (BookDao) ctx.getBean("bookDao");
    System.out.println(bookDao);
    BookService bookService = ctx.getBean(BookService.class);
    System.out.println(bookService);
}
```

## 三.小结

**小结:**

这一节重点掌握的是使用注解完成Spring的bean管理，需要掌握的内容为:

* 记住@Component、@Controller、@Service、@Repository这四个注解
* applicationContext.xml中`<context:component-san/>`的作用是指定扫描包路径，注解为@ComponentScan
* @Configuration标识该类为配置类，使用类替换applicationContext.xml文件
* ClassPathXmlApplicationContext是加载XML配置文件
* AnnotationConfigApplicationContext是加载配置类

## 四.@Scope

| 名称 | @Scope                                                       |
| ---- | ------------------------------------------------------------ |
| 类型 | 类注解                                                       |
| 位置 | 类定义上方                                                   |
| 作用 | 设置该类创建对象的作用范围<br/>可用于设置创建出的bean是否为单例对象 |
| 属性 | value（默认）：定义bean作用范围，<br/>==默认值singleton（单例），可选值prototype（非单例）== |

## 五.@PostConstruct  @PreDestroy

| 名称 | @PostConstruct         |
| ---- | ---------------------- |
| 类型 | 方法注解               |
| 位置 | 方法上                 |
| 作用 | 设置该方法为初始化方法 |
| 属性 | 无                     |

| 名称 | @PreDestroy          |
| ---- | -------------------- |
| 类型 | 方法注解             |
| 位置 | 方法上               |
| 作用 | 设置该方法为销毁方法 |
| 属性 | 无                   |

标注在类里方法上

```java
@Repository
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    @PostConstruct //在构造方法之后执行，替换 init-method
    public void init() {
        System.out.println("init ...");
    }
    @PreDestroy //在销毁方法之前执行,替换 destroy-method
    public void destroy() {
        System.out.println("destroy ...");
    }
}
```

要想看到两个方法执行，需要注意的是`destroy`只有在容器关闭的时候，才会执行，所以需要修改App的类

```java
public class App {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao1 = ctx.getBean(BookDao.class);
        BookDao bookDao2 = ctx.getBean(BookDao.class);
        System.out.println(bookDao1);
        System.out.println(bookDao2);
        ctx.close(); //关闭容器
    }
}
```

**==注意:@PostConstruct和@PreDestroy注解如果找不到，需要导入下面的jar包==**

```java
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```

找不到的原因是，从JDK9以后jdk中的javax.annotation包被移除了，这两个注解刚好就在这个包中。

## 六.注解依赖注入

### 1.@Autowired

@Autowired可以写在属性上，也可也写在setter方法上，最简单的处理方式是`写在属性上并将setter方法删除掉`

暴力反射可以删除setter即使属性由private修饰

@Autowired默认按照类型自动装配，如果IOC容器中同类的Bean找到多个，就按照变量名和Bean的名称匹配。

当根据类型在容器中找到多个bean,注入参数的属性名又和容器中bean的名称不一致，这个时候该如何解决，就需要使用到`@Qualifier`来指定注入哪个名称的bean对象。

```java
@Autowired
@Qualifier("bookDao1")
private BookDao bookDao;
```

==注意:@Qualifier不能独立使用，必须和@Autowired一起使用==

### 2.简单数据类型注入@Value

```java
@Value("itheima")
private String name;
```

### 3.@PropertySource用法：读取配置文件如yml

步骤1：resource下准备properties文件

jdbc.properties

```properties
name=itheima888
```

步骤2: 使用注解加载properties配置文件

在配置类上添加`@PropertySource`注解

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("jdbc.properties")
public class SpringConfig {
}

```

步骤3：使用@Value读取配置文件中的内容

```java
@Repository("bookDao")
public class BookDaoImpl implements BookDao {
    @Value("${name}")
    private String name;
    public void save() {
        System.out.println("book dao save ..." + name);
    }
}
```

* 如果读取的properties配置文件有多个，可以使用`@PropertySource`的属性来指定多个

  ```java
  @PropertySource({"jdbc.properties","xxx.properties"})
  ```

* `@PropertySource`注解属性中不支持使用通配符`*`,运行会报错

  ```java
  @PropertySource({"*.properties"})
  ```

* `@PropertySource`注解属性中可以把`classpath:`加上,代表从当前项目的根路径找文件

  ```java
  @PropertySource({"classpath:jdbc.properties"})
  ```

## 七.一些注解

### 1.@Bean  @Import

@Bean注解的作用是将方法的返回值制作为Spring管理的一个bean对象

```java
@Bean
public static Book getBook(){
    return new Book();
}
```

但需要放在配置类@Configuration类里写

```java
@Configuration
@ComponentScan("org.gzy")
@PropertySource(value = {"classpath:config/jdbc.properties","classpath:application.properties"})
public class SpringConfig {
    @Bean
    public static Book getBook(){
        return new Book();
    }
}
```

或者使用@Import引入

```java
@Configuration
@ComponentScan("org.gzy")
@PropertySource(value = {"classpath:config/jdbc.properties","classpath:application.properties"})
@Import({MyGetBean.class})
public class SpringConfig {

}
```

**假如@Bean方法里需要用到引用类型数据呢：**

1. **首先确保引用对象能被spring管理到@ComponentScan**
2. **将引用对象之间作为方法入参写在括号内就行**

# AOP

## 一.概念

AOP(Aspect Oriented Programming)面向切面编程，一种编程范式，指导开发者如何组织程序结构。

OOP(Object Oriented Programming)面向对象编程

作用:在不惊动原始设计的基础上为其进行功能增强，前面咱们有技术就可以实现这样的功能即代理模式。



连接点：被增强类中所有方法

切入点：需被增强的方法

通知类：通知所在的类

通知：共性功能增强的功能

切面：通知与切入点的关系描述

## 二.实现流程

1.引入依赖

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.19</version>
</dependency>
```

* 因为`spring-context`中已经导入了`spring-aop`,所以不需要再单独导入`spring-aop`
* 导入AspectJ的jar包,AspectJ是AOP思想的一个具体实现，Spring有自己的AOP实现，但是相比于AspectJ来说比较麻烦，所以我们直接采用Spring整合ApsectJ的方式进行AOP开发。

2.定义通知类、定义切入点

```Java
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

切入点定义依托一个不具有实际意义的方法进行，即无参数、无返回值、方法体无实际逻辑。

3.制作切面------切入点与通知的关系

4.将通知类配给容器并表示其为切面类

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}

    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

5.开启注解格式AOP

```java
@Configuration
@ComponentScan("com.itheima")
@EnableAspectJAutoProxy
public class SpringConfig {
}
```

6.运行程序

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
    ctx.getBean(MyMeth.class).del();
}
```

注意以这种方式才能被spring管理到

切入点表达式标准格式：动作关键字(访问修饰符  返回值  包名.类/接口名.方法名(参数) 异常名）

 @Before("pt()")      

 @After("pt()")

@Around("pt()")   使用时要在通知类主动调用原方法、来表明原方法在哪一步执行、带返回值带参如下

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp)throws Throwable {
        Object[] args = pjp.getArgs();
        System.out.println(Arrays.toString(args));
        Object ret = pjp.proceed();
        return ret;
    }
	//其他的略
}
```

  @AfterReturning("pt2()")   返回后通知是需要在原始方法`select`正常执行后才会被执行，如果`select()`方法执行的过程中出现了异常，那么返回后通知是不会被执行。后置通知是不管原始方法有没有抛出异常都会被执行。

  @AfterThrowing



pjp.proceed()方法是构造方法

```java
@Around("pt()")
public Object around(ProceedingJoinPoint pjp) throws Throwable{
    Object[] args = pjp.getArgs();
    System.out.println(Arrays.toString(args));
    args[0] = 666;
    Object ret = pjp.proceed(args);
    return ret;
}
```

改变参数、可以用来对参数做过滤



@AfterReturning返回后通知获得返回值

```java
@AfterReturning(value = "pt()",returning = "ret")
public void afterReturning(Object ret) {
    System.out.println("afterReturning advice ..."+ret);
}

```
获取异常----省略

# 事务

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void log(String out,String in,Double money ) {
    logDao.log("转账操作由"+out+"到"+in+",金额："+money);
}
```

无论转账操作是否成功，日志必须保留、日志记录不会回滚

![1630254257628](images\1630254257628.png)



事务配置、也是加在 @Transactional(rollbackFor = {IOException.class})

Spring的事务只会对`Error异常`和`RuntimeException异常`及其子类进行事务回顾，其他的异常类型是不会回滚的，对应IOException不符合上述条件所以不回滚
 此时就可以使用rollbackFor属性来设置出现IOException异常不回滚

![1630250069844](images\1630250069844.png)



使用：

```java
//配置事务管理器，mybatis使用的是jdbc事务
@Bean
public PlatformTransactionManager transactionManager(DataSource dataSource){
    DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
    transactionManager.setDataSource(dataSource);
    return transactionManager;
}
```



@Configuration

//开启注解式事务驱动
@EnableTransactionManagement
public class SpringConfig {
}
