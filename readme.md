

# Q1: How to that user-sensitive information such as usernames and passwords are sent to the correct website and to maintain a secure environment?

A:  implement several measures on both the backend and frontend sides:
- **SSL/TLS Encryption:**<br><br>
  Use SSL/TLS certificates to enable HTTPS on your website. This ensures that the data transmitted between the user's browser and your server is encrypted, making it difficult for attackers to intercept or tamper with the sensitive information in transit.
- **Use Secure Protocols:**<br><br>
  Employ secure and updated communication protocols like TLS 1.2 or higher and avoid outdated or insecure protocols like SSL.
- **Domain Validation and Certificates:**<br><br>
  Ensure the domain validation of your website and use valid SSL/TLS certificates issued by trusted Certificate Authorities (CAs). This helps users trust that they are submitting their data to a legitimate site.
- **CSRF Protection:**
  Implement Cross-Site Request Forgery (CSRF) protection on your website to prevent unauthorized requests from being made on behalf of users. 
Use CSRF tokens to ensure that requests originate from your frontend and not from malicious sources.
- **Secure Cookies:**
  Set the Secure and HttpOnly flags on your cookies. The Secure flag ensures that cookies are transmitted only over HTTPS, while the HttpOnly
flag prevents client-side scripts from accessing the cookies, reducing the risk of XSS attacks.


## Q2:  which framework/go lang you worked with?
###Frameworks:

- **Gin:** Gin is a web framework written in Go (Golang). It is lightweight and fast, and it's designed for building web applications and RESTful APIs. It provides a router and various middleware to simplify development.
Chi/Mux: Chi and Mux are two separate Go router packages that can be used to build web applications and APIs. Chi is known for its simplicity and high performance, while Mux is part of the standard Go library and provides a more basic routing mechanism.
ORM (Object-Relational Mapping):

- **Gorm:** Gorm is a popular ORM library for Go. It provides a convenient way to interact with databases, allowing you to define models as Go structs and perform CRUD (Create, Read, Update, Delete) operations on the database.

- **Entgo:** Entgo is another ORM library for Go that focuses on code generation and type safety. It allows you to generate type-safe APIs for your database models and queries.

###CLI (Command-Line Interface) and Configuration:

- **Cobra:** Cobra is a powerful library for building command-line applications in Go. It provides a simple interface for defining and handling commands, flags, and arguments, making it easy to create robust CLI applications.

- **Viper:** Viper is a configuration management library for Go. It supports various configuration formats like JSON, YAML, TOML, and more. Viper allows you to load and access configuration values easily in your applications.

### Testing:

- **Gocheck:** Gocheck is a popular testing framework for Go. It provides a set of useful functions and patterns for writing test suites and assertions in your Go tests.

## Q3: What is a Circuit Breaker pattern, and what problem does it solve and how does a Circuit Breaker prevent cascading failures in a distributed system?
### Definition:
The Circuit Breaker pattern is a design pattern used in distributed systems to manage and handle failures gracefully. It is primarily used to improve the resilience and fault-tolerance of the system by preventing cascading failures and reducing the impact of failing components.

### Problem it Solves:
In distributed systems,
services often depend on each other to complete requests. 
service becomes slow /unresonsive ->  other services waiting for a respons
e can start queuing up and consuming resources  ===> resource exhaustion and a complete system failure ( cascading failure). 
-Providing a mechanism to detect and handle failures in a controlled manner.

### How it Works:
Works by introducing a state mechanism into the interaction between services
&Monitors the state of the service & it is protecting and takes actions based on that state.
The Circuit Breaker can be in one of three states: Closed, Open, or Half-Open.

#### 3 states:

- Closed State:
Circuit Breaker allows requests to pass through as usual.Monitors the number of failures
(e.g., timeouts, errors) that occur within a predefined window of time.

- Open State:
If the number of failures exceeds a threshold within the time, the Circuit Breaker 
**trips into the Open state. In this state, prevents any further requests from reaching the problematic service**.
=> returns a predefined fallback response or throws an exception, **depending on the implementation**.

- Half-Open State:
After a certain period of time, the Circuit Breaker transitions 
to the Half-Open state. In this state, 
the Circuit Breaker allows a limited number of requests to pass through to the service 
to test its health. If succeed -> resets to the `Closed state` -> (maybe) the service has recovered. `If not ? ---yes-->` it goes back to the Open state,
knowing the service is still experiencing issues.


## Q4: In complex systems, how would you implement hierarchical Circuit Breakers to handle dependencies between microservices or subsystems?

Strategies:
 - Implement Circuit Breaker for Each Microservice: -> monitor the health and failures of each service independently.
 - Parent Circuit Breaker (Aggregate Circuit Breaker): Aggregate Circuit Breaker(higher-level or parent Circuit Breaker) ----responsible--->  managing and coordinating the Circuit Breakers of all dependent microservices.
 - Decide Aggregate Circuit Breaker Behavior:  behavior based on the status of its dependent io: ` if a certain percentage of the dependent Circuit Breakers are open, the Aggregate Circuit Breaker might decide to open as well.`
 - Fail Fast Strategy: -> avoid cascading failures. Aggregate Circuit Breaker is open? ---yes---> quickly fail requests to the entire system instead of ~~attempting to make calls to dependent services~~.

    


