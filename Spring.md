## Building an Application with Spring Boot

This guide provides a sampling of how Spring Boot helps you accelerate application development.
As you read more Spring Getting Started guides, you will see more use cases for Spring Boot.
This guide is meant to give you a quick taste of Spring Boot. If you want to create your own Spring Boot-based project,
visit Spring Initializr, fill in your project details, pick your options, and download a bundled up project as a zip file.

# What You Need
- About 15 minutes

- A favorite text editor or IDE

- JDK 1.8 or later

- Gradle 4+ or Maven 3.2+

- You can also import the code straight into your IDE:

- Spring Tool Suite (STS)

- IntelliJ IDEA


# we Can Do with Spring Boot :

- Spring Boot offers a fast way to build applications. It looks at your classpath and at the beans you have configured,
  makes reasonable assumptions about what you are missing, and adds those items. With Spring Boot, you can focus more on business features and less on infrastructure.

The following examples show what Spring Boot can do for you:

.Is Spring MVC on the classpath? There are several specific beans you almost always need, and Spring Boot adds them automatically.
A Spring MVC application also needs a servlet container, so Spring Boot automatically configures embedded Tomcat.

.Is Jetty on the classpath? If so, you probably do NOT want Tomcat but instead want embedded Jetty. Spring Boot handles that for you.

.Is Thymeleaf on the classpath? If so, there are a few beans that must always be added to your application context. Spring Boot adds them for you.

These are just a few examples of the automatic configuration Spring Boot provides. At the same time, Spring Boot does not get in your way. For example, if Thymeleaf is on your path, Spring Boot automatically adds a SpringTemplateEngine to your application context. But if you define your own SpringTemplateEngine with your own settings, Spring Boot does not add one. This leaves you in control with little effort on your part.
