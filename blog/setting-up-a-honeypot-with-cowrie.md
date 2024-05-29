---
description: 🍯🍯🍯🍯🍯
---

# 🍯 Setting Up a Honeypot 🍯 with Cowrie

## Setting Up a Honeypot with Cowrie: An SSH Example

In this blog post, we'll dive into the fascinating world of honeypots, specifically focusing on setting up a Cowrie honeypot for SSH. Honeypots are powerful tools in the cybersecurity arsenal, designed to lure and analyze malicious activity. Let's explore what a honeypot is, how it works, and walk through a practical example using Cowrie.

### What is a Honeypot?

A honeypot is a decoy system designed to attract cyber attackers and gather intelligence on their techniques. By simulating a vulnerable system, honeypots can provide valuable insights into attack vectors and malicious behavior without compromising real systems.

#### Types of Honeypots

* **Low-Interaction Honeypots:** Simulate a limited number of services and interactions.
* **High-Interaction Honeypots:** Offer a more realistic environment, allowing attackers to interact with a fully functional system.

### Why Use Cowrie for SSH?

Cowrie is a well-known high-interaction SSH and Telnet honeypot that emulates a Unix-like system. It is highly configurable and records the activities of intruders, providing detailed logs for analysis. This makes it an excellent tool for studying SSH-based attacks.

### Setting Up Cowrie: A Step-by-Step Guide

We'll now walk through the steps to set up Cowrie on your system.

#### Step 1: Install System Dependencies

First, ensure you have all necessary system dependencies installed:

```sh
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv
```

#### Step 2: Create a User Account

Create a dedicated user account for running Cowrie:

```sh
sudo adduser --disabled-password cowrie
```

#### Step 3: Checkout the Code

Clone the Cowrie repository and navigate into the directory:

```sh
git clone http://github.com/cowrie/cowrie
cd cowrie
```

#### Step 4: Setup Virtual Environment

Set up a Python virtual environment and install the required Python packages:

```sh
python3 -m venv cowrie-env
source cowrie-env/bin/activate
python -m pip install --upgrade pip
python -m pip install --upgrade -r requirements.txt
```

#### Step 5: Configure Cowrie

Edit the configuration file to enable SSH and optionally Telnet:

```sh
nano cowrie.cfg
```

For example, to enable Telnet, add the following line:

```ini
[telnet]
enabled = true
```

#### Step 6: Start Cowrie

Finally, start the Cowrie honeypot:

```sh
bin/cowrie start
```

### Monitoring and Analyzing Attacks

Once Cowrie is up and running, it will log all interactions. You can monitor these logs to analyze the behavior of potential attackers. Logs are typically stored in `log/cowrie.json` and `log/cowrie.log`.

#### Example Attack Log

Here's an example of what an SSH attack log might look like:

```json
{
  "eventid": "cowrie.login.success",
  "username": "root",
  "password": "123456",
  "timestamp": "2023-05-29T12:34:56.789Z"
}
```

This log entry indicates a successful login attempt using the username "root" and password "123456".

### Resources

For more detailed installation instructions and configuration options, refer to the official Cowrie documentation and community resources:

* [Cowrie GitHub Repository](https://github.com/cowrie/cowrie)
* [Cowrie Documentation](https://cowrie.readthedocs.io/en/latest/INSTALL.html)
* [IT-Connect Guide on Cowrie](https://www.it-connect.fr/mise-en-place-et-etude-dun-honey-pot-ssh-cowrie/)
* [StarmTech Guide on Cowrie](https://starmtech.fr/2023/05/10/guide-complet-cowrie-honeypot/)

### Conclusion

Setting up a honeypot like Cowrie provides invaluable insights into malicious activities targeting your systems. By following the steps outlined in this guide, you can create a powerful tool for monitoring and analyzing SSH attacks. Happy hunting!
