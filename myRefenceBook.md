# Spring and MVC Topics to learn

## Index
* [Core](#core)
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

There are about 20 modules in spring. They canbe grouped into 7 groups. They are : 
* **Core Containers :**Consists of Core, Beans, Context, Expression modules.
* **Data Access/ Integration :**Consists of JDBC, ORM, OXM, JMS, Transactions
* **Web :**Web, servlet, Portlet, Struts
* **AOP :**Aspect Oriented Programming
* **Aspects :** Integration with AspectJ
* **Instrumentation :**Class instrumentation support and classloader implementations in application server
* **Test :**JUnit, TestNG



## Understand about the necessary environment setup to work with Spring

At first we need a JDK, an editor and maven installed in our pc to work with spring.

## Maven Dependency Management

It is a mechanism for centralizing deoendency information. It is a tag consists of dependencies tag whuch itself can contains multiple dependency tag. Each dependency supposed to have at least 3 main tags: groupId, artifactId and version


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

Traditionally spring allows to manage bean dependencies by using XML-based configuration.
Unlike the XML approach, Java-based configuration allows you to manage bean components programatically through spring annotations. Annotation injection is performed before XML injection. So annotation configuration is override by xml xml configuration.

Some important spring annotations are:

* **@Configuration:** Used to indicate that a class declares one or more @Bean methods. These classes are processed by the Spring container to generate bean definitions and service requests for those beans at runtime.
* **@Bean:** Indicates that a method produces a bean to be managed by the Spring container. This is one of the most used and important spring annotation.
* **@PreDestroy** and **@PostConstruct** are alternative way for bean initMethod and destroyMethod. It can be used when the bean class is defined by us.
* **@ComponentScan:** Configures component scanning directives for use with **@Configuration** classes. Here we can specify the base packages to scan for spring components.
* **@Component**: Indicates that an annotated class is a “component”. Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning.
* **@PropertySource**: provides a simple declarative mechanism for adding a property source to Spring’s Environment. There is a similar annotation for adding an array of property source files i.e **@PropertySources**.
* **@Service:** Indicates that an annotated class is a “Service”. This annotation serves as a specialization of **@Component**, allowing for implementation classes to be autodetected through classpath scanning.
* **@Repository:** Indicates that an annotated class is a “Repository”. This annotation serves as a specialization of @Component and advisable to use with DAO classes.
* **@Autowired:** Spring @Autowired annotation is used for automatic injection of beans. Spring @Qualifier annotation is used in conjunction with Autowired to avoid confusion when we have two of more bean configured for same type.

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
4. Rollback
5. Timeout

**Isolation**

Isolation level defines how the changes made to the same data by one transaction affect other simultaneous concurrent transactions and also how and when that changed data becomes available to other transactions.

* **Dirty Read** occur when transaction reads a uncommited data.
* **non-repeatable read** occurs when a transaction reads the same data multiple times but gets different results each time. It happens when another transaction commited **updates**.
* **Phantom read** are similar to non-repeatable reads, but when reading from commited **inserts** and **deletes**.

To overcome this problems spring provides some Isolation levels.

**Isolation Levels**

* **ISOLATION_DEFAULT** : Default isolation specific to the data source.
* **ISOLATION_READ_UNCOMMITED** : Read changes that are uncommitted. Leads to dirty reads, phantom reads and non repeatable reads.
* **ISOLATION_READ_COMMITED** : Read only commited data. Dirty read is prevented but Non-repeatable read and phantom read are possible.
* **ISOLATION_REPEATABLE_READ** : Multiple Reads of the same field will yield the same results untill it is changed by itself. Dirty Reads and non repeatable reads are prevented but phantom reads are possible as other transactions may edit the fields.
* **ISOLATION_SERIALIZABLE** : dirty, phantom and norepeatable reads are prevented but hampers the performance of the application.

**Propagation**
Propagation configuration tells the transaction manager if a new transaction should be started or can use the transaction which already exists.

**Propagation Attributes**
* **PROPAGATION_MANDATORY** : Method should run in a transaction and if no transaction exits exception will be thrown.
* **PROPAGATION_NESTED** : Method should run in a nested transaction.
* **PROPAGATION_NEVER** : Method should not run in a transaction. If a transaction exists exception will be thrown.
* **PROPAGATION_NOT_SUPPORTED** : Method should not run in a transaction. If a transaction exists it will be suspended untill the method completes execution.
* **PROPAGATION_REQUIRED** : Method should run in a transaction. If already exists, method will run in it and if not a new transaction will be created.
* **PROPAGATION_REQUIRES_NEW** : Method should run in a new transaction. If a transaction already exists, it will be suspende till the method finished.
* **PROPAGATION_SUPPORTS** : Method need not run in a transaction. But if already exists , it supports the one which is already in progress.

**ReadOnly**

By applying ReadOnly to a transaction, the underlying data store will apply some performance optimizations to render data more faster.

**Timeout**

By declaring the Timeout attribute, we can ensure that long running transactions are rolled back after certain time. It is useful to apply in PROPAGATION_REQUIRED, PROPAGATION_REQUIRES_NEW and PROPAGATION_NESTED

**Rollback**

Rollback tells a transaction manager when to rollback a transaction when an exception occurs. By default the transaction will be rolled back when runtime exception occurs.


**Local vs. Global Transactions**

Local transactions are specific to a single transactional resource like a JDBC connection, whereas global transactions can span multiple transactional resources like transaction in a distributed system.

Local transaction management can be useful in a centralized computing environment where application components and resources are located at a single site, and transaction management only involves a local data manager running on a single machine. Local transactions are easier to be implemented.

Global transaction management is required in a distributed computing environment where all the resources are distributed across multiple systems. In such a case, transaction management needs to be done both at local and global levels. A distributed or a global transaction is executed across multiple systems, and its execution requires coordination between the global transaction management system and all the local data managers of all the involved systems.

Transaction Management simply means: How does spring start, commit or rollback JDBC transactions. Whereas with plain JDBC we only have one way (setAutoCommit(false)) to manage transactions, spring offers us many different, more convinient ways to achieve the same.

**Spring Framework Transaction Management**

Spring Support two types of transaction managements. They are: 

**Programmatic Transaction**

Programming tranasctions gives us the precise control on the boundaries of the transaction. This gives us extreme flexibility but is difficult to maintain. Either through a TransactionTemplate or directly through the PlatformTransactionManager.
In PlatformTransactionManager Interface all methods throw TransactionException. This Exception itself is UncheckedException means developer is not forced to handle these exceptions.

TransactionStatus interface defines several methods to get the status of transaction and controls the transaction execution as well.

**Declarative Transaction**
Declarative transaction offers to separate transaction management from buisiness code. We only use annotations or XML-based configuration to manage the transactions.

Declarative transaction management is preferable over programmatic transaction management though it is less flexible than programmatic transaction management, which allows you to control transactions through your code. But as a kind of crosscutting concern, declarative transaction management can be modularized with the AOP approach. Spring supports declarative transaction management through the Spring AOP framework.

Programmatic approach has a tight coupling on the transaction code with  business logic. In Declarative transactions, we can separate transaction management code from business logic.

So if the the number of steps in the transaction is smaller then we will use programmatic transaction management otherwise we will use declarative transaction management.

Spring supports declarative transactions using : 

**Transaction Advices (using Aspect Oriented Programming) **

In this approach we need to-  a)  declare a transaction advice via the element defined in the tx namespace.  For example

	<tx:advice id=”txAdvice” transaction-manager=”transactionManager”>
	<tx:attributes>
		<tx:method name=”buy*” propagation=”REQUIRED”/>
		<tx:method name=”*” propagation=”SUPPORTS” />
	
	</tx:attributes>
	</tx:advice>

Transaction advice defines element which can have several tags to define several properties. In above example, any method whose name starts with “buy”  are required or a part of the transaction, but all other methods will execute in current transaction but will not create a new if the transaction does not exist.

b.  Now we need to associate transaction advice ()  with a pointcut using

	<aop:config>
	<aop:advisor advice-ref=”txAdvice”
		pointcut =” execution(* jdbc.BuyProduct.buyProduct(..))”/>
	</aop:config>

**@Transactional Annotation**

Along with the declarative approach with pointcut , advisors configuration in beans configuration file , Spring allows another way of declarative transaction management using @Transactional annotation  on the method which requires transaction and enabling element in the beans configuration file. 


**What is the difference between physical and logical transactions?**

**Physical Transactions:** Are your actual JDBC transactions.

**Logical Transactions:** Are the (potentially nested) @Transactional-annotated (Spring) methods.





## i18n

i18n is an acronym for internationalization. Internationalization is the process of desigining a software appication so that it can potentially be adapted to various languages and regions without engineering changes.
The Spring framework uses LocaleResolver to support the internationalization and localization as well.

An application written in Java, and Spring as well, are capable to support different languages by providing textual messages externally. These messages are usually written in .properties files.

**Naming convention for resource files**

	basename_languageCode_countryCode.properties
'basename' can be related to the application part where these properties belong to. For example orderView_en_us.properties.

The main Spring interface to support of I18n/L10n messages is MessageSource.


**Steps of i18n :**

1. Have each locale specific properties file having texts in that locale specific language. Spring doesn't provide any annotations based approach for message resolutions. The only appropriate way is to inject the implementation of MessageSource as a bean.

2. Then we have to register the beans.

3. make view changes to support displaying locale specific text messages






## Data Binding

## Logging (Log4j)
