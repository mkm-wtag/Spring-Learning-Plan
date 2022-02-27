# Spring and MVC Topics to learn

## Index
* [1. Core](#core)
  * [Architecture of Spring Framework](#architecture-of-spring-framework)
  * [Understand about the necessary environment setup to work with Spring](#understand-about-the-necessary-environment-setup-to-work-with-spring)
  * [Maven Dependency Management](#maven-dependency-management)
  * [Dependency injection and IOC](#dependency-injection-and-ioc)
    * [Constructor or Setter](#constructor-or-setter)
    * [Autowire](#autowire)
  * [Spring annotations](#spring-annotations)
  * [Bean life cycle](#bean-life-cycle)
  * [Bean scopes](#bean-scopes)
  * [Events](#events)
  * [AOP with Spring Framework](#aop-with-spring-framework)
  * [JDBC Framework](#jdbc-framework)
  * [Resources](#resources)
  * [Transaction Managements](#transaction-managements)
  * [i18n](#i18n)
  * [Data Binding](#data-binding)
  * [Logging Log4j](#logging-log4j)



## Core

## Architecture of Spring Framework



## Understand about the necessary environment setup to work with Spring


## Maven Dependency Management


## Dependency injection and IOC

Suppose we have two objects related to each other. On eis dependant on the other. The idea is to decouple dependency so they are not tie to each other.

Let's say that class A is dependent on an object from class B. We remove that dependency from class A and inject that dependency from another class.

This is called dependency injection.

Dependency injection is just a way to achieve IoC.

IoC, Inversion of control : Reversing the control of the flow of an application. It is transferred to an external framework or container.

In traditional programming our custom code makes to a library. ToC enable a framework to take control of the flow of theprogram and makes calls to our custom code. Frameworks uses additional behaviour with abstraction buid in. If we want to add out own behaviour, we need to extend the class of the framework or plugin.

Spring IoC container gets initialized when the application starts and when a bean is requested, the dependencies are injected automatically.

ANy object we initialize through spring container is called spring bean. Any POJO class can be a spring bean if it is configured to be initialized via container by providing configuration metadata.


**IOC Advantages:**

1. Decoupling the execution of a task from its implementation
2. Easier to switch between different implementations
3. Easy to test a program by isoating a component
 
## Constructor or Setter
**CI vs SI**

1. Partial dependency is possible only i SI
2. SI overrides the CI
3. We can easily change the value by SI without create instance.



## Autowire
Suppose we need to inject dependency of b into A. This can be done manually and automatically. The automatic process is called autowiring.

It can be done through XML and Annotation.

**Advantage**

Automatic
Less Code

**Disadvantage**
No cntrol of programmer.
Can not be used for primitive and string values

**Opinion**

If the number of beans are less - Autowiring
Else Explicitly/manually (CI/SI)



## Spring annotations 


## Bean life cycle
A Spring bean need to be instantiated when the container starts. Some pre and post initialization steps to get the bean into a usuable state. When the bean is no longer needed, it will be removed from IoC container. Some pre and post destruction steps to free the other system resource.
Spring Bean Factory controls the creation and destruction of beans. To execute custom code, the bean factory provides the callback methods, which can be categorized broadly into two groups. Post Initialization and Post destruction.

Spring framework provides the following four way for controlling life cycle events of a bean.
1. InitializingBean and DisposableBean callback Interfaces
2. Aware interfaces for specific behaviour
3. Custom init() and destroy() methods in bean configuration file.
4. @PostConstruct and @PostDestroy Anootations

Implemented Methods called before custom methods.
Suppose we have multiple beans. By default the init methods runs sequentially/FIFO for each bean and destroyer methods are called in slack/LIFO.

BeanPostProcessor : It is an interface which we can implement and override methods. It has 2 methods.
1. postProcessBeforeInitialization()
2. postProcessAfterInitialization()

BeanFactoryPostProcessor : It is an interface which we can implement and override only one method.
* PropertyPlace : Load Properties of properties file into XML placeholder

There are 3 ways to configure beans.
1. XML Based Configuration : By creating spring configuration XML file.
2. Annotation Based Configuration : By using @Component annotation. Scope details can be provided with @Scope annotation.
3. Java Based Configuration : From spring 3.0. we can config spring beans using java programs. @Configuration, @ComponentScan, @Bean

By implementing InitializingBean and Disposable Bean interfaces each having only one methods each afterPropertiesSet() and destroy(). But it is not recommended because it will create tight coupling with the spring Framework.

Providing init method and destroy method attribute values for th ebean in the spring bean configuration. This is recommmended.

@PostConstruct and @PreDestroy annotations can be used for post-init and pre destroy.

At first the constructor method are used, then the post init method.

When context is getting closed, beans are destroyed in the reverse order.


## Bean scopes
The scope of a bean defines the life cycle and visibility of that bean.

The latest version of spring defines 6 types of scopes.

1. Singleton : Single Bean Instance per spring IoC Container. This is the default scope
2. Prototype : Creates new instance each and every time a bean is requested.
3. Request
4. Session
5. Application
6. websocket

The last four scopes mentioned are only available in web aware application.



## Events

## AOP with Spring Framework

## JDBC Framework
JDBC stands for Java Database Connectivity. JDBC is Java API to connect and execute the query with the database. JDBC API uses JDBC drivers to connect with the database. 

**JDBC STEPS**

There are 7 steps to connect any java application with the database using JDBC.
They are :

* Import the package
* Load and Register the Driver class
* Create Connection
* Create Statement
* Execute queries
* Process results
* Close Connection


While working with the database usng JDBC, it is very hard to write unnecessary code to handle exceptions, opening and closing database connections for every operation methods - insert, update delete. It just not efficient, ugly, error prone.

Spring JDBC internally uses JDBC api, but eliminates a lot of problems of JDBC API.

Spring JDBC Framework takes care of all the low-level details starting from opening the connection, prepare and execute the SQL statement, process exceptions, handle transactions and finally close the connection.
That means with JdbcTemplate, we can save a lot of typing on the redundant codes, because JdbcTemplate will handle it automatically.

So we have to just define connection parameters and specify the SQL statements.

So we can configure a single instance and inject this shared reference into multiple DAO's.

Spring framework provides following approaches:

1. JdbcTemplate
2. NamedParameter JdbcTemplate
3. Simple Jdbcemplate

**JdbcTemplate**
It is the central class in the Spring JDBC support classes. It take care of creation and closing of connection and resources. So it will not be a problem if we forget to close some resource or connection.
Let's see the methods of spring JdbcTemplate class.


* 	**public int update(String query)** is used to insert, update and delete records.
* 	**public int update(String query,Object... args)** is used to insert, update and delete records using PreparedStatement using given arguments.
* 	**public void execute(String query**) is used to execute DDL query.
* 	**public T execute(String sql, PreparedStatementCallback action)** executes the query by using PreparedStatement callback.
* 	**public T query(String sql, ResultSetExtractor rse)** is used to fetch records using ResultSetExtractor.
* 	**public List query(String sql, RowMapper rse)** is used to fetch records using RowMapper.

**NamedParameterJdbcTemplate**
Spring provides another way to insert data by named parameter. In such way we use names instead of "?". So we have to remember column name.

**SimpleJdbcTemplate Example**



## Resources

## Transaction Managements

Transaction is an activity or a group pf activities that are performed as a single unit of work.
Example : To withdraw 500 from account. The steps are:

1. open_account(A)
2. old-balance = A.balance
3. new_balance = old-balance - 500
4. A.balance = new_balance
5. close_account(A)


**Transaction Properties**

* **Atomicity** means either all successful or none.
* **Consistency** ensures bringing the database from one consistent state to another consistent state.
* **Isolation** ensures that transaction is isolated from other transaction.
* **Durability** means once a transaction has been committed, it will remain so, even in the event of errors, power loss etc.

**Transaction Attributes**

1. Propagation
2. Isolation
3. ReadOnly
4. RollbackRules
5. Timeout

**Isolation Level**

 

 



## i18n

## Data Binding

## Logging (Log4j)
