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
