<div align="center">

<img src="https://img.shields.io/badge/AyTech-Contact%20Studio-4f46e5?style=for-the-badge&logo=vcard&logoColor=white" alt="AyTech Contact Studio" height="40">

# 📇 AyTech Contact Studio

### A powerful, privacy-first vCard manager that runs entirely in your browser

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![License: MIT](https://img.shields.io/badge/License-MIT-34d399?style=flat-square&logo=opensourceinitiative&logoColor=white)](LICENSE)
[![No Backend](https://img.shields.io/badge/Backend-None-fbbf24?style=flat-square&logo=shield&logoColor=white)]()
[![Privacy First](https://img.shields.io/badge/Privacy-First-818cf8?style=flat-square&logo=lock&logoColor=white)]()

<br>

> **Merge, deduplicate, normalize, and export vCards — all locally, with zero data leaving your device.**

</div>

---

## ✨ Overview

<div align="center">
  <table>
    <tr>
      <td align="center" width="25%">
        <h3>🔒</h3>
        <b>100% Client-Side</b><br>
        <sub>No servers. No uploads. No tracking.</sub>
      </td>
      <td align="center" width="25%">
        <h3>🧠</h3>
        <b>Smart Deduplication</b><br>
        <sub>Union-Find clustering by phone, email & name.</sub>
      </td>
      <td align="center" width="25%">
        <h3>📞</h3>
        <b>Phone Normalization</b><br>
        <sub>Auto-detects &amp; unifies +98 / 09xx variants.</sub>
      </td>
      <td align="center" width="25%">
        <h3>☁️</h3>
        <b>URL Import</b><br>
        <sub>Google Drive &amp; GitHub links supported.</sub>
      </td>
    </tr>
  </table>
</div>

**AyTech Contact Studio** is a single-file, browser-based application for managing `.vcf` (vCard) contact files. Whether you're migrating between phones, cleaning up duplicate entries after a merge, or normalizing Iranian phone numbers to international `+98` format — everything happens instantly, offline, and securely.

---

## 🚀 Features

<table>
  <tr>
    <td width="50%" valign="top">

### 📥 Import
- 🗂️ **Drag & Drop** multiple `.vcf` files at once
- 📄 **File Picker** for traditional uploads
- 🔗 **Import from URL** — direct `.vcf` links
- ☁️ **Google Drive** share links (auto-converted to direct download)
- 🐙 **GitHub** blob links (auto-converted to raw content)
- 📦 Supports **vCard 2.1, 3.0 & 4.0**
- 🔤 Handles **quoted-printable** encoding (vCard 2.1)

    </td>
    <td width="50%" valign="top">

### 🧹 Manage
- 🔍 **Live search** across name, phone, email, org, notes, and source
- 🏷️ **Filter by source file**
- 📊 **Sortable columns** (name, phone, email, org, source)
- ✏️ **Inline editing** of any contact
- 🗑️ **Bulk selection** & deletion
- 📑 **Pagination** (25 / 50 / 100 / 250 per page)
- 💾 **Auto-save** via IndexedDB (falls back to localStorage)

    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">

### 🧠 Deduplicate
- ⚡ **Union-Find** algorithm for near-instant clustering
- 📞 Match by **normalized phone number**
- ✉️ Match by **canonical email**
- 👤 Match by **full name**
- 🔀 Toggle strategies independently
- 👀 **Live preview** of merge clusters before applying
- 📝 Detailed **match reasons** per cluster

    </td>
    <td width="50%" valign="top">

### 📤 Export
- 💾 **vCard 3.0** format (universal compatibility)
- 📞 **Phone normalization** to `+98` international format
- 🎯 Export **all** or **selected** contacts
- 🏷️ Preserves source info via `X-AYTECH-SOURCE`
- 🔁 Line folding at 75 octets (RFC 2426 compliant)
- 📱 Compatible with Apple, Google, Outlook & Android

    </td>
  </tr>
</table>

---

## 📸 Screenshots

<div align="center">

| Dashboard | Deduplication |
|:---------:|:-------------:|
| *Coming soon* | *Coming soon* |

| Contact Editor | Export Dialog |
|:--------------:|:-------------:|
| *Coming soon* | *Coming soon* |

</div>

---

## 🎯 Key Concepts

### 📞 Iranian Phone Number Normalization

AyTech Contact Studio treats all these representations as **the same number**:

```
  +989115166854
  +98 911 516 6854
  989115166854
  09115166854
  9115166854
```

- **Deduplication** & **search** use a canonical match key (`989115166854`).
- **Export** always writes `+989115166854` (E.164-style).

This means searching `09305178688` will match a contact stored as `+989305178688` — and vice versa.

### 🧬 Deduplication Algorithm

Powered by a **Union-Find (Disjoint Set Union)** structure with path compression:

```
┌─────────────────────────────────────────────────────────┐
│  Pass 1: Build indexes                                  │
│  ├─ phoneIndex:  canonicalPhone  → contactId            │
│  ├─ emailIndex:  normalizedEmail → contactId            │
│  └─ nameIndex:   normalizedFullName → contactId         │
├─────────────────────────────────────────────────────────┤
│  Pass 2: Union matching contacts                        │
├─────────────────────────────────────────────────────────┤
│  Pass 3: Group by root, merge each cluster              │
└─────────────────────────────────────────────────────────┘
```

Each cluster's merged record intelligently combines:
- 🥇 **Longest full name** wins
- 📞 **All unique phones** (deduped by canonical key)
- ✉️ **All unique emails**
- 🏢 **First non-empty** org / title / role
- 📝 **All unique notes** joined with `---`
- 🏷️ **All source files** preserved

---

## 🛠️ Tech Stack

<div align="center">

| Layer | Technology |
|:-----:|:-----------|
| **UI** | Vanilla HTML5 + CSS3 (no frameworks) |
| **Logic** | ES2022 JavaScript Modules |
| **Storage** | IndexedDB → localStorage → in-memory |
| **Fonts** | Plus Jakarta Sans · JetBrains Mono |
| **Icons** | Inline SVG (zero dependencies) |
| **Bundle** | Single `.html` file |

</div>

> ⚡ **Zero build step.** Just open `index.html` in any modern browser.

---

## 📦 Installation

### Option 1 — Direct Download

```bash
# Clone the repository
git clone https://github.com/shammay-PC/AyTech-Contact-Studio.git

# Navigate into the folder
cd AyTech-Contact-Studio

# Open in your browser
open index.html      # macOS
start index.html     # Windows
xdg-open index.html  # Linux
```

### Option 2 — Local Server (for URL import)

Some browsers restrict `fetch()` on `file://` URLs. To use the **URL import** feature, serve the file locally:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve

# Then visit http://localhost:8000
```

### Option 3 — Host Anywhere

Since it's a single static file, you can deploy it to:

- 🐙 **GitHub Pages**
- ⚡ **Netlify**
- ▲ **Vercel**
- 🌐 **Cloudflare Pages**
- 📦 Any static host

---

## 🎮 Usage

### 1️⃣ Import Contacts

```text
┌────────────────────────────────────────────┐
│  Drag & drop .vcf files here               │
│  — OR —                                    │
│  Paste a URL:                              │
│    • https://example.com/contacts.vcf      │
│    • https://drive.google.com/file/d/ID/…  │
│    • https://github.com/u/r/blob/main/x.vcf│
└────────────────────────────────────────────┘
```

### 2️⃣ Review & Edit

- Use the **search bar** to find contacts instantly
- Click any row to open the **editor**
- Toggle columns via the **sort headers**
- Filter by **source file** using the dropdown

### 3️⃣ Deduplicate

- Click **Smart Deduplicate**
- Choose match strategies (phone / email / name)
- Review detected **clusters**
- Click **Apply Merge** to consolidate

### 4️⃣ Export

- Click **Export Merged VCF**
- Choose scope: **all** or **selected**
- Set a filename and download

---

## 🔗 URL Import Support

<table>
  <tr>
    <th>Source</th>
    <th>Input Example</th>
    <th>Auto-Resolution</th>
  </tr>
  <tr>
    <td>🌐 <b>Direct</b></td>
    <td><code>https://example.com/file.vcf</code></td>
    <td>Fetched as-is</td>
  </tr>
  <tr>
    <td>☁️ <b>Google Drive</b></td>
    <td><code>drive.google.com/file/d/FILE_ID/view</code></td>
    <td>→ <code>uc?export=download&id=FILE_ID</code></td>
  </tr>
  <tr>
    <td>🐙 <b>GitHub Blob</b></td>
    <td><code>github.com/u/r/blob/main/x.vcf</code></td>
    <td>→ <code>github.com/u/r/raw/main/x.vcf</code></td>
  </tr>
</table>

> 💡 **Google Drive Tip:** The file must be shared as *"Anyone with the link"*. AyTech automatically handles the virus-scan confirmation page.

---

## 🏗️ Architecture

```
AyTech-Contact-Studio/
├── index.html          ← Complete application (single file)
├── favicon.ico         ← Browser tab icon
├── README.md           ← This file
└── LICENSE             ← MIT license
```

### Internal Modules

```
┌──────────────────────────────────────────────────────────────┐
│                        PARSER LAYER                          │
│  decodeQuotedPrintable · unfoldVCardLines · parseVCF         │
├──────────────────────────────────────────────────────────────┤
│                       NORMALIZE LAYER                        │
│  normalizePhoneNumber · toInternationalPhone · getPhoneMatchKey│
│  normalizeEmail · normalizeName                              │
├──────────────────────────────────────────────────────────────┤
│                        DEDUPE LAYER                          │
│  UnionFind · deduplicateContacts · mergeContactCluster       │
├──────────────────────────────────────────────────────────────┤
│                        EXPORT LAYER                          │
│  serializeVCard · serializeVCards · foldVCardLine            │
├──────────────────────────────────────────────────────────────┤
│                        STORAGE LAYER                         │
│  IndexedDB  →  localStorage  →  in-memory fallback           │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔐 Privacy & Security

<div align="center">

|  |  |
|:---:|:---|
| 🚫 | **No network requests** during normal use |
| 🚫 | **No analytics**, no cookies, no telemetry |
| 🚫 | **No third-party services** |
| ✅ | **All data stays on your device** |
| ✅ | **Persistence via IndexedDB** (local only) |
| ✅ | **Works fully offline** (after first load) |
| ✅ | **Open source** — audit every line |

</div>

> The only network calls are those you explicitly trigger via **Import from URL**.

---

## 🌐 Browser Support

| Browser | Version | Status |
|:--------|:--------|:------:|
| Chrome / Edge | 90+ | ✅ |
| Firefox | 88+ | ✅ |
| Safari | 14+ | ✅ |
| Opera | 76+ | ✅ |
| Mobile Chrome | 90+ | ✅ |
| Mobile Safari | 14+ | ✅ |

> Requires ES2022 modules, IndexedDB, and the Fetch API.

---

## 🗺️ Roadmap

- [x] vCard 2.1 / 3.0 / 4.0 parsing
- [x] Smart deduplication (Union-Find)
- [x] Iranian phone normalization
- [x] Google Drive & GitHub URL import
- [x] IndexedDB persistence
- [x] Light / dark theme
- [x] Contact editor
- [ ] CSV / JSON import & export
- [ ] Group / tag management
- [ ] Profile photo (PHOTO) support
- [ ] vCard 4.0 export
- [ ] PWA offline installation
- [ ] Multi-language UI (FA / AR / EN)

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

```bash
# 1. Fork the repository
# 2. Create your feature branch
git checkout -b feature/amazing-feature

# 3. Commit your changes
git commit -m "feat: add amazing feature"

# 4. Push to the branch
git push origin feature/amazing-feature

# 5. Open a Pull Request
```

### Guidelines

- ✅ Follow existing code style (no linter, but keep it clean)
- ✅ Test in at least two browsers
- ✅ Keep it **dependency-free** (vanilla HTML/CSS/JS only)
- ✅ Update this README if you add features
- ❌ Don't introduce a build step
- ❌ Don't add tracking or analytics

---

## 📄 License

<div align="center">

**MIT License** © 2025 AyTech

[![MIT](https://img.shields.io/badge/License-MIT-34d399?style=for-the-badge)](LICENSE)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction.

</div>

---

## 💬 Acknowledgements

- 🙏 [RFC 2426](https://datatracker.ietf.org/doc/html/rfc2426) — vCard 3.0 specification
- 🙏 [RFC 6350](https://datatracker.ietf.org/doc/html/rfc6350) — vCard 4.0 specification
- 🙏 [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) — UI font
- 🙏 [JetBrains Mono](https://www.jetbrains.com/lp/mono/) — monospace font
- 🙏 [Shields.io](https://shields.io) — badges

---

<div align="center">

### ⭐ If AyTech Contact Studio saved you time, give it a star!

<a href="#top">
  <img src="https://img.shields.io/badge/⬆_Back_to_Top-4f46e5?style=for-the-badge" alt="Back to top">
</a>

<br><br>

<sub>Built with ❤️ by <a href="https://github.com/shammay-PC">AyTech</a></sub>

<sub>**No servers. No uploads. No nonsense.**</sub>

</div>