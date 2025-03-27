### **Method Declarations in Java**  
A **method declaration** in Java defines a function within a class, specifying its return type, name, parameters, and visibility. Methods encapsulate reusable behavior and are a fundamental part of object-oriented programming. A method declaration consists of the following components:  

```java
public int add(int a, int b)
{
    return a + b;
}
```  
The first line is the method's signatue, how it will be identified when it is called.
In this example:  
- `public` is the **visibility modifier**, determining who can access the method.  
- `int` is the **return type**, specifying that the method returns an integer.  
- `add` is the **method name**.  
- `(int a, int b)` are the **parameters**, defining inputs the method expects.
  
  After the signature comes the metho's body, where the actual operation is defined.
  
 `{ return a + b; }` is the **method body**, containing the actual logic.  

Java methods must be declared inside a class and cannot exist independently.  


### **Method Signatures**  
A **method signature** uniquely identifies a method within a class. It consists of the **method name** and **parameter list** (number, order, and types of parameters). The return type and visibility modifiers are **not** part of the method signature.  

For example, the following two methods have different signatures:  

```java
public void printMessage(String message) { ... }
public void printMessage(int count) { ... }
```  

Even though they have the same name (`printMessage`), they have different parameter lists, making them distinct methods. Java allows multiple methods with the same name as long as their signatures are unique, which enables **method overloading**.  


### **Parameter Passing to a Method in Java**  

In Java, methods can accept parameters to process input data dynamically. Java follows **pass-by-value**, meaning a copy of the argument's value is passed to the method, rather than the actual reference (except for objects, where the reference itself is copied).  

#### **Passing Primitive Data Types**  
When passing primitive types like `int`, `double`, or `char`, Java copies their values into the method parameters. Any modifications inside the method do not affect the original variable.  

```java
public class Example
{
    public static void modifyValue(int num)
    {
        num = num * 2;  // Modifies the local copy
    }

    public static void main(String[] args)
    {
        int x = 10;
        modifyValue(x);
        System.out.println(x);  // Output: 10 (unchanged)
    }
}
```  

Here, `num` is a separate copy, so changes inside `modifyValue()` do not affect `x`.  

#### **Passing Objects (Reference Types)**  
When an object is passed as a parameter, Java still follows **pass-by-value**, but the **reference** (memory address) is copied, not the object itself. This means modifications to the object's fields **affect the original object**.  

```java
class Person
{
    String name;
}

public class Example
{
    public static void changeName(Person p)
    {
        p.name = "Alice";  // Modifies the original object
    }

    public static void main(String[] args)
    {
        Person person = new Person();
        person.name = "John";

        changeName(person);
        System.out.println(person.name);  // Output: Alice
    }
}
```  

However, if a method **reassigns** the reference to a new object, the original reference remains unchanged outside the method.  

```java
public static void changeReference(Person p)
{
    p = new Person();  // New object assigned (original object unaffected)
    p.name = "Bob";
}
```  



### **Returning Values from a Method**  

Methods in Java can return values using the `return` statement. The return type is specified in the method signature.  

#### **Returning Primitive Types**  
A method can return primitive values like `int`, `double`, or `boolean`:  

```java
public int square(int num)
{
    return num * num;
}
```  

This can be used as follows:  

```java
int result = square(5);  // result = 25
```  

#### **Returning Objects**  
Methods can also return objects, allowing for more complex data processing.  

```java
public Person createPerson(String name)
{
    Person p = new Person();
    p.name = name;
    return p;
}
```  

#### **Returning Multiple Values**  
Since Java does not support returning multiple values directly, developers typically return an object, an array, or a collection:  

```java
public int[] getCoordinates()
{
    return new int[]{10, 20};
}
```  

Returning values allows methods to process data and pass results back to the caller, promoting modular and reusable code.
### **Method Overloading**  
**Method overloading** allows multiple methods with the same name but different parameter lists in a class. This enhances readability and usability by providing multiple ways to call a method with different arguments.  

For example:  

```java
class MathsUtils
{
    public int multiply(int a, int b)
    {
        return a * b;
    }

    public double multiply(double a, double b)
    { // Overloaded method
        return a * b;
    }
}
```  

The compiler determines which method to invoke based on the method signature. Overloading improves flexibility and code organization, reducing redundancy.  



### **The "this" Reference**  
The **`this` keyword** in Java is a reference to the current object. It is used to distinguish between instance variables and parameters with the same name, invoke constructors within the same class, and return the current object from a method.  

Example of using `this` to resolve variable shadowing:  

```java
class Person
{
    private String name;

    public Person(String name)
    {
        this.name = name; // "this.name" refers to the instance variable
    }
}
```  

`this` is also used to call another constructor within the same class:  

```java
public class Car
{
    private String model;
    private int year;

    public Car(String model)
    {
        this(model, 2024); // Calls the other constructor
    }

    public Car(String model, int year)
    {
        this.model = model;
        this.year = year;
    }
}
```  

Using `this` improves code clarity and prevents ambiguity.  

The `this` object is particularly useful when using a debugger. Execution is always inside one and only one object (or class if static) at any given instant of time. So when you see the stripe showing where execution is it is inside `this` object and the debugger will show you what `this` object is. Anything declared as `private` (see below) is not accessible unless it is in `this` object (i.e. where execution currently is).

### **Visibility Modifiers (Public and Private)**  
Java provides **visibility modifiers** to control access to classes, methods, and variables. The two most commonly used are:  

- **`public`**: The method or variable is accessible from anywhere in the program.  
- **`private`**: The method or variable is accessible only within the same class.  

Example:  

```java
class BankAccount
{
    private double balance; // Only accessible within this class

    public void deposit(double amount)
    { // Accessible anywhere
        balance += amount;
    }
}
```  

Encapsulation relies on visibility modifiers to **restrict direct access** to data, improving security and maintainability.  



### **Setters and Getters**  
**Setters and getters** are methods used to access and modify private fields while maintaining control over data. A **getter** retrieves a value, while a **setter** updates it.  

Example:  

```java
class Person
{
    private String name;

    public String getName()
    { // Getter
        return name;
    }

    public void setName(String name)
    { // Setter
        this.name = name;
    }
}
```  

By using setters and getters, developers can enforce validation and maintain encapsulation while still allowing controlled access to private data.


### **Variable Scope in Java**  

**Variable scope** in Java determines where a variable can be accessed within a program. There are three main types of variable scope:  

1. **Local Scope:** Variables declared inside a method or block `{}` are local variables. They exist only within that method and cannot be accessed outside it.  
   ```java
   public void printMessage()
   {
       String message = "Hello!"; // Local variable
       System.out.println(message);
   }
   // 'message' is not accessible outside the method
   ```  

2. **Instance Scope:** Instance variables are declared inside a class but outside methods. They belong to an instance of the class and are accessible by all methods in that class.  
   ```java
   class Person
   {
       String name; // Instance variable
   }
   ```  

3. **Class (Static) Scope:** Static variables belong to the class itself rather than individual objects. They are shared across all instances of the class.  
   ```java
   class Counter
   {
       static int count = 0; // Class-level variable
   }
   ```  

Understanding scope ensures proper variable access and memory management, preventing unintended modifications and reducing errors.  



### **Constructors in Java**  

A **constructor** is a special method used to initialize objects when they are created. It has the same name as the class and does not have a return type. Constructors are automatically called when an object is instantiated.  

#### **Default Constructor**  
If no constructor is provided, Java supplies a default constructor:  
```java
class Person
{
    String name;
    
    // Default constructor
    public Person()
    {
        name = "Unknown";
    }
}
```  

#### **Parameterized Constructor**  
A constructor can accept parameters to initialize object properties:  
```java
class Person
{
    String name;
    
    // Parameterized constructor
    public Person(String name)
    {
        this.name = name;
    }
}
```  

#### **Constructor Overloading**  
Java supports multiple constructors with different parameter lists:  
```java
class Car
{
    String model;
    int year;
    
    public Car(String model)
    { // Overloaded constructor
        this(model, 2024);
    }
    
    public Car(String model, int year)
    {
        this.model = model;
        this.year = year;
    }
}
```  

Constructors ensure objects are properly initialized, improving code readability and reducing the risk of uninitialized variables.
