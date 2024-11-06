---
icon: lock
---

# A02 - Cryptographic Failures

Cryptographic failures often arise from the use of outdated or weak cryptographic techniques, insecure protocols, or insufficient encryption. Below are some common examples and issues associated with cryptographic failures:

## Examples of Cryptographic Failures

1. **Not Using HTTPS**: Transmitting data over HTTP exposes sensitive information to interception and man-in-the-middle attacks.
2. **Deprecated Cryptographic Suites or Hash Functions**: Using weak or outdated algorithms, such as MD5 or SHA1 for password storage, can lead to quick and easy compromise of sensitive data.
3. **Use of Weak Secrets/Keys for Encryption**: Relying on predictable or short encryption keys increases the risk of unauthorized access.
4. **Use of Insecure Protocols**:
   * HTTP (unencrypted)
   * FTP (unencrypted)
   * Telnet (unencrypted)
   * SMTP (unencrypted by default)
   * POP3 (unencrypted by default)
   * IMAP (unencrypted by default)
   * DNS (unencrypted by default)

## Vulnerability Examples

Below are examples of data encoded or hashed with insecure algorithms, which can be cracked using common tools or websites like [crackstation.net](https://crackstation.net).

* **Base64**: `YWRtaW46VnVsbkFwcHtCQTVlNjRfMTVfTm90X3NlQ1VSMy4uLn0=`
* **NTLM**: `F8F07F198A71F8F974EF0A23C25FFBBC`
* **MD5**: `41eb9128c6834194cfc7cf89893e6d92`
* **SHA1**: `0935ea842b85bf3fc4c1ee22e1ae7c1fbac53e8c`

These encodings and hashes can be broken with tools like `hashcat` or `John the Ripper`, or by utilizing online services to reveal the plaintext information.

#### Exploiting JWT with a Weak Secret

We got for example this JWT :&#x20;

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJWdWxuQXBwe2pXNy1pUy1zRWNVUjN9IiwibmFtZSI6IkpvaG4gRGlmZm9sIiwiaWF0IjoxNTE2MjM5MDIyLCJhcnRlZmFjdCI6IkluY2FsIiwiZW1haWwiOiJzZWNyZXQtZmJpQHlhaG9vLm1lIiwicGFzc3dvcmQiOiIyMzY1MDQ3NDA3YTYxNzUzZTQ2N2M5NzliZGYyMTllZmI5ZGQzYzljIn0.ikMLn8EPR4_B49VReA032XX4PI7z_v9rjJaBMrZFbMs
```

If a JSON Web Token (JWT) is signed with a weak or predictable secret, it is vulnerable to brute-force attacks, allowing attackers to decode sensitive data.

To crack a weak JWT secret, we can use `hashcat`:

```
git clone https://github.com/wallarm/jwt-secrets.git
hashcat -m 16500 -a 0 jwt_token.txt /jwt-secrets/jwt.secrets.list
```

#### Information in a JWT Example

By decoding the following JWT, we can access sensitive information stored within it due to weak security practices:

```json
{
  "sub": "VulnApp{jW7-iS-sEcUR3}",
  "name": "John Diffol",
  "iat": 1516239022,
  "artefact": "Incal",
  "email": "secret-fbi@yahoo.me",
  "password": "2365047407a61753e467c979bdf219efb9dd3c9c"
}
```

In this example, sensitive data such as the user’s name, email, and password hash are exposed in the JWT payload, highlighting the risks associated with weak cryptographic practices.

## Solution and Recommendations

To mitigate cryptographic vulnerabilities, consider the following best practices:

1. **Enforce HTTPS**: Use HTTPS for all web traffic to secure data in transit.
2. **Strong Cryptographic Algorithms**: Use up-to-date cryptographic standards, such as SHA-256 for hashing and AES for encryption.
3. **Secure Secrets and Keys**: Generate secure, random secrets and keys with sufficient length to prevent brute-force attacks.
4. **Avoid Insecure Protocols**: Use secure versions of protocols, such as FTPS, SSH, SMTPS, and DNS over HTTPS (DoH).
5. **Review and Regularly Update Security Practices**: Regularly audit cryptographic practices to ensure they adhere to current security standards and do not include deprecated algorithms or protocols.
