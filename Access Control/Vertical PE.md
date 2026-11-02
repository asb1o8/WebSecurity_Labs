
# Vertical Privilege Escalation

## 1. What Is Vertical Privilege Escalation?

Vertical privilege escalation occurs when a user gains access to functionality or privileges assigned to a higher-privileged user or role.

In simple terms, a user with lower privileges performs actions that should only be available to users with higher privileges.

## 2. Example

Consider a web application with two user roles:

- **Regular User:** Can view and manage their own account.
- **Administrator:** Can manage users, delete accounts, and access administrative functionality.

If a regular user can access an administrative page and delete other users' accounts, this indicates a potential vertical privilege escalation vulnerability.

## 3. Security Impact

Depending on the privileges obtained, an attacker may be able to:

- Access administrative functionality.
- Modify or delete other users' accounts.
- Change application configurations.
- Access restricted information.
- Gain administrative control over the application.

**Key Takeaway:** Vertical privilege escalation occurs when a user gains permissions or functionality belonging to a higher-privileged role.
