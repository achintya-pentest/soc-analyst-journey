# Windows Authentication Logs

## Objective

Understand how Windows Security Event Logs help detect suspicious authentication activity such as brute force attempts, password spraying, and post-compromise behavior.

---

## Key Event IDs

**4624 – Successful Logon**
Indicates a successful authentication attempt.

**4625 – Failed Logon**
Occurs when a login attempt fails. Multiple occurrences may indicate brute force attempts or password spraying.

**4634 – Logoff**
Indicates a user logged out of the system.

**4672 – Special Privileges Assigned**
Indicates that an account with administrative privileges has logged in.

**4688 – Process Creation**
Indicates that a new process has been created on the system.

---

## Important Logon Types

**Logon Type 2 – Interactive Logon**
User logged in locally on the machine.

**Logon Type 3 – Network Logon**
Authentication occurred while accessing a network resource.

**Logon Type 10 – Remote Interactive Logon**
Used when logging in through Remote Desktop Protocol (RDP).

---

## Common Authentication Attack Patterns

### Brute Force Pattern

```text
4625
4625
4625
4625
4624 (Logon Type 10)
```

Multiple failed login attempts followed by a successful login may indicate a brute force attack where an attacker repeatedly tries passwords until authentication succeeds.

---

### Password Spraying Pattern

```text
4625 | user1
4625 | user2
4625 | user3
4625 | user4
```

A single source attempting to authenticate to many accounts may indicate password spraying.

---

## Practice Investigation

### Scenario

```text
4625 | User: administrator | Source IP: 185.199.110.153 | Logon Type: 10
4625 | User: administrator | Source IP: 185.199.110.153 | Logon Type: 10
4625 | User: administrator | Source IP: 185.199.110.153 | Logon Type: 10
4624 | User: administrator | Source IP: 185.199.110.153 | Logon Type: 10
4672 | User: administrator
4688 | Process Created | Process: powershell.exe | User: administrator
```

### Analysis

The logs show multiple failed login attempts followed by a successful RDP login. This may indicate a brute force attack where an attacker eventually guessed the correct password.

Event ID **4672** shows that the logged-in account has administrative privileges. Shortly after login, **PowerShell was executed**, which may indicate post-compromise activity such as running scripts or downloading malicious payloads.

---

## Investigation Approach

A SOC analyst would typically:

* Check the **source IP address reputation**
* Verify whether the **administrator login was expected**
* Examine **PowerShell command-line arguments**
* Investigate the **parent process that launched PowerShell**
* Determine whether the same IP attempted access to **other accounts or systems**

---

## Key Takeaway

Authentication logs provide critical insight into login activity. Recognizing patterns such as brute force attempts, password spraying, and suspicious administrative logins is essential for SOC analysts when investigating potential security incidents.
