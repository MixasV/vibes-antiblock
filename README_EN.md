# Vibes TCG Connector

🌐 [Русская версия](README.md)

A lightweight DPI-blocking bypass for the **Vibes TCG** card game. One button: launch — and play. Lobby, shop, events and cards load instantly.

**Author:** [🌐 mixas.pro](https://mixas.pro) · [✈️ Telegram: mixaseth.t.me](https://mixaseth.t.me)

> Want to watch YouTube, use Discord and visit other sites without a VPN too?
> Get the full [Zapret2](https://github.com/MixasV/zapret2-gui/tree/fix/graceful-exit-and-bridge-cooldowns) for free.

⭐ **If you find this useful — star the repository!** It's free support and the best way to say "thank you".

## How it works

Inside — the [winws](https://github.com/bol-van/zapret) (zapret) engine + the WinDivert driver. The app runs it with a single fixed strategy tuned for the Vibes TCG servers:

- **QUIC and TCP desync** for the game domains (`vibes.game`, lobby, API, assets)
- **IP-subnet desync** for the game servers and the CloudFront CDN (their traffic does not always carry a domain name, so it is matched by IP)
- **UDP any-protocol** on the game ports — covers the game's own protocol

The lists live in `bin/lists/` — editable with any text editor.

## Quick start

1. Download the release (or build it yourself — below)
2. Run `Запустить.bat` — it will request administrator rights (required by WinDivert)
3. Press «Подключиться» (Connect) — the game's lobby and shop will load

Closing the window fully exits the program — no background processes, no autostart. If the bypass ever "sticks" after closing — run `Остановить_обход.bat`, it stops everything for sure.

## Building from source

You need: [Node.js](https://nodejs.org), [Rust](https://rustup.rs), Visual Studio Build Tools.

```powershell
npm install
npm run build
cargo build --release
```

The resulting exe: `src-tauri\target\release\vibes-connector.exe`. Run `Запустить.bat` from the root — it locates the binary and the engine in `bin\` on its own.

## Structure

```
vibes/
  bin/                  engine (winws.exe, WinDivert) and domain lists
    lists/              domain and IP-subnet lists
  src/                  interface (React)
  src-tauri/            backend (Rust)
  Запустить.bat         launch with administrator rights
  Остановить_обход.bat  emergency bypass stop
```

## Disclaimer

Unofficial utility. **Not affiliated with the Vibes TCG developers.** The program does not modify the game — it only processes network packets. Use at your own risk.

## Third-party components

| Component | Project | License |
|---|---|---|
| `bin/winws.exe` | [zapret](https://github.com/bol-van/zapret) | [MIT](https://raw.githubusercontent.com/bol-van/zapret/master/docs/LICENSE.txt) |
| `bin/WinDivert.dll`, `bin/WinDivert64.sys` | [WinDivert](https://reqrypt.org/windivert.html) © basil | LGPL v3 / GPL v2 (your choice) |
| `bin/cygwin1.dll` | [Cygwin](https://cygwin.com/) | LGPL v3 |
