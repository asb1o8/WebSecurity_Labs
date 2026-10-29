
# Path Traversal

## 1. What Is Path Traversal?

Path traversal is a vulnerability that allows an attacker to manipulate file paths to access files outside the intended directory.

## 2. Example: Image Loading Application

Suppose an application loads images using the following URL:

```http
GET /loadImage?filename=218.png
```

Images are stored in:

```text
/var/www/images/
```

The application should only allow access to files within this directory.

### Normal Request

```text
/loadImage?filename=218.png
```

Resolved path:

```text
/var/www/images/218.png
```

### Malicious Request

```http
GET /loadImage?filename=../../../etc/passwd
```

The `../` sequences move up one directory level at a time.

Resolved path:

```text
/etc/passwd
```

On a vulnerable Linux server, this could expose the `/etc/passwd` file, which contains account information.

## 3. Windows Path Traversal

Windows applications may also be vulnerable to path traversal.

Example:

```http
GET /loadImage?filename=..\..\..\Windows\win.ini
```

Potential target:

```text
C:\Windows\win.ini
```

The exact result depends on how the application processes the path.

## 4. Common Path Traversal Patterns

### Basic Traversal

```text
../../../etc/passwd
```

### Windows Traversal

```text
..\..\..\Windows\win.ini
```

### URL-Encoded Traversal

```text
%2e%2e%2f%2e%2e%2fetc%2fpasswd
```

### Double URL-Encoded Traversal

```text
%252e%252e%252f
```

These variations may work only when the application decodes or processes the input in a vulnerable way.

## 5. Security Impact

Depending on the vulnerability and the server's permissions, path traversal may allow attackers to:

- Read sensitive configuration files.
- Access application source code or credentials.
- Expose system information.
- Access files outside the intended directory.
- Modify files if a separate writable-file operation is vulnerable.

Path traversal does not automatically provide shell access or remote code execution.

## 6. Prevention

- Canonicalize file paths and verify that they remain inside the permitted directory.
- Prefer server-side file identifiers over user-controlled filesystem paths.
- Apply strict allowlists and input validation.
- Restrict filesystem permissions using least privilege.
- Avoid relying only on blocking `../`, since alternative encodings and path formats may bypass simplistic filters.

**Key takeaway:** Path traversal occurs when an application fails to properly restrict user-controlled file paths to the intended directory.
