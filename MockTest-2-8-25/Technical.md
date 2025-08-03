Here is the content formatted neatly.

-----

## `Arrays.toString()` Output

### Question

Select the correct output for the given code:

```java
int[] arr = {10, 20, 30};
System.out.println(Arrays.toString(arr));
```

  * `10, 20, 30`
  * `[10, 20, 30]`
  * `{10, 20, 30}`
  * `Compilation error`

### Answer ✅

The correct output is **`[10, 20, 30]`**.

#### Explanation

The `Arrays.toString()` method in Java returns a string representation of an array's contents. The format is a comma-separated list of the elements, enclosed in square brackets (`[]`).

-----

## Identifying Java Keywords

### Question

One of the following is **not** a Java keyword:

  * `static`
  * `void`
  * `null`
  * `volatile`

### Answer ✅

The correct answer is **`null`**.

#### Explanation

  * **`static`**, **`void`**, and **`volatile`** are all reserved keywords in Java.
  * **`null`** is a special literal, not a keyword. It represents a reference that does not point to any object. While it has special meaning, it's technically classified as a literal, similar to `true` and `false`.

-----

## `ArrayList` Insertion

### Question

Select the correct output for the given code:

```java
import java.util.ArrayList;

ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
list.add(1, 15);
System.out.println(list);
```

  * `[10, 15, 20]`
  * `[10, 20, 15]`
  * `[10, 15]`
  * `Compilation error`

### Answer ✅

The correct output is **`[10, 15, 20]`**.

#### Explanation

1.  `list` starts as `[]`.
2.  `list.add(10);` makes it `[10]`.
3.  `list.add(20);` makes it `[10, 20]`.
4.  `list.add(1, 15);` inserts `15` at index `1`. The element at index `1` (`20`) is shifted to the right.
5.  The final list is `[10, 15, 20]`.

-----

## String Reference Comparison

### Question

What is the output of the following code?

```java
String s1 = "Java";
String s2 = new String("Java");
System.out.println(s1 == s2);
```

  * `true`
  * `false`
  * `Compilation error`
  * `java`

### Answer ✅

The correct output is **`false`**.

#### Explanation

  * `String s1 = "Java";` creates a string in the **String Constant Pool**.
  * `String s2 = new String("Java");` uses the `new` keyword to create a **new object** on the heap, separate from the pool.
  * The `==` operator compares object references (memory addresses). Since `s1` and `s2` refer to different objects in different memory locations, the result is `false`. To compare their content, you would use `s1.equals(s2)`.

-----

## `do-while` Loop Properties

### Question

One of the following is true about the `do-while` loop in Java:

  * It checks the condition before execution.
  * It guarantees the loop runs at least once.
  * It is not supported in Java.
  * It can never be infinite.

### Answer ✅

The correct statement is: **It guarantees the loop runs at least once.**

#### Explanation

A `do-while` loop is a **post-test loop**. It executes the loop body *first* and then checks the condition. Because the condition is checked after the first pass, the loop body is guaranteed to execute at least one time, even if the condition is initially false.

-----

## Java Stream Consumption

### Question

What does this code print when executed?

```java
import java.util.stream.Stream;

Stream<Integer> stream = Stream.of(1, 2, 3, 4);
stream.filter(x -> x % 2 == 0);
stream.forEach(System.out::print);
```

  * `24`
  * `1234`
  * `Compilation error`
  * `IllegalStateException` at runtime

### Answer ✅

The code will throw a runtime **`IllegalStateException`**.

#### Explanation

The key principle of Java Streams is that **a stream can only be operated on once**.

1.  `stream.filter(...)` is an intermediate operation that consumes the original `stream`. The result (a new stream) is discarded because it's not assigned to a variable.
2.  `stream.forEach(...)` then attempts to operate on the original `stream` variable, which has already been consumed.
3.  This causes the Java runtime to throw an `IllegalStateException` with the message "stream has already been operated upon or closed."

To get the intended output (`24`), the operations must be chained:

```java
Stream.of(1, 2, 3, 4)
      .filter(x -> x % 2 == 0)
      .forEach(System.out::print); // Prints "24"
```

-----

## `Integer` Caching (Within Range)

### Question

What is the output of the following code?

```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b);
```

  * `true`
  * `false`
  * `Compilation error`
  * `Runtime error`

### Answer ✅

The correct output is **`true`**.

#### Explanation

Java maintains a cache of `Integer` objects for values from **-128 to 127**. When autoboxing an `int` literal within this range, Java reuses the same object from its cache. Since `127` is in the cached range, both `a` and `b` point to the exact same object in memory, so `a == b` is `true`.

-----

## Infinite `while` Loop

### Question

What will be the output of the following code?

```java
int i = 0;
while (i < 3) {
    System.out.print(i + " ");
    i = 1;
}
```

  * `1 2 3`
  * `0 1 2`
  * `0 1 2 3`
  * `Infinite loop`

### Answer ✅

The correct answer is an **Infinite loop**.

#### Explanation

1.  **First iteration:** `i` is `0`. The loop prints "0 " and then sets `i` to `1`.
2.  **Second iteration:** `i` is `1`. The loop prints "1 " and then resets `i` to `1`.
3.  **Subsequent iterations:** The value of `i` is always reset to `1`, so the condition `i < 3` is always true. The loop will continuously print "1 " after the initial "0 ".

-----

## `Integer` Caching (Outside Range)

### Question

What is the output of the following code?

```java
Integer a = 128;
Integer b = 128;
System.out.println(a == b);
```

  * `true`
  * `false`
  * `Compilation error`
  * `Runtime error`

### Answer ✅

The correct output is **`false`**.

#### Explanation

Java caches `Integer` objects for values from -128 to 127. The value `128` is **outside** this range. Therefore, Java creates two distinct `Integer` objects on the heap for `a` and `b`. Since `a` and `b` refer to different objects, the `==` comparison evaluates their memory addresses, which are different, resulting in `false`.

-----

## Functional Interfaces

### Question

Which one of the following functional interfaces returns a `boolean` value?

  * `Function<T, R>`
  * `Predicate<T>`
  * `Supplier<T>`
  * `Consumer<T>`

### Answer ✅

The correct answer is **`Predicate<T>`**.

#### Explanation

  * **`Predicate<T>`** is specifically designed to test a condition. Its functional method is `boolean test(T t)`, which takes an argument and returns a `boolean`.
  * **`Function<T, R>`** takes a `T` and returns an `R`.
  * **`Supplier<T>`** takes nothing and returns a `T`.
  * **`Consumer<T>`** takes a `T` and returns nothing (`void`).

-----

## `Optional` Method Chaining

### Question

What is the output of the following code?

```java
import java.util.Optional;

Optional<String> opt = Optional.of("Java");
System.out.println(opt.map(String::toUpperCase).get());
```

  * `java`
  * `JAVA`
  * `Optional[JAVA]`
  * `Compilation error`

### Answer ✅

The correct output is **`JAVA`**.

#### Explanation

1.  `Optional.of("Java")` creates an `Optional` containing the string `"Java"`.
2.  `.map(String::toUpperCase)` applies the `toUpperCase` function to the contained value, returning a new `Optional` containing `"JAVA"`.
3.  `.get()` extracts the value from this new `Optional`.
4.  The extracted value, `"JAVA"`, is printed.

-----

## String Concatenation Precedence

### Question

What is the output of the following program?

```java
class Test {
    public static void main(String[] args) {
        System.out.println("Hello" + 1 + 2);
    }
}
```

  * `Hello3`
  * `Hello12`
  * `3Hello`
  * `Compilation error`

### Answer ✅

The correct output is **`Hello12`**.

#### Explanation

In Java, the `+` operator is evaluated from left to right.

1.  `"Hello" + 1` is evaluated first. Since one operand is a `String`, this becomes string concatenation, resulting in `"Hello1"`.
2.  The expression becomes `"Hello1" + 2`. This is also string concatenation, resulting in `"Hello12"`.

To perform addition first, use parentheses: `System.out.println("Hello" + (1 + 2));` would print `Hello3`.

-----

## Uninitialized Local Variables

### Question

Read the given snippet and choose the correct output:

```java
class Demo {
    public static void main(String[] args) {
        int a;
        // System.out.println(a);
    }
}
```

  * Will print `0`
  * Will throw `NullPointerException`
  * Will not compile due to uninitialized variable
  * Will compile and run fine

### Answer ✅

The correct answer is: **Will compile and run fine.**

#### Explanation

A local variable must be initialized before it is **used**. In this code, the line that would use `a` (`System.out.println(a);`) is commented out. Since the compiler ignores comments, the uninitialized variable `a` is declared but never used. This is perfectly valid, so the code compiles and runs without error.

-----

## Dangling `else`

### Question

What is the output of the following code?

```java
int x = 5;
if (x > 2)
    if (x < 4)
        System.out.println("A");
    else
        System.out.println("B");
```

  * `A`
  * `B`
  * `Compilation error`
  * `No output`

### Answer ✅

The correct output is **`B`**.

#### Explanation

This demonstrates the "dangling else" problem. An `else` clause always binds to the nearest `if` statement that doesn't already have one. Here, the `else` belongs to `if (x < 4)`.

1.  `if (x > 2)`: `5 > 2` is `true`. The program proceeds.
2.  `if (x < 4)`: `5 < 4` is `false`.
3.  The program skips the `if` block and executes its corresponding `else` block, printing "B".

-----

## Java Record Properties

### Question

Which one of the following statements about Java Records is **false**?

  * Records are implicitly `final`.
  * Records extend `java.lang.Record`.
  * Records can have mutable fields.
  * Records generate `equals()`, `hashCode()`, and `toString()` automatically.

### Answer ✅

The false statement is: **Records can have mutable fields.**

#### Explanation

A core feature of Java Records is **immutability**. The fields declared in a record's header are implicitly `private` and **`final`**, meaning their values cannot be changed after the object is created. The other three statements are all true properties of records.