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

To transcribe the best practices for Embedded C coding from the document, I'll create a condensed markdown file summarizing the key points from the "best practices" sections of the book. Here's a draft based on the provided structure:

---

### Embedded C Best Practices

#### **General Rules**
- Follow **C99** standards for all programs.
- Limit the line width to **80 characters** for readability and peer reviews.
- Use **braces** even for single-line statements.
- Rely on **parentheses** for clarity in complex expressions.
- Maintain a **table of abbreviations** for consistency and clarity.
- Avoid keywords like `goto` and `continue` unless absolutely necessary.

#### **Commenting**
- Use **clear, complete sentences** for comments with proper grammar.
- Prefer **single-line comments** (//) over block comments (/* ... */).
- Avoid commented-out code; use `#if 0 ... #endif` for disabling code blocks.
- Highlight assumptions and references to external specifications in comments.

#### **Naming Conventions**
- Use descriptive names for variables, functions, and modules.
- **Variables**: Prefix globals with `g_`, pointers with `p_`, and booleans with `b_`.
- **Modules**: Names should be lowercase, with `.h` for headers and `.c` for source files.
- Avoid names overlapping with **standard libraries** or **reserved keywords**.

#### **Data Types**
- Use **fixed-width integers** (`int8_t`, `uint16_t`, etc.) for precise control.
- Avoid bit-fields with signed integers and restrict floating-point use when possible.
- Always use `bool` for boolean values.

#### **Functions**
- Limit function length to **100 lines** or a single printed page.
- Prefer functions with a single exit point and declare unused functions as `static`.
- Use `const` and `volatile` to ensure correct handling of read-only and shared variables.

#### **Code Structure**
- Separate logical blocks with blank lines and align similar code elements.
- Indent code with **4 spaces** instead of tabs for uniformity.
- Define all modules with clear **header and source file templates**.

#### **Error Handling**
- Use `isfinite()` for floating-point checks.
- Avoid unchecked overflows by explicitly managing signed and unsigned types.

#### **Concurrency**
- Suffix **thread** or **task** to functions implementing threads or processes.
- Declare **interrupt service routines (ISRs)** as `static` with `_isr` suffix and ensure they are protected against concurrent execution issues.

#### **Best Practices Summary**
- Code must be maintainable, portable, and free of unnecessary dependencies.
- Always prioritize **readability**, **modularity**, and **safety** in design.

---
Here is a detailed and comprehensive draft for `best-practices.md` based on the Embedded C Coding Standard:

---

# Best Practices for Embedded C Development

This document outlines the best practices for Embedded C development. These practices are based on reducing defects, improving code maintainability, ensuring safety, and fostering collaboration across teams.

---

## **General Rules**

1. **Adopt the C99 Standard:**
   - All programs must comply with the C99 ISO standard to ensure compatibility and access to modern language features.

2. **Line Width:**
   - Limit all lines to a maximum of **80 characters** for readability in reviews and printouts.

3. **Braces Usage:**
   - Always use braces (`{}`) to enclose blocks for `if`, `else`, `while`, `do`, and `for` statements, even for single lines.

4. **Operator Clarity:**
   - Use parentheses to make the order of operations explicit, avoiding reliance on operator precedence.

5. **Keywords to Avoid:**
   - Prohibit the use of `goto` (unless necessary for error handling), `continue`, `auto`, and `register`.

6. **Keywords to Use:**
   - Leverage `const` for read-only variables, `volatile` for hardware/memory-mapped variables, and `static` for module-private variables and functions.

7. **Comment Standards:**
   - Write clear, complete comments using proper grammar. Avoid obvious or redundant explanations.

8. **Documentation Integration:**
   - Use tools like **Doxygen** to generate automatic documentation for functions, variables, and APIs.

---

## **Commenting Rules**

1. **Preferred Formats:**
   - Use single-line comments (`//`) for brief notes.
   - Do not comment out code; use `#if 0` blocks for disabling code temporarily.

2. **Location and Content:**
   - Place comments above the code they describe. Use **TODO**, **NOTE**, or **WARNING** markers to emphasize specific areas.

3. **Assumptions and References:**
   - Document any assumptions or references to external documents, such as specifications or patents.

---

## **Naming Conventions**

1. **Variables:**
   - Use descriptive names:
     - Globals: `g_variable_name`
     - Pointers: `p_variable_name`
     - Booleans: `b_is_condition_met`
   - Avoid short or cryptic names (minimum 3 characters).

2. **Functions:**
   - Use action verbs or questions in names, e.g., `read_sensor()` or `is_device_active()`.

3. **Modules and Files:**
   - Use lowercase names with underscores (e.g., `device_driver.c`).
   - Include "main" in any file with the `main()` function.

4. **Reserved Names:**
   - Avoid names from standard libraries (e.g., `errno`, `strlen`) or reserved keywords.

---

## **Code Organization**

1. **File Structure:**
   - Separate headers (`.h`) and source files (`.c`).
   - Include:
     - Header guards (`#ifndef HEADER_NAME`) for headers.
     - Section markers for constants, variables, functions, etc.

2. **File Templates:**
   - Use predefined templates for all files to ensure consistency.

3. **Block Layout:**
   - Separate logical blocks with blank lines.
   - Place related declarations and definitions together.

---

## **Data Type Rules**

1. **Fixed-Width Integers:**
   - Use `int8_t`, `uint16_t`, etc., for precision. Avoid `short` and `long`.

2. **Booleans:**
   - Declare all Boolean variables as `bool` from `stdbool.h`.

3. **Floating Point:**
   - Minimize floating-point usage. Use fixed-point arithmetic where possible.

4. **Structures and Unions:**
   - Use `typedef` for all structs and unions.
   - Prevent padding issues by validating layout sizes with preprocessor checks.

---

## **Function Rules**

1. **Length and Layout:**
   - Limit function length to one printed page (approx. 100 lines).
   - Use a single `return` statement for clarity.

2. **Prototypes:**
   - Declare all public functions in the corresponding header file.

3. **Thread and ISR Naming:**
   - Name threads with `_thread` suffix and interrupt service routines with `_isr`.

4. **Avoid Function-Like Macros:**
   - Prefer inline functions over macros for better safety and debugging.

---

## **White Space and Formatting**

1. **Indentation:**
   - Use 4 spaces per indentation level. Do not use tabs.

2. **Alignment:**
   - Align variable declarations and assignment operators for readability.

3. **Spacing:**
   - Use spaces around operators (`+`, `=`, etc.) and after keywords (`if`, `for`, etc.).

---

## **Error Handling and Debugging**

1. **Assertions and Validation:**
   - Use `assert()` for debugging and enforce preconditions with comments.

2. **Interrupts:**
   - Handle ISRs carefully to avoid race conditions. ISRs should never block or wait for events.

3. **Floating Point Validations:**
   - Always validate floating-point operations with `isfinite()` to check for NaN or Infinity.

---

## **Concurrency and Multithreading**

1. **Thread Safety:**
   - Use `volatile` for shared variables and protect critical sections with mutexes.

2. **Deadlocks and Race Conditions:**
   - Ensure proper ordering of resource acquisition and release to avoid deadlocks.

---

## **Miscellaneous**

1. **Version Control:**
   - Use meaningful commit messages and follow branching strategies outlined in `version-control/branching-strategy.md`.

2. **Code Reviews:**
   - Enforce all rules via code reviews and automated static analysis tools.

3. **Static Analysis:**
   - Integrate tools to detect violations of coding standards, unused code, and potential bugs.

4. **Tool Configuration:**
   - Configure editors to replace tabs with spaces, enforce line endings, and highlight rule violations.

---

## **Key Takeaways**

1. **Readability Over Convenience:**
   - Prioritize clarity, even if it means more verbose code.

2. **Portability and Safety:**
   - Write code that works consistently across compilers and platforms.

3. **Collaboration:**
   - Maintain consistent practices to enable teamwork and reduce maintenance costs.

---
