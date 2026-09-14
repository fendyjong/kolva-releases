# KolVa releases

Published builds of the **KolVa agent**. Each release is produced automatically from the
KolVa source repository and published here.

## Downloads

Go to [**Releases**](../../releases) and pick the latest.

| file | platform |
|---|---|
| `KolvaAgent-win.zip` | Windows — unzip, run `install.ps1` |
| `kolva-agent-linux-desktop.tar.gz` | Linux desktop — extract, run `install.sh` |
| `KolvaAgent-macos.zip` | macOS — unzip, run `install.sh` |
| `kolva-agent-linux-amd64` | Linux server — headless binary, no tray |

The bare binaries beside the archives are what an installed agent downloads when it updates
itself. For a first install, use the archive for your platform.

## Verifying a release

Every release carries `manifest.json` and `manifest.sig.json`. The manifest lists each
artifact with its size and SHA-256; the signature is Ed25519 over the exact manifest bytes.

An installed agent checks this automatically before applying an update, against a public key
compiled into the binary — so an agent will refuse an update it cannot verify.

## Support

This repository holds build artifacts only. For help with KolVa, contact support through the
application.
