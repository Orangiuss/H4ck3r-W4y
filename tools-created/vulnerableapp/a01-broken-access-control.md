---
icon: screwdriver
---

# A01 - Broken Access Control

In this vulnerability, the page is exposed to an **Insecure Direct Object Reference (IDOR)** flaw because the user ID is directly accessible via the URL without authorization verification. The user ID is, in fact, an MD5 hash of the username, which allows an attacker to manipulate the URL to access other accounts.

## Vulnerability Details

When analyzing the source code, the following comment is found:

```html
<!-- If the user is the admin admin_78, display the control panel -->
```

This means that the page will check the ID in the URL to determine whether to display the control panel. By modifying the user ID in the URL, it is possible to access the administrator’s profile without appropriate permissions.

#### Exploitation Example

To access the administrator profile, we need to obtain the MD5 hash of the identifier `admin_78`. The MD5 hash of `admin_78` is:

```
20541eeb668da7d30c80c56f00726f07
```

With this information, we can directly access the administrator’s profile using the following URL:

```
http://localhost:8042/profile.php?id=20541eeb668da7d30c80c56f00726f07
```

Accessing this URL provides the validation flag.

## Solution and Recommendations

To fix this vulnerability, it is essential to implement proper authorization checks on the server. Here are some best practices to strengthen access controls:

1. **Server-Side Verification**: Ensure each request is authenticated, and the user has the necessary permissions to access the object.
2. **Avoid Exposed Identifiers**: Use random identifiers and robust authorization mechanisms rather than simple identifiers like hashes of sensitive information.
3. **Role-Based Access Controls**: Implement a role-based system to restrict access to sensitive information to authorized users only.
