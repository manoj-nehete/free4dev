<div align="center">

```text
   __ _  _       _ 
  / _| || |   __| |
 | |_| || |_ / _` |
 |  _|__   _| (_| |
 |_|    |_|  \__,_|  v1.0.0
```

# Free4Dev (`f4d`)
### Authoritative Anycast Subdomains for Vibe Coders & Indie Hackers

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Next.js 15](https://img.shields.io/badge/Next.js-15-black?logo=next.js)](https://nextjs.org/)
[![DNS Backbone](https://img.shields.io/badge/DNS-Hetzner%20Anycast-red?logo=hetzner)](https://hetzner.com)
[![2FA Shield](https://img.shields.io/badge/2FA-Telegram%20Bot-blue?logo=telegram)](https://telegram.org)
[![Security](https://img.shields.io/badge/Audits-Cloudflare%20Harness-orange?logo=cloudflare)](https://github.com/cloudflare/security-audit-skill)

<p align="center">
  <b>Free4Dev empowers vibe coders and indie hackers with 100% free subdomains across curated apex domains. Featuring an in-place web terminal, instant Hetzner Anycast DNS synchronization, 1-click presets for Vercel and Netlify, Telegram 2FA bot security, and privacy-first WHOIS message relay.</b>
</p>

---

</div>

## 💡 The Problem & The Vision

When developers, indie hackers, and "vibe coders" build weekend prototypes, hackathon tools, or open-source experiments, they face a recurring friction point: **domains cost \$10–\$20/year per project**. 

Purchasing and configuring new domains for every creative spark creates financial friction and delays shipping. Existing free subdomain solutions often rely on slow GitOps pull requests (taking hours to days to merge) or operate without modern security, leaving their root domains vulnerable to phishing, email spam, and registry blacklisting.

**Free4Dev reimagines free developer domains from first principles:**
- **Zero Friction**: Instant self-service provisioning in under 30 seconds.
- **Zero Cost**: Completely free subdomains across multiple curated root domains.
- **Developer-Native DX**: An interactive retro-futuristic web terminal (`f4d`), backed by a persistent cross-platform CLI tool for macOS, Linux, and Windows PowerShell.
- **Bulletproof Guardrails**: Real-time multi-category anti-phishing firewalls, a strict zero-MX email policy, and mandatory Telegram 2FA on first login.

---

## 🏛️ System Architecture

Free4Dev is architected as an all-in-one, ultra-efficient full-stack platform designed to run on a single budget server (e.g. €3.79/month Hetzner VPS) while delegating 99.9% of global internet DNS queries to Hetzner’s worldwide anycast infrastructure.

```
┌────────────────────────────────────────────────────────────────────────┐
│                        DEVELOPER / VIBE CODER                          │
│                                                                        │
│   Web Terminal UI (Browser)    OR    Local Shell (Mac / Linux / Win)   │
│   `guest@free4dev:~$ f4d start`       `curl ... | bash`  /  `irm ...`  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ 1. GitHub OAuth 2.0
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                  FREE4DEV PLATFORM (Next.js 15 App)                    │
│                                                                        │
│   • In-Place Terminal State Machine (Zero URL route changes)           │
│   • Mandatory Telegram 2FA Gatekeeper (/auth/setup-2fa)                │
│   • Telegram Webhook Handler (POST /api/telegram/webhook)              │
│   • Anti-Phishing Compound Token Analyzer                              │
│   • Automated Tier Verification Engine (Follow, Star, README Badge)    │
│   • SQLite Database (Prisma ORM)                                       │
└───────────────┬───────────────────────────────────────┬────────────────┘
                │                                       │
                │ 2. Real-time Record Provisioning      │ 3. 2FA OTP & Contact Relay
                ▼                                       ▼
┌──────────────────────────────┐        ┌────────────────────────────────┐
│   HETZNER CLOUD DNS API      │        │       TELEGRAM BOT API         │
│   (https://api.hetzner.cloud)│        │       (@Free4DevBot)           │
│   • Primary Anycast Zones    │        │   • 6-Digit Login 2FA OTP      │
│   • A, CNAME, TXT (No MX)    │        │   • WHOIS Contact Relay        │
│   • Sub-second propagation   │        │   • Admin 1-Click Incident Taps│
└──────────────────────────────┘        └────────────────────────────────┘
```

---

## ⚡ Core Innovations & Features

### 1. Dual-Interface Experience (Web Terminal + Visual GUI)
- **Web Terminal (`f4d`)**: Visitors land on a retro-futuristic terminal shell (`guest@free4dev:~$`). Typing `f4d start` boots the DNS engine and displays ASCII art and command guide.
- **Dynamic Identity Morph**: Upon signing in with GitHub and verifying the Telegram 2FA code, the prompt dynamically updates to `username@free4dev:~$`.
- **Zero-URL Changes**: Commands execute in-place on the terminal screen without changing the browser address bar (`https://free4dev.com`), eliminating page refreshes and flickering query parameters.
- **GUI Toggle**: Users can switch between the interactive Web Terminal and a standard visual dashboard at any time using `f4d gui` or a floating button.

### 2. Cross-Platform Persistent CLI (`f4d`)
Developers can execute the exact same commands in their local terminal as in the browser, installed via a persistent single-line script that permanently modifies `PATH` across system reboots:
- **macOS & Linux**: `curl -fsSL https://free4dev.com/install.sh | bash`
- **Windows PowerShell**: `irm https://free4dev.com/install.ps1 | iex`
- **Universal Zero-Install**: `npx free4dev start`

### 3. 1-Click Platform Presets ("Quick Connect")
Rather than manually wrestling with raw DNS configurations, developers can connect their subdomains in 1 click:
- **Vercel**: Configures `CNAME` pointing to `cname.vercel-dns.com` (with optional verification TXT).
- **Netlify**: Points `CNAME` to `<site-name>.netlify.app`.
- **Cloudflare Pages**: Points `CNAME` to `<project>.pages.dev`.
- **GitHub Pages**: Points `CNAME` to `<user>.github.io` + ownership challenge TXT.
- **Render**: Points `CNAME` to `<service>.onrender.com`.
- **Custom VPS**: Configures authoritative `A` record pointing to public IPv4.

### 4. Uncompromising Security & Abuse Prevention
Free subdomain services are frequent targets for malicious actors. Free4Dev enforces four defensive tiers:
- **Strict Zero-MX Policy**: Free4Dev strictly forbids `MX`, `NS`, `SOA`, and `SRV` records. Subdomains cannot be configured for email routing, eliminating email spoofing, spam blasting, and protecting root domain sender reputation.
- **Multi-Category Compound Blocklist**: Tokenizes incoming subdomain requests (e.g. `secure-paypal-login` $\rightarrow$ `['secure', 'paypal', 'login']`) and blocks financial, banking, credential-theft, and brand-impersonation keywords.
- **Mandatory 1st-Login Telegram 2FA**: Every user must link their Telegram account and verify a 6-digit OTP before gaining dashboard access, completely neutralizing disposable bot account farms.
- **Cloudflare Security Audit Workflow**: Pre-configured integration with Cloudflare's `security-audit` harness for automated multi-stage vulnerability verification.

### 5. Community Quota Tiers & Fair Allocation
To balance accessibility with namespace preservation, Free4Dev implements an automated, verifiable 3-tier model:
- **Tier 1 (Base - 1 Subdomain)**: Granted immediately after GitHub login + Telegram 2FA.
- **Tier 2 (Community Supporter - 3 Subdomains)**: Instant 1-click verification verifying that the user followed the GitHub profile, starred the repository, and placed the Free4Dev badge in a repo README.
- **Tier 3 (GitHub Sponsor - 10 Subdomains)**: Instant verification of GitHub Sponsorship.
- **Custom Quota Requests**: Developers building impactful open-source tools can request higher allocations; administrators receive real-time Telegram prompts with 1-click `[Approve]` / `[Reject]` actions.

### 6. Privacy-Preserving Public WHOIS & Telegram Relay
Every active subdomain has an official WHOIS registry card (`/whois/:subdomain` and `f4d whois <subdomain>`) displaying ownership transparency:
- Publicly shows registration date, status, and the owner's verified GitHub profile.
- **Anonymous Contact Form**: Visitors or security researchers can contact the subdomain owner without exposing the owner's personal email address.
- **Telegram Forwarding**: Submissions are relayed directly to the owner's Telegram chat in real time.

### 7. Automated Zombie Pruning (Inactivity Heartbeat)
To prevent permanent namespace hoarding by abandoned hackathon weekend projects:
- An automated weekly background task pings active subdomains.
- If an endpoint remains unreachable for 60 consecutive days, an automated reminder is dispatched.
- Following a 14-day grace period without response, the subdomain is safely recycled back into the public pool, and its Hetzner records are cleaned.

---

## 🛠️ Technology Stack

| Layer | Component | Purpose |
|---|---|---|
| **Framework** | Next.js 15 (App Router, Server Actions, TypeScript) | Unified full-stack web and API architecture |
| **Terminal Engine** | React/Xterm In-Place State Machine | Web terminal with command history, autocomplete & zero URL shifts |
| **Styling** | Tailwind CSS + Lucide Icons | Responsive cyber-minimalist developer aesthetic |
| **Authentication** | Auth.js / NextAuth v5 | GitHub OAuth provider + session encryption |
| **Telegram Integration** | Telegram Bot API (`grammY` / Telegraf) | Webhook-driven 2FA OTP, WHOIS relay & Admin incident alerts |
| **DNS Provider** | Hetzner Cloud DNS REST API | Sub-second Anycast provisioning for `A`, `CNAME`, `TXT` |
| **DNS Health Checks** | Cloudflare & Google DoH (DNS-over-HTTPS) | Live global propagation status validation |
| **Database & ORM** | Prisma ORM + SQLite (Dev) / PostgreSQL (Prod) | Type-safe schema for users, domains, records & audit trails |
| **CLI Distribution** | Shell (`install.sh`), PowerShell (`install.ps1`), NPX | Persistent 1-liner installation across macOS, Linux, and Windows |
| **Security Audit** | Cloudflare Security Audit Harness | 6-stage evidence-driven vulnerability review workflow |

---

## 🗺️ Project Status & Documentation

The Free4Dev project is governed by structured multi-agent collaboration specifications:

- **[PLAN.md](PLAN.md)**: Master architectural blueprint and 9-phase implementation roadmap.
- **[REQUIREMENTS.md](REQUIREMENTS.md)**: Verified external credentials, Hetzner Zone IDs, and configuration checklist.
- **[command-list.md](command-list.md)**: Complete index of all `f4d` commands with descriptions and examples.
- **[AGENTS.md](AGENTS.md)**: Collaboration protocol for Antigravity, Codex, and other AI coding agents.
- **[continuefrom.md](continuefrom.md)**: Live state tracking, completed milestones, and immediate next actions.

---

<div align="center">
  <sub>Built with ❤️ for vibe coders, indie hackers, and open-source developers worldwide.</sub>
</div>
