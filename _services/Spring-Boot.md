---
title: "Spring Boot"
date: 2019-01-28T15:15:26+10:00
weight: 2
---

Spring Boot is an extension of the Spring Framework that simplify the setup and development of new spring application

![Accounting Services](/images/springboot/spring-boot.png)

- A convention -over -configuration approach to avoid boilerplate code.
- Embedded server like Tomcat, Jetty or Undertow  to run application without needing a separate sever installation.
- Auto configuration to automatically configuring spring application based on dependency present in the class path.
- Reduce the configuration time and efforts in contacts, in traditional spring boot require extensive configuration either XML or Annotations. 

# How We create spring boot application ?

- Spring initializer  web based.
- Manually by setting up Gradle or Maven dependencies.
- Using IDEs like IntelliJ and Eclipse have build in spring project.


# What is purpose of '@SpringBootApplication' annotation ?

'@SpringBootApplication' is a key annotation in a spring boot that signify simplify the configuration and setup of spring application by combining several important annotation into one. It allow to quickly and minimal configuration to casing the logic rather than setup.

### '@SpringBootApplication' is equivalent to 3 annotation.

1. @ComponentScan
2. @Configuration
3. @EnableAutoConfiguration

- **@ComponentScan**
  - With Spring, we use the @ComponentScan annotation along with the @Configuration annotation to specify the packages that we want to be scanned. @ComponentScan without arguments tells Spring to scan the current package and all of its sub-packages.

- **@Configuration**
  - @Configuration annotation which indicates that the class has @Bean definition methods. So Spring container can process the class and generate Spring Beans to be used in the application.

- **@EnableAutoConfiguration**
  - It enable Spring Boot auto-configuration to automatically configure your Spring Application based on their jar dependencies you added.

# What is IoC container ?

IoC(Inversion of Control) container is fundamental concept of Spring Framework, which is responsible for managing the life cycle.

The IoC container make use of dependency injection to mange component and their dependencies.

### Key responsiblility of the IoC container

1. **Bean Creation :** Container initiate bean which are define in the configuration.
2. **Dependency Injection :** The container inject necessary dependency into bean, either view constructor injection, setter injection or field injection.
3. **Lifecycle Management :** The container mange lifecycle of bean, including initializer and distraction.
4. **Configuration Management :** The container read the configuration metadata to understand how to initiate, configure and assemble the bean.

# What is @Bean?

Bean is object that manged by IoC container. @Bean annotation is spring annotation in Spring Framework is used to declare a method as a bean provider, meaning that the method's return value will be registered as a Spring bean within the application context. This is typically used in configuration classes (classes annotated with @Configuration), where you define beans that are managed by the Spring container.

### Lifecycle of a @Bean:

1. **Instantiation :** 
  - When the Spring container is started, it processes configuration classes and invokes methods annotated with @Bean to instantiate and configure the beans.
2. **Dependency Injection :**
  - After the bean is created and dependencies are injected, the bean can undergo additional initialization. If the bean implements InitializingBean or has a custom initialization method specified by @Bean(initMethod = "methodName"), that method is called.
3. **Usage :**
  - The bean is now fully initialized and ready to be used by other beans or components in the application. It can be injected into other beans using @Autowired, @Inject, or constructor injection.
4. **Destruction :**
  - When the application context is being shut down, the Spring container will call the bean's destroy method, if defined. This can be done by implementing DisposableBean or specifying a custom destroy method using @Bean(destroyMethod = "methodName").

### Example

Using '@Configuration'
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

Using @Component
```java
import org.springframework.stereotype.Component;

@Component
public class MyBean {
    // Bean logic
}
```

In this example, myService will be a Spring-managed bean in the application context. The AppConfig class is a configuration class where MyService is defined as a bean.

This lifecycle management ensures that beans are created, initialized, and destroyed in a controlled and predictable way, allowing for complex dependencies and resource management in Spring applications.

#  What are types of annotation in Spring Boot ?
1. **Core Annotations**
- ___@SpringBootApplication___:
  - Combines @SpringBootConfiguration, @EnableAutoConfiguration, and @ComponentScan into a single annotation. It is usually placed on the main application class to enable Spring Boot’s auto-configuration and component scanning.
- ___@Configuration___:
  - Indicates that a class can be used by the Spring IoC container as a source of bean definitions.
- ___@Bean___:
  - Indicates that a method produces a bean to be managed by the Spring container.

2. **StereoType Annotations**  
- ___@Component___:
  - A generic stereotype for any Spring-managed component. It can be used to annotate classes that need to be managed by Spring.
- ___@Service___:
  - A specialized version of @Component, it indicates that an annotated class is a service, which holds business logic.
- ___@Repository___:
  - A specialization of @Component that indicates a Data Access Object (DAO). It also enables automatic exception translation in Spring.
- ___@Controller___:
  - A specialization of @Component used to define a Spring MVC controller.
- ___@RestController___:
  - A combination of @Controller and @ResponseBody, it is used to create RESTful web services. The methods in a @RestController return domain objects instead of views.

3. **Dependency Injection Annotations**
- ___@Autowired___:
  - Marks a constructor, field, setter method, or configuration method to be autowired by Spring’s dependency injection facilities.
- ___@Qualifier___:
  - Used along with @Autowired to specify which bean should be injected when there are multiple candidates.
- ___@Primary___:
  - Indicates that a particular bean should be given preference when multiple beans qualify for autowiring.
- ___@Value___:
  - Used to inject values from properties files, environment variables, or system properties into beans.

4. **Configuration and Conditional Annotations**
- ___@PropertySource___:
  - Used to specify the location of properties files that Spring should load.
- ___@EnableAutoConfiguration___:
  - Enables Spring Boot’s auto-configuration mechanism, which attempts to automatically configure your Spring application based on the jar dependencies you have added.
- ___@Conditional___:
  - Used to conditionally include a bean or configuration based on certain criteria.

5. **Spring MVC and REST Annotations**
- ___@RequestMapping___:
  - Used to map HTTP requests to handler methods of MVC and REST controllers.
- ___@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping___:
  - Variants of @RequestMapping that are specialized for HTTP GET, POST, PUT, DELETE, and PATCH requests.
- ___@PathVariable___:
  - Used to extract values from the URI path.
- ___@RequestParam___:
  - Used to extract query parameters from the URL.
- ___@RequestBody___:
  - Indicates that a method parameter should be bound to the body of the HTTP request.
- ___@ResponseBody___:
  - Indicates that the return value of a method should be used as the response body, instead of a view.

Difference Between **@RequestMapping** and **@GeMapping**

| @RequestMapping | @GeMapping   |
| ----------- | --------- |
|**General Purpose**: Can map to any HTTP method (GET, POST, PUT, DELETE, etc.) by specifying the method attribute.|**Specialized**: Specifically maps to HTTP GET requests only.  |
|**Flexible**: Allows mapping URLs to controller methods with various HTTP methods using attributes like method, params, headers, etc. |**Simplified**: A shorthand for @RequestMapping with method = RequestMethod.GET, used when only GET requests need to be handled.|
|**Usage**: @RequestMapping("/path") can handle multiple HTTP methods if no specific method is defined.|**Usage**: @GetMapping("/path") is used for GET requests, making the code more readable when only GET is required.|
|**Introduced in**: Available since Spring 2.5, providing a general mechanism to map URLs to controller methods.|**Introduced in**: Introduced in Spring 4.3 to provide a more concise and clearer way to handle GET requests.|
|**Example**: ``@RequestMapping(value = "/example", method = RequestMethod.GET)``| **Example**: ``@GetMapping("/example")``|

Difference between **@GetMapping** and **@PostMapping**:

| @GetMapping | @PostMapping   |
| ----------- | --------- |
|**Purpose:** Used to map HTTP GET requests to a specific handler method. GET requests are typically used to retrieve data from the server without modifying it.|**Purpose:** Used to map HTTP POST requests to a specific handler method. POST requests are typically used to submit data to the server, often resulting in a change in state or side effects on the server.|
|**Usage**: Commonly used for fetching data, such as displaying a web page, retrieving data from an API, or loading resources.|**Usage**: Commonly used for sending data to the server, such as submitting form data, uploading a file, or creating a new resource.|
|**Idempotent**: GET requests are idempotent, meaning that making the same request multiple times will have the same effect as making it once.|**Non-Idempotent**: POST requests are generally non-idempotent, meaning that making the same request multiple times can have different effects (e.g., creating multiple records).|
|**Example**: @GetMapping("/example")|**Example**: @PostMapping("/example")|
|**Cacheable**: GET requests are usually cacheable by browsers and intermediate caches.|**Not Cacheable**: POST requests are generally not cacheable, as they are intended to change the server's state.|
|**Parameter Passing**: Parameters are typically passed via the URL query string (e.g., /example?id=1).|**Parameter Passing**: Parameters are typically passed in the body of the request (e.g., form data, JSON).|
|**Security**: Since parameters are passed in the URL, they are visible in browser history, bookmarks, and logs.|**Security**: Parameters are passed in the request body, making them less visible in logs and URLs, though they still need to be secured appropriately.|

>In summary, @GetMapping is used for retrieving data and handling requests where the server's state is not altered, while @PostMapping is used for sending data to the server, typically to create or update resources.

Difference between **@PutMapping** and **@PatchMapping**:

| @PutMapping | @PatchMapping   |
| ----------- | --------- |
|**Purpose**: Used to map HTTP PUT requests to a specific handler method. PUT requests are typically used to update an existing resource with a full update (i.e., replacing the entire resource).|**Purpose**: Used to map HTTP PATCH requests to a specific handler method PATCH requests are typically used to make partial updates to an existing resource (i.e., updating only certain fields).|
|**Idempotent**: PUT requests are idempotent, meaning that making the same request multiple times will have the same effect as making it once. If the same data is sent multiple times, the resource will remain unchanged after the first successful update.|**Non-Idempotent**: PATCH requests can be idempotent or non-idempotent, depending on how the server processes the request. However, PATCH is generally used for making partial changes, so it may not be idempotent in all cases.|
|**Usage**: Commonly used for updating a complete resource. If a resource does not exist, some implementations may create it (though this is not universally agreed upon).|**Usage**: Commonly used for applying partial updates to a resource, where only specific fields are modified, leaving the rest of the resource unchanged.|
|**Example**: @PutMapping("/example/{id}") could be used to update an entire resource with the ID specified in the URL.|**Example**: @PatchMapping("/example/{id}") could be used to update specific fields of a resource with the ID specified in the URL.|
|**Request Body**: The request body typically contains the full representation of the resource, which will replace the existing resource.|**Request Body**: The request body typically contains a set of changes or a partial representation of the resource, indicating which fields should be updated.|
|**Use Case**: Replacing an entire user profile, including all fields, even if some have not changed.|**Use Case**: Updating just the email address of a user profile, without altering the other fields like name or address.|

Here's a comparison between @PathVariable and @RequestParam in Spring:

| @PathVariable | @RequestParam   |
| ----------- | --------- |
|**Purpose**: Used to extract values from the URI path. It is typically used when the URL contains dynamic values that need to be passed to the controller method.|**Purpose**: Used to extract query parameters from the URL. It is typically used for passing optional or additional parameters in the query string.|
|**Binding**: Binds a method parameter to a specific path segment in the URL.|**Binding**: Binds a method parameter to a query parameter in the URL.|
|**Usage**: Commonly used when the URL has a hierarchical structure or when identifying a specific resource (e.g., /users/{id}).|**Usage:** Commonly used for filtering, sorting, or pagination where additional data is passed through the URL (e.g., /users?page=2&sort=asc).|
|**Example URL**: /users/123 where 123 is the id captured by @PathVariable.|**Example URL**: /users?page=2&sort=asc where page=2 and sort=asc are query parameters captured by @RequestParam.|
|**Required by Default**: The value bound by @PathVariable is required and must be present in the URL. You can make it optional by using the required attribute set to false.|**Optional by Default:** The value bound by @RequestParam can be optional. You can specify default values using the defaultValue attribute.|
|**Example:** ``@GetMapping("/users/{id}") public User getUser(@PathVariable("id") Long id) { return userService.getUserById(id); }``|**Example:** ``@GetMapping("/users") public List<User> getUsers(@RequestParam(value = "page", defaultValue = "1") int page, @RequestParam(value = "sort", defaultValue = "asc") String sort) { return userService.getUsers(page, sort); }``|

>In summary, @PathVariable is used to capture dynamic values from the URL path, typically identifying specific resources, while @RequestParam is used to capture query parameters from the URL, typically used for additional filters or options.




## Relevance

Relevance is the capacity of the financial information to influence the decision of its users. The ingredients of relevance are the predictive value and confirmatory value. Materiality is a sub-quality of relevance.

> The ingredients of relevance are the predictive value and confirmatory value.

Information is considered material if its omission or misstatement could influence the economic decisions of users taken on the basis of the financial statements.

## Faithful Representation

Faithful representation means that the actual effects of the transactions shall be properly accounted for and reported in the financial statements. The words and numbers must match what really happened in the transaction. The ingredients of faithful representation are completeness, neutrality and free from error.

## Enhancing Qualitative Characteristics

### Verifiability

Verifiability implies consensus between the different knowledgeable and independent users of financial information. Such information must be supported by sufficient evidence to follow the principle of objectivity.

### Comparability

Comparability is the uniform application of accounting methods across entities in the same industry. The principle of consistency is under comparability. Consistency is the uniform application of accounting across points in time within an entity.

### Understandability

Understandability means that accounting reports should be expressed as clearly as possible and should be understood by those to whom the information is relevant.
Timeliness: Timeliness implies that financial information must be presented to the users before a decision is to be made.

---

## Statement of cash flows

The statement of cash flows considers the inputs and outputs in concrete cash within a stated period. The general template of a cash flow statement is as follows: Cash Inflow - Cash Outflow + Opening Balance = Closing Balance

| Cash Inflow | Outflow   | Opening Balance |
| ----------- | --------- | --------------- |
| _Monday_    | `Tuesday` | **Wednesday**   |
| 1           | 2         | 3               |

**Example 1:** in the beginning of September, Ellen started out with $5 in her bank account. During that same month, Ellen borrowed $20 from Tom. At the end of the month, Ellen bought a pair of shoes for $7. Ellen's cash flow statement for the month of September looks like this:

- Cash inflow: $20
- Cash outflow:$7
- Opening balance: $5
- Closing balance: $20 – $7 + $5 = $18

**Example 2:** in the beginning of June, WikiTables, a company that buys and resells tables, sold 2 tables. They'd originally bought the tables for $25 each, and sold them at a price of $50 per table. The first table was paid out in cash however the second one was bought in credit terms. WikiTables' cash flow statement for the month of June looks like this:

> **Important:** the cash flow statement only considers the exchange of actual cash, and ignores what the person in question owes or is owed.

## Statement of financial position (balance sheet)

The balance sheet is the financial statement showing a firm's assets, liabilities and equity (capital) at a set point in time, usually the end of the fiscal year reported on the accompanying income statement.

- **fixed assets**
  - property
  - building
  - equipment (such as factory machinery)
- **intangible assets**
  - copyrights
  - trademarks
  - patents
    - pending
    - international
- goodwill

Owner's equity, sometimes referred to as net assets, is represented differently depending on the type of business ownership. Business ownership can be in the form of a sole proprietorship, partnership, or a corporation. For a corporation, the owner's equity portion usually shows common stock, and retained earnings (earnings kept in the company). Retained earnings come from the retained earnings statement, prepared prior to the balance sheet.
