# Installing the KolVa agent

The agent connects your WhatsApp number to KolVa. It runs quietly in the background with a
small tray icon, starts automatically when you log in, and keeps itself up to date.

**Install once per computer.** Download the file for your system from
[Releases](../../releases), then follow the section below.

> **These builds are not code-signed.** Windows and macOS will each warn you once, the first
> time you run it. The steps below tell you exactly what you will see and what to click.
> Nothing is hidden — you can read every install script before running it; they are plain text
> inside the archive.

---

## Windows

**Download:** `KolvaAgent-win.zip`

1. Right-click the downloaded zip → **Extract All**.
2. Open the extracted folder. You will see `install.ps1`, `uninstall.ps1` and `kolva-agent.exe`.
3. Right-click **`install.ps1`** → **Run with PowerShell**.
4. **Windows will show a blue "Windows protected your PC" box.** Click **More info**, then
   **Run anyway**. This appears because the app is not code-signed; it appears once.

**What it does:** copies the agent into your local app data folder, saves its settings as your
user environment variables, and adds a startup entry so the tray starts when you log in.

**To remove it:** run `uninstall.ps1` the same way.

### If PowerShell refuses to run the script

Windows may block scripts by default. Open PowerShell and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\install.ps1
```

---

## macOS

**Download:** `KolvaAgent-macos.zip`

1. Double-click the zip to unpack it.
2. Open **Terminal**, and drag the unpacked folder into the window after typing `cd ` — then
   press Enter.
3. Run:

   ```bash
   ./install.sh
   ```

**You do not need to pass the binary** — it ships inside the archive beside the script.

**What it does:** removes the download quarantine flag and ad-hoc signs the app so Gatekeeper
does not block it, installs it under your Library folder, and registers a Login Item so it
starts when you log in and restarts if it ever stops.

**To remove it:** run `./uninstall.sh` from the same folder.

---

## Linux — desktop

For a machine with a normal desktop session. **If this is a server with no desktop, see the
next section.**

**Download:** `kolva-agent-linux-desktop.tar.gz`

```bash
tar -xzf kolva-agent-linux-desktop.tar.gz
cd kolva-agent-linux-desktop
./install.sh ./kolva-agent-linux-desktop
```

⚠️ **The binary path is required** — unlike macOS, this installer does not find it for you.
It is the file named `kolva-agent-linux-desktop` that came out of the archive.

**What it does:**

| goes to | what |
|---|---|
| `~/.local/bin/kolva-agent` | the program |
| `~/.config/kolva-agent` | its settings |
| `~/.local/share/kolva-agent` | its working data |
| `~/.config/autostart/` | the entry that starts it at login |

**To remove it:** `./uninstall.sh`

---

## Linux — server / headless

**Download:** `kolva-agent-linux-amd64`

⚠️ **There is no installer for this one yet.** The release ships the bare program only — no
install script and no service file. Running it by hand works, but it will not start
automatically after a reboot.

```bash
chmod +x kolva-agent-linux-amd64
./kolva-agent-linux-amd64
```

If you need this to run as a proper background service, contact support — the service
definition exists but is not yet part of the download.

---

## After installing

The agent needs to be linked to your KolVa organisation before it does anything. Open KolVa,
go to your WhatsApp settings, and follow the linking steps there. The agent finds the rest on
its own.

## Updating

**You do not need to do anything.** The agent checks for new versions and updates itself.

Each release is published with a signed manifest listing every file and its checksum. The
agent verifies that signature against a key built into it before applying an update, so it
will refuse anything it cannot verify.

## Troubleshooting

**The tray icon never appears (Linux).** The desktop installer needs a graphical session. On a
server, use the headless download instead.

**macOS says the app is damaged or from an unidentified developer.** Run `./install.sh` rather
than double-clicking the program — the installer clears the quarantine flag for you.

**Windows SmartScreen keeps appearing.** It should appear only once, on first run. If it
repeats, the file is probably being re-downloaded each time rather than run from where it was
installed.

**It was working and now it is not.** Restart the computer first — the agent starts at login
and that is the quickest way to get it back into a known state.
