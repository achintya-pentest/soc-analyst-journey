# 📘 Windows Threat Detection 2 – SOC Investigation Report

## 🧠 Overview
This project documents my investigation and analysis of simulated attack scenarios in the **TryHackMe: Windows Threat Detection 2** room.

The focus was on detecting malicious activity using **Sysmon logs**, understanding attacker behavior, and mapping actions to the **MITRE ATT&CK framework**.

---

## 🎯 Objectives
- Analyze Sysmon logs to identify malicious activity  
- Track attacker behavior across multiple stages  
- Detect file collection and data exfiltration  
- Identify abuse of legitimate tools (LOLBins)  
- Understand ingress tool transfer techniques  

---

## 🛠️ Tools & Technologies
- Windows Event Viewer  
- Sysmon Logs  
- PowerShell  
- CMD utilities (curl, certutil)  
- TryHackMe AttackBox  

---

## 🔍 Scenario Summary
A simulated phishing attack was executed where a malicious file (`invoice.pdf.exe`) was run.

The attacker performed:
- System reconnaissance  
- Privilege discovery  
- File collection  
- Clipboard harvesting  
- Data exfiltration  
- Downloading tools using multiple methods  

---

# ⚔️ Attack Chain Analysis

## 1️⃣ Initial Execution
- Malicious file executed: `invoice.pdf.exe`
- Observed in **Sysmon Event ID 1 (Process Create)**

**Suspicious Indicators:**
- Executable disguised as a PDF file  
- Likely delivered via phishing  

---

## 2️⃣ Discovery Phase

### Commands Observed:
- whoami
- tasklist /v

**Purpose:**
- Identify current user  
- Enumerate running processes  
- Detect security tools  

**Detection Source:**
- Sysmon Event ID 1  

---

## 3️⃣ Defense Evasion Check
- cmd /c "tasklist /v | findstr MsSense.exe || echo No MS Defender EDR"

**Insight:**
- Malware checks for Microsoft Defender EDR presence  
- Indicates awareness of defensive controls  

---

## 4️⃣ Collection Phase

### File Search
Malware searched for:
- docx, pdf, xlsx

**Insight:**
- Malware checks for Microsoft Defender EDR presence  
- Indicates awareness of defensive controls  

---

**Reason:**
- Documents likely contain sensitive or valuable data  

---

### Clipboard Collection
- Get-Clipboard

**Risk:**
- Captures copied sensitive data such as passwords or tokens  

---

## 5️⃣ Directory Creation

- Malware created files in: C:\Users\Administrator\AppData\Local\Temp

**Insight:**
- Common attacker technique to avoid detection  
- Temporary directories are less monitored  

---

## 6️⃣ Data Exfiltration

### Domain Identified:
- selecteddata-storage-2025.s3.amazonaws.com

**Key Insight:**
- Uses AWS S3 (trusted service)  
- Blends malicious traffic with legitimate cloud usage  

**MITRE Technique:**
- Exfiltration Over Web Services  

---

## 7️⃣ Ingress Tool Transfer

### Same payload downloaded using multiple tools:

**Browser:**
**curl:**
**certutil:**
**PowerShell:**

---

## 🧠 Key Concept: LOLBins

Attackers used legitimate tools:

- curl.exe  
- certutil.exe  
- powershell.exe  

**Technique:**
- Living Off The Land Binaries (LOLBins)

**Why attackers use them:**
- Trusted by the system  
- Harder to detect  
- No need to drop additional malware  

---

# 🧩 MITRE ATT&CK Mapping

| Stage              | Technique                          |
|-------------------|-----------------------------------|
| Execution         | User Execution                    |
| Discovery         | Account Discovery, Process Discovery |
| Defense Evasion   | Security Software Discovery       |
| Collection        | Data from Local System, Clipboard Data |
| Exfiltration      | Exfiltration Over Web Services    |
| Ingress Transfer  | Ingress Tool Transfer             |

---

# 🚨 Key Findings

- Malware used PowerShell extensively  
- Suspicious process execution patterns observed  
- Repeated commands indicated automation  
- Cloud services used for data exfiltration  
- Legitimate system tools were abused  

---

# 🧠 Lessons Learned

- Legitimate tools can be used maliciously  
- Behavioral analysis is more important than signatures  
- Process relationships are critical for detection  
- DNS logs help identify exfiltration  
- Correlating multiple logs is essential  

---

# 🚀 Skills Gained

- Sysmon log analysis  
- Process behavior investigation  
- Detection of data exfiltration techniques  
- Understanding attacker methodology  
- MITRE ATT&CK mapping  

---

# 📌 Conclusion

This lab provided hands-on experience in detecting and analyzing real-world attack techniques.

It reinforced the importance of:
- Monitoring system behavior  
- Detecting abuse of legitimate tools  
- Correlating logs across different sources  

---

# 🔗 Author
**Achintya Pandey**  
Aspiring SOC Analyst | Cybersecurity Enthusiast  

---

⭐ If you found this useful, feel free to connect or collaborate!
