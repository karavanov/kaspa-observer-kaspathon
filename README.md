# Kaspa Observer

<p align="center">
  <img src="logo-high-res.png" alt="Kaspa Observer" width="360">
</p>

Real-time Kaspa portfolio dashboard for tracking multiple addresses, tokens, NFTs, and domains in one place.

## Links
- Live app: https://www.kasobs.app
- Demo video: https://www.youtube.com/shorts/qR-7dPZchRc
- Chrome Web Store: https://chromewebstore.google.com/detail/kaspa-observer/hnhhgcggnahdcjgngkpojdoijabodfgb
- iOS TestFlight beta: https://testflight.apple.com/join/vh51VTmD
- GitHub repo: https://github.com/karavanov/kaspa-observer-kaspathon
- Discord: https://discord.gg/QA5jTrWD

## Summary
Kaspa Observer helps users monitor multiple wallets and notable addresses without bouncing between explorers. It combines live balance changes with KRC-20 tokens, KRC-721 media, and KNS domains, plus grouping, sorting, and history.

## Features
- Multi-address watchlists with grouping and sorting
- Real-time balance updates via WebSocket (REST fallback)
- KRC-20 token holdings and metadata
- KRC-721 NFT media gallery
- KNS domains and profiles
- Balance history and price charts
- Multi-language UI (EN/DE/RU)
- QR scanning and sharing

## Architecture (short)
- Flutter UI + Provider state management
- REST services for balances/price/history
- WebSocket backend for live updates
- Local cache (Hive + SharedPreferences)

Backend dependency: the app subscribes to addresses over a dedicated WebSocket backend and receives live balance/UTXO updates. 
REST nodes are used for fallback and initial loads.

## Code Structure (snapshot)
- Providers: 20
- Widgets: 32
- Screens: 8
- Services: 7
- Models: 26
- Dart files: 116
- Lines of code (lib/): ~23,642

## Platforms & Builds
- Web app (kasobs.app)
- Chrome extension (built from web package)
- Android and iOS targets
- Desktop targets included (macOS, Windows, Linux)

## Tech Stack
Flutter, Provider, Hive, WebSocket + REST APIs.

## Environment
Flutter 3.4+ (Dart >= 3.4)
