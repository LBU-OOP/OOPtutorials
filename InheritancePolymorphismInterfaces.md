# Inheritance, Polymorphism and Interfaces

Object-Oriented Programming (OOP) is a fundamental paradigm in Java that organizes software design around objects, encapsulating data and behaviour. Key concepts in OOP include **inheritance**, **polymorphism**, and **interfaces**. This tutorial introduces these concepts to novice programmers using two GitHub projects: [InheritanceExample](https://github.com/LBU-OOP/InheritanceExample) and [OOPShapesInheritanceExample](https://github.com/LBU-OOP/OOPShapesInhertianceExample).

## Inheritance
Inheritance is a major tool is the arsenal of a Software Engineer. It allows us to take code that pre-exists and without having to understand or even look at the actual code, use it, add functionality to it and change the existing functionality of it. All we need to know is what it does and how to make it do it. Interfaces allow the original designer to specify rules that anyone inheriting the classes has to comply with. This is in line with the OO concept of Encapsulation.

Inheritance allows a new class (subclass) to acquire properties and behaviours from an existing class (superclass), promoting code reusability and establishing a hierarchical relationship between classes.

### Example from InheritanceExample

The `InheritanceExample` project demonstrates inheritance through a simple shape hierarchy.

**Shape.java**


```java
public class Shape
{
    protected int x, y;

    public Shape(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    public void draw()
    {
        System.out.println("Drawing Shape at (" + x + ", " + y + ")");
    }
}
```


The `Shape` class defines common properties `x` and `y` for positioning and a `draw` method to simulate drawing the shape. I say "simulate" because we can't actually draw a "Shape", it's too abstract, we need to get into more detail about this shortly.

**Rectangle.java**


```java
public class Rectangle extends Shape
{
    private int width, height;

    public Rectangle(int x, int y, int width, int height)
    {
        super(x, y);
        this.width = width;
        this.height = height;
    }

    @Override
    public void draw()
    {
        System.out.println("Drawing Rectangle at (" + x + ", " + y +
                           ") with width " + width + " and height " + height);
    }
}
```
Note the use of the @Override. This is a Java thing. Anything starting with an @ is not actually part of Java, it is a Java Annotation and it tells the compiler that we are overriding the preexisting draw method in the Shape class. This is so it can do some additional checks. You don't actually have to put it, but it aids clarity. Annotations are also used to comment your code so the nice web site can be built from your comments.

The `Rectangle` class extends `Shape`, inheriting its properties and overriding the `draw` method to provide specific behaviour for rectangles. Here it can add the full information about the shape, so it could draw it now, but for simplicity we'll do that later.

**Square.java**


```java
public class Square extends Rectangle
{
    public Square(int x, int y, int side)
    {
        super(x, y, side, side);
    }

    @Override
    public void draw()
    {
        System.out.println("Drawing Square at (" + x + ", " + y +
                           ") with side " + width);
    }
}
```


The `Square` class extends `Rectangle`, using inheritance to set both width and height to the same value, and overrides the `draw` method for square-specific behaviour. Here it might have been more logical to do it the other way around (Rectangle inherits from Square) and that's probably how you'd learn about shapes in primary school, but here I have decided that it actually makes the code simpler to do it this way because I can call on the original functionality of Rectangle to draw a square. There is no right and wrong answer to this.

**Main.java**


```java
public class Main
{
    public static void main(String[] args)
    {
        Shape shape = new Shape(10, 20);
        shape.draw();

        Rectangle rectangle = new Rectangle(30, 40, 50, 60);
        rectangle.draw();

        Square square = new Square(70, 80, 90);
        square.draw();
    }
}
```


**Output:**


```
Drawing Shape at (10, 20)
Drawing Rectangle at (30, 40) with width 50 and height 60
Drawing Square at (70, 80) with side 90
```


Not very exciting admittedly.

## Polymorphism

Polymorphism allows objects to be treated as instances of their parent class, enabling us to write one chunk of code to handle everything, i.e.. we don't need separate data structures and loop processing code for Circles, Squares, Rectangle and Ellipses, we can have just one that handles Shapes.

**Main.java with Polymorphism**


```java
public class Main
{
    public static void main(String[] args)
    {
        Shape[] shapes = new Shape[3];
        shapes[0] = new Shape(10, 20);
        shapes[1] = new Rectangle(30, 40, 50, 60);
        shapes[2] = new Square(70, 80, 90);

        for (Shape shape : shapes)
        {
            shape.draw();
        }
    }
}
```


**Output:**


```
Drawing Shape at (10, 20)
Drawing Rectangle at (30, 40) with width 50 and height 60
Drawing Square at (70, 80) with side 90
```


By storing different shape objects in a `Shape` array and calling their `draw` methods, polymorphism allows each shape to be drawn correctly based on its actual type.
When we look at the code now, at development time, before it is running, where it does shape.draw() we don't actually know which draw() method it is calling. Is it the one in Shape, or Circle, or Rectangle etc?
We don't get to find out until run-time. Thi is called late-binding or run-time-binding. It is very powerful.
## Interfaces
I like to explain Interfaces as being like rules that the designer of a class can state must be adhered to before the class can be inherited (extended). Looking back at the example above. Imagine you wanted to add a triangle, but if you forgot to add a draw method. That's why I put a dummy draw method in Shape, because if I hadn't this would result in the code that has always worked (Main.Java) suddenly throwing a run-time exception. I have alleviated this by having it resorting to calling an incomplete method. This is still not great though as it doesn't remind us to add the extra functionality.
An interface in Java is a reference type that defines a set of abstract methods that a class must implement (abstract means they aren't complete, and the rule is that anyone inheriting must complete them), providing a way to achieve abstraction and multiple inheritance. Interfaces cannot contain instance fields or constructors. By implementing an interface, a class agrees to perform the specific behaviours defined by that interface. 
An example of an interface in everyday life is the interface to a manual car. It has steering, brake and accelerate. A car implements this interface and we know how to drive it, regardless whether it's carburettor, fuel injection or electric driven.
### Example from OOPShapesInheritanceExample

The `OOPShapesInheritanceExample` project demonstrates the use of interfaces alongside inheritance.

**Shapes.java**


```java
import java.awt.Color;
import java.awt.Graphics;
/**
 * 
 * @author Duncan Mullier
 * Shapes interface
 */
public interface Shapes 
{
	/**
	 * set setter for an instance, sets the colour of a shape and its properties 
	 * @param c colour of object
	 * @param list, can vary depending on object but take the form x,y, size, size
	 * 
	 */
	void set(Color c, int... list); //note params int[] list in c#
	
	/**
	 * draw renders the object on the graphics context passed
	 * @param g graphics context ion which to draw the object
	 */
    void draw(Graphics g);
    
    /**
     * Calculates the area of the shape
     * @return area
     */
    double calcArea();
    
    /**
     * calculates the perimeter of the shape
     * @return perimeter
     */
    double calcPerimeter();

}
```


The `Shapes` interface defines a contract for drawing shapes, specifying that any class implementing this interface must provide an implementation for the `draw` method. I've also added CalcArea() and CalcPerimeter().

**Shape.java**


```java
import java.awt.Color;
import java.awt.Graphics;

public abstract class Shape implements Shapes 
{
	protected Color colour; //shape's colour
    protected int x, y; //not I could use c# properties for this
    
    public Shape()
    {
        colour = Color.RED;
        x = y = 100;
    }
    public Shape(Color colour, int x, int y)
    {

        this.colour = colour; //shape's colour
        this.x = x; //its x pos
        this.y = y; //its y pos
        //can't provide anything else as "shape" is too general
    }
	
    public void set(Color c, int... list) 
    {
	 this.colour = c;
         this.x = list[0];
         this.y = list[1];
    }

    public String ToString()
    {
        return super.toString()+"    "+this.x+","+this.y+" : "; //note c# base instead of super and ToString()
    }
    public abstract void draw(Graphics g); 
	

    @Override
    public abstract double calcArea(); 

    @Override
    public abstract double calcPerimeter(); 

}
```

The `Shape` class implements the `Shapes` interface, committing to providing a `draw` method, which its subclasses must implement.
But Shape can't actually implement them here as it is, as stated above, too abstract. So it passes on the responsibility. It does this by declaring "abstract methods" for each method it can't implement. This passes the responsibility on to any inheriting classes, they must either implement them or pass the responsibility on. Any class that has abstract methods in it must itself be declared abstract. This makes it absolutely clear to an software engineer that an object of this class cannot be instantiated because it is abstract and therefore not complete (it is being used as a building block).


**Rectangle.java**


```java
import java.awt.Color;
import java.awt.Graphics;

public class Rectangle extends Shape
{
	 protected int width, height;

	 public Rectangle() {
		 super();
		 width = 100;
		 height = 100;
	 }

	 public Rectangle(Color colour, int x, int y, int width, int height)
	 {
	   	 super(colour, x, y);
	   	 this.width = width; //the only thing that is different from shape
	     this.height = height;
	 }

    public void set( Color colour, int... list)
	{
	     //list[0] is x, list[1] is y, list[2] is radius
	     super.set(colour, list[0], list[1]);
	     this.width = list[2];
	     this.height = list[3];
	}

    public void draw(Graphics g)
     {
         g.setColor(colour);
         g.fillRect(x, y, width, height);
         g.setColor(Color.BLACK);
         g.drawRect(x, y, width, height);
     }

   public double calcArea()
   {
   	 return width * height;
   }

   public double calcPerimeter()
   {
   	 return 2 * width + 2 * height;
   }

   public String ToString() //all classes inherit from object and ToString() is abstract in object
   {
        return super.ToString()+ "rectangle  "+this.width+","+this.width;
   }
}
```
Here Rectangle extends Shape and it can implement the abstract methods and actually do the drawing. 


The main class creates an [ArrayList](https://github.com/LBU-OOP/OOPtutorials/blob/main/ArraysAndArrayLists.md) and populates it with some shapes to draw a face. It iterates over the ArrayList and calls the draw() method of each Shape (whatever it is).
