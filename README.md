# CyVault: Digital Risk Protection

> "There's no silver bullet in cybersecurity; only layered defense works."

CyVault is an AI-assisted **Digital Risk Protection** prototype that helps a brand find fake websites, copycat apps, scam links, malicious APK files and copied logos. Every item gets a risk score from 0 to 100, and every score comes with plain-language reasons, so nothing is a black box.

It is a hackathon prototype built as a **single HTML file**. It needs no server, no install and no internet connection to run.

Built by Rupa Puvvala.

---

## Quick start

1. Download `cyvault-v5.html`.
2. Open it in a modern browser (Chrome or Edge recommended).
3. On the login screen, press **Continue as demo user**.
4. On **Brand setup**, enter a brand name, official handle and official website, then press **Scan brand**.

Example brand to try:

| Field | Example |
|---|---|
| Brand name | Nova Bank |
| Official handle | novabank |
| Official website | novabank.com |
| Official app name | Nova Mobile |
| Package ID | com.novabank.app |

---

## Features

| Section | What it does |
|---|---|
| **Brand setup** | Stores your official handle, website, app, package ID and logo. This is the allow-list and the reference for every comparison. |
| **Evidence Report** | Overview cards, risk distribution donut, 12-week threat chart, a searchable, filterable, sortable table of flagged items, CSV export, and a history of every check. |
| **Threat detail** | Score gauge, full evidence list, similarity breakdown bars, status buttons (Safe, Investigating, Reset) and a takedown report. |
| **Takedown report** | Auto-drafts a removal request addressed to Google Play or App Store, the domain registrar, or the social platform, with numbered evidence. |
| **App Monitoring** | Ranked list of copycat apps, an official-app card for comparison, and a form to report a fake app (name, publisher, store, permissions, description, icon). |
| **Websites and Report** | Look-alike domain list and a form to report a fake website (domain, age, HTTPS, asks for OTP or card). |
| **URL Scanner** | Scores up to 10 pasted links for domain tricks, scam keywords, file downloads, missing HTTPS and imitation of your brand domain. |
| **APK Scanner** | Static analysis of an APK file (or pasted permissions): dangerous permissions, download source, missing signature, hidden droppers, SHA-256 fingerprint. The app is never run or uploaded. |
| **Logo Scanner** | Compares a suspicious picture or app icon with your official logo using shape, layout and colour similarity. |
| **Scam Alerts** | Six scam types with how each happened, warning signals and how to stay safe. |
| **Honeypot AI** | Simulation: when a scammer opens your account, a decoy balance is shown instead of the real one while every action is logged as evidence. |
| **Risk Dashboard** | All scam information in one place, with a downloadable **PDF report**. |
| **Check** | Quick domain lookup, saved to the Evidence Report history. |
| **Architecture** | A seven-step explanation of how CyVault works. |
| **AI Chat** | Type or speak questions. Voice replies can be switched on or off. |
| **Accounts and themes** | Sign up, sign in, demo user, account code to move an account between devices, and a light/dark theme. |

---

## How risk is scored

Each score adds up weighted signals and shows every reason.

| Level | Score |
|---|---|
| Low | 0 to 29 |
| Medium | 30 to 59 |
| High | 60 to 79 |
| Critical | 80 to 100 |

**Apps:** name similarity, publisher mismatch, icon similarity, description similarity, scam words in the name, third-party store, risky permissions (SMS, Contacts, Accessibility, Overlay), low or fake reviews.

**Websites and URLs:** similarity to your official domain, risky endings (.xyz, .top and similar), scam keywords, hyphens and digits mixed into words, new domain, missing HTTPS, raw IP address, link shorteners, punycode, file downloads, OTP or PIN in the address.

**APK files:** dangerous permissions, download source, missing compiled code, unsigned package, hidden APK or DEX in assets, very small installer, brand name from an unofficial source, and the SMS plus screen-control banking-trojan pattern.

**Logos:** shape correlation (40%), layout (30%) and colour mix (30%).

**Official assets** that match your handle, website, or app plus publisher score **0** and are never flagged.

Scores are estimates to help a person review quickly. They are not proof of fraud.

---

## Privacy and storage

- Everything runs **in your browser**. Nothing is uploaded to a server.
- Passwords are never stored. Only a salted SHA-256 hash is kept.
- Data is saved in browser `localStorage` under `cv_user`, `cv_accts` and `cv_honeypot`.
- Accounts are per browser. To use an account on another device, choose **Copy account code** in the sidebar, then paste it in the login screen's "Signed up on another device?" section. The code holds only the salted hash.
- This is a demo. Do not treat the login as production-grade security.

---

## Tech

- Plain HTML, CSS and JavaScript in one file, with no frameworks and no build step.
- Web Crypto for hashing, `DecompressionStream` for reading APK contents, Canvas for logo comparison, and the Web Speech API for voice input and output.
- Fuzzy name matching uses Levenshtein distance plus a "leet-speak" normaliser (for example 0 to o, 1 to l).
- The PDF report is generated directly in the browser, with no library.
- The AI chat uses a live Claude connection when the host provides one. Otherwise it falls back to a built-in knowledge base covering common scams, OTP and UPI safety, KYC, SIM swap, malware, QR codes, loan apps and more.

---

## Browser support

| Feature | Needs |
|---|---|
| Sign in, APK hash | Web Crypto (secure context, such as `https://`, `localhost` or a local file in most browsers) |
| APK scanning | A browser with `DecompressionStream` (current Chrome, Edge, Safari, Firefox) |
| Voice input (microphone) | Chrome or Edge (Web Speech Recognition) |
| Voice replies | Any browser with speech synthesis |

---

## Limitations

- App and website lists are **generated sample data** based on your brand details. They are not pulled from live app stores or the web. You can add real findings by hand or by using the scanners.
- The URL Scanner uses heuristics and **no live blocklist**. A Low score means "no red flags found", not "guaranteed safe".
- The logo check is approximate, so review matches by eye.
- The APK scan is static. It does not run the app.
- Honeypot AI is a simulation and does not connect to any real bank.
- Score-band text on the Architecture page, in the built-in chat answer and in the PDF report (High 70+, Medium 40 to 69, Low below 40) differs from the badge thresholds above, which are the ones actually used.

---

## If you have been scammed (India)

1. Call the cyber crime helpline **1930** as soon as possible.
2. Report at **cybercrime.gov.in**.
3. Call your bank to block cards, UPI and net banking.
4. Change passwords for banking, email and social accounts.
5. Keep screenshots, links, numbers and transaction IDs as proof.

---

## Project structure

```
cyvault-v5.html   # the entire app: styles, logic, mock data, UI
README.md         # this file
```
