<p align="center">
  <b>aurora-stealer</b>
</p>

<p align="center">
  <sub>mail · vpn · browsers</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>Aurora</code> &nbsp;·&nbsp; <code>aurora</code>
</p>

---

## About

Aurora stealer module map — mail clients, VPN configs, structured log export.

Named in quarterly infostealer roundups; slug matches report titles.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Browsers | Chromium + Gecko — cookies, logins, autofill |
| Apps | Discord, Steam, Telegram, VPN, FTP, mail |
| Crypto | Desktop wallets + browser extensions |
| Output | Panel-ready JSON/ZIP logs |


## Supported targets (lab reference)

Full grabber stack as shipped in typical **aurora-stealer**-class builds. Profile paths documented for SOC parsing exercises.

### Browsers
Chromium (Chrome, Edge, Brave, Opera, Vivaldi, Yandex, forks) and Gecko (Firefox, LibreWolf, Waterfox): cookies, logins, autofill, cards, history, bookmarks, extension list, OAuth tokens.

### Apps & crypto
Discord, Telegram, Steam, Epic, VPN configs, FTP clients, desktop wallets (Exodus, Electrum, Atomic, MetaMask / Phantom extensions), 2FA and password-manager paths.

### System
HWID, screenshot, clipboard, file grab masks, structured JSON/ZIP log bundle. Exfil stubs disabled in this lab build.


---

## Layout

```
aurora-stealer/
├── aurora-stealer.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore aurora-stealer.slnx
dotnet build aurora-stealer.slnx -c Release
dotnet test aurora-stealer.slnx -c Release
```

```bash
dotnet run --project src/App -- harvest
```

---

## CLI

| Command | Description |
|---------|-------------|
| `harvest` | Run local harvest simulation |
| `list` | List captured profile bundles |
| `export` | Export structured log dump |
| `status` | Module and pipeline status |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
security-research malware-analysis infostealer csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
