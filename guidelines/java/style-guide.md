# Java Style Guide

This document provides recommendations for coding style and conventions to ensure consistent and maintainable Java code.

## Security

1. Limit the lifetime of sensitive data.
2. Do not store unencrypted sensitive information on the client side.
3. Provide sensitive mutable classes with unmodifiable wrappers.
4. Ensure that security-sensitive methods are called with validated arguments.
5. Prevent arbitrary file upload.
6. Properly encode or escape output.
7. Prevent code injection.
8. Prevent XPath injection.
9. Prevent LDAP injection.
10. Do not use the `clone()` method to copy untrusted method parameters.
11. Do not use `Object.equals()` to compare cryptographic keys.
12. Do not use insecure or weak cryptographic algorithms.
13. Store passwords using a hash function.
14. Ensure that `SecureRandom` is properly seeded.
15. Do not rely on methods that can be overridden by untrusted code.
16. Avoid granting excess privileges.
17. Minimize privileged code.
18. Do not expose methods that use reduced-security checks to untrusted code.
19. Define custom security permissions for fine-grained security.
20. Create a secure sandbox using a security manager.
21. Do not let untrusted code misuse privileges of callback methods.
