1# 🔐 Splunk SOC Home Lab — SSH Brute Force Detection#

> Built a Splunk-based SOC home lab to detect SSH brute force attacks using real-time log monitoring, detection queries, and firewall response actions.

---

## 📌 Project Overview

This project demonstrates the design and implementation of a **Security Operations Center (SOC) home lab** using **Splunk SIEM** to detect SSH brute force attacks in real time.

The lab simulates a realistic attack scenario where an attacker attempts to gain unauthorized access to a Linux system using brute force techniques. Authentication logs are collected, forwarded to Splunk, analyzed using SPL detection queries, and visualized through dashboards.

**Detection Accuracy: 95%+**

---

## 🧠 Skills Demonstrated

| Area | Skills |
|---|---|
| SIEM | Splunk Enterprise, SPL Queries, Dashboard Creation |
| Log Analysis | auth.log parsing, pattern detection |
| Threat Detection | Brute force threshold rules |
| Incident Response | UFW firewall IP blocking |
| Linux | SSH configuration, service management |
| Networking | VM networking, port configuration |

---

## 🏗️ Lab Architecture

```
[Kali Linux - Attacker]
        |
        | SSH Brute Force (Hydra)
        ↓
[Linux Mint - Target Machine]
  /var/log/auth.log
        |
        | Splunk Universal Forwarder → Port 9997
        ↓
[Splunk Enterprise - SIEM Server]
  Search, Analyze, Dashboard
```

### Virtual Machines

| Role | OS | IP |
|---|---|---|
| Attacker | Kali Linux | 192.168.1.187 |
| Target (Victim) | Linux Mint | 192.168.0.100 |
| SIEM Server | Splunk Enterprise (Kali) | 192.168.1.187 |

---

## 🛠️ Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Kali Linux
- Linux Mint
- Hydra (Brute force tool)
- UFW Firewall
- VirtualBox

---

## ⚔️ Attack Simulation

A brute force attack was simulated using **Hydra**:

```bash
hydra -l users.txt -P passwords.txt ssh://192.168.0.100
```

This generated hundreds of failed SSH login attempts recorded in `/var/log/auth.log`, which were forwarded in real time to the Splunk server.

---

## 🔍 Detection Logic

### Primary Detection Query (SPL)

```spl
index=main sourcetype=linux_secure "Failed password"
| stats count by src_ip
| where count > 10
```

Detects repeated failed logins from a single IP — classic brute force signature.

### Log Verification Query

```spl
index=main sourcetype=linux_secure
```

---

## 🛡️ Incident Response

Once a malicious IP is identified, it is blocked using UFW:

```bash
sudo ufw deny from 192.168.1.187 to any port 22
```

---

## 📸 Screenshots

| Figure | Description | File |
|---|---|---|
| A.1 | Attacker Machine (Kali Linux) Setup | `screenshots/attacker_kali_setup.png` |
| A.2 | Target Machine (Linux Mint) Setup | `screenshots/target_linux_setup.png` |
| A.3 | inputs.conf Configuration | `screenshots/inputs_conf_config.png` |
| A.4 | Hydra Attack Execution | `screenshots/hydra_attack.png` |
| A.5 | Authentication Logs in Splunk Search | `screenshots/splunk_logs.png` |
| A.6 | Brute Force Detection Query Results | `screenshots/detection_query.png` |
| A.7 | Splunk Dashboard – Complete View | `screenshots/splunk_dashboard.png` |
| A.8 | Dashboard Summary Statistics Panel | `screenshots/dashboard_statistics.png` |


---

## 📁 Repository Structure

```
splunk-soc-home-lab/
├── README.md
├── architecture/
│   ├── soc_architecture
├── screenshots/       
├── configuration/
│   ├── inputs.conf
│   ├── outputs.conf
│   └── ssh_config.txt
├── detection/
│   ├── brute_force_detection.spl
│   └── dashboard_queries.spl
├── scripts/
│   ├── start_splunk.sh
│   ├── check_forwarder.sh
│   ├── run_hydra_attack.sh
│   └── block_ip_ufw.sh
├── logs/
│   └── sample_auth.log
└── documentation/
    ├── SOC_Lab_Report.pdf
    └── Final_SOC_Lab_Report.pdf
```

---

## 🔮 Future Improvements

- [ ] Threat intelligence feed integration
- [ ] Automated IP blocking script triggered by Splunk alert
- [ ] Machine learning anomaly detection

---

## 👤 Author

**Vignesh**  
Aspiring SOC Analyst | Cybersecurity & Threat Detection  

---

## 📚 References

- [Splunk Documentation](https://docs.splunk.com)
- [Hydra - THC](https://github.com/vanhauser-thc/thc-hydra)
- [Splunk Add-on for Unix and Linux](https://splunkbase.splunk.com/app/833)
# splunk-hone-lab
# splunk-soc-home-lab
# splunk-soc-home-lab
