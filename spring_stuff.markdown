Spring Boot
===========
* Spring Boot is a utility framework to bootstrap Spring based applications quickly and easily
* Increases development speed and provides a set of production ready ops features like health checks and metric collection.
* Spring Boot recognizes the nature of application based on the libraries present in the class path and runs the autoconfiguration classes packaged with those libraries
* Spring Boot enables Microservices development by packaging all the required runtime dependencies in a fat executable jar file.
* Whatever the language the program is written in it can be executed using *`spark run filename.language`*
  + No **war** file created and no Tomcat server was run. Spring Boot automatically picked up Tomcat as the webserver and embedded it into the application
* SPRING BOOT STARTER PARENT : Its a pattern called Bill Of Materials (BOM) used by Maven's dependency management (SBSP is specified in the pom file)
  + BOM is a spl kind of POM that manages different library versions required for a project
  + SBSP takes care of the compatible versions of different libraries and developers don't have to do that
* It can be run from Eclipse or can also be run from command line as follows
  + mvn clean && mvn install
  + java -jar target/jarFilename.jar
  + That jar file will have everything needed to run it
* SPRING INITIALIZR : Can create the project from the browser and can be imported into an IDE. Available at https://start.spring.io/
* A Separate Microservice to monitor and baby sit the configuration of the existing Microservices is good (CONFIG SERVER)
* Spring Framework
  + A Container of Beans (Objects)
  + Uses Factory Pattern
  + Factory Object (Object Factory) creates the required objects by reading from the XML blueprint and passes it to the appropriate object
    - BeanFactory
    - ApplicationContext : The xml file need to be in the class path
  + Auto Wiring : Helps to reduce the manual config we need to do by intelligently guessing the references for beans
    - byName      : Automatically references beans with id's same as some variable name
    - byType      : Auto wiring with the type of the bean. Works if there is only one bean of a particular and only one variable of that type in the class
    - constructor : similar to byType but does a constructor injection rather than a Setter injection
  + Scopes :
    - Singleton : By default all beans are in Singleton scope. Creates **only one** object and keeps passing that for every getBean() call. Creates all bean during initialisation (different from Java Singleton pattern because its possible multiple Spring containers exist and each of them might have this bean too)
    - Prototype : New bean crated for every request or reference. Creates beans only when they are requested
    - Web-aware Scopes : Request scope, Session scope, Global session scope
  + Aware Beans:
    - ApplicationContextAware
    - BeanNameAware etc
  + Bean Life cycle Methods : Method that can be called at init and destruction of beans. Not really recommended because the beans become Spring specific. Use your own POJO to do this
    - For triggering something during a bean's destruction, the context should register the shutdown using `context.registerShutdownHook()`
    - Methods in Springs methods take priority over the user methods
  + Bean post processor : Similar to above but can be used to run methods not present in the corresponding class. No destroy methods here. One for use during initialisation
    - Needs a class that implements the `BeanPostProcessor` which would contain the method to run
    - Also that class needs to be registered in xml file to make sure Spring knows about this
    - PreferencesPlaceholderConfigurer : Out of the box post processor from Spring
  + Even Handler : Another benefit because of using Application Context
    - Event Listener : Needs to implement `ApplicationListener` interface and implement the `onApplicationEvent` method

Annotations
===========
* @SpringBootAplication      : Top level annotation that encapsulates three other annotations
  + @Configuration           : Hints that the contained class declares one or mean *@Bean* definitions
  + @EnableAutoConfiguration : Tells Spring Boot to automatically configure the Spring Application based on dependencies in the class path
  + @ComponentScan
* @WebIntegrationTest        : Ensures that the tests are fired against a fully up and running server.
* @RestController            : Indicates that a class has REST endpoints declared
* @RequestMapping            : Indicates a REST Endpoint which can be typed in the browser to get a resource
* @ResponseBody              : Indicates that some Entity is being returned from the resource. Usually some html will be displayed in the browser
* @ActiveProfiles            : Used to specify the configuration profile to be sued for a particular test case
* @EnableGlobalMethodSecurity
* @EnableConfigServer        : Baby sitter Microservice
* @EnableDiscoveryClient
* @AutoWired                 : Does auto wiring
  + Needs `AutowiredAnnotationBeanPostProcessor` added in xml because that checks for autowiring stuff
* @Required                  : Indicates to Spring that a particular variable needs to be initialized. Put this on the setter for that variable
  + Needs `RequiredAnnotationBeanPostProcessor` added in xml because that class checks for the required dependencies
* @Resource                  : Does dependency Injection just by using the name
* @PostConstruct             : Calls a function after a bean has been created - Initialization Method
* @PreDestroy                : Calls a function before a bean has been destroyed - Destruction Method
* @Component                 : Defines a class as a bean and so we don't have to declare it in Spring.xml. Can't be used to create multiple beans
  + Needs `component-scan` context added in the xml file
* @Controller
* @Service

Configuration Stuff
===================
* Download STS from spring website.
* Set proxy in eclipse *network settings*. Refer to D:\\Work_Files\\InnovationTeam\\Spark\\spark_stuff.markdown
  + Set password for both http and https as *welcome1*
* `application.properties` file is in *src/main/resources*. Important file to configure any required properties for the Spring boot application
* Spring boot, for each `spring-boot-starter-*` dependency in the pom file, executes a default `AutoConfiguration` class. For each repository there is a separate class.
  + For JPA repo's there is JpaRespositoriesAutoConfiguration
  + For JMS repo's there is JmsAutoConfiguration ... Etc.
  + Its possible to exclude some classes too as `@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})`
* When some settings are added in `Application.properties` file, we need to use _@AutoWired_ and then call the property using an `Environment` variable. So,
  + System.out.println(env.getProperty("bootrest.customproperty"))
  + env is an Environment object created as `Environment env`
* Default Http listeners can be customized/changed from the pom.xml file using <exclusions> in <dependecy> to exclude something and then add something else.

Definitions & Terms
===================
* Actuator End Points : Endpoints exposed via REST, JMX or others that give you the ability to see what the system is doing and ask questions on the system.
* Eureka : Netflix's Service Registry
* ApplicationEvent : Base event class provided by Spring for creating custom events
* ApplicationEventPublisher : To publish the created events
  + Needs the class to implement `ApplicationEventPublisherAware` interface
* Aspected Oriented Programming (AOP)

Testing
=======
* For testing JUnit is used and Assert statements are used to check if the expected value is same as the value returned

Password : base64 encode your clientid:clientsecret and then pass it in url as localhost:8080/oauth/token/<string>
