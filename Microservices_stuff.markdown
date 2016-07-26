Microservices
=============
* Data Exchange only through the API layer or messaging. SHOULD NOT access data stores across Microservices
* First Do It. Then Do It Right. Then Do It Better
* An architectural style to building IT systems as a set of business capabilities that are autonomous, self contained and loosely coupled

Service Characteristics
=======================
* Service Contract: For JSON/REST we can use JSON schema, WADL, Swagger and RAML
* Loose Coupling: MS are independent and loosely coupled. Message based endpoints provide higher levels of Decoupling
* Service Abstractions
* Service Reuse
* Statelessness
* Discoverable Services
* Interoperability
* Composeability

Requirements for MS Implementation
==================================
* Service Registry  \
* API Load Balancer |
* API Gateway       |-----> Generally recommended for MS
* Service Discovery |
* Security          |
* Configuration     /
* Eventing
* Messaging
* Logging
* Security
* Monitoring
* Scaling

Definitions
===========
* Service Registry - Will have a list of all the nodes and instances running. It has their IP, ports and other stuff.
* Load Balancer    - Routes the traffic to the less used node to keep pressure off the most used ones. Queries Service Registry to determine the best end point
* API Gateway      - Provides backend for each frontend
  - If there are N MS's required to build a response, it **asynchronously** calls them
  - Does Load balancing (uses Load balancer, I guess or does it on its own)
  - Aggregates the responses from many Microservices
* Service Discovery - Must resolve host,port,version of each MS.
  - Should not hard code IP's or port's because they can change quickly.
  - Approaches Include
    * Hierarchical namespaces
    * SRV DNS records - gives IP + Port
    * Instance tagging in the cloud
* Antifragility - Software systems are continuously challenged and they evolve through these challenges and get better
* Fail Fast Approach - Instead of building systems that never fail we should expect failure and try to look at the how quickly the system can recover if it fails. Focus on Mean Time To Recover (MTTR)
* Self Healing - Used in MS deployments where system automatically learns from failures and adjusts itself preventing future failures.
* Edge Services - They are of two types
  - Micro Proxy : Blindly forwards packets from outside to the services behind the Load balancer
  - API Gateway : Transforms the requests ton the services behind the Load balancer

Notes
=====
* The major theme of MS is their small foot print. So, the supported technologies should also be light and manageable. So, Jetty or Tomcat are better choices for MS compared to WebLogic or WebSphere.
* Since everything under the API's is abstracted, each MS can have its own internal implementation and architecture. So, once can be java and the other can be in Scala. One can use DB2 and the other can use Oracle as a database (Polyglot architecture - Each MS can have its own language implementation)
* Microservices have to be automated end-to-end. So, Automated builds, Automated Testing, Automated deployment and Elastic scaling.
  - Automated builds         : CI tools such as Jenkins, Travis CI
  - Automated Testing        : Selenium, Cucumber etc.
  - Automated Infrastructure Provisioning : Container tech like Docker + release management tools lie Chef or Puppet + Configuration management tools like Ansible
  - Automated Deployment : handled using tools like Spring Cloud, Kubernetes, Mesos and Marathon
* Circuit Breaker Pattern : A stateful watcher (Circuit breaker) takes care of the fall back measures to be done in case of a failure in another Microservice
  - Histrix (by Netflix) is a Circuit breaker


API Design Things
=================
* What functionality to expose?
* How to expose it?
* What is the best way to expose it?
* How to adjust it and improve?

Messaging Compatibility
=======================
* Communication b/w Microservices can be done using protocols such as HTTP, REST or messaging protocols such as JMS or AMQP(Advanced Message Queuing Protocol)
* Always design for backwards compatibility
* Assume any Microservice has two or more different versions running concurrently. So, backwards compatibility is possible easily.

API Modeling
============
## Steps in API Modeling
1. Identify Participants
2. Identify Activities
3. Break Into Steps
4. Create API Definitions
5. Validate Your API

## Tips For API Modeling
* Don't worry about the tools (for taking notes)
* Consistent process for documentation
* Document everything you learn. It doesn't count unless it is written

## Terms and definitions
* Idempotency - Clients making the same call should produce the same result - Applicable for messages

Things To Learn
===============
* Angular JS : To create presentation layers,client side JS MVC framework like Angular JS should be used. These client side frameworks are capable of invoking REST calls directly

