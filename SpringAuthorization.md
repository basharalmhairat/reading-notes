## SpringAuthorization

OAuth is an authorization framework that enables applications — such as Facebook, GitHub, and DigitalOcean — to obtain limited access to user accounts on an HTTP service. It works by delegating user authentication to the service that hosts a user account and authorizing third-party applications to access that user account. OAuth 2 provides authorization flows for web and desktop applications, as well as mobile devices.

This informational guide is geared towards application developers, and provides an overview of OAuth 2 roles, authorization grant types, use cases, and flows.

### OAuth Roles
OAuth defines four roles:

Resource Owner: The resource owner is the user who authorizes an application to access their account. The application’s access to the user’s account is limited to the scope of the authorization granted (e.g. read or write access)
Client: The client is the application that wants to access the user’s account. Before it may do so, it must be authorized by the user, and the authorization must be validated by the API.
Resource Server: The resource server hosts the protected user accounts.
Authorization Server: The authorization server verifies the identity of the user then issues access tokens to the application.
From an application developer’s point of view, a service’s API fulfills both the resource and authorization server roles. We will refer to both of these roles combined, as the Service or API role.

### Abstract Protocol Flow
Now that you have an idea of what the OAuth roles are, let’s look at a diagram of how they generally interact with each other:
![image](https://user-images.githubusercontent.com/97823170/161040108-421cdd28-9531-448e-8fcc-34b4d70cac2b.png)

### Abstract Protocol Flow

Here is a more detailed explanation of the steps in the diagram:

The application requests authorization to access service resources from the user
If the user authorized the request, the application receives an authorization grant
The application requests an access token from the authorization server (API) by presenting authentication of its own identity, and the authorization grant
If the application identity is authenticated and the authorization grant is valid, the authorization server (API) issues an access token to the application. Authorization is complete.
The application requests the resource from the resource server (API) and presents the access token for authentication
If the access token is valid, the resource server (API) serves the resource to the application
The actual flow of this process will differ depending on the authorization grant type in use, but this is the general idea. We will explore different grant types in a later section.

### Application Registration
Before using OAuth with your application, you must register your application with the service. This is done through a registration form in the developer or API portion of the service’s website, where you will provide the following information (and probably details about your application):
![image](https://user-images.githubusercontent.com/97823170/161040973-a21d3938-4bcc-4eff-b5a9-36e17842afe7.png)

Application Name
Application Website
Redirect URI or Callback URL
The redirect URI is where the service will redirect the user after they authorize (or deny) your application,
and therefore the part of your application that will handle authorization codes or access tokens.

### Grant Type: Authorization Code
The authorization code grant type is the most commonly used because it is optimized for server-side applications, where source code is not publicly exposed, and Client Secret confidentiality can be maintained. This is a redirection-based flow, which means that the application must be capable of interacting with the user-agent (i.e. the user’s web browser) and receiving API authorization codes that are routed through the user-agent.

Now we will describe the authorization code flow:
![image](https://user-images.githubusercontent.com/97823170/161040643-82ac9605-1643-457b-b2a8-ddef953cf6c9.png)

11.1.1 Authorities
As we saw in the technical overview, all Authentication implementations store a list of GrantedAuthority objects. These represent the authorities that have been granted to the principal. the GrantedAuthority objects are inserted into the Authentication object by the AuthenticationManager and are later read by AccessDecisionManager s when making authorization decisions.

GrantedAuthority is an interface with only one method:

String getAuthority();
This method allows AccessDecisionManager s to obtain a precise String representation of the GrantedAuthority. By returning a representation as a String, a GrantedAuthority can be easily "read" by most AccessDecisionManager s. If a GrantedAuthority cannot be precisely represented as a String, the GrantedAuthority is considered "complex" and getAuthority() must return null.

An example of a "complex" GrantedAuthority would be an implementation that stores a list of operations and authority thresholds that apply to different customer account numbers. Representing this complex GrantedAuthority as a String would be quite difficult, and as a result the getAuthority() method should return null. This will indicate to any AccessDecisionManager that it will need to specifically support the GrantedAuthority implementation in order to understand its contents.

Spring Security includes one concrete GrantedAuthority implementation, SimpleGrantedAuthority. This allows any user-specified String to b
e converted into a GrantedAuthority. All AuthenticationProvider s included with the security architecture use

11.1.2 Pre-Invocation Handling
As we’ve also seen in the Technical Overview chapter, Spring Security provides interceptors which control access to secure objects such as method invocations or web requests. A pre-invocation decision on whether the invocation is allowed to proceed is made by the AccessDecisionManager.

The AccessDecisionManager
The AccessDecisionManager is called by the AbstractSecurityInterceptor and is responsible for making final access control decisions. The AccessDecisionManager interface contains three methods:

void decide(Authentication authentication, Object secureObject,
    Collection<ConfigAttribute> attrs) throws AccessDeniedException;

boolean supports(ConfigAttribute attribute);

boolean supports(Class clazz);
The AccessDecisionManager's decide method is passed all the relevant information it needs in order to make an authorization decision. In particular, passing the secure Object enables those arguments contained in the actual secure object invocation to be inspected. For example, let’s assume the secure object was a MethodInvocation. It would be easy to query the MethodInvocation for any Customer argument, and then implement some sort of security logic in the AccessDecisionManager to ensure the principal is permitted to operate on that customer. Implementations are expected to throw an AccessDeniedException if access is denied.

The supports(ConfigAttribute) method is called by the AbstractSecurityInterceptor at startup time to determine if the AccessDecisionManager can process the passed ConfigAttribute. The supports(Class) method is called by a security interceptor implementation to ensure the configured AccessDecisionManager supports the type of secure object that the security interceptor will present.

SimpleGrantedAuthority to populate the Authentication object.
