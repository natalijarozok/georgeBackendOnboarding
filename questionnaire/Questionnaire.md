
## OOP
**1. What is the meaning of loose coupling?**

Coupling relates to usage of one class by another class. 
Loose coupling means that the object gets the object to be used from the outside (tight coupling means that the object creates by itself the object to be used).  
In case of loose coupling to objects (components) are not dependent on each other. Changes done in one object does not affect another object to change.<br/><br/>

**2. What is the meaning of high cohesion?**

Cohesion is a measure of how well class is designed and how strongly methods of class are related. Cohesion helps to check that class has a single purpose. It shows how focused the class is.
The more Single responsibility principle is kept - the more cohesive is class.<br/><br/>

**3. What Java constructs are necessary to support a loosely coupled design?**

- class instance variables with setters and getters
- class constructor
- class method with parameters
- interfaces
- abstract classes
- method overriding<br/><br/>

**4. How can cohesion be measured within a Java class?**

Class has high cohesion if it has a small number of instance variables and each method of a class uses at least one of instance variables. The more class methods are dependent on class variables the more cohesive is class.<br/><br/>

**5. What is Dependency Injection?**

When one class (client) needs to use functionality of another class (dependency) we say that class is dependent on another class.
Dependency injection is a technique that passes dependency to the client. Client delegates a process of dependency constructing to some external code (injector).<br/><br/>

**6. Do I need a Framework for Dependency Injection?**

No. Dependency injection can be implemented manually. But a framework can make implementation easier or even take all responsibility for implementation.<br/><br/>

**7. What types of Dependency Injection are there?**

There are 3 type of dependency injection:
- constructor injection  
Dependency is passed to class via constructor. Dependencies are declared as parameters of the constructor. Usually the main class can not work without dependencies.

- property injection  
Dependency is passed to class via property setter. Usually is used when class does not strictly require dependency (it is optional) and can work without it in some cases. Or when a dependency can be changed after class instantiation.
A property of a class can be setup with instance of dependency or not.

- method injection  
Dependency is passed to class via method. Is used when dependency is going to change very often. In this case it is better to inject it at the point of use (in the method). For example, when dependency is an interface and we want to pass different implementations to the class.<br/><br/>

**8. Where would you put an Interface: into the package of the consuming class, or into the package of the implementing class?**

Into the package of consuming class (for dependency injection).<br/><br/>

**9. What is the Onion Architecture (Hexagonal Architecture, Clean Architecture)?**

**Onion architecture** consists of several layers (with dependency on system complexity some layers can be omitted (for example facade))

- domain model layer(describe business objects)  
This is the central layer. All further layers are put around this layer. Database is an external storage or service here, it is not a real core. 

- repository layer (perform CRUD operations on domain model objects)
- service layer (uses repository layer to perform more complex logic)
- facade layer (can for example perform validation, conversion of input objects to DTO objects, call services and return result)
- controllers (entry point for service)

There should be no coupling between layers. Layers must be connected via interfaces. External dependencies like database, external services are introduced in external layers of system.

**Hexagonal architecture** contains 3 main parts
- user-side  
Responsible for communication with the application end-user. 

- business logic  
Contains code that implements application logic.

- server-side  
Contains code that communicates with infrastructure that is essential for application (database, filesystem, network connection, external services).

Business logic is isolated from application input/output.

**Clean architecture** means that the system is divided into independent (there is no coupling) layers. Layers are independent of databases, independent of third-party components. Principle of separation of concerns is strictly followed.<br/><br/>

**10. When would you decouple two classes by introducing an Interface? (Hint: Volatile vs. Stable Dependencies)**

In case of volatile dependency.

Volatile dependency leads to strong coupling within a dependent class as change in volatile components will lead to changes in dependent class. Decoupling can be done via introducing abstraction (interface) and injection of that abstraction to dependent class.

Stable dependency is dependency of stable components.
Volatile dependency is dependency of volatile components.

Every system uses (is dependent) on 2 types of components (classes): stable and volatile. 
Stable components are components that:
- already exists
- are not considered to be changed often (components have passed the test of time, all use cases when components can be changed already studied, identified and addressed)
- have deterministic return values
- if a new version is published then id does not break dependent system classes (cause compilation errors)   
Examples: standard Java APIs; high-level entities inside application domain; Graphql schema on which rely both FE and BE.

Volatile components are components that:
- are not yet implemented or implementation is in progress
- return non-deterministic values
- are dependent on runtime environment  
Examples: database connection and setup; filesystem configuration; network access; CSS style on frontend.
Such components do not allow to write stable unit tests as tests will be broken very often.<br/><br/>

## Refactoring
**1. Please, name some Code Smells and explain what Refactorings could be applied to get rid of them**

- classes, variables, method names are not meaningful  
Use clear, intention-revealing names, develop domain-specific language for naming.

- code formatting is not kept  
Agree and keep code formatting rules that are conventional in specific language.

- code is duplicated  
Keep functions as small as possible. Use pointer to functions, lambda-expressions, add additional abstraction layers.             

- there are many comments that substitute meaningful code, comments are redundant, misleading  
Avoid using comments at all by writing self-explanatory code. Make periodical code review.

- functions are too large  
Keep single-responsibility principle (do 1 logic thing).

- function has many parameters  
Make functions smaller. Make some function parameters a member variable of the current class or move the function under another class to call it on the instance of that class. That will be more clear.

- input variables are reassigned in function  
Make functions smaller or add additional data structures.

- classes are too large and single-responsibility principle is broken  
Split large classes into smaller ones so that each class is responsible for fewer things. Increase cohesion.

- classes coupling is high  
Use dependency-injection.

- classes reveal their logic  
Use encapsulation.

- error handling and other logic are mixed in 1 function  
Make functions smaller.

- error codes are returned from function  
Always throw exceptions instead of returning error codes. This will make calling code cleaner and will not break the Open/Closed principle as changing error code in 1 function will cause changes in all calling functions. 

- third-party code is not isolated in class  
Use dependency-injection, wrap third-party classes.

- dead code  
Make periodical code review or use tools detecting dead-code.<br/><br/>

## Automated Tests
**1. What are the properties of “good” Unit-Tests?**

- tests should be written before production code is written
- test code is clean (readable): kept small, Build-Operate-Check pattern is used
- domain-specific language is used for all tests
- one concept in the test is tested
- independence: tests are not dependent on each other
- runnable in any (production, testing, etc.) environment
- tests are fast.<br/><br/>

**2. What is a Stub?**

Stub in testing means a piece of code that stands in for an existing code or temporary substitute to-be-developed code. Usually stubs are used in testing during top-down integration to replace modules that are in development. Stubs return the same values as substituted code.<br/><br/>

**3. What is a Mock?**

Mock is a “fake” version of an existing class or service.
An object that is tested in unit tests can be dependent on other objects. To isolate behaviour of tested object mocks are used.<br/><br/>

## (Http-) API Design
**1. What are reasons to use APIs?**

API (Application Programming Interface) is a special kind of software that acts as an intermediary/gateway between different applications/services/OS. 
API makes it possible for one applications to use data and functionality from another applications in some standard way (described in API type technical specifications and API documentation). 
API is defined by specifying data exchnage protocol, data formats, other communication constraints (rules).<br/><br/>

**2. What is an alternative approach to APIs?**

In spite of there is a plenty amount of API types:  
- SOAP 
- REST API 
- GraphQL 
- XML/JSON RPC.  

There are still other ways to connect application counterparts:
- monolithic architecture of system (does not user any API and all functionality is available inside a large application (opposite approach is using microservices - that communicate via API))
- data exchange via files of different formats via SMTP/FTP/HTTP/TCP and other protocols (exchange can be automatic or manual via export/import)
- webhooks
- direct access to other systems (crazy but still it is a way of connection).<br/><br/>

**3. What are the constraints of REST?**

There are 6 constraints/rules that define REST (Representational State Transfer) architecture style:  
3.1. Uniform interface  
Means - there must be a standard/uniform way of how the client communicates with server: 
 - there is an API resource, resource has only 1 logical URI and client manipulates with a resource via that URI. All resources are manipulated in the same way (via resource URI)  
- each resource must have it’s representation (info about resource). The representation must contain all necessary information about the resource and the way the resource can be manipulated (updated, deleted, selected)  
- resources can contain Hypermedia (links to other resources).

3.2. Client-server architecture  
There are 2 parts in communication: Client that requests some resource, “knows” only URI of resource and does not care about how and where resource is stored and processed. And Server that servers incoming requests, holds resources, hides all internal logic. 
Client and Server are independent.

3.3. Stateless  
Server does not keep any information about previous client calls. There are no sessions/history on the server. Each client request should contain all necessary information for the server to process request correctly.

3.4. Cacheable  
Server resources can be declared cacheable. Every response from the server should include info about if a resource is cacheable or not. Cacheable responses reduce load on both client  and server sides.

3.5. Layered system architecture  
RESTful API may contain many service layers: proxy, load balancer, caching service, DB service, etc. But layers are transparent to clients.

3.6. Code on demand  
It is legal that API can provide some compiled code to Client (like Javascript code, Java applet, etc.).<br/><br/>

**4. What is Hypermedia?**

Hypermedia is an aspect of REST architecture. It means that resource representation contains not only information about resource but also links to related resources. 
Using hypermedia in RESTful api has some advantages:
- api is self-descriptive and even does not need additional documentation
- client and Server are more decoupled: Client does not need to hardcode or remember links to server resources (links can be processed dynamically).<br/><br/>

**5. What does a client need to know (minimal requirements) to call an API endpoint?**

Client should know the API base URL. 
If API uses HATEOAS (Hypermedia as the engine of application state) Base URI should be enough as Client can discover other resources and actions from hyperlinks.
If not - it is good to have some API documentation (link to Swagger).<br/><br/>

**6. What formats do you know to transmit data between client and server?**

JSON, YAML, XML - industry standards.  
In some cases just text with delimiters can be used.<br/><br/>

