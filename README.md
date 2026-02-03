# Kaspa Observer (Kasobs)

Real-time Kaspa wallet monitoring and portfolio insights across multiple addresses.

## Quick Links
- Live app: https://kasobs.app
- Live app (alt): https://www.kasobs.app
- Demo video: https://www.youtube.com/shorts/qR-7dPZchRc
- Chrome Web Store: https://chromewebstore.google.com/detail/kaspa-observer/hnhhgcggnahdcjgngkpojdoijabodfgb
- iOS TestFlight beta: https://testflight.apple.com/join/vh51VTmD
- GitHub repo: https://github.com/karavanov/kaspa-observer-kaspathon
- Discord invite: https://discord.gg/QA5jTrWD
- DoraHacks BUIDL page: https://dorahacks.io/hackathon/kaspathon/buidl

## TL;DR
- Track many Kaspa addresses in one dashboard
- Live updates via WebSocket with REST fallback and caching
- KRC-20 balances, KRC-721 media, and KNS domains in one place
- Flutter app for web, mobile, and desktop

## Vision
Users often manage multiple wallets and keep an eye on large or notable addresses. Kaspa Observer brings everything together in one place with smart grouping and sorting, real-time balance updates, and full support for KRC and KNS tokens and NFTs.

## Key Innovation Domains (Crypto/Web3)
Wallet, Infra/API, Kaspa, Real-time

## What It Does
- Multi-address watchlists with grouping and sorting
- Real-time balance updates via WebSocket (REST fallback)
- KRC-20 token holdings and metadata
- KRC-721 NFT media gallery
- KNS domains and profiles
- Balance history and price charts
- Multi-language UI (EN/DE/RU)
- QR scanning and sharing of addresses

## Why It Matters
Kaspa moves fast, but portfolio monitoring across many wallets is fragmented. Kaspa Observer consolidates everything into one fast, Kaspa-native view, so users can monitor important addresses and assets instantly.

## Architecture (High Level)

```
+----------------------+        +---------------------------+
| Flutter UI (screens) | <----> | Providers (state + logic) |
+----------------------+        +-------------+-------------+
                                              |
                     +------------------------+------------------------+
                     |                         |                       |
             +-------v--------+        +-------v--------+      +--------v--------+
             | REST services  |        | WS provider    |      | Local cache     |
             | (HTTP)         |        | (real-time)    |      | (Hive, prefs)   |
             +-------+--------+        +-------+--------+      +--------+--------+
                     |                         |                       |
                     +-----------+-------------+-----------+-----------+
                                 |
                         +-------v--------+
                         | External APIs  |
                         | Kaspa/KRC/KNS  |
                         +----------------+
```

### Provider Graph (from main.dart)
This is the actual dependency layout used at app startup. It shows how REST, WebSocket, and cache logic are composed and why the data is reliable under poor connectivity.

```
MultiProvider
  ThemeProvider
  MessageProvider
  NetworkStatusProvider
  AppearanceProvider
  CacheModeProvider <- NetworkStatusProvider
  AddressGroupProvider
  KasRESTProvider   <- AddressGroupProvider + NetworkStatusProvider + CacheModeProvider
  KasWSProvider     <- NetworkStatusProvider + AddressGroupProvider + CacheModeProvider
  PriceProvider     <- KasRESTProvider + KasWSProvider
  BalanceProvider   <- KasRESTProvider + KasWSProvider + CacheModeProvider
  TransactionsProvider <- KasWSProvider + KasRESTProvider
  KrcServiceProvider / KrcProvider
  Krc721ServiceProvider / Krc721Provider
  KnsServiceProvider / KnsProvider
  PriceChartProvider
  BalanceSparklineProvider
```

### Data Flow (Price + Balances)
1. NetworkStatusProvider detects online/offline state.
2. CacheModeProvider decides whether to use cached data or live data.
3. KasRESTProvider fetches price and balances (node fallback).
4. KasWSProvider streams live price and UTXO updates.
5. BalanceProvider, PriceProvider, and TransactionsProvider combine streams.
6. UI reacts through Provider and renders updated cards and charts.

### Core Modules
- `providers/` state orchestration (REST, WS, cache mode, price, balance, tokens, domains)
- `services/` API clients (Kaspa REST, Kasplex KRC-20, KRC-721, KNS, price history)
- `models/` domain models (address, group, tokens, domains, transactions)
- `screens/` user flows (dashboard, add/edit address, settings, groups, donate)
- `wedgets/` reusable UI widgets (cards, charts, filters, QR, banners)
- `theme/` colors, fonts, and layout
- `localization/` EN/DE/RU strings and helpers

## Data Sources
All endpoints are centralized in `lib/config/app_globals.dart` and can be swapped for custom nodes.

- Kaspa REST nodes for balances and price (multiple nodes with fallback)
- Kaspa WebSocket node for live updates
- Kasplex API for KRC-20 (`https://api.kasplex.org/v1`)
- KRC-721 indexer (`https://mainnet.krc721.stream/api/v1`)
- KNS API (`https://api.knsdomains.org/mainnet/api/v1`)
- CoinGecko for price chart range data (`https://api.coingecko.com/api/v3`)

## Storage and Caching
- Hive for addresses, groups, settings, tokens, domains, and price history
- SharedPreferences for transaction history cache
- CacheModeProvider switches to cached data when the network or WS is unhealthy

## Project Structure

```
kaspa_observer/
|-- lib/
|   |-- config/          # global constants, endpoints, timeouts
|   |-- constant/        # enums and UI constants
|   |-- helpers/         # platform helpers (web vs io)
|   |-- localization/    # translations and localization helpers
|   |-- models/          # address, group, token, domain, tx models
|   |-- providers/       # state management (REST/WS/cache/etc)
|   |-- screens/         # main screens and flows
|   |-- services/        # API clients and storage services
|   |-- theme/           # colors, fonts, UI theme
|   |-- utils/           # small utilities and helpers
|   |-- wedgets/         # reusable UI widgets
|   |-- main.dart        # app entry point
|-- assets/
|-- android/ ios/ web/ linux/ macos/ windows/
|-- pubspec.yaml
```

## Getting Started

### Prerequisites
- Flutter 3.4+ (Dart >= 3.4)


## Configuration
Edit `lib/config/app_globals.dart` to adjust:
- Kaspa REST/WS endpoints and timeouts
- KRC-20/KRC-721/KNS API roots
- Balance history and chart settings
- Network health check parameters
- Debug panel and initial layout mode

## Localization and Themes
- Built-in EN/DE/RU localization via `flutter_localization`
- ThemeProvider persists and restores theme settings
- Compact and full layout modes for different screen sizes

## Security and Privacy
- No private keys, seed phrases, or signing
- Read-only, address-based monitoring
- All cached data is stored locally on the device

## Hackathon Submission
- Project name: Kaspa Observer
- Track: TBD
- Repo: https://github.com/karavanov/kaspa-observer-front
- Demo video: https://www.youtube.com/shorts/qR-7dPZchRc
- Team: Solo (end-to-end)
- Submission date: 2026-01-31

## Team
Built solo, end-to-end - from idea and product design to UI/UX, Flutter development, and real-time Kaspa blockchain integrations.

## License
TBD
