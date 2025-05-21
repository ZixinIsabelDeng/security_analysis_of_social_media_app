# 🔐 Security Analysis of Social Media Applications

This repository contains the research, methodology, and results of a comprehensive security assessment of 43 widely used social media applications and websites. The analysis identifies critical privacy and security vulnerabilities using both static and dynamic methods.

## 📄 Abstract

Social media platforms store sensitive personal data and are integral to daily communication. This project investigates vulnerabilities in web and mobile social media apps using a hybrid evaluation model involving **Burp Suite**, **Wireshark**, **MobSF**, and custom-built tools. Vulnerabilities identified include:

- Broken authentication and access control
- Cross-site request forgery (CSRF) and insecure CORS
- Injection attacks (XSS, XPath, SQL)
- Unencrypted data transmission
- Legacy Flash cross-domain policy risks
- Persistent background tracking

## 🛠️ Tools Used

| Tool         | Purpose                                                                 |
|--------------|-------------------------------------------------------------------------|
| **Burp Suite Pro** | Dynamic analysis, session/cookie validation, CSRF & injection testing |
| **Wireshark**      | Monitoring DNS/TLS traffic and detecting background activity       |
| **MobSF**          | Static analysis for mobile apps                                    |
| **Custom Python Plugin** | Automated vulnerability detection in Burp Suite using Jython       |

---

## 🔍 Methodology

The testing followed industry standards:
- **OWASP Web Security Testing Guide (WSTG)**
- **OWASP API Security Top 10**
- **OWASP Mobile Security Testing Guide (MSTG)**
- **Penetration Testing Execution Standard (PTES)**

### Steps:
1. **Static Analysis** – Performed with MobSF on Android apps.
2. **Dynamic Testing** – Authenticated scans with Burp Suite.
3. **Manual Investigation** – Used Wireshark to detect background data flow.
4. **Custom Automation** – Used Python plugin in Burp Suite for identifying missing security headers, token misuses, and cookie misconfigurations.

---

## 🧪 Sample Findings

### ⚠️ Insecure Authentication & Session Handling
- **Yiyo.io**: QR code login accepts requests without CSRF protection.
- **Mingle2.com**: Sends session cookies without the `Secure` flag over HTTP.

### 🔓 Sensitive Data in Transit
- **Rumble.com** and **Mastodon.social**: Transmit passwords and emails in plaintext.

### 🧬 Injection Vulnerabilities
- **Mengchenghui.com**: Uses vulnerable jQuery (v1.8.3), allowing XSS via `.load()`.
- **Rumble.com**: XPath injection via unsanitized user input in URL.

### 🌐 Legacy & CORS Misconfigurations
- **Tagged.com**: Permissive Flash policy with credentials allowed in CORS requests.
- **Plurk.com**: Flash crossdomain.xml allows universal access.

### 📡 Background Telemetry (While App Idle)
| Application | Behavior |
|-------------|----------|
| Facebook    | Sends data to `graph.facebook.com` and `b-graph.facebook.com` |
| YouTube     | Frequent QUIC packets with PING and CRYPTO frames |
| Instagram   | DNS and TLS handshakes with `gateway.instagram.com` |
| QQ          | Background queries to `astrategy.beacon.qq.com` |
| LinkedIn    | Sends data to `px.ads.linkedin.com` during idle time |

---

## 📋 List of Analyzed Applications

`Badoo, Bluesky, Bumble, Clubhouse, Discord, Facebook, imo, Instagram, Likee, Line, LinkedIn, Mastodon, Messenger, MeWe, Mengchenghui, Mingle2, Parler, Pinterest, Plurk, QQ, Quora, Reddit, Rumble, Skype, Snapchat, Steemit, Tango, Tapatalk, Tagged, Teams, Telegram, Threads, TikTok, Tinder, Truth Social, Tumblr, Twitch, WhatsApp, X, Yiyo, YouTube, Yubo, Zello`

---

## 💡 Key Recommendations

- Enforce secure transport: always use HTTPS and secure cookies
- Validate input: sanitize and filter user inputs to prevent XSS, XPath, SQL injection
- Fix CORS and CSRF: avoid `Access-Control-Allow-Origin: *` with credentials
- Monitor background telemetry: be transparent with users and provide opt-outs
- Deprecate Flash: remove or secure outdated Flash policy files

---

## 📢 Disclaimer

This project was conducted for educational and research purposes at **Concordia University**. No unauthorized access or disruption was performed. All findings are based on publicly accessible application behaviors.

---

## 👥 Authors

- Christelle Charles
- Zixin Deng
- Imen Khezzar
- Hanseok Kim
- Sonali Patel
- Vanisha Patel

April 2025 — SOEN 321: Information Systems Security

---

