---
icon: crop-simple
---

# A04 - Insecure Design

Insecure design refers to vulnerabilities arising from poor planning or a lack of security considerations in an application’s design phase. In this example, we have an insecure password recovery page that unintentionally reveals user information and lacks protections against brute-force attacks. Here’s how this vulnerability manifests and examples of insecure design choices.

#### Description of the Vulnerability

The password recovery page displays overly specific error messages that can help attackers identify valid users. When attempting to recover a password, the error message indicates whether or not a user exists in the system. Once a valid username is found, such as `administrateur`, an attacker can answer a "security question" to retrieve the password.

The design allows for unlimited attempts, meaning that an attacker could try every possible city in response to the security question without facing any account lockout or rate-limiting restrictions. In this case, by guessing the city `Paris`, we successfully retrieve the flag.

#### Examples of Insecure Design Choices

Here are additional insecure design examples that illustrate common security oversights:

1. **Insecure Secret Questions for Account Recovery**: Security standards discourage the use of secret questions, as they are often easily guessed or researched, offering minimal security.
2. **No Password Re-Prompt for Sensitive Actions**: Failing to prompt users to re-enter their password for actions like changing an email or password is a significant security risk, as it allows unauthorized individuals with access to the session to make critical changes.
3. **Lack of Protection Against Authentication Attacks**: Without a lockout mechanism or other protections, an attacker can attempt an excessive number of login attempts to guess credentials or gain access through brute force.
4. **Insecure "Forgot Password" Feature**: Insecure password recovery mechanisms may allow attackers to enumerate valid users and lack strong identification controls.

**Password Recovery Example**

In this case, the password recovery design flaw allows us to exploit the following sequence:

* Determine if a user exists based on error messages.
* Use a security question with an easily guessable answer, such as a city name.
* Submit guesses repeatedly without restriction until the correct answer (`Paris`) is identified, revealing the flag.

#### Broader Examples of Insecure Design

Insecure design isn’t limited to authentication flaws. Poorly conceived application designs can lead to a wide range of security issues, including:

* **Information Disclosure**: Application responses may inadvertently reveal sensitive information to unauthorized users.
* **Access Control Failures**: Improperly designed access controls can allow users to perform actions or view data beyond their permissions.
