## SpringAuthentication

Spring Security is a framework that focuses on providing authentication and authorization mechanisms to Spring applications.
It was started in 2003 as an open-source project under the name of "Acegi Security" before officially being included in Spring Projects.
![image](https://user-images.githubusercontent.com/97823170/160487224-cdfe38c8-748d-46ef-a3ba-71793b828502.png)


***What is Spring Boot security?***

Spring Boot security can mean different things. In general, it is adding the Spring Security framework to your Spring Boot web application by including the Spring Boot security starter dependency. Spring Security is an authentication and access-control framework and can be easily included in a Spring Boot application. On the other hand, Spring Boot security is more than just including the Spring Security framework.
This cheatsheet focuses on the broader topic of Spring Boot security and how to secure your application created with Spring Boot.

### Authentication and Access Control

Application security boils down to two more or less independent problems: authentication (who are you?) and authorization (what are you allowed to do?). Sometimes people say “access control” instead of "authorization", which can get confusing, but it can be helpful to think of it that way because “authorization” is overloaded in other places. Spring Security has an architecture that is designed to separate authentication from authorization and has strategies and extension points for both.

Authentication
The main strategy interface for authentication is AuthenticationManager, which has only one method:
```
public interface AuthenticationManager {

  Authentication authenticate(Authentication authentication)
    throws AuthenticationException;
}
```
![image](https://user-images.githubusercontent.com/97823170/160487284-6b4f14d8-a7b0-445c-bb26-6efb373f188c.png)

An AuthenticationManager can do one of 3 things in its authenticate() method:

- Return an Authentication (normally with authenticated=true) if it can verify that the input represents a valid principal.

- Throw an AuthenticationException if it believes that the input represents an invalid principal.

- Return null if it cannot decide

```
public interface AuthenticationProvider {

	Authentication authenticate(Authentication authentication)
			throws AuthenticationException;

	boolean supports(Class<?> authentication);
}
```
![image](https://user-images.githubusercontent.com/97823170/160487319-577ddb9a-22de-45fd-a694-23630a4b825b.png)

### Customizing Authentication Managers

Spring Security provides some configuration helpers to quickly get common authentication manager features set up in your application. The most commonly used helper is the AuthenticationManagerBuilder, which is great for setting up in-memory, JDBC, or LDAP user details or for adding a custom UserDetailsService. The following example shows an application that configures the global (parent) AuthenticationManager:

@Configuration
public class ApplicationSecurity extends WebSecurityConfigurerAdapter {

 
```
  @Autowired
  public void initialize(AuthenticationManagerBuilder builder, DataSource dataSource) {
    builder.jdbcAuthentication().dataSource(dataSource).withUser("dave")
      .password("secret").roles("USER");
  }

}
```
### Authorization or Access Control

Once authentication is successful, we can move on to authorization, and the core strategy here is AccessDecisionManager. There are three implementations provided by the framework and all three delegate to a chain of AccessDecisionVoter instances, a bit like the ProviderManager delegates to AuthenticationProviders.

An AccessDecisionVoter considers an Authentication (representing a principal) and a secure Object, which has been decorated with ConfigAttributes:
```
boolean supports(ConfigAttribute attribute);

boolean supports(Class<?> clazz);

int vote(Authentication authentication, S object,
        Collection<ConfigAttribute> attributes);
```
        
### Web Security
 
Spring Security in the web tier (for UIs and HTTP back ends) is based on Servlet Filters,
so it is helpful to first look at the role of Filters generally. The following picture shows the typical layering of the handlers for a single HTTP request.

***Spring Boot security***

The following curated list will go beyond just introducing Spring Security for authentication and authorization in your Spring Boot application. It focuses on the broader Spring Boot security strategy and covers the following topic:

- Use HTTPS in production
- Test your dependencies and find Spring Boot vulnerabilities 
- Enable CSRF protection
- Use a content security policy for Spring Boot XSS protection
- Use OpenID Connect for authentication
- Use password hashing
- Use the latest releases
- Store secrets securely
- Pen test your app
- Have your security team do a code review

### How do I add security to Spring Boot?
When Adding Spring Security to your Spring Boot application begins with adding the security starter dependency.
```
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

By default, authentication is enabled when the starter dependency is included.
You can configure the credentials by setting the properties spring.security.user.name and spring.security.user.password

***How do I disable Spring Security in Spring Boot?***

By default, Spring Security is enabled whenever you include the spring-boot-starter-security package. This can by easily disabled by excluding the SecurityAutoConfiguration in the application.properties file.

spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.security.SecurityAutoConfiguration

Ready to fix Spring Boot vulnerabilities?
