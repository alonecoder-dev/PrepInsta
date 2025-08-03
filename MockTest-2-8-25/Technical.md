

# Select the correct output for the given code:

int[] arr = {10, 20, 30};
System.out.println(Arrays.toString(arr));

10, 20, 30

[10, 20, 30]

{10, 20, 30}

Compilation error

The call `Arrays.toString(arr)` formats the array elements inside square brackets and separates them with commas and spaces. Hence the printed result is:

---

# Select the correct output for the given code:

int[] arr = {10, 20, 30};
System.out.println(Arrays.toString(arr));

10, 20, 30

[10, 20, 30]

{10, 20, 30}

Compilation error

The call `Arrays.toString(arr)` prints the array in its standard string representation, which includes square brackets:

---

# Select the correct output for the given code:

int[] arr = {10, 20, 30};
System.out.println(Arrays.toString(arr));

10, 20, 30

[10, 20, 30]

{10, 20, 30}

Compilation error

The correct output is:

---

# Select the correct output for the given code:

int[] arr = {10, 20, 30};
System.out.println(Arrays.toString(arr));

10, 20, 30

[10, 20, 30]

{10, 20, 30}

Compilation error

The correct output is:

```
[10, 20, 30]
```

**Explanation:**

The `Arrays.toString()` method in Java returns a string representation of the contents of the specified array. The format is a list of the array's elements, enclosed in square brackets (`"[]"`), with adjacent elements separated by a comma followed by a space (`", "`).

---

# One of the following is not a Java keyword:

static

void

null

volatile

The correct answer is **null**.

**Explanation:**

* **`static`**, **`void`**, and **`volatile`** are all reserved keywords in Java.
* **`null`** is a special literal, not a keyword. It represents a reference that does not point to any object. While you cannot use `null` as an identifier (like a variable name), it is technically classified as a literal, alongside `true` and `false`.

---

# Select the correct output for the given code:

ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
list.add(1, 15);
System.out.println(list);

[10, 15, 20]

[10, 20, 15]

[10, 15]

Compilation error

The correct output is:

```
[10, 15, 20]
```

**Explanation:**

1. `ArrayList<Integer> list = new ArrayList<>();`: An empty ArrayList is created. `list` is `[]`.
2. `list.add(10);`: 10 is added to the end of the list. `list` is ``.
3. `list.add(20);`: 20 is added to the end of the list. `list` is ``.
4. `list.add(1, 15);`: This command inserts the integer `15` at index `1`. The element currently at index 1 (which is `20`) and all subsequent elements are shifted one position to the right.
5. The final state of the list becomes ``.
6. `System.out.println(list);`: This prints the string representation of the ArrayList.

---

# The output of following code:

String s1 = "Java";
String s2 = new String("Java");
System.out.println(s1 == s2);

true

false

Compilation error

java

The correct output is:

```
false
```

**Explanation:**

* **`String s1 = "Java";`**: This creates a string literal. The Java Virtual Machine (JVM) places this string in a special memory area called the "String Constant Pool". The variable `s1` holds a reference to this object in the pool.
* **`String s2 = new String("Java");`**: The `new` keyword explicitly creates a brand new `String` object in the main heap memory. This new object is separate from any object in the String Constant Pool, even if they contain the same characters. The variable `s2` holds a reference to this new object on the heap.
* **`System.out.println(s1 == s2);`**: The `==` operator, when used with objects, compares their memory addresses (references), not their actual content. Since `s1` and `s2` refer to two different objects in different memory locations (one in the String Pool, one on the heap), the comparison `s1 == s2` evaluates to `false`.

To compare the actual content of the strings, you would use the `.equals()` method: `s1.equals(s2)`, which would return `true`.

---

# One of the following is true about do-while loop in Java:

It checks the condition before execution

It guarantees the loop runs at least once

It is not supported in Java

It can never be infinite

The correct statement is:

**It guarantees the loop runs at least once**

**Explanation:**

A `do-while` loop is a post-test loop, which means it executes the body of the loop first and then checks the condition. Because the condition is not checked until after the first iteration, the code block inside the `do` statement is guaranteed to execute at least one time, even if the condition is initially false.

Let's review the other options:

* **It checks the condition before execution:** This describes a `while` loop or a `for` loop, not a `do-while` loop.
* **It is not supported in Java:** This is incorrect. The `do-while` loop is a standard control flow statement in Java.
* **It can never be infinite:** This is incorrect. A `do-while` loop can be infinite if its condition always evaluates to `true` (e.g., `do { ... } while (true);`).

---

# What does this code print when executed ?

Stream<Integer> stream = Stream.of(1, 2, 3, 4);
stream.filter(x -> x % 2 == 0);
stream.forEach(System.out::print);

24

1234

2 4

Compilation error

This is a trick question. The correct answer is that the code will fail, but the provided options are slightly inaccurate. The code will throw a runtime exception, not a compilation error. However, among the choices, "Compilation error" is the intended answer representing that the code will not run successfully.

**The output is:**

**Compilation error** (more accurately, a runtime `IllegalStateException`)

**Explanation:**

The key principle of Java Streams is that **a stream can only be operated on once**. Once a terminal or intermediate operation is called on a stream, it is considered "consumed" and cannot be used again.

1. `Stream<Integer> stream = Stream.of(1, 2, 3, 4);`
    * A stream is created.
2. `stream.filter(x -> x % 2 == 0);`
    * This is an **intermediate operation**. It consumes the original `stream` to produce a new stream containing only the even numbers.
    * Crucially, the result of this operation (the new stream) is not assigned to any variable; it's discarded.
    * The original `stream` variable is now considered "consumed" or "closed."
3. `stream.forEach(System.out::print);`
    * This line attempts to call a **terminal operation** (`forEach`) on the *original* `stream` variable.
    * Since that stream has already been operated on by `filter`, the Java runtime will throw an `IllegalStateException` with the message "stream has already been operated upon or closed."

Because the code throws an exception at runtime, it does not print `24` or `1234`. While it's a runtime error, not a compilation error, "Compilation error" is the only option that indicates the code fails to execute as intended.

To get the intended output of `24`, the code should be written by chaining the methods:

```java
Stream.of(1, 2, 3, 4)
      .filter(x -> x % 2 == 0)
      .forEach(System.out::print); // This would print "24"
```


---

# The output of the following code:

Integer a = 127;
Integer b = 127;
System.out.println(a == b);

true

false

Compilation error

Runtime error

The correct output is:

```
true
```

**Explanation:**

This question tests the concept of **`Integer` caching** in Java.

1. When you declare `Integer a = 127;` and `Integer b = 127;`, Java uses a feature called autoboxing to convert the primitive `int` literals into `Integer` objects.
2. To save memory and improve performance, Java maintains a cache of `Integer` objects for a specific range of values. By default, this range is from **-128 to 127**.
3. Since the value `127` falls within this cached range, instead of creating two separate `Integer` objects, Java reuses the same object from its cache for both `a` and `b`.
4. The `==` operator, when used with objects, compares their memory addresses (references). Because both `a` and `b` point to the exact same object in the `Integer` cache, the comparison `a == b` evaluates to `true`.

If the value were outside the cache range (e.g., `Integer a = 128; Integer b = 128;`), Java would create two distinct objects on the heap, and `a == b` would evaluate to `false`.

---

# What will be the output of the following code?

int i = 0;
while (i < 3) {
System.out.print(i + " ");
i = 1;
}

1 2 3

0 1 2

0 1 2 3

Infinite loop

The correct answer is:

**Infinite loop**

**Explanation:**

1. **Initialization:** The variable `i` is initialized to `0`.
2. **First Iteration:**
    * The condition `while (i < 3)` is checked. `0 < 3` is `true`.
    * The loop body executes.
    * `System.out.print(i + " ");` prints "0 ".
    * `i = 1;` sets the value of `i` to `1`.
3. **Second Iteration:**
    * The condition `while (i < 3)` is checked again. `1 < 3` is `true`.
    * The loop body executes.
    * `System.out.print(i + " ");` prints "1 ".
    * `i = 1;` sets the value of `i` back to `1`.
4. **Subsequent Iterations:**
    * In every following iteration, the loop will start by checking the condition `1 < 3` (which is always true), print "1 ", and then reset `i` to `1`.

Because the value of `i` is reset to `1` inside the loop and never increments beyond that, the condition `i < 3` will never become false. This creates an infinite loop that continuously prints "1 " after the initial "0 ".

---

# The output of following code:

Integer a = 128;
Integer b = 128;
System.out.println(a == b);

true

false

Compilation error

Runtime error

The correct output is:

```
false
```

**Explanation:**

This question tests a specific detail about how Java handles `Integer` objects through autoboxing, specifically the **`Integer` cache**.

1. **`Integer` Caching:** To improve performance and save memory, Java caches a pool of `Integer` objects for a specific range of values. By default, this range is from **-128 to 127**.
2. **Autoboxing:** When you write `Integer a = 128;`, Java automatically converts the primitive `int` `128` into an `Integer` object.
3. **The Comparison:**
    * The value `128` is **outside** the default cache range of `[-128, 127]`.
    * Because it's outside the range, Java creates a `new Integer(128)` object for the variable `a`.
    * It then creates a *separate, new* `Integer(128)` object for the variable `b`.
    * The `==` operator, when used on objects, compares their memory addresses (references). Since `a` and `b` refer to two different objects in memory, the comparison `a == b` evaluates to `false`.

If the value had been within the cache range (e.g., `127`), both `a` and `b` would have pointed to the exact same cached object, and `a == b` would have been `true`.

---

# One of the following functional interfaces returns a boolean value?

Function<T, R>

Predicate

Supplier

Consumer

The correct answer is **`Predicate`**.

**Explanation:**

Here is a breakdown of the standard functional interfaces listed and what they do:

* **`Function<T, R>`**: Represents a function that takes an argument of type `T` and returns a result of type `R`. Its main method is `R apply(T t)`.
* **`Predicate<T>`**: Represents a function that takes an argument of type `T` and returns a `boolean` value. It is typically used for testing a condition. Its main method is `boolean test(T t)`.
* **`Supplier<T>`**: Represents a function that takes no arguments but produces (supplies) a value of type `T`. Its main method is `T get()`.
* **`Consumer<T>`**: Represents an operation that takes a single argument of type `T` and returns no result (`void`). It is used for its side effects. Its main method is `void accept(T t)`.

Therefore, **`Predicate`** is the functional interface designed to return a boolean.

---

# Output of the following code:

Optional<String> opt = Optional.of("Java");
System.out.println(opt.map(String::toUpperCase).get());

java

JAVA

Optional[JAVA]

Compilation error

The correct output is:

```
JAVA
```

**Explanation:**

1. **`Optional<String> opt = Optional.of("Java");`**: This creates an `Optional` object that "wraps" the non-null string `"Java"`.
2. **`.map(String::toUpperCase)`**: The `map` method is called on the `Optional`.
    * Since the `Optional` is not empty, it applies the provided function (`String::toUpperCase`) to the value it contains (`"Java"`).
    * `"Java".toUpperCase()` results in the string `"JAVA"`.
    * The `map` method returns a new `Optional` containing this result: `Optional<String>` wrapping `"JAVA"`.
3. **`.get()`**: This method is called on the new `Optional` returned by `map`.
    * The `get()` method extracts and returns the value from the `Optional`. In this case, it returns the string `"JAVA"`.
4. **`System.out.println(...)`**: This prints the value returned by `get()`, which is `JAVA`.

---

# The output of the following program:

class Test {
public static void main(String[] args) {
System.out.println("Hello" + 1 + 2);
}
}

Hello3

Hello12

3Hello

Compilation error

The correct output is:

```
Hello12
```

**Explanation:**

In Java, the `+` operator is evaluated from left to right. The behavior of the `+` operator depends on the types of its operands.

1. The expression is ` "Hello" + 1 + 2`.
2. Because of left-to-right associativity, the first operation evaluated is `"Hello" + 1`.
3. When one of the operands is a `String`, the `+` operator performs string concatenation. The integer `1` is converted to its string representation, `"1"`.
4. The result of the first operation is the string `"Hello1"`.
5. The expression now becomes `"Hello1" + 2`.
6. Again, one of the operands is a `String`, so the integer `2` is converted to its string representation, `"2"`.
7. The result is the string `"Hello12"`, which is then printed to the console.

If you wanted to perform the addition first, you would need to use parentheses to change the order of operations: `System.out.println("Hello" + (1 + 2));`, which would print `Hello3`.

---

# Read the given snippet and choose the correct output:

class Demo {
public static void main(String[] args) {
int a;
// System.out.println(a);
}
}

Will print 0

Will throw NullPointerException

Will not compile due to uninitialized variable

Will compile and run fine

The correct answer is:

**Will compile and run fine**

**Explanation:**

In Java, a local variable (a variable declared inside a method) must be initialized before it is used. If you try to read its value without first assigning one, the compiler will generate an error.

However, in this specific code snippet, the line that attempts to use the variable `a` is commented out:

```java
// System.out.println(a);
```

Since the compiler ignores comments, the uninitialized variable `a` is never actually used. Declaring a local variable and not using it is perfectly valid in Java (though some IDEs might show a warning).

Therefore, the code will compile successfully and run without any output or errors.

If the line were not commented out (`System.out.println(a);`), the correct answer would have been **"Will not compile due to uninitialized variable"**.

---

# The output of the following code:

int x = 5;
if (x > 2)
if (x < 4)
System.out.println("A");
else
System.out.println("B");

A

B

Compilation error

No output

The correct output is:

```
B
```

**Explanation:**

This code demonstrates the "dangling else" problem. In Java (and many other languages), an `else` statement always belongs to the nearest preceding `if` statement within the same block that doesn't already have an `else`.

Let's break down the execution:

1. `int x = 5;`: The variable `x` is initialized to 5.
2. `if (x > 2)`: The condition `5 > 2` is `true`. So, the code controlled by this `if` statement will be executed.
3. The statement immediately following the outer `if` is the entire inner `if-else` block:

```java
if (x < 4)
  System.out.println("A");
else // This 'else' belongs to 'if (x < 4)'
  System.out.println("B");
```

4. `if (x < 4)`: The condition `5 < 4` is `false`.
5. Since the inner `if` condition is false, its corresponding `else` block is executed.
6. `System.out.println("B");`: The program prints "B".

Using curly braces makes the logic clearer:

```java
int x = 5;
if (x > 2) {
  if (x < 4) {
    System.out.println("A");
  } else {
    System.out.println("B");
  }
}
```


---

# Which one of the following statements about Java Record is false?

Records are implicitly final

Records extend java.lang.Record

Records can have mutable fields

Records generate equals(), hashCode(), and toString() automatically

The false statement is:

**Records can have mutable fields**

**Explanation:**

A core principle of Java Records is **immutability**. Records are designed to be simple, transparent, and immutable carriers for data.

To enforce this:

* The fields corresponding to the record components (declared in the header) are implicitly `private` and **`final`**.
* The `final` keyword means that once a record object is constructed, the values of its fields cannot be changed.

Let's review why the other statements are true:

* **Records are implicitly final:** A record class cannot be extended (you cannot create a subclass of a record). This is to ensure its behavior, particularly methods like `equals()`, cannot be altered by a subclass, preserving its data-carrier nature.
* **Records extend java.lang.Record:** All records implicitly extend the `java.lang.Record` class. This is similar to how all enums implicitly extend `java.lang.Enum`. Because of this, a record cannot extend any other class.
* **Records generate equals(), hashCode(), and toString() automatically:** This is the primary convenience of records. The compiler automatically generates implementations for a canonical constructor, public accessor methods, and the `equals()`, `hashCode()`, and `toString()` methods based on all the record's components.

