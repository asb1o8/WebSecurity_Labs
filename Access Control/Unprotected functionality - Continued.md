
## Unprotected Functionality – Continued

### Security Through Obscurity

Some applications hide sensitive functionality by using unpredictable URLs. This approach is known as **security through obscurity**.

However, hiding an administrative URL does not provide effective access control because attackers may discover it through other sources.

### Example

An application hosts its administrative panel at:

```text
https://insecure-website.com/administrator-panel-yb556
```

Although the URL is difficult to guess, it may still be exposed in the application's JavaScript code.

```javascript
var isAdmin = false;

if (isAdmin) {
    var adminPanelTag = document.createElement('a');
    adminPanelTag.setAttribute(
        'href',
        'https://insecure-website.com/administrator-panel-yb556'
    );
    adminPanelTag.innerText = 'Admin panel';
}
```

### Key Observation

- The script displays the admin panel link only to administrators.
- However, the JavaScript source code is visible to all users.
- Therefore, non-administrative users can discover the hidden admin URL by inspecting the client-side code.

**Key Takeaway:** Hiding or obfuscating URLs is not access control. Applications must enforce proper server-side authorization checks.
