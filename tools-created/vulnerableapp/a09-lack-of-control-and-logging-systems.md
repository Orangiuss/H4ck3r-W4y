---
icon: newspaper
---

# A09 - Lack of Control and Logging Systems

**Problem Description**

Weaknesses in logging and monitoring system activities can significantly hinder the ability to detect and respond to security incidents. This category covers a variety of vulnerabilities that are difficult to test but are crucial for detecting attacks and ensuring operational security. Proper logging and monitoring are key components in the work of SOC teams and log surveillance.

**Examples of Deficiencies:**

* **Missing auditable events**: Events such as logins, failed login attempts, and high-value transactions are not logged.
* **Inadequate or unclear log messages**: Warnings and errors fail to generate log messages, or the messages are vague and insufficient.
* **Lack of log monitoring**: Application and API logs are not monitored for suspicious activity.
* **Failure to alert on security tests**: Penetration tests and vulnerability scans performed by security tools do not trigger alerts, or no such tools exist.
* **Inability to detect or alert on active attacks**: The application cannot detect or alert in real time when an active attack is occurring.

**Question:**

What is the IP address of a potential attacker in the following log file: `logs.txt`?

To answer this question, you would typically need to review the log file for entries related to suspicious activities, such as failed login attempts, unusual access patterns, or IP addresses that may indicate unauthorized access.
