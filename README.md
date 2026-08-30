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

### Option A — Registry (recommended, one-time setup)

Friends never re-paste a URL each session.

1. Host runs a small registry once (VPS or always-on PC):
   ```bash
   cargo run -p tv_cli -- serve-registry --port 8799
   ```
2. Each match session, host runs:
   ```bash
   cargo run -p tv_cli -- serve-host --remote --registry http://YOUR_VPS:8799
   ```
3. Friends put the same registry URL in **`registry.txt`** next to `tv_flight.exe` (uncomment/edit the line in the template file).
4. Friends leave **Join link** blank → name → **Connect**.

### Option B — Paste JOIN LINK (quick test)

1. Host: `serve-host --remote` → copy the **`https://….trycloudflare.com`** line from the console.
2. Friends: paste that link → name → **Connect**.

**Important:** each host restart mints a **new** URL. Send the fresh link every time, or use Option A.

Host also writes **`join_link.txt`** beside `tv_flight.exe` on the host PC — copy/send that file if not using a registry.

## Starting a match (everyone)

1. Stay on **Home** to see who is in the room.
2. **Claim a club** (click a chip — squad opens in the dossier).
3. Admin picks format + clubs → **Start** (or **Start auction**).
4. If the hub says **In progress** but no tactics board: everyone clicks **Next match**.
5. On the **Match** tab, both human managers press **Ready — kick off**, then wait for the **5s countdown**.

## If something is stuck

Check the hub phase (or ask the host):

| Phase | What to do |
|-------|------------|
| `lobby` | Admin: pick mode + clubs → **Start** |
| `between_fixtures` | **Everyone** → **Next match** |
| `prematch` | Both humans → **Ready — kick off** on Match tab |
| `in_fixture` | Open **Match** tab — pitch should animate |
| `auction` | Admin → **Finish auction**, then **Next match** |

## If Connect fails

- **Same Wi‑Fi:** confirm `serve-host --lan` is running, or paste the LAN join link from the host console.
- **Abroad (paste link):** confirm the link is from **this** session (not an old trycloudflare URL) and the host is still online.
- **Abroad (registry):** confirm `registry.txt` matches the host’s `--registry` URL and `serve-registry` is running.
- **Stale link in the field:** clear Join link and use `registry.txt`, or paste only the latest URL from the host console / `join_link.txt`.

## Two players on one PC (testing)

Only one Flight window can use port **8790**. For a second manager on the same machine:

```powershell
.\tv_flight.exe --port 8791
```

Use a **different name** in each window. Do not use two tabs in the same browser on the same port — they share one seat.

## After developers change Flight

From the ManagerX repo:

```powershell
cargo test -p tv_cli --test flight_contract
cargo test -p tv_cli --test flight_host_flow
cargo pack-flight
```

These guard squad dossier, prematch squad, match kickoff, and “New competition” restart.
