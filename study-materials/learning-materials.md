**Expanded Java Fundamentals Curriculum**  
**Build a Complete Console Library Management System (Pure Java, No Frameworks)**

This version gives much richer explanations for every topic so a complete beginner can understand *why* something exists, *how* it works, and *when* to use it, before seeing the code example. The examples remain focused and practical. Work through the topics in order, type the examples yourself, experiment, then complete the Activity.

---

### Section 0: Environment Setup

**JDK (Java Development Kit)**  
The JDK is the complete package you need to write and run Java programs. It contains:
- The compiler (`javac`) that turns your human-readable `.java` files into bytecode (`.class` files).
- The Java Virtual Machine (JVM) launcher (`java`) that runs the bytecode.
- Many standard libraries.

You must install a JDK (version 17 or 21 is recommended) before you can do anything. After installation, you should be able to open a terminal and type `java -version` and `javac -version` and see version numbers.

**IDE (Integrated Development Environment)**  
An IDE is a program that makes writing code much easier. It provides syntax highlighting, auto-completion, error detection, and a “Run” button. Popular free choices:
- IntelliJ IDEA Community Edition
- Visual Studio Code + “Extension Pack for Java”
- Eclipse

You can also write code in a plain text editor and compile from the command line, but an IDE is strongly recommended for beginners.

**Project and file rules**
- One public class per file.
- The file name must exactly match the public class name (including capital letters).  
  Example: class `LibraryApp` must live in `LibraryApp.java`.
- Source files are usually placed in a `src` folder.

**Activity**  
Install a JDK, set up an IDE, create a new Java project, and run a program that simply prints `Hello Library`.

**Runnable result**  
You can create, compile, and run a Java program.

---

### Section 1: Java Basics – Syntax, Variables, Data Types, Operators, Basic I/O

**1. Class structure**  
In Java, *everything* lives inside a class. A class is a container that groups related data and behavior. Even the simplest program needs at least one class.

Think of a class as a blueprint. Later you will create many objects from the same blueprint. For now, just remember that your code must sit inside a class declaration.

```java
public class LibraryApp {
    // all your code goes inside these curly braces
}
```

The word `public` means the class can be accessed from anywhere. For beginners, almost every class you write will be `public`.

**2. The `main` method**  
When you run a Java program, the JVM looks for a special method called `main`. This is the official starting point of every standalone application. The signature must be written exactly like this (the JVM is very strict about it):

```java
public static void main(String[] args) {
    // the program begins executing here
}
```

- `public` – accessible from outside.
- `static` – the method belongs to the class itself, not to an object (you will understand `static` more deeply later).
- `void` – the method does not return any value.
- `String[] args` – an array that can receive command-line arguments (you can ignore it for now).

**3. Primitive types**  
Java has two kinds of data types: primitives and reference types.

Primitives are the simplest building blocks. They store their value directly in memory and are very fast. There are exactly eight primitive types. The ones you will use most often are:

| Type     | What it stores                  | Example                  | Size   |
|----------|---------------------------------|--------------------------|--------|
| `int`    | Whole numbers                   | 42, -7, 2026             | 32-bit |
| `double` | Decimal numbers                 | 3.14, 99.9               | 64-bit |
| `boolean`| True or false                   | `true`, `false`          | 1-bit  |
| `char`   | A single character              | `'A'`, `'9'`, `'@'`      | 16-bit |

You declare a variable by writing the type, then the name, then (optionally) an initial value:

```java
int year = 2026;
double version = 1.0;
boolean isOpen = true;
char grade = 'A';
```

**Important**: Primitive names are all lowercase. If you write `Int` or `Boolean` (with capital letters) you are referring to the *wrapper classes*, which are different.

**4. `String`**  
`String` is used for text. It is **not** a primitive type; it is a class. That is why it starts with a capital letter.

Strings are written inside double quotes:

```java
String libraryName = "MyLibrary Management System";
String empty = "";          // empty string
String message = "Hello " + "World";  // concatenation with +
```

Once a `String` object is created, its content cannot be changed (it is immutable). When you appear to change a string, Java actually creates a new one behind the scenes.

**5. Operators**  
Operators let you perform calculations and comparisons.

Arithmetic operators: `+ - * / %` (the `%` is the remainder/modulo operator)  
Assignment: `=`  
Comparison (always produce a `boolean`): `== != < > <= >=`  
Logical: `&&` (AND), `||` (OR), `!` (NOT)

```java
int a = 10;
int b = 3;
int sum = a + b;               // 13
int remainder = a % b;         // 1
boolean isEqual = (a == b);    // false
boolean bothPositive = (a > 0) && (b > 0);  // true
```

Be careful with `==` for objects (especially Strings). For Strings you should normally use `.equals()` instead of `==`. You will learn why later.

**6. `System.out` – printing to the console**  
`System.out` is the standard way to show information to the user.

- `println(...)` – prints the value and then moves to the next line.
- `print(...)` – prints the value and stays on the same line.
- `printf(...)` – formatted printing (similar to C).

```java
System.out.println("Welcome to the library");
System.out.print("Enter choice: ");
System.out.printf("Version: %.1f%n", 1.0);   // %n is a platform-independent newline
```

**7. `Scanner` – reading user input**  
To get input from the keyboard you use the `Scanner` class (part of `java.util`).

```java
import java.util.Scanner;   // must be at the top of the file

Scanner scanner = new Scanner(System.in);

System.out.print("Enter your name: ");
String name = scanner.nextLine();     // reads the entire line

System.out.print("Enter your age: ");
int age = scanner.nextInt();          // reads an integer
```

Common methods:
- `nextLine()` – entire line as String
- `next()` – next word
- `nextInt()`, `nextDouble()`, `nextBoolean()` – corresponding primitives

**Warning**: After calling `nextInt()` or `nextDouble()`, a leftover newline character often remains. The next `nextLine()` may read an empty string. A common fix is to call an extra `scanner.nextLine()` to clear the buffer.

**8. Simple formatting and concatenation**  
You can build messages by joining strings with `+`:

```java
String name = "Alex";
int year = 2026;
System.out.println("Hello " + name + ", welcome to the library in " + year);
```

**Activity**  
Create the main class. Print a nice welcome banner for “MyLibrary Management System”. Store library name, version, and current year in variables. Ask the user for their name and greet them.

**Runnable result**  
Program starts, shows a banner, asks for a name, greets the user, and exits.

---

### Section 2: Control Flow (if / switch / loops)

**1. `if-else` statements**  
These let the program make decisions.

```java
int choice = 2;

if (choice == 1) {
    System.out.println("You chose option 1");
} else if (choice == 2) {
    System.out.println("You chose option 2");
} else {
    System.out.println("Invalid choice");
}
```

The conditions are evaluated from top to bottom. As soon as one is true, its block runs and the rest are skipped. The final `else` is optional but very useful for handling unexpected cases.

**2. `switch` statement**  
When you have many discrete options (especially numbers or enums), `switch` is often cleaner than a long chain of `if-else`.

```java
switch (choice) {
    case 1:
        System.out.println("View books");
        break;          // very important!
    case 2:
        System.out.println("Exit");
        break;
    default:
        System.out.println("Invalid option");
}
```

The `break` statement is crucial. Without it, execution “falls through” into the next case. (Modern Java has a new switch expression syntax that does not need `break`, but the classic form is still widely used and important to know.)

**3. `for` loop**  
Best when you know exactly how many times you want to repeat something.

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Count: " + i);
}
```

The three parts inside the parentheses are:
1. Initialization (`int i = 1`)
2. Condition (`i <= 5`) – loop continues while this is true
3. Update (`i++`) – runs after each iteration

**4. `while` and `do-while` loops**  
Use `while` when you do not know in advance how many times the loop should run (for example, “keep asking until the user types exit”).

```java
int i = 0;
while (i < 3) {
    System.out.println(i);
    i++;
}
```

`do-while` is similar but guarantees the body runs **at least once**, because the condition is checked at the end:

```java
do {
    System.out.println("This always runs at least once");
} while (false);
```

**5. `break` and `continue`**
- `break` immediately exits the nearest loop or switch.
- `continue` skips the rest of the current iteration and jumps to the next one.

These are powerful but can make code harder to read if overused. Prefer clear loop conditions when possible.

**Activity**  
Implement a repeating menu with options such as “1. Show welcome again” and “2. Exit”. Keep the menu alive with a loop until the user chooses Exit. Reject non-numeric input with a simple message.

**Runnable result**  
A menu that keeps appearing until the user chooses to exit.

---

### Section 3: Methods and Arrays

**1. Methods**  
A method is a named block of code that performs a specific task. Methods help you avoid repeating the same code and make programs easier to read and maintain.

```java
public static void printWelcome() {
    System.out.println("=== MyLibrary Management System ===");
}
```

You *call* (execute) the method by writing its name followed by parentheses:

```java
printWelcome();
```

**2. Parameters and return values**  
Methods can receive data (parameters) and can send a result back (return value).

```java
public static int add(int a, int b) {
    return a + b;          // sends the result back to the caller
}

int sum = add(5, 3);       // sum becomes 8
```

- `void` means the method does not return anything.
- If a method has a return type other than `void`, every path through the method must end with a `return` statement.

**3. Method overloading**  
You can have multiple methods with the **same name** as long as their parameter lists are different (different number or types of parameters). This is called overloading.

```java
public static void display(String title) { ... }
public static void display(String title, String author) { ... }
```

The compiler chooses the correct version based on the arguments you pass.

**4. Arrays**  
An array is a fixed-size container that holds multiple values of the **same type**. Once created, its length cannot change.

```java
// Declare and create an array that can hold 5 Strings
String[] titles = new String[5];

// Assign values
titles[0] = "Java Basics";
titles[1] = "Object-Oriented Programming";

// Alternative short syntax when you know the values immediately
String[] moreTitles = {"Clean Code", "Effective Java"};
```

Important points:
- Indexes start at 0.
- The length is available via `.length` (note: it is a field, not a method, so no parentheses).
- Accessing an index that does not exist causes an `ArrayIndexOutOfBoundsException`.

**5. Looping through arrays**  
Classic indexed loop:

```java
for (int i = 0; i < titles.length; i++) {
    System.out.println(titles[i]);
}
```

Enhanced for-loop (simpler when you do not need the index):

```java
for (String title : titles) {
    System.out.println(title);
}
```

**Activity**  
Extract menu printing and input reading into methods. Create a fixed-size array of book titles (and authors if you like). Add methods to display all books, add a book (with capacity check), and search by title.

**Runnable result**  
You can add a limited number of books, list them, and search. Still using arrays of strings.

---

### Section 4: Object-Oriented Programming Foundations

**1. Classes and objects**  
A class is a blueprint. An object is a concrete instance created from that blueprint.

Real-world analogy: the class `Book` describes what every book has (title, author, etc.). Each actual book on the shelf is an object.

```java
public class Book {
    // fields and methods will go here
}
```

You create an object with the `new` keyword:

```java
Book book1 = new Book();
```

**2. Fields (instance variables)**  
Fields store the state (data) of an object. They should almost always be declared `private` so that outside code cannot change them directly (this is the start of encapsulation).

```java
private String title;
private String author;
private String isbn;
private int year;
private boolean available;
```

Each object gets its own copy of these fields.

**3. Constructors**  
A constructor is a special method that runs automatically when you create an object with `new`. Its job is to initialize the object into a valid state.

Rules:
- The name of the constructor must be exactly the same as the class name.
- It has no return type (not even `void`).

```java
public Book(String title, String author, String isbn, int year) {
    this.title = title;
    this.author = author;
    this.isbn = isbn;
    this.year = year;
    this.available = true;   // default value
}
```

You can have multiple constructors (constructor overloading).

**4. The `this` keyword**  
`this` refers to the current object. It is most often used when a parameter has the same name as a field, to distinguish them:

```java
public void setTitle(String title) {
    this.title = title;     // this.title is the field, title is the parameter
}
```

**5. Getters and setters – Encapsulation**  
Encapsulation means hiding the internal details of an object and controlling access to them.

Instead of letting outside code reach into the object and change fields directly, you provide public methods:

```java
public String getTitle() {
    return title;
}

public void setTitle(String title) {
    if (title != null && !title.isBlank()) {
        this.title = title;
    }
}
```

Benefits:
- You can add validation.
- You can change the internal representation later without breaking other code.
- You protect the object from being put into an invalid state.

**6. The `toString()` method**  
When you print an object, Java calls its `toString()` method. By default it produces something ugly like `Book@1a2b3c`. You should override it to return a readable description:

```java
@Override
public String toString() {
    return title + " by " + author + " (" + year + ")";
}
```

The `@Override` annotation is optional but highly recommended; it tells the compiler you intend to override a parent method.

**Activity**  
Create a proper `Book` class with private fields, constructors, getters/setters, and a good `toString()`. Replace the arrays of strings with an array of `Book` objects. Update the add/list/search methods. Start a simple `Library` class that owns the collection of books.

**Runnable result**  
Real `Book` objects are created and displayed with meaningful output. Encapsulation is visible.

---

### Section 5: Inheritance, Polymorphism, Method Overriding

**1. Inheritance (`extends`)**  
Inheritance lets you create a new class based on an existing one. The new class (subclass / child) inherits fields and methods from the existing class (superclass / parent).

This models an “is-a” relationship: a `Book` *is a* `LibraryItem`.

```java
public class LibraryItem {
    protected String title;     // protected = visible to subclasses
    // common methods
}

public class Book extends LibraryItem {
    private String isbn;
}
```

The child class can add its own fields and methods and can also override (replace) methods from the parent.

**2. The `super` keyword**  
`super` refers to the parent class. It is used in two main situations:
- To call the parent’s constructor: `super(...);` (must be the first statement in the child constructor).
- To call a parent method that you have overridden: `super.someMethod();`

**3. Method overriding**  
When a subclass provides its own version of a method that already exists in the parent, it is called overriding. The method signature (name + parameters) must be identical.

```java
@Override
public void displayInfo() {
    System.out.println("Book: " + title + ", ISBN: " + isbn);
}
```

**4. Polymorphism**  
Polymorphism means “many forms”. In practice it means you can treat a subclass object as if it were an instance of its parent type.

```java
LibraryItem item = new Book("Effective Java", "978-0134685991");
item.displayInfo();   // calls the Book version at runtime
```

This is extremely powerful. You can write code that works with the parent type and later plug in any subclass without changing that code.

**Activity**  
Create a base class (`LibraryItem` or `Media`). Make `Book` extend it. Optionally add another subclass (e.g. `Magazine`). Store items in an array of the base type and demonstrate polymorphic display.

**Runnable result**  
The system can handle different kinds of items through a common type while still showing type-specific details.

---

### Section 6: Abstract Classes, Interfaces, and Enums

**1. Abstract classes**  
An abstract class is a class that cannot be instantiated directly (you cannot write `new AbstractClass()`). It is meant to be extended.

It can contain:
- Abstract methods (methods without a body – subclasses *must* implement them).
- Regular methods with full implementations.
- Fields, constructors, etc.

```java
public abstract class LibraryItem {
    protected String title;

    public abstract void displayInfo();   // no body

    public void printTitle() {            // regular method
        System.out.println(title);
    }
}
```

Use abstract classes when you have shared code *and* want to force subclasses to provide certain behavior.

**2. Interfaces**  
An interface is a pure contract. It defines what methods a class must have, but (until recent Java versions) contained no implementation. A class can implement multiple interfaces (unlike inheritance, which is single).

```java
public interface Borrowable {
    void borrow();
    void returnItem();
}

public class Book extends LibraryItem implements Borrowable {
    @Override
    public void borrow() { ... }

    @Override
    public void returnItem() { ... }
}
```

Interfaces are excellent for defining capabilities (“this object can be borrowed”).

**3. Enums**  
An enum is a special data type that represents a fixed set of constants. It is much safer than using plain integers or strings for status values.

```java
public enum BookStatus {
    AVAILABLE,
    BORROWED,
    RESERVED,
    LOST
}
```

Usage:

```java
BookStatus status = BookStatus.AVAILABLE;

if (status == BookStatus.AVAILABLE) {
    // ...
}

// You can also give enums fields and methods if needed
```

Enums make your code more readable and prevent invalid values.

**Activity**  
Make the base item abstract or introduce a `Borrowable` interface. Replace boolean flags with a `BookStatus` enum. Update the borrow/return skeleton so it uses the new constructs.

**Runnable result**  
Status is type-safe and the borrow/return structure is expressed with interfaces or abstract methods.

---

### Section 7: Collections Framework

**1. Why collections?**  
Arrays have a fixed size. In real programs you rarely know in advance how many books or members you will have. The Collections Framework provides dynamic, resizable data structures.

**2. `List` and `ArrayList`**  
`List` is an interface. `ArrayList` is the most commonly used implementation. It grows automatically as you add elements.

```java
import java.util.ArrayList;
import java.util.List;

List<Book> books = new ArrayList<>();
books.add(new Book(...));
books.size();
books.get(0);               // first element
books.remove(0);
books.isEmpty();
```

The `<Book>` part is a generic type parameter. It tells the compiler that this list can only hold `Book` objects (or subclasses). This gives you type safety and removes the need for casting.

**3. `Map` and `HashMap`**  
A `Map` stores key-value pairs. It is perfect when you want fast lookup by a unique identifier (ISBN, member ID, etc.).

```java
import java.util.HashMap;
import java.util.Map;

Map<String, Book> bookByIsbn = new HashMap<>();
bookByIsbn.put("978-0134685991", book);
Book found = bookByIsbn.get("978-0134685991");
boolean exists = bookByIsbn.containsKey("978-0134685991");
```

**4. Iterating**
```java
for (Book book : books) {
    System.out.println(book);
}

// For maps
for (Map.Entry<String, Book> entry : bookByIsbn.entrySet()) {
    System.out.println(entry.getKey() + " → " + entry.getValue());
}
```

**Activity**  
Replace fixed arrays with `ArrayList<Book>`. Use a `HashMap` for fast ISBN lookup. Create a `Member` class and an `ArrayList<Member>`. Implement proper add/remove/search/list operations.

**Runnable result**  
Dynamic number of books and members with fast lookups and real CRUD operations.

---

### Section 8: Exception Handling

**1. What is an exception?**  
An exception is an event that disrupts the normal flow of the program (invalid input, missing file, division by zero, etc.). Java forces you to deal with many of these situations so your program does not crash unexpectedly.

**2. `try-catch-finally`**
```java
try {
    // code that might throw an exception
    int number = Integer.parseInt(userInput);
} catch (NumberFormatException e) {
    System.out.println("That was not a valid number.");
} finally {
    // this block always runs (optional)
}
```

You can have multiple `catch` blocks for different exception types.

**3. Checked vs unchecked exceptions**
- **Unchecked** (RuntimeException and its subclasses) – the compiler does not require you to handle them (e.g. `NullPointerException`, `IllegalArgumentException`).
- **Checked** – the compiler forces you to either handle them with `try-catch` or declare them with `throws`.

**4. Throwing exceptions**  
You can create and throw exceptions yourself when something is wrong:

```java
if (book == null) {
    throw new BookNotFoundException("No book found with that ISBN");
}
```

**5. Custom exceptions**  
You can (and often should) create your own exception classes for domain-specific errors:

```java
public class BookNotFoundException extends Exception {
    public BookNotFoundException(String message) {
        super(message);
    }
}
```

**Activity**  
Create custom exceptions (`BookNotFoundException`, `BookAlreadyBorrowedException`, `InvalidInputException`, etc.). Wrap user input parsing and business operations so the program never crashes on bad data. Show clear messages and return to the menu.

**Runnable result**  
Invalid actions produce clear messages and the menu continues running.

---

### Section 9: File I/O and Persistence

**1. Why file I/O?**  
Until now all data lives only in memory. When the program ends, everything disappears. Writing to files lets the library data survive between runs.

**2. Writing text files**
```java
import java.io.PrintWriter;
import java.io.FileWriter;
import java.io.IOException;

try (PrintWriter writer = new PrintWriter(new FileWriter("books.txt"))) {
    writer.println("Effective Java,Joshua Bloch,978-0134685991");
} catch (IOException e) {
    System.out.println("Could not save data: " + e.getMessage());
}
```

The try-with-resources syntax (the `try (...)`) automatically closes the file even if an error occurs.

**3. Reading text files**
```java
import java.util.Scanner;
import java.io.File;

try (Scanner fileScanner = new Scanner(new File("books.txt"))) {
    while (fileScanner.hasNextLine()) {
        String line = fileScanner.nextLine();
        // split the line and recreate Book objects
    }
} catch (IOException e) {
    System.out.println("Could not load data.");
}
```

**4. Choosing a format**  
For beginners, a simple delimited text format (comma-separated or `|`-separated) is easiest. Later you can learn object serialization, JSON, etc., but they are not required here.

**Activity**  
Add Save and Load functionality (or automatic load on start and save on exit). Persist the lists of books and members to text files.

**Runnable result**  
Data survives when you close and reopen the program.

---

### Section 10: Generics, More Features, and Business Logic

**1. Generics (deeper look)**  
Generics let you write classes and methods that work with different types while still remaining type-safe. You have already used them with `List<Book>` and `Map<String, Book>`.

They prevent the old pre-Java-5 style of storing everything as `Object` and then casting, which was error-prone.

**2. `java.time.LocalDate`**  
The modern date/time API (introduced in Java 8). Prefer it over the old `Date` and `Calendar` classes.

```java
import java.time.LocalDate;

LocalDate today = LocalDate.now();
LocalDate dueDate = today.plusDays(14);
boolean isOverdue = dueDate.isBefore(LocalDate.now());
```

**3. Building real business logic**  
Now you have enough tools to implement proper borrow/return:
- Check that the book is available.
- Create a `Loan` object that records which member borrowed which book and when it is due.
- Update the book’s status.
- Later calculate fines if the book is returned late.

**Activity**  
Add a `Loan` class. Implement full borrow and return flows with date handling. Add simple reports (list overdue books, list books borrowed by a specific member). Use generics consistently.

**Runnable result**  
Complete core library workflow is working.

---

### Section 11: Packages, Code Organization, Static, Final

**1. Packages**  
As the project grows, putting every class in the default package becomes messy. Packages let you organize classes into logical groups (and also control access).

```java
package model;          // this file lives in a folder named model

public class Book { ... }
```

Other classes import it:

```java
import model.Book;
```

Common package structure for this project:
- `model` – Book, Member, Loan, enums
- `service` or `manager` – business logic
- `exception` – custom exceptions
- `util` – helper methods
- main class at the root or in a `main` / `app` package

**2. `static` members**  
A `static` field or method belongs to the *class* itself, not to any particular object. There is only one copy.

Good uses:
- Constants: `public static final String LIBRARY_NAME = "MyLibrary";`
- Utility methods that do not need object state.

**3. `final`**
- `final` variable → must be assigned once and can never change.
- `final` method → cannot be overridden by subclasses.
- `final` class → cannot be extended.

Constants are conventionally written in ALL_CAPS and marked `static final`.

**Activity**  
Reorganize the code into proper packages. Move business logic out of the main class into service classes. Introduce constants and clean up the overall structure.

**Runnable result**  
A clean, professional project layout that is easy to navigate and extend.

---

### Section 12 (Optional): Multithreading Basics

**Creating and starting a thread**
```java
Thread autoSaveThread = new Thread(() -> {
    while (true) {
        // save the data
        try {
            Thread.sleep(30_000);   // 30 seconds
        } catch (InterruptedException e) {
            break;
        }
    }
});
autoSaveThread.setDaemon(true);   // thread will not prevent the program from exiting
autoSaveThread.start();
```

This is only a light introduction. Real concurrent programming has many more rules (synchronization, thread safety, etc.). For a console library system a background auto-save is a nice demonstration but not required.

**Activity**  
Add a simple background auto-save thread (keep data access straightforward).

**Runnable result**  
Demonstration of a background task running while the menu remains usable.

---

### Final Capstone
After Section 11 you possess a complete, working pure-Java Library Management System that demonstrates virtually every core language feature. Suggested extra challenges:
- Fine calculation for overdue books
- Search by multiple fields
- Export a readable text report
- Stronger input validation and confirmation prompts
- A clear README explaining how to compile and run the project

You now have detailed conceptual grounding plus working examples for every major topic. Move section by section, type every example, experiment freely, and only proceed when the Activity for that section runs correctly. This approach turns abstract language features into concrete, visible behavior inside a real application.