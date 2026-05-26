# 🔒 WebPentest Auto Tool v2.0

> Automated Web Application Penetration Testing Tool for Kali Linux.
> **Only test websites you own or have written permission to test.**

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-purple?style=flat-square)
![Version](https://img.shields.io/badge/Version-2.0-green?style=flat-square)

---

## ⚠️ Disclaimer
This tool is for **authorized testing only**. Only use it on sites you own. Unauthorized scanning is illegal.

---

## 📦 Install

```bash
# 1. Clone
git clone https://github.com/Prathiv-Raj/Pen_Test_Automation
cd Pen_Test_Automation

# 2. Python dependencies
pip install -r requirements.txt --break-system-packages

# 3. System tools
sudo apt install -y nmap nikto gobuster whatweb sslscan sqlmap whois dnsutils seclists wpscan

# 4. Go tools (optional)
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install github.com/hahwul/dalfox/v2@latest
go install github.com/hakluke/hakrawler@latest
go install github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
nuclei -update-templates
```

---

## 🚀 Usage

```bash
# Check tools installed
python3 pentest_auto_v2.py --url https://yoursite.com --check-tools

# Full scan (all 8 phases)
python3 pentest_auto_v2.py --url https://yoursite.com

# Fast mode
python3 pentest_auto_v2.py --url https://yoursite.com --fast

# Specific phases only
python3 pentest_auto_v2.py --url https://yoursite.com --phases 1,2,4

# WordPress site
python3 pentest_auto_v2.py --url https://yoursite.com --wp-token YOUR_TOKEN

# Custom output folder
python3 pentest_auto_v2.py --url https://yoursite.com --output ~/reports
```

---

## 🗂️ Phases

| # | Phase | Tools |
|---|---|---|
| 1 | Reconnaissance | nmap, gobuster, subfinder, whatweb, whois, dig |
| 2 | Scanning & Enumeration | nikto, sslscan, hakrawler, gau |
| 3 | Authentication Testing | requests (built-in) |
| 4 | Input Validation | sqlmap, dalfox |
| 5 | Access Control | requests (built-in) |
| 6 | Misconfiguration | requests (built-in) |
| 7 | Nuclei Scan | nuclei |
| 8 | WPScan | wpscan |

---

## 📊 Output

Reports saved to `./pentest_reports/pentest_yoursite_TIMESTAMP/`

```
├── pentest_report.html   ← Open in Firefox (best view)
├── pentest_report.txt    ← Plain text
└── raw_results.json      ← Raw JSON data
```

```bash
firefox pentest_reports/pentest_yoursite_*/pentest_report.html
```

---

## 📁 Files

```
webpentest-auto/
├── pentest.py
├── requirements.txt
└── README.md
```

---

## 🔧 Common Issues

| Problem | Fix |
|---|---|
| Gobuster wildcard 403 | Script auto-detects and adds `--exclude-length` flag |
| Subfinder finds nothing | Script falls back to DNS brute-force + crt.sh automatically |
| Nikto timeout | Capped at 4 min internally — runs in parallel with other tasks |
| Go tools not found | `echo 'export PATH=$PATH:$HOME/go/bin' >> ~/.bashrc && source ~/.bashrc` |
| SQLMap finds nothing | Need URLs with GET params — script crawls site first to find them |
