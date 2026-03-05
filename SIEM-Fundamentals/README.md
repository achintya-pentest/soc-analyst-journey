# SIEM Fundamentals

## Objective

Understand the purpose of Security Information and Event Management (SIEM) systems and how SOC analysts use them to collect logs, normalize data, search events, and investigate security alerts.

---

## What is SIEM?

Security Information and Event Management (SIEM) is a platform that collects and analyzes security logs from multiple sources across an organization.

These sources may include:

* Servers
* Endpoints
* Firewalls
* Intrusion Detection Systems (IDS)
* Applications

SIEM platforms allow security teams to centralize logs and investigate security events efficiently.

---

## Core Functions of a SIEM

### Log Collection

Logs from different systems are gathered into one central platform.

### Log Parsing

Parsing is the process of extracting meaningful fields from raw log data.

For example, a raw log may contain multiple pieces of information such as:

* timestamp
* username
* IP address
* event ID

Parsing separates these values so they can be analyzed individually.

---

### Log Normalization

Different devices generate logs in different formats. Normalization converts these logs into a **standard format** so they can be analyzed consistently.

For example:

```id="d3c4wz"
Firewall log → source_ip
Windows log → src_ip
```

After normalization both may appear as:

```id="5m8hfs"
source_ip
```

This makes searching across different log sources easier.

---

### Log Aggregation

Logs from various devices are collected and stored centrally so analysts can investigate events from one platform.

---

### Log Searching

SOC analysts use queries to find suspicious events such as failed logins or unusual activity.

Example search:

```id="fa9d6v"
EventID=4625
```

---

### Event Correlation

SIEM platforms can correlate multiple events to detect potential attack patterns.

Example:

```id="7c7thf"
4625 → Failed login  
4625 → Failed login  
4625 → Failed login  
4624 → Successful login
```

This sequence may indicate a brute-force attack.

---

### Alert Generation

SIEM tools generate alerts when certain conditions are met.

Example detection rule:

* More than 5 failed login attempts from the same IP within 5 minutes.

---

## Practice Investigation

### Scenario

```id="7q8z2r"
10:01 4625 User: admin  SourceIP: 185.33.12.4
10:02 4625 User: admin  SourceIP: 185.33.12.4
10:02 4625 User: admin  SourceIP: 185.33.12.4
10:03 4625 User: admin  SourceIP: 185.33.12.4
10:03 4624 User: admin  SourceIP: 185.33.12.4 LogonType:10
```

### Analysis

The logs show multiple failed login attempts followed by a successful login. This pattern may indicate a brute-force attack where an attacker repeatedly attempts passwords until authentication succeeds.

The successful login uses **Logon Type 10**, which indicates a Remote Desktop (RDP) login. If the source IP address is external or unfamiliar, this could indicate unauthorized remote access.

---

## Investigation Approach

A SOC analyst would typically investigate the following:

* Source IP reputation and geolocation
* Number of failed login attempts
* Whether the login activity is expected for the user
* Other accounts targeted by the same IP
* Suspicious processes executed after login

---

## Key Takeaway

SIEM platforms help SOC analysts centralize logs, normalize and parse data, search for suspicious activity, correlate security events, and detect potential attacks efficiently.
