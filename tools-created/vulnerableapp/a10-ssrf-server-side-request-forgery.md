---
icon: server
---

# A10 - SSRF (Server-Side Request Forgery)

## **Overview**

Server-Side Request Forgery (SSRF) is a vulnerability that allows an attacker to make requests on behalf of a vulnerable server. The attacker exploits this by tricking the server into sending requests to arbitrary domains or IP addresses. This can often involve targeting internal systems, cloud services, or even third-party APIs that would not normally be accessible from outside the network.

## **Risks Associated with SSRF:**

* **Access to Internal Networks**: Attackers can access systems behind firewalls or private networks that are normally protected.
* **Sensitive Data Theft**: SSRF vulnerabilities may allow attackers to retrieve sensitive data that is only available on internal networks.
* **Service Exploitation**: Attackers can use the internal services to carry out further attacks, such as port scanning or exploiting vulnerable services.
* **Configuration Manipulation**: In some cases, attackers can modify configurations or metadata, especially with cloud services.

### **Example:**

In an application, we are given the ability to provide a URL, and the server will fetch the content of that URL. We are trying to access the `flag_ssrf.txt` file, but we do not have permission to do so directly. Using SSRF, we can attempt to retrieve the `flag_ssrf.txt` file via the following requests:

```
http://127.0.0.1/flag_ssrf.txt
http://localhost/flag_ssrf.txt
```

By exploiting SSRF, we can retrieve the flag file successfully.

### Solution Approach:

1. **Identifying the SSRF Endpoint**: Look for a feature where the application allows you to enter a URL (such as fetching content from an external URL or API).
2. **Attempt Localhost Access**: If the application fetches URLs on the server's behalf, you can attempt to retrieve sensitive files from internal paths using SSRF. For instance, use URLs like `http://127.0.0.1/flag_ssrf.txt` or `http://localhost/flag_ssrf.txt`.
3. **Fetching the Flag**: If SSRF is successfully exploited, the server will retrieve the content of the flag file from the internal server, which will be returned to the attacker.

### **Conclusion:**

SSRF vulnerabilities can lead to significant risks, including unauthorized access to sensitive files, networks, and services. They can also be a stepping stone to other attacks if exploited properly. Therefore, it’s important to implement proper input validation and avoid making untrusted requests to internal resources in response to user input.
