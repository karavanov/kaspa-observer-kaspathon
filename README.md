# Kaspa Observer 𐤊

<p align="center">
  <img src="assets/logo/logo-high-res.png" alt="Kaspa Observer" width="360">
</p>

Kaspa Observer is a real-time, read-only, non-custodial dashboard for the Kaspa ecosystem.

It is designed as a practical pocket observer for tracking multiple Kaspa addresses, balances, KRC-20 tokens, KRC-721 NFTs, and KNS domains in one interface.

---

## Solution Platforms

- Web application
- Chrome extension
- iOS app
- Android app
- Desktop (macOS, Windows, Linux)

---

## Links

- Live Web App: https://www.kasobs.app
- Demo Video: https://www.youtube.com/shorts/qR-7dPZchRc
- Chrome Web Store: https://chromewebstore.google.com/detail/kaspa-observer/hnhhgcggnahdcjgngkpojdoijabodfgb
- iOS App Store: https://apps.apple.com/app/kaspa-observer/id6749205046
- iOS TestFlight: https://testflight.apple.com/join/vh51VTmD
- GitHub Repo: https://github.com/karavanov/kaspa-observer-kaspathon
- Discord: https://discord.gg/QA5jTrWD
- DoraHacks BUIDL: https://dorahacks.io/hackathon/kaspathon/buidl

---

## What Kaspa Observer Solves

1. Multi-wallet visibility in one place.
2. Safe monitoring without private keys or signing.
3. Fragmented token/NFT/domain tooling across separate services.
4. Real-time transfer and balance awareness.
5. Flexible grouping and personalized layout.

---

## Summary

Kaspa Observer solves multi-address monitoring fragmentation by combining live blockchain updates, token/NFT/domain context, and local resilience into a single dashboard.

Core principles:

- Read-only
- Non-custodial
- No private keys
- No signing
- No transaction execution

---

## Core Features

- Multi-address watchlists with grouping, filtering, and sorting
- Real-time KAS balance updates (WebSocket) with REST fallback
- Offline-aware behavior with cached balances/history/settings
- KRC-20 token tracking with metadata
- KRC-721 NFT media and gallery support
- KNS domain and profile context
- Balance history and price charting
- QR scan/share/save workflows
- Localization: EN / DE / RU / ES / FR / ZH

---

## Architecture Overview

- Flutter UI layer (`screens` + reusable `wedgets`)
- Provider-based state layer (`lib/providers`)
- Service/data access layer (`lib/services`)
- Typed domain models (`lib/models`)
- Persistent storage via Hive boxes and SharedPreferences keys
- Platform-aware networking (`network_status_provider_io/web`)

---

## Runtime Layers

### UI Layer

- `lib/screens` contains page-level composition and navigation targets.
- `lib/wedgets` contains reusable section widgets and visual components.

### State Layer

- `lib/providers` contains Provider-based orchestration.
- Providers manage lifecycle, loading flags, cache-vs-network state, and UI notifications.

### Service Layer

- `lib/services` contains network clients, storage gateways, and operational helpers.
- Services are focused on data acquisition, persistence, and adaptation.

### Domain Layer

- `lib/models` defines typed entities for balances, groups, transactions, KRC20, KRC721, KNS, and historical series.

---

## Main Data Flow

### Startup

1. Flutter binds and initializes Hive.
2. Hive adapters are registered.
3. Storage boxes are opened.
4. Providers are composed in `main.dart`.
5. Initial cache data is loaded and rendered.

### Live Mode

1. WS provider subscribes to address-level updates.
2. REST provider performs bootstrap and fallback loading.
3. Domain providers (`KRC`, `KRC721`, `KNS`) enrich per-address context.
4. Balance and chart providers merge streams and cached values for UI.

### Offline/Cache Continuity

1. Network status provider detects connectivity.
2. Cache mode provider computes ONLINE/OFFLINE/CACHE state.
3. UI consumes cached data while network recovery runs in background.

---

## Client-Server Interaction

Kaspa Observer communicates with these backend/API blocks:

- WS gateway for live address-level updates
- Kaspa REST nodes for bootstrap and fallback refresh
- KRC-20 API service for token balances and metadata
- KRC-721 API service for NFT ownership and metadata/media
- KNS API service for domains, profiles, and primary-name resolution
- Price feed service for chart/range data
- Feedback worker for user feedback delivery
- Optional analytics provider (user-controlled)

Data channels:

- WebSocket for stream updates
- REST for initial load/recovery/enrichment
- Hive + SharedPreferences for local persistence

---

## Repository Structure

- `lib/config` - global runtime configuration and timeouts
- `lib/models` - address/token/NFT/KNS/history data models
- `lib/providers` - state orchestration and reactive data flow
- `lib/services` - API/storage/analytics/feedback services
- `lib/screens` - page-level UI composition
- `lib/wedgets` - reusable UI components and section widgets
- `lib/localization` - locale dictionaries and language setup
- `lib/theme` - app theming
- `web` - web runtime assets and extension bridge scripts

---

## Persistence Model

Storage technologies:

- Hive for structured local objects and settings
- SharedPreferences for lightweight key-value state

Persisted categories include:

- Addresses and groups
- Token/NFT/domain caches
- Media caches (KNS/KRC721)
- Price and balance history points
- User settings (appearance/sorting/filtering/language/analytics flags)

---

## Reliability Controls

- Request timeouts configured in `lib/config/app_globals.dart`
- WS reconnection, ping, and health-state signaling
- REST fallback for degraded WS/network conditions
- Local cache warm start and continuity behavior
- Per-address loading states for responsive partial refresh

---

## Security Posture

Kaspa Observer is read-only and non-custodial by design:

- No private key collection
- No seed phrase handling
- No transaction signing
- No fund movement capability

---

## Codebase Snapshot

Current repository metrics (`lib/`):

- Providers: 20
- Widgets (`lib/wedgets`): 58
- Screens: 9
- Services: 10
- Models: 26
- Dart files (`lib/`): 149
- Lines of code (`lib/`): ~28,798

---

## Platforms

- Web app
- Chrome extension (from web build package)
- iOS / Android targets
- macOS / Windows / Linux targets

---

## Tech Stack

- Flutter (Dart)
- Provider
- Hive + SharedPreferences
- WebSocket + REST
- Kaspa / Kasplex / KNS APIs

---

## Environment

- Dart SDK: `>=3.4.1 <4.0.0`
- Flutter: stable channel compatible with current dependencies
