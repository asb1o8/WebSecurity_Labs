
## Unprotected Functionality

Unprotected functionality occurs when an application fails to enforce access restrictions on sensitive features, allowing unauthorized users to access them.

For example, administrative functions may be linked only from an administrator's dashboard, but this does not prevent regular users from accessing them directly through the admin URL.

### Example

An application hosts administrative functionality at:

```text
https://insecure-website.com/admin
```

If proper access controls are missing, any user may be able to access this URL, not just administrators.

### Discovering Unprotected Functionality

- **Direct URL Access:** An attacker may manually browse to the administrative URL.
- **robots.txt:** The administrative URL may be disclosed in the `robots.txt` file.

  ```text
  https://insecure-website.com/robots.txt
  ```

- **Wordlist Brute-Forcing:** An attacker may use a wordlist to discover hidden administrative endpoints.

**Key Takeaway:** Hiding administrative links does not provide security. Applications must enforce server-side authorization checks on every sensitive function.
