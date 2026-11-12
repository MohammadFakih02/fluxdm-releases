# Changelog

What changed for people using FluxDM. Developer notes are in `PROJECT_STATE.md`.

## 3.5.1 — 2026-11-12

- **Get the phone app with a QR code:** the PC's Devices window now has a "Get the Android app" card. Scan the code with your phone's camera and the matching Android app starts downloading. It also has a Copy link button. If the app is already on your phone you don't need it: the app updates itself.
- **The Android download is half the size:** about 15 MB instead of 30 MB. It takes the same space once installed.

## 3.5.0 — 2026-11-12

### A real phone app
- **FluxDM on Android has its own phone screens** instead of the PC window squeezed onto a phone: four tabs at the bottom (Downloads, Browse, Queues, Devices), a top bar on every screen and a + button to add a download.
- **Downloads:** tap a download to open its page (Open and Share when finished, Pause or Resume, connections with a Change button). Swipe right to pause or resume, left to delete (FluxDM asks first). Long-press to select several. Lists of thousands of downloads scroll smoothly.
- **Add screen:** a proper phone screen over wherever you were, with several links, file name, folder, queue, connections, speed limit and the file list for torrents. A shared link never pops the keyboard, and the Start button stays above it.
- **Queues tab:** each queue has its own page with its downloads in order, Start/Stop, a schedule (days, start and stop time), how many at once and a speed limit.
- **Settings** is a list of sections, one page each; every change applies at once.
- **Arabic** with a right-to-left layout (Settings > Appearance > Language: System / English / العربية). Sizes, speeds and file names stay left-to-right.
- **Tablets and landscape:** a side rail instead of the bottom bar, with the open download shown beside the list.
- TalkBack can read and open downloads.

### Downloading on Android
- **Queues can wait for the right moment:** Wi-Fi only, only while charging, or only above a battery level. A waiting queue says why ("Waiting for the charger") and carries on by itself.
- **Scheduled queues start on time** even when Android has closed FluxDM, and again after the phone restarts. If FluxDM can't open by itself, a notification asks you to tap it.
- **No more 6-hour limit:** Android 15 no longer stops long downloads after six hours a day.
- **A notification per download** with progress, speed, time left, Pause and Cancel, grouped under a summary with Pause all. Cancel asks "Remove this download and its unfinished data?" first. A Quick Settings tile pauses or resumes everything.
- The notification goes away when nothing is downloading; nothing runs in the background then.
- The global **Wi-Fi only** setting shows "Waiting for Wi-Fi" instead of silently pausing.
- **Browse tab** with FluxDM's own browser: downloads keep the site's sign-in, tabs and history, file uploads, fullscreen video, and Google sign-in works.
- **.torrent files and download links** tapped in a file manager, Telegram, Discord or mail open in FluxDM. A torrent's menu has Save .torrent file and Share .torrent.
- Finished and received files show up in Gallery and music apps, with an Open button.
- **FluxDM updates itself:** Settings > About > Check for updates (and at launch, at most every 12 hours) finds a new version, shows what's new, and downloads and checks the APK before Android's installer opens.
- Other apps and web pages can no longer control FluxDM's local download port.
- The Android download now comes with a SHA-256 checksum and a signature, like the PC setup, and the app checks it before installing an update.

### Your devices together (PC and phone)
- **Send files and whole folders** between paired devices, with progress, speed and time left on both screens and in an Android notification. Either side can cancel. A broken transfer continues where it stopped, and every file is checked with SHA-256 when it arrives.
- **Continue on another device now really continues:** a half-done download (a web download whose server allows resuming, or a torrent) moves with its finished parts, and the other device carries on from there. If the server's file changed, it starts over and says why. FluxDM asks before replacing anything.
- **Add by address:** when a device doesn't show up under Nearby (another subnet, a VPN, Tailscale), type its IP or name. It's remembered, and the list shows whether it's online.
- **Watching another device's downloads is live:** one connection stays open and only changes are sent, on the PC and the phone. Older FluxDM 3.4.0 devices still work the old way.
- **Receiving files is safer:** a paired device can't make FluxDM write outside the download folder or overwrite or delete a file that's already there.

### Fixes
- PC list: switching to Table view widens a narrow list column so you see the size and progress columns instead of a name and a cut-off number.
- PC Add window: in a narrow window the "Open .torrent…" button no longer squeezes its words into a tiny square, the "N links" chip counts only real links (a stray word on a line no longer inflates it), and a bad link is shown as a warning. The update dialog no longer shows an empty progress bar before you press Update. The status bar drops the long queue summary first so "1 running · 7.99 MB/s" is not cut off.
- PC window: the side rail no longer cuts "All downloads" down to "All do…" in a narrow window (it collapses to icons and remembers your width), the title bar no longer draws the name over the search box at 640 px, right-click menus taller than the window now sit fully inside it, and the details banner no longer clips its status text in a narrow window. Pause is greyed out for a download that is already paused, and a stopped torrent's Peers tab no longer says the same sentence twice.
- **Connections come back:** when the line struggled, FluxDM used fewer connections and kept the lower number until you paused and resumed. It now raises them again once the line is calm.
- Another device's list shows its pictures much sooner.
- Android: the home-screen icon fills its shape (no black ring).
- PC Settings → Torrents: the magnet-links text is no longer squeezed beside its button, and it now says when magnet links open in another FluxDM copy (with a "Use this copy" button). Settings cards no longer run off the window edge at narrow widths.

## 3.4.0 — 2026-11-10

### Added
- **Devices: your PCs and phone work together.** FluxDM finds your other PCs and your phone on the home network by itself. Pair two devices once like Bluetooth: both screens show the same 6 digits and you press Pair on both. After that, the Add window has a **Download on** choice (This device, your PC, your laptop, your phone): the link, file name, cookies and referrer go to that device, it starts the download in its own folder and shows "From Phone", and you see its real answer ("Downloading on Desktop: file.iso", or why it refused). Everything between paired devices is encrypted and checked against the key saved when they paired; a device that isn't paired can't send anything. Devices is in the side rail on a PC and at the top of the phone screen. On a PC, FluxDM offers once to let your devices through Windows Firewall (private networks only). The browser-based phone remote is hidden from Settings now (it still shows while it is switched on, so it can be turned off).
- **See and control your other devices' downloads.** Once devices are paired, a switch above the list (This phone | Desktop | Laptop) shows another device's downloads right in your list, live, with the same cards, game art, banners and totals as on that device. Pause, Resume, Retry, Pause all and the details pane work on that device; removing, moving and editing stay on the device itself, and FluxDM says so if you try. Right-click (long-press on the phone) a download and choose **Send to** to start the same download on a paired device. When a download finishes or fails, your other online devices get a notification ("On Desktop: finished"); a switch in Devices turns this off.
- **Devices keep finding each other on two networks.** A PC that is on Wi-Fi and on the phone's USB tethering at the same time now announces itself on both, and each device remembers which address really works and tries that one first (one that doesn't answer is tried last for a while). Before, the phone could keep trying the tether address that Windows Firewall blocks and say it couldn't reach the PC.
- **FluxDM for Android.** The same app on the phone, with the same look as on the PC: the same theme, colours, game art banners, cards, icons and fonts. Downloads (several connections per file), torrents and magnet links, queues and schedules, speed limits and speed rules, download health, smarter retries and Settings all work. The layout is made for touch: a tab bar at the bottom (All, Active, Finished, Queues, More), one card per download, a long press for the right-click menu, the details as a full-screen page with the same tabs, Settings one section per screen, and a round Add button. Share a link to FluxDM or tap a magnet link, and a notification keeps the downloads going in the background. Left out on Android, with the reason shown in Settings: the browser extension, video downloads (yt-dlp and ffmpeg are Windows programs), the tray, start with Windows, in-app updates (install the newer APK) and the phone remote.
- **Smarter retries.** FluxDM now tells failures apart. A refused or expired link (401, 403, 410, or a login page instead of the file) stops at once with "Link expired or refused ... use Refresh link" and keeps what was downloaded; a missing file (404), a full disk and a folder Windows will not let it write to also stop with exactly that reason instead of retrying. A server that is busy or rate-limiting (429, 503) is obeyed: FluxDM waits for the time in its Retry-After header (up to 10 minutes) and uses fewer connections. Timeouts and resets wait longer each time (with a little randomness) and also lower the connections after the second failure. When your internet drops, downloads wait for it to come back instead of using up their retries.
- **Retry failed downloads later** (Settings > Reliability, on by default). A download that failed for a reason that can pass (timeout, busy server, no internet) tries again by itself after 5 minutes, then 15, then 60, and then stays failed. It shows "Retrying at 14:05 (attempt 2 of 3)", and runs right away when the internet comes back. Refused links, missing files and full disks are never retried this way, and queue retries skip them too.
- **Stuck connections heal.** Inside one download, a connection that receives nothing for 15 seconds while the others keep going, or stays below a quarter of the others' speed for 20 seconds, is replaced: its part of the file continues on a fresh connection from exactly where it stopped, so no byte is lost or downloaded twice. Each part is left alone for a minute after a replacement.
- **Download health.** Every download in the list has a small dot (green running well, amber trouble, red failing, grey waiting) and hovering it gives the reason. The details pane has a new Health tab: connections (active, failed, replaced), retries with the reason and time, speed over the last minute, whether resume works and why, backup links and their state, when a signed link expires, the automatic retry plan, and for torrents the trackers working or failing, seeds, peers and availability. A new Health entry in the side list opens a page with every download that is stuck, failing, slow or waiting to retry, each with the reason in plain words and buttons for the usual fixes (Refresh link, Retry now, Add mirror, Open folder, Lower connections).
- **Speed schedule rules.** The speed schedule can now hold several rules, each with its own days, hours, download limit and torrent upload limit, for example slow downloads and no upload from 18:00 to 23:00 while gaming, and unlimited from 01:00 to 08:00. A rule can replace the normal limits (so it can lift them at night) or only lower them. Rules are checked from the top and the first match is used. Your existing schedule becomes the first rule automatically. A scheduled "No upload" only pauses sending; torrents keep sharing afterwards.
- A guided tour opens the first time you start FluxDM (also if you already use it, once). It walks through the real window step by step: adding downloads, the browser extension (install it and catch downloads, right-click links and videos), fast resumable downloads, torrents, videos, queues, the speed limit and schedule, the phone remote, notifications, looks and updates, and opens the matching Settings page for each. Back, Next and Skip move around, Skip tour (or Esc) ends it, and Settings > Updates > Show the tour again brings it back.
- Settings > Advanced has a new Save diagnostics button. It saves one zip you can send with a bug report: FluxDM and Windows versions, how many downloads are in each state, the error log, your settings and a short summary of the download list. PINs, passwords, cookies, links, file names and your Windows user name are removed first, and the window tells you exactly where the file went.

### Fixed
- The torrent engine is updated to librqbit 9.1.0, with all of FluxDM's changes kept. It brings upstream fixes: a rare freeze when changing which files of a torrent to download, writes past 2 GB, safer handling of broken peer messages and blocklists, socks5h:// proxies, and hybrid (v1 + v2) torrents with duplicate padding names.
- Right-click menus and drop-down lists no longer open out of sight when part of the FluxDM window is below the screen edge or under the taskbar: they fit in the part you can see, open upward when there's no room below, and scroll when they're taller than that.
- A window saved partly off-screen (for example taller than the screen, or dragged low) opens fully on screen again, shrunk to fit if needed.
- FluxDM no longer hangs at start without opening its window, the browser bridge or downloads (a lock-up added with the lower GPU use while hidden).
- The Android app shows the FluxDM icon on the home screen instead of a placeholder logo.
- Android: Back closes the open menu, sheet, Queues, Settings or dialog (inside Settings it goes back to the section list) instead of leaving the app.
- Android: Settings has a gear button at the top of the main screen, and More opens with big buttons (Settings, Stats, Select, Pause all, Clear finished, Health) above the lists and categories, so nothing is hidden below the edge.
- Android: more room for downloads: the desktop toolbar row is gone (actions are on each card and in More), and the count and sort share one slim line.
- Android: the Queues page lists a queue's downloads as compact cards with move and remove buttons in reach, and Settings pages are less crowded: one level of cards, the section's name in the back bar, and long explanations folded under "How it works".
- Android: the launch screen is dark, without the icon in a white box, and the icon follows the launcher's shape.
- Android: a download's details fit a small screen better: Resume, Open folder, Copy link and ⋯ share one row, the stats sit three across, and the folder and link take the full width under their labels.
- Android: the home-screen icon follows the icon colour chosen in Settings > Appearance (Full heat, Ice, Neon, Emerald, Mono). After a change some launchers drop the icon from the home screen; add it again from the app list.
- A pinned taskbar button, Start menu and desktop shortcuts now show the chosen icon colour (Settings > Appearance > App icon) instead of the original orange one. Changing the colour updates them right away and tells you how many it changed; the original colour puts them back. Existing pins are brought in line once at start, so the running window stays on the same taskbar button as its pin.
- The download health dot uses strong green, amber and red with a glow and is a little bigger, so it can be told apart from across the room.
- `error.log` no longer grows forever: past 1 MB it becomes `error.old.log` and a new one starts.
- Lower GPU use while FluxDM is hidden in the tray or minimized: hidden main, Add and notification windows stop painting and pause their visual refreshes; downloads continue in the background.
- A download list damaged by a power cut is no longer replaced by an empty one: if `downloads.json` (or settings) was cut off in the middle of a character, FluxDM started with an empty list and the next save overwrote the real one. It now loads the copy from the save before and keeps the damaged file aside.
- FluxDM uses much less CPU while idle: the hidden notification window kept redrawing at your monitor's refresh rate even with no notification on screen (about 12% of a CPU core and some GPU on a typical PC).
- Other devices entering wrong phone PINs can no longer lock your own phone out of the phone remote. After 50 wrong PINs the remote still pauses for 15 minutes, but only for devices that have never entered the right PIN; one device is still locked for five minutes after ten wrong tries.

### Security
- The Send and Grab bookmarklets only pass web and magnet links (no local file paths or other link types), and a page address can no longer add extra request headers. Other websites can no longer bring the FluxDM window to the front.
- Phone remote PINs must now be at least 6 digits. A shorter PIN from an older version is replaced with a new 6-digit one, so scan the pairing QR code again (Settings → Phone remote) once after updating.
- Updates are now signed. FluxDM only installs an update when its checksum carries a valid signature from the FluxDM release key and names exactly that version, so a tampered or swapped download is refused.
- Updates reject unsafe version names and download addresses outside GitHub's secure download hosts. Each setup is saved in its own newly created temporary folder.
- Backup links on another site, protocol or port no longer receive the original download's cookies or sign-in headers.

## 3.3.0 — 2026-11-03

### Changed
- **Settings pages are easier to read.** Torrents, Appearance, Downloads, Videos and audio, Browser integration, Speed schedule, Phone remote, Discord notifications and Advanced now look like the Browser extension page: a one-line summary, a few short bullet points, and the options grouped into cards with numbered steps where you have to do something outside FluxDM. Copy buttons for the bookmarklets say when they copied. Every option is still there, and Find a setting still finds each one.
- **A download whose link expired offers "Refresh link…" right in its header** (in place of Copy link), so the fix is one click away instead of inside the ⋯ menu or the Options tab.
- **Video errors explain themselves:** a quality the video doesn't come in, a removed or region-blocked video, "too many requests", a full drive, missing ffmpeg and an unreachable page each say what happened and what to do, instead of yt-dlp's raw message.
- **Torrent Peers tab:** while a torrent is running but no peers are connected yet it says "Connecting to peers…" / "No peers connected yet" instead of "Start the torrent", the Peers card shows the connected count while the live numbers load, and the small peer table fits its column instead of cutting off the upload speed. Piece counts use thousands separators everywhere.
- **"Backup links" everywhere:** the Mirrors tab and its "Add mirror…" button now use the same name as the Options tab, the Add window and the right-click menu. The right-click "Copy URL" is now "Copy link", like the button.
- **Queue editor:** the retry fields are number-sized like "At the same time", and the 60-second countdown note sits under "When it finishes" and only shows when a finish action is picked.
- **Phone remote:** a button press that fails says so instead of doing nothing, and when the PC can't be reached the page explains what to check and dims the stale list until it reconnects.
- Screen readers get names for the Add window's folder, file name, checksum and upload-limit boxes and for each file's checkbox in a torrent; the folder arrows in a torrent's file list are easier to hit.
- FluxDM saves its lists less often to disk while downloading: settings, queues and statistics are only rewritten when they actually changed (before, all four files were rewritten, flushed and backed up every five seconds).

### Fixed
- Messages that point to a setting now name the real page (Settings → Videos and audio, Settings → Behaviour) instead of pages that don't exist ("Video", "Videos", "General").
- Enter and Space on a focused button, tab or switch press that control again; before, they opened or paused the selected download instead.
- Queue members with an unknown size show "—" instead of "?".

## 3.2.0 — 2026-11-03

### Added
- **Pause all and Start/Stop queue sit on the toolbar:** Pause all is always visible (it was hidden in the More menu), and the queue button starts or stops the queue you're looking at, or the only queue; with several queues it opens a short list.
- Right-click menus work with the keyboard (arrows, Right/Left for submenus, Enter), and greyed-out items say why on hover ("Available once the download finishes").
- **Drop-down lists are FluxDM's own now instead of the plain Windows ones:** rounded, animated, the chosen value marked with an accent bar, and they open upwards when there's no room below. Arrow keys, Home/End, Enter, Esc and typing a letter work as before.
- **Any download can be moved to another folder:** Move… next to "Saving to" in the details, or right-click → Move to folder…. Before, only torrents could be moved, from a menu item at the bottom called "Set location". A finished file moves with it; an unfinished one takes its partial file along and carries on in the new folder. Videos can be moved once they finish.

### Changed
- **The download list does far less work while things download:** a moving download now updates its numbers in place instead of rebuilding its card (and re-creating its pictures) twice a second. With 300 downloads and 30 active, each update went from about 520 new page elements and 48 re-created pictures to 18 and none. Group headings are reused instead of rebuilt.
- While the window is hidden in the tray or minimized, FluxDM stops building list updates nobody sees (they held the list lock for every download twice a second). Showing the window catches up at once.
- Toolbar buttons that can't do anything for the selection (Pause on something already paused, anything with nothing selected) are disabled instead of silently doing nothing, and the count says "3 of 7 selected" when several are picked.
- **The details panel says something useful in every state:** several downloads selected, nothing selected, or an empty list. Empty Connections, Trackers, Files, Peers and Pieces tabs explain why (a video, not started yet, finished, waiting for the torrent's details) instead of showing a bare table.
- Banner titles stay readable over busy pictures (video thumbnails with their own headlines) thanks to a soft shade behind the text.
- **The footer stays on one line in narrow windows:** the paused/queued counts go first, then the limit labels give way to small ↓/↑ marks.
- **The sidebar fades at the edge when there are more categories to scroll to.**
- **Add window:** the video options (quality, playlist, part) sit with the form instead of inside Advanced, and checksum and backup links, which only apply to plain files, are hidden for videos and torrents rather than greyed out. A torrent's file list gets enough room to scan, and the name box explains itself when several links are added.
- **Settings:** options that only matter while a switch is on (speed schedule hours and limit, phone remote port and PIN) fade while it's off. The phone remote's PIN lockout text now mentions the global lockout too.
- **Statistics:** dates sit under their bar and the last one is no longer cut off; a faint line marks the busiest day with its amount, and today's bar stands out.
- Network failures read in plain words ("The site's address couldn't be found", "The server refused the connection", "The server closed the connection"…), and a file held by another program says so and can be resumed.
- **Short colour transitions** on buttons and cards and a sliding tab underline; all motion switches off with Windows' reduced-motion setting.
- Menus (right-click, presets, More) share the new look, and scrollbars are slim pills that stay faint until you hover the area and take the accent colour while dragged.
- **Patch notes in the update window show bold text, code and links properly** instead of raw `**` marks.
- Names that are only a code ("d83e47b5-63b8-…", "sha256-…") are no longer searched, so they don't hold up the art for other downloads.
- **Game lookups are faster:** the banner picture is fetched once instead of twice, and the square icon is searched alongside the banner.
- Known programs (7-Zip, Discord, VLC, Firefox, Chrome, Python, Blender…) are found under their real name, with their real logo. A screenshot or photo is never used as a program's icon any more; until the installer is downloaded such a program shows no picture, then the installer's own icon.
- **Pictures of downloads you removed long ago are cleaned out of FluxDM's data folder.**
- **The taskbar and tray icon fills its square and is centred, instead of sitting small and to the left.**

### Fixed
- The connection bar no longer draws eight identical fake segments when FluxDM has no per-connection data (videos, downloads that haven't started); it shows one honest bar. "Started" says "Not yet" instead of a dash, a size the server never sent reads "Size not known yet" instead of "of ?", and the "?" on failed cards is gone.
- **A finished download's Average speed is no longer blank.** It came from a speed log that only covers the last two minutes and isn't saved; it's now the size over the time data was actually moving. Downloads finished before this keep the blank card hidden instead.
- **"Started" in the details shows the date when it wasn't today.**
- **The Add window finds a game's icon and banner in a few seconds again.** It was waiting behind FluxDM's background art checks, and behind its own earlier searches for the link's code name.
- **Icons cut from a tall cover no longer slice through the game's title.** XCOM showed only the bottom half of its name; the frame now moves or zooms out to keep lettering whole. Icons made before are redone once.
- A download that gets its real name only after it starts (common with file hosts) is now looked up again under that name. Before, the search for the temporary name found nothing and the item stayed without art for a week.
- **Art you found by typing a name (Icon ▸ Find art) is kept after a restart instead of being thrown away.**
- **Logos are no longer cropped like photos.** Ubuntu's icon was "ub" beside half its symbol; a logo now gives its symbol, shown whole. A see-through wordmark is no longer used as a banner.
- **Old YouTube thumbnails lose the black bars above and below the picture.**
- **The banner above the details no longer shifts a moment after it appears.**
- **A video's burnt-in thumbnail headline no longer competes with the title in the download list.**
- **Your downloads list survives a power cut or a hard reset in the middle of a save:** FluxDM writes the file to disk completely before replacing the old one, and falls back to the copy from the save before if the file is damaged.
- Finishing a download whose unfinished file is on another drive no longer freezes the window while it's copied, and a file briefly held by an antivirus no longer makes the last step fail.
- The phone remote's PIN can no longer be read by a website through a trick called DNS rebinding, and too many wrong PINs from any devices pause the remote for 15 minutes.
- **Settings:** the descriptions beside "Look", "App icon", "Glass" and the art options were shifted by one row, and so were the descriptions and icons of the pages from "Discord notifications" down. Each is in its place again.
- **The Add window's art panel is lower, so "Advanced" no longer slides under the buttons.**

## 3.1.2 — 2026-11-02

- The timer line along the bottom of a notification runs smoothly instead of in small jumps.
- Video thumbnails fill the whole banner again, as they did in 3.1.0, instead of sitting in a box on the right.
- A YouTube video's icon is now its channel's picture rather than a thumbnail squeezed into a square. Videos already in the list get it too.
- FluxDM's own logo in its messages ("FluxDM is still running", updates) no longer sits on a grey square.

## 3.1.1 — 2026-11-02

- Games, programs and updates with release words in their names get their icon and banner again. Names like "XCOM Enemy Unknown The Complete Edition MULTi9-ElAmigos", "Absolum Update Build r35192-RUNE", "Cloudflare_WARP_2026.8.2110.0" or "RobloxPlayerInstaller" are now searched without the version, "Setup", "Update Build", "MULTi9" and "22H2", and with joined words split. Before, nothing matched, and the item wasn't tried again for a week. "Alan-Wake-2-SteamRIP.com" no longer loses its whole name.
- A new download's icon and banner arrive in seconds again. After FluxDM's art rules change, every saved item is checked once more, and a new download used to wait behind all of those checks. It now goes first. A first lookup that failed on the network is tried again after a minute instead of ten.
- A new setup, in one window: it says whether it will install, update, reinstall or go back a version, and has one button. It closes FluxDM itself (no "file in use" box), and downloads that were running carry on afterwards. You can choose the folder on a first install. The uninstaller says what it removes, gives magnet links back to the app that had them (with its icon), removes start with Windows and FluxDM's Default apps entry, and has a box to also delete your downloads list and settings (downloaded files always stay).
- Updates: FluxDM looks for a new version every day, not only when it starts. With "Install updates by themselves" on (Settings → Updates, on by default), an update goes in once nothing is downloading and the window is closed. FluxDM starts again in the tray, and says once that it was updated. Updating from the window also starts the new version straight away, wherever FluxDM is installed.
- Films and shows downloaded under release names such as "Superman 2025 1080p WEB DL HEVC x265" get their poster and banner again. The search now uses only the title before the year and release tags, and prefers the film from that year.
- YouTube and other video thumbnails are shown whole: on the right of the details banner and the list card (over a blurred copy), and letterboxed in the icon, instead of cropped so the burnt-in text was cut off.
- The User-Agent FluxDM sends to sites now carries the app's real version (for example FluxDM/3.1.0, not the old FluxDM/1.0 or 2.0 saved by earlier versions). One you typed yourself is kept.
- The sidebar opens expanded on a new install, just wide enough for its labels; a copy that only had the old collapsed default opens expanded once. Double-clicking its edge toggles between collapsed and that width.
- The download speed shown is right within a second of starting. It used to begin from the first reading, taken while the connections were still opening, and creep up for 10–30 seconds, so a download looked stuck at a few KB/s while it was already running at full speed (a small file could finish before the number caught up). It is now the average over the last 3 seconds.
- With a download, queue or scheduled speed limit on, a download that starts now gets the whole limit straight away instead of climbing from a crawl for half a minute, and the speed no longer dips and recovers under the limit whenever the server has a slow moment. Several downloads still share the limit fairly.
- A Discord button next to the list's actions turns Discord notifications on and off. It glows while they're on and is dim when they're off. With no webhook link yet, or a link Discord refused (a red dot), clicking it opens Settings at the Discord section.
- Queues: each download in the list has up and down arrows to change the order (dragging still works).
- Queues: the Name column can be resized like the others; a wide Name column scrolls the list sideways while the arrows and remove button stay in view.
- Settings → Discord notifications explains how to get the webhook link in numbered steps, with Discord's own names (Edit Channel, Integrations, Webhooks, Copy Webhook URL).

## 3.1.0 — 2026-11-02

### Look and layout
- Download cards are easier to read: a larger title, one status per card (no "Paused" pill plus "Paused at 86%"), no second line repeating the file name (it shows on hover and in the details), and finished downloads drop their full progress bar and "Done" pill. Cards have a visible edge so they no longer run together.
- Empty labels such as "Seeds: Peers: Ratio:" no longer appear on downloads that aren't torrents.
- The details header shows the site and one line of state under the percentage; the Resumable, category and queue chips are gone (the queue still shows while a download waits in one). A finished download shows when it finished instead of "100%".
- The details no longer repeat the progress: the "File map" under the speed graph and the "Downloaded" card are gone, and the checksum line only appears when a checksum is set. A paused or finished download shows its average speed and start time instead of empty speed, time-left and connection cards; Retries shows only when something was retried.
- One Queues button replaces Scheduler and Queues in the sidebar; it opens the queues and schedules window. Opening a queue now shows its Start/Stop controls in a bar above its downloads instead of a floating card that stayed on screen. Queues get their own sidebar section once there is more than one; tags always show there.
- The sidebar starts open (with labels) on a new install.
- The Queues window is simpler: the queue's name with one Start/Stop button at the top, then the downloads in it, then when it starts. "Start" is one choice (only when you press Start, when FluxDM opens, or at a set time), and "Repeat" is one choice (every day, weekdays, weekends, pick days, once on a date) instead of checkboxes plus shortcut buttons. Retries and what happens when the queue finishes sit under "More options". The main window's queue bar and a queue's right-click menu have one Start/Stop and "Edit…".
- A queue's downloads are a table with resizable #, Size and Status columns; long names wrap instead of being cut, and the list is no longer squeezed to a few rows. Reorder by dragging (or Alt+↑/↓), take one out with its ×, or Clear them all; the downloads always stay in your list.
- Long names (a hash, a release name without spaces) no longer make the details title jump as the numbers next to it change: the title is smaller for long names and stops at two lines (the full name shows on hover).
- Column widths you drag in the Files, Peers and Trackers tabs are saved again.
- App icons (a program's own icon, Windows file icons such as WinRAR's) show whole and centred instead of being cropped to fill a frame, and Windows file icons are taken at full size, so they are sharp in the details header. Store icons, covers and video thumbnails still fill their frame.

### Artwork
- Scene-style names such as "Control.Resonant.v.1.4.2.REPACK-VHSTaPE" are cleaned properly ("Control Resonant"), and a name with a leftover tag is retried shorter, accepting only an exact store name.
- Dark store banners are no longer thrown away: official Steam, PlayStation and GOG banners are never cropped as if their dark areas were empty borders (Bloodborne had no banner because of this).
- Every banner source is tried in order until one fits, instead of stopping at the first picture that turned out too small. Steam's large art is also found for newer games, whose pictures live at addresses the old lookup didn't try.
- "God of War III" no longer matches "God of War": sequel numbers written as Roman numerals count.
- Downloads from GitHub no longer get GitHub's generated card or GitHub's own home-page picture as their banner. Organisations' logos are used as icons, release files that aren't games still get their repository's art, and a file named only for its platform ("windows-x64.zip") is titled with the repository's name. File-hosting sites' home-page pictures are never used.
- GitHub repositories without their own preview picture fall back to their README: its first wide picture becomes the banner and its logo the icon (status badges are skipped). Source-code zips of a repository count as coming from it.
- All saved downloads are checked once more with these rules.

### Downloads and updates
- FluxDM now downloads and updates from its new public home, [fluxdm-releases](https://github.com/MohammadFakih02/fluxdm-releases). The source code moves to a private repository. Copies that still point at the old update source are switched over by themselves; copies older than this version update one last time from the old place.
- Releases carry only the setup (no portable FluxDM.exe).

### GitHub
- Pasting a GitHub repository link (github.com/owner/repo, or its Releases page) downloads the latest release's Windows file instead of the web page: an installer first, then a 64-bit .exe or .zip; Linux, macOS, ARM and checksum files are skipped. A release without a Windows file gives its source code zip; a repository without releases says so. The phone remote does the same.

### Videos
- A video's title and thumbnail appear as soon as it is added (YouTube answers instantly; other sites once yt-dlp is installed), instead of "Video from youtube.com" with no picture until it finished.
- The first video download on a new PC shows the yt-dlp/ffmpeg install progress on its card instead of a silent "Connecting". An ffmpeg already installed on the PC is used instead of downloading another, and if gyan.dev doesn't answer, ffmpeg comes from yt-dlp's own builds on GitHub.

## 3.0.2 — 2026-10-31

### Updates
- Updates install from the setup now: FluxDM downloads it, checks its SHA-256, installs it quietly and restarts. Releases from 3.0.3 on carry only the setup (no portable FluxDM.exe); this release still has it so older copies can update.
- Settings → Updates installs the update right there, with a progress bar; no need to go back to the main window.
## 3.0.1 — 2026-10-31

### Appearance
- "Choose your look" on first start: five complete looks (Full heat, Midnight, Neon, Forest, Mono), each shown as a small preview of the window and applied live while you pick. It can be opened again from Settings → Appearance.
- New option: keep the same look for every download, so the window's colours and background art no longer change when you select a download.

### Fixed
- The empty part of the title bar right of the search box now drags the window, and a double-click maximizes it.
- After an update, Windows refreshes its icon cache once, so a pinned taskbar button or an old shortcut shows the new icon instead of the old one.
- Banners no longer differ from one PC to another when one store answers slowly: Microsoft Store hero pictures (which leave a wide empty area for store text) are only used when no PlayStation, GOG or Steam picture exists. Banners are re-checked once.
## 3.0.0 — 2026-10-31

### Appearance
- Five app icon themes: Full heat (the original), Ice, Neon, Emerald and Mono, shown as icon previews. They change the tray icon, the taskbar/window icons and the logo inside the app, keeping the original artwork's light and shade. Colour swatches show a smooth ring when chosen.
- Selected download art strength (25-400%) and blur for the highlighted card in the list (applied to game banners too). The card's text follows the art behind it: a soft shadow on medium art, dark text with a light halo on bright art, so it stays readable at any strength.
- The column headers of the details tables (connections, peers, files…) are soft glass with rounded ends instead of a hard black strip.
- Header banner strength (25-150%) and blur for the big picture above the details.
- Background art strength (25-500%) and blur (Automatic, None to Very strong), so more of the game art can show behind the window.
- The Theme choice under Behaviour was removed: it had no effect (the app is always dark; Appearance sets its look).

### Artwork
- Every banner, from every source, is checked before it's used: blank padding is cropped off (e.g. a square cover on a white share image), and pictures that aren't wide and big enough are turned down, so the header shows the blurred icon or cover instead of a boxed, square or tiny picture. Existing items are re-checked once.
- Game icons come first from the PlayStation store (512 px square icons) and the Microsoft Store (square box art); only without those is the source's own icon used, and tiny ones (e.g. Steam's 32 px) are replaced by the sharper cover art. Wide or tall pictures used as icons are framed around their detail (the title and faces) instead of the plain middle; when that's wider than a square, the icon zooms out to show all of it over a blurred copy of the picture.
- In Add download, a pasted link shows from its start, and a long link no longer runs under the link icon.
- More free sources with proper wide pictures: Cinemeta backdrops for films and series, TVmaze backgrounds for series, AniList and Kitsu for anime, then Wikipedia and iTunes as fallbacks.
- Soundtracks, demos, artbooks and similar side releases are no longer taken as the art for a game. Console tags glued to other words (DLCs_PS5) now mark a download as a game.
- Right-click → Banner → Choose banner image… uses any picture from your PC (blank borders are cropped); "Find a banner automatically again" undoes it. A chosen banner is kept through automatic lookups.

### Fixed (torrents)
- If the saved DHT port is in use by another program (or a second FluxDM using a copy of the data folder), DHT starts again on a free port instead of every torrent failing; if that fails too, torrents run on trackers alone with a notice.
- Long error messages in the details header are cut to two lines; hover shows the whole text.
- Pausing a torrent works at once, even while the engine is starting or the torrent is still checking its files (it used to wait without limit).
### Discord notifications
- Settings → Discord notifications: paste a channel webhook link and choose any of five messages: a download finished, a download failed, a queue finished, the disk is almost full (a free-space level you set, at most one message per drive per hour) and a daily summary at a time you set (skipped when nothing happened). All are off by default. "Send test message" says exactly what happened. Messages are sent in the background and wait out Discord's rate limit; a failure never slows a download.

### Videos and audio
- New qualities: Smallest file, Opus and FLAC audio, and a custom yt-dlp format (Settings → Videos and audio).
- Subtitles can be downloaded as files or put inside the video, in the languages you choose (default English and Arabic), optionally with auto-generated captions.
- The thumbnail, title/artist details and chapters are added inside the file (can be turned off).
- SponsorBlock for YouTube: mark sponsor segments as chapters, or cut them out.
- A cookies.txt file can be used instead of browser cookies.
- The Add window lists a playlist's videos so you can tick which ones to download (All, None, or a range such as 1-10,15).
- Download only part of a video: type start-end (e.g. 1:30-2:45) in the Add window.
- Live streams: the Add window says when a link is live or scheduled; options to record from the start and to wait for a scheduled stream. The list shows "waiting for the stream to start", "live - recording" and "finishing the file".
- Optional "Don't download the same video twice" remembers downloaded videos; the Add window also warns when the same video is already in the list.

### Fixed (videos and links)
- The app icon has a small margin like other Windows icons and the F sits in the middle, at every size (the tray and taskbar use the largest one).
- Selecting another download no longer makes the window, the banner or the list blink: pictures are decoded before they're swapped in, measured banner sizes are reused, and known art colours apply in the same frame, new art keeps the current look until it is ready, and cards aren't rebuilt on selection.
- Dark banners (night scenes, horror games) and pictures that can't be measured now show behind the window instead of staying near-black.
- yt-dlp and ffmpeg now stop with FluxDM even when FluxDM crashes or is ended from Task Manager, instead of carrying on in the background.
- Videos with Arabic, emoji or other non-Latin titles or folders finish and appear in the list correctly, even when yt-dlp reports the path in a different encoding.
- Reading a video page no longer fails when yt-dlp prints a notice next to its answer.
- yt-dlp and ffmpeg are checked against their published checksums before they are installed, and yt-dlp must start successfully; otherwise nothing is installed and the reason is shown.
- Pasted links lose invisible characters, wrapping quotes and brackets; several links on one line are all added.
### Torrent settings
- Added an optional watched folder: stable .torrent files use the default torrent destination/category, retain cached metadata and move into an added subfolder. Invalid files remain in place with a warning; duplicate torrents are not added twice.
- Added an optional PeerGuardian IP blocklist from an HTTP(S) URL or local file, with gzip support and weekly refreshes. Failed or empty refreshes retain the last good ranges for new peer connections; initial load failures report an engine error.
- Added saved DHT, local peer discovery and IPv4-only switches. Defaults preserve existing networking; changes to these switches and the blocklist apply after restart.
- Added an optional seeding time limit in minutes, alongside the ratio target, with Stop sharing or Remove torrent (keep files). Sharing time survives restarts and excludes paused/checking time and long suspend gaps.
- New torrents and magnets can receive a saved global tracker list. Add previews and deferred/bulk additions untick configurable filename patterns, with manual file choices taking priority.
- New torrents can mark unfinished files with .!fx and remove the marker as each file completes. Saved paths survive pause, restart and moves; filename filters use original names. Conflicting marker names are rejected, and publication never replaces another file.

### Download settings
- Added None/System/HTTP/SOCKS5 proxies, optional masked login and local-address bypass for downloads, metadata and covers. SOCKS5 supports torrent TCP peers with uTP disabled; Settings explains direct DHT/UDP traffic and restart requirements.
- Regular file collisions can Ask, Add a number (default), Overwrite or Skip, preserving existing files and partial data until a choice is made.
- New HTTP and torrent downloads can use an optional unfinished folder, with saved staging paths and completion moves to their final destination.
- Speed schedules now select weekdays, including overnight windows anchored to their starting day.

### Fixed (download storage and queue safety)
- Torrent filenames now use shared Windows-safe paths for storage, Files, missing-file checks, moves and deletion. Invalid characters, reserved names, trailing dots/spaces and oversized components are sanitized; names that clash after cleaning (or differ only in upper/lower case) get " (2)", " (3)"… instead of the torrent being rejected.
- HTTP and torrent disk-full write errors pause with free-space guidance and retain partial data without automatic queue retries. HTTP paused rows now show their reason.
- Force rechecks run one at a time across torrents, support cancellation while waiting or checking, report engine failures and time out after 30 minutes. A cancelled or timed-out check retains its slot until hashing stops.
- Queue finish actions skip other active or waiting downloads and check again when the countdown ends. Failed batches report their failure count once without running an action.
- Editing a future queue start re-arms today without replaying yesterday's slot. Renaming preserves the shared speed limiter and rejects duplicate names; invalid saves leave the name unchanged.

### Scheduler and queue controls
- Scheduler now groups Name, When, Limits, finish actions and Items in order, with a plain schedule summary, weekday/weekend shortcuts, one-off dates and next-start countdowns beside queue status and counts.
- Queue items support move up/down/top/bottom, drag reordering, removal and confirmed clearing while keeping downloads and files. Live Start/Stop controls refresh without replacing edits; failed saves recover the saved form.
- Scheduled queues catch up during their current time window, including overnight and one-off schedules. Local-date guards prevent repeated starts during clock changes; a missed stop is honoured after sleep.
- Queues can stay enabled when empty and automatically start later additions. Completion notifications fire once per batch, and repeated Start requests preserve the current batch.
- Each queue has its own retry count and delay, off for new queues. Existing saved retry preferences carry over.
- Manual downloads share a configurable concurrency limit, defaulting to three across HTTP, video and torrents. Waiting downloads can be paused.
- Add remembers the last chosen queue, including None, while explicit incoming queue choices take priority. Remembered choices follow queue renames and clear when a queue is deleted.

### Fixed (torrent pause and missing files)
- Pause, Resume, Force recheck and location changes run one operation at a time per torrent. Resume requests made during another operation show a retry note; pausing interrupts magnet resolution and disk checks, including checks waiting for a slot.
- Pause waits for the previous transfer tasks to release their sockets and callbacks before resuming. Disk checking shows Checking progress and offers Pause, while cancelled resolution returns to Paused without stale Connecting text.
- Starting a saved torrent with missing or truncated wanted files preserves its progress and asks for Force recheck. Remembered engine torrents no longer open or recreate missing files before this check; unticked files do not block resuming.

### Fixed (torrent file selection)
- Unticked torrent files are no longer created for shared boundary pieces. Their bytes stay in a sparse file under `.fluxdm.parts`, which also supplies uploads of those pieces. Selecting a file later restores its retained bytes; existing files moved out of the selection keep their data there.
- Rechecks, restarts and location changes retain boundary data. Removing a torrent deletes its own part-file, including with Keep files, without affecting other torrents sharing the folder.

### Fixed (torrent checks and resume data)
- Force reannounce asks trackers and peer discovery immediately without pausing, replacing the torrent or checking files again. Paused torrents show Start it first.
- Initial checks skip pieces belonging only to unticked files and count selected boundary pieces in checking progress, reading retained bytes from part-file storage.
- Pausing, finishing and exiting save resume data, including small transfers; downloads also save every minute. Unchanged moves and tracker additions retain verified progress, while Force recheck still checks the whole selection. Failed resume hashes trigger a fresh check, and a pause during checking stays paused.

### Fixed (HTTP progress)
- Changed files, lost resume support and expired links pause with a clear explanation while keeping partial data. Only Restart from zero discards existing progress.
- HTML login and expiry pages are rejected before writing file downloads, including mirrors and single-connection transfers; intentional HTML downloads remain supported.
- Ignored byte ranges retry with backoff and fall back to one connection only before any bytes are downloaded. Servers that close ranged probes are retried without Range.

### Fixed (art fit)
- "Start with Windows" stays on after an update or reinstall: FluxDM restores its startup entry when the setting was on, and recognises its own exe however the path is spelled (short 8.3 names, different case).
- Notifications: app messages such as "FluxDM is still running" show the FluxDM icon instead of a success check, have no second frame around the card, and hovering freezes the timer bar where it is instead of restarting it. Problems (port in use, firewall, a video that couldn't be removed) show an amber warning; failed downloads show a warning sign unless they are retrying a lost connection.
- Large banners fill the header and list card cropped around the picture's subject, with a soft fade instead of a hard edge; wide windows no longer zoom in.

### Added
- New app icon: a leaning gold F with speed trails on a graphite tile that glows hot where it is heading. Drawn separately for each size, so the taskbar, tray and title bar icons stay sharp.
- While "Start with Windows" is off, FluxDM asks once every two weeks whether to turn it on ("Not now" waits another two weeks; turning it off in Settings also resets the wait).
- Seamless title bar like Windows 11 Settings in the main and Add windows: the app's own background runs to the top, search sits in the middle of the bar, and the window buttons keep snap layouts (tauri-plugin-decorum).
- Torrent Files tab is a folder tree: a top row for the whole torrent and collapsible folders with combined size, progress, priority ("Mixed" when they differ) and remaining; checking or setting a folder applies to everything in it. Files and Trackers use the full width of the details pane.
- Game artwork is keyless: Steam library heroes, Microsoft Store SuperHeroArt, PlayStation key art by ID or exact name, GOG wide covers, then smaller Steam and web images.
- Programs and ISO images can use Store heroes, vendor share images, GitHub repository art and referrer/host images, with Wikipedia, Snapcraft and Flathub as fallbacks. Screenshots stay dim; publisher and distro colours tint icon washes.
- Optional list grouping by date added, status, type/category, site or queue, saved alongside sorting; existing and new lists start ungrouped.
- Torrent Options has separate per-download pickers for download, upload while downloading and seeding. Item menus collect their presets under Bandwidth limit.
- The navigation rail can be dragged wider to show labels and counts, remembers its width, and toggles between icons and labels when its edge is double-clicked.
- Redesigned Add window with verified Steam artwork, type banners, file selection and priorities, destination free-space feedback, queue and speed controls, and a persistent action footer. Advanced keeps video quality, playlists, checksums, mirrors and request headers available.
- Redesigned notifications with completion artwork and metadata, Open and Show in folder, retry and pause actions, torrent sharing controls, and queue countdown actions synchronized with the existing confirmation dialog. Notification ordering, hover holds and click-to-reveal remain available.
- Settings now has searchable section pages, an icon rail and live Appearance controls for backgrounds, artwork accents, glass, line glow and game art. Cancel restores the preview; unsaved edits ask before being discarded.
- Details banners show game artwork or type colours, progress reveal with adjustable glow, quick actions, six live statistics and source information. Connections, Options, Mirrors and Log join torrent Peers, Trackers, Files and verified Pieces views; speed graphs include torrent uploads and file maps remain visible beside the tabs.
- Main window: seamless icon rail, resizable download cards and a full-height details column; selected banner backgrounds, type artwork and optional colours sampled from game art.
- Saved sorting with date groups, queue and tag filters, an optional column table, and footer disk space plus download/upload limit controls.
- Desktop appearance foundation: saved background, accent, glass, progress glow and game-art preferences, shared dark controls and status pills, a bundled Inter font and consistent outline icons with a gear for Settings.
- Steam matches cache a wide library banner with capsule and store-header fallbacks alongside their existing icons and covers.

### Fixed
- Files, Peers, Trackers and Connections table headers stay above scrolled rows with solid backgrounds and their own bottom borders. Files has a select-all checkbox with partial-selection feedback.
- Game lookups drop trailing platform words: Windows, PC, Win64, Win32, x64, x86, Linux and Portable.
- Artwork revision 9 refreshes automatic lookups. Images are type-sniffed when a CDN omits Content-Type, including PlayStation art; PlayStation name searches retry shorter queries to handle registered trademark symbols in store names.
- Rail resizing captures the pointer across WebView boundaries, with a wider hover target and touch support. Labels and counts reappear when expanded; saved widths, keyboard controls and double-click toggling remain available.
- Navigation targets have solid hover/active backing, centered icons, compact corner badges, even spacing and a hidden scrollbar.
- Wide artwork keeps its aspect in details, selected cards and Add, fading into a colour wash at large widths instead of zooming; details height grows up to 420px.
- Ordinary filenames keep software and operating-system versions; game cleanup no longer leaves dangling separator tokens.
- Small Steam artwork tries the 616?353 capsule before the store header and displays without enlargement or cropping over a blurred colour wash. Older Steam banner caches refresh automatically.
- Console packages display their resolved game title while keeping the original filename; existing artwork matches also recover the missing title.
- Downloads without wide artwork use a dark, blurred icon backdrop with a sharp icon tile in selected cards, details, Add and completion notifications. Web artwork tries the matched page's wide social image first and repairs missing cached banners.
- Short or generic download names require an exact Steam title; other matches require multiple significant words. Saved incompatible matches are cleared for a fresh lookup.
- Game and application cards use cleaned display titles while retaining the real filename underneath. Finished files hide Resume in details, the selection toolbar and the item menu; torrent sharing remains available.
- Completion notifications keep game art in a fading top strip, with an overlapping icon, dark text area and accent timer. Retry notifications retain a red connection icon and border even for games; unnamed queue countdowns say "Queue finished" and keep a neutral Cancel button.
- Add links have a leading link icon. Bright detected artwork dims adaptively while keeping the left side dark, and yellow artwork produces a warmer gold accent shared with the main window. Start download includes its download icon.
- Details tables and graphs stack earlier in narrow windows; Options controls fit at minimum width, wide connection tables scroll, and footer limit labels wrap with their pickers. Numeric fields, details tables, paths and notification countdown/sharing values use the bundled monospace font.
- Bright game banners are sampled once to keep window backgrounds dark and softly coloured, with muted artwork accents and dark backing behind row pills and banner chips. Details artwork keeps its colour.
- Completed downloads without a completion date show just Done.
- Inactive download cards describe paused, queued, completed, sharing and error states without idle download speeds or connection counts. Footer speed pickers show the full limit text.
- Dialogs keep keyboard focus inside, offer a close button, protect forms from backdrop clicks and wrap footer actions.
- Removal uses one action with an optional Recycle Bin checkbox; prompts and countdowns name their actions, and update notes use readable formatting.
- Settings groups align controls, simplify wording and share speed presets with Scheduler. Theme changes reach open windows and native title bars.
- Small desktop windows keep extra list actions in More, scroll details in their right column, and stack cramped General, Scheduler and Add layouts; the main minimum is now 640x420.
- Frozen windows can recover after a repaint attempt. Recovery waits while you are away, the session is locked or the display is off, and gives the window time to recover when you return.
- Queue completion and shutdown/sleep countdowns depend only on downloads started during that queue run. Older failed or paused entries do not block completion; paused or failed downloads from the current run still do, and removed downloads are ignored. Each countdown keeps its captured force setting.
- Adding the same torrent again keeps the existing download and shows its name and status, including when adding several links or resolving magnet metadata.
- Pausing a checksum check keeps the download paused. Resuming checks the saved file again before marking it complete, notifying you or opening it.
- Updates resume the previous downloads and queues once. If the updated version cannot start, FluxDM stays open and resumes downloading.
- “Check now” in Settings checks the entered repository without saving other changes in the form.
- Enter and Escape affect only the top dialog after its controls have handled their own keys. Enter chooses the intended primary button, and closing a dialog restores the previous focus.
- HTTP downloads restart safely when the source file changes, while different mirror identifiers preserve progress.
- Moving torrent files refuses existing destination files. If a copy fails, partial copies are removed and the original location is kept.
- Global and queue speed budgets share spare bandwidth fairly across downloads, torrents and videos. Videos reconnect only for substantial speed changes, at most once a minute.
- Torrent upload limits apply separately to downloading and seeding torrents. Disabling uploads while downloading no longer blocks finished torrents from sharing, and seeding caps still apply during other downloads.
- Incoming links merge into matching Add forms; requests with different headers, filenames, queues or video choices stay separate, including while forms load.
- Authenticated .torrent links keep their browser request headers when fetching metadata. Redirects to a different origin receive none of those custom headers.
- The browser extension leaves POST downloads and their redirects in the browser.
- Removing or restarting new video jobs cleans their partial files and fragments. Finished outputs follow Keep files or Recycle Bin choices; cleanup failures remain available to retry. Older untracked partials need manual cleanup.
- Finished playlists show the combined file size, and Open / Show in folder target the playlist folder.
- Seeding torrents show their upload speed and peers in the list, and the footer shows the seeding count and upload speed.
- Inactive torrent details stop polling and redrawing until relevant data changes. Selection and content edits still refresh, including while an earlier request is in flight. Parsed torrent metadata is cached while its file stays unchanged.

## 2.2.1 — 2026-10-26

### New
- **Upload limits in the Add window for torrents:** *while downloading* and *when finished*, with the same presets as the right-click menu, including *No upload*.
- **Resume sharing a finished torrent** (right-click → *Resume sharing*). *Pause* on a finished torrent is now called *Stop sharing*. Before, nothing could start sharing again, and finished torrents never shared again after FluxDM restarted. FluxDM won't resume one whose files were moved or deleted, and says why in its status.

### Fixed
- **"No upload" uploaded at 32 KB/s**, and every torrent limit under 32 KB/s (such as the 20 KB/s preset) was raised to 32 KB/s. Both now work as set.
- A finished torrent whose seeding limit is *No upload* no longer sits "seeding" forever without sending anything; it stops sharing.
- **Clear finished** left finished torrents sharing in the background, with no row left to see or stop them.
- **Updating FluxDM could leave it closed:** the new version sometimes started while the old one was still closing, handed itself over to it, and quit. It now waits for the old one to exit.
- An app update, or the first-time yt-dlp/ffmpeg download, could hang forever on a connection that went silent. They now stop with a message after 60 seconds without data.
- *Give magnet links back* did nothing when FluxDM had been chosen in Windows' Default apps; it now opens Default apps and says what to pick there.
- *Force recheck* on several torrents stopped at the first one that couldn't be checked; the rest are checked now, and every failure is listed. A finished torrent whose recheck fails stays finished instead of turning into "Paused".
- With backup links, a full disk or a folder Windows won't let FluxDM write to was blamed on the links one by one ("link dropped"); it now stops with the real reason straight away.
- The phone remote's page refused magnet links, although the PC accepts them, and a link the PC rejected failed silently.

## 2.2.0 — 2026-10-16

### New
- **Torrent file picker, qBittorrent-style.** The Add window's file list is now the main part of the window: folders you can open and close, a box per folder that ticks everything inside, sizes, and a filter. *All* / *None* work on the files the filter shows.
- **One-line link box** in the Add window, with a ▾ to see every line and a copy button. A batch shows how many links it has. Enter starts the download; Shift+Enter adds another line.
- **Speed limits you can pick or type** in the Add window and in the details panel, like the global limit. More presets, with finer steps at the low end (64, 128, 192, 256, 384, 512, 768 KB/s, 1, 1.5, 2, 3, 4, 5, 7.5 MB/s and up).
- **Open when it finishes:** tick it in the Add window, in the details panel, or right-click a download.
- **Browser extension 1.4.0: catch every file type** (on by default). The file-type list is much longer and is only used when this is off, and by *Grab download links*.
- Updates are checked against this repository by default.

### Changed
- Torrents don't show connections, a file name or a checksum in the Add window. The checksum box moved into *Advanced* for normal downloads.

### Fixed
- Notifications that stayed on screen, or showed an old message, after a failed download.
- A "Download started" notification that was never followed by "Download complete".

## 2.1.6 and earlier

See the release notes on GitHub and `PROJECT_STATE.md`.
