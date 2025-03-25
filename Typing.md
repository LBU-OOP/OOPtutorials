### Static vs. Dynamic Typing in Programming Languages  

Typing in programming languages refers to how variables are assigned and checked for data types. 
The two main approaches to typing are **static typing** and **dynamic typing**, each with distinct characteristics and trade-offs.  

The reason why we allocate types in a programming language is because we are asking for storage space, a box to put something in, if you want to put a big thing in then you want a big box, but if you want to store only a small thin then it is a waste to use a big box. By box I mean memory. You may say, “well who care, there’s loads of memory”, but it isn’t just that. A processor can do billions of instructions per second, but one that access memory takes longer than one that does not. Some boxes are too big to bring onto the processor in a single grab, each grab takes time. It might not be much in one, but when it’s being done several million times per second then it makes a massive difference. So someone, or something, has to decide how small the box can be. In static typing we, the programmer decides, in dynamic typing it is the programming language that decides. Generally, if it is easier for us (takes us less time) then it is less efficient for the processor (takes more time to execute). Horses for courses.

#### **Static Typing**  
In statically typed languages, the data type of a variable is explicitly declared and checked at compile time. This means that once a variable is assigned a type, it cannot change to another type later in the program. Java, C, C++, and Swift are examples of statically typed languages.  

In Java, for instance, variables must be declared with a specific type before they are used:  

```java
int number = 10;   // number is explicitly declared as an integer
number = "Hello";  // Compilation error: Type mismatch
```  

The compiler enforces type safety, catching errors early before the program runs. This results in better performance and fewer runtime errors but can sometimes make the code more rigid, requiring explicit type conversions when necessary.  

#### **Dynamic Typing**  
Dynamically typed languages, such as Python, JavaScript, and Ruby, do not require explicit type declarations. Instead, the type is determined at runtime, 
allowing greater flexibility. This flexibility is at the expense of clarity, as it isn't explicit what type is being used. In software engineering we always err on the side of clarity.


```python
number = 10  # Initially an integer
number = "Hello"  # Now a string, no error
```  

Since variables can change types dynamically, dynamically typed languages enable rapid development and more flexible code. However, they may introduce runtime errors if type mismatches occur unexpectedly. This may be ok for smaller projects but it is not good in software engineering, where code might be used by many people over a long lifespan.

#### **Java and Static Typing**  
Java is a statically typed language, meaning type checking happens at compile time. However, Java introduced **type inference** in Java 10 with the `var` keyword:  

```java
var number = 10;  // Compiler infers that 'number' is an int
```  

Even with `var`, Java remains statically typed because the inferred type cannot change. This balances type safety with reduced verbosity.  

Overall, static typing in Java enhances reliability and performance, making it well-suited for large-scale applications, while dynamic typing in other languages offers more flexibility at the cost of potential runtime errors.
