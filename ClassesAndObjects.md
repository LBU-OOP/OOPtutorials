### **Classes and Objects in Java**  

In Java, a **class** is a blueprint for creating objects. It defines the structure (fields) and behavior (methods) of an object. An **object** is an instance of a class, representing a real-world entity with state and behaviour.  

For example, consider a `Bicycle` class:  

```java
class Bicycle
{
    String model;
    int weight;

    void displayInfo()
    {
        System.out.println("Model: " + model + ", Weight: " + weight + "kg");
    }
}
```  

To create and use objects from this class:  

```java
public class Main
{
    public static void main(String[] args)
    {
        myBike = new Bicycle();  // Creating an object
        myBike.model = "SWorks SL7";
        myBike.weight = 8;
        myBike.displayInfo();  // outputs Model : Sworks SL7 Weight 8kg
    }
}
```  

Here, `myBike` is an object of the `Bicycle` class, storing specific data while using shared behavior.  



### **The Static Context in Java and Why to Avoid It**  

In Java, **static** members belong to the class rather than any specific instance. A static method or variable is shared across all instances of the class.  

For example:  

```java
class MathsUtils
{
    static int add(int a, int b)
    {
        return a + b;
    }
}
```  

Since `add()` is static, it can be called without creating an object:  

```java
int result = MathsUtils.add(5, 3);
```  

While static methods are useful, overusing them can lead to problems. Since they **do not operate on instance variables**, they break encapsulation and make code less flexible. If everything is static, we lose the benefits of **object-oriented programming (OOP)** like **inheritance, polymorphism, and encapsulation**.  

To avoid this, static methods should be used only for **utility functions** (like `Math.sqrt()`). Most methods should be **instance methods** to work with object-specific data.  

### **Understanding the Static Context in `public static void main()`**  

The `main` method in Java serves as the entry point of a program and is defined as:  

```java
public static void main(String[] args)
{
    // Program execution starts here
}
```  

The **`static`** keyword in `static void main()` means that the method belongs to the class rather than any instance of it. Because Java needs a starting point for execution **without requiring an object to be created**, `main` is declared as `static`.  



### **Drawbacks of the Static Context in `main()`**  

While `static` in `main()` is necessary, working within a **static context** has limitations:  

1. **No Access to Instance Variables Without an Object**  
   Since `static` methods belong to the class, they **cannot directly access instance variables** or instance methods.  

   ```java
   class Example
   {
       int x = 10; // Instance variable

       public static void main(String[] args)
       {
           System.out.println(x); // ❌ Compilation error
       }
   }
   ```  

   To access `x`, we need an object:  

   ```java
   public static void main(String[] args)
   {
       Example obj = new Example();
       System.out.println(obj.x); // ✅ Works
   }
   ```  

2. **No Object-Oriented Features Like Inheritance and Polymorphism**  
   Since `static` methods do not belong to instances, they cannot be overridden in subclasses in the usual way. This limits flexibility when designing extensible, object-oriented systems.  

3. **Encourages Procedural-Style Programming**  
   Excessive reliance on static methods makes the program more procedural rather than object-oriented, reducing encapsulation and maintainability.  

### **Best Practices**  
While `main()` must be static, it should only be used to initialize the program and delegate tasks to instance methods and objects. This keeps code **object-oriented** and scalable.  

Example of good practice:  

```java
public class Application
{
    public void start()
    {
        System.out.println("Application started.");
    }

    public static void main(String[] args).
    {
        Application app = new Application();
        app.start(); // Delegating work to an instance method
    }
}
```  
This is why you should get ut of the static context as soon as possible. You can do this by creating an object and calling a method inside it. Which is what is happening above.
The start() method is called straight after the object of Application is created and is not static, so when execution gets there we are in the clear and not in a static context.
However, it is clearer to just use a constructor, which is explained later, but is a method with the same name as the class but no return type (it can't return anything because it is already returning the object's reference). It is called after the "new" keyword.
It would look lke this.

```java
public class Application
{
    public Application()
    {
        System.out.println("Application started.");
    }

    public static void main(String[] args).
    {
        Application app = new Application(); //the constructor is called here
        
    }
}
```  
It's just that bit simpler.
By minimizing logic inside `main()` and avoiding excessive use of static methods, we maintain a more flexible and object-oriented design.

## Pre-Existing and Standard Classes
### **The `Scanner` Class – A Pre-Existing Java Class**  

Java provides many built-in classes, called the Standard Classes, such as `[Scanner](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)`, which allows user input. The `Scanner` class is part of `java.util` and is used to read input from the console, files, or other sources. [The Documentation for the standard classes is here.](https://docs.oracle.com/javase/8/docs/api/)

Example:  

```java
import java.util.Scanner;

public class UserInputExample
{
    public static void main(String[] args)
    {
        Scanner scanner = new Scanner(System.in);  // Creating a Scanner object
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();  // Reading user input
        System.out.println("Hello, " + name + "!");
        scanner.close();  // Closing the scanner
    }
}
```  

Here, `Scanner` is an example of a pre-existing Java class that simplifies input handling. It has methods like `nextInt()`, `nextDouble()`, and `nextLine()` to read different data types.  
### The String Class
String may seem like a primitive data type but it is actually a Class because it has lots of useful functionality associated with it, such as comparing strings alphabetically, splitting a string up, changing its case etc.
[See the documentation for String].(https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

### The Locale Class
Other Classes provide useful functionality that is required in so many applications it is incorporated into the standard Java Classes. 
The Locale Class provides functionality to deal with different locations in the world displaying numbers and currencies in different ways.
Locale locale = new Locale("en", "GB"); //make our locale Great Britain

```Java
NumberFormat numberFormat = NumberFormat.getInstance(locale);
NumberFormat currencyFormat = NumberFormat.getCurrencyInstance(locale);
String currency = currencyFormat.format(totalPrice);
System.out.println("Price is "+ currency); //display with pound sign
````
### The Integer Class
The [Integer class](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html) is a “Wrapper Class”, this means that it is a collection of utility methods associated with integers because the int type is not a class. It is special because methods inside it are “static”, which means they can be called without making an object of it.
```Java
        Scanner scanner = new Scanner(System.in);  // Creating a Scanner object
        System.out.print("Enter a value ");
        String numberString = scanner.nextLine();  // Reading user input as a String
        int value = Integer.parseInt(numberString); //convert it to a number
```

### The Random Class
The [Random class](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html), produces pseudo random numbers (pseudo because it is really hard to create a genuinely random number). We'd find this useful in a Dice Class, below.

## Designing Your Own Classes
We can also create our own classes. They are included as java files in our project. Generally, there are two types of classes. One is data-driven, the Time class is an example of this. It is a bit like a database record in that it is collecting several data items together into a single unit, here hours, minutes and seconds into a single Time. It then goes further than a database because it provided functionality to manipulate the data. The second type is a behaviour-driven class, the Dice is an example of this. It isn't representing data as such, but something that has a behaviour.

### **Example: A `Time` Class**  

A `Time` class can represent hours, minutes, and seconds while providing methods to manipulate time values. To use it it must be in a file called Time.java inside our project.

```java
class Time
{
    private int hours;
    private int minutes;
    private int seconds;

    public Time(int hours, int minutes, int seconds)
    {
        this.hours = hours;
        this.minutes = minutes;
        this.seconds = seconds;
    }

    public void displayTime()
    {
        System.out.printf("%02d:%02d:%02d\n", hours, minutes, seconds);
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Time currentTime = new Time(10, 30, 45);
        currentTime.displayTime();  // Output: 10:30:45
    }
}
```  
#### Visibility modifiers, public and private
This `Time` class uses **encapsulation** by making fields `private` and provides a constructor for initialization. 
As it stands this means that once a Time is created we couldn't change the value of the time. The technical term is it is "immutable" (can't change).
Strings are immutable, but you can change them by creating another one and attaching the reference to it. All of the methods inside string that appear to change the string actually just return a new string.
But Time is our class and we can do what we like. What we'd actually do is ensure in the constructor that hours, minutes and seconds are acceptable values with if statements.
We can also provide "setter and getter" methods that do the same thing but CAN be called after the object is created and hence can "mutate" it.
For clarity I'll only do one set for hours, but you'd do it for all members.

Inside the class and by convention after the constructor, you would put the following code:
```Java
  public void setHour(int hour) //setter for hour
  {
    if (hour >=0 && hour <=23)
      this.hour = hour;
  }

  public int hour() //getter method
  {
      return hour;
  }
```
Because hour is private no one can create an object of Time and set it's hour directly. They have to go through the setHour() method and it checks it's a sensible value. Because it's private no one can read it either, so we provide a corresponding getter method.
Most IDEs will produce skeleton methods for you at the click of the mouse, leaving you to fill in the logic.

To make our code more robust we would alter the constructor to (assuming I'd completed the setters for minute and second as well:

```Java
  public Time(int hour, int minute, int second)
  {
    setHour(hour);
    setMinute(minute);
    setSecond(second);
  }
```
What I could have done is put the same if statement in the constructor, but I've already written it and I don't want to repeat code, this way if there's a bug in it, there is only one and not two!

In reality we'd make our Time class more useful by adding functionality to add and subtract hours, minutes and seconds. Think about it, it is not so simple.

### **Example: A `Dice` Class**  
The Time class is rather like a data class, this example is a behaviour type class.
A `Dice` class models a dice that generates random numbers between 1 and 6.  

```java
import java.util.Random;

class Dice
{
    private Random random;

    public Dice()
    {
        random = new Random();
    }

    public int roll()
    {
        return random.nextInt(6) + 1;  // Generates a number between 1 and 6
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Dice dice = new Dice();
        System.out.println("Rolling the dice: " + dice.roll());
    }
}
```  
Notice that this class doesn't even define any instance data. All it does is provide a roll() method. When this calls it produces a new value and returns it. As it stands this class does not allow you to look at it again. To do that you would have to add an attribute to represent its value and and way of reading it (but ytou wuldn't provide a setter because that would be like picking up a dice and putting it down as a set face and you just don't do that with a dice). 

The `Dice` class uses the `Random` class from `java.util` to generate a random dice roll, demonstrating how we can combine built-in Java classes with our own custom classes. We don't need to set it or get it, we just need the behaviour method roll() which does both setting and getting.
