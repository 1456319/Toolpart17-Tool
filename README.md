# 🔐 SheerID Verification Tool for Submitting Your ID Seamlessly (ID REQUIRED)

[![GitHub Stars](https://img.shields.io/github/stars/ThanhNguyxn/SheerID-Verification-Tool?style=social)](https://github.com/ThanhNguyxn/SheerID-Verification-Tool/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Documentation](https://img.shields.io/badge/Docs-Website-2ea44f?style=flat&logo=github&logoColor=white)](https://thanhnguyxn.github.io/SheerID-Verification-Tool/)

A comprehensive collection of tools for automating SheerID verification workflows for various services (Spotify, YouTube, Google One, etc.).

---

## 🛠️ Available Tools

| Tool | Type | Target | Description |
|------|------|--------|-------------|
| [spotify-verify-tool](./spotify-verify-tool/) | 🎵 Student | Spotify Premium | University student verification |
| [youtube-verify-tool](./youtube-verify-tool/) | 🎬 Student | YouTube Premium | University student verification |
| [one-verify-tool](./one-verify-tool/) | 🤖 Student | Gemini Advanced | Google One AI Premium verification |
| [boltnew-verify-tool](./boltnew-verify-tool/) | 👨‍🏫 Teacher | Bolt.new | Teacher verification (University) |
| [canva-teacher-tool](./canva-teacher-tool/) | 🇬🇧 Teacher | Canva Education | UK Teacher verification (K-12) |
| [k12-verify-tool](./k12-verify-tool/) | 🏫 K12 | ChatGPT Plus | K12 Teacher verification (High School) |
| [veterans-verify-tool](./veterans-verify-tool/) | 🎖️ Military | General | Military status verification |
| [veterans-extension](./veterans-extension/) | 🧩 Chrome | Browser | Chrome extension for military verification |

### 🔗 External Tools

| Tool | Type | Description |
|------|------|-------------|
| [RoxyBrowser](https://roxybrowser.com?code=01045PFA) | 🦊 Browser | **Anti-detect browser** — Safely manage multiple verified accounts without getting banned |
| [Check IP](https://ip123.in/en?code=01045PFA) | 🌐 Web | **Check IP** — Check your IP address and proxy status |
| [SheerID Verification Bot](https://t.me/SheerID_Verification_bot?start=ref_LdPKPES3Ej) | 🤖 Bot | Automated Telegram verification bot |
| [Gmail Farmer Bot](https://t.me/GmailFarmerBot?start=7762497789) | 🤖 Bot | Create Gmail accounts automatically |
| [GitHub Bot](https://t.me/AutoGHS_Bot?start=7762497789) | 🤖 Bot | Auto GitHub Stars & engagement service |
| [Student Card Generator](https://thanhnguyxn.github.io/student-card-generator/) | 🎓 Tool | Create student cards for manual verification |
| [Payslip Generator](https://thanhnguyxn.github.io/payslip-generator/) | 💰 Tool | Generate payslips for teacher verification |

---

## 🧠 Core Architecture & Logic

All Python tools in this repository share a common, optimized architecture designed for high success rates.

### 1. The Verification Flow
The tools follow a standardized "Waterfall" process:
1.  **Data Generation**: Creates a realistic identity (Name, DOB, Email) matching the target demographic.
2.  **Submission (`collectStudentPersonalInfo`)**: Submits data to SheerID API.
3.  **SSO Skip (`DELETE /step/sso`)**: Crucial step. Bypasses the requirement to log in to a school portal.
4.  **Document Upload (`docUpload`)**: Uploads a generated proof document (Student ID, Transcript, or Teacher Badge).
5.  **Completion (`completeDocUpload`)**: Signals to SheerID that upload is finished.

### 2. Intelligent Strategies

#### 🎓 University Strategy (Spotify, YouTube, Gemini)
- **Weighted Selection**: Uses a curated list of **45+ Universities** (US, VN, JP, KR, etc.).
- **Success Tracking**: Universities with higher success rates are selected more often.
- **Document Gen**: Generates realistic-looking Student ID cards with dynamic names and dates.

#### 👨‍🏫 Teacher Strategy (Bolt.new)
- **Age Targeting**: Generates older identities (25-55 years old) to match teacher demographics.
- **Document Gen**: Creates "Employment Certificates" instead of Student IDs.
- **Endpoint**: Targets `collectTeacherPersonalInfo` instead of student endpoints.

#### 🏫 K12 Strategy (ChatGPT Plus)
- **School Type Targeting**: Specifically targets schools with `type: "K12"` (not `HIGH_SCHOOL`).
- **Auto-Pass Logic**: K12 verification often **auto-approves** without document upload if the school and teacher info match.
- **Fallback**: If upload is required, it generates a Teacher Badge.

#### 🎖️ Veterans Strategy (ChatGPT Plus)
- **Strict Eligibility**: Targets Active Duty or Veterans separated within the **last 12 months**.
- **Authoritative Check**: SheerID verifies against DoD/DEERS database.
- **Logic**: Defaults to recent discharge dates to maximize auto-approval chances.

#### 🛡️ Anti-Detection Module
All tools now include `anti_detect.py` which provides:
- **Random User-Agents**: 10+ real browser UA strings (Chrome, Firefox, Edge, Safari)
- **Browser-like Headers**: Proper `sec-ch-ua`, `Accept-Language`, etc.
- **TLS Fingerprint Spoofing**: Uses `curl_cffi` to impersonate Chrome's JA3/JA4 fingerprint
- **Random Delays**: Gamma distribution timing to mimic human behavior
- **Smart Session**: Auto-selects best available HTTP library (curl_cffi > cloudscraper > httpx > requests)
- **NewRelic Headers**: Required tracking headers for SheerID API calls
- **Session Warming**: Pre-verification requests to establish legitimate browser session
- **Email Generation**: Creates realistic student emails matching university domains
- **Proxy Geo-Matching**: Matches proxy location to university country for consistency
- **Multi-Browser Impersonation**: Rotates between Chrome, Edge, and Safari fingerprints

#### 📄 Document Generation Module
New `doc_generator.py` provides anti-detection for generated documents:
- **Noise Injection**: Random pixel noise to avoid template detection
- **Color Variation**: 6 different color schemes for uniqueness
- **Dynamic Positioning**: ±3px variance on element positions
- **Multiple Types**: Student ID, Transcript, Teacher Badge
- **Realistic Details**: Random barcodes, QR codes, course grades

> [!WARNING]
> **API-Based Tools Have Inherent Limitations**
>
> SheerID uses advanced detection including:
> - **TLS Fingerprinting**: Python `requests`/`httpx` have detectable signatures
> - **Signal Intelligence**: IP address, device attributes, email age analysis
> - **AI Document Review**: Detects forged/template documents
>
> For best results: Use **residential proxies** + install `curl_cffi` for TLS spoofing.
> Browser extensions generally have higher success rates than API tools.

> [!IMPORTANT]
> **Gemini/Google One is US-ONLY (since Jan 2026)**
>
> The `one-verify-tool` only works with US IPs. International users will see verification failures.

---

## 📋 Quick Start

### Prerequisites
- Python 3.8+
- `pip`

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ThanhNguyxn/SheerID-Verification-Tool.git
    cd SheerID-Verification-Tool
    ```

2.  **Install dependencies:**
    ```bash
    pip install httpx Pillow
    ```

3.  **🚨 REQUIRED: TLS Fingerprint Spoofing:**
    ```bash
    pip install curl_cffi
    ```
    > ⚠️ **Without `curl_cffi`, success rate drops from ~60-80% to ~5-20%!**
    > SheerID detects Python's TLS fingerprint and will reject most requests.

4.  **[Optional] Cloudflare Bypass:**
    ```bash
    pip install cloudscraper
    ```

4.  **[Optional] Cloudflare Bypass:**
    ```bash
    pip install cloudscraper
    ```

5.  **Run a tool (e.g., Spotify):**
    ```bash
    cd spotify-verify-tool
    python main.py "YOUR_SHEERID_URL"
    ```

---

## 🔧 Troubleshooting: `fraudRulesReject` Error

This is the **#1 issue** users face. SheerID's fraud detection blocked your request.

### Why It Happens

| Cause | Description |
|-------|-------------|
| **TLS Fingerprint** | Python's HTTP libraries have detectable signatures |
| **Datacenter IP** | VPN/datacenter IPs are often blacklisted |
| **Request Frequency** | Too many requests from same IP |
| **Data Patterns** | Generated data looks automated |

### Solutions (in order of importance)

| Priority | Solution | Command/Action |
|----------|----------|----------------|
| 🔴 **CRITICAL** | Install `curl_cffi` | `pip install curl_cffi` |
| 🟠 **HIGH** | Use residential proxy | `--proxy http://user:pass@residential-ip:port` |
| 🟡 **MEDIUM** | Wait before retry | Wait 24-48 hours between attempts |
| 🟢 **LOW** | Try different university | Tool auto-rotates, or specify manually |
| 🟢 **LOW** | Rotate fingerprint | Each attempt generates new fingerprint |

### Quick Fix Checklist

```bash
# 1. Install curl_cffi (REQUIRED!)
pip install curl_cffi

# 2. Verify it's working
python -c "from curl_cffi import requests; print('✅ curl_cffi OK')"

# 3. Run with residential proxy
python main.py "URL" --proxy http://user:pass@residential.proxy.com:8080
```

> [!TIP]
> If you don't have a residential proxy, try [RoxyBrowser](https://roxybrowser.com?code=01045PFA) which provides anti-detect browser with residential IPs.

---

## 🦊 Official Partner: RoxyBrowser

🛡 **Anti-Detect Protection** — Unique fingerprint for each account, looks like different real devices.

📉 **Prevent Linkage** — Stops SheerID and platforms from linking your accounts.

🚀 **Ideal for Bulk Users** — Safely manage hundreds of verified accounts.

[![Try for free](https://img.shields.io/badge/Try%20for%20free-RoxyBrowser-ff6b35?style=for-the-badge&logo=googlechrome&logoColor=white)](https://roxybrowser.com?code=01045PFA)

---

## ⚠️ Disclaimer

This project is for **educational purposes only**. The tools demonstrate how verification systems work and how they can be tested.
- Do not use this for fraudulent purposes.
- The authors are not responsible for any misuse.
- Respect the Terms of Service of all platforms.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## ❤️ Support

If you find this project helpful, consider supporting me:

[![GitHub Sponsors](https://img.shields.io/badge/Sponsor-GitHub-ea4aaa?style=for-the-badge&logo=github)](https://github.com/sponsors/ThanhNguyxn)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/thanhnguyxn)

---

## 🌐 Translations

| 🇺🇸 [English](./README.md) | 🇻🇳 [Tiếng Việt](./docs/README.vi.md) | 🇨🇳 [中文](./docs/README.zh.md) | 🇯🇵 [日本語](./docs/README.ja.md) | 🇰🇷 [한국어](./docs/README.ko.md) |
|:---:|:---:|:---:|:---:|:---:|
| 🇪🇸 [Español](./docs/README.es.md) | 🇫🇷 [Français](./docs/README.fr.md) | 🇩🇪 [Deutsch](./docs/README.de.md) | 🇧🇷 [Português](./docs/README.pt-BR.md) | 🇷🇺 [Русский](./docs/README.ru.md) |
| 🇸🇦 [العربية](./docs/README.ar.md) | 🇮🇳 [हिन्दी](./docs/README.hi.md) | 🇹🇭 [ไทย](./docs/README.th.md) | 🇹🇷 [Türkçe](./docs/README.tr.md) | 🇵🇱 [Polski](./docs/README.pl.md) |
| 🇮🇹 [Italiano](./docs/README.it.md) | 🇮🇩 [Bahasa Indonesia](./docs/README.id.md) | | | |
