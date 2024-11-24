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
