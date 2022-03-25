## one-to-many relationship

What Does One-to-Many Relationship Mean? In relational databases, a one-to-many relationship occurs when a parent record in one table can potentially
reference several child
records in another table
One-to-many relationships

***What Are Relationships and Why Do We Need Them?***

If we take a deeper look at the table used in the prior example, we will see that it does not really represent a complete order. It does not have all the information you would expect it to have. You will notice that it does not include any data related to the customer that made the order, nor does it have anything about the products or services ordered.

What should we do to complete this design to store order data? Should we add customer and product information to the Order table? That would require adding new columns (attributes) for customer names, tax identifiers, addresses, etc. as shown below:

In a one-to-many relationship, one record in a table can be associated with one or more records in another table. For example, each customer can have many sales orders.
![image](https://user-images.githubusercontent.com/97823170/160113571-1bc7c1d8-4e62-4fb5-99da-4b4d7c46881e.png)

A one-to-many relationship looks like this in the relationships graph:

Customers table and orders table with a one-to-many relationship line between them

In this example the primary key field in the Customers table, Customer ID, is designed to contain unique values. The foreign key field in the Orders table, Customer ID, is designed to allow multiple instances of the same value.

This relationship returns related records when the value in the Customer ID field in the Orders table is the same as the value in the Customer ID field in the Customers table.

![image](https://user-images.githubusercontent.com/97823170/160113646-131a9a0f-071c-4293-a2ab-68d81577bde5.png)


## Integration Testing

It is important to be able to perform some integration testing without requiring deployment to your application server or connecting to other enterprise infrastructure. This will enable you to test things such as:

The correct wiring of your Spring IoC container contexts.
Data access using JDBC or an ORM tool. This would include such things as the correctness of SQL statements, Hibernate queries, JPA entity mappings, etc.
The Spring Framework provides first-class support for integration testing in the spring-test module. The name of the actual JAR file might include the release version and might also be in the long org.springframework.test form, depending on where you get it from (see the section on Dependency Management for an explanation). This library includes the org.springframework.test package, which contains valuable classes for integration testing with a Spring container. This testing does not rely on an application server or other deployment environment. Such tests are slower to run than unit tests but much faster than the equivalent Selenium tests or remote tests that rely on deployment to an application server.

In Spring 2.5 and later, unit and integration testing support is provided in the form of the annotation-driven Spring TestContext Framework.
The TestContext framework is agnostic of the actual testing framework in use, thus allowing instrumentation of tests in various environments including JUnit,
TestNG, and so on.

### Dependency Injection of test fixtures

When the TestContext framework loads your application context, it can optionally configure instances of your test classes via Dependency Injection. This provides a convenient mechanism for setting up test fixtures using preconfigured beans from your application context. A strong benefit here is that you can reuse application contexts across various testing scenarios (e.g., for configuring Spring-managed object graphs, transactional proxies, DataSources, etc.), thus avoiding the need to duplicate complex test fixture setup for individual test cases.

As an example, consider the scenario where we have a class, HibernateTitleRepository, that implements data access logic for a Title domain entity. We want to write integration tests that test the following areas:

The Spring configuration: basically, is everything related to the configuration of the HibernateTitleRepository bean correct and present?
The Hibernate mapping file configuration: is everything mapped correctly, and are the correct lazy-loading settings in place?

### Support classes for integration testing

The Spring TestContext Framework provides several abstract support classes that simplify the writing of integration tests. These base test classes provide well-defined hooks into the testing framework as well as convenient instance variables and methods, which enable you to access:

The ApplicationContext, for performing explicit bean lookups or testing the state of the context as a whole.
A JdbcTemplate, for executing SQL statements to query the database. Such queries can be used to confirm
database state both prior to and after execution of database-related application code, and Spring ensures that
such queries run in the scope of the same transaction as the application code. When used in conjunction with an ORM tool, be sure to avoid false positives.

### JDBC Testing Support

The org.springframework.test.jdbc package contains JdbcTestUtils, which is a collection of JDBC related utility functions intended to simplify standard database testing scenarios. Specifically, JdbcTestUtils provides the following static utility methods.

countRowsInTable(..): counts the number of rows in the given table
countRowsInTableWhere(..): counts the number of rows in the given table, using the provided WHERE clause
deleteFromTables(..): deletes all rows from the specified tables
![image](https://user-images.githubusercontent.com/97823170/160114921-fe6363db-cfb8-4125-af7b-726536f1fdd6.png)

### Spring Testing Annotations
The Spring Framework provides the following set of Spring-specific annotations that you can use in your unit and integration tests in conjunction with the TestContext framework. Refer to the corresponding javadocs for further information, including default attribute values, attribute aliases, and so on.

``` @ContextConfiguration ```

Defines class-level metadata that is used to determine how to load and configure an ApplicationContext for integration tests. Specifically, @ContextConfiguration declares the application context resource locations or the annotated classes that will be used to load the context.
![image](https://user-images.githubusercontent.com/97823170/160115016-8b3daa36-5082-407f-9988-455607335e1e.png)

Resource locations are typically XML configuration files located in the classpath; whereas, annotated classes are typically @Configuration classes. However, resource locations can also refer to files in the file system, and annotated classes can be component classes, etc.
```
@ContextConfiguration("/test-config.xml")
public class XmlApplicationContextTests {
    // class body...
}
```
```
@ContextConfiguration(classes = TestConfig.class)
public class ConfigClassApplicationContextTests {
    // class body...
}
```

deleteFromTableWhere(..): deletes rows from the given table, using the provided WHERE clause
dropTables(..): drops the specified tables
