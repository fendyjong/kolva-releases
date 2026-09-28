# KolVa releases

Published builds of **KolVa** — the app you use, and the agent that connects your WhatsApp
number to it. Both are built automatically from the KolVa source repository and published here.

## 📥 [Installation guide](https://github.com/fendyjong/kolva-releases/blob/main/docs/installer-manual.md)

Step-by-step instructions for every platform — including the one-time security warning
Windows and macOS each show, and exactly what to click.

## Downloads

### 👉 [**Get the latest app release**](https://github.com/fendyjong/kolva-releases/releases/latest)

That link always resolves to the newest build — there is no version to remember, and nothing
here goes stale when a new one is published.

Agent releases are listed separately: [**all agent releases**](https://github.com/fendyjong/kolva-releases/releases?q=kolva-agent).

Releases come in two families, and you can tell them apart by the tag:

| tag | what it is |
|---|---|
| `kolva-app-v…` | **the KolVa app** — the thing you look at and click |
| `kolva-agent-v…` | **the KolVa agent** — runs quietly in the background and connects WhatsApp |

Most people want **both**: install the app on your computer or phone, and the agent on the
computer that will stay on.

### The app

| file | platform |
|---|---|
| `kolva-v<version>.exe` | Windows |
| `kolva-v<version>.deb` | Linux (Debian, Ubuntu and derivatives) |
| `kolva-v<version>.apk` | Android |

The app's filenames carry the version; `<version>` above is whatever the release you are on
says. Take the files from the release page rather than typing a name by hand.

### The agent

| file | platform |
|---|---|
| `kolva-agent-windows-v<version>.exe` | Windows |
| `kolva-agent-mac-v<version>` | macOS (Intel and Apple Silicon, one file) |
| `kolva-agent-linux-desktop-v<version>` | Linux with a desktop |
| `kolva-agent-linux-server-v<version>` | Linux server / headless |

**The agent's filenames carry the version too, just like the app's** — the only files that are
never versioned are `manifest.json` and `manifest.sig.json`.

🔑 **Each of these four files IS the installer.** There is nothing to unpack: you download one
file and run it. Running it with no arguments installs it. The same file is also what an
already-installed agent downloads when it updates itself — there is no separate "installer"
and "program".

## Verifying a release

Every agent release also carries `manifest.json` and `manifest.sig.json`. **These are not
downloads for you** — they are how an installed agent checks itself.

The manifest lists each file with its SHA-256, and the signature is Ed25519 over the exact
manifest bytes. An installed agent verifies that signature *before* it decides whether a newer
version exists, against a public key compiled into it. That ordering is deliberate: it means
nobody can serve an agent a stale version list to keep it from noticing an urgent update.

## Support

**This is the first KolVa release.** If something does not work, please tell support rather than
working around it — on a first release you may well be the first person to hit it, and that is
useful to know.

This repository holds build artifacts only. For help with KolVa, contact support through the
application.
