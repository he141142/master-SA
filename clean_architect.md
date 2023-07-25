
# Clean architecture 
Clean Architecture. 
It is a design approach that promotes separation of
concerns and modularity in a codebase.
The Onion Architecture helps create loosely coupled 
and maintainable applications by organizing code into concentric layers,
each with a specific responsibility and level of abstraction.

Clean Architecture consists of the following layers, moving from the innermost to the outermost layers:

- Core Layer (Innermost Layer):
  + This layer contains the most fundamental and essential components of the application.
  + It includes domain entities, domain services, and interfaces for repositories or data access.
  + The core layer represents the business logic and contains the heart of the application's functionality.
  + *It should be independent of any external frameworks or technologies.*
- Infrastructure Layer (Outer Core Layer):
    + This layer contains implementations of the interfaces defined in the Core layer.
    + It provides concrete implementations for data access, external services, and other infrastructure-related concerns.
    + The infrastructure layer may include database access code, API clients, file system access, etc.
- Application Layer (Outer Layer):
    + The application layer serves as a mediator between the presentation layer (e.g., UI) and the core business logic.
    + It handles user interactions, orchestrates the flow of data, and calls the appropriate methods in the core layer.
    + The application layer is responsible for translating user input into actions that the core can process.
    + It also contain data validation and mapping logic.
- Presentation Layer (Outermost Layer):
  + The presentation layer communicates with the application layer to retrieve data and perform actions.


Summary:
Ennables the application's core business logic to remain independent and easily testable without being tied to any specific frameworks or external services. 
The outer layers act as adapters or interfaces that interact with the core business logic.
The key factor is inner layers do not depend on the outer layers.

Benefit : improves maintainability, testability, and flexibility of the codebase
allows for easier migration or replacement of components -> ease to swap out external dependencies without affecting the core logic
easy to brake down the monolithic architect to distributed architecture

explain:
lean Architecture emphasizes using interfaces and adapters to communicate between layers. When moving to a distributed system, you can use these same principles to define communication interfaces between different services,
making it easier to switch underlying communication mechanisms or protocols as needed.


#Solid Design
SOLID is an acronym that represents five fundamental principles of software design:
## S - Single Responsibility Principle (SRP):
  The Single Responsibility Principle states 
that a class should have only one reason to change,
which means it should have only one responsibility or job. 
This  promotes high cohesion, where each class is focused on a specific task 
, making the code easier to understand, test, and maintain.<br>
When a class has multiple responsibilities:
  + Changes in one area may inadvertently affect other unrelated areas
  + leading to code that is difficult to maintain and understand.
  
## O - Open/Closed Principle (OCP):
  software entities (classes, modules, functions)
should be open for extension but closed for modification. 
=> be able to add new functionality or behavior without modifying existing code.
  Usually achieved through the use of abstractions (interfaces or abstract classes) and polymorphism<br> <br>
**Benefit**: can add new features to a system without risking introducing bugs or breaking existing functionality.

## L - Liskov Substitution Principle (LSP):
States that objects of a superclass should be replaceable with objects of a 
subclass without affecting the correctness of the program.

. In other words, a subclass should be able to replace
the base class in any context without altering the desired behavior of the program


```text
For the Liskov Substitution Principle

I have example:

Example we programming A game 
I design a base calss called Item and  subclass is Weapon extend from Item
Both of them have method Consume()
but the item when consume ,it will substract the amount of usage while the weapon consume is not
So it will violate the Liskov Substitution Principle. Is it correct?
```
```text
Yes, you are correct. The example you provided violates the Liskov Substitution Principle (LSP) because the subclass Weapon behaves differently from its base class Item in terms of the Consume() method.

The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In other words, a subclass should adhere to the contract defined by its base class and should not change or extend the behavior in a way that breaks the expected behavior of the base class.

In your example, the Weapon subclass overrides the Consume() method but does not behave the same as the base class Item. This difference in behavior violates the LSP. If code that expects an Item object to be consumed in a certain way is passed a Weapon object instead, it may lead to unexpected results or errors since the behavior of Weapon deviates from the contract defined by Item.

To adhere to the Liskov Substitution Principle in this scenario, you have a few options:

Refactor the Class Hierarchy: If Weapon and Item have significant differences in behavior, consider refactoring the class hierarchy to avoid having Weapon inherit directly from Item. Perhaps, you can introduce a more specific base class for consumable items, and then have both Item and Weapon inherit from that new base class.

Extract Common Behavior: If possible, try to extract the common behavior between Item and Weapon into the base class, and make the Consume() method generic enough to handle both cases. If Weapon requires additional behavior beyond what Item provides, consider adding separate methods in Weapon without overriding the Consume() method.

Use Composition: Instead of using inheritance, consider using composition to share common functionality between Item and Weapon. This way, you can create separate classes for specific behaviors and then compose them as needed in both Item and Weapon.

Remember, adhering to the Liskov Substitution Principle ensures that your code is more maintainable, and objects can be substituted seamlessly, leading to a more robust and flexible design.
```
