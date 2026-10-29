
## What Is Path Traversal?

**Path Traversal (Directory Traversal)** is a vulnerability that allows attackers to access files outside an application's intended directory by manipulating file paths.

### What Can an Attacker Access?

- **Application files:** Source code and application data.
- **Credentials:** Passwords, API keys, and configuration files.
- **System files:** Sensitive operating-system information.
- **Other files:** In some cases, files may be modified or overwritten.

### What Are Arbitrary Files?

**Arbitrary files** means files the attacker can target beyond those the application is intended to provide access to. Actual access depends on the application's permissions and security controls.

### Example

```text
Normal request:
/download?file=report.pdf

Path traversal attempt:
/download?file=../../../../etc/passwd
```

The `../` sequences attempt to navigate to parent directories and reach a file outside the permitted location.

**Impact:** Sensitive data exposure, unauthorized file modification, and potentially further server compromise.
