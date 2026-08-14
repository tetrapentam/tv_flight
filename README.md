# TV Flight

Football manager client. You need the **join link** from whoever is running the match server (or the same Wi‑Fi).

## Windows

Run `tv_flight.exe`.

## Mac

1. Use `tv_flight-macos` (universal: Apple Silicon + Intel).
2. First launch: **right-click → Open** (Gatekeeper), or in Terminal:
   ```bash
   chmod +x tv_flight-macos
   xattr -dr com.apple.quarantine tv_flight-macos
   ./tv_flight-macos
   ```

Backgrounds and match sounds are baked into the binary — you only need the exe (or `tv_flight-macos`).

## Same Wi‑Fi

1. Someone starts the match server (`serve-host --lan`)
2. Run Flight → leave **Join link** blank → enter your name → **Connect**

## Friends abroad

Your host sends a **JOIN LINK** (one line, usually `https://….trycloudflare.com`).

1. Run Flight
2. Paste the join link
3. Enter your name → **Connect** → claim a club → play

## If Connect fails

- Same Wi‑Fi: confirm `serve-host --lan` is running, or paste the LAN join link from the host console
- Abroad: confirm the join link is correct and the match server is still online
