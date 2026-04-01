# Windows Threat Detection Investigation

## 📌 Objective

The objective of this investigation is to analyze Windows event logs to identify potential malicious activity and understand attacker behavior using common attack patterns such as brute force attempts and privilege escalation.

---

## 🧪 Scenario

Suspicious login activity was observed on a Windows system. The task was to analyze authentication logs and identify whether the activity represents a potential attack.

---

## 🛠️ Tools Used

* Windows Event Logs
* Event Viewer
* Security Log Analysis

---

## 🔍 Events Observed

### Key Event IDs

* **4625** → Failed login attempt
* **4624** → Successful login
* **4672** → Special privileges assigned (admin access)

---

## 🧠 Analysis

### Pattern Identified

```text
4625 → 4625 → 4625 → 4624 → 4672
```

### Interpretation

* Multiple failed login attempts indicate possible **password guessing or brute force attack**
* A successful login following failures suggests the attacker eventually gained access
* Event ID 4672 indicates that the account has **administrative privileges**

---

## 🚨 Findings

* Repeated failed login attempts were detected
* A successful login occurred after multiple failures
* The account was assigned elevated privileges

👉 This strongly suggests a **brute force attack followed by privileged access**

---

## 🧠 MITRE ATT&CK Mapping

* **T1110 – Brute Force**
* **T1078 – Valid Accounts**
* **T1068 – Privilege Escalation (possible)**

---

## 📚 Lessons Learned

* Windows Event Logs provide critical visibility into authentication activity
* Attack patterns can be identified through event correlation
* Multiple failed logins followed by success is a strong indicator of brute force attacks
* Privilege-related events help identify high-impact compromises

---

## ✅ Conclusion

This investigation demonstrates how analyzing Windows authentication logs and correlating event IDs can reveal attacker behavior. Recognizing patterns such as repeated failed logins followed by successful access is essential for detecting brute force attacks in a SOC environment.

---
