# Exceptions: Handling the Inevitable

## Introduction
In an ideal world, every line of code we write would execute perfectly every time. However, we don't like in a perfect universe. Real-world programs are messy: users type letters into number boxes, files you expect to open have been deleted, and network connections drop mid-transfer.

In older languages like C, programmers had to rely on **return codes**. A function would return a special value (like `-1` or `0`) to signal that something went wrong. This meant that after every single function call, you had to write an `if` statement to check if it worked. If you had five layers of methods, you had to manually "pass" that error code back up through all five layers. It was repetitive and cluttered and meant that code needed to exist to handle the error at every level, regardless of whether it needed to do anything with it.
Java uses a much more structured system called **Exception Handling**. Instead of a return code, Java uses an **Exception Object**. When an error occurs, this object is "thrown" and it automatically travels up the call stack until it finds a handler. This allows us to separate our "normal" logic from our "error" logic, making the code much cleaner and more reliable.

## What is an Exception?
An exception is an object that represents an error or an unexpected event that occurs while the program is running. When one occurs, the normal flow of the program is interrupted. 



Why bother with this?
* **Avoid Crashes:** Instead of the program simply disappearing, we can catch the error and keep going.
* **Feedback:** We can give the user a helpful message like "Please enter a valid number" instead of a cryptic system crash.
* **Recovery:** For certain problems, like a missing file, we can ask the user to pick a different file and try again.

## The Basic Structure: Try and Catch
To handle an exception, we use two main keywords: `try` and `catch`.
1.  **Try:** You put the "risky" code that might fail inside the `try` block.
2.  **Catch:** If an exception occurs, the code inside the `catch` block runs to handle the problem.

### Example: Division by Zero
In math, you can't divide by zero. In Java, doing so triggers an `ArithmeticException`.

```java
try
{
    int result = 10 / 0; // This will fail! 
} catch (ArithmeticException e)
{
    System.out.println("Cannot divide by zero"); // This handles it
}
```

### Example: Invalid User Input
If you ask for an integer but the user types "Hello", the `Scanner` will throw an `InputMismatchException`.

```java
try
{
    int age = input.nextInt(); // Risky input
} catch (InputMismatchException e)
{
    System.out.println("Please enter a valid number");
}
```

## Checked vs. Unchecked Exceptions
Java divides exceptions into two main categories. This is a key "Static Typing" philosophy: the compiler wants to know if you've planned for failure.
Note that C++ and C# do not have checked exceptions (and no throws keyword). The reason being that it stops the programmer just putting an empty catch block (even temporarily and then forgetting about it). I have sympathy with this view.

### 1. Checked Exceptions
These are checked at **compile-time**. Java refuses to compile your program unless you either handle them with a `try-catch` or "declare" them. These are usually things outside your control, like files (`FileNotFoundException`) or network issues.

### 2. Unchecked Exceptions (Runtime)
These occur at **runtime** and the compiler does not force you to handle them. These usually indicate **programming mistakes** (bugs). 
Consequently, you should never try and handle these exceptions. You should write normal code (ifs and bug fixes) to ensure they never occur.
* **NullPointerException:** Trying to use an object that hasn't been initialized.
* **ArrayIndexOutOfBoundsException:** Trying to access `marks[5]` when the array only has 5 elements (0-4).



## The `throws` Keyword
Sometimes, a method doesn't know how to fix an error, so it decides to "pass the responsibility" to whoever called it. We do this using the `throws` keyword in the method signature.

```java
public void readFile() throws IOException
{
    // I'm not handling the error here; 
    // the method that calls me MUST handle it!
}
```

## Best Practices (and Misuses)
Exceptions are powerful, but they shouldn't be overused:
* **DO** use them for unexpected runtime errors, file problems, or database failures.
* **DON'T** use them to control normal program logic. For example, don't use a `try-catch` to handle a user reading or writing to array indexes that don't exists, use ifs to make sure.
* **DON'T** put them inside "tight loops" where performance is critical, as creating exception objects takes more time than a simple `if` check.

## Summary
Exceptions allow us to write **reliable** programs that don't just "die" when something goes wrong. By separating our error-handling code from our main logic, our programs become easier to read and maintain. Remember the big three keywords: `try` it, `catch` it, or `throws` it up the line.

---

