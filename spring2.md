Spring Boot is a project that is built on the top of the Spring Framework. It provides an easier and faster way to set up,
configure, and run both simple and web-based applications.

![image](https://user-images.githubusercontent.com/97823170/159148363-2ce8b392-2033-4844-91f9-d3e5fdc71ee0.png)

Why should we use Spring Boot Framework?

We should use Spring Boot Framework because:

The dependency injection approach is used in Spring Boot.
It contains powerful database transaction management capabilities.
It simplifies integration with other Java frameworks like JPA/Hibernate ORM, Struts, etc.
It reduces the cost and development time of the application.
Along with the Spring Boot Framework, many other Spring sister projects help to build applications addressing modern business needs. There are the following Spring sister projects are as follows:

Spring Data: It simplifies data access from the relational and NoSQL databases.
Spring Batch: It provides powerful batch processing.
Spring Security: It is a security framework that provides robust security to applications.
Spring Social: It supports integration with social networking like LinkedIn.
Spring Integration: It is an implementation of Enterprise Integration Patterns. It facilitates integration with other enterprise applications using lightweight messaging and declarative adapters.

### Building an MVC Application with Spring Framework: A Beginner's Tutorial

![image](https://user-images.githubusercontent.com/97823170/159148636-b2105a15-e026-4399-9970-d3cae4bc7589.png)

The Spring Framework is a powerful, feature-rich, and well-designed framework for the Java platform.
It offers a collection of programming and configuration models that aim to simplify and streamline the development process of robust and testable applications in Java.
In this article, Toptal engineer Stefan Varga challenges the popular notion of Java as a complicated platform for simple needs, and walks us through
a step by step tutorial to building a simple MVC application with the Spring Framework and JPA.

![image](https://user-images.githubusercontent.com/97823170/159148662-37faeb90-482e-4e62-85c7-ee892fec919e.png)

***Repositories***
With JPA we can define a very useful DeveloperRepository interface and SkillRepository interface, which allow for easy CRUD operations. These interfaces will allow us to access stored developers and skills through simple method calls, such as:

“respository.findAll()”: returns all developers
“repository.findOne(id)”: returns developer with given ID
To create these interfaces, all we need to do is extend the CrudRepository interface.

***Controller***
Next, we can work on the controller for this application.
The controller will map request URIs to view templates and perform all necessary processing in between.
Mapping of URIs to methods is done via simple “@RequestMapping” annotations. In this case, every method of the controller is mapped to a URI.

The model parameter of these methods allows data to be passed to the view. In essence, these are simple maps of keys to values.

Each controller method either returns the name of the Thymeleaf template to be used as view, or a URL in a specific pattern (“redirect:”) to redirect to. For example, the methods “developer” and “_developersList_” returns the name of a template, while “developersAdd” and “developersAddSkill” return URLs to redirect to.

Within the controller, the “@Autowired” annotations automatically assigns a valid instance of our defined repository in the corresponding field.
This allows access to relevant data from within the controller without having to deal with a lot of boilerplate code.

![image](https://user-images.githubusercontent.com/97823170/159148704-2f3462b6-25c4-4a90-b988-6f56530911d5.png)

***Views***
Finally, we need to define some templates for the views to be generated. For this we are using Thymeleaf, a simple templating engine. The model we used in controller methods is available directly within the templates, i.e. when we enter a contract into “contract” key in a model, we will be able to access the name field as “contract.name” from within the template.

Thymeleaf contains some special elements and attributes that control generation of HTML. They are very intuitive and straightforward. For example, to populate the contents of a span element with the name of a skill, all you need to do is define the following attribute (assuming that the key “skill” is defined in the model):
```
<span th:text="${skill.label}"></span>
```

