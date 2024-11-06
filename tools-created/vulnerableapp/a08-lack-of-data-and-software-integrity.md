---
icon: binary-circle-check
---

# A08 - Lack of Data and Software Integrity

## **Problem Description**

Lack of data and software integrity refers to issues where code and infrastructure do not protect against integrity violations. This is particularly risky when an application relies on external, untrusted sources for libraries or components, such as third-party servers or CDNs. An improperly configured CI/CD pipeline can also introduce risks, such as unauthorized access or the injection of malicious code.

### **Example: Incorrect Use of jQuery Without Integrity Check**

In this example, a web application uses a third-party library (jQuery) that is fetched directly from an external server (CDN) without verifying its integrity. Here’s how this happens:

A website includes jQuery via a CDN URL like this:&#x20;

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```

When a user visits the website, their browser downloads jQuery from the external server.

### **Security Issue**

If an attacker manages to compromise the official jQuery repository, they could inject malicious code into the file. Users visiting the site would then download this modified file unknowingly, and it would execute in their browsers. This represents a software integrity failure because there’s no check to ensure that the downloaded file is the intended, unmodified version.

### **Recommended Solution: Subresource Integrity (SRI)**

The solution is to use **Subresource Integrity (SRI)**, a mechanism that adds a hash of the file being downloaded in the `integrity` attribute of the `<script>` tag. This mechanism ensures that the file hasn’t been altered. If the file’s integrity doesn’t match the hash, it is rejected by the browser.

Here’s how you should correctly implement it with the SHA-256 hash for the jQuery library:

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js" 
 integrity="sha256-o88AwQnZB+VDvE9tvIXrMQaPlFFSUTR+nldQm1LuPXQ=" crossorigin="anonymous"></script>
```

With this approach, even if an attacker manages to compromise the CDN server, the malicious file will be rejected by the browser, ensuring the integrity of the code executed on the user’s device.

**Summary**

The integrity of third-party resources is essential for the security of modern applications. By using the SRI mechanism, you ensure that libraries loaded from external servers are not altered, protecting your users from malicious code injection attacks.
