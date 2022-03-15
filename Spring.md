# Building an Application with Spring Boot

This guide provides a sampling of how Spring Boot helps you accelerate application development.
As you read more Spring Getting Started guides, you will see more use cases for Spring Boot.
This guide is meant to give you a quick taste of Spring Boot. If you want to create your own Spring Boot-based project,
visit Spring Initializr, fill in your project details, pick your options, and download a bundled up project as a zip file.

## What You Need
- About 15 minutes

- A favorite text editor or IDE

- JDK 1.8 or later

- Gradle 4+ or Maven 3.2+

- You can also import the code straight into your IDE:

- Spring Tool Suite (STS)

- IntelliJ IDEA


## we Can Do with Spring Boot :
![thyme](https://user-images.githubusercontent.com/97823170/158384173-f1fce749-8bbf-4b86-b23d-17b685b7a990.jpg)

- Spring Boot offers a fast way to build applications. It looks at your classpath and at the beans you have configured,
  makes reasonable assumptions about what you are missing, and adds those items. With Spring Boot, you can focus more on business features and less on infrastructure.

The following examples show what Spring Boot can do for you:

.Is Spring MVC on the classpath? There are several specific beans you almost always need, and Spring Boot adds them automatically.
A Spring MVC application also needs a servlet container, so Spring Boot automatically configures embedded Tomcat.

.Is Jetty on the classpath? If so, you probably do NOT want Tomcat but instead want embedded Jetty. Spring Boot handles that for you.

.Is Thymeleaf on the classpath? If so, there are a few beans that must always be added to your application context. Spring Boot adds them for you.

These are just a few examples of the automatic configuration Spring Boot provides. At the same time, Spring Boot does not get in your way. For example, if Thymeleaf is on your path, Spring Boot automatically adds a SpringTemplateEngine to your application context. But if you define your own SpringTemplateEngine with your own settings, Spring Boot does not add one. This leaves you in control with little effort on your part.
![1554742446913_Screen Shot 2019-04-08 at 6 51 40 pm](https://user-images.githubusercontent.com/97823170/158384005-99c5ac77-1858-4e90-b13c-38c53b36cea0.png)

## Run the Application
To run the application, run the following command in a terminal window (in the complete) directory:

./gradlew bootRun
If you use Maven, run the following command in a terminal window (in the complete) directory:

./mvnw spring-boot:run

## Add Unit Tests
You will want to add a test for the endpoint you added, and Spring Test provides some machinery for that.

If you use Gradle, add the following dependency to your build.gradle file:

testImplementation('org.springframework.boot:spring-boot-starter-test')COPY
If you use Maven, add the following to your pom.xml file:
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-test</artifactId>
	<scope>test</scope>
</dependency>COPY
```
Now write a simple unit test that mocks the servlet request and response through your endpoint, as the following listing (from src/test/java/com/example/springboot/HelloControllerTest.java) shows:

# Spring MVC and Thymeleaf: how to access data from templates

2. Project Setup
First, we'll need to add our Thymeleaf dependency:
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
    <version>2.6.1</version>
</dependency>
Second, let's include the Spring Boot web starter:

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.6.1</version>
</dependency>
```
This dependency provides us with REST support that we'll later use to create some endpoints.
3. Model Attributes
Model attributes are used inside controller classes that prepare the data for rendering inside a view.

One way we can add attributes to our model is to require an instance of Model as a parameter in a controller method.


freestar
Let's pass our emailData as an attribute:
```
@GetMapping(value = "/email/modelattributes")
public String emailModel(Model model) {
    model.addAttribute("emailData", emailData);
    return "mvcdata/email-model-attributes";
}
```
Spring will then inject an instance of Model for us when /email/modelattributes is requested.

Then, we can refer to our emailData model attribute in a Thymeleaf expression:
```
<p th:text="${emailData.emailSubject}">Subject</p>
```
Another way we can do it is by telling our Spring container what attribute is required in our view by using @ModelAttribute:
```
@ModelAttribute("emailModelAttribute")
EmailData emailModelAttribute() {
    return emailData;
}
```
And then we can represent the data in our view as:

