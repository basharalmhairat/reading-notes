

a specification that defines an API for object-relational mappings and for managing persistent objects.
Hibernate and EclipseLink are 2 popular implementations of this specification. 

Spring Data JPA adds a layer on top of JPA. That means it uses all features defined by the JPA specification, especially the entity and association mappings, the entity lifecycle management, and JPA’s query capabilities. On top of that,
Spring Data JPA adds its own features like a no-code implementation of the repository pattern and the creation of database queries from method names.

 if the JPA specification and its implementations provide most of the features that you use with Spring Data JPA, do you really need the additional layer? Can’t you just use the Hibernate or EclipseLink directly?

You can, of course, do that. That’s what a lot of Java SE applications do. Jakarta EE provides a good integration for JPA without adding an extra layer.

But the Spring Data team took the extra step to make your job a little bit easier. The additional layer on top of JPA enables them to integrate JPA into the Spring stack seamlessly. They also provide a lot of functionality that you otherwise would need to implement yourself.

Here are my 3 favorite features that Spring Data adds on top of JPA.
![image](https://user-images.githubusercontent.com/97823170/159149103-dcf843ea-e1a9-40db-af93-122b1087979d.png)

1. No-code Repositories
The repository pattern is one of the most popular persistence-related patterns. It hides the data store specific implementation details and enables you to implement your business code on a higher abstraction level.

Implementing that pattern isn’t too complicated but writing the standard CRUD operations for each entity creates a lot of repetitive code. Spring Data JPA provides you a set of repository interfaces which you only need to extend to define a specific repository for one of your entities.
 example of a repository that provides the required methods:

```
public interface AuthorRepository extends CrudRepository<Author, Long> {}
```

2. Reduced boilerplate code
To make it even easier, Spring Data JPA provides a default implementation for each method defined by one of its repository interfaces. That means that you no longer need to implement basic read or write operations. And even so all of these operations don’t require a lot of code, not having to implement them makes life a little bit easier and it reduces the risk of stupid bugs.

3. Generated queries
Another comfortable feature of Spring Data JPA is the generation of database queries based on method names. As long as your query isn’t too complex, you just need to define a method on your repository interface with a name that starts with find…By. Spring then parses the method name and creates a query for it.

```
public interface BookRepository extends CrudRepository<Book, Long> {
     
    Book findByTitle(String title);
}
```
Using Spring Data JPA with Spring Boot
As you have seen, Spring Data JPA can make the implement of your persistence layer much easier. So, what do you have to do to use it in your application? Not much, if you’re using Spring Boot and structure your application in the right way.

You only need to add the spring-boot-starter-data-jpa artifact, and your JDBC driver to your maven build. The Spring Boot Starter includes all required dependencies and activates the default configuration.


***Creating a JPA Repository***
![image](https://user-images.githubusercontent.com/97823170/159149226-5462c4a9-c505-49de-9625-29db6c57d692.png)

In the previous section, we have created a table in-memory database and saw that all the data is populated correctly. In this section, we will create a repository that returns the response for the service.

Step 1: Create an interface with the name ExchangeValueRepository and extends the JpaRepository class. We have to pass two parameters: type of the entity that it manages and the type of the Id field.

public interface ExchangeValueRepository extends JpaRepository<ExchangeValue, Long>  
Step 2: Open CurrencyExchageController.java file and autowired the ExchageValueRepository.

```
@Autowired  
private ExchangeValueRepository repository;  
Step 3: Create a query method in the ExcahngeValueRepository.java file.
```

ExchangeValue findByFromAndTo(String from, String to);  
In the above statement, ExchangeValue is the expected response. There are two columns that we have to find are from and to.

If we want to find data on the basis of single column, we can pass a column name. For example:
![image](https://user-images.githubusercontent.com/97823170/159149241-01850648-3ea4-4a5c-aa04-2a7d763574ae.png)

ExchangeValue findByFrom (String from);  
Step 4: In the CurrencyExchangeController.java use the following statement:

ExchangeValue exchangeValue=repository.findByFromAndTo(from,to);  

Step 5: Restart the application to pick up the changes. Open the browser and type the URI

