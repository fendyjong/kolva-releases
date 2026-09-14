# Installing KolVa

There are two pieces, and most people want both:

- **The KolVa app** — what you look at and click. Install it wherever you work.
- **The KolVa agent** — connects your WhatsApp number to KolVa. It runs quietly in the
  background with a small tray icon, starts when you log in, and keeps itself up to date.
  Install it **once**, on the computer that stays on.

# ⏳ There is nothing to download yet

**The first release has not been published.** These instructions describe what the downloads
**will** be. Until the first release appears there is nothing to install.

---

Download from the [**latest release**](../../releases/latest) — that link always resolves to the
newest build. Releases are tagged `kolva-ui-v…` for the app and `kolva-agent-v…` for the agent.

> **These builds are not code-signed.** Windows and macOS each warn you once, the first time
> you run something new. The steps below tell you exactly what you will see and what to click.

---

# The agent

**Every download below is a single file, and that file is the installer.** There is no archive
to unpack and no script to find. Download it, run it, done.

## Windows

**Download:** `kolva-agent.exe`

1. Double-click it.
2. **Windows shows a blue "Windows protected your PC" box.** Click **More info**, then
   **Run anyway**. This is because the build is not code-signed. It appears once.

Installs for your user only — no administrator password needed. It copies itself into your
local app data folder and adds a startup entry so the tray appears when you log in.

## macOS

**Download:** `kolva-agent-darwin` — one file for both Intel and Apple Silicon.

Double-click it.

If macOS refuses, open **Terminal**, `cd` to your Downloads folder and run:

```bash
chmod +x kolva-agent-darwin
./kolva-agent-darwin
```

Installs for your user only — no administrator password needed. It clears the download
quarantine flag and ad-hoc signs itself so Gatekeeper stops objecting, installs under your
Library folder, and registers a Login Item so it starts when you log in and restarts if it
ever stops.

## Linux — desktop

For a machine with a normal desktop session. **If this is a server with no desktop, see the
next section.**

**Download:** `kolva-agent-linux-desktop`

Double-click it, or from a terminal:

```bash
chmod +x kolva-agent-linux-desktop
./kolva-agent-linux-desktop
```

Installs for your user only — no `sudo` needed.

| goes to | what |
|---|---|
| `~/.local/bin/kolva-agent` | the program |
| `~/.config/kolva-agent` | its settings |
| `~/.local/share/kolva-agent` | its working data |
| `~/.config/autostart/` | the entry that starts it at login |
| `~/.config/kolva-agent/kolva-agent.env` | its saved settings file |

## Linux — server / headless

**Download:** `kolva-agent-linux-amd64`

🔑 **This is the only one that needs root**, because it installs a system service so the agent
survives a reboot:

```bash
chmod +x kolva-agent-linux-amd64
sudo ./kolva-agent-linux-amd64
```

## If you prefer to be explicit

Running the binary with no arguments installs it. You can also say so outright, which does
exactly the same thing:

```bash
./kolva-agent-darwin install
```

Both forms are supported. Use whichever you find clearer.

---

# The app

## Windows

**Download:** `KolVa-<version>-Setup.exe`

Double-click it and follow the installer. **Windows shows the same one-time "Windows protected
your PC" box** — **More info** → **Run anyway**.

## Linux

**Download:** `kolva_<version>_amd64.deb`

Open a terminal in your Downloads folder and run:

```bash
sudo apt install ./kolva_<version>_amd64.deb
```

This installs it properly — it lands in your applications menu, resolves its own dependencies,
and uninstalls cleanly with `sudo apt remove kolva`.

Double-clicking the file may also work, depending on which desktop you run and whether it has
a handler for `.deb` packages installed. The command above always works, so it is the one we
document.

## Android

**Download:** `KolVa-<version>.apk`

Open it on the phone. Android asks once for permission to install apps from this source;
allow it, then continue.

There is **no macOS or iOS build of the app.** The agent runs on macOS; the app does not yet.

---

# After installing

The agent needs to be linked to your KolVa organisation before it does anything. Open KolVa,
go to your WhatsApp settings, and follow the linking steps there. The agent finds the rest on
its own.

# Updating

**You do not need to do anything.** The agent checks for new versions and updates itself,
downloading the same file you would have downloaded by hand.

Each release carries a signed manifest listing every file and its checksum. The agent verifies
that signature — against a key built into it — *before* it decides whether a newer version
exists, so it will refuse anything it cannot verify, and nobody can quietly hide an update
from it.

# Removing it

## Windows, macOS and Linux with a desktop

Open the KolVa tray menu and choose **Uninstall KolVa**.

**It asks twice, on purpose.** The first click does not remove anything — the menu item changes
to read *"Click again to remove KolVa — unlinks WhatsApp and erases this computer's
enrollment"*, and the tray tooltip says the same. Click it a second time, shortly after, to go
ahead.

**To change your mind, do nothing.** The item goes back to normal on its own. Opening the
dashboard or restarting the computer also cancels it.

While it works the item reads *"Removing KolVa…"*. **When the tray icon disappears, it is
done** — that is how you know it finished. If something goes wrong the item says *"Uninstall did
not start — click to try again"*, and you can.

> **This cannot be undone.** Removing the agent unlinks WhatsApp and erases this computer's
> enrollment. To use KolVa on this computer again you will install and link it from scratch.

## Linux — server / headless

There is no tray on a server, so run:

```bash
sudo /etc/kolva-agent/uninstall.sh
```

## If the tray is not available

Each install also leaves an uninstaller on disk:

| platform | run this |
|---|---|
| macOS | `/Applications/Kolva Agent.app/Contents/Resources/uninstall.sh` |
| Linux desktop | `~/.config/kolva-agent/uninstall.sh` |
| Windows | `%LOCALAPPDATA%\KolvaAgent\uninstall.ps1` |
| Linux server | `sudo /etc/kolva-agent/uninstall.sh` |

**Use the tray item or one of these scripts — nothing else.** They stop the agent before
removing anything, and skipping that step can leave the agent running with its data already
gone.

# Troubleshooting

**The tray icon never appears (Linux).** The desktop download needs a graphical session. On a
server, use `kolva-agent-linux-amd64` instead.

**macOS says the app is damaged or from an unidentified developer.** Run the file from Terminal
as shown above — it clears the quarantine flag itself on the way in.

**Windows SmartScreen keeps appearing.** It should appear only once, on first run. If it
repeats, the file is probably being re-downloaded each time rather than run from where it was
installed.

**The agent is not running after a reboot (Linux server).** It needs the system service, which
only installs when you run it with `sudo`. Re-run it with `sudo`.

**It was working and now it is not.** Restart the computer first — the agent starts at login,
and that is the quickest way back to a known state.
