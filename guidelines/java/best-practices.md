# Java Best Practices

This document outlines best practices for writing secure, reliable, and efficient Java code.

## Defensive Programming

22. Minimize the scope of variables.
23. Minimize the scope of the `@SuppressWarnings` annotation.
24. Minimize the accessibility of classes and their members.
25. Document thread-safety and use annotations where applicable.
26. Always provide feedback about the resulting value of a method.
27. Identify files using multiple file attributes.
28. Do not attach significance to the ordinal associated with an `enum`.
29. Be aware of numeric promotion behavior.
30. Enable compile-time type checking of variable arity parameter types.
31. Do not apply `public final` to constants whose value might change in later releases.
32. Avoid cyclic dependencies between packages.
33. Prefer user-defined exceptions over more general exception types.
34. Try to gracefully recover from system errors.
35. Carefully design interfaces before releasing them.
36. Write garbage collection–friendly code.

## Reliability

37. Do not shadow or obscure identifiers in subscopes.
38. Do not declare more than one variable per declaration.
39. Use meaningful symbolic constants to represent literal values in program logic.
40. Properly encode relationships in constant definitions.
41. Return an empty array or collection instead of a `null` value for methods that return an array or collection.
42. Use exceptions only for exceptional conditions.
43. Use a try-with-resources statement to safely handle closeable resources.
44. Do not use assertions to verify the absence of runtime errors.
45. Use the same type for the second and third operands in conditional expressions.
46. Do not serialize direct handles to system resources.
47. Prefer using iterators over enumerations.
48. Do not use direct buffers for short-lived, infrequently used objects.
49. Remove short-lived objects from long-lived container objects.

## Program Understandability

50. Be careful using visually misleading identifiers and literals.
51. Avoid ambiguous overloading of variable arity methods.
52. Avoid in-band error indicators.
53. Do not perform assignments in conditional expressions.
54. Use braces for the body of an `if`, `for`, or `while` statement.
55. Do not place a semicolon immediately following an `if`, `for`, or `while` condition.
56. Finish every set of statements associated with a `case` label with a break statement.
57. Avoid inadvertent wrapping of loop counters.
58. Use parentheses for precedence of operation.
59. Do not make assumptions about file creation.
60. Convert integers to floating-point for floating-point operations.
61. Ensure that the `clone()` method calls `super.clone()`.
62. Use comments consistently and in a readable fashion.
63. Detect and remove superfluous code and values.
64. Strive for logical completeness.
65. Avoid ambiguous or confusing uses of overloading.

## Programmer Misconceptions

66. Do not assume that declaring a reference `volatile` guarantees safe publication of the members of the referenced object.
67. Do not assume that the `sleep()`, `yield()`, or `getState()` methods provide synchronization semantics.
68. Do not assume that the remainder operator always returns a nonnegative result for integral operands.
69. Do not confuse abstract object equality with reference equality.
70. Understand the differences between bitwise and logical operators.
71. Understand how escape characters are interpreted when strings are loaded.
72. Do not use overloaded methods to differentiate between runtime types.
73. Never confuse the immutability of a reference with that of the referenced object.
74. Use the serialization methods `writeUnshared()` and `readUnshared()` with care.
75. Do not attempt to help the garbage collector by setting local reference variables to `null`.


# Effective Java: Best Practices

## Creating and Destroying Objects

### Item 1: Consider static factory methods instead of constructors
- Static factory methods provide named constructors, making the code easier to read and use.
- They allow control over instance creation, enabling instance reuse or returning instances of subclasses.
- Classes without public constructors cannot be subclassed, encouraging immutability.
- Use common naming conventions like `from`, `of`, `valueOf`, `getInstance`, `newInstance`.

### Item 2: Consider a builder when faced with many constructor parameters
- Telescoping constructors are hard to manage with many parameters.
- Use a builder pattern to handle optional parameters while maintaining readability and consistency.
- Builders are particularly effective for immutable objects and hierarchical class structures.

### Item 3: Enforce the singleton property with a private constructor or an enum type
- Use a private constructor with a static instance field or an enum type to enforce a single instance.
- Enum types are more concise and handle serialization correctly.

### Item 4: Enforce noninstantiability with a private constructor
- Use a private constructor for utility classes to prevent instantiation.
- The compiler generates a default public constructor unless explicitly defined.

### Item 5: Prefer dependency injection to hardwiring resources
- Dependency injection increases flexibility and testability.
- Avoid hard-coded dependencies; use frameworks like Spring or Guice for injection.

### Item 6: Avoid creating unnecessary objects
- Reuse immutable objects whenever possible.
- Avoid instantiating objects unnecessarily in loops.

### Item 7: Eliminate obsolete object references
- Nullify object references to eliminate memory leaks.
- Use tools like `try-with-resources` to manage resources effectively.

### Item 8: Avoid finalizers and cleaners
- Finalizers and cleaners are unpredictable and can cause performance issues.
- Use `try-with-resources` or explicit resource management.

### Item 9: Prefer try-with-resources to try-finally
- `try-with-resources` ensures proper resource closure and is less error-prone.
- Use for classes implementing `AutoCloseable`.

---

## Methods Common to All Objects

### Item 10: Obey the general contract when overriding `equals`
- Maintain consistency, reflexivity, symmetry, transitivity, and non-nullity in equality checks.

### Item 11: Always override `hashCode` when you override `equals`
- Failing to do so violates the general contract for `hashCode` and causes issues in hash-based collections.

### Item 12: Always override `toString`
- Provide a human-readable string representation of the object for debugging and logging.

### Item 13: Override `clone` judiciously
- Use `Cloneable` sparingly due to its inconsistent behavior.

### Item 14: Consider implementing `Comparable`
- Implement `Comparable` for natural ordering of objects in collections.

---

## Classes and Interfaces

### Item 15: Minimize the accessibility of classes and members
- Use the lowest possible access level.
- Prefer private or package-private over public unless necessary.

### Item 16: In public classes, use accessor methods, not public fields
- Encapsulation ensures maintainability and flexibility in your code.

### Item 17: Minimize mutability
- Immutable classes are simpler, safer, and thread-safe by default.
- Make all fields final and private.

### Item 18: Favor composition over inheritance
- Inheritance violates encapsulation; use composition and delegation instead.

### Item 19: Design and document for inheritance or else prohibit it
- Document the inheritance behavior to ensure subclassing is safe and predictable.

### Item 20: Prefer interfaces to abstract classes
- Interfaces are more flexible and allow for multiple inheritance.

### Item 21: Design interfaces for posterity
- Anticipate future changes to avoid breaking clients.

### Item 22: Use interfaces only to define types
- Avoid using interfaces to define constants.

### Item 23: Prefer class hierarchies to tagged classes
- Replace tagged classes with proper hierarchies for better clarity and maintainability.

### Item 24: Favor static member classes over nonstatic
- Nonstatic member classes hold an implicit reference to the outer class and can lead to memory leaks.

### Item 25: Limit source files to a single top-level class
- Improves readability and reduces errors.

---

## Generics

### Item 26: Don’t use raw types
- Raw types lose type safety and can result in runtime errors.

### Item 27: Eliminate unchecked warnings
- Suppress warnings with `@SuppressWarnings` and ensure type safety.

### Item 28: Prefer lists to arrays
- Generics work better with collections than arrays due to type mismatch issues.

### Item 29: Favor generic types
- Generic types improve readability and reusability.

### Item 30: Favor generic methods
- Generic methods allow for flexible and type-safe methods.

### Item 31: Use bounded wildcards to increase API flexibility
- Use `? extends` and `? super` for producer/consumer generics.

### Item 32: Combine generics and varargs judiciously
- Ensure type safety when using both generics and varargs.

### Item 33: Consider typesafe heterogeneous containers
- Use typesafe containers for flexibility, e.g., `Class<T>` as keys.

---

## Enums and Annotations

### Item 34: Use enums instead of int constants
- Enums are more readable, type-safe, and maintainable.

### Item 35: Use instance fields instead of ordinals
- Ordinals can lead to errors; use fields to associate data with enums.

### Item 36: Use `EnumSet` instead of bit fields
- `EnumSet` is more flexible and type-safe.

### Item 37: Use `EnumMap` instead of ordinal indexing
- `EnumMap` provides efficient and type-safe mappings for enums.

### Item 38: Emulate extensible enums with interfaces
- Interfaces allow extending enums indirectly.

### Item 39: Prefer annotations to naming patterns
- Annotations are more robust and readable than naming conventions.

### Item 40: Consistently use the `@Override` annotation
- Prevents errors by ensuring methods override superclass methods.

### Item 41: Use marker interfaces to define types
- Marker interfaces are cleaner than marker annotations.
