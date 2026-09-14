# KolVa releases

Published builds of the **KolVa agent**. Each release is produced automatically from the
KolVa source repository and published here.

## 📥 [Installation guide](docs/installer-manual.md)

Step-by-step instructions for Windows, macOS and Linux — including the one-time security
warning Windows and macOS each show, and what to click.

## Downloads

Go to [**Releases**](../../releases) and pick the latest.

| file | platform | installer |
|---|---|---|
| `KolvaAgent-win.zip` | Windows | ✅ `install.ps1` inside |
| `KolvaAgent-macos.zip` | macOS | ✅ `install.sh` inside |
| `kolva-agent-linux-desktop.tar.gz` | Linux with a desktop | ✅ `install.sh` inside |
| `kolva-agent-linux-amd64` | Linux server / headless | ⚠️ none yet — bare program, run by hand |

The other bare binaries beside the archives are what an already-installed agent downloads when
it updates itself. **For a first install, use the archive for your platform.**

## Verifying a release

Every release carries `manifest.json` and `manifest.sig.json`. The manifest lists each
artifact with its size and SHA-256; the signature is Ed25519 over the exact manifest bytes.

An installed agent checks this automatically before applying an update, against a public key
compiled into the binary — so an agent will refuse an update it cannot verify.

## Support

This repository holds build artifacts only. For help with KolVa, contact support through the
application.
