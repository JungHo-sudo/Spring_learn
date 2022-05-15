# 1、Spring概述

  ## 1.1 简介

就是一个后端模板；
==官网 : http://spring.io/==
==官方下载地址 : https://repo.spring.io/libs-release-local/org/springframework/spring/ 
GitHub : https://github.com/spring-projects==

## 1.2 优点

- Spring是一个开源免费的框架 , 容器 .
- Spring是一个轻量级的框架 , 非侵入式的 . 
- 控制反转 IoC , 面向切面 Aop 
- 对事物的支持 , 对框架的支持

一句话概括:Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器(框架)。

## 1.3 组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/1039a86919f24040ae6a17f2af41f45e.png#pic_center)
Spring 框架是一个分层架构，由 7 个定义良好的模块组成。Spring 模块构建在核心容器之上，核心容器 定义了创建、配置和管理 bean 的方式 .
![在这里插入图片描述](https://img-blog.csdnimg.cn/6e17d2764c264637bdcea4b9d0041e38.png#pic_center)


---

组成 Spring 框架的每个模块(或组件)都可以单独存在，或者与其他一个或多个模块联合实现。每个模 块的功能如下:

- 核心容器:核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 ==BeanFactory== ，它 是工厂模式的实现。 ==BeanFactory== 使用 (IOC) 模式将应用程序的配置和依赖性规范 与实际的应用程序代码分开。
- Spring 上下文:Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文 包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。
- Spring AOP:通过配置管理特性，Spring AOP 模块直接将面向切面的编程功能 , 集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理任何支持 AOP的对象。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖组件，就可以 将声明性事务管理集成到应用程序中。
- Spring DAO:JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不 同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异 常代码数量(例如打开和关闭连接)。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次 结构。
- Spring ORM:Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包 括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结 构。
- Spring Web 模块:Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提 供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请 求以及将请求参数绑定到域对象的工作。
- Spring MVC 框架:MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口， MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。


## 1.4 拓展

Spring Boot与Spring Cloud

- Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发单个微服务; 
- Spring Cloud是基于Spring Boot实现的;
- Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架; 
- Spring Boot使用了约束优于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置 , Spring Cloud很大的一部分是基于Spring Boot来实现，Spring Boot可以离开Spring Cloud独立使 用开发项目，但是Spring Cloud离不开Spring Boot，属于依赖的关系。 
- SpringBoot在SpringClound中起到了承上启下的作用，如果你要学习SpringCloud必须要学习 SpringBoot。

## 1.5 依赖地址

仓库地址：https://mvnrepository.com/
下载地址：https://maven.apache.org/download.cgi
spring官方文档：https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html

```xml
 <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.7</version>
</dependency>
 <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.7</version>
</dependency>
    
```



- ---

# 2、IoC基础

##  2.1 IOC是什么？

IOC是一种思想，本质上把主动权由程序员转换为用户，提供Set接口，通过set注入使得程序员可以把更多精力集中在业务实现上，而不必去管理对象的创建了。本质上是实现解耦的过程。

---

## 2.2 IOC本质：

**控制反转IoC(Inversion of Control)**，是一种设计思想，DI(依赖注入)是实现IoC的一种方法，也有人认 为DI只是IoC的另一种说法。没有IoC的程序中 , 我们使用面向对象编程 , 对象的创建与对象间的依赖关系 完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为 所谓控制反转就是:获得依赖对象的方式反转了。

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/c7ef4f0b8dd74bdaa3d6bc3284a33556.png#pic_center)
**IoC是Spring框架的核心内容**，使用多种方式完美的实现了IoC，可以使用XML配置，也可以使用注解， 新版本的Spring也可以零配置实现IoC。
Spring容器在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用 时再从Ioc容器中取出需要的对象。
![在这里插入图片描述](https://img-blog.csdnimg.cn/cbe99424149f4e19b6bbc960cd4e5ce9.png#pic_center)

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为 一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。
**控制反转是一种通过描述(XML或注解)并通过第三方去生产或获取特定对象的方式。在Spring中实现 控制反转的是IoC容器，其实现方法是依赖注入(Dependency Injection,DI)。**

==需要注意的是，DI只是实现IOC的一种方式手段而已，并不是唯一方法。==

==对于如何理解IOC我们要搞清楚控制什么？反转什么？既然有反转，什么是正转？==

---

# 3、HelloSpring

## @Test设置

关于test模块支持的挺多，像是junit、testNG
建议用junit4加入到类路径中，其他的容易报错，同时要只安装一个test模块，否则冲突。出现bug请检查pom文件。
[Test设置链接](https://blog.csdn.net/qq_45679541/article/details/106246714?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1.pc_relevant_paycolumn_v3&utm_relevant_index=2)

***对象由Spring来创建，管理，装配！***

---

# 4、 IOC对象创建方式

## 4.1 通过无参构造来创建对象

==结果可以发现，在调用show方法之前，User对象已经通过无参构造初始化了!==

## 4.2 通过有参构造来创建对象

三种方式：
beans.xml 有三种方式编写

```xml
<!-- 第一种根据index参数下标设置 -->
<bean id="userT" class="com.kuang.pojo.UserT">
<!-- index指构造方法 , 下标从0开始 -->
    <constructor-arg index="0" value="kuangshen2"/>
</bean>

<!-- 第二种根据参数名字设置 -->
<bean id="userT" class="com.kuang.pojo.UserT">
<!-- name指参数名 -->
    <constructor-arg name="name" value="kuangshen2"/>
</bean>

<!-- 第三种根据参数类型设置 -->
<bean id="userT" class="com.kuang.pojo.UserT">
    <constructor-arg type="java.lang.String" value="kuangshen2"/>
</bean>

```

==结论:在配置文件加载的时候。其中管理的对象都已经初始化了!==


---


# 5、Spring配置说明

## 5.1 别名

alias 设置别名 , 为bean设置别名 , 可以设置多个别名

```xml
 <!--设置别名:在获取Bean的时候可以使用别名获取--> 
<aliasname="userT"alias="userNew"/>
```

## 5.2. Bean的配置

```xml
<!--bean就是java对象,由Spring创建和管理-->
<!--
id 是bean的标识符,要唯一,如果没有配置id,name就是默认标识符 如果配置id,又配置了name,那么name是别名 name可以设置多个别名,可以用逗号,分号,空格隔开 如果不配置id和name,可以根据applicationContext.getBean(.class)获取对象;
class是bean的全限定名=包名+类名 -->
<bean id="hello" name="hello2 h2,h3;h4" class="com.kuang.pojo.Hello">
    <property name="name" value="Spring"/>
</bean>

```

## 5.3. import

团队的合作通过import来实现 .

```xml
<importresource="{path}/beans.xml"/>
```

---

# 6、依赖注入(DI)

- 依赖注入(Dependency Injection,DI)。
- 依赖 : 指Bean对象的创建依赖于容器 . Bean对象的依赖资源 . 注入 : 指- Bean对象所依赖的资源 , 由容器来设置和装配 .

常用注入方式：

- Dependency Injection
- Straight Values (Primitives, Strings, and so on)
- Inner Beans
- Collections
- Null and Empty String Values 

## 6.1 构造器注入

## 6.2 set注入 (重点)

要求被注入的属性 , 必须有set方法 , set方法的方法名由set + 属性首字母大写 , 如果属性是boolean类型
, 没有set方法 , 是 is .

- 依赖注入 ： SET注入！
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中所有属性通过容器注入

【环境搭建】

1、复杂类型

```java
public class Student {

    private String name;
    private Address address;
    private String[] books;
    private List<String> hobbys;
    private Map<String,String> card;
    private Set<String> games;
    private String wife;
    private Properties info;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public String[] getBooks() {
        return books;
    }

    public void setBooks(String[] books) {
        this.books = books;
    }

    public List<String> getHobbys() {
        return hobbys;
    }

    public void setHobbys(List<String> hobbys) {
        this.hobbys = hobbys;
    }

    public Map<String, String> getCard() {
        return card;
    }

    public void setCard(Map<String, String> card) {
        this.card = card;
    }

    public Set<String> getGames() {
        return games;
    }

    public void setGames(Set<String> games) {
        this.games = games;
    }

    public String getWife() {
        return wife;
    }

    public void setWife(String wife) {
        this.wife = wife;
    }

    public Properties getInfo() {
        return info;
    }

    public void setInfo(Properties info) {
        this.info = info;
    }



    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", address=" + address.toString()+
                ", books=" + Arrays.toString(books) +
                ", hobbys=" + hobbys +
                ", card=" + card +
                ", games=" + games +
                ", wife='" + wife + '\'' +
                ", info=" + info +
                '}';
    }
}



-------------------------------------------

public class Address {

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    private String address;

    @Override
    public String toString() {
        return "Address{" +
                "address='" + address + '\'' +
                '}';
    }
}

```

2、真实测试对象

```java
public class mytest {
    public static void main(String[] args) {
      ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student.toString());
//        Student{name='jungho',
//        address=Address{address='仁川'}, 
//        books=[红楼梦, 水浒传, 三国演义], 
//        hobbys=[听歌, 写代码, 玩游戏, 看电影], 
//        card={身份证=12345678990, 银行卡=2131251312312, 型号=123123123123123}, 
//        games=[LOL, LO, LOLLLL], 
//        wife='null', 
//        info={测试2=2, 学号=32131231, 测试1=1, 性别=男}}
    }
}

```

3. beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.kuang.pojo.Address">
        <property name="address" value="仁川">

        </property>
    </bean>
    <bean id="student" class="com.kuang.pojo.Student">

<!--        普通值注入 value-->
        <property name="name" value="jungho"/>

<!--        Bean注入 ref-->
        <property name="address" ref="address"/>

<!--        数组注入 ref-->
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>水浒传</value>
                <value>三国演义</value>
            </array>
        </property>

<!--        list注入-->
        <property name="hobbys">
            <list>
                <value>听歌</value>
                <value>写代码</value>
                <value>玩游戏</value>
                <value>看电影</value>
            </list>
        </property>

<!--        Map-->
        <property name="card">
            <map>
                <entry key="身份证" value="12345678990"/>
                <entry key="银行卡" value="2131251312312"/>
                <entry key="型号" value="123123123123123"/>
            </map>
        </property>

<!--        set-->
        <property name="games">
            <set>
                <value>LOL</value>
                <value>LO</value>
                <value>LOLLLL</value>
            </set>
        </property>

<!--        NULL and empty-->
        <property name="wife">
<!--            自闭合-->
            <null/>
        </property>

<!--        properties-->
        <property name="info">
            <props>
                <prop key="学号">32131231</prop>
                <prop key="性别">男</prop>
                <prop key="测试1">1</prop>
                <prop key="测试2">2</prop>
            </props>
        </property>

    </bean>


</beans>
```

## 6.3 拓展注入实现

**了解即可，属于扩展内容**


我们可以使用P/C命名空间进行注入
官方文档：
P命名空间：[P命名空间链接](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-p-namespace)
C命名空间：[C命名空间链接](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-c-namespace)

User类：

```java
package com.kuang.pojo;

public class User {
    private String name;
    private int age;

    public User() {
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

XML文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--    P命名空间的注入，可以直接注入属性的值；property的缩写-->
    <bean id="user" class="com.kuang.pojo.User" p:name = "jungho" p:age = "18"/>
<!--        c命名空间注入 通过构造器注入 construct-args-->
    <bean id="user2" class="com.kuang.pojo.User" c:age="18" c:name="tang"/>

</beans>
```

测试类:

```java
import com.kuang.pojo.Student;
import com.kuang.pojo.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.testng.annotations.Test;

public class mytest {
    @Test
    public void test2(){
        ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
        User user = context.getBean("user2",User.class);
        System.out.println(user);
    }
}
```

注意点：P命名合C命名空间不可直接使用，需要导入XML约束，约束语句见官网！
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"

## 6.4 Bean的作用域

Bean Scopes（bean 作用域）
![在这里插入图片描述](https://img-blog.csdnimg.cn/8a72bb3d422a4f17a377eebb2f21bf5f.png#pic_center)

### 6.4.1 Singleton（单例模式 默认）

![在这里插入图片描述](https://img-blog.csdnimg.cn/d884e5c7199f49c5a013345cb14248cc.png#pic_center)
当一个bean的作用域为Singleton，那么Spring IoC容器中只会存在一个共享的bean实例，并且所有对 bean的请求，只要id与该bean定义相匹配，则只会返回bean的同一实例。Singleton是单例类型，就是 在创建起容器时就同时自动创建了一个bean的对象，不管你是否使用，他都存在了，每次获取到的对象 都是同一个对象。注意，Singleton作用域是Spring中的缺省作用域。要在XML中将bean定义成 singleton，可以这样配置:
显式方法：

```xml
<beanid="ServiceImpl"class="cn.csdn.service.ServiceImpl"scope="singleton">
```

测试:

```java
@Test
public void test03(){
    ApplicationContext context = new
ClassPathXmlApplicationContext("applicationContext.xml");
    User user = (User) context.getBean("user");
    User user2 = (User) context.getBean("user");
    System.out.println(user==user2);
}
```

输出结果为：True！



### 6.4.2 Prototype（原型模式）

![在这里插入图片描述](https://img-blog.csdnimg.cn/6db20cac363349b087864ed3eea3db5c.png#pic_center)
当一个bean的作用域为Prototype，表示一个bean定义对应多个对象实例。Prototype作用域的bean会 导致在每次对该bean请求(将其注入到另一个bean中，或者以程序的方式调用容器的getBean()方法) 时都会创建一个新的bean实例。Prototype是原型类型，它在我们创建容器的时候并没有实例化，而是 当我们获取bean的时候才会去创建一个对象，而且我们每次获取到的对象都不是同一个对象。根据经 验，对有状态的bean应该使用prototype作用域，而对无状态的bean则应该使用singleton作用域。在 XML中将bean定义成prototype，可以这样配置:

```xml
<bean id="account" 
class="com.foo.DefaultAccount" 
scope="prototype"/> 
或者
<bean id="account" 
class="com.foo.DefaultAccount" 
singleton="false"/>
```

用6.4.1的测试类测试，输出结果为False！

也可以检查hashcode是否一致:

```java
    User user = (User) context.getBean("user");
    User user2 = (User) context.getBean("user");
	System.out.println(user.hashcode());
	System.out.println(user2.hashcode());
    System.out.println(user==user2);
```

每一次从容器中get都会产生新的对象！

### 6.4.3 其余四种

request 、 session 、application 只能在web中用到。

最后两种作用域常常归结为一种。

---

# 7、Bean的自动装配

- 自动装配是spring满足bean依赖的一种方式。
- spring会在上下文中自动寻找并自动给bean装配属性。

在spring中有三种装配的方式：

1. 在xml中显式配置
2. 在java中显式配置
3. 隐式的自动装配bean（重点）

## 7.1 测试

新建两个实体类，Cat Dog 都有一个叫的方法

```java
public class Cat {
    public void shout() {
        System.out.println("miao~");
    }
}

public class Dog {
    public void shout() {
        System.out.println("wang~");
    }
}
```

新建一个用户类 User

```java
public class User {
    private Cat cat;
    private Dog dog;
    private String str;
}
set
get
tostring
```

xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="dog" class="com.kuang.pojo.Dog"/>
    <bean id="cat" class="com.kuang.pojo.Cat"/>
    <bean id="user" class="com.kuang.pojo.User">
        <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>
        <property name="str" value="qinjiang"/>
    </bean>
</beans>

```

测试

```java
public class MyTest {
    @Test
    public void testMethodAutowire() {
        ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
        User user = (User) context.getBean("user");
        user.getCat().shout();
        user.getDog().shout();
} 
}
```

## 7.2、byName

autowire byName (按名称自动装配) 由于在手动配置xml过程中，常常发生字母缺漏和大小写等错误，而无法对其进行检查，使得开发效率
降低。
采用自动装配将避免这些错误，并且使配置简单化。
测试:

1. 修改bean配置，增加一个属性 autowire="byName"

```xml
<bean id="user" class="com.kuang.pojo.User" autowire="byName">
    <property name="str" value="qinjiang"/>
</bean>
```

2. 再次测试，结果依旧成功输出!
3. 我们将 cat 的bean id修改为 catXXX
4. 再次测试， 执行时报空指针java.lang.NullPointerException。因为按byName规则找不对应set方 法，真正的setCat就没执行，对象就没有初始化，所以调用时就会报空指针错误。
   小结:
   当一个bean节点带有 autowire byName的属性时。
5. 将查找其类中所有的set方法名，例如setCat，获得将set去掉并且首字母小写的字符串，即cat。 2. 去spring容器中寻找是否有此字符串名称id的对象。
6. 如果有，就取出注入;如果没有，就报空指针异常。


## 7.3、byType

autowire byType (按类型自动装配)
使用autowire byType首先需要保证:同一类型的对象，在spring容器中唯一。如果不唯一，会报不唯一 的异常。

> NoUniqueBeanDefinitionException

测试:

1. 将user的bean配置修改一下 : ==autowire="byType"==
2. 测试，正常输出
3. 在注册一个cat 的bean对象!

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
<bean id="user" class="com.kuang.pojo.User" autowire="byType">
    <property name="str" value="qinjiang"/>
</bean>
```

4. 测试，报错:NoUniqueBeanDefinitionException
5. 删掉cat2，将cat的bean名称改掉!测试!因为是按类型装配，所以并不会报异常，也不影响最后的结果。甚至将id属性去掉，也不影响结果。
   这就是按照类型自动装配!

## 7.4 使用注解

jdk1.5开始支持注解，spring2.5开始全面支持注解。 准备工作: 利用注解的方式注入属性。

1. 在spring配置文件中引入context文件头

```xml
xmlns:context="http://www.springframework.org/schema/context"
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd

```


2. 开启属性注解支持!

```xml
<context:annotation-config/>
```

### 7.4.1、@Autowired

注解是写在class中 属性或者set方法上。 
在方法名后()中加入@Nullable有参构造器为空也不报错 。
==Autowired默认bytype方式==


- @Autowired是按类型自动转配的，不支持id匹配。
- 需要导入 spring-aop的包! 测试:

1. 将User类中的set方法去掉，使用@Autowired注解


```java
public class User {
    @Autowired
    private Cat cat;
    @Autowired
    private Dog dog;
    private String str;
    public Cat getCat() {
        return cat;
    }
    public Dog getDog() {
    return dog; }
    public String getStr() {
        return str;
}
 }
```

2. 此时配置文件内容

```xml
<context:annotation-config/>
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>
<bean id="user" class="com.kuang.pojo.User"/>

```

3. 测试，成功输出结果!

扩展：@Autowired(required=false) 说明: false，对象可以为null;true，对象必须存对象，不能为null。

```java
//如果允许对象为null，设置required = false,默认为true @Autowired(required = false)
private Cat cat;
```

### 7.4.2、@Qualifier

- @Autowired是根据类型自动装配的，加上@Qualifier则可以根据byName的方式自动装配
- @Qualifier不能单独使用。 测试实验步骤:

1. 配置文件修改内容，保证类型存在对象。且名字不为类的默认名字!

```xml
<bean id="dog1" class="com.kuang.pojo.Dog"/>
<bean id="dog2" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
```

2. 没有加Qualifier测试，直接报错 
3. 在属性上添加Qualifier注解

```java
@Autowired
@Qualifier(value = "cat2")
private Cat cat;
@Autowired
@Qualifier(value = "dog2")
private Dog dog;
```

4. 测试，成功输出!

### 7.4.3、@Resource

- @Resource如有指定的name属性，先按该属性进行byName方式查找装配; 
- 其次再进行默认的byName方式进行装配;
- 如果以上都不成功，则按byType的方式自动装配。
- 都不成功，则报异常。


实体类:

```java
public class User {
//如果允许对象为null，设置required = false,默认为true @Resource(name = "cat2")
private Cat cat;
@Resource
private Dog dog;
private String str;
}
```

beans.xml

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
<bean id="user" class="com.kuang.pojo.User"/>
```


测试:结果OK 

配置文件2:beans.xml ， 删掉cat2

```xml
<beanid="dog"class="com.kuang.pojo.Dog"/> <beanid="cat1"class="com.kuang.pojo.Cat"/>\
```

实体类上只保留注解

```java
@Resource
private Cat cat;
@Resource
private Dog dog;
```

结果:OK 结论:先进行byName查找，失败;再进行byType查找，成功。

---

### 7.5、小结

@Autowired与@Resource异同:

1. 两者都可以自动装配bean，都可以卸写在属性字段上，或写在setter方法上。
2. @Autowired默认采取类型装配(属于spring规范)，默认情况下必须要求依赖对象必须存在，如果 要允许null 值，可以设置它的required属性为false==如:@Autowired(required=false) ，如果我
   们想使用名称装配可以结合@Qualifier注解进行使用。
3. @Resource(属于J2EE复返)，默认按照名称进行装配，名称可以通过name属性进行指定。如果没有指定name属性，当注解写在字段上时，默认取字段名进行按照名称查找，如果注解写在 setter方法上默认取属性名进行装配。 当找不到与名称匹配的bean时才按照类型进行装配。但是 需要注意的是，如果name属性一旦指定，就只会按照名称进行装配。

二者执行顺序：

- @Autowired：bytype ——> byname
- @Resource：byname ——> bytype


---

# 8、使用注解开发

## 8.1、说明

在spring4之后，想要使用注解形式，必须得要引入aop的包

【aop的包在mvc下已经包含，所以只需要导入约束】

![在这里插入图片描述](https://img-blog.csdnimg.cn/d3c520173b134f499a748d6edd816c0d.png#pic_center)



在配置文件当中，还得要引入一个context约束

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
</beans>

```

## 8.2、Bean的实现

我们之前都是使用 bean 的标签进行bean注入，但是实际开发中，我们一般都会使用注解!


### 1. 配置扫描哪些包下的注解


```xml
1 <!--指定注解扫描包-->
2 <context:component-scanbase-package="com.kuang.pojo"/>
```

### 2. 在指定包下编写类，增加注解

component注解需要加在类上而不是方法上
getbean名字默认为类的小写，普遍唯一


```java
@Component("user")
// 相当于配置文件中 <bean id="user" class="当前注解的类"/> public class User {
public String name = "秦疆"; }

```

### 3. 测试

```java
@Test
public void test(){
    ApplicationContext applicationContext =
        new ClassPathXmlApplicationContext("beans.xml");
    User user = (User) applicationContext.getBean("user");
    System.out.println(user.name);
}
```

## 8.3、属性注入

使用注解注入属性

1. 可以不用提供set方法，直接在直接名上添加@value("值")

```java
@Component("user")
// 相当于配置文件中 <bean id="user" class="当前注解的类"/> public class User {
@Value("秦疆")
// 相当于配置文件中 <property name="name" value="秦疆"/> public String name;
}
```

2. 如果提供了set方法，在set方法上添加@value("值");

```java 
@Component("user")
public class User {
    public String name;
@Value("秦疆")
public void setName(String name) {
        this.name = name;
    }
}
```

## 8.4、衍生注解

我们这些注解，就是替代了在配置文件当中配置步骤而已!更加的方便快捷!


@Component（组成部分）三个衍生注解 为了更好的进行分层，Spring可以使用其它三个注解，功能一样，目前使用哪一个功能都一样。

- @Controller （管理者） : web层
- @Service （服务）: service层  （业务层）
- @Repository （仓库）: dao层 （数据访问层）
  写上这些注解，就相当于将这个类交给Spring管理装配了!

**web结构**
浏览器端——>web层——>业务层——>数据访问层——>数据库




## 8.5、自动装配注解

自动装配注解就是
@Autowired【@Qualifier(value = “xxx”)】、  
@Nullable、
@ Resource等等


## 8.6、作用域

@scope
相当于 bean scope  = "singleton"

- singleton:默认的，Spring会采用单例模式创建这个对象。关闭工厂 ，所有的对象都会销毁。
- prototype:多例模式。关闭工厂 ，所有的对象不会销毁。内部的垃圾回收机制会回收

```java
@Controller("user")
@Scope("prototype")
public class User {
@Value("XXX")
    public String name;
}

```

## 8.7、小结

XML与注解比较

- XML可以适用任何场景 ，结构清晰，维护方便 
- ==注解不是自己提供的类使用不了==，开发简单方便

**xml与注解整合开发** :推荐最佳实践

- xml管理Bean
- 注解完成属性注入
- 使用过程中， 可以不用扫描，扫描是为了类上的注解

```xml
<context:annotation-config/>
```


***作用:***

- 进行注解驱动注册，从而使注解生效 
- 用于激活那些已经在spring容器里注册过的bean上面的注解，也就是显示的向Spring注册 
- 如果不扫描包，就需要手动配置bean
- 如果不加注解驱动，则注入的值为null!


## 8.8、基于Java类进行配置

JavaConfig 原来是 Spring 的一个子项目，它通过 Java 类的方式提供 Bean 的定义信息，在 Spring4 的
版本， JavaConfig 已正式成为 Spring4 的核心功能 。

测试环境搭建：

1. 编写一个实体类，Dog

```java
@Component //将这个类标注为Spring的一个组件，放到容器中! public class Dog {
    public String name = "dog";
}
```

2. 新建一个config配置包，编写一个MyConfig配置类

```xml
@Configuration //代表这是一个配置类 public class MyConfig {
@Bean //通过方法注册一个bean，这里的返回值就Bean的类型，方法名就是bean的id! public Dog dog(){
        return new Dog();
    }
}
```

3. 测试

```java
@Test
public void test2(){
    ApplicationContext applicationContext =
            new AnnotationConfigApplicationContext(MyConfig.class);
    Dog dog = (Dog) applicationContext.getBean("dog");
    System.out.println(dog.name);
}

```


4. 成功输出结果!



**导入其他配置如何做呢?**

-  我们再编写一个配置类!

```java
@Configuration //代表这是一个配置类 
public class MyConfig2 {
}
```

- 在之前的配置类中我们来选择导入这个配置类

```java
@Configuration
@Import(MyConfig2.class) //导入合并其他配置类，类似于配置文件中的 inculde 标签 public class MyConfig {
@Bean
    public Dog dog(){
        return new Dog();
} }
```

关于这种Java类的配置方式，我们在之后的SpringBoot 和 SpringCloud中还会大量看到，我们需要知道 这些注解的作用即可!

---


# 9、代理模式

==AOP底层机制就是动态代理！==

代理模式分：

- 动态代理
- 静态代理

代理模式图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/02efc8e864aa48d3b3a3910f075c836c.png#pic_center)

## 9.1、静态代理

静态代理角色分析

- 抽象角色 : 一般使用接口或者抽象类来实现（对对象进行相同抽取）
- 真实角色 : 被代理的角色 （房东）
- 代理角色 : 代理真实角色 ; 代理真实角色后 , 一般会做一些附属的操作 （中介）
- 客户 : 使用代理角色来进行一些操作 . （租户）


代码实现
Rent . java 即抽象角色

```java
//抽象角色:租房
public interface Rent {
    public void rent();
}
```

Host . java 即真实角色

```java
//真实角色: 房东，房东要出租房子
public class Host implements Rent{
public void rent() { System.out.println("房屋出租");
} }
```

Proxy . java 即代理角色

```java
//代理角色:中介
public class Proxy implements Rent {
    private Host host;
    public Proxy() { }
    public Proxy(Host host) {
        this.host = host;
    }
    //租房
public void rent(){
        seeHouse();
        host.rent();
        fare();
}
//看房
public void seeHouse(){
System.out.println("带房客看房"); }
//收中介费
public void fare(){
System.out.println("收中介费"); }
}
```

Client . java 即客户

```java
//客户类，一般客户都会去找代理! public class Client {
public static void main(String[] args) { //房东要租房
Host host = new Host(); //中介帮助房东
Proxy proxy = new Proxy(host);
//你去找中介!
        proxy.rent();
    }
}
```

分析：在此过程中虽然用户并没有接触到房东，但是确确实实租到了房东的房子，通过的就是中介，也就是代理，这就是代理模式。



## 9.2、静态代理的好处

- 可以使得我们的真实角色更加纯粹 ，只需要把注意力集中到我们所需要的功能上。
- 公共的业务由代理来完成 . 实现了业务的分工 , 
- 公共业务发生扩展时变得更加集中和方便 .
  缺点 :
- 单一真实角色只对应一个代理类，如果上增数量，则代理数量同步上增，导致工作量变大，代码冗余度增加，同时程序也变得笨重。

于是动态代理克服静态代理缺点。


## 9.3、静态代理再理解

练习步骤:

1. 创建一个抽象角色，比如咋们平时做的用户业务，抽象起来就是增删改查!

```java
//抽象角色:增删改查业务
public interface UserService {
    void add();
    void delete();
    void update();
    void query();
}
```


2. 我们需要一个真实对象来完成这些增删改查操作

```java
//真实对象，完成增删改查操作的人
public class UserServiceImpl implements UserService {
public void add() { System.out.println("增加了一个用户");
}
public void delete() { System.out.println("删除了一个用户");
}
public void update() { System.out.println("更新了一个用户");
}
public void query() { System.out.println("查询了一个用户");
} }
```

3. 需求来了，现在我们需要增加一个日志功能，怎么实现!
   思路1 :在实现类上增加代码 【麻烦!】
   思路2:使用代理来做，能够不改变原来的业务情况下，实现此功能就是最好的了! 
4. 设置一个代理类来处理日志! 代理角色

```java
//代理角色，在这里面增加日志的实现
public class UserServiceProxy implements UserService {
    private UserServiceImpl userService;
    public void setUserService(UserServiceImpl userService) {
        this.userService = userService;
}
    public void add() {
        log("add");
        userService.add();
    }
    public void delete() {
        log("delete");
        userService.delete();
    }
    public void update() {
        log("update");
        userService.update();
    }
 public void query() {
        log("query");
        userService.query();
    }
public void log(String msg){ System.out.println("执行了"+msg+"方法");
} 
}

```

5. 测试访问类:

```java
public class Client {
    public static void main(String[] args) {
//真实业务
UserServiceImpl userService = new UserServiceImpl(); //代理类
UserServiceProxy proxy = new UserServiceProxy(); //使用代理类实现日志功能! proxy.setUserService(userService);
        proxy.add();
    }
}
```



==我们在不改变原来的代码的情况下，实现了对原有功能的增强，这是AOP中最核心的思想==

![在这里插入图片描述](https://img-blog.csdnimg.cn/f935f117ba274f239f9ed95bed834fc6.png#pic_center)
 【聊聊AOP:纵向开发，横向开发】




---

## 9.4、动态代理

- 动态代理的角色和静态代理的一样 .
- 动态代理的代理类是动态生成的 . 静态代理的代理类是我们提前写好的 
- 动态代理分为两类 : 一类是基于接口动态代理 , 一类是基于类的动态代理
  基于接口的动态代理----JDK动态代理
  基于类的动态代理--cglib
  现在用的比较多的是 javasist 来生成动态代理 . 百度一下javasist
  我们这里使用JDK的原生代码来实现，其余的道理都是一样的!

JDK的动态代理需要了解两个类
核心 : InvocationHandler 和 Proxy ， 打开JDK帮助文档看看

【InvocationHandler:调用处理程序】

![在这里插入图片描述](https://img-blog.csdnimg.cn/80fa1e45f02d491db1105fee03a5b609.png#pic_center)


【Proxy : 代理】

![在这里插入图片描述](https://img-blog.csdnimg.cn/ee3c09f6dcd84a4ab8e68326ab7d5438.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/5dfb79a1a07f4894a2a8960405124e1e.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/7ade4d19e2c24a23aa6fcf28ebabe92c.png#pic_center)

代码实现
抽象角色和真实角色和之前的一样! Rent . java 即抽象角色


```java
//抽象角色:租房
public interface Rent {
    public void rent();
}
```

Host . java 即真实角色


```java
//真实角色: 房东，房东要出租房子
public class Host implements Rent{
public void rent() { System.out.println("房屋出租");
} }
```

ProxyInvocationHandler. java 即代理角色

```java
public class ProxyInvocationHandler implements InvocationHandler {
    private Rent rent;
    public void setRent(Rent rent) {
        this.rent = rent;
}
//生成代理类，重点是第二个参数，获取要代理的抽象角色!之前都是一个角色，
//w现在可以代理一 类角色
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                rent.getClass().getInterfaces(),this);
}
// proxy : 代理类 method : 代理类的调用处理程序的方法对象.
// 处理代理实例上的方法调用并返回结果
@Override
public Object invoke(Object proxy, Method method, Object[] args) throws
Throwable {
        seeHouse();
//核心:本质利用反射实现!
Object result = method.invoke(rent, args); fare();
return result;
}
//看房
public void seeHouse(){
System.out.println("带房客看房"); }
//收中介费
public void fare(){
System.out.println("收中介费"); }
}
```

Client . java

```java
//租客
public class Client {
public static void main(String[] args) {
 //真实角色
Host host = new Host();
//代理实例的调用处理程序
ProxyInvocationHandler pih = new ProxyInvocationHandler(); pih.setRent(host); //将真实角色放置进去!
Rent proxy = (Rent)pih.getProxy(); //动态生成对应的代理类! proxy.rent();
}
}
```

核心:一个动态代理 , 一般代理某一类业务 , 一个动态代理可以代理多个类，代理的是接口!、


## 9.5、深化理解

我们来使用动态代理实现代理我们后面写的UserService! 我们也可以编写一个通用的动态代理实现的类!所有的代理对象设置为Object即可!


![在这里插入图片描述](https://img-blog.csdnimg.cn/39c336aa8ff149cc81b96a0f99a43f8d.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/8d9afd48698440b1abcf058697ade273.png#pic_center)



## 9.6、动态代理的好处

静态代理有的它都有，静态代理没有的，它也有!

- 可以使得我们的真实角色更加纯粹 . 不再去关注一些公共的事情 . 
- 公共的业务由代理来完成 . 实现了业务的分工 ,
- 公共业务发生扩展时变得更加集中和方便 .
- 一个动态代理 , 一般代理某一类业务 
- 一个动态代理可以代理多个类，代理的是接口!

---


# 10、AOP

## 10.1 什么是AOP

AOP(Aspect Oriented Programming)意为:面向切面编程，通过预编译方式和运行期动态代理实现 程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的 一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使 得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20b03aa6e4c24521ae966a9c7a054b7d.png#pic_center)

## 10.2 Aop在Spring中的作用 

==提供声明式事务;允许用户自定义切面==

- 横切关注点:跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要 关注的部分，就是横切关注点。如日志 , 安全 , 缓存 , 事务等等 ....
- 切面(ASPECT):横切关注点 被模块化 的特殊对象。即，它是一个类。 
- 通知(Advice):切面必须要完成的工作。即，它是类中的一个方法。 
- 目标(Target):被通知对象。
- 代理(Proxy):向目标对象应用通知之后创建的对象。 
- 切入点(PointCut):切面通知 执行的 “地点”的定义。 
- 连接点(JointPoint):与切入点匹配的执行点。

![在这里插入图片描述](https://img-blog.csdnimg.cn/8d95566f85dd47f19f1f389d1c05b71e.png#pic_center)
SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice:
![在这里插入图片描述](https://img-blog.csdnimg.cn/414979011f1e49bab4c10f77734fbe37.png#pic_center)
即 Aop 在 不改变原有代码的情况下 , 去增加新的功能 .

## 10.3 使用Spring实现Aop

【重点】使用AOP织入，需要导入一个依赖包!

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```


### 第一种方式

**通过 Spring API 实现**

首先编写我们的业务接口和实现类

```java 
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void search();
}
```

```java
public class UserServiceImpl implements UserService{
@Override
public void add() { System.out.println("增加用户");
}
@Override
public void delete() { System.out.println("删除用户");
}
@Override
public void update() { System.out.println("更新用户");
}
@Override
public void search() { System.out.println("查询用户");
}
 }

```

然后去写我们的增强类 , 我们编写两个 , 一个前置增强 一个后置增强

```java
public class Log implements MethodBeforeAdvice {
//method : 要执行的目标对象的方法 //objects : 被调用的方法的参数 //Object : 目标对象
@Override
    public void before(Method method, Object[] objects, Object o) throws
Throwable {
System.out.println( o.getClass().getName() + "的" + method.getName() + "方法被执行了");
} 
}

```



```java
public class AfterLog implements AfterReturningAdvice { 
//returnValue 返回值
//method被调用的方法
//args 被调用的方法的对象的参数
//target 被调用的目标对象
@Override
public void afterReturning(Object returnValue, Method method, Object[]args, Object target) throws Throwable { 
	System.out.println("执行了" + target.getClass().getName() 	    +"的"+method.getName()+"方法,"
+"返回值:"+returnValue);
} }
```



最后去spring的文件中注册 , 并实现aop切入实现 , 注意导入约束 .


```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
<!--注册bean-->
<bean id="userService" class="com.kuang.service.UserServiceImpl"/> <bean id="log" class="com.kuang.log.Log"/>
<bean id="afterLog" class="com.kuang.log.AfterLog"/>
<!--aop的配置--> <aop:config>
<!--切入点 expression:表达式匹配要执行的方法-->
        <aop:pointcut id="pointcut" expression="execution(*
com.kuang.service.UserServiceImpl.*(..))"/>
<!--执行环绕; advice-ref执行方法 . pointcut-ref切入点--> <aop:advisor advice-ref="log" pointcut-ref="pointcut"/> <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
    </aop:config>
</beans>

```


测试

```java
public class MyTest {
    @Test
    public void test(){
        ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
        UserService userService = (UserService)
context.getBean("userService");
        userService.search();
} }

```



Aop的重要性 : 很重要 . 一定要理解其中的思路 , 主要是思想的理解这一块 . Spring的Aop就是将公共的业务 (日志 , 安全等) 和领域业务结合起来 , 当执行领域业务时 , 将会把公共业
务加进来 . 实现公共业务的重复利用 . 领域业务更纯粹 , 程序猿专注领域业务 , 其本质还是动态代理 .

## 第二种方式

自定义类来实现Aop
目标业务类不变依旧是userServiceImpl 
第一步 : 写我们自己的一个切入类

```java
public class DiyPointcut {
public void before(){ System.out.println("---------方法执行前---------");
    }
    public void after(){
System.out.println("---------方法执行后---------"); }
}

```

去spring中配置

```xml
<!--第二种方式自定义实现-->
<!--注册bean-->
<bean id="diy" class="com.kuang.config.DiyPointcut"/>
<!--aop的配置--> <aop:config>
<!--第二种方式:使用AOP的标签实现--> <aop:aspect ref="diy">
        <aop:pointcut id="diyPonitcut" expression="execution(*
com.kuang.service.UserServiceImpl.*(..))"/>
        <aop:before pointcut-ref="diyPonitcut" method="before"/>
        <aop:after pointcut-ref="diyPonitcut" method="after"/>
    </aop:aspect>
</aop:config>
```

测试:

```java
public class MyTest {
    @Test
    public void test(){
        ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
        UserService userService = (UserService)
context.getBean("userService");
        userService.add();
} }

```


---

## 第三种方式

使用注解实现
第一步:编写一个注解实现的增强类


```java
package com.kuang.config;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
@Aspect
public class AnnotationPointcut {
    @Before("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void before(){
System.out.println("---------方法执行前---------"); }
    @After("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void after(){
System.out.println("---------方法执行后---------"); }
    @Around("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable {

	System.out.println("环绕前"); 
	System.out.println("签名:"+jp.getSignature()); 
	//执行目标方法	proceed
	Object proceed = jp.proceed(); 
	System.out.println("环绕后"); 
	System.out.println(proceed);

}
}

```

第二步:在Spring配置文件中，注册bean，并增加支持注解的配置

```xml
<!--第三种方式:注解实现-->
<bean id="annotationPointcut" class="com.kuang.config.AnnotationPointcut"/> <aop:aspectj-autoproxy/>

```

aop:aspectj-autoproxy:说明



> 通过aop命名空间的<aop:aspectj-autoproxy />声明自动为spring容器中那些配置@aspectJ切面
> 的bean创建代理，织入切面。当然，spring 在内部依旧采用 
>
> AnnotationAwareAspectJAutoProxyCreator进行自动代理的创建工作，但具体实现的细节已经被
> <aop:aspectj-autoproxy />隐藏起来了
>
> <aop:aspectj-autoproxy />有一个proxy-target-class属性，默认为false，表示使用jdk动态
> 代理织入增强，当配为<aop:aspectj-autoproxy poxy-target-class="true"/>时，表示使用
> CGLib动态代理技术织入增强。不过即使proxy-target-class设置为false，如果目标类没有声明接
> 口，则spring将自动使用CGLib动态代理。

---

# 11、整合Mybatis

## 步骤:

- 导入相关jar包 

1. junit

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

2. mybatis

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>
```

3. mysql-connector-java

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>

```

4. spring相关

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.1.10.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.1.10.RELEASE</version>
</dependency>

```

5. aspectJ AOP 织入器

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```

6. mybatis-spring整合包 【重点】

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.2</version>
</dependency>

```

7. 配置Maven静态资源过滤问题!

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>

```

-  编写配置文件
 -  代码实现

## 回忆MyBatis


编写pojo实体类

```java
package com.kuang.pojo;
public class User {
private int id;//id 
private String name; //姓名 
private String pwd; //密码
}
```


实现mybatis的配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>
     <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url"
value="jdbc:mysql://localhost:3306/mybatis?
useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <package name="com.kuang.dao"/>
    </mappers>
</configuration>
```


UserDao接口编写

```java
public interface UserMapper {
    public List<User> selectUser();
}
```

接口对应的Mapper映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.dao.UserMapper">
    <select id="selectUser" resultType="User">
      select * from user
    </select>
</mapper>

```


测试类


```java
@Test
public void selectUser() throws IOException {
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new
SqlSessionFactoryBuilder().build(inputStream);
    SqlSession sqlSession = sqlSessionFactory.openSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    List<User> userList = mapper.selectUser();
    for (User user: userList){
        System.out.println(user);
    }
	sqlSession.close();
}
```


## MyBatis-Spring学习

**引入Spring之前需要了解mybatis-spring包中的一些重要类;**

[http://www.mybatis.org/spring/zh/index.html](http://www.mybatis.org/spring/zh/index.html)

**什么是 MyBatis-Spring?**

MyBatis-Spring 会帮助你将 MyBatis 代码无缝地整合到 Spring 中。


**知识基础**

在开始使用 MyBatis-Spring 之前，你需要先熟悉 Spring 和 MyBatis 这两个框架和有关它们的术语。这 很重要
  MyBatis-Spring 需要以下版本:

![在这里插入图片描述](https://img-blog.csdnimg.cn/77282c7eef764a319b1400e5b9a468b8.png#pic_center)


如果使用 Maven 作为构建工具，仅需要在 pom.xml 中加入以下代码即可:


```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.2</version>
</dependency>


```

要和 Spring 一起使用 MyBatis，需要在 Spring 应用上下文中定义至少两样东西:一个 ==SqlSessionFactory== 和至少一个数据映射器类。

在 MyBatis-Spring 中，可使用 ==SqlSessionFactoryBean ==来创建 ==SqlSessionFactory== 。 要配置 这个工厂 bean，只需要把下面代码放在 Spring 的 XML 配置文件中:


```xml
<bean id="sqlSessionFactory"
class="org.mybatis.spring.SqlSessionFactoryBean">
  <property name="dataSource" ref="dataSource" />
</bean>

```


![在这里插入图片描述](https://img-blog.csdnimg.cn/71e3c8232b394549b5f02a529ea32937.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/358b1d3f89d24624a10a2d4a19c9d364.png#pic_center)

```xml
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
  <constructor-arg index="0" ref="sqlSessionFactory" />
</bean>

```


现在，这个 bean 就可以直接注入到你的 DAO bean 中了。你需要在你的 bean 中添加一个 SqlSession 属性，就像下面这样:


```java
public class UserDaoImpl implements UserDao {
  private SqlSession sqlSession;
  public void setSqlSession(SqlSession sqlSession) {
    this.sqlSession = sqlSession;
}
  public User getUser(String userId) {
    return sqlSession.getMapper...;
} 
}

```

按下面这样，注入 ==SqlSessionTemplate== :

```xml
<bean id="userDao" class="org.mybatis.spring.sample.dao.UserDaoImpl">
  <property name="sqlSession" ref="sqlSession" />
</bean>

```


## 整合实现一

1. 引入Spring配置文件beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
```

2. 配置数据源替换mybaits的数据源

```xml
<!--配置数据源:数据源有非常多，可以使用第三方的，也可使使用Spring的-->
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis?
useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
</bean>
```



3. 配置SqlSessionFactory，关联MyBatis

```xml

<!--配置SqlSessionFactory--> <beanid="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<property name="dataSource" ref="dataSource"/> <!--关联Mybatis-->
<property name="configLocation" value="classpath:mybatis-
config.xml"/>
    <property name="mapperLocations"
value="classpath:com/kuang/dao/*.xml"/>
</bean>


```

4. 注册sqlSessionTemplate，关联sqlSessionFactory;

```xml
<!--注册sqlSessionTemplate , 关联sqlSessionFactory-->
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
<!--利用构造器注入-->
    <constructor-arg index="0" ref="sqlSessionFactory"/>
</bean>
```


5. 增加Dao接口的实现类;私有化sqlSessionTemplate

```java
public class UserDaoImpl implements UserMapper { //sqlSession不用我们自己创建了，Spring来管理
    private SqlSessionTemplate sqlSession;
    public void setSqlSession(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
}
    public List<User> selectUser() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        return mapper.selectUser();
}
 }
```

6. 注册bean实现

```xml
<bean id="userDao" class="com.kuang.dao.UserDaoImpl">
    <property name="sqlSession" ref="sqlSession"/>
</bean>

```


7. 测试

```java
@Test
    public void test2(){
        ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
        UserMapper mapper = (UserMapper) context.getBean("userDao");
        List<User> user = mapper.selectUser();
        System.out.println(user);
}

```


结果成功输出!现在我们的Mybatis配置文件的状态!发现都可以被Spring整合!


```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>
</configuration>

```


# 整合实现二


mybatis-spring1.2.3版以上的才有这个 . 
官方文档截图 :
dao继承Support类 , 直接利用 getSqlSession() 获得 , 然后直接注入SqlSessionFactory . 比起方式1 , 不 需要管理SqlSessionTemplate , 而且对事务的支持更加友好 . 可跟踪源码查看
![在这里插入图片描述](https://img-blog.csdnimg.cn/06ba11adad5a4e578bc8364cd884618b.png#pic_center)

**测试:**

1. 将我们上面写的UserDaoImpl修改一下:

```java
public class UserDaoImpl extends SqlSessionDaoSupport implements
UserMapper {
    public List<User> selectUser() {
        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
        return mapper.selectUser();
} }
```


2. 修改bean的配置

```xml
<bean id="userDao" class="com.kuang.dao.UserDaoImpl">
    <property name="sqlSessionFactory" ref="sqlSessionFactory" />
</bean>
```


3. 测试

```java
@Test
public void test2(){
    ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
    UserMapper mapper = (UserMapper) context.getBean("userDao");
    List<User> user = mapper.selectUser();
    System.out.println(user);
}
```

**总结 : 整合到spring中以后可以完全不要mybatis的配置文件，除了这些方式可以实现整合之外，我们还 可以使用注解来实现，这个等我们后面学习SpringBoot的时候还会测试整合!**



# 12、声明式事务

## 12.1、回顾事务

- 事务在项目开发过程非常重要，涉及到数据的一致性的问题，不容马虎!
- 事务管理是企业级应用程序开发中必备技术，用来确保数据的完整性和一致性。
  ==事务就是把一系列的动作当成一个独立的工作单元，这些动作要么全部完成，要么全部不起作用。==

**事务四个属性ACID**

1. 原子性(atomicity)
   事务是原子性操作，由一系列动作组成，事务的原子性确保动作要么全部完成，要么完全不起作用

2. 一致性(consistency)
   一旦所有事务动作完成，事务就要被提交。数据和资源处于一种满足业务规则的一致性状态中 

3. 隔离性(isolation)
   可能多个事务会同时处理相同的数据，因此每个事务都应该与其他事务隔离开来，防止数据损坏

4. 持久性(durability)
   事务一旦完成，无论系统发生什么错误，结果都不会受到影响。通常情况下，事务的结果被写到持久化存储器中


## 12.2、测试

将上面的代码拷贝到一个新项目中
在之前的案例中，我们给userDao接口新增两个方法，删除和增加用户;

```java
//添加一个用户
int addUser(User user);
//根据id删除用户
int deleteUser(int id);
```

mapper文件，我们故意把 deletes 写错，测试!


```xml
<insert id="addUser" parameterType="com.kuang.pojo.User">
 insert into user (id,name,pwd) values (#{id},#{name},#{pwd})
 </insert>
 <delete id="deleteUser" parameterType="int">
 deletes from user where id = #{id}
</delete>
```


编写接口的实现类，在实现类中，我们去操作一波

```java
public class UserDaoImpl extends SqlSessionDaoSupport implements UserMapper
{
//增加一些操作
public List<User> selectUser() {
User user = new User(4,"小明","123456");
UserMapper mapper = getSqlSession().getMapper(UserMapper.class); mapper.addUser(user);
mapper.deleteUser(4);
return mapper.selectUser();
}
//新增
public int addUser(User user) {
        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
        return mapper.addUser(user);
    }
//删除
public int deleteUser(int id) {
        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
        return mapper.deleteUser(id);
    }
}
```

测试

```java
@Test
public void test2(){
    ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
    UserMapper mapper = (UserMapper) context.getBean("userDao");
    List<User> user = mapper.selectUser();
    System.out.println(user);
}
```


报错:sql异常，delete写错了
结果 :插入成功! 
没有进行事务的管理;我们想让他们都成功才成功，有一个失败，就都失败，我们就应该需要==事务==! 
以前我们都需要自己手动管理事务，十分麻烦! 
但是Spring给我们提供了事务管理，我们只需要配置即可;


## 12.3、Spring中的事务管理

Spring在不同的事务管理API之上定义了一个抽象层，使得开发人员不必了解底层的事务管理API就可以使用Spring的事务管理机制。Spring支持编程式事务管理和声明式的事务管理。

**编程式事务管理**

- 将事务管理代码嵌到业务方法中来控制事务的提交和回滚
 - 缺点:必须在每个事务操作业务逻辑中包含额外的事务管理代码

**声明式事务管理**

- 一般情况下比编程式事务好用。 
- 将事务管理代码从业务方法中分离出来，以声明的方式来实现事务管理。
 - 将事务管理作为横切关注点，通过aop方法模块化。Spring中通过Spring AOP框架支持声明式事务 管理。


**使用Spring管理事务，注意头文件的约束导入 : tx**

```xml
xmlns:tx="http://www.springframework.org/schema/tx"
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd">
```


**事务管理器**

- 无论使用Spring的哪种事务管理策略(编程式或者声明式)事务管理器都是必须的。 
- 就是 Spring的核心事务管理抽象，管理封装了一组独立于技术的方法。

**JDBC事务**

```xml
<bean id="transactionManager"
class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
 </bean>
```


**配置好事务管理器后我们需要去配置事务的通知**

```xml
<!--配置事务通知-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <tx:attributes>
<!--配置哪些方法使用什么样的事务,配置事务的传播特性--> <tx:method name="add" propagation="REQUIRED"/> <tx:method name="delete" propagation="REQUIRED"/> <tx:method name="update" propagation="REQUIRED"/> <tx:method name="search*" propagation="REQUIRED"/> <tx:method name="get" read-only="true"/> <tx:method name="*" propagation="REQUIRED"/>
    </tx:attributes>
</tx:advice>
```


**spring事务传播特性:**

事务传播行为就是多个事务方法相互调用时，事务如何在这些方法间传播。spring支持7种事务传播行
为:

- propagation_requierd:如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这 个事务中，这是最常见的选择。 - propagation_supports:支持当前事务，如果没有当前事务，就以非事务方法执行。 
- propagation_mandatory:使用当前事务，如果没有当前事务，就抛出异常。 
- propagation_required_new:新建事务，如果当前存在事务，把当前事务挂起。 
- propagation_not_supported:以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。 
- propagation_never:以非事务方式执行操作，如果当前事务存在则抛出异常。 
- propagation_nested:如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与 propagation_required类似的操作

---

Spring 默认的事务传播行为是 PROPAGATION_REQUIRED，它适合于绝大多数的情况。

假设 ServiveX#methodX() 都工作在事务环境下(即都被 Spring 事务增强了)，假设程序中存在如下的 调用链:Service1#method1()->Service2#method2()->Service3#method3()，那么这 3 个服务类的 3 个方法通过 Spring 的事务传播机制都工作在同一个事务中。

就好比，我们刚才的几个方法存在调用，所以会被放在一组事务当中!


**配置AOP**

导入aop的头文件!

```xml
<!--配置aop织入事务--> <aop:config>
    <aop:pointcut id="txPointcut" expression="execution(* com.kuang.dao.*.*
(..))"/>
    <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointcut"/>
</aop:config>

```

**进行测试**
删掉刚才插入的数据，再次测试!

```java
@Test
public void test2(){
    ApplicationContext context = new
ClassPathXmlApplicationContext("beans.xml");
    UserMapper mapper = (UserMapper) context.getBean("userDao");
    List<User> user = mapper.selectUser();
    System.out.println(user);
}
```
