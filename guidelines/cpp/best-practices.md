# C++ Best Practices

## Security Principles
- Prefer `std::string` over C-style strings to avoid manual memory management and buffer overflows.
- Always validate input size and type when using standard input/output streams.

---

## Memory Management
- **Smart Pointers:**
  - Use `std::unique_ptr` for ownership semantics and `std::shared_ptr` for shared ownership.
  - Avoid raw pointers wherever possible.

- **Containers:**
  - Use `std::vector` instead of dynamic arrays for automatic memory management.
  - Prefer `std::map` and `std::unordered_map` for associative data storage.

---

## Exception Safety
- Use exception handling (`try-catch`) for robust error management.
- Always catch exceptions by reference:
  ```cpp
  try {
      // code
  } catch (const std::exception& e) {
      std::cerr << e.what() << std::endl;
  }

# C++ Coding Standards: Best Practices

This document highlights the best practices for developing maintainable and high-quality C++ code. It is derived from the 101 rules and guidelines provided in **C++ Coding Standards: 101 Rules, Guidelines, and Best Practices** by Herb Sutter and Andrei Alexandrescu.

---

## Organizational and Policy Issues
1. Don’t sweat the small stuff. (Know what not to standardize.)
2. Compile cleanly at high warning levels.
3. Use an automated build system.
4. Use a version control system.
5. Invest in code reviews.

---

## Design Style
6. Give one entity one cohesive responsibility.
7. Correctness, simplicity, and clarity come first.
8. Know when and how to code for scalability.
9. Don’t optimize prematurely.
10. Don’t pessimize prematurely.
11. Minimize global and shared data.
12. Hide information.
13. Know when and how to code for concurrency.
14. Ensure resources are owned by objects. Use explicit RAII and smart pointers.

---

## Coding Style
15. Prefer compile- and link-time errors to runtime errors.
16. Use `const` proactively.
17. Avoid macros.
18. Avoid magic numbers.
19. Declare variables as locally as possible.
20. Always initialize variables.
21. Avoid long functions. Avoid deep nesting.
22. Avoid initialization dependencies across compilation units.
23. Minimize definitional dependencies. Avoid cyclic dependencies.
24. Make header files self-sufficient.
25. Always write internal `#include` guards. Never write external `#include` guards.

---

## Functions and Operators
26. Take parameters appropriately by value, (smart) pointer, or reference.
27. Preserve natural semantics for overloaded operators.
28. Prefer the canonical forms of arithmetic and assignment operators.
29. Prefer the canonical form of `++` and `--`. Prefer calling the prefix forms.
30. Consider overloading to avoid implicit type conversions.
31. Avoid overloading `&&`, `||`, `,` (comma).
32. Don’t write code that depends on the order of evaluation of function arguments.

---

## Class Design and Inheritance
33. Be clear about the kind of class you’re writing.
34. Prefer minimal classes to monolithic classes.
35. Prefer composition to inheritance.
36. Avoid inheriting from classes that were not designed to be base classes.
37. Prefer providing abstract interfaces.
38. Public inheritance is substitutability. Inherit, not to reuse, but to be reused.
39. Practice safe overriding.
40. Consider making virtual functions nonpublic, and public functions nonvirtual.
41. Avoid providing implicit conversions.
42. Make data members private, except in behaviorless aggregates (C-style structs).
43. Don’t give away your internals.
44. Use the Pimpl idiom judiciously.
45. Prefer writing nonmember nonfriend functions.
46. Always provide `new` and `delete` together.
47. If you provide any class-specific `new`, provide all of the standard forms (plain, in-place, and `nothrow`).

---

## Construction, Destruction, and Copying
48. Define and initialize member variables in the same order.
49. Prefer initialization to assignment in constructors.
50. Avoid calling virtual functions in constructors and destructors.
51. Make base class destructors public and virtual, or protected and nonvirtual.
52. Destructors, deallocation, and `swap` never fail.
53. Copy and destroy consistently.
54. Explicitly enable or disable copying.
55. Avoid slicing. Consider `Clone` instead of copying in base classes.
56. Prefer the canonical form of assignment.
57. Whenever it makes sense, provide a no-fail `swap` (and provide it correctly).

---

## Namespaces and Modules
58. Keep a type and its nonmember function interface in the same namespace.
59. Keep types and functions in separate namespaces unless they’re specifically intended to work together.
60. Don’t write namespace `using` in a header file or before an `#include`.
61. Avoid allocating and deallocating memory in different modules.
62. Don’t define entities with linkage in a header file.
63. Don’t allow exceptions to propagate across module boundaries.
64. Use sufficiently portable types in a module’s interface.

---

## Templates and Genericity
65. Blend static and dynamic polymorphism judiciously.
66. Customize intentionally and explicitly.
67. Don’t specialize function templates.
68. Don’t write unintentionally nongeneric code.

---

## Error Handling and Exceptions
69. Assert liberally to document internal assumptions and invariants.
70. Establish a rational error-handling policy, and follow it strictly.
71. Distinguish between errors and non-errors.
72. Design and write error-safe code.
73. Prefer to use exceptions to report errors.
74. Throw by value, catch by reference.
75. Report, handle, and translate errors appropriately.
76. Avoid exception specifications.

---

## STL: Containers
77. Use `vector` by default. Otherwise, choose an appropriate container.
78. Use `vector` and `string` instead of arrays.
79. Use `vector` (and `string::c_str`) to exchange data with non-C++ APIs.
80. Store only values and smart pointers in containers.
81. Prefer `push_back` to other ways of expanding a sequence.
82. Prefer range operations to single-element operations.
83. Use the accepted idioms to really shrink capacity and really erase elements.

---

## STL: Algorithms
84. Use a checked STL implementation.
85. Prefer algorithm calls to handwritten loops.
86. Use the right STL search algorithm.
87. Use the right STL sort algorithm.
88. Make predicates pure functions.
89. Prefer function objects over functions as algorithm and comparer arguments.
90. Write function objects correctly.

---

## Type Safety
91. Avoid type switching; prefer polymorphism.
92. Rely on types, not on representations.
93. Avoid using `reinterpret_cast`.
94. Avoid using `static_cast` on pointers.
95. Avoid casting away `const`.
96. Don’t use C-style casts.
97. Don’t `memcpy` or `memcmp` non-PODs.
98. Don’t use unions to reinterpret representation.
99. Don’t use varargs (`ellipsis`).
100. Don’t use invalid objects. Don’t use unsafe functions.
101. Don’t treat arrays polymorphically.

# Best Practices for C++ Development in Critical Systems

This document outlines comprehensive best practices derived from the MISRA C++:2023 guidelines for using C++17 in safety-critical and security-critical systems. These guidelines are intended to enhance reliability, maintainability, and robustness in software design and implementation.

---

## General Principles

### 1. Use a Predictable Subset of C++
- Adopt MISRA C++ as a subset of the C++17 standard.
- Avoid reliance on undefined, unspecified, implementation-defined, and conditionally supported behavior.
- Use static analysis tools to detect violations and enforce compliance.

### 2. Emphasize Code Safety and Security
- Avoid constructs that introduce safety risks, such as uninitialized variables, unchecked operations, or invalid memory access.
- Adhere to the principle of least privilege in all code design decisions.

### 3. Ensure Consistency and Readability
- Follow a consistent style guide for variable naming, indentation, and layout.
- Modularize code into small, well-defined functions with single responsibilities.

---

## Best Practices for Language Features

### Avoid Undefined and Unspecified Behavior
**Rule 0.0.1**: Functions shall not contain unreachable statements.
- **Rationale**: Unreachable code often indicates a logical error and makes maintenance harder.
- **Compliant Example**:
  ```cpp
  int calculate(int value) {
      if (value > 0) {
          return value * 2;
      }
      return 0;
  }
  ```
- **Non-compliant Example**:
  ```cpp
  int calculate(int value) {
      return 0;
      value++; // Unreachable code
  }
  ```

---

### Avoid Excessive Use of Implementation-Defined Features
**Guideline**: Minimize dependency on compiler-specific behavior for better portability and maintainability.
- **Best Practice**:
  - Document all assumptions about compiler behavior explicitly.
  - Use portable libraries and abstractions where possible.

---

## Best Practices for Code Quality

### 1. Minimize Unused Declarations
**Rule 0.2.1**: Variables with limited visibility should be used at least once.
- **Rationale**: Unused declarations add noise to the code and may lead to confusion or maintenance errors.
- **Example**:
  ```cpp
  namespace {
      int value = 42; // Non-compliant if unused
  }

  void process(int a) {
      [[maybe_unused]] bool flag = (a > 0); // Compliant with attribute
      assert(flag);
  }
  ```

### 2. Avoid Writing to Unused Objects
**Rule 0.1.1**: A value should not be unnecessarily written to a local object.
- **Rationale**: Writing to variables without observing their values wastes resources and might indicate logic errors.
- **Example**:
  ```cpp
  int process() {
      int temp = 0; // Non-compliant if temp is not used
      return 0;
  }
  ```

---

## Best Practices for Floating-Point Arithmetic

### Ensure Numerical Stability
**Directive 0.3.1**: Use floating-point operations carefully to avoid precision loss or overflow.
- Validate inputs and handle special cases such as NaN and infinity explicitly.
- **Example**:
  ```cpp
  float compute(float value) {
      if (std::isnan(value)) {
          throw std::invalid_argument("NaN encountered");
      }
      return value * 2.0f;
  }
  ```

---

## Best Practices for Exception Handling

### Use Exception Handling Judiciously
**Rule 4.18**: Exceptions should not introduce runtime instability or obscure program flow.
- **Compliant Example**:
  ```cpp
  try {
      performOperation();
  } catch (const SpecificError& e) {
      handleError(e);
  } catch (...) {
      logGeneralError();
  }
  ```
- **Non-compliant Example**:
  ```cpp
  try {
      performOperation();
  } catch (...) {
      // Catch-all with no logging or handling
  }
  ```

---

## Best Practices for Type Safety

### Use Explicit Type Conversions
**Rule 6.7.4**: Avoid implicit conversions that might lead to data loss or undefined behavior.
- **Compliant Example**:
  ```cpp
  float value = 42.0f;
  int result = static_cast<int>(value); // Explicit cast
  ```
- **Non-compliant Example**:
  ```cpp
  float value = 42.0f;
  int result = value; // Implicit cast
  ```

---

## Best Practices for Resource Management

### Use RAII for Resource Safety
- Encapsulate resource management using constructors and destructors to ensure deterministic cleanup.
- **Example**:
  ```cpp
  class ResourceHandler {
  public:
      ResourceHandler() { acquireResource(); }
      ~ResourceHandler() { releaseResource(); }
  };
  ```

---

## Best Practices for Multi-threading

### Avoid Data Races
**Rule 4.12.1**: Synchronize shared resources to avoid data races.
- **Compliant Example**:
  ```cpp
  std::mutex mutex;
  void safeIncrement(int& counter) {
      std::lock_guard<std::mutex> lock(mutex);
      ++counter;
  }
  ```

---

## Documentation Practices

### Use Consistent Commenting Style
- Provide meaningful comments for complex logic, exceptions, and assumptions.
- Avoid redundant comments that merely restate the code.

---

## References
- **MISRA C++: 2023** Guidelines.
- ISO/IEC 14882:2017 (C++17 Standard).
- Industry standards such as IEC 61508, ISO 26262.

---

### Notes
This document is a living guideline, intended to evolve with project needs and updates to coding standards. All team members should follow these practices and contribute suggestions for improvement.

This document is comprehensive and includes key examples, rationales, and rules based on the MISRA guidelines. It can be further expanded or customized to align with project-specific coding conventions.
