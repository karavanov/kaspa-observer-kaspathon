# Kaspa Observer

<p align="center">
  <img src="logo-high-res.png" alt="Kaspa Observer" width="360">
</p>

**Kaspa Observer** is a real-time, read-only, non-custodial portfolio dashboard for the Kaspa ecosystem — **your pocket observer for Kaspa addresses**.

It allows users to track multiple wallets and notable addresses in one place, delivering instant balance changes alongside KRC-20 tokens, KRC-721 NFTs, and KNS domains — without custody, signing, or transaction capabilities.

---

## 🔗 Links

- **Live Web App:** https://www.kasobs.app  
- **Demo Video:** https://www.youtube.com/shorts/qR-7dPZchRc  
- **Chrome Web Store:** https://chromewebstore.google.com/detail/kaspa-observer/hnhhgcggnahdcjgngkpojdoijabodfgb  
- **iOS TestFlight (beta):** https://testflight.apple.com/join/vh51VTmD  
- **GitHub Repo:** https://github.com/karavanov/kaspa-observer-kaspathon  
- **Discord:** https://discord.gg/QA5jTrWD  

---

## 🧭 Summary

Kaspa Observer helps users monitor multiple Kaspa wallets and public addresses without bouncing between block explorers.

Designed as a **pocket observer**, it combines real-time balance updates, rich asset context, and offline resilience into a single, clean portfolio-style interface — focused purely on observation and insight.

The app is **read-only and non-custodial by design**:
- no private keys
- no transaction signing
- no custody
- no ability to move funds

All data is retrieved from public blockchain infrastructure and backend APIs.

---

## ✨ Features

- **Multi-address watchlists** with portfolio-style grouping and sorting  
- **Real-time balance updates** via WebSocket (REST fallback)  
- **Offline-friendly mode** with cached balances and history  
- **KRC-20 token tracking** with rich metadata  
- **KRC-721 NFT media gallery** with previews  
- **KNS domains and profiles** linked to observed addresses  
- **Balance history and price charts** for quick insights  
- **Multilingual UI** (EN / DE / RU)  
- **QR tools**: scan, generate, share, and save address QR codes  

---

## 🏗 Architecture (Short)

- **Flutter UI** with Provider-based state management  
- **WebSocket backend** for live balance and UTXO updates  
- **REST services** for initial loads, fallback, prices, and history  
- **Local cache** using Hive and SharedPreferences  

**Backend dependency:**  
The app subscribes to addresses via a dedicated WebSocket backend and receives live balance / UTXO updates. REST endpoints are used for fallback and initial data loading.

---

## 🧱 Code Structure (Snapshot)

- **Providers:** 20  
- **Widgets:** 32  
- **Screens:** 8  
- **Services:** 7  
- **Models:** 26  
- **Dart files:** 116  
- **Lines of code (`lib/`):** ~23,600  

The codebase is structured for scalability and cross-platform reuse.

---

## 📱 Platforms & Builds

- 🌍 Web app (https://www.kasobs.app)  
- 🧩 Chrome extension (built from the web package)  
- 📱 Android & iOS  
- 🖥 Desktop targets (macOS, Windows, Linux)  

---

## 🧰 Tech Stack

- **Flutter (Dart)**  
- **Provider** (state management)  
- **Hive** (local cache)  
- **WebSocket + REST APIs**  
- **Kaspa / Kasplex / KNS APIs**  

---

## ⚙️ Environment

- **Flutter:** 3.4+  
- **Dart:** >= 3.4  

---

## 🔐 Security & Philosophy

Kaspa Observer is intentionally **non-custodial and read-only**.

- No private keys are ever requested or stored  
- No transactions can be created or signed  
- The app cannot move funds under any circumstances  

This design minimizes risk and makes Kaspa Observer suitable for monitoring personal wallets, whales, and public addresses alike.

---

## 📌 About

Kaspa Observer provides real-time visibility into the Kaspa network through a clean, portfolio-style interface — combining live data, offline resilience, and rich on-chain context in a single observer-focused experience.
