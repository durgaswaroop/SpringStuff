Spring Boot
===========
* Spring Boot is a utility framework to bootstrap Spring based applications quickly and easily
* Increases development speed and provides a set of production ready ops features like health checks and metric collection. 
* Spring Boot recognizes the nature of application based on the libraries present in the class path and runs the autoconfiguration classes packaged with those libraries
* Spring Boot enables Microservices development by packaging all the required runtime dependencies in a fat executable jar file.
* Whatever the language the program is written in it can be executed using *`spark run filename.language`*
  - No **war** file created and no Tomcat server was run. Spring Boot automatically picked up Tomcat as the webserver and embedded it into the application
* SPRING BOOT STARTER PARENT : Its a pattern called Bill Of Materials (BOM) used by Maven's dependency management (SBSP is specified in the pom file)
  - BOM is a spl kind of POM that manages different library versions required for a project
  - SBSP takes care of the compatible versions of different libraries and developers don't have to do that
* It can be run from Eclipse or can also be run from command line as follows
  - mvn clean && mvn install
  - java -jar target/jarFilename.jar
  - That jar file will have everything needed to run it
* SPRING INITIALIZR : Can create the project from the browser and can be imported into an IDE. Available at https://start.spring.io/
* A Separate Microservice to monitor and baby sit the configuration of the existing Microservices is good (CONFIG SERVER)

Annotations
===========
* @SpringBootAplication      : Top level annotation that encapsulates three other annotations
  - @Configuration           : Hints that the contained class declares one or mean *@Bean* definitions
  - @EnableAutoConfiguration : Tells Spring Boot to automatically configure the Spring Application based on dependencies in the class path
  - @ComponentScan
* @WebIntegrationTest        : Ensures that the tests are fired against a fully up and running server.
* @RestController            : Indicates that a class has REST endpoints declared
* @RequestMapping            : Indicates a REST Endpoint which can be typed in the browser to get a resource
* @ResponseBody              : Indicates that some Entity is being returned from the resource. Usually some html will be displayed in the browser
* @AutoWired
* @ActiveProfiles            : Used to specify the configuration profile to be sued for a particular test case
* @EnableGlobalMethodSecurity
* @EnableConfigServer        : Baby sitter Microservice
* @EnableDiscoveryClient

Configuration Stuff
===================
* Download STS from spring website.
* Set proxy in eclipse *network settings*. Refer to D:\\Work_Files\\InnovationTeam\\Spark\\spark_stuff.text
  - Set password for both http and https as *welcome1*
* `application.properties` file is in *src/main/resources*. Important file to configure any required properties for the Spring boot application
* Spring boot, for each `spring-boot-starter-*` dependency in the pom file, executes a default `AutoConfiguration` class. For each repository there is a separate class. 
  - For JPA repo's there is JpaRespositoriesAutoConfiguration
  - For JMS repo's there is JmsAutoConfiguration ... Etc.
  - Its possible to exclude some classes too as `@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})`
* When some settings are added in `Application.properties` file, we need to use _@AutoWired_ and then call the property using an `Environment` variable. So,
  - System.out.println(env.getProperty("bootrest.customproperty"))
  - env is an Environment object created as `Environment env`
* Default Http listeners can be customized/changed from the pom.xml file using <exclusions> in <dependecy> to exclude something and then add something else.

Definitions
===========
* Actuator End Points : Endpoints exposed via REST, JMX or others that give you the ability to see what the system is doing and ask questions on the system. 
* Eureka : Netflix's Service Registry

Testing
=======
* For testing JUnit is used and Assert statements are used to check if the expected value is same as the value returned
 
Password : base64 encode your clientid:clientsecret and then pass it in url as localhost:808/oauth/token/<string>
