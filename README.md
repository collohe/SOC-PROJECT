# Operation Agrodefend – A SOC in a Segmented Network

## About the Project

This project demonstrates the design, implementation, and evaluation of a **Security Operations Center (SOC)** using open-source tools. The goal was to simulate real-world cyberattacks and observe how a SOC environment detects, analyzes, and responds to threats.

### Key Objectives:
- Simulate attacks such as phishing and brute-force login.
- Use tools like **pfSense**, **Wazuh**, **Ubuntu**, **Windows 10**, and **Kali Linux**.
- Segment the network using interfaces: **WAN**, **IT Department**, **Corpnet**, and **DMZ**.
- Analyze alerts and logs to assess SOC effectiveness.

---

## Network Architecture

The setup includes:
- **WAN** – External access
- **DMZ** – Externally accessible servers (e.g., web server)
- **IT Department** – Internal users
- **Corpnet** – Corporate services

### Segmentation:
- Clear firewall rules applied via **pfSense** to ensure:
  - Minimal lateral movement
  - Principle of least privilege
  - Proper isolation between zones

---

## Firewall Rules Summary

### IT Dept → DMZ:
- ✅ Allow web access to DMZ-hosted applications

### DMZ → IT Dept:
- ❌ Block all traffic by default
- ✅ Allow ICMP (ping) for diagnostics

### DMZ → WAN:
- ✅ Allow outbound HTTP/HTTPS
- ❌ Block unsolicited inbound traffic unless explicitly required

---

## Attack Simulation

### Reconnaissance (Nmap)
Used to gather information:
```bash
nmap -A -T4 192.168.70.10
```

### Brute-Force Attack (Hydra)
Used to test SSH login with generated credentials:
```bash
sudo hydra -t 1 -L user.list -P wordlist.txt ssh://192.168.70.10 -vV
```

---

## Wazuh Alerts & Analysis

### Total Events: 5,099
- 🔴 **4 High Severity**
- 🟠 **95 Medium Severity**
- 🟢 **5000+ Low Severity**

### 🔴 High Severity Alerts:
- Successful brute-force attacks
- Unauthorized access
- Exploits in DMZ servers

**Recommended Actions:**
- Immediate investigation
- Correlate logs across systems
- Patch or isolate affected systems

### 🟠 Medium Severity Alerts:
- Repeated failed logins
- Outdated software use
- Unusual scripts

**Recommended Actions:**
- Harden systems
- Increase monitoring
- Investigate patterns

### 🟢 Low Severity Alerts:
- Informational logs
- System changes
- Minor misconfigurations

**Recommended Actions:**
- Sample for patterns
- Tweak rules to reduce noise
- Use for trend analysis

---

## Conclusion

This SOC lab demonstrates the importance of:
- Segmentation
- Proactive detection
- Log correlation
- Continuous improvement

Integrating **Wazuh** with threat intelligence and refining alert rules can further enhance detection while reducing alert fatigue.

---

## Tools Used
- 🛡️ pfSense – Firewall & Network Segmentation
- 📊 Wazuh – SIEM/Monitoring
- 🐧 Ubuntu Server – Target VM
- 🪟 Windows 10 – Analyst Machine
- 🐍 Kali Linux – Attacker Machine
- 🔎 Nmap – Reconnaissance Tool
- 🔓 Hydra – Brute-force Tool

---

## Screenshots

> *(Insert Wazuh dashboard and alert screenshots here if available)*

---

## License

This project is intended for **educational and research purposes only**. Use responsibly in a controlled environment.
