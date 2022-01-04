黑马 SpringData JPA笔记
===================

![](https://csdnimg.cn/release/blogv2/dist/pc/img/original.png)

[每天进步一點點](https://blog.csdn.net/DDDDeng_) 2020-08-24 14:29:03 

分类专栏： [Web开发](https://blog.csdn.net/ddddeng_/category_10162590.html) [Spring](https://blog.csdn.net/ddddeng_/category_10132441.html)

版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

本文链接：[https://blog.csdn.net/DDDDeng\_/article/details/108197565](https://blog.csdn.net/DDDDeng_/article/details/108197565)

课程链接：[https://www.bilibili.com/video/BV1Y4411W7Rx?from=search&seid=415951199875837982](https://www.bilibili.com/video/BV1Y4411W7Rx?from=search&seid=415951199875837982)

**第一 orm思想**

 主要目的：操作实体类就相当于操作数据库表

 建立两个映射关系：

 实体类和表的映射关系

```
	实体类中属性和字段的映射关系

```

**第二 hibernate框架介绍**

 Hibernate是一个开放源代码的对象关系映射框架，

 它对JDBC进行了非常轻量级的对象封装，

 它将POJO与数据库表建立映射关系，是一个全自动的orm框架

**第三 JPA规范**

**第四 JPA的基本操作**

```
- 环境搭建
- 完成基本的curd案例

```

《— 第1天 —》
---------

一、ORM概述
-------

ORM（Object-Relational Mapping） 表示对象关系映射。在面向对象的软件开发中，通过ORM，就可以把对象映射到关系型数据库中。只要有一套程序能够做到建立对象与数据库的关联，操作对象就可以直接操作数据库数据，就可以说这套程序实现了ORM对象关系映射

简单的说：ORM就是建立实体类和数据库表之间的关系，从而达到操作实体类就相当于操作数据库表的目的。

### 为什么使用ORM

当实现一个应用程序时（不使用O/R Mapping），我们可能会写特别多数据访问层的代码，从数据库保存数据、修改数据、删除数据，而这些代码都是重复的。而使用\*\*ORM则会大大减少重复性代码。\*\*对象关系映射（Object Relational Mapping，简称ORM），主要实现程序对象到关系数据库数据的映射。

### 常见的ORM框架

常见的orm框架：Mybatis（ibatis）、Hibernate、Jpa

二、hibernate与JPA的概述
------------------

### hibernate概述

 Hibernate是一个开放源代码的对象关系映射框架，它对JDBC进行了非常轻量级的对象封装，它将POJO与数据库表建立映射关系，是一个全自动的orm框架，hibernate可以自动生成SQL语句，自动执行，使得Java程序员可以随心所欲的使用对象编程思维来操纵数据库。

### JPA概述

JPA的全称是**Java Persistence API**， 即Java 持久化API，是SUN公司推出的一套基于ORM的规范，内部是由一系列的接口和抽象类构成。

JPA通过JDK 5.0注解描述对象－关系表的映射关系，并将运行期的实体对象持久化到数据库中。

### JPA的优势

1.  标准化
2.  容错级特性的支持
3.  简单方便
4.  查询能力
5.  高级特性

### JPA与hibernate的关系

 JPA规范本质上就是一种ORM规范，**注意不是ORM框架**——因为JPA并未提供ORM实现，它只是制订了一些规范，提供了一些编程的API接口，但具体实现则由服务厂商来提供实现。

![](https://img-blog.csdnimg.cn/20200824133406690.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

> JPA和Hibernate的关系就像JDBC和JDBC驱动的关系，JPA是规范，Hibernate除了作为ORM框架之外，它也是一种JPA实现。JPA怎么取代Hibernate呢？JDBC规范可以驱动底层数据库吗？答案是否定的，也就是说，如果使用JPA规范进行数据库操作，底层需要hibernate作为其实现类完成数据持久化工作。

三、JPA入门案例
---------

我们是实现的功能是保存一个客户到数据库的客户表中。

#### 环境搭建

1.  导入依赖：

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.hibernate.version>5.0.7.Final</project.hibernate.version>
</properties>

<dependencies>
    <!-- junit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

    <!-- hibernate对jpa的支持包 -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-entitymanager</artifactId>
        <version>${project.hibernate.version}</version>
    </dependency>

    <!-- c3p0 -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-c3p0</artifactId>
        <version>${project.hibernate.version}</version>
    </dependency>

    <!-- log日志 -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.12.1</version>
    </dependency>


    <!-- Mysql and MariaDB -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>

    <!--lombok-->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.12</version>
        <scope>provided</scope>
    </dependency>
</dependencies>

```

2. 创建客户的数据库表

   ```sql
    /*创建客户表*/
       CREATE TABLE cst_customer (
         cust_id bigint(32) NOT NULL AUTO_INCREMENT COMMENT '客户编号(主键)',
         cust_name varchar(32) NOT NULL COMMENT '客户名称(公司名称)',
         cust_source varchar(32) DEFAULT NULL COMMENT '客户信息来源',
         cust_industry varchar(32) DEFAULT NULL COMMENT '客户所属行业',
         cust_level varchar(32) DEFAULT NULL COMMENT '客户级别',
         cust_address varchar(128) DEFAULT NULL COMMENT '客户联系地址',
         cust_phone varchar(64) DEFAULT NULL COMMENT '客户联系电话',
         PRIMARY KEY (`cust_id`)
       ) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
   
   ```

3. 创建客户的实体类 & 编写实体类和数据库表的映射配置 **（重点）**

   ```java
   /**
    * 客户的实体类
    *      配置映射关系
    *
    *
    *   1.实体类和表的映射关系
    *      @Entity:声明实体类
    *      @Table : 配置实体类和表的映射关系
    *          name : 配置数据库表的名称
    *   2.实体类中属性和表中字段的映射关系
    *
    *
    */
   @Data
   @NoArgsConstructor
   @AllArgsConstructor
   
   @Entity
   @Table(name = "cst_customer")
   public class Customer {
   
       /**
        * @Id：声明主键的配置
        * @GeneratedValue:配置主键的生成策略
        *      strategy
        *          GenerationType.IDENTITY ：自增，mysql
        *                 * 底层数据库必须支持自动增长（底层数据库支持的自动增长方式，对id自增）
        *          GenerationType.SEQUENCE : 序列，oracle
        *                  * 底层数据库必须支持序列
        *          GenerationType.TABLE : jpa提供的一种机制，通过一张数据库表的形式帮助我们完成主键自增
        *          GenerationType.AUTO ： 由程序自动的帮助我们选择主键生成策略
        * @Column:配置属性和字段的映射关系
        *      name：数据库表中字段的名称
        */
       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       @Column(name = "cust_id")
       private Long custId; //客户的主键
   
       @Column(name = "cust_name")
       private String custName;//客户名称
   
       @Column(name="cust_source")
       private String custSource;//客户来源
   
       @Column(name="cust_level")
       private String custLevel;//客户级别
   
       @Column(name="cust_industry")
       private String custIndustry;//客户所属行业
   
       @Column(name="cust_phone")
       private String custPhone;//客户的联系方式
   
       @Column(name="cust_address")
       private String custAddress;//客户地址
     }
   
   ```

#### 配置JPA的核心配置文件

在java工程的src路径下创建一个名为META-INF的文件夹，在此文件夹下创建一个名为persistence.xml的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://java.sun.com/xml/ns/persistence" version="2.0">
    <!--需要配置persistence-unit节点
        持久化单元：
            name:持久化单元名称
            transaction-type:事务管理的方式
                JTA:分布式事务管理
                RESOURCE_LOCAL:本地事务管理
    -->
    <persistence-unit name="myJpa" transaction-type="RESOURCE_LOCAL">
        <!--jpa的实现方式-->
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <!--可选配置：配置jpa实现方式的配置信息-->
        <properties>
            <!-- 数据库信息
                用户名，javax.persistence.jdbc.user
                密码，  javax.persistence.jdbc.password
                驱动，  javax.persistence.jdbc.driver
                数据库地址   javax.persistence.jdbc.url
            -->
            <property name="javax.persistence.jdbc.user" value="root"/>
            <property name="javax.persistence.jdbc.password" value="root"/>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/HeimaSpringData?userSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=Asia/Shanghai"/>

            <!--配置jpa实现方(hibernate)的配置信息
                显示sql           ：   false|true
                自动创建数据库表    ：  hibernate.hbm2ddl.auto
                        create      : 程序运行时创建数据库表（如果有表，先删除表再创建）
                        update      ：程序运行时创建表（如果有表，不会创建表）
                        none        ：不会创建表
            -->
            <property name="hibernate.show_sql" value="true" />
            <property name="hibernate.hbm2ddl.auto" value="update" />
        </properties>
    </persistence-unit>

</persistence>

```

#### 测试

```java
@Test
public void testSave(){
    // 1.加载配置文件创建工厂（实体管理器工厂）对象
    EntityManagerFactory factory = Persistence.createEntityManagerFactory("myJpa");
    // 2.通过实体管理器工厂获取实体管理器
    EntityManager em = factory.createEntityManager();
    // 3.获取事务对象，开启事务
    EntityTransaction tx = em.getTransaction();
    tx.begin();// 开启事务
    // 4.完成增删改查操作
    Customer customer = new Customer();
    customer.setCustName("传智播客");
    customer.setCustIndustry("教育");
    // 保存
    em.persist(customer);
    // 5.提交事务
    tx.commit();
    // 6.释放资源
    em.close();
    factory.close();
}

```

四、JPA主键生成策略
-----------

JPA提供的四种标准用法为TABLE,SEQUENCE,IDENTITY,AUTO。

*   **IDENTITY : 主键由数据库自动生成（主要是自动增长型）**

*   **SEQUENCE：根据底层数据库的序列来生成主键，条件是数据库支持序列。** 

*   **AUTO：主键由程序控制**

*   **TABLE：使用一个特定的数据库表格来保存主键**

五、JPA的API介绍
-----------

> JPA的操作步骤

1.  加载配置文件创建实体管理工厂
2.  根据实体管理工厂，创建实体管理器
3.  创建事务对象，开启事务
4.  增删改查操作
5.  提交事务
6.  释放资源

* * *

### Persistence对象

 Persistence对象主要作用是用于获取 _EntityManagerFactory_ 对象的 。通过调用该类的createEntityManagerFactory静态方法，根据配置文件中持久化单元名称创建EntityManagerFactory。

```java
//1. 创建 EntitymanagerFactory
@Test
String unitName = "myJpa";
EntityManagerFactory factory= Persistence.createEntityManagerFactory(unitName);

```

### EntityManagerFactory

EntityManagerFactory 接口主要用来创建 EntityManager 实例

```java
//创建实体管理类
EntityManager em = factory.createEntityManager();

```

> EntityManagerFactory对象内部维护了很多的内容

*   数据库信息
*   缓存信息
*   所有的实体管理器对象
*   在创建EntityManageFactoryr的过程中会根据配置创建数据库表

> 特点：EntityManagerFactory是一个线程安全的对像

 多个线程访问同一个EntityManagerFactory不会有线程安全问题。

 EntityManagerFactory的创建过程比较浪费资源，如何解决？

 === 》 静态代码块的形式创建EntityManagerFactory

### EntityManager

 在 JPA 规范中, EntityManager是完成持久化操作的核心对象。实体类作为普通 java对象，只有在调用 EntityManager将其持久化后才会变成持久化对象。EntityManager对象在一组实体类与底层数据源之间进行 O/R 映射的管理。它可以用来管理和更新 Entity Bean, 根椐主键查找 Entity Bean, 还可以通过JPQL语句查询实体。

> 方法说明

 getTransaction : 获取事务对象

 persist ： 保存操作

 merge ： 更新操作

 remove ： 删除操作

 find/getReference ： 根据id查询

### EntityTransaction

在 JPA 规范中, EntityTransaction是完成事务操作的核心对象

> 方法说明

begin：开启事务

commit：提交事务

rollback：回滚事务

六、抽取JPAUtil工具类
--------------

```java
  public final class JPAUtil {
    // JPA的实体管理器工厂：相当于Hibernate的SessionFactory
    private static EntityManagerFactory em;
    // 使用静态代码块赋值
    static {
      // 注意：该方法参数必须和persistence.xml中persistence-unit标签name属性取值一致
      em = Persistence.createEntityManagerFactory("myPersistUnit");
    }

    /**
     * 使用管理器工厂生产一个管理器对象
     * @return
     */
    public static EntityManager getEntityManager() {
      return em.createEntityManager();
    }
  }

```

七、使用JPA完成CURD
-------------

> 保存

```java
  @Test
  public void testSave2(){
    EntityManager em = JpaUtils.getEntityManager();
    EntityTransaction tx = em.getTransaction();
    tx.begin();

    Customer customer = new Customer();
    customer.setCustName("博学谷");
    em.persist(customer);

    tx.commit();
    em.close();
  }

```

> 修改

```java
  @Test
  // 更新
  public void testUpdate(){
    EntityManager em = JpaUtils.getEntityManager();
    EntityTransaction tx = em.getTransaction();
    tx.begin();

    Customer customer = em.getReference(Customer.class, 3L);
    customer.setCustIndustry("餐饮");
    em.merge(customer);

    tx.commit();
    em.close();
  }

```

> 删除

```java
  @Test
  // 删除
  public void testRemove(){
    EntityManager em = JpaUtils.getEntityManager();
    EntityTransaction tx = em.getTransaction();
    tx.begin();

    Customer customer = em.getReference(Customer.class, 2L);

    em.remove(customer);

    tx.commit();
    em.close();
  }

```

> 根据id查询

*   立即加载 find
*   延迟加载 getReference（优选）

```java
  @Test
  // 立即加载
  public void testFind(){
    EntityManager em = JpaUtils.getEntityManager();
    EntityTransaction tx = em.getTransaction();
    tx.begin();

    Customer customer = em.find(Customer.class, 1L);
    System.out.println(customer);

    tx.commit();
    em.close();
  }

```

```java
  @Test
  // 延迟加载
  public void testReference(){
    EntityManager em = JpaUtils.getEntityManager();
    EntityTransaction tx = em.getTransaction();
    tx.begin();

    Customer customer = em.getReference(Customer.class, 1L);
    System.out.println(customer);

    tx.commit();
    em.close();
  }

```

### JPA中的复杂查询（JPQL）

_JPQL全称Java Persistence Query Language_

 基于首次在EJB2.0中引入的EJB查询语言(EJB QL),Java持久化查询语言(JPQL)是一种\*\*\*可移植\*\*\*的查询语言，旨在以面向对象表达式语言的表达式，将SQL语法和简单查询语义绑定在一起·使用这种语言编写的查询是可移植的，可以被编译成所有主流数据库服务器上的SQL。

> 查询步骤

1.  创建query查询对象

2.  对参数进行赋值

3.  查询，并得到返回结果

> 查询全部

```java
  /**
       * 查询全部
       *      jqpl：from cn.itcast.domain.Customer
       *      sql：SELECT * FROM cst_customer
       */
  @Test
  public void testFindAll() {
    //1.获取entityManager对象
    EntityManager em = JpaUtils.getEntityManager();
    //2.开启事务
    EntityTransaction tx = em.getTransaction();
    tx.begin();
    //3.查询全部
    String jpql = "from Customer ";
    Query query = em.createQuery(jpql);//创建Query查询对象，query对象才是执行jqpl的对象

    //发送查询，并封装结果集
    List list = query.getResultList();

    for (Object obj : list) {
      System.out.print(obj);
    }

    //4.提交事务
    tx.commit();
    //5.释放资源
    em.close();
  }

```

> 排序查询

```java
/**
     * 排序查询： 倒序查询全部客户（根据id倒序）
     *      sql：SELECT * FROM cst_customer ORDER BY cust_id DESC
     *      jpql：from Customer order by custId desc
     *
     * 进行jpql查询
     *      1.创建query查询对象
     *      2.对参数进行赋值
     *      3.查询，并得到返回结果
     */
@Test
public void testOrders() {
  //1.获取entityManager对象
  EntityManager em = JpaUtils.getEntityManager();
  //2.开启事务
  EntityTransaction tx = em.getTransaction();
  tx.begin();
  //3.查询全部
  String jpql = "from Customer order by custId desc";
  Query query = em.createQuery(jpql);//创建Query查询对象，query对象才是执行jqpl的对象

  //发送查询，并封装结果集
  List list = query.getResultList();

  for (Object obj : list) {
    System.out.println(obj);
  }

  //4.提交事务
  tx.commit();
  //5.释放资源
  em.close();
}

```

> 统计总数

```java
	/**
     * 使用jpql查询，统计客户的总数
     *      sql：SELECT COUNT(cust_id) FROM cst_customer
     *      jpql：select count(custId) from Customer
     */

```

> 分页查询

```java
    /**
     * 分页查询
     *      sql：select * from cst_customer limit 0,2
     *      jqpl : from Customer
     */
    @Test
    public void testPaged() {
        //1.获取entityManager对象
        EntityManager em = JpaUtils.getEntityManager();
        //2.开启事务
        EntityTransaction tx = em.getTransaction();
        tx.begin();
        //3.查询全部
        //i.根据jpql语句创建Query查询对象
        String jpql = "from Customer";
        Query query = em.createQuery(jpql);
        //ii.对参数赋值 -- 分页参数
        //起始索引
        query.setFirstResult(0);
        //每页查询的条数
        query.setMaxResults(2);

        //iii.发送查询，并封装结果

        /**
         * getResultList ： 直接将查询结果封装为list集合
         * getSingleResult : 得到唯一的结果集
         */
        List list = query.getResultList();

        for(Object obj : list) {
            System.out.println(obj);
        }

        //4.提交事务
        tx.commit();
        //5.释放资源
        em.close();
    }

```

> 条件查询

```java
    /**
     * 条件查询
     *     案例：查询客户名称以‘传智播客’开头的客户
     *          sql：SELECT * FROM cst_customer WHERE cust_name LIKE  ?
     *          jpql : from Customer where custName like ?
     */

```

* * *

《— 第2天 —》
---------

一、Spring Data JPA的概述
--------------------

 Spring Data JPA 是 Spring 基于 ORM 框架、JPA 规范的基础上封装的一套JPA应用框架，可使开发者用极简的代码即可实现对数据库的访问和操作。它提供了包括增删改查等在内的常用功能，且易于扩展！学习并使用 Spring Data JPA 可以极大提高开发效率！

 Spring Data JPA 让我们解脱了DAO层的操作，基本上所有CRUD都可以依赖于它来实现,在实际的工作工程中，推荐使用Spring Data JPA + ORM（如：hibernate）完成操作，这样在切换不同的ORM框架时提供了极大的方便，同时也使数据库层操作更加简单，方便解耦。

> Spring Data JPA 与 JPA 和 hibernate之间的关系

 JPA是一套规范，内部是有接口和抽象类组成的。hibernate是一套成熟的ORM框架，而且Hibernate实现了JPA规范，所以也可以称hibernate为JPA的一种实现方式，我们使用JPA的API编程，意味着站在更高的角度上看待问题（面向接口编程）。

 Spring Data JPA是Spring提供的一套对JPA操作更加高级的封装，是在JPA规范下的专门用来进行数据持久化的解决方案。

二、快速入门
------

### 环境搭建

使用Spring Data JPA，需要整合Spring与Spring Data JPA，并且需要提供JPA的服务提供者hibernate，所以需要导入spring相关坐标，hibernate坐标，数据库驱动坐标等。

> 导入依赖

```xml
<properties>
    <spring.version>4.2.4.RELEASE</spring.version>
    <hibernate.version>5.0.7.Final</hibernate.version>
    <slf4j.version>1.7.30</slf4j.version>
    <log4j.version>2.12.1</log4j.version>
    <c3p0.version>0.9.1.2</c3p0.version>
    <mysql.version>8.0.16</mysql.version>
</properties>

<dependencies>
    <!-- junit单元测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

    <!-- spring beg -->
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.6.8</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aop</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-support</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <!-- spring end -->

    <!-- hibernate beg -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>${hibernate.version}</version>
    </dependency>
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-entitymanager</artifactId>
        <version>${hibernate.version}</version>
    </dependency>
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-validator</artifactId>
        <version>5.2.1.Final</version>
    </dependency>
    <!-- hibernate end -->

    <!-- c3p0 beg -->
    <dependency>
        <groupId>c3p0</groupId>
        <artifactId>c3p0</artifactId>
        <version>${c3p0.version}</version>
    </dependency>
    <!-- c3p0 end -->

    <!-- log end -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>${log4j.version}</version>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>${slf4j.version}</version>
    </dependency>
    <!-- log end -->


    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>${mysql.version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.data</groupId>
        <artifactId>spring-data-jpa</artifactId>
        <version>1.9.0.RELEASE</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <!-- el beg 使用spring data jpa 必须引入 -->
    <dependency>
        <groupId>javax.el</groupId>
        <artifactId>javax.el-api</artifactId>
        <version>2.2.4</version>
    </dependency>

    <dependency>
        <groupId>org.glassfish.web</groupId>
        <artifactId>javax.el</artifactId>
        <version>2.2.4</version>
    </dependency>
    <!-- el end -->

    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.12</version>
    </dependency>
</dependencies>

```

> 整合SpringData JPA 与 Spring

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:jpa="http://www.springframework.org/schema/data/jpa" xmlns:task="http://www.springframework.org/schema/task"
       xsi:schemaLocation="
      http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
      http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
      http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc.xsd
      http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd
      http://www.springframework.org/schema/data/jpa
      http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">

    <!--spring 和 spring data jpa 的配置-->

    <!--1.创建entityManagerFactory对象交给spring容器管理-->
    <bean id="entityManagerFactory" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="packagesToScan" value="cn.itcast.domain"/>
        <!--jpa的供应商适配器 -->
        <property name="jpaVendorAdapter">
            <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter">
                <!--配置是否自动创建数据库表 -->
                <property name="generateDdl" value="false" />
                <!--指定数据库类型 -->
                <property name="database" value="MYSQL" />
                <!--数据库方言：支持的特有语法 -->
                <property name="databasePlatform" value="org.hibernate.dialect.MySQLDialect" />
                <!--是否显示sql -->
                <property name="showSql" value="true" />
            </bean>
        </property>
    </bean>

    <!--2. 创建数据库连接池-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="user" value="root"/>
        <property name="password" value="root"/>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/HeimaSpringData?userSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=Asia/Shanghai"/>
        <property name="driverClass" value="com.mysql.cj.jdbc.Driver"/>
    </bean>

    <!--3.整合spring dataJpa-->
    <jpa:repositories base-package="cn.itcast.dao" transaction-manager-ref="transactionManager"
                      entity-manager-factory-ref="entityManagerFactory" />

    <!--4.配置事务管理器 -->
    <bean id="transactionManager" class="org.springframework.orm.jpa.JpaTransactionManager">
        <property name="entityManagerFactory" ref="entityManagerFactory"/>
    </bean>

    <!-- 4.txAdvice-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="save*" propagation="REQUIRED"/>
            <tx:method name="insert*" propagation="REQUIRED"/>
            <tx:method name="update*" propagation="REQUIRED"/>
            <tx:method name="delete*" propagation="REQUIRED"/>
            <tx:method name="get*" read-only="true"/>
            <tx:method name="find*" read-only="true"/>
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <!-- 5.aop-->
    <aop:config>
        <aop:pointcut id="pointcut" expression="execution(* cn.itcast.service.*.*(..))" />
        <aop:advisor advice-ref="txAdvice" pointcut-ref="pointcut" />
    </aop:config>


    <!--5.声明式事务 -->

    <!-- 6. 配置包扫描，使用注解开发 -->
    <context:component-scan base-package="cn.itcast" />

</beans>

```

> 编写实体类，使用jpa注解配置映射关系

```java
/*
* 1.实体类和表的映射关系
*   @Entity
*   @Table
* 2.类中属性和表中字段的映射关系
*   @Id
*   @GeneratedValue
*   @Column
*
* */

```

### 编写一个符合springDataJpa的dao层接口

* * *

*   只需要编写dao层接口，不需要编写dao层接口的实现类

*   dao层接口规范

    1.  需要继承两个接口（JpaRepository, JpaSpecificationExecutor）
    2.  需要提供相应的泛型

```java
/**
 * 符合SpringDataJpa的dao层接口规范
 *      JpaRepository < 操作的实体类类型，实体类中主键属性的类型>
 *          * 封装了基本CRUD操作
 *      JpaSpecificationExecutor< 操作的实体类类型 >
 *          * 封装了复杂查询（分页）
 */
public interface CustomerDao extends JpaRepository<Customer,Long> , JpaSpecificationExecutor<Customer> {

}

```

### 测试

```java
@RunWith(SpringJUnit4ClassRunner.class) //声明spring提供的单元测试环境
@ContextConfiguration(locations = "classpath:applicationContext.xml")//指定spring容器的配置信息

public class CustomerDaoTest {
    @Autowired
    private CustomerDao customerDao;

    /**
     * 根据id查询
     */
    @Test
    public void testFindOne() {
        Customer customer = customerDao.findOne(4l);
        System.out.println(customer);
    }

    /**
     * save : 保存或者更新
     *      根据传递的对象是否存在主键id，
     *      如果没有id主键属性：保存
     *      存在id主键属性，根据id查询数据，更新数据
     */
    @Test
    public void testSave() {
        Customer customer  = new Customer();
        customer.setCustName("黑马程序员");
        customer.setCustLevel("vip");
        customer.setCustIndustry("it教育");
        customerDao.save(customer);
    }

    @Test
    public void testUpdate() {
        Customer customer  = new Customer();
        customer.setCustId(4l);
        customer.setCustName("黑马程序员很厉害");
        customerDao.save(customer);
    }

    @Test
    public void testDelete () {
        customerDao.delete(3l);
    }


    /**
     * 查询所有
     */
    @Test
    public void testFindAll() {
        List<Customer> list = customerDao.findAll();
        for(Customer customer : list) {
            System.out.println(customer);
        }
    }

    /**
     * 测试统计查询：查询客户的总数量
     *      count:统计总条数
     */
    @Test
    public void testCount() {
        long count = customerDao.count();//查询全部的客户数量
        System.out.println(count);
    }

    /**
     * 测试：判断id为4的客户是否存在
     *      1. 可以查询以下id为4的客户
     *          如果值为空，代表不存在，如果不为空，代表存在
     *      2. 判断数据库中id为4的客户的数量
     *          如果数量为0，代表不存在，如果大于0，代表存在
     */
    @Test
    public void  testExists() {
        boolean exists = customerDao.exists(4l);
        System.out.println("id为4的客户 是否存在："+exists);
    }


    /**
     * 根据id从数据库查询
     *      @Transactional : 保证getOne正常运行
     *
     *  findOne：
     *      em.find()           :立即加载
     *  getOne：
     *      em.getReference     :延迟加载
     *      * 返回的是一个客户的动态代理对象
     *      * 什么时候用，什么时候查询
     */
    @Test
    @Transactional
    public void  testGetOne() {
        Customer customer = customerDao.getOne(4l);
        System.out.println(customer);
    }
}

```

三、SpringData JPA源码分析
--------------------

1.  客户接口开始

2.  SpringData JPA创建动态代理对象 simpleJpaRepository

3.  …

![](https://img-blog.csdnimg.cn/20200824142713407.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

> SpringData Jpa的运行过程和原理剖析

1.  通过JdkDynamicAopProxy的invoke方法创建了一个动态代理对象（SimpleJpaRepository）
2.  SimpleJpaRepository当中封装了JPA的操作（借助JPA的api完成数据库的CURD）
3.  通过hibernate完成数据库操作（封装了jdbc）

四、Spring Data JPA的查询方式
----------------------

### 接口查询

* 继承JpaRepository的方法列表

  ![](https://img-blog.csdnimg.cn/20200824142739305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

* 继承JpaSpecificationExecutor方法列表

  ![](https://img-blog.csdnimg.cn/2020082414275826.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0RERERlbmdf,size_16,color_FFFFFF,t_70#pic_center)

### JPQL查询

jpql：jpa query language (jpa查询语言)

特点:

*   语法或关键字和sql语句类似

*   查询的是类和类中的属性

**需要将JPQL语句配置到接口方法上**

1.  特有的查询：需要在dao接口上配置的方法
2.  在新添加的方法上，使用注解的形式配置jpql查询语句
3.  注解：@Query

> 查询

```java
public interface CustomerDao extends JpaRepository<Customer, Long>,JpaSpecificationExecutor<Customer> {    
    //@Query 使用jpql的方式查询。
    @Query(value="from Customer")
    public List<Customer> findAllCustomer();
    
    //@Query 使用jpql的方式查询。?1代表参数的占位符，其中1对应方法中的参数索引
    @Query(value="from Customer where custName = ?1")
    public Customer findCustomer(String custName);
}

```

> 更新

此外，也可以通过使用 @Query 来执行一个更新操作，为此，我们需要在使用 @Query 的同时，用 @Modifying 来将该操作标识为修改查询，这样框架最终会生成一个更新的操作，而非查询。

```java
    @Query(value="update Customer set custName = ?1 where custId = ?2")
    @Modifying
    public void updateCustomer(String custName,Long custId);

```

**测试方法需要增加事务支持：** 

```java
    /*
    * springDataJpa中使用jpql完成 更新/删除操作
    *   需要手动添加事务的支持
    *   默认会执行结束之后，回滚事务
    * */
    @Test
    @Transactional
    @Rollback(false)
    public void testUpdate(){
        customerDao.updateCustNameById(5L,"尚硅谷");
    }

```

### SQL语句查询

1. 特有的查询：需要在dao接口上配置方法

2. 在新添加的方法上，使用注解的形式配置sql查询语句

3. 注解 ：@Query

    value : jpql语句 | sql语句

    nativeQuery : false（使用jpql查询） | true（使用本地查询 ：sql查询）

```java
    /**
     * 使用sql的形式查询：
     *     查询全部的客户
     *  sql ： select * from cst_customer;
     *  Query : 配置sql查询
     *      value ： sql语句
     *      nativeQuery ： 查询方式
     *          true ： sql查询
     *          false：jpql查询
     *
     */
    //@Query(value = " select * from cst_customer" ,nativeQuery = true)
    @Query(value="select * from cst_customer where cust_name like ?1",nativeQuery = true)
    public List<Object [] > findSql(String name);

```

### 方法命名规则查询

*   是对jpql查询，更加深入的一层封装
*   我们只需要按照SpringDataJpa提供的方法名称规则来定义方法，不需要再去配置jpql语句，就能完成查询

> 规则

*   findBy开头： 代表查询，对象中属性的名称（首字母大写）
*   含义：根据属性名称进行查询

#### 精准匹配

> 测试

```java
    /**
     * 方法名的约定：
     *      findBy : 查询
     *            对象中的属性名（首字母大写） ： 查询的条件
     *            CustName
     *            * 默认情况 ： 使用 等于的方式查询
     *                  特殊的查询方式
     *
     *  findByCustName   --   根据客户名称查询
     *
     *  再springdataJpa的运行阶段
     *          会根据方法名称进行解析  findBy    from  xxx(实体类)
     *                                      属性名称      where  custName =
     *
     *      1.findBy  + 属性名称 （根据属性名称进行完成匹配的查询=）
     *      2.findBy  + 属性名称 + “查询方式（Like | isnull）”
     *          findByCustNameLike
     *      3.多条件查询
     *          findBy + 属性名 + “查询方式”   + “多条件的连接符（and|or）”  + 属性名 + “查询方式”
     */
    public Customer findByCustName(String custName);

```

```java
  //测试方法命名规则的查询
  @Test
  public void testNaming(){
    Customer customer = customerDao.findByCustName("博学谷");
    System.out.println(customer);
  }

```

#### 模糊查询

findBy + 属性名称 + “查询方式（Like | isnull）”

> 测试

```java
public List<Customer> findByCustNameLike(String custName);

```

#### 多条件查询

findBy + 属性名 + “查询方式” + “多条件的连接符

> 测试

```java
//使用客户名称模糊匹配和客户所属行业精准匹配的查询
public Customer findByCustNameLikeAndCustIndustry(String custName,String custIndustry);

```

《— 第3天 —》
---------

一、Specification动态查询
-------------------

 有时我们在查询某个实体的时候，给定的条件是不固定的，这时就需要动态构建相应的查询语句，在Spring Data JPA中可以通过JpaSpecificationExecutor接口查询。相比JPQL,其优势是类型安全,更加的面向对象。

> JpaSpecificationExecutor方法列表

1. T findOne(Specification spec); //查询单个对象

2. List findAll(Specification spec); //查询列表

3. 查询全部，分页

   pageable：分页参数

   返回值：分页pageBean（page：是springdatajpa提供的）

   Page findAll(Specification spec, Pageable pageable);

4. 查询列表

   Sort：排序参数

   List findAll(Specification spec, Sort sort);

5. long count(Specification spec);//统计查询

> Specification：查询条件

自定义我们自己的Specification实现类

实现

```java
//root：查询的根对象（查询的任何属性都可以从根对象中获取）
//CriteriaQuery：顶层查询对象，自定义查询方式（了解：一般不用）
//CriteriaBuilder：查询的构造器，封装了很多的查询条件
Predicate toPredicate(Root<T> root, CriteriaQuery<?> query, CriteriaBuilder cb); //封装查询条件

```

### 单个条件查询

```java
    /**
     * 根据条件，查询单个对象
     *
     */
    @Test
    public void testSpec() {
        //匿名内部类
        /**
         * 自定义查询条件
         *      1.实现Specification接口（提供泛型：查询的对象类型）
         *      2.实现toPredicate方法（构造查询条件）
         *      3.需要借助方法参数中的两个参数（
         *          root：获取需要查询的对象属性
         *          CriteriaBuilder：构造查询条件的，内部封装了很多的查询条件（模糊匹配，精准匹配）
         *       ）
         *  案例：根据客户名称查询，查询客户名为传智播客的客户
         *          查询条件
         *              1.查询方式
         *                  cb对象
         *              2.比较的属性名称
         *                  root对象
         *
         */
        Specification<Customer> spec = new Specification<Customer>() {
            @Override
            public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
                //1.获取比较的属性
                Path<Object> custName = root.get("custId");
                //2.构造查询条件  ：    select * from cst_customer where cust_name = '传智播客'
                /**
                 * 第一个参数：需要比较的属性（path对象）
                 * 第二个参数：当前需要比较的取值
                 */
                Predicate predicate = cb.equal(custName, "传智播客");//进行精准的匹配  （比较的属性，比较的属性的取值）
                return predicate;
            }
        };
        Customer customer = customerDao.findOne(spec);
        System.out.println(customer);
    }

```

### 多条件查询

```java
    /**
     * 多条件查询
     *      案例：根据客户名（传智播客）和客户所属行业查询（it教育）
     *
     */
    @Test
    public void testSpec1() {
        /**
         *  root:获取属性
         *      客户名
         *      所属行业
         *  cb：构造查询
         *      1.构造客户名的精准匹配查询
         *      2.构造所属行业的精准匹配查询
         *      3.将以上两个查询联系起来
         */
        Specification<Customer> spec = new Specification<Customer>() {
            @Override
            public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
                Path<Object> custName = root.get("custName");//客户名
                Path<Object> custIndustry = root.get("custIndustry");//所属行业

                //构造查询
                //1.构造客户名的精准匹配查询
                Predicate p1 = cb.equal(custName, "传智播客");//第一个参数，path（属性），第二个参数，属性的取值
                //2..构造所属行业的精准匹配查询
                Predicate p2 = cb.equal(custIndustry, "it教育");
                //3.将多个查询条件组合到一起：组合（满足条件一并且满足条件二：与关系，满足条件一或满足条件二即可：或关系）
                Predicate and = cb.and(p1, p2);//以与的形式拼接多个查询条件
                // cb.or();//以或的形式拼接多个查询条件
                return and;
            }
        };
        Customer customer = customerDao.findOne(spec);
        System.out.println(customer);
    }

```

### 模糊查询

```java
/**
     * 案例：完成根据客户名称的模糊匹配，返回客户列表
     *      客户名称以 ’传智播客‘ 开头
     *
     * equal ：直接的到path对象（属性），然后进行比较即可
     * gt，lt,ge,le,like : 得到path对象，根据path指定比较的参数类型，再去进行比较
     *      指定参数类型：path.as(类型的字节码对象)
     */
    @Test
    public void testSpec3() {
        //构造查询条件
        Specification<Customer> spec = new Specification<Customer>() {
            @Override
            public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
                //查询属性：客户名
                Path<Object> custName = root.get("custName");
                //查询方式：模糊匹配
                Predicate like = cb.like(custName.as(String.class), "传智播客%");
                return like;
            }
        };
//        List<Customer> list = customerDao.findAll(spec);
//        for (Customer customer : list) {
//            System.out.println(customer);
//        }
        //添加排序
        //创建排序对象,需要调用构造方法实例化sort对象
        //第一个参数：排序的顺序（倒序，正序）
        //   Sort.Direction.DESC:倒序
        //   Sort.Direction.ASC ： 升序
        //第二个参数：排序的属性名称
        Sort sort = new Sort(Sort.Direction.DESC,"custId");
        List<Customer> list = customerDao.findAll(spec, sort);
        for (Customer customer : list) {
            System.out.println(customer);
        }
    }


```

### 分页查询

```java
 /**
     * 分页查询
     *      Specification: 查询条件
     *      Pageable：分页参数
     *          分页参数：查询的页码，每页查询的条数
     *          findAll(Specification,Pageable)：带有条件的分页
     *          findAll(Pageable)：没有条件的分页
     *  返回：Page（springDataJpa为我们封装好的pageBean对象，数据列表，共条数）
     */
    @Test
    public void testSpec4() {

        Specification spec = null;
        //PageRequest对象是Pageable接口的实现类
        /**
         * 创建PageRequest的过程中，需要调用他的构造方法传入两个参数
         *      第一个参数：当前查询的页数（从0开始）
         *      第二个参数：每页查询的数量
         */
        Pageable pageable = new PageRequest(0,2);
        //分页查询
        Page<Customer> page = customerDao.findAll(null, pageable);
        System.out.println(page.getContent()); //得到数据集合列表
        System.out.println(page.getTotalElements());//得到总条数
        System.out.println(page.getTotalPages());//得到总页数
    }

```

二、多表之间的关系和操作
------------

**表关系**

* 一对一

* 一对多：

   一的一方：主表

   多的一放：从表

   外键：需要在从表上新建一列作为外键，他的取值来源于主表的主键

* 多对多

   中间表：中间表中最少应该由两个字段组成，这两个字段作为外键指向两张表的主键，又组成了联合主键。



**实体类中的关系**

*   包含关系：可以通过实体类中的包含关系描述表关系
*   继承关系

**分析步骤**

1.  明确表关系
2.  确定表关系（描述 外键 | 中间表）
3.  编写实体类，在实体类中描述表关系（包含关系）
4.  配置映射关系

三、多表操作
------

### 一对多操作

```
	案例：客户和联系人的案例（一对多关系）
		客户：一家公司
		联系人：这家公司的员工
	
		一个客户可以具有多个联系人
		一个联系人从属于一家公司
		
	分析步骤
		1.明确表关系
			一对多关系
		2.确定表关系（描述 外键|中间表）
			主表：客户表
			从表：联系人表
				* 再从表上添加外键
		3.编写实体类，再实体类中描述表关系（包含关系）
			客户：再客户的实体类中包含一个联系人的集合
			联系人：在联系人的实体类中包含一个客户的对象
		4.配置映射关系
			* 使用jpa注解配置一对多映射关系

```

> 实体类

**Customer.java**

```java
/*
* 1.实体类和表的映射关系
*   @Entity
*   @Table
* 2.类中属性和表中字段的映射关系
*   @Id
*   @GeneratedValue
*   @Column
*
* */
@Data
@AllArgsConstructor
@NoArgsConstructor

@Entity
@Table(name = "cst_customer")
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="cust_id")
    private Long custId;
    @Column(name="cust_address")
    private String custAddress;
    @Column(name="cust_industry")
    private String custIndustry;
    @Column(name="cust_level")
    private String custLevel;
    @Column(name="cust_name")
    private String custName;
    @Column(name="cust_phone")
    private String custPhone;
    @Column(name="cust_source")
    private String custSource;

    //配置客户和联系人之间的关系（一对多关系）
    /**
     * 使用注解的形式配置多表关系
     *      1.声明关系
     *          @OneToMany : 配置一对多关系
     *              targetEntity ：对方对象的字节码对象
     *      2.配置外键（中间表）
     *              @JoinColumn : 配置外键
     *                  name：外键字段名称
     *                  referencedColumnName：参照的主表的主键字段名称
     *
     *  * 在客户实体类上（一的一方）添加了外键了配置，所以对于客户而言，也具备了维护外键的作用
     *
     */

//    @OneToMany(targetEntity = LinkMan.class)
//    @JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")
    /**
     * 放弃外键维护权
     *      mappedBy：对方配置关系的属性名称\
     * cascade : 配置级联（可以配置到设置多表的映射关系的注解上）
     *      CascadeType.all         : 所有
     *                  MERGE       ：更新
     *                  PERSIST     ：保存
     *                  REMOVE      ：删除
     *
     * fetch : 配置关联对象的加载方式
     *          EAGER   ：立即加载
     *          LAZY    ：延迟加载

      */
    @OneToMany(mappedBy = "customer",cascade = CascadeType.ALL)
    private Set<LinkMan> linkMans = new HashSet<>();
}

```

**Linkman.java**

```java
@Data
@NoArgsConstructor
@AllArgsConstructor

@Entity
@Table(name = "cst_linkman")
public class LinkMan {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "lkm_id")
    private Long lkmId; //联系人编号(主键)
    @Column(name = "lkm_name")
    private String lkmName;//联系人姓名
    @Column(name = "lkm_gender")
    private String lkmGender;//联系人性别
    @Column(name = "lkm_phone")
    private String lkmPhone;//联系人办公电话
    @Column(name = "lkm_mobile")
    private String lkmMobile;//联系人手机
    @Column(name = "lkm_email")
    private String lkmEmail;//联系人邮箱
    @Column(name = "lkm_position")
    private String lkmPosition;//联系人职位
    @Column(name = "lkm_memo")
    private String lkmMemo;//联系人备注

    /**
     * 配置联系人到客户的多对一关系
     *     使用注解的形式配置多对一关系
     *      1.配置表关系
     *          @ManyToOne : 配置多对一关系
     *              targetEntity：对方的实体类字节码
     *      2.配置外键（中间表）
     *
     * * 配置外键的过程，配置到了多的一方，就会在多的一方维护外键
     *
     */
    @ManyToOne(targetEntity = Customer.class,fetch = FetchType.LAZY)
    @JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")
    private Customer customer;
}

```

#### 测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath:applicationContext.xml")
public class OneToManyTest {

    @Autowired
    private CustomerDao customerDao;

    @Autowired
    private LinkManDao linkManDao;

    /**
     * 保存一个客户，保存一个联系人
     *  效果：客户和联系人作为独立的数据保存到数据库中
     *      联系人的外键为空
     *  原因？
     *      实体类中没有配置关系
     */
    @Test
    @Transactional //配置事务
    @Rollback(false) //不自动回滚
    public void testAdd() {
        //创建一个客户，创建一个联系人
        Customer customer = new Customer();
        customer.setCustName("百度");

        LinkMan linkMan = new LinkMan();
        linkMan.setLkmName("小李");

        /**
         * 配置了客户到联系人的关系
         *      从客户的角度上：发送两条insert语句，发送一条更新语句更新数据库（更新外键）
         * 由于我们配置了客户到联系人的关系：客户可以对外键进行维护
         */
        customer.getLinkMans().add(linkMan);


        customerDao.save(customer);
        linkManDao.save(linkMan);
    }


    @Test
    @Transactional //配置事务
    @Rollback(false) //不自动回滚
    public void testAdd1() {
        //创建一个客户，创建一个联系人
        Customer customer = new Customer();
        customer.setCustName("百度");

        LinkMan linkMan = new LinkMan();
        linkMan.setLkmName("小李");

        /**
         * 配置联系人到客户的关系（多对一）
         *    只发送了两条insert语句
         * 由于配置了联系人到客户的映射关系（多对一）
         *
         *
         */
        linkMan.setCustomer(customer);

        customerDao.save(customer);
        linkManDao.save(linkMan);
    }

    /**
     * 会有一条多余的update语句
     *      * 由于一的一方可以维护外键：会发送update语句
     *      * 解决此问题：只需要在一的一方放弃维护权即可
     *
     */
    @Test
    @Transactional //配置事务
    @Rollback(false) //不自动回滚
    public void testAdd2() {
        //创建一个客户，创建一个联系人
        Customer customer = new Customer();
        customer.setCustName("百度");

        LinkMan linkMan = new LinkMan();
        linkMan.setLkmName("小李");


        linkMan.setCustomer(customer);//由于配置了多的一方到一的一方的关联关系（当保存的时候，就已经对外键赋值）
        customer.getLinkMans().add(linkMan);//由于配置了一的一方到多的一方的关联关系（发送一条update语句）

        customerDao.save(customer);
        linkManDao.save(linkMan);
    }

    /**
     * 级联添加：保存一个客户的同时，保存客户的所有联系人
     *      需要在操作主体的实体类上，配置casacde属性
     */
    @Test
    @Transactional //配置事务
    @Rollback(false) //不自动回滚
    public void testCascadeAdd() {
        Customer customer = new Customer();
        customer.setCustName("百度1");

        LinkMan linkMan = new LinkMan();
        linkMan.setLkmName("小李1");

        linkMan.setCustomer(customer);
        customer.getLinkMans().add(linkMan);

        customerDao.save(customer);
    }


    /**
     * 级联删除：
     *      删除1号客户的同时，删除1号客户的所有联系人
     */
    @Test
    @Transactional //配置事务
    @Rollback(false) //不自动回滚
    public void testCascadeRemove() {
        //1.查询1号客户
        Customer customer = customerDao.findOne(1l);
        //2.删除1号客户
        customerDao.delete(customer);
    }
}

```

#### 级联

 操作一个对象的同时操作他的关联对象

 级联操作：

  1. 需要区分操作主体

  2. 需要在操作主体的实体类上，添加级联属性（需要添加到多表映射关系的注解上）

  3. cascade级联

 级联添加

 案例：当我保存一个客户的同时保存联系人

 级联删除

 案例：但我删除一个客户的同时删除此客户所有的联系人

* * *

### 多对多操作

案例：用户和角色

```
	分析步骤
		1.明确表关系
			多对多关系
		2.确定表关系（描述 外键|中间表）
			中间间表
		3.编写实体类，再实体类中描述表关系（包含关系）
			用户：包含角色的集合
			角色：包含用户的集合
		4.配置映射关系

```

> 实体类

**User.java**

```java
@Entity
@Table(name = "sys_user")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="user_id")
    private Long userId;
    @Column(name="user_name")
    private String userName;
    @Column(name="age")
    private Integer age;

    /**
     * 配置用户到角色的多对多关系
     *      配置多对多的映射关系
     *          1.声明表关系的配置
     *              @ManyToMany(targetEntity = Role.class)  //多对多
     *                  targetEntity：代表对方的实体类字节码
     *          2.配置中间表（包含两个外键）
     *                @JoinTable
     *                  name : 中间表的名称
     *                  joinColumns：配置当前对象在中间表的外键
     *                      @JoinColumn的数组
     *                          name：外键名
     *                          referencedColumnName：参照的主表的主键名
     *                  inverseJoinColumns：配置对方对象在中间表的外键
     */
    @ManyToMany(targetEntity = Role.class,cascade = CascadeType.ALL)
    @JoinTable(name = "sys_user_role",
            //joinColumns,当前对象在中间表中的外键
            joinColumns = {@JoinColumn(name = "sys_user_id",referencedColumnName = "user_id")},
            //inverseJoinColumns，对方对象在中间表的外键
            inverseJoinColumns = {@JoinColumn(name = "sys_role_id",referencedColumnName = "role_id")}
    )
    private Set<Role> roles = new HashSet<>();

    public Long getUserId() {
        return userId;
    }

    public void setUserId(Long userId) {
        this.userId = userId;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public Set<Role> getRoles() {
        return roles;
    }

    public void setRoles(Set<Role> roles) {
        this.roles = roles;
    }
}

```

**Role.java**

```java
@Entity
@Table(name = "sys_role")
public class Role {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "role_id")
    private Long roleId;
    @Column(name = "role_name")
    private String roleName;

    //配置多对多
    @ManyToMany(mappedBy = "roles")  //配置多表关系(对方配置映射关系的属性)
    private Set<User> users = new HashSet<>();

    public Long getRoleId() {
        return roleId;
    }

    public void setRoleId(Long roleId) {
        this.roleId = roleId;
    }

    public String getRoleName() {
        return roleName;
    }

    public void setRoleName(String roleName) {
        this.roleName = roleName;
    }

    public Set<User> getUsers() {
        return users;
    }

    public void setUsers(Set<User> users) {
        this.users = users;
    }
}

```

> 测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath:applicationContext.xml")
public class ManyToManyTest {

    @Autowired
    private UserDao userDao;
    @Autowired
    private RoleDao roleDao;

    /*
    * 保存一个用户，保存一个角色
    *
    * 多对多放弃维护权，被动的一方放弃
    * */
    @Test
    @Transactional
    @Rollback(false)
    public void testAdd(){
        User user = new User();
        user.setUserName("小刘");

        Role role = new Role();
        role.setRoleName("程序员");

        //配置用户到角色关系，可以对中间表中的数据进行维护
        user.getRoles().add(role);

        userDao.save(user);
        roleDao.save(role);
    }
}

```

### 多表的查询

1. 对象导航查询

   查询一个对象的同时，通过此对象查询他的关联对象

   案例：一个客户对应多个联系人

   *   从一方查询多方

    默认：使用延迟加载

   * 从多方查询一方

      默认：使用立即加载

> 实体类

**Customer.java**

```java
/**
 * 1.实体类和表的映射关系
 *      @Eitity
 *      @Table
 * 2.类中属性和表中字段的映射关系
 *      @Id
 *      @GeneratedValue
 *      @Column
 */
@Entity
@Table(name="cst_customer")
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="cust_id")
    private Long custId;
    @Column(name="cust_address")
    private String custAddress;
    @Column(name="cust_industry")
    private String custIndustry;
    @Column(name="cust_level")
    private String custLevel;
    @Column(name="cust_name")
    private String custName;
    @Column(name="cust_phone")
    private String custPhone;
    @Column(name="cust_source")
    private String custSource;

    //配置客户和联系人之间的关系（一对多关系）
    /**
     * 使用注解的形式配置多表关系
     *      1.声明关系
     *          @OneToMany : 配置一对多关系
     *              targetEntity ：对方对象的字节码对象
     *      2.配置外键（中间表）
     *              @JoinColumn : 配置外键
     *                  name：外键字段名称
     *                  referencedColumnName：参照的主表的主键字段名称
     *
     *  * 在客户实体类上（一的一方）添加了外键了配置，所以对于客户而言，也具备了维护外键的作用
     *
     */

//    @OneToMany(targetEntity = LinkMan.class)
//    @JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")
    /**
     * 放弃外键维护权
     *      mappedBy：对方配置关系的属性名称\
     * cascade : 配置级联（可以配置到设置多表的映射关系的注解上）
     *      CascadeType.all         : 所有
     *                  MERGE       ：更新
     *                  PERSIST     ：保存
     *                  REMOVE      ：删除
     *
     * fetch : 配置关联对象的加载方式
     *          EAGER   ：立即加载
     *          LAZY    ：延迟加载

      */
    @OneToMany(mappedBy = "customer",cascade = CascadeType.ALL)
    private Set<LinkMan> linkMans = new HashSet<>();

```

**LinkMan.java**

```java
@Entity
@Table(name = "cst_linkman")
public class LinkMan {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "lkm_id")
    private Long lkmId; //联系人编号(主键)
    @Column(name = "lkm_name")
    private String lkmName;//联系人姓名
    @Column(name = "lkm_gender")
    private String lkmGender;//联系人性别
    @Column(name = "lkm_phone")
    private String lkmPhone;//联系人办公电话
    @Column(name = "lkm_mobile")
    private String lkmMobile;//联系人手机
    @Column(name = "lkm_email")
    private String lkmEmail;//联系人邮箱
    @Column(name = "lkm_position")
    private String lkmPosition;//联系人职位
    @Column(name = "lkm_memo")
    private String lkmMemo;//联系人备注

    /**
     * 配置联系人到客户的多对一关系
     *     使用注解的形式配置多对一关系
     *      1.配置表关系
     *          @ManyToOne : 配置多对一关系
     *              targetEntity：对方的实体类字节码
     *      2.配置外键（中间表）
     *
     * * 配置外键的过程，配置到了多的一方，就会在多的一方维护外键
     *
     */
    @ManyToOne(targetEntity = Customer.class,fetch = FetchType.LAZY)
    @JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")

```

> 测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath:applicationContext.xml")
public class ObjectQueryTest {
    @Autowired
    private CustomerDao customerDao;

    @Autowired
    private LinkManDao linkManDao;

    //could not initialize proxy - no Session
    //测试对象导航查询（查询一个对象的时候，通过此对象查询所有的关联对象）
    @Test
    @Transactional // 解决在java代码中的no session问题
    public void  testQuery1() {
        //查询id为1的客户
        Customer customer = customerDao.getOne(1l);
        //对象导航查询，此客户下的所有联系人
        Set<LinkMan> linkMans = customer.getLinkMans();

        for (LinkMan linkMan : linkMans) {
            System.out.println(linkMan);
        }
    }

    /**
     * 对象导航查询：
     *      默认使用的是延迟加载的形式查询的
     *          调用get方法并不会立即发送查询，而是在使用关联对象的时候才会差和讯
     *      延迟加载！
     * 修改配置，将延迟加载改为立即加载
     *      fetch，需要配置到多表映射关系的注解上
     *
     */

    @Test
    @Transactional // 解决在java代码中的no session问题
    public void  testQuery2() {
        //查询id为1的客户
        Customer customer = customerDao.findOne(1l);
        //对象导航查询，此客户下的所有联系人
        Set<LinkMan> linkMans = customer.getLinkMans();

        System.out.println(linkMans.size());
    }

    /**
     * 从联系人对象导航查询他的所属客户
     *      * 默认 ： 立即加载
     *  延迟加载：
     *
     */
    @Test
    @Transactional // 解决在java代码中的no session问题
    public void  testQuery3() {
        LinkMan linkMan = linkManDao.findOne(2l);
        //对象导航查询所属的客户
        Customer customer = linkMan.getCustomer();
        System.out.println(customer);
    }

}

```