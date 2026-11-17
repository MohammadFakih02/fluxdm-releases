# Third-party notices

FluxDM's own code is MIT-licensed (see `LICENSE`). It includes or downloads these:

| Component | Where | License |
|---|---|---|
| [librqbit](https://github.com/ikatson/rqbit) 9.0.1 (`librqbit`, `librqbit-peer-protocol`, `librqbit-tracker-comms`), patched | `src-tauri/vendor/` (changes listed in `src-tauri/vendor/PATCHES.md`) | Apache-2.0, `src-tauri/vendor/LICENSE-APACHE` |
| [Tauri](https://tauri.app) and the other Rust crates | `src-tauri/Cargo.lock` | MIT and/or Apache-2.0 (each crate's own) |
| [yt-dlp](https://github.com/yt-dlp/yt-dlp) | downloaded on Windows; bundled as Python bytecode on Android | Unlicense; Android assets include YTDLP-LICENSE.txt |
| [FFmpeg](https://ffmpeg.org) | downloaded on Windows only; absent from Android | LGPL/GPL (depending on the Windows build) |
| [CPython](https://www.python.org) 3.14.10 Android distribution | Android APK native libraries and stdlib.zip | PSF License and bundled third-party notices in PYTHON-LICENSE.txt |
| [QuickJS](https://bellard.org/quickjs/) 2026-06-04 | Android APK libqjs.so, built from official sources | MIT; Android assets include QUICKJS-LICENSE.txt |
| OpenSSL 3.5.9 and SQLite in the CPython Android distribution | Android APK native libraries | Apache-2.0 (OPENSSL-LICENSE.txt) and public domain respectively; NATIVE-NOTICES.txt accompanies assets |
| yt-dlp-ejs, requests, urllib3, idna, charset-normalizer, websockets, certifi | Android deps.zip and reqs.zip | EJS: Unlicense; requests: Apache-2.0; urllib3 and charset-normalizer: MIT; idna and websockets: BSD; certifi: MPL-2.0. Upstream licenses retained in each archive's licenses/ entries |
| [Inter](https://github.com/rsms/inter) 4.001, variable UI font | `ui/fonts/Inter.woff2` | SIL Open Font License 1.1, `ui/fonts/Inter-OFL.txt`; Copyright 2016 The Inter Project Authors |
| [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono), variable, Latin subset, for numbers and paths | `ui/fonts/JetBrainsMono.woff2` | SIL Open Font License 1.1, `ui/fonts/JetBrainsMono-OFL.txt`; Copyright 2020 The JetBrains Mono Project Authors |

FluxDM is not affiliated with any of these projects.
