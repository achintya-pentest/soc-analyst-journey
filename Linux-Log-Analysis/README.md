# Linux Log Analysis

## 🧠 Objective

Analyze log files using Linux commands to identify activity from a specific IP address.

---

## 📂 Scenario

Two log files were provided:

* `access1.log`
* `access2.log`

Goal: Combine and analyze logs to find relevant activity.

---

## 🔧 Steps

### Combine logs

```bash id="qfslcb"
cat access1.log access2.log > combined_access.log
```

### Search for IP activity

```bash id="3wmjxt"
grep "192.168.1.10" combined_access.log
```

### Read large logs

```bash id="6ev8t7"
less combined_access.log
```

---

## 🔍 Findings

* Activity from the IP address `192.168.1.10` was identified in the logs
* Repeated entries may indicate suspicious or automated behavior

---

## 🧠 What I Learned

* Logs contain useful information for investigations
* `grep` can be used to filter specific activity
* Combining logs helps in analyzing data efficiently

---
## 📎 Detailed Notes
Detailed notes for this topic can be found here:
https://github.com/achintya-pentest/linux-learning-journey/main/basics/log-analysis.md
