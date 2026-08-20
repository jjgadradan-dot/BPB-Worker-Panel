<h1 align="center">🐶 DogHub Panel — Installation Guide</h1>

<p align="center"><em>Step-by-step guide to install DogHub Panel on Cloudflare — free, no server needed</em></p>

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Method 1: Online install with BPB Wizard (recommended)](#2-method-1-online-install-with-bpb-wizard-recommended)
3. [Method 2: Install with Wizard CLI](#3-method-2-install-with-wizard-cli)
4. [Method 3: Build a custom version (for developers)](#4-method-3-build-a-custom-version-for-developers)
5. [Method 4: Manual install on Cloudflare (no wizard)](#5-method-4-manual-install-on-cloudflare-no-wizard)
6. [First login](#6-first-login)
7. [Getting your configs](#7-getting-your-configs)
8. [Update & delete](#8-update--delete)

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

> ⚠️ **Important:** Panel v5 requires embedded settings (`EMBEDED_SETTINGS`) that are either created by **BPB Wizard** during installation or added manually to the top of the script (see Method 4).

---

## 5. Method 4: Manual install on Cloudflare (no wizard)

If you prefer not to use the wizard, you can install the panel manually and directly on your Cloudflare account. It's a bit more technical but gives you full control.

### Step 1: Get the `worker.js` file

Two options:

- **Build from this fork's source (DogHub):**

  ```bash
  git clone https://github.com/jjgadradan-dot/BPB-Worker-Panel.git
  cd BPB-Worker-Panel
  npm install
  npm run build
  ```

  Output: `dist/worker.js`

- **Download the latest official build:**

  ```url
  https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.js
  ```

### Step 2: Create a KV Namespace

The panel stores its password, settings and Warp data in KV:

1. Cloudflare dashboard → **Storage & Databases → KV**
2. Click **Create namespace** and give it a name (e.g. `doghub-kv`).

### Step 3: Create an API Token (optional but recommended)

The token is used for in-panel updates, custom domains and Warp. Without it the panel and configs still work, but those features won't.

1. **My Profile → API Tokens → Create Token**
2. Pick the **Edit Cloudflare Workers** template (add **DNS → Edit** too if you plan to use a custom domain later).
3. Create the token and **copy it immediately**.

### Step 4: Create the Worker and add the settings

1. In the dashboard go to **Compute (Workers & Pages) → Create → Worker**
2. Name it (e.g. `doghub`), **Deploy**, then click **Edit code**.
3. On the **first line** of the editor paste this block and fill in your values:

   ```js
   Object.assign(globalThis, {
       EMBEDED_SETTINGS: {
           accID: "ACCOUNT_ID",
           accEmail: "you@example.com",
           apiToken: "YOUR_API_TOKEN",
           vlUUID: "A_RANDOM_UUID",
           trPass: "A_RANDOM_STRONG_PASSWORD",
           securePath: "MySecretPath123",
           proxyIpMode: "proxyip",
           proxyIPs: [],
           prefixes: [],
           fallback: "",
           dohUrl: "https://cloudflare-dns.com/dns-query",
           mainDomain: "doghub.yourname.workers.dev"
       }
   });
   ```

4. Paste the entire `worker.js` content (step 1) **below this block** and hit **Deploy**.

**Field reference:**

| Field | Value |
|---|---|
| `accID` | Your account ID — copy it from the dashboard home page, **Account ID** (right sidebar) |
| `accEmail` | The email you log into Cloudflare with |
| `apiToken` | The token from step 3 |
| `vlUUID` | A random UUID — from [uuidgenerator.net](https://www.uuidgenerator.net/) or any similar tool |
| `trPass` | A strong random string (the Trojan password) |
| `securePath` | The secret panel path — letters, digits, `-` and `_` (e.g. 16 random chars) |
| `proxyIpMode` | `proxyip` or `prefix` (for NAT64) |
| `proxyIPs` | List of Proxy IPs — empty `[]` means public defaults |
| `prefixes` | List of NAT64 prefixes — empty `[]` means defaults |
| `fallback` | Fallback destination (can be empty) |
| `dohUrl` | DoH server — the Cloudflare default works fine |
| `mainDomain` | Your worker address **without `https://`** — exactly the one created in step 4 (e.g. `doghub.yourname.workers.dev`) — used in config links |

### Step 5: Bind the KV to the worker

1. Open the worker's **Settings → Bindings**
2. Click **Add binding → KV Namespace**.
3. The **Variable name must be exactly `kv`** (lowercase) — then select the KV namespace from step 2.
4. Save and redeploy.

> ⚠️ **Important:** do **not** define `UUID` or `TR_PASS` environment variables! Panel v5 treats them as a legacy install and refuses to start.

### Step 6: Open the panel

Your panel URL looks like:

```
https://doghub.yourname.workers.dev/MySecretPath123/panel
```

Since no password is set yet, the panel opens the **Set Password** dialog:

- **Username:** your account email (`accEmail`)
- **Password:** a strong password — at least 8 characters, with an uppercase letter and a number

From then on you log in with that password. That's it!

---

## 6. First login

1. Open the URL the wizard gave you, something like:

   ```
   https://my-panel.my-account.workers.dev/MySecretPath123
   ```

2. On the login page enter:
   - **Username:** your Cloudflare account email
   - **Password:** the password you set in the wizard (if you installed manually, the **Set Password** dialog opens on your first visit and you set it right there)
3. You're in — the DogHub panel greets you with its settings and config tabs.

> 🔐 Your panel URL contains the Secure Path — that's what makes it unguessable for strangers. Keep the URL to yourself.

---

## 7. Getting your configs

1. Go to the **Configs** tab.
2. Click **Best Pings** to find the best IPs for your connection.
3. Press **Generate Configs** to create your subscription link.
4. Add the subscription link to your client app (v2rayNG, Streisand, sing-box, Hiddify, …).
5. From the panel tabs you can change clean IP, Proxy IP, ports, Warp and more, then regenerate configs.

See the [full list of supported clients](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/usage/supported-clients/) and minimum versions.

---

## 8. Update & delete

- **Update:** when a new version is released the panel notifies you and updates itself in seconds via the **Update** button (your settings and configs are preserved). ⚠️ If you installed manually or use the DogHub fork, the Update button installs the official upstream build — for your own version, rebuild and replace the code in the worker editor instead.
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
