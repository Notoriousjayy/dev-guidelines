### **C++: Updated `style-guide.md`**

# C++ Style Guide

## Formatting
- Use 4 spaces for indentation.
- Place braces `{}` on their own line for classes and methods.
- Align `*` and `&` with the variable name:
  ```cpp
  int* ptr; // Recommended
  
## Naming Conventions
- Variables and functions: `camelCase`
- Classes: `PascalCase`
- Constants: `UPPER_SNAKE_CASE`

---

## Modern C++ Practices
- Use `auto` for type inference where appropriate:
  ```cpp
  auto sum = a + b;
  for (auto& element : container) {
    // Logic
  }

# C++ Coding Standards: Style Guide

This document outlines style guidelines for writing consistent and readable C++ code.

---

## General Style
- Prefer readable and consistent naming conventions.
- Avoid deeply nested structures for readability.
- Maintain a consistent indentation style across files.
- Use self-documenting variable and function names.

## Comments
- Use comments to explain the "why," not the "what."
- Document complex logic with clear comments.
- Avoid redundant comments that duplicate what the code states.

## Code Structure
- Limit the length of files and functions.
- Group related functions and classes logically.
- Separate interface (header files) from implementation.

## Naming Conventions
- Use `PascalCase` for class names.
- Use `camelCase` for variables and functions.
- Prefix member variables with `m_` or an equivalent convention.

## Header Files
- Include necessary `#include` guards.
- Minimize includes in headers to reduce dependencies.

