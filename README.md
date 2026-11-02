<div align="center">

<img src="docs/icon.png" width="88" alt="FluxDM icon">

# FluxDM

[![Release](https://img.shields.io/github/v/release/MohammadFakih02/fluxdm-releases?label=download&color=4f8cff)](https://github.com/MohammadFakih02/fluxdm-releases/releases/latest)
![Windows 10/11](https://img.shields.io/badge/Windows-10%20%7C%2011-0078d4)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

</div>

A fast download manager for Windows: multi-connection downloads that survive pauses and reboots, videos from
YouTube and 1000+ sites, and a built-in BitTorrent client, all in one small exe with nothing else to install.

FluxDM 2 is a rewrite of the original .NET/WPF FluxDM in Rust + Tauri. It reads the same data folder
(`%APPDATA%\FluxDM`), so your download list, queues, settings and statistics carry straight over.

## Install

Download `FluxDM-Setup-<version>.exe` from the [latest release](https://github.com/MohammadFakih02/fluxdm-releases/releases/latest) and run it.
It installs for your Windows account only (no admin) and adds a Start Menu entry and the `.torrent` file association.
The setup has one page and one button: it closes FluxDM itself, and downloads that were running carry on afterwards.
FluxDM then updates itself: it looks for a new version every day and installs it once nothing is downloading and
its window is closed (Settings → Updates).
FluxDM updates itself from the same page (Settings → Updates).
The files aren't code-signed, so Windows SmartScreen may say "Windows protected your PC": click **More info → Run anyway**.

It runs on Windows 10/11. The only runtime it uses is Microsoft Edge WebView2, which comes with Windows 11 and
current Windows 10. If it's missing, the setup installs it.

## What it does

- **Files:** up to 64 connections per download. Each connection writes straight into the file, and the
  progress of every connection is saved, so a pause, crash or reboot resumes where it stopped.
  - When a connection finishes early, it steals half of the slowest one's remaining work.
  - Backup links (mirrors) are used in parallel. Each one is checked to serve the same bytes before it helps.
  - MD5 / SHA-1 / SHA-256 / SHA-512 verification; Hugging Face's published SHA-256 is picked up automatically.
  - Fresh links for expired downloads keep the bytes you already have.
- **Videos:** yt-dlp + ffmpeg, fetched once from their official releases on first use. Pick a quality up to
  4K, audio-only MP3/M4A, or whole playlists. Browser cookies can be used for age-restricted or members-only
  videos.
- **Torrents:** magnet links, .torrent links and files, using librqbit.
  - TCP + µTP, DHT, UPnP and fast resume.
  - Pick which files to download. Unticked files stay absent; shared boundary bytes are retained in a hidden part-file folder and restored if you select the files later.
  - Separate upload limits while downloading and while seeding (for all torrents, or per torrent in the Add window
    and the right-click menu), with a real *No upload*, a seed-ratio target and an optional seeding time limit.
  - When either seeding target is reached, stop sharing or remove the torrent while keeping its files.
  - Global extra trackers, filename exclusions (initially unticked files) and optional per-file `.!fx` unfinished markers for new torrents.
  - *Stop sharing* / *Resume sharing* on a finished torrent (right-click).
  - Force recheck/reannounce, move data, add trackers, export .torrent, copy the magnet link.
  - **Download in order** (right-click): fetches each file from its first piece to its last, so a video can be watched while it downloads.
  - Set location on an unfinished torrent moving to another drive offers to start over there instead of copying the full-size placeholder files.
- **Organising:** categories, tags, queues with a scheduler that can start and stop queues at set times on
  chosen days, catching up within the current window after a late start or sleep, including overnight windows.
  Queues can stay enabled when empty and retry failures with their own count and delay. Add remembers the last queue.
  Manual downloads run up to three at once by default, configurable in Settings > Downloads.
  When a queue finishes, FluxDM can exit, sleep, hibernate, shut down or restart, with a
  60-second countdown you can cancel. Finish actions are skipped while other downloads are active or waiting; failed batches report their failure count without running an action.
- **Main window:** icon filters, resizable download cards, saved sorting and optional grouping by date, status, type, site or queue (ungrouped by default), and details on the right. The list’s More menu keeps bulk actions, Columns and an optional table view. The footer shows free space and download/upload limits; its upload picker sets both torrent phases, with separate limits in Settings and each torrent?s Options tab.
- **Artwork:** Keyless Steam, Microsoft Store, PlayStation and GOG banners, with smaller Steam and web images as fallbacks. Programs and ISO images also try vendor, GitHub, referrer/host, Wikipedia, Snapcraft and Flathub artwork. Screenshots are subdued, and publisher/distro colours tint icon washes. Wide images retain their proportions when the window grows.
- **Storage and proxy:** optional unfinished folders for new HTTP/torrent downloads, regular-file collision choices, and None/System/HTTP/SOCKS5 proxies. SOCKS5 torrent TCP peers disable uTP; DHT/UDP remain direct.
- **Speed:** a global limit, per-queue and per-download limits, and a speed schedule with selected weekdays and overnight windows.
  Global and queue budgets share spare bandwidth fairly across download types;
  videos reconnect for changes over 30%, at most once a minute.
- **Catching downloads:**
  - Copying a download link opens the Add window.
  - Incoming links merge into Add forms with matching options; different contexts stay separate. POST downloads stay in the browser.
  - Drag links, `.txt` lists or `.torrent` files onto the window.
  - The browser extension and bookmarklets send downloads to FluxDM. The Firefox build is signed by Mozilla,
    so Settings → Browser extension installs it in one click. Chrome, Edge, Brave, Opera and Vivaldi load it
    unpacked (the button opens everything needed).
  - FluxDM can become the system's `magnet:` handler. If Windows still has another app (e.g. qBittorrent) set as the default, FluxDM opens Settings → Default apps for you to pick FluxDM for MAGNET.
- **Blank-window protection:** the app keeps WebView2 rendering, repaints a freshly shown window, and has a tray item *Reload window* if it ever looks blank.
- **Phone remote:** a PIN-protected web page on your home Wi-Fi with a QR code to pair. No app needed.
- **Updates:** Settings → Updates checks this repository's releases (any `owner/repo` can be set).

What's new in each version: [CHANGELOG.md](CHANGELOG.md). FluxDM downloads the new exe,
  verifies its SHA-256 and restarts into it.

## Command line

| | |
|---|---|
| `FluxDM.exe <url or magnet or .torrent path>` | opens the Add window (or hands it to the running copy) |
| `FluxDM.exe --tray` | starts hidden in the tray (used by *Start with Windows*) |
| `FluxDM.exe --exit` | asks the running copy to pause everything, save and quit |
| `FLUXDM_DATA=<folder>` | uses another data folder; such a copy runs beside the normal one (for testing) |

## Credits

[librqbit](https://github.com/ikatson/rqbit) (Apache-2.0), [yt-dlp](https://github.com/yt-dlp/yt-dlp)
(Unlicense, downloaded at runtime), [FFmpeg](https://ffmpeg.org) builds by gyan.dev (GPL, downloaded at
runtime), [Tauri](https://tauri.app) (MIT/Apache-2.0).

## License

[MIT](LICENSE) © 2026 Mohammad Fakih. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for what FluxDM uses and their licences.


Torrent settings include an optional watched .torrent folder, a weekly refreshed HTTP(S)/local PeerGuardian IP blocklist, and DHT, local discovery and IPv4-only controls. Networking defaults are unchanged; discovery/IP/blocklist changes require restart. See GUIDE.md for import and refresh behavior.
