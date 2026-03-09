# Tic Tac Trap

A strategic twist on tic-tac-toe where pieces come in three sizes and can stack on top of each other. Built as a native desktop app using [Tauri v2](https://v2.tauri.app/).

## How to Play

Each player has 6 pieces: 2 small, 2 medium, and 2 large. On your turn, you can:

- **Place** a piece from your hand onto an empty space
- **Stack** a larger piece on top of any smaller piece (yours or your opponent's)
- **Move** one of your visible board pieces to a different space

Get three of your pieces in a row to win — but only the top piece in each space counts.

**Watch out!** Moving a piece can reveal a hidden piece underneath. If that completes your opponent's row, *they* win — not you!

## Game Modes

- **vs Friend** — local two-player
- **vs Computer** — Easy, Medium, or Hard AI (Hard uses minimax with alpha-beta pruning)

## Prerequisites

- [Rust](https://www.rust-lang.org/tools/install) (via rustup)
- [Node.js](https://nodejs.org/) (LTS or later)
- **macOS:** Xcode or Xcode Command Line Tools
- **Windows:** Microsoft C++ Build Tools
- **Linux:** webkit2gtk, build-essential, and related packages ([see Tauri docs](https://v2.tauri.app/start/prerequisites/))

## Getting Started

```bash
# Install dependencies
npm install

# Run in development mode
npm run dev

# Build for production
npm run build
```

Production builds output to `src-tauri/target/release/bundle/`:
- **macOS:** `.app` bundle + `.dmg` installer
- **Windows:** `.exe` + `.msi` installer
- **Linux:** `.deb` + `.AppImage`

## Code Signing (macOS)

To distribute the app without Gatekeeper warnings, you need an [Apple Developer account](https://developer.apple.com/programs/) ($99/year):

1. Create a "Developer ID Application" certificate
2. Find your signing identity: `security find-identity -v -p codesigning`
3. Add it to `src-tauri/tauri.conf.json` under `bundle.macOS.signingIdentity`
4. Set notarization env vars before building:
   ```bash
   export APPLE_ID="you@email.com"
   export APPLE_PASSWORD="xxxx-xxxx-xxxx-xxxx"  # app-specific password
   export APPLE_TEAM_ID="XXXXXXXXXX"
   npm run build
   ```

Without signing, recipients can still run the app by right-clicking > Open on first launch.

## Project Structure

```
├── index.html          # The complete game (HTML + CSS + JS)
├── package.json        # npm scripts and Tauri CLI dependency
├── src-tauri/          # Tauri native app wrapper
│   ├── tauri.conf.json # App configuration
│   ├── Cargo.toml      # Rust dependencies
│   ├── src/            # Rust entry point
│   └── icons/          # App icons
└── dist/               # Build output (auto-generated)
```

## License

MIT
