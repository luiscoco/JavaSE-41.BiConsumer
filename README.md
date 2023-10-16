# JavaSE-BiConsumer

In Java, BiConsumer is a functional interface that represents an operation that takes two input arguments and returns no result. 

It's a part of the java.util.function package introduced in Java 8 to support functional programming.

The BiConsumer interface has a single method called accept, which takes two parameters and performs some operation on them. Here's the method signature:

```java
void accept(T t, U u);
```

T: the type of the first input argument.
U: the type of the second input argument.

Here's a simple example to illustrate how you might use BiConsumer:

```java
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        // Example 1: Concatenating two strings
        BiConsumer<String, String> concatenateStrings = (s1, s2) -> {
            String result = s1 + s2;
            System.out.println("Concatenated string: " + result);
        };

        concatenateStrings.accept("Hello", "World");

        // Example 2: Adding two numbers
        BiConsumer<Integer, Integer> addNumbers = (num1, num2) -> {
            int sum = num1 + num2;
            System.out.println("Sum of numbers: " + sum);
        };

        addNumbers.accept(5, 7);
    }
}
```

In this example:

concatenateStrings is a BiConsumer that takes two strings and prints their concatenation.

addNumbers is a BiConsumer that takes two integers and prints their sum.

When you run this program, you'll see output like:

```
Concatenated string: HelloWorld
Sum of numbers: 12
```
You can use BiConsumer in various scenarios where you need to perform an operation on two inputs without returning any result, such as updating state, printing, or logging.

# More samples about "BiConsumer" in Java

## Example 1: Map Iteration

```java
import java.util.HashMap;
import java.util.Map;
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        Map<String, Integer> ages = new HashMap<>();
        ages.put("Alice", 30);
        ages.put("Bob", 25);
        ages.put("Charlie", 35);

        // BiConsumer to print key-value pairs
        BiConsumer<String, Integer> printEntry = (key, value) ->
                System.out.println("Name: " + key + ", Age: " + value);

        // Iterate through the map and apply the BiConsumer
        ages.forEach(printEntry);
    }
}
```

## Example 2: Exception Handling

```java
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        int key = 0;

        // BiConsumer to handle division and print result or error message
        BiConsumer<Integer, Integer> divideAndPrint = (num, divisor) -> {
            try {
                System.out.println("Result: " + (num / divisor));
            } catch (ArithmeticException e) {
                System.err.println("Error: Division by zero!");
            }
        };

        // Apply the BiConsumer to each element in the array
        for (int num : numbers) {
            divideAndPrint.accept(num, key);
        }
    }
}
```

## Example 3: Updating Collections

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("John");
        names.add("Jane");
        names.add("Doe");

        // BiConsumer to update each element in the list
        BiConsumer<Integer, String> updateName = (index, newName) ->
                names.set(index, newName);

        // Update names at specific indices
        updateName.accept(1, "Janet");
        updateName.accept(2, "Smith");

        // Print the updated list
        names.forEach(System.out::println);
    }
}
```

These examples showcase different scenarios where BiConsumer can be applied, such as iterating through a map, handling exceptions, and updating collections. 

You can adapt and use BiConsumer based on the requirements of your specific use case.

# More advance topics about "BiConsumer" in Java

Let's explore some advanced topics related to BiConsumer in Java.

# 1. Chaining BiConsumers:

You can chain multiple BiConsumer instances together using the andThen method. This allows you to create a sequence of operations that will be executed in order.

```java
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        // First BiConsumer: Convert names to uppercase
        BiConsumer<String, String> toUpperCase = (s1, s2) ->
                System.out.println("Uppercase: " + s1.toUpperCase() + ", " + s2.toUpperCase());

        // Second BiConsumer: Print the length of names
        BiConsumer<String, String> printLength = (s1, s2) ->
                System.out.println("Length: " + s1.length() + ", " + s2.length());

        // Chain the BiConsumers
        BiConsumer<String, String> combined = toUpperCase.andThen(printLength);

        // Apply the chained BiConsumer
        combined.accept("John", "Doe");
    }
}
```

In this example, combined is a BiConsumer that first converts names to uppercase and then prints their lengths.

## 2. Handling Checked Exceptions:

If your BiConsumer involves code that throws checked exceptions, you can use the ExceptionUtils class from Apache Commons Lang or handle it using a lambda that wraps the checked exception.

```java
import java.io.IOException;
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {
        // BiConsumer with a checked exception
        BiConsumer<String, String> fileCopier = (source, destination) -> {
            try {
                // Code that may throw IOException
                // For example, copying a file
                // Files.copy(Paths.get(source), Paths.get(destination), StandardCopyOption.REPLACE_EXISTING);
                System.out.println("File copied successfully");
            } catch (IOException e) {
                // Handle the exception
                System.err.println("Error: " + e.getMessage());
            }
        };

        // Apply the BiConsumer
        fileCopier.accept("source.txt", "destination.txt");
    }
}
```

## 3. BiConsumer with Generics:

You can use generics to create a more flexible BiConsumer that can handle different types of input.

```java
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static <T, U> void processPair(T t, U u, BiConsumer<T, U> consumer) {
        consumer.accept(t, u);
    }

    public static void main(String[] args) {
        BiConsumer<String, Integer> printLength = (s, i) ->
                System.out.println("Length of " + s + ": " + i);

        processPair("Java", 5, printLength);
        processPair("BiConsumer", 10, printLength);
    }
}
```

In this example, the processPair method takes two parameters and a BiConsumer, allowing you to process different types of pairs.
