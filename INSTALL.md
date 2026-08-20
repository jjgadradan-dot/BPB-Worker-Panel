<h1 align="center">🐶 DogHub Panel — Installation Guide</h1>

<p align="center"><em>Step-by-step guide to install DogHub Panel on Cloudflare — free, no server needed</em></p>

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Method 1: Online install with BPB Wizard (recommended)](#2-method-1-online-install-with-bpb-wizard-recommended)
3. [Method 2: Install with Wizard CLI](#3-method-2-install-with-wizard-cli)
4. [Method 3: Build a custom version (for developers)](#4-method-3-build-a-custom-version-for-developers)
5. [First login](#5-first-login)
6. [Getting your configs](#6-getting-your-configs)
7. [Update & delete](#7-update--delete)

---

## 1. Prerequisites

- **A free Cloudflare account** — [sign up here](https://dash.cloudflare.com/sign-up/) and confirm your email. (No domain purchase required)
- For the terminal method: **PowerShell** (Windows), **Termux** (Android), or a Linux/macOS terminal.
- A client app such as **v2rayNG**, **Streisand**, **sing-box**, or **Hiddify**.

> 💡 The whole installation takes under **2 minutes** and runs entirely on Cloudflare's free plan.

---

## 2. Method 1: Online install with BPB Wizard (recommended)

The easiest way is the web edition of [BPB Wizard](https://github.com/bia-pain-bache/BPB-Wizard):

```url
https://wizard.bpb-panel.workers.dev
```

### Step 1: Create an API Token

1. In the Cloudflare dashboard go to **My Profile → API Tokens** (or use the link the wizard gives you).
2. Click **Create Token** and pick the dedicated BPB template.
3. Name it, create the token and **copy it immediately** (it is shown only once).

### Step 2: Install the panel

1. Paste the token into the wizard.
2. Choose a deployment method:

   | Method | Panel URL | Note |
   |---|---|---|
   | **Workers** | `panel.<username>.workers.dev/<path>` | Recommended to start |
   | **Pages** | `panel.pages.dev/<path>` | Use if workers.dev is not reachable for you |

3. Fill in the initial settings (the wizard suggests random values):
   - **Panel Password** — a strong password you'll remember.
   - **Proxy IP path (Secure Path)** — a random secret path for your configs.
   - **UUID / Trojan Password** — generated automatically.
4. Hit install; after a few seconds you'll get your **panel URL**. ✅
5. After the first install the wizard also gives you a **Private Link** enabling **one-click** future installs on the same account — keep it somewhere safe.

---

## 3. Method 2: Install with Wizard CLI

The CLI edition works on Windows, Android, Linux and macOS and supports **multiple Cloudflare accounts** (logins are stored on your own device).

### Windows (PowerShell)

```powershell
irm https://raw.githubusercontent.com/bia-pain-bache/BPB-Wizard/main/install.ps1 | iex
```

### Android (Termux) — Linux — macOS

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/bia-pain-bache/BPB-Wizard/main/install.sh)
```

> ⚠️ **Important Termux notes**
> - Install Termux [from the official GitHub releases](https://github.com/termux/termux-app/releases/latest), **not** Google Play (the Play version is outdated and breaks).
> - Preferably turn your VPN **off** before running the script.

The script walks you through everything: login with API token, Workers or Pages, panel password and secure path — just like the web edition.

---

## 4. Method 3: Build a custom version (for developers)

If you want to customize this fork (DogHub), you can build it yourself.

**Requirement:** Node.js 20+

```bash
git clone https://github.com/jjgadradan-dot/BPB-Worker-Panel.git
cd BPB-Worker-Panel
npm install
npm run build
```

The output is a single file: `dist/worker.js` (the whole panel bundled into one file).

To type-check the code before building:

```bash
npm run check
```

> ⚠️ **Important:** Panel v5 requires embedded settings (`EMBEDED_SETTINGS`) that are only created by **BPB Wizard** during installation. So the local build is intended for **development, debugging and code review** — the final deployment to your Cloudflare account still goes through the wizard (methods 1 or 2).

---

## 5. First login

1. Open the URL the wizard gave you, something like:

   ```
   https://my-panel.my-account.workers.dev/MySecretPath123
   ```

2. On the login page enter:
   - **Username:** your Cloudflare account email
   - **Password:** the password you set during installation
3. You're in — the DogHub panel greets you with its settings and config tabs.

> 🔐 Your panel URL contains the Secure Path — that's what makes it unguessable for strangers. Keep the URL to yourself.

---

## 6. Getting your configs

1. Go to the **Configs** tab.
2. Click **Best Pings** to find the best IPs for your connection.
3. Press **Generate Configs** to create your subscription link.
4. Add the subscription link to your client app (v2rayNG, Streisand, sing-box, Hiddify, …).
5. From the panel tabs you can change clean IP, Proxy IP, ports, Warp and more, then regenerate configs.

See the [full list of supported clients](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/usage/supported-clients/) and minimum versions.

---

## 7. Update & delete

- **Update:** when a new version is released the panel notifies you and updates itself in seconds via the **Update** button (your settings and configs are preserved).
- **Delete:** press **Delete** inside the panel, or remove the corresponding Worker/Pages project from the Cloudflare dashboard.
- **Troubleshooting:** if the panel doesn't open, first double-check the secure path (no extra `/` at the start or end), then check the [FAQ](https://bia-pain-bache.github.io/BPB-Worker-Panel/en/faq/).

---

## Useful links

- [Full settings guide](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/configuration/)
- [Config usage guide](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/usage/)
- [BPB Wizard repository](https://github.com/bia-pain-bache/BPB-Wizard)
- [FAQ](https://bia-pain-bache.github.io/BPB-Worker-Panel/en/faq/)

---

<details>
<summary>🌍 نسخه فارسی این راهنما</summary>

راهنمای فارسی نصب رو در [INSTALL_fa.md](INSTALL_fa.md) ببینید.

</details>
