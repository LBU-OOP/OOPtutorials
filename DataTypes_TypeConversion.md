### Data Types

Typing in programming languages refers to how variables are assigned and checked for data types. 
The two main approaches to typing are **static typing** and **dynamic typing**, each with distinct characteristics and trade-offs. 
### Static vs. Dynamic Typing in Programming Languages  
 
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

### **Data Type Conversion in Java**  

In Java, data type conversion occurs when a value of one type is assigned to another type. Java enforces strict type safety, requiring explicit or implicit conversions when transitioning between data types. These conversions can be categorized into **widening conversions** (automatic type promotion) and **narrowing conversions** (explicit casting).  

#### **Widening Conversions (Implicit Type Conversion)**  
Widening conversion occurs when a smaller data type is converted into a larger data type without any explicit action from the programmer. This process is **safe** because the larger type can accommodate all possible values of the smaller type without data loss. Java automatically performs widening conversions.  

For example, converting an `int` to a `long` happens automatically:  

```java
int num = 100;
long bigNum = num;  // Implicit widening conversion
System.out.println(bigNum);  // Output: 100
```  

Other common widening conversions include `byte → short → int → long → float → double`. Since no data is lost, these conversions do not require explicit casting.  

#### **Narrowing Conversions (Explicit Type Casting)**  
Narrowing conversion occurs when a larger data type is converted into a smaller data type. This process **requires explicit casting** because there is a risk of losing precision or truncating data.  

For example, converting a `double` to an `int` requires an explicit cast:  

```java
double pi = 3.14159;
int truncatedPi = (int) pi;  // Explicit narrowing conversion
System.out.println(truncatedPi);  // Output: 3
```  

Narrowing conversions may result in data loss if the target type cannot fully represent the original value. The following example shows precision loss when converting from `double` to `int`:  

```java
double value = 9.99;
int intValue = (int) value;  // Fractional part is lost
System.out.println(intValue);  // Output: 9
```  
#### Float and Double
In Java that there are two data types to represent real numbers. They are float and double. The names come from the method of representing real numbers in a computer, since we cannot represent a potentially infinite number (think PI or 1/3) in a finite amount of memory. The method of approximation used is called floating point, so we have float (which is accurate to about ten decimal places) and double (double precision floating point), which is accurate to a fairly astonishing twenty decimal places. Java defaults to double. This is because although ten decimal places is very, very accurate, it rapidly gets inaccurate when you start multiplying and dividing. So, it errs on the side of caution and defaults to double. The upshot is that if you have:

```Java
float price = 10.99;
```
You will get a syntax error, because the 10.99 is a double in Java's eyes (if programming languages have eyes and I'm saying they do) and this is a narrowing conversion, so you would have to use a cast, or tell it that the 10.99 is a float by putting an "f" after it.

```Java
double price = 10.99;
float price = 10.99f;
```

#### **Casting Between Primitive Types**  
Casting is required when performing a narrowing conversion, and it is done using parentheses:  

```java
long bigNumber = 100000L;
int smallerNumber = (int) bigNumber;  // Explicit cast from long to int
```  

Similarly, converting a `char` to an `int` follows the same principle:  

```java
char letter = 'A';
int asciiValue = (int) letter;  // Output: 65 (ASCII value of 'A')
```  

#### **Casting Between Object Types**  
Java also supports type conversion between objects in an **inheritance hierarchy**. Upcasting (converting a subclass to a superclass reference) happens implicitly, while downcasting (converting a superclass reference to a subclass) requires explicit casting:  

```java
class Animal { }
class Dog extends Animal { }

Animal animal = new Dog();  // Upcasting (implicit)
Dog dog = (Dog) animal;  // Downcasting (explicit)
```  

### **Conclusion**  
Understanding data type conversion in Java is essential for writing clear and efficient code. Widening conversions occur automatically and are risk-free, while narrowing conversions require explicit casting and can lead to data loss. Mastering these conversions ensures type safety and prevents unexpected runtime errors in Java programs.
