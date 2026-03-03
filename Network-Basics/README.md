# Network Basics for SOC

## 🧠 Objective

Understand how IP addresses, ports, and protocols help in analyzing network activity during security investigations.

---

## 🌐 Internal vs External Traffic

Internal Traffic:

* Communication between private IP addresses
* Example: `10.0.0.5 → 10.0.0.20:445`

External Traffic:

* Communication between internal and public IP addresses
* Example: `185.44.12.9 → 10.0.0.15:3389`

---

## 🔢 Common Ports to Remember

* 80 → HTTP
* 443 → HTTPS
* 22 → SSH
* 3389 → RDP
* 445 → SMB
* 53 → DNS

These ports frequently appear in security alerts.

---

## 🔐 Protocol Basics

HTTP (80):

* Web traffic
* Not encrypted

HTTPS (443):

* Encrypted web traffic
* Not automatically safe — context matters

SSH (22):

* Secure remote login
* Common brute-force target

TCP:

* Reliable, connection-based

UDP:

* Faster, connectionless
* Commonly used for DNS

---

## 🔍 SOC Perspective

When analyzing logs:

* IP address indicates source/destination
* Port indicates service being accessed
* Protocol indicates type of communication

Context determines whether activity is normal or suspicious.

---

## 🎯 Conclusion

Basic networking knowledge is essential for interpreting logs and identifying potentially malicious activity in a SOC environment.
