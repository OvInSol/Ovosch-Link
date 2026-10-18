<a href="https://github.com/user-attachments/assets/c8313d5b-01e8-4de7-9cfe-5277dd97f47f" target="_blank">
  <img 
    src="https://github.com/user-attachments/assets/c8313d5b-01e8-4de7-9cfe-5277dd97f47f" 
    alt="Интерфейс приложения" 
    width="700"
  />
</a>

# Ovosch Link

Ovosch Link is an Android VPN/proxy client built on [Xray-core](https://github.com/XTLS/Xray-core), with a native Kotlin + Jetpack Compose UI. It supports VLESS (with Reality), VMess, Trojan, Shadowsocks, and Hysteria2, and can run either as a full-device VPN or as a scoped local proxy.

## Download

Grab the latest APK from the [Releases](../../releases) page and install it directly — no Play Store required. You'll need "install from unknown sources" enabled for whichever app you download it through (browser, Telegram, etc.).

## Social media
The official Telegram channel of the project is https://OvoschLink.t.me.

## Features

- **Protocols:** VLESS+Reality, VMess, Trojan, Shadowsocks, Hysteria2
- **Two connection modes:**
  - **VPN mode** — routes all (or selected) device traffic through the tunnel
  - **Proxy mode** — a lighter, scoped alternative for split routing or when a full VPN isn't desired/allowed
- **Subscriptions** — import server lists from a subscription URL (HTTP/HTTPS), with auto-refresh on a configurable interval
- **Split tunneling** — exclude or include specific apps from the tunnel
- **Kill switch** — blocks network traffic if the tunnel drops, so nothing leaks to the raw connection
- **Smart routing** — route specific traffic classes (e.g. local/regional destinations) outside the tunnel automatically
- **Ad/tracker blocking** — via a bundled domain list, applied at the routing layer
- **Server health checks & failover** — pings the active server and can automatically switch to a working one
- **Fastest-server selection** — pings all servers in a subscription and picks the best one on demand
- **Quick Settings tile & home-screen widget** — connect/disconnect without opening the app
- **Localization** — Russian, English, and Esperanto

## Requirements

- Android 8.0 (API 26) or newer
- arm64-v8a or armeabi-v7a device (virtually all real phones; x86/x86_64 emulator builds are not distributed in releases)

## Building from source

**Note:** The repository is currently private. The build instructions are provided for internal use only.

```bash
git clone https://github.com/OvInSol/ovosch-link.git
cd ovosch-link
./gradlew assembleRelease
```

The unsigned build requires a signing config to produce an installable release APK — see `app/build.gradle.kts`'s `signingConfigs.release` block, which reads `RELEASE_STORE_FILE` / `RELEASE_STORE_PASSWORD` / `RELEASE_KEY_ALIAS` / `RELEASE_KEY_PASSWORD` from `gradle.properties` (not committed — see `.gitignore`).

## Status

This project is under active, pre-1.0-in-spirit development. Core functionality (all five protocols, VPN + proxy modes, kill switch, split tunneling, subscriptions) is implemented and tested on a real Xiaomi/MIUI device plus stock-Android testers. Expect rough edges; issues and feedback are welcome.

## Security

- Per-session random SOCKS5 credentials, never reused across connections
- `allowBackup="false"` — app data is excluded from Android's automatic backup
- Kill switch fails closed on tunnel loss (best-effort — see source comments in `OvoschVpnService.kt` for the documented edge case where a blocking TUN can't be established)
- No telemetry or analytics; no ads

This app is provided as-is for personal use. The source code is not publicly available. No independent security audit has been performed.

## License

Copyright © 2026 Alex (OvInSol). All rights reserved.

The source code of Ovosch Link is proprietary and is not licensed for use, modification, or redistribution by third parties. The compiled APK is made available for personal, non-commercial use as-is, without warranty of any kind.

This app uses [Xray-core](https://github.com/XTLS/Xray-core) via [AndroidLibXrayLite](https://github.com/2dust/AndroidLibXrayLite), both licensed under the [Mozilla Public License 2.0](https://www.mozilla.org/en-US/MPL/2.0/), as an unmodified third-party dependency.
