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
