# C Best Practices

## Security Principles
- **Input Validation:**
  - Use secure functions like `fgets()` instead of `gets()` to prevent buffer overflows.
  - Validate input length and format before processing.
  - Avoid trusting input from unverified sources.

- **Secure String Handling:**
  - Use `strncpy()` instead of `strcpy()` to avoid buffer overflows.
  - Always null-terminate strings explicitly if needed.

- **Avoid Hardcoded Secrets:**
  - Use secure storage mechanisms (e.g., environment variables) instead of embedding secrets directly in code.

---

## Memory Safety
- **Memory Allocation:**
  - Prefer `calloc()` over `malloc()` to zero-initialize memory and reduce vulnerabilities due to uninitialized memory access.
  - Free dynamically allocated memory with `free()` and ensure double-free vulnerabilities are avoided.

- **Buffer Safety:**
  - Avoid off-by-one errors by ensuring buffer bounds checks.
  - Use functions like `memcpy_s()` and `strncpy()` for safer memory copying.

- **Pointer Safety:**
  - Always initialize pointers to `NULL` and check before dereferencing.
  - Avoid pointer arithmetic unless absolutely necessary, and validate the resulting pointer.

---

## Error Handling
- **Use Return Codes:**
  - Check the return values of all standard library functions.
  - For critical functions, log and handle errors explicitly.

- **`errno` Management:**
  - Reset `errno` before operations that may fail and check its value afterwards.
  - Avoid overwriting `errno` unintentionally.

---

## Compiler Settings
- **Recommended Compiler Flags:**
  - `-Wall -Wextra -Wpedantic` for GCC/Clang to catch common coding errors.
  - `-fsanitize=address` to detect memory corruption issues.

- **Standards Conformance:**
  - Use `-std=c99` or later to ensure modern C practices and compatibility.

---

## File I/O
- **Avoid Vulnerable Functions:**
  - Replace `sprintf()` with `snprintf()` to prevent buffer overflows.
  - Always validate file handles before performing read/write operations.

- **Safe File Access:**
  - Use `fopen_s()` instead of `fopen()` on platforms where it's available.
  - Avoid hardcoding file paths; use configurable parameters instead.

---

## Integer Safety
- **Prevent Overflow:**
  - Use `size_t` for array indices and avoid signed integer overflow.
  - Validate ranges before performing arithmetic operations.

- **Avoid Truncation:**
  - Use explicit casting to prevent truncation during type conversion.
Here is a more thorough and comprehensive version of the `best-practices.md` file, based on MISRA C:2023 guidelines. This version includes details across all relevant areas with examples and justifications.

# Best Practices for C Programming in Critical Systems

## Overview
This document outlines best practices derived from MISRA C:2023 for developing safe, secure, and portable C programs in critical systems. These guidelines ensure compliance with safety, security, and reliability requirements.

---

## General Principles

### Adherence to Standards
- Use a defined subset of the C language to reduce ambiguity and potential programming errors.
- Eliminate or mitigate undefined and implementation-specific behaviors.
- Follow mandatory, required, and advisory guidelines as outlined by MISRA C.

### Documentation and Traceability
- All implementation-defined behaviors that affect program output **must** be documented and thoroughly understood.
- Ensure every piece of code is traceable to specific, documented requirements to eliminate unnecessary or unintentional functionality.

---

## Code Design and Development

### Robustness Against Failures
- Perform **dynamic checks** to minimize run-time errors:
  - Ensure array indices are within bounds before accessing.
  - Validate all pointers before dereferencing.
  - Guard against arithmetic errors such as overflow, underflow, or divide-by-zero.
- Provide clear documentation for areas where dynamic checks are omitted, supported by static analysis or design assumptions.

### Encapsulation
- Encapsulate assembly language within macros or inline functions for portability and maintainability.
- Use opaque data types to hide implementation details and reduce unintentional modifications.

### Use of Typedefs
- Replace basic types (`int`, `float`, etc.) with specific-length typedefs (`int32_t`, `uint8_t`) to ensure predictable memory use.
- Avoid defining types that do not match their intended size or signedness.

---

## Use of Libraries and Functions

### Validation of Inputs
- Validate all inputs passed to library functions, including those in the Standard Library and custom libraries.
- Examples:
  - Check that arguments to `sqrt` are non-negative.
  - Ensure the second argument of `fmod` is non-zero.

### Error Handling
- Test all error information returned by functions immediately after execution.
- If error testing is not required due to pre-validation, document this explicitly.

### Avoid Function-Like Macros
- Prefer inline functions over function-like macros to ensure argument type-checking and prevent multiple evaluations of macro arguments.

---

## Memory Management

### Avoid Dynamic Allocation
- Avoid using dynamic memory allocation (`malloc`, `free`) in critical systems to prevent undefined behaviors such as memory leaks or invalid access.

---

## File and Header Management

### Prevent Multiple Inclusions
- Use include guards to prevent the same header file from being included multiple times:
  ```c
  #ifndef HEADER_NAME
  #define HEADER_NAME
  // Header content
  #endif
  ```

### Consistent Naming
- Use meaningful, typographically unambiguous names for identifiers:
  - Avoid `O` vs. `0`, `l` vs. `1`, `I` vs. `l`.
  - Prefer descriptive names with underscores or camelCase for clarity.

---

## Concurrency and Synchronization

### Concurrency Awareness
- Design for thread safety when using C11/C18 threading features.
- Avoid race conditions by using synchronization primitives such as mutexes or atomics.

### Minimize Shared Resources
- Encapsulate shared resources and use controlled access patterns to ensure consistency.

---

## Static Analysis and Tools

### Leverage Analysis Tools
- Use static analysis tools capable of checking MISRA C compliance. Ensure these tools are correctly configured for the project.
- Address all reported violations, especially for mandatory and required rules.

### Scope of Analysis
- Analyze both system-level and translation-unit-level code for full coverage of rules and guidelines.

---

## Example Implementations

### Avoiding Undefined Behavior
**Non-compliant Example:**
```c
int x = 0;
if (x = 1) { // Mistake: assignment instead of comparison
    // Code
}
```

**Compliant Example:**
```c
int x = 0;
if (x == 1) { // Correct: comparison operator
    // Code
}
```

### Validating Inputs
**Non-compliant Example:**
```c
double result = sqrt(-1); // Invalid input for sqrt
```

**Compliant Example:**
```c
if (value >= 0) {
    double result = sqrt(value);
} else {
    // Handle error
}
```

---

## Exceptions and Deviations

### Formal Documentation of Deviations
- If deviations from mandatory or required guidelines are necessary, document them formally as per MISRA Compliance processes.
- Justify deviations with clear reasoning, impact analysis, and any mitigating strategies.

---

## Advanced Topics

### Automatically Generated Code
- Ensure code generated by tools adheres to MISRA C where applicable.
- Validate the configuration and behavior of code-generation tools to ensure compliance.

### Multi-Organization Collaboration
- For shared projects, define a unified compliance strategy and agree on coding standards upfront.
- When sharing precompiled libraries, provide documentation or compliance declarations.

---

## Summary of Key Rules

| Guideline                        | Type       | Importance |
|----------------------------------|------------|------------|
| Validate all input values        | Mandatory  | High       |
| Use specific-length typedefs     | Required   | High       |
| Avoid dynamic memory allocation  | Required   | High       |
| Encapsulate assembly instructions | Advisory  | Medium     |

---

## References

- MISRA C:2023, Guidelines for the use of the C language in critical systems.
- IEC 61508:2010, Functional Safety of Electrical/Electronic/Programmable Electronic Safety-related Systems.
- ISO 26262:2018, Road Vehicles – Functional Safety.

---

This document is intended as a living reference and should be updated periodically to reflect project-specific requirements or updates to MISRA guidelines.

This file is structured comprehensively, covering general principles, code design, and advanced considerations with specific examples and actionable advice. Let me know if you need any further refinements!

Here’s a comprehensive and thorough example for `best-practices.md` based on the **MISRA C++:2023 Guidelines**. The document will be aligned to cover all critical aspects, including examples, rationale, and exceptions where applicable.

### Complete `best-practices.md`

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
