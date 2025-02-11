# Java Exception Handling Lab

Java exceptions are events that occur during the execution of a program and disrupt its normal flow. They signal that an error or unexpected condition has occurred, allowing your program to respond gracefully rather than crashing unexpectedly. Java's robust exception handling mechanism enables you to catch and manage these errors, ensuring your applications remain reliable and user-friendly.

This lab is divided into several standalone sections, each focusing on a specific aspect of Java exception handling. Every section includes:
- **An Explanation:** A brief description of the concept.
- **An Example:** Practical code demonstrating the concept.
- **A DIY Exercise:** A hands-on activity with an expected output dropdown to help you verify your work.

You can complete each section independently, allowing you to learn and practice Java exceptions step by step.

---

## Setup

Before you begin any section, create a new Java package named `ie.atu.exceptions`. Use the **JAVA PROJECTS** pane in the Explorer panel on the left to create this package. Inside this package, create a class named `Main` (or another appropriate class for each section) and insert the main method. Add a simple print statement to ensure everything is set up correctly.

---

## Agenda

1. [Introduction to Exception Handling](#1-introduction-to-exception-handling)
2. [Common Exceptions](#2-common-exceptions)
3. [Checked vs Unchecked Exceptions](#3-checked-vs-unchecked-exceptions)
4. [try-catch Blocks](#4-try-catch-blocks)
5. [finally Block](#5-finally-block)
6. [try-with-resources](#6-try-with-resources)
7. [throw and throws Keywords](#7-throw-and-throws-keywords)
8. [Custom Exceptions](#8-custom-exceptions)
9. [Error vs Exception](#9-error-vs-exception)

---

## 1. Introduction to Exception Handling

### Explanation
An **exception** in Java is an event that disrupts the normal flow of a program's execution. When an error occurs within a method, an exception object is created and passed to the runtime system—a process known as "throwing an exception." Exception handling enables your program to manage these unexpected events gracefully.

### Example
```java
public class ExceptionIntroduction {
    public static void main(String[] args) {
        // This code will throw a NullPointerException because 'text' is null.
        String text = null;
        System.out.println(text.length());
    }
}
```

<details>
<summary>Expected Output</summary>

```
Exception in thread "main" java.lang.NullPointerException
    at ExceptionIntroduction.main(ExceptionIntroduction.java:4)
```

</details>

### DIY Exercise 🔦
- **Task**: Modify the above code so that it first checks whether `text` is `null` before attempting to access its length.  
- **Hint**: Use an if-statement to verify if `text` is not `null`. If it is `null`, print a custom message instead of calling `length()`.

<details>
<summary>Expected Output</summary>

```
Text is null. Cannot retrieve length.
```

*Note: The output will depend on your custom message.*
</details>

---

## 2. Common Exceptions

### Explanation
Java provides several built-in exceptions that represent common error conditions:
- **`NullPointerException`**: Occurs when you try to use a reference that points to no object.
- **`ArrayIndexOutOfBoundsException`**: Thrown when attempting to access an array with an invalid index.
- **`ArithmeticException`**: Happens when an illegal arithmetic operation is performed (for example, division by zero).
- **`IOException`**: Signals that an input/output operation has failed.

### Example
```java
public class CommonExceptions {
    public static void main(String[] args) {
        // Uncomment each section to see the exception in action.
        
        // 1. NullPointerException example:
        // String text = null;
        // System.out.println(text.length());
        
        // 2. ArrayIndexOutOfBoundsException example:
        int[] numbers = {1, 2, 3};
        // System.out.println(numbers[5]);

        // 3. ArithmeticException example:
        // int result = 10 / 0;
        // System.out.println(result);
    }
}
```

<details>
<summary>Expected Output</summary>

If you uncomment any of the problematic lines, you will see the corresponding exception message (for example, a NullPointerException or ArrayIndexOutOfBoundsException).
</details>

### DIY Exercise 🔦
- **Task**: Write a short Java program that intentionally triggers an `ArithmeticException` by dividing an integer by zero.  
- **Hint**: Wrap the division in a try-catch block and print the exception message in the catch block.

<details>
<summary>Expected Output</summary>

```
Caught ArithmeticException: / by zero
```

*Note: The exact message may vary depending on your implementation.*
</details>

---

## 3. Checked vs Unchecked Exceptions

### Explanation
Java exceptions are divided into two main categories:
- **Checked Exceptions**: These exceptions are checked at compile time. They must be either caught using a try-catch block or declared in the method signature with the `throws` keyword (e.g., `IOException`).
- **Unchecked Exceptions**: These are subclasses of `RuntimeException` (e.g., `NullPointerException`, `ArithmeticException`). They are not checked at compile time and typically indicate programming errors.

### Example
```java
import java.io.FileReader;
import java.io.IOException;

public class CheckedVsUnchecked {
    public static void main(String[] args) {
        // Checked Exception Example:
        try {
            FileReader reader = new FileReader("nonexistent.txt");
            System.out.println("File opened successfully");
        } catch (IOException e) {
            System.out.println("Caught checked exception: " + e.getMessage());
        }

        // Unchecked Exception Example:
        String text = null;
        // Uncomment to trigger an unchecked exception:
        // System.out.println(text.length());
    }
}
```

<details>
<summary>Expected Output</summary>

```
Caught checked exception: nonexistent.txt (No such file or directory)
```

*Note: The output for the unchecked exception depends on whether you uncomment the line.*
</details>

### DIY Exercise 🔦
- **Task**: Create a method that demonstrates both a checked and an unchecked exception:
  - For the checked exception, attempt to open a file that does not exist and handle the resulting `IOException`.
  - For the unchecked exception, try to access an element from an empty array and let the exception occur.
- **Hint**: Write separate code blocks in your method for each exception type, ensuring each is self-contained.

<details>
<summary>Expected Output</summary>

```
Caught checked exception: nonexistent.txt (No such file or directory)
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 0
    at YourClassName.methodName(YourClassName.java:XX)
```

*Note: The line numbers and class names will vary based on your implementation.*
</details>

---

## 4. try-catch Blocks

### Explanation
A try-catch block allows you to execute code that might throw an exception, and then catch and handle that exception without crashing the program. The code that might fail is placed in the try block, and the error-handling code is in the catch block.

### Example
```java
public class TryCatchDemo {
    public static void main(String[] args) {
        try {
            int division = 10 / 0;  // This will throw an ArithmeticException.
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
        }
    }
}
```

<details>
<summary>Expected Output</summary>

```
Error: Cannot divide by zero!
```

</details>

### DIY Exercise 🔦
- **Task**: Write a program that defines an array of 5 integers. Ask the user to input an index, and then try to access the array at that index using a try-catch block to handle any `ArrayIndexOutOfBoundsException`.
- **Hint**: Use a `Scanner` to read user input and wrap the array access code in a try-catch structure.

<details>
<summary>Expected Output</summary>

*If the user enters an invalid index (e.g., 7):*
```
Caught ArrayIndexOutOfBoundsException: 7
```

*If the user enters a valid index, the corresponding integer from the array is printed.*
</details>

---

## 5. finally Block

### Explanation
The `finally` block is used in conjunction with try-catch blocks. It executes code regardless of whether an exception was thrown or caught, and is often used for cleanup operations like closing files or releasing resources.

### Example
```java
public class FinallyDemo {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]); // This will throw an exception.
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Caught exception: Index out of bounds!");
        } finally {
            System.out.println("Cleanup: This message prints regardless of exceptions.");
        }
    }
}
```

<details>
<summary>Expected Output</summary>

```
Caught exception: Index out of bounds!
Cleanup: This message prints regardless of exceptions.
```

</details>

### DIY Exercise 🔦
- **Task**: Create a program that simulates opening and processing a file. Use a try-catch block to handle a potential exception, and include a finally block that prints a message like "File processing complete."  
- **Hint**: You may simulate file processing with print statements rather than actual file I/O.

<details>
<summary>Expected Output</summary>

```
Caught exception: [Exception message]
File processing complete.
```

*Note: The exception message will depend on your simulation.*
</details>

---

## 6. try-with-resources

### Explanation
The try-with-resources statement simplifies resource management by automatically closing resources when the try block is exited. It works with any object that implements the `AutoCloseable` interface, such as files or network connections.

### Example
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class TryWithResourcesDemo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {
            String line = br.readLine();
            System.out.println("First line: " + line);
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
        }
    }
}
```

<details>
<summary>Expected Output</summary>

If the file "example.txt" does not exist:
```
IOException: <error message>
```
</details>

### DIY Exercise 🔦
- **Task**: Write a program that uses try-with-resources to read and print the first line of a file. Handle the case where the file is missing by catching the appropriate exception and printing an error message.
- **Hint**: Use `BufferedReader` and `FileReader` as shown in the example.

<details>
<summary>Expected Output</summary>

```
IOException: <error message indicating file not found>
```
</details>

---

## 7. throw and throws Keywords

### Explanation
- **`throw`**: Used to explicitly throw an exception within a method or block of code.
- **`throws`**: Declares that a method may throw one or more exceptions, which must then be handled by the calling code.

### Example
**Using `throw`:**
```java
public class ThrowDemo {
    public static void main(String[] args) {
        try {
            validateAge(15); // This will throw an exception.
        } catch (IllegalArgumentException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    public static void validateAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be at least 18.");
        }
        System.out.println("Age is valid.");
    }
}
```

**Using `throws`:**
```java
public class ThrowsDemo {
    public static void main(String[] args) {
        try {
            performOperation();  // This method declares it throws Exception.
        } catch (Exception e) {
            System.out.println("Exception handled: " + e.getMessage());
        }
    }

    public static void performOperation() throws Exception {
        throw new Exception("An error occurred.");
    }
}
```

<details>
<summary>Expected Output</summary>

For the `throw` example:
```
Caught exception: Age must be at least 18.
```

For the `throws` example:
```
Exception handled: An error occurred.
```
</details>

### DIY Exercise 🔦
- **Task**:  
  1. Create a method `calculateGrade` that accepts a student's score. If the score is negative or greater than 100, use `throw` to raise an `IllegalArgumentException` with the message "Invalid score".  
  2. In your main method, call `calculateGrade` and use a try-catch block to catch and print the error message.
- **Hint**: Ensure that the method either handles the exception internally or declares it using `throws` so that the caller can handle it.

<details>
<summary>Expected Output</summary>

```
Caught exception: Invalid score
```

*Note: This output will appear if an invalid score is provided.*
</details>

---

## 8. Custom Exceptions

### Explanation
Custom exceptions allow you to create your own exception types to represent specific error conditions in your application. You create a custom exception by extending the `Exception` class (or one of its subclasses).

### Example
**Creating a custom exception:**
```java
public class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

**Using the custom exception:**
```java
public class CustomExceptionDemo {
    public static void main(String[] args) {
        try {
            registerUser(15); // This will throw an InvalidAgeException.
        } catch (InvalidAgeException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static void registerUser(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("User must be at least 18 years old.");
        }
        System.out.println("User registered successfully.");
    }
}
```

<details>
<summary>Expected Output</summary>

```
Error: User must be at least 18 years old.
```
</details>

### DIY Exercise 🔦
- **Task**:  
  Create a custom exception called `InsufficientFundsException` (extending `Exception`). Then, write a `BankAccount` class that includes a `withdraw` method. If a withdrawal amount exceeds the account balance, the method should throw an `InsufficientFundsException`.
- **Hint**: In the `withdraw` method, check if the withdrawal amount is greater than the balance and throw the exception with a suitable message if so.

<details>
<summary>Expected Output</summary>

```
Error: Insufficient funds. Withdrawal amount exceeds balance.
```

*Note: The exact wording depends on your implementation.*
</details>

---

## 9. Error vs Exception

### Explanation
Both **errors** and **exceptions** are subclasses of the `Throwable` class, but they are used for different scenarios:
- **Exceptions**: Represent conditions that a program can catch and handle, such as invalid input or missing files.
- **Errors**: Represent serious problems that are usually not handled by the application (e.g., `OutOfMemoryError`, `StackOverflowError`). They indicate issues in the runtime environment and are not meant to be caught.

### Example
```java
public class ErrorVsExceptionDemo {
    public static void main(String[] args) {
        try {
            // The following line is commented out because errors are not typically caught.
            // throw new StackOverflowError("Simulated Error");
        } catch (Exception e) {
            System.out.println("Caught Exception: " + e.getMessage());
        }
        System.out.println("Program continues normally.");
    }
}
```

<details>
<summary>Expected Output</summary>

```
Program continues normally.
```
</details>

### DIY Exercise 🔦
- **Task**:  
  Write a short Java program that includes comments explaining why errors (such as `OutOfMemoryError`) are generally not caught by try-catch blocks. Optionally, simulate an error by writing a comment that explains what would happen if you tried to catch such an error.
- **Hint**: Focus on writing clear code comments that explain the severity of errors compared to exceptions.

<details>
<summary>Expected Output</summary>

```
[No direct output, as the program includes only comments. The program should print "Program continues normally." if run.]
```
</details>

---

## Summary

In this lab, you learned about:
- **Exception Handling**: The mechanism for managing runtime anomalies.
- **Common Exceptions**: Such as `NullPointerException`, `ArrayIndexOutOfBoundsException`, and `ArithmeticException`.
- **Checked vs Unchecked Exceptions**: The distinction between compile-time and runtime exceptions.
- **try-catch Blocks**: How to catch and handle exceptions.
- **finally Block**: How to execute cleanup code irrespective of exceptions.
- **try-with-resources**: How to automatically manage resources.
- **throw and throws**: How to explicitly throw exceptions and declare exception-throwing methods.
- **Custom Exceptions**: How to create your own exception classes.
- **Error vs Exception**: The differences between critical errors and manageable exceptions.

Each section is designed to be self-contained so you can work on them independently.

Enjoy exploring Java's exception handling mechanisms!
