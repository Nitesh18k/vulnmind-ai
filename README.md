# VulnMind AI 🛡️

**Enterprise-Grade CLI Vulnerability Assessment Platform for Kali Linux**

AI-powered security analysis with automated reconnaissance, vulnerability scanning, CVE mapping, risk scoring, and report generation — all from your terminal.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🤖 **AI Analysis** | OpenAI, Gemini, Claude, Groq, Ollama support |
| 🌐 **Recon Engine** | subfinder, amass, assetfinder, crt.sh, HackerTarget |
| 🔌 **Port Scanner** | nmap, naabu, masscan + Python fallback |
| 🐛 **Vuln Scanner** | nuclei, nikto, sqlmap, dalfox + built-in checks |
| 📋 **CVE Mapping** | NVD API, CWE references, MITRE ATT&CK |
| 📊 **Risk Scoring** | 0-100 risk score with breakdown |
| 📄 **Reports** | PDF, HTML, TXT with executive summary |
| 💾 **Database** | SQLite — persistent scan history |
| 🔐 **Auth** | Multi-user with role-based access |

---

## 🚀 Quick Start

### 1. Install

```bash
git clone https://github.com/yourname/vulnmind-ai
cd vulnmind-ai
bash install.sh
```

### 2. Run

```bash
# Interactive mode (recommended)
vulnmind

# OR
python3 vulnmind.py

# Quick scan
vulnmind -t example.com

# First-time setup wizard
vulnmind --config
```

### 3. Login
Default credentials: `admin` / `admin`
> ⚠️ Change your password after first login!

---

## 📋 Manual Installation

```bash
# Python dependencies
pip install -r requirements.txt --break-system-packages

# Kali Linux tools (apt)
sudo apt install nmap nikto sqlmap whois openssl masscan amass

# Go tools (requires Go: apt install golang)
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
go install github.com/projectdiscovery/katana/cmd/katana@latest
go install github.com/tomnomnom/assetfinder@latest
go install github.com/tomnomnom/waybackurls@latest
go install github.com/hahwul/dalfox/v2@latest

# Add Go binaries to PATH
echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> ~/.zshrc
source ~/.zshrc
```

---

## 🤖 AI Provider Setup

Go to **AI Settings** in the menu, or configure during setup wizard.

| Provider | Get API Key | Free Tier |
|---|---|---|
| **OpenAI** | https://platform.openai.com | No |
| **Gemini** | https://aistudio.google.com | Yes |
| **Claude** | https://console.anthropic.com | No |
| **Groq** | https://console.groq.com | Yes ✅ |
| **Ollama** | Local install | Yes ✅ Free |

**Groq** and **Ollama** are free options. Ollama runs fully offline.

```bash
# Install Ollama
curl https://ollama.ai/install.sh | sh
ollama pull llama3
```

---

## 📖 Usage Guide

### Main Menu
```
[1] Dashboard       — Stats, recent scans, findings overview
[2] Targets         — Manage scan targets
[3] New Scan        — Start a vulnerability assessment
[4] Scan History    — View past scans and results
[5] Vulnerabilities — Browse all findings
[6] Reports         — Generate/view reports
[7] AI Settings     — Configure AI provider
[8] Profile         — Account settings, API keys
[9] Tools Check     — Verify installed tools
```

### Scan Types

| Type | Duration | Description |
|---|---|---|
| **Quick** | ~2 min | DNS + common ports + security headers |
| **Standard** | ~5-10 min | Full recon + ports + vuln scan + AI analysis |
| **Full** | ~15-30 min | Everything + deep vuln scan + CVE mapping |
| **Recon Only** | ~1-2 min | Subdomain discovery + DNS + WHOIS |
| **Port Scan Only** | ~1-3 min | Port scanning only |

### Direct Scan (CLI)
```bash
# Quick scan from command line
vulnmind -t example.com

# Show version
vulnmind --version

# Configuration wizard
vulnmind --config
```

---

## 📁 File Structure

```
vulnmind/
├── vulnmind.py          # Main entry point
├── install.sh           # Kali Linux installer
├── requirements.txt     # Python dependencies
│
├── core/
│   ├── banner.py        # ASCII art banner
│   ├── menu.py          # Interactive menu system
│   ├── auth.py          # Authentication & session
│   ├── scanner.py       # Scan orchestrator
│   ├── dashboard.py     # Dashboard & stats
│   ├── config_wizard.py # First-run wizard
│   └── quick_scan.py    # CLI quick scan
│
├── modules/
│   ├── recon.py         # Reconnaissance engine
│   ├── portscan.py      # Port scanner
│   ├── vulnscan.py      # Vulnerability scanner
│   └── cve_mapper.py    # CVE & MITRE mapping
│
├── ai/
│   └── providers.py     # AI abstraction layer
│
├── database/
│   └── models.py        # SQLAlchemy models
│
└── reports/
    └── generator.py     # Report generator (PDF/HTML/TXT)
```

---

## 🔒 Security & Ethics

> **LEGAL NOTICE**: Only use VulnMind AI on systems you own or have **explicit written permission** to test. Unauthorized scanning is illegal and may violate laws including the Computer Fraud and Abuse Act (CFAA) and similar legislation worldwide.

- AI analysis is strictly passive — it analyzes collected data only
- No automated exploitation or destructive testing
- SQLMap and DalFox run in safe, non-destructive mode
- All targets and results stored locally in SQLite

---

## 📊 Database Location

```
~/.vulnmind/
├── vulnmind.db      # SQLite database
├── session.json     # Login session
└── reports/         # Generated reports
    ├── report_example.com_20241201_143022.html
    ├── report_example.com_20241201_143022.pdf
    └── report_example.com_20241201_143022.txt
```

---

## 🛠️ Troubleshooting

**"No AI provider configured"**
→ Go to Profile → Manage API Keys, or AI Settings → Configure

**"nuclei templates not found"**
→ Run: `nuclei -update-templates`

**Go tools not found after install**
→ Add to PATH: `export PATH=$PATH:$(go env GOPATH)/bin`

**Permission denied for nmap**
→ Run: `sudo vulnmind` or `sudo python3 vulnmind.py`

**SQLite error on fresh install**
→ Run: `python3 -c "from database.models import init_db; init_db()"`

---

## 📄 License

MIT License. For authorized security testing only.

---

*Built with ❤️ for security professionals on Kali Linux*
