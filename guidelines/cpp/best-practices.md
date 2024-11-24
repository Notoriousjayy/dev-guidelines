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
