# Changelog

What changed for people using FluxDM. Developer notes are in `PROJECT_STATE.md`.

## 3.8.2 — 2026-11-27
- Torrent details: selected and hovered rows in the Trackers, Peers and Files tables are visible again (they were selected but looked unselected).
- Split into parts: Refresh link... on any part now puts a fresh link, or a link to the same file on another site, on every unfinished part at once. FluxDM first checks it is the same file (same size, byte ranges, and sample bytes the parts already saved match) and says exactly what happened, for example "New link put on 3 parts (1 resumed)", or why it refused. Add backup link... on a part checks each link the same way and adds only the ones that match. A part stopped by an expired or changed link now says to use Refresh link... and offers it. The same works from a paired device: Refresh link on one part covers the group.
- Build: the merged torrent peer tests compile again (no user-visible change).
- Torrent details: the Peers card's seeds/peers line uses the same live snapshot as the Peers tab, so the two no longer disagree for a moment.
- PC torrent Peers tab: right-click a peer (or press the menu key / Shift+F10 on a focused row) for Copy address and Add peer. Add peer also has a button beside the peers summary, takes one or more IP:port or [IPv6]:port lines, refuses bad lines with the reason, and says plainly what happened: how many were handed to the torrent engine (it does not claim they connected), or "Start the torrent first". It is disabled for another device's torrents ("Only for torrents on this device"); Copy address works there too. Adding peers restarts the torrent's engine briefly, as adding a tracker does. The new text is in Arabic too.
- Add window: the split line's free space and its "not enough space" warning now follow a folder chosen with Browse... or picked by file type (it kept the first drive's numbers).
- Android build: opening a finished file compiles again (the PC-only error check had no phone counterpart).
- PC: the device switch above the list wraps onto a second line instead of clipping the last device behind a hidden scrollbar.
- PC torrent Files tab: the totals (files picked of all, size, progress, what is left or Done) are a plain line above the file list instead of a pinned bottom row that the file rows showed through; the line stays in view while the list scrolls.
- PC torrent Files tab: the totals (files picked of all, size, progress, what is left or Done) are a plain line above the file list instead of a pinned bottom row that the file rows showed through; the line stays in view while the list scrolls.
- PC details: the speed graph now has a time axis (60s, 30s, now), speed labels on the top and middle lines (still at least 1 KB/s), lines in the same colours as the download/upload legend, and a quiet "Waiting for speed data" instead of a lone label until there are two samples. In Arabic the time runs right to left.
- PC torrent Peers tab: each peer shows its client with the address under it, how much of the torrent it has (percent, a "Seed" badge, or "?" while that is unknown instead of an empty 0% bar), the connection type (TCP, uTP, Proxy) and what you downloaded from and uploaded to it. Idle peers show a dash instead of a bare 0, the rows no longer reshuffle every second, the "(N seeds)" count covers every peer when more than 200 are connected (with a "Showing 200 of N peers" note), the previous torrent's peers no longer linger after you pick another download, and the text for a queued, checking or failed torrent says so instead of "not running". Column widths dragged in the overview are remembered (Arabic included). The header bar's end no longer looks cut short, and in Arabic its rounded corners are on the correct sides.

- Phone remote login now sends a one-use HMAC challenge response and keeps only a 15-minute session token in session storage. Previously saved PINs are removed. Legacy x-pin clients remain supported for one release with a deprecation log; existing PIN lockouts also cover challenge login.
- Video downloads now verify yt-dlp's signed checksum list against a built-in signing key and check the executable before each run. Settings updates use the same verification instead of yt-dlp self-update. An old or damaged copy without valid signed checksums is replaced by a verified download; if that fails, it is refused with an English/Arabic message.
- The Android Quick Settings tile resumes only downloads it paused, including after an app restart.
- Pairing between updated devices now commits to hidden keys before revealing them, preventing adaptive pairing-code searches. Older versions still pair, with a visible security warning on the updated device (English and Arabic).
- New: Split into parts (engine and Join). A big file can be downloaded as 2 to 99 separate parts (`name.part2of4`), each an ordinary resumable download of its own byte range, so a drive smaller than the file can fetch it part by part; the parts are moved to another PC and joined there into the one file. A server without byte-range support is refused with the reason, and a part whose server file changed (size, ETag or Last-Modified) stops with a clear error instead of mixing two versions.

- New: Split into parts on the PC. In the Add window, a "Split into parts" control (Off, 2, 3, 4 or a number you type) shows each part's size and the free space of the chosen drive, lets you tick which parts start now, and refuses with the reason when the server has no byte-range support or does not say the file's size. The parts sit together in the list, each tagged "Part 2 of 4", with "Download only this part" in the right-click menu (it pauses the other parts). "Join parts..." in the More actions menu takes the part files or their folder, shows the detected file, the parts found and missing, the joined size, the free space and a "delete parts after joining" box, then reports the real result (bytes, path, warnings). A failed join keeps its reason on screen. Starting parts and joining are queued correctly with the other list actions. All of it reads in Arabic.

- Device link: a fake network announcement can no longer rename a paired device or hide its real address, and if something else answers at an address the other known addresses are still tried. Strangers on the network can no longer fill memory with fake devices. A changed file in a re-sent folder is sent again instead of being skipped; two receives of the same folder or download never write into the same folder; on storage without hard links a received file never replaces a file that appeared at the same moment; a torrent hand-over stopped halfway makes the old download recheck its files.

- Torrent Peers tab: it no longer says the torrent is not running while it is downloading, a busy moment no longer empties the peer list (it says how many peers are connected when their details are unavailable), and the connection tables fit a narrow pane (Downloaded, Uploaded and Flags show only when the pane is wide).
- Opening FluxDM again from the app icon while a download runs no longer crashes the app (the second launch is dropped cleanly). "Delete permanently" on a finished video now deletes even on a USB or network drive. The Recycle Bin refusal, its reasons, the "Not deleted" title and the paired-folder refusal now read in Arabic.

- Link refresh keeps the old link and partial file unchanged when saved bytes fail a comparison with the new link (the message says to use Restart); with no saved bytes to compare it simply proceeds, and answering Replace in the browser-capture question keeps the bytes unchecked, with a note saying so. Shortened partial files fetch missing bytes again. New downloads avoid partial-file and checksum-sidecar name collisions. Device transfers sync received files before reporting success and reject overlapping or incomplete resume maps.

- If FluxDM cannot save before exit and stays open, the message now says what is true: downloads were paused (or that pausing did not finish in time), every queue was stopped and must be started again, and torrents cannot resume until FluxDM is restarted; pausing a waiting download can no longer overwrite one that has just started.

- Removing several finished downloads that cannot go to the Recycle Bin now names them (count and first names) and "Delete permanently" deletes only those, never the rest of the selection. A refused delete no longer leaves the row stuck as "being removed"; "Remove from list only" works on it afterwards. The Recycle Bin size check no longer assumes a larger bin than Windows gives, so a big file is never deleted for good without asking. A finished file whose size changed now says how to proceed. A paused torrent no longer shows its old peers, and peers that failed for a day are no longer redialled every 30 seconds. The tracker note "(added by you, not used: private torrent)" and "(offline)" read in Arabic.

- The Arabic message for a failed pause, resume, restart, retry or reset now reads fully in Arabic (part of it stayed English), and a failed first-run look save really applies the chosen look until you close FluxDM.

- Open on a finished download now says why when it cannot open the file (moved or deleted, no app set for it, access denied) instead of doing nothing. Pause, resume, pause all, retry, reset, restart and clear-finished report failures with the number of downloads, and Clear finished says how many were removed. A refused speed-limit change no longer shows the new limit, and dismissing the 'File already exists' dialog or a failed first-run look save now explains what happens next. Arabic included.
- Reduced memory used by list updates and the work done between downloads; speed history now keeps its last minute without shifting older samples.
- Toasts and device and queue views use fewer background timer wakeups.

- A paired device can no longer save into a network folder (a \\server\share path) that is outside your allowed folders; the check was skipped for those paths by mistake.

- Deleting a finished video or torrent whose files cannot go to the Recycle Bin now also keeps the download in the list, so the 'Delete permanently' choice can be retried; before, the row could be gone by then.

- A paired device can now only choose save and move folders inside the folders you allow on this PC (Settings > Where files go > 'Folders other devices may save into'). It starts with Downloads, Videos, Documents, Music, Pictures and Desktop, plus your default save folder, and you can edit the list. Any other folder is refused with a message naming the folder and why. Existing settings get the starting list; a download already saved elsewhere is not touched, but a new add or move to such a folder from a paired device is refused until you add that folder to the list.

- Deleting a downloaded file never silently deletes it for good any more. If a file cannot go to the Recycle Bin (it is on a USB, network or removable drive, bigger than the bin allows, or the bin is set to delete at once), FluxDM keeps the download in the list, says which file and why, and asks. There is a new 'Delete permanently (skip the Recycle Bin)' tick box in the Remove window on PC and, for a paired PC, on the phone (English and Arabic).

- An address that already entered the right PIN is now locked for 5 minutes after 100 wrong PINs, so a device that later gets that address cannot guess the PIN without limit.

- Another device can no longer save into your user profile folder itself, Documents\WindowsPowerShell, Documents\PowerShell, .ssh or .config (files there run or load at the next shell start).

- A web page open on a paired phone can no longer lock that phone out of the PC remote: browser preflight requests are answered without counting as wrong PINs, and an address that already entered the right PIN is not locked by failed attempts.

- Fixes the phone page's error message for files that could not be copied for sending.

- After swiping FluxDM out of Recents, the phone app now ends itself once the last download or transfer finishes (it used to stay cached with the engine running), and reopening it while it was still running starts cleanly instead of risking a crash.

- Sending a download from the phone browser to FluxDM no longer risks a duplicate: it retries only when FluxDM could not be reached at all, and if FluxDM did not answer in time it says the result is unknown instead of trying again.

- Reopening the phone app after swiping it out of Recents, what happens now: with nothing running, it restarts cleanly in a fresh process and keeps what you opened it with (a shared link or file, the copied-link shortcut, a notification tap). While a download or transfer is still running, FluxDM no longer ends the process (that used to stop the work): the launch is dropped with a message to open it again once the work is done, and the shared link or tap is not kept; the work carries on and the process ends itself when idle. The same applies if Android destroys the backgrounded screen under memory pressure or with "Don't keep activities" while the process lives on: idle means a clean restart with the launch kept, busy means the message above. Rotation and other window changes do not recreate the screen at all, so they are not affected.

- The phone's storage and battery permission prompts are now only marked as asked after you return from the system screen, so one that never opened is asked again next time.

- Downloads caught in the phone browser are no longer lost when FluxDM's engine is briefly down: the browser retries for about 30 seconds, and says plainly if FluxDM still did not take it (English and Arabic).

- Downloads caught in the phone browser are no longer lost when FluxDM's engine is briefly down: the browser retries for about 30 seconds, and says plainly if FluxDM still did not take it (English and Arabic).

- Sending files or a folder from the phone now checks there is room for the copy first and tells you plainly, naming the item and the reason, when it could not be copied or when files in a folder could not be read (English and Arabic).

- Folder sends from the phone work again after a broken change: the copy now names each file it writes, and two folders with the same cleaned name no longer merge.

- Sending a folder from the phone no longer sends a short folder when a file cannot be read: the copy is dropped instead, and files whose names collide after cleaning get a number (name (2)) rather than overwriting each other.

- Swiping FluxDM out of Recents on the phone no longer stops downloads or device transfers that are still running; the next cold start cleans up as before.

- The phone app no longer restarts its engine when the system font weight, grammatical gender or mobile network codes change (the main screen now handles those changes itself).

- Downloads from a mirror redirector (different servers, different ETags, same file) no longer stop as 'file changed': FluxDM now compares the actual bytes before deciding, and a real content change, even at the end of the saved part or on a third mirror, still stops the download.

- A failed background save of the downloaded data no longer stops further background saves for the rest of the download; FluxDM retries after a pause and notes the problem once in the download's health log.

- With backup links, a failing connection now retries after 1 second only twice, then waits longer each time, so the retries are no longer used up in half a minute.

- A backup link that cannot resume or serves different bytes is now dropped on its own; the download carries on from the other links instead of stopping.
- The old bookmarklet links (/add, /batch) can no longer refresh or replace a download's link; they only open the Add window. Requests that are not a page navigation (a hidden image, script or fetch) are refused, while the bookmarklets' popup windows keep working.

- Updates only install the signed FluxDM-Setup. The old fallback to the portable FluxDM.exe is gone; when a release has no installer, no checksum or no signature, the update window says exactly which piece is missing and points to the release page. Arabic included.

- 'Maximum connections per torrent' now shows 200 on PC and phone, the same default the engine uses, so saving Settings no longer lowers it silently, and the restart notice no longer appears when only the unset default is written.

- Force recheck no longer gives up after 30 minutes on big torrents: the limit is the larger of 30 minutes and the torrent's size read at 15 MB/s plus half again (about 3 hours for 110 GB). If it still runs out, the message gives the minutes allowed and says everything verified so far and all downloaded data were kept; Arabic included.

- Removing the only running download of a queue no longer shows 'Queue finished' or runs the queue's shutdown/sleep action.

- Removing a download with its files now says exactly which files were left on disk (torrent files that could not be deleted, or a path too long for the Recycle Bin) instead of staying silent.

- Removing a finished download with its file no longer deletes a file that changed size, turned into a folder, or is used by another row; the message names the file that was left.

- When FluxDM refuses to delete a finished file (changed, now a folder, shared with another row, or a path too long for the Recycle Bin), the download now stays in the list so you can retry or choose Remove from list only.

- A torrent stopped by a disk error starts again when you resume it (it used to stay stopped until restarted). A torrent with no connected peers retries peers it had given up on when trackers report them again, on Re-announce, and after 5 minutes without peers.
- Peers a torrent gave up on are no longer redialled every 30 seconds when trackers keep reporting them: they keep their growing wait, and only Re-announce starts over. The 5-minute no-peers retry no longer asks trackers before their minimum interval has passed.
- Private torrents only use their own first tracker; the extra trackers from Settings are no longer added to them.
- The Trackers tab can copy every tracker of a torrent (Copy trackers), select rows, copy the selected ones, and edit or remove the trackers you added. The torrent file's own trackers stay read-only. Messages say exactly what was copied, changed or refused; the phone has Copy trackers too; all in Arabic. Changing or removing a tracker now applies to paused torrents too, and a failed change no longer leaves the torrent paused. Private torrents refuse extra trackers.
- Torrent checks show the good data found so far, including progress for each file.
- Pausing and resuming a torrent keeps its check. When drive error reports are on, old saved data is checked once per session.
- Drive error reports are off by default. Settings > Behaviour lets you turn them on for each drive; the switches and messages also work in Arabic.
- A torrent check no longer counts a piece as good when part of it could not be read from the drive.
- A damaged block-check file or a link with an extreme expiry time no longer crashes FluxDM; the refresh page keeps a site's port number.
- The speed graph draws its fill with every accent colour again; column widths are saved after resizing; a new download is scrolled into view in a grouped list; the tour finds Settings pages in Arabic.
- Phone: speed-rule changes are really saved (and undone on screen when refused); a cancelled swipe or queue drag no longer acts.
- A schedule time with extra text after it ("09:30:xx") is refused instead of quietly read as 09:30.
- Phone: some file errors were wrongly reported as "disk full" or "another program has the file open". Video sections with an endless time ("inf") are refused.
- Devices: sending two folders with the same name keeps them apart ("Folder" and "Folder (1)"); links inside a sent folder are no longer followed, so nothing outside the folder is sent.
- Devices: if the device key can't be read for a moment, FluxDM no longer makes a new identity (which made paired devices pair again).
- Code cleanup across the desktop and phone app (less code, same behaviour); console artwork no longer re-reads .torrent files every few seconds; settings are read without copying them.
- PlayStation torrents can find their title and artwork from the title ID in their files. Numbered games and films no longer take artwork from a different entry in the series.

## 3.8.1 — 2026-11-25

- Phone: the bottom bar keeps its labels clear of rounded screen corners.
- Phone: the Queues page and failed downloads no longer have a large empty gap in their cards.
- Phone: the + button works while you look at another device's downloads; the Add page opens with that device already chosen, also while it is offline.
- Phone: **Stay reachable in the background** (Devices page, off by default) lets your paired devices send to and control the phone while FluxDM is not on screen. On Tecno, Infinix and itel phones a row below it opens the page where No Restrictions stops the phone from freezing FluxDM; on Samsung phones two rows open the battery pages to change.
- Phone: a paused download's page shows one percent instead of two different ones, and in Arabic a failed card's size sits under its text.
- **Refresh link** and **Add backup link** now work on another device's downloads. You type or paste the link here; the other device checks it and makes the change. If the new file is a different size you are asked here first. An older FluxDM on the other device says it needs updating. A slow answer says the result is unknown instead of failed.

## 3.8.0 — 2026-11-25

**In short**

- **The window keeps answering** while a torrent is checked or a drive is busy.
- **Your files are safer:** downloads are verified after saving, damaged blocks are fetched again, and deleting, moving or adding a torrent touches only its own files.
- **Refreshing a link** tests the new link first, compares what is already saved, and never restarts a download by itself.
- **Save diagnostics** makes one clear zip for a bug report, with private names and links hidden. Nothing is sent by itself.
- **Notifications** stay out of your games and can be turned down.
- **Devices:** orders, queues and permissions between your PC, laptop and phone are more reliable.

**Everything**

- Arabic and layout polish: the Add window's "When done" list no longer clips its last letter, the video options and placeholders are translated, a paused phone card keeps its percent in view, English done dates stay on one line, long actions on a download's page get their own row clear of the gesture bar, and a few phone messages that were still English are translated.
- Two downloads with the same name never share a partial file, also when their folder is written differently (slashes, capital letters).
- **Adding a torrent never takes a file of yours.** A file already in the folder with the name of a torrent file you left out used to disappear into FluxDM's hidden store.
- The Refresh link dialog says why a new link was refused and that the old one was kept. Arabic phone details show sizes in order.
- Refresh link checks the new address with its intended headers before stopping the current download or replacing its link. A rejected link keeps the old link and saved data; a newer refresh, Remove or Move wins over an older check.
- Refresh link checks the saved file size, server checksum and comparable ETag/Last-Modified before reusing progress. Changing a signed URL's query no longer bypasses its saved validator; another site's ETag is kept separate.
- Before resuming a refreshed link, FluxDM compares bounded samples of saved bytes with the new server. Different bytes keep the partial file and old link. A server that refuses sample ranges is reported as unverified.
- A refreshed link is announced as resumed only after new download bytes arrive. Saving the link alone no longer claims that the download has resumed.
- Pasting a link on another site drops the previous cookies and headers and tells you. Empty browser captures cannot carry the previous site's credentials to the new site. Same-origin pasted links keep their headers, including during the dialog's check.
- Refreshing a finished download or a video only swaps the link, as before. A refused new link now says why: sign-in needed, expired, deleted, or the site's limit or quota (with the wait it asked for), in English and Arabic on PC and phone.
- The browser's new link is matched by the file's id on known sites (Pixeldrain, Gofile, MediaFire, GitHub, Hugging Face, Drive, Dropbox, Archive.org and more) or by its download page; a matching size alone never replaces a link without asking. A checksum the new site publishes is kept for the final check.
- **Refreshing a link never restarts a download by itself.** When the new link does not say the file size, FluxDM asks first instead of deleting what is already downloaded, and the button says so.
- **Deleting or moving a torrent touches only its own files.** Other files you keep in its folder stay where they are. When the torrent's info is missing, FluxDM refuses instead of guessing. Files you left out of a torrent are not touched.
- A paired device needs the delete permission to start an unfinished torrent over on another drive. A cancelled shutdown or restart can never come back after FluxDM starts again.
- Removing a playlist never deletes its whole folder when its own files are unknown or replaced. Remove and Restart no longer wait for ever for an archive check on a dead drive.
- Removing or restarting a video whose file was replaced by another download never deletes that newer file.
- **Force recheck reads the whole torrent.** A finished torrent that was not being shared could be reported as fine after reading only a few pieces.
- A crash is noticed at the next start even if another program still watches the ended process.
- Arabic phone: the size on the Add page and the reason of a check cut short read correctly.
- **Restart from zero** moved into the Advanced submenu (PC: More > Advanced), away from everyday actions.
- Diagnostics keep version numbers, setting names and plain words readable while private names stay hidden.
- The PC Add window no longer shifts File name beside its label (it was squeezed into the narrow label column with Queue next to it) when the drive-warning line is empty.
- Restart on a download that another download replaced now warns, when the file-exists setting is Overwrite, that the other download's file at that place will be replaced. The restart text uses the words of each app (phone: Keep both / Replace, PC: Add a number / Overwrite), and a torrent with one file no longer says "up to 1 files".
- Diagnostics: info.txt, the event log and the saved message say Android, System WebView, "Phone uptime" and phone names on Android (no Windows, WebView2, administrator or drive-letter wording); Windows 11 is no longer reported as Windows 10. The saved message is Arabic in Arabic on the PC and the phone.
- Retries, DNS and network waits appear as warnings in the event log (at most one per 10 s, the rest stay info and are counted), so problems.txt shows them; the final failure of a download was already an error.
- Phone Settings shows the quiet "FluxDM didn't close normally last time" note under Save diagnostics after a crash; saving clears it.
- The phone Settings note about closing FluxDM from recent apps now says downloads stay paused (they only start by themselves again when a queue is set to start when FluxDM opens).
- Phone, small screens and Arabic: a paused download's percent wraps instead of being cut, the Add window's size line keeps "300 KB" in order, a long path in the details breaks at / and not inside a name, tab labels keep a margin, and "Accept this file anyway" wraps.
- Android: a torrent that is only sharing shows "Sharing" (and its upload speed) in the notification instead of "100.0%". A torrent's average speed no longer counts the time it spent sharing.
- A long list uses less processor time while nothing is happening.
- Restart confirmations now say that an already finished copy stays until the new one is done, then the file-exists setting decides (Keep both adds a number).
- Phone download details show **Accept this file anyway** beside Retry for a server checksum mismatch. Arabic now covers checksum, connection, disk and save errors on both layouts.
- Arabic paths, rates and link placeholders keep their reading order. The PC Add window fits its Arabic controls, and sidebar labels can wrap.
- Phone lists wrap finished dates and problem reasons, give navigation labels breathing room and leave space below the last row for the Add button. The Add page follows the keyboard's visible area.
- Short single-word file names need an exact game title and separate supporting evidence before receiving game artwork. Add-by-address failures show the address once.
- Android no longer treats a finished HTTP worker as pending work; idle foreground notifications stop, while downloads, seeds and device transfers stay active. Overwriting a file keeps its old download row and marks it as replaced. Replaced rows are not restarted by bulk actions.
- Restart now says what it really deletes: torrents delete their files (even ones that were there before), videos delete their saved files, web downloads keep a finished copy. A check cut short by closing FluxDM comes back Paused with that reason.
- When a device refuses a handover that would replace its download (permission off), the sender now says why instead of "did not arrive".
- **Android: downloads that stopped at "Paused" when finishing.** Phone storage that refuses a safe rename ("Invalid argument") no longer keeps a finished download from being put in place. A download paused by a problem now says which, and never shows 100% before it is done.
- **Save diagnostics.** Settings can save a zip of recent problems, crash reports, settings and download/device summaries for you to send by hand. Links and paths are shortened and known private names and secrets are removed. Copy summary includes recorded crashes. Detailed log is available on PC and phone, turns off after 24 hours, and stays off after it expires until you explicitly enable it again.
- Diagnostics keep old file, queue and device names private after renaming or deleting them, handle equivalent Unicode spellings, and stay bounded when a download-list or device-link lock is busy. Very large parts are shortened or omitted with an explanation to keep the zip within 8 MB.
- **Notifications stay out of your games.** New setting "Show notifications above full-screen games and apps" (off by default, also for existing installs). While a game or full-screen app is in front, FluxDM's notifications wait and never take focus from it; when it ends they appear as one summary ("While you were in full screen: 3 finished, 1 failed"), or as themselves when there is only one. Pairing and browser-approval windows wait too. The shutdown / restart / sleep countdown always shows.
- **More control over notifications.** Notifications: All, Important only, or Off; switches for finished, failed or needs attention, devices, torrents, and updates and tips. "Stay on screen": Short (3 s), Normal, Long (10 s) or Until closed; failures stay 1.5 times longer, the time stops while the pointer is over a notification, and it fades quickly (not at all with reduced motion). "Show a test notification" says if it is being held. Anyone who had notifications off keeps failures quiet.
- Interrupted device adds recover on retry or restart. Waiting sends reach older devices once; a lost answer never sends them twice. Handovers carry block checksums and recover from a failed save. Add selects the device being viewed and its requested queue when available.
- Device delivery journals keep the latest 500 answers per device and release unused delivery locks.
- **Hugging Face models get a picture.** A model file from huggingface.co shows the picture its model card names (wide pictures as the banner, square ones as the icon), otherwise the publishing organisation's logo. A personal account's photo is not used.
- **Dark logos of GitHub projects are readable.** A project's own README logo that is black on a see-through background (PS5 Upload) is shown on a light plate: a wide one as the banner, its symbol as the icon. Badges, screenshots and other pictures are judged as before. Items that found nothing are looked up once more.
- **Accept a file anyway.** When the checksum the server published does not match, the file is kept and you can choose "Accept this file anyway" (right-click menu, details, and the phone item sheet). It asks first and says the file does not match. It only covers that exact server checksum and those exact bytes, never your own hash or the drive checks, and the finished download keeps a note about it. Restarting clears it.
- **Archive check** can be cancelled from the window, is stopped when the download is removed or FluxDM exits, never stores a result for a file that changed or moved, and has a row and action on the phone. Its messages are translated, Arabic included.
- The drive warning also shows in Settings beside the download folder.
- **The window no longer shows "Not responding" while the drive is busy.** Everything the page asks for (details, saving, checking files, opening folders, torrent engine calls) now runs in the background; the window only draws. Actions that must keep their order (start/pause, edits, limits, queues, settings) still apply in the order you made them. Changes are saved a moment later by a background saver, and Exit still saves everything first: if the drive is slow it says so and waits, and if saving fails it stays open (choose Exit again to close anyway).
- A watcher writes one line to the log when the window stalls for over 3 seconds and one when it recovers (no file names or links), so a freeze can be traced.
- Lists and status that refresh on a timer never have more than one request waiting.
- **The window no longer freezes while a finished torrent is checked.** Checking the saved data of a torrent could leave the whole app "Not responding" until it ended. The list, details and limits now answer from the last known state while the engine is busy, and checks (torrent verification, hash and block checks, archive tests) take turns on a drive (for up to a minute). Cancelling a check also works while it waits for its turn.
- **Verified saving.** Every downloaded block is checksummed as it arrives, and when a download is finished the file is read back from the drive (not the cache) and compared. Damage from the drive, its cable, the file system or memory is found and only the damaged blocks are fetched again (3 tries, then the download stops with an error naming the drive and keeps the partial file). After a restart the saved blocks are checked too. The details say "Checked after saving"; fetching blocks again also shows a notice. New setting "Verify after saving" (on by default).
- A checksum the server publishes for the whole file (Repr-Digest, Digest, x-goog-hash, Content-MD5 on a full answer, x-amz-checksum-sha256) is checked after saving too; your own hash always wins. A mismatch is an error with Retry, never a completed download.
- **Torrents are read back before they finish.** Pieces saved during a download are read from the drive again (bypassing the Windows cache) and checked before the files are published; damaged ones are downloaded again, up to 3 times, then the torrent stops with an error naming the drive instead of finishing with a corrupt file.
- **After a crash or power loss every torrent piece is re-checked**, not a sample, so damaged pieces in the middle of a download are found. A normal restart still resumes instantly.
- **Drive warning.** FluxDM reads the Windows event log (read only) and warns, once a day per drive, when Windows reported disk errors on a drive it saves to, in the Add window's folder row and the Health tab.
- Remote orders retry safely without repeating changes, report which downloads were skipped and why, and support queue edits, torrent checks, tags, connections and seeding limits when both devices are updated.
- Downloads can show a background made from their artwork when no banner is available, and FluxDM and Deck installers use their own artwork.
- Installers avoid unrelated game pictures, GitHub homebrew files can show their project's art, and supported Nexus mods show their game's art while keeping the mod name.
- **Speed limits apply at once.** Raising or removing a limit wakes downloads that were waiting on the old one, a torrent no longer runs over its limit while limits are shared out, and a video follows a changed limit after about 5 seconds.
- **The main upload limit covers everything.** It caps downloading and seeding torrents together; the seeding limit works within it. "No upload" stops seeding too.
- A picture search cut off by a dropped connection is tried again soon instead of a week later.
- **A speed limit goes to the download you set it for.** Clicking another download while in the limit box put the limit on that one; leaving a limit box no longer brings back an old value.
- A changed limit no longer interrupts a video that is being merged.
- **Shutting down when finished is reliable.** FluxDM waits for other downloads instead of skipping it, runs the 60-second countdown itself even when its window is closed, then Windows closes every app after 2 more minutes (save your work or press Cancel). Your other devices are told what really happened and can cancel it. Closing the dialog only hides it.
- **Moving a download to another device is safe when the connection drops.** The other device's copy is replaced only once everything arrived, the download never runs on both, and FluxDM checks whether it arrived instead of guessing. Waiting sends stay in order, and a device that doesn't answer no longer holds up the others.
- **Names with special letters are read correctly** ("Ghost of Yōtei"), and archives named by a PlayStation ID get the game's name and art; its DLC says so.
- The Add window's space warning is for the device and folder chosen.
- **Archives are tested after downloading** (zip by FluxDM; rar and 7z with an installed 7-Zip or WinRAR): damaged files are named, and a package that was cut short is noticed. Right-click > Check archive does it any time.
- **Permissions per device** (Devices > Permissions): whether it may delete or replace files here, and shut down, restart, sleep or close FluxDM. Devices already paired keep both; a newly paired one starts without them.
- Titles of PS5 tools no longer end in "elf".
- **Phone:** downloads and transfers started from another device keep running while the app is in the background, a pairing request shows a notification, and "Send files" sends only what you picked.
- Files sent through Discord no longer show Discord's own banner. Homebrew packages from GitHub show their project's art.
- **Orders to your other devices are reliable.** An order is done once even when its answer is lost or it is tapped twice, a dropped connection is retried for 20 seconds, and the message says what really happened ("3 paused on Laptop. 1 skipped: X (finishing)").
- **Queues of another device.** Edit, start and stop act on the device shown; only what you changed is sent, so a change made there isn't undone.
- **More from another device:** seeding limit, downloads at once, connections, download in order, tags, recheck and reannounce; the limit really in effect is shown while a schedule runs.
- Saving Settings no longer puts back a speed limit changed elsewhere while the window was open.
- **Right game for a wrong PlayStation ID.** When a file plainly names a different game than its ID (one mistyped digit), the file's name is used.
- Downloads whose site hides the name ("[DLPSGAME.COM]-G_04865_...") show the right game and its art.

## 3.7.1 — 2026-11-22

- Switching downloads is smoother: the picture behind the window cross-fades and the colours fade more slowly.
- The Add URL button lines up with the sidebar rows below it.
- **Settings sections fill the sidebar.** The section rows grow to use the available height, stay compact in short windows, and keep their icons and labels left-aligned.
- The art strip on the selected list card frames near the top for every picture, not only ones FluxDM had analysed.
- **Artwork stays put while dragging.** Download pictures no longer start native image drags or trigger the link drop overlay inside FluxDM.
- **Faces stay in wide banners.** When you haven't positioned a wide banner yourself, FluxDM frames its upper part, so heads are no longer cut off (e.g. Iron Man).
- **Faces stay in download cards.** The narrow artwork strip frames its upper part automatically, including portrait pictures.
- **Better poster framing.** Portrait posters now show more of the upper part in icons and wide artwork, helping keep faces in view.

- **Icons for known programs.** VLC, Blender and Debian downloads can now show their logos alongside their banners.

- **Clearer torrent file status.** The Files tab now shows the selected file count and remaining download size in easier-to-read text, with room below the last row and total.
- **Reposition icon.** Right-click a download, Look, Icon, Reposition icon: drag the picture (or use the arrow keys) to choose which part shows in its square icon, for example to show a face the automatic crop cut off. Reset goes back to automatic; choosing a new icon image starts centred again. Works for downloads on your other devices too.
- **A total under the file list.** A torrent's Files tab ends with a Total row (the ticked files, their size, progress and what is left, the amount left in the accent colour) that stays at the bottom while the list scrolls.
- **Custom starts from what you had.** Switching to Custom from Simple starts with every part off, and from Full with every part on, instead of always turning everything on.
- **No more colour flicker.** When the colours follow the selected download's art, they now fade to the new colour instead of jumping, and only once you stop on a download, so clicking or arrowing through the list no longer flashes the whole window.

## 3.7.0 — 2026-11-22

### Simple, Full or Custom interface
- **Simple** shows only what most people need: All, Downloading and Finished; six categories (Games and AI Models count under Programs, Compressed and Torrents under Other); Resume, Pause and Remove; no Queues or Stats buttons, grouping, network details or speed-limit boxes; a details pane with just progress, speed, time left and where the file goes (Files for torrents); and a short right-click menu with everything else under More.
- **Full** is FluxDM as before, and stays the setting for everyone who already uses it. **Custom** lets you tick each of the eight parts on or off.
- Switch in Settings, Appearance, Interface, or from the "..." menu. New installs choose Simple or Full on first start. Nothing is turned off by hiding it, and a download with a problem still shows Health and its fix buttons in every mode.

### Pictures
- **Repacks with short names get their banner and icon.** A name like "Metal Gear Solid V - TPP [FitGirl Repack]" now finds the game: short capital abbreviations match the title they spell ("TPP" = The Phantom Pain, "DC" = Director's Cut), and a torrent that still finds nothing tries the full name from its magnet link.
- Names cut off in the middle of a bracket (common in magnet links) no longer search with the leftover piece.
- Downloads that found no picture before and that these changes can help are searched once more by themselves.

### Look
- **Search moved to the download list.** The search box is now at the top of the list, above the action buttons, instead of in the title bar. Ctrl+F still jumps to it.

### Download health
- **The Health window uses its full width.** A single problem no longer sits squeezed in the left half, a long name ends in "…" instead of pushing the status out of its card, and the status is shown as a small label.
- **The right buttons after a restart.** A download paused with an error kept only "Retry now" once FluxDM was restarted; it now offers the fixes for that error again, such as Refresh link and Add a mirror for an expired link or a web page instead of the file.

## 3.6.1 — 2026-11-21

### Phone
- **One way to switch devices.** The row of device buttons above the filters is gone; the device name at the top switches, and its menu shows a green dot next to each online device.
- **Speed limits for the device you're viewing.** While the phone shows a PC, Speed limits changes that PC's limits (it changed only the phone's before), and the bar at the bottom shows the PC's own limit. The PC needs this version too.
- **Queue order from the phone works.** The up arrows (and dragging) on another device's queue now move the download; before, the phone said "Queue updated" and nothing moved. The other device needs this version too.
- **"Lowered to 1 for now" goes away.** A download's details no longer keep saying its connections were lowered after it is back on all of them.
- **Notifications after a failed download.** A download that failed no longer keeps its progress or "waiting" notification on the phone until you delete it.
- **Smoother scrolling.** The download list no longer jumps around by itself after a fast scroll.
- **Instagram photo posts** say plainly that only videos are downloaded from them, instead of "There is no video in this post".

### Other devices from the PC
- **Speed limits:** while the PC shows another device, the Download limit and Upload limit boxes in the status bar change that device's limits; before, the choice snapped back and could even change this PC's own limit to the other device's.
- **Queue order:** the queue window for another device now has the up and down arrows (and dragging) to change the order.

### Browser
- A download sent from the browser is no longer downloaded twice (by the browser and FluxDM) when the site is slow to answer.
- Settings → Browser extension no longer shows two install buttons for the same unsigned extension in builds without a signed one.

## 3.6.0 — 2026-11-20

### Torrents
- **Huge torrents work.** Torrents with a very large number of pieces no longer lose almost every peer or stop after their first pieces, and FluxDM no longer sends each new peer a list of every piece while it has only a few, which saves a lot of upload on slow lines.
- **Magnet links with thousands of files** no longer stay on "getting the torrent's info from peers" forever. The file list is fetched from many peers at once, a peer that drops carries on where it stopped, and peers that lie, stay silent or repeat themselves can't stall it.
- **A Files tab for thousands of files.** Folders start closed so the list stays smooth, and there are Select all, Select none, folder ticks and a "Find a file or folder" search that change many files in one step. A torrent too big for the drive tells you to choose fewer files, and Resume opens the Files tab.
- **Better tracker timing.** Torrents ask trackers for peers as often as the tracker asks, wait longer after each failure (up to an hour) like qBittorrent, and try a UDP tracker's other addresses before counting a failure. A tracker that never answers no longer stalls for good.
- **Choose the files of a paired device's torrent.** From the phone, pick which files of a PC torrent to download (All, None, folders, files, priority), and from the PC do the same for a phone torrent. A device on an older FluxDM tells you to update it.
- **Safer with bad peers.** One peer can no longer make FluxDM use a lot of memory, or get honest peers banned by sending a broken file list. Changing a torrent's files while it is being checked or moved now says so at once.

### Getting files out
- **Copy files and drag to Explorer.** Right-click > Copy files (or Ctrl+C) puts finished downloads on the clipboard to paste in Explorer, and you can drag them onto Explorer or the desktop. Unfinished, missing or busy ones are skipped and named, and a copy Windows refuses says so.
- **Show in folder scrolls to the file**, even when that folder was already open.

### Fresh links from the browser
- **Refresh link can open the download page.** Click Download on that page again and FluxDM takes the new link for the same file and resumes, keeping what it already has.
- **"Already in FluxDM" question.** Clicking Download in the browser on an unfinished download asks whether to use the new link and resume, instead of adding it twice. A file of unknown size starts over rather than continuing onto old bytes, and the question says so. It also works when the main window shows another device's list.
- **File hosts with a download button stay in the browser.** Pages that make the download themselves (Free download, captcha, countdown) are left to the browser instead of failing with "returned a web page".

### Game art for all consoles
- Games for Switch, Wii, GameCube, Wii U, DS, 3DS, PS3 and PSP get their real cover by game ID or serial, PS1 and PS2 games by serial, and NES, SNES, N64, Game Boy, GBA, Sega and other retro files get box art by their official name. Only exact matches are used, a picture you chose is never replaced, and downloads that found nothing retry once. A download named by a serial shows the game's name once its cover is found.

### Arabic on the PC
- **New Language setting** (System, English, Arabic). Arabic mirrors the main, Add and notification windows right to left and translates labels, menus, dialogs and notifications, while download names, paths and links stay as they are. Settings pages show their own icons, and Settings can be saved while a speed limit is unlimited.

### Easier to use
- **Simpler right-click menu.** Grouped by task and showing only what fits the download. Nothing was removed.
- **Tidier Settings.** Language has its own page after Appearance, Updates is the last page, and Appearance packs its cards in two columns.
- **The list scrolls to a new download** when you add one (a large batch keeps your place).

### Browser extension 1.5.1
- **New look** matching the app, and private-window downloads keep their cookies in memory only.
- **Clear messages** when FluxDM isn't reachable (with the port), needs approval, leaves a download to the browser, or can't download a link.
- "Let my next download go to the browser" now works in Waterfox too, and the clipboard list is now "File types to catch from the clipboard".
- **Installed by hand for now.** Waterfox and Firefox get the signed version from Settings > Browser extension, which shows the signed and the newest version. While the newest isn't signed yet, a second button installs it unsigned (for browsers with signature checks turned off).

### Your other devices
- **Remove and move downloads on your other devices.** From a PC or phone, open a paired device's list to remove downloads or move them to another folder there, including a USB drive or SD card. Remove asks first and keeps finished files unless you choose to delete them. Moves are checked carefully (protected folders, shared folders, network shares) and a mixed selection reports what was moved, skipped or failed by name. The receiving device needs FluxDM 3.6.0 or newer.
- **Speed limits and banners on a paired device's list.** Set a download's speed limits and its banner (reposition, choose an image, find one again). The phone can set speed limits and find a banner again for another device too.
- **Download later works for another device.** Download later and the Queue picker work when the download goes to a paired device, and sends to an offline device are kept, even after a restart, and delivered once it comes online. An older FluxDM is refused clearly.
- **Choose a destination and finish action from your phone** on a paired device.
- **Reposition a download's picture** from More > Banner, and it follows the desktop, phone and linked-device lists.

### Phone
- A torrent's Files section is a folder tree with closed folders, a search box and All / None, so torrents with thousands of files stay smooth.
- The phone gets the torrent engine fixes above, and its messages for other devices are in Arabic too.

## 3.5.9 — 2026-11-17

- **Phone browser: address bar and tabs at the top.** Normal and private tabs now show the address, the tab count and the menu at the top of the screen, with the status bar in the toolbar's colour.

- **Bundled phone video engine integration.** Android gets video quality, M4A audio, playlist selection and keyframe clip controls, plus subtitle and built-in browser cookie settings. CPython, yt-dlp and QuickJS are packaged in the APK; Android MediaMuxer joins streams without ffmpeg. Tested on a real phone: YouTube videos, Shorts and channels/playlists at full quality, audio only (saved as a standard M4A), clips, Instagram reels (with sound), TikTok and public Facebook videos. The Add screen shows the video's thumbnail as a banner on the phone and as the card picture on the PC. The APK grows from about 15 MB to about 30 MB.

- **Phone settings catch up with the PC.** Speed schedule rules can be moved up and down to change which is checked first. Torrents get a random listening port button, the maximum connections per torrent and an IPv4-only switch. Appearance offers the ready-made looks (Full heat, Midnight, Neon, Forest, Mono). Tapping a day in the 30-day statistics chart shows how much was downloaded that day.
- **Phone: the Browse sheet follows the text size** chosen in Settings.

- **Phone: what the other device answered is shown in full** when sending a link with a folder or finish action (refused folder, older FluxDM).
- **The phone app can open another paired device's downloads and queues.** A device switcher above the filters shows This phone and each paired device with its online state. Choosing one shows its live list with the usual cards, a Retry note when the link drops, and the allowed actions only (resume, pause, restart, copy link, When it finishes, Move to queue). The Queues tab shows and edits that device's queues. Every action reports the device's real answer; an older device says it needs 3.5.8. Switching back restores your own list, filter, search and scroll.

- **Files received from paired devices appear in your list.** Each received folder has one completed row showing its size and sender.

- **Downloads wait when a Windows drive disappears.** FluxDM pauses downloads using that drive, keeps their partial files and progress, and names the drive and affected folder. It resumes them when the original volume returns. A different disk using the same letter is blocked; if the original disk returns under another letter, FluxDM asks you to move the download or change its folder. Pausing a download yourself cancels automatic resume.
- **Choose a save folder on a paired device.** The Add window can browse the other device's available drives and folders, including USB drives, and send a chosen destination with the download.

- **Add window lines up when sending to another device.** Choosing another device under Download on pushed rows one column over. Settings that only apply to this PC (Save to, free space, queue, connections, speed limits, Download later) are now hidden for another device, so the window shows only the device, the file name and what to do when done.

- **The real file name always shows under a download's title.** It was hidden when the title matched the file name without its extension (Deck over Deck.apk), so some downloads showed only "Deck" and others showed the full file name.

- **Another device's queues open from the side bar.** The extra Queues chip next to the device chips looked like a fourth device and is gone. While you view another device's list, the side bar's Queues reads "Queues · <device>" and opens that device's queues; back on This PC it opens your own. The side bar shows it as Queues with the device name on a small line under it (a dot on the icon when the side bar is collapsed).

- **A download's finish action really runs.** Restart, Shut down, Sleep and the others set on a single download were always skipped when it finished, because FluxDM counted that same download as "still running". The countdown now starts as intended, and the action is still skipped when other downloads are running or waiting.

- **A device that closes turns grey within about 15 seconds.** Its dot above the list stayed green for up to 2 minutes after FluxDM closed there (for example while it was installing an update).

- **Pick a finish action while adding.** The Add window has "When done" next to Open it when finished: Do nothing, Sleep, Hibernate, Shut down, Restart or Exit FluxDM (a phone offers Close FluxDM). It works for this device and when sending to another device, runs once with the usual 60-second countdown on the device that downloads it, and the result says whether it was set there.

- **Countdown notification reads cleanly:** "FluxDM will exit in 55 seconds" instead of "55  s" with a wide gap.

- **Programs from GitHub get their picture in seconds.** A download from a GitHub release now takes its project's own logo and banner first instead of searching game stores and Wikipedia for ~20 s; names that look like games still try Steam first.

- **Notifications close when you click them.** A notification could stay on screen and ignore clicks and its x for up to 25 seconds when a new one arrived at the same moment. Clicking the card or its x now always closes it.

- **Games holds games.** PS5 homebrew (title IDs PPSA99xxx, like vkQuake or Doom ports), program installers a Wikipedia search tied to an article (YouTube Music), and generic names matched to a Steam game (Payload.zip) no longer land in Games; wrong Steam matches from generic names are looked up again.

## 3.5.8 — 2026-11-17

- **A finish action for a single download.** Right-click a download, choose When it finishes, and pick Sleep, Hibernate, Shut down, Restart or Exit FluxDM (the phone offers Close FluxDM). It happens once, with the usual countdown you can cancel, and is skipped with a message if other downloads are still running or waiting. If the download fails or is removed, the action is dropped.
- **Control another device's queues from this PC.** Open a paired device's list and press Queues to edit its queues with the same editor as your own: rename, create or delete them, start or stop them, change how many run at once, the speed limit, retries, the schedule, the finish action, and on a phone the Wi-Fi, charging and battery rules. You can also add its downloads to a queue, take them out, and set a finish action on them. The countdown runs on that device and can be cancelled there; your other paired devices are told when it starts or is skipped. A phone only accepts Do nothing or Close FluxDM, and every action reports the device's real answer. A device on an older version says it needs 3.5.8.

## 3.5.7 — 2026-11-17

- **FluxDM comes back after an update on slower PCs.** Pressing Install closed FluxDM and, on some PCs, it never reopened: the new version started while the old one was still pausing its downloads, handed itself over to it and quit. The new version now waits until the old one has really closed. This takes effect from this update on.

## 3.5.6 — 2026-11-16

- **Every category stays visible on laptops.** On a shorter window or a laptop at 125-150% display scale, the side bar's rows share the height the window really has instead of hiding Documents, Music, Images and Other below a scroll with no visible bar. On any window size the rows grow to use the space under the last category, so the bar doesn't end in an empty gap.

## 3.5.5 — 2026-11-16

- **Devices explains why your other devices can't reach this PC.** When devices are paired, none of them has reached this PC for 10 minutes, and Windows treats your real Wi-Fi or Ethernet network as Public (FluxDM's firewall rules are for Private networks only), Devices shows one quiet note naming the network with a Make it Private button. If FluxDM's firewall rule points at an old copy of the app, the note offers Fix it instead. Each needs one Windows prompt and tells you exactly what happened (cancelled, refused by policy, timed out, or done). Dismiss silences it for that network. Nothing shows when everything works. Fix it no longer removes the rules of another FluxDM copy, and a cellular (mobile broadband) connection is never offered as the network to change.
- **The "Lost the link" message now says why**, for example the address tried or "not paired", and the reason is written to the error log.

## 3.5.4 — 2026-11-16

- **Approve browser extensions once in FluxDM.** The first connection shows the full extension origin with Approve and Deny. Approval is saved for that exact origin, including Firefox's per-install address. Unknown extensions are refused, and repeated requests cannot flood approval prompts. Retry the browser download after approving.
- **Browser extension approval is harder to abuse and can be undone.** A repeat request no longer pulls FluxDM to the front, an unanswered request expires after two minutes, and Settings → Browser extension lists approved extensions with a Remove button. The extension now says "Approve this browser in FluxDM, then retry" instead of "FluxDM unreachable". Only genuine Chrome (32 letters a-p) and Firefox (UUID) extension ids are accepted.
- **Extension and pairing prompts are harder to spam.** Only the Deny button remembers a denial (Escape or the X just closes the box), and it lasts 10 minutes; Settings lists denied extensions with Allow again. A request that expired closes its dialog, and Approve on a stale one says "This request expired. Retry the download in your browser." Only one prompt per 10 minutes pulls FluxDM to the front; later ones just flash the taskbar. At most two strangers can hold a pairing prompt at once, and a device address only counts as paired after a real authenticated connection, not from a broadcast.

- **Device pairing keeps its full two minutes** to compare the code and press Pair, while a stranger that sends half a hello is dropped after 15 seconds and can no longer crowd paired devices out.

- **Interrupted torrent and playlist saves can finish on Retry.** Partial copies no longer block later attempts. A move that never started keeps a finished torrent Completed at its original location and reports that the move did not happen. Keeping files after Remove also preserves torrent data if finishing fails. Long saves no longer hold up unrelated downloads, and Reset cannot race Retry.


- **Android browser: the menu sheet always leaves a dimmed strip above it to tap and close it.** In portrait the sheet stops at about 78% of the screen height and scrolls inside.

- **Changing an unrelated setting no longer fails when the default save folder is on a drive that is not connected.** The default folder only has to be creatable when you change it; downloads into a missing folder still report their own error.
- **Android browser: new look, laid out like Firefox for Android.** The toolbar is at the bottom, where your thumb is: a rounded address pill (lock, the site's name, and reload / stop inside it; tap it to see and edit the full address), then the tab counter and the menu button, with a thin progress line on top. The menu is a bottom sheet with quick actions (Back, Forward, Reload, Bookmark) over grouped rows with icons, including Find in page and Share. The tab counter opens a tab tray with a Normal | Private switch, tabs as cards (swipe a card sideways to close it, Close all in the small menu) and a New tab button. The start page matches, with cards for Most visited and Bookmarks and links to History and Downloads (the address bar at the bottom is the only search field). Everything is in Arabic and mirrors right to left.
- **Android browser: Settings.** Menu > Settings has the search engine (DuckDuckGo, Google or Bing), Clear history and Clear cookies and site data (each says what it really cleared), desktop site by default for new tabs, JavaScript, blocking pop-ups, page text size, and the WebView version. A private tab follows these but cannot change them.

- **Android browser: Desktop site.** The browser's menu has a checkable "Desktop site" entry (normal and private) that switches the current tab to a Chrome-for-Windows identity and a wide zoomable page, then reloads; switching back restores the mobile identity. It is per tab (new tabs start mobile), remembered with your saved tabs (a private tab saves nothing), and downloads send the same identity the page used.
- **Android private tabs are more private, and say honestly what a download keeps.** A download you start in a private tab goes to FluxDM with its link and the site's sign-in for as long as it downloads: FluxDM keeps that sign-in in memory only (never in its saved list or sent to another device) and drops it when the download finishes, fails for good or is removed. It stays in FluxDM's list until you remove it, and the private note now says so. Also: private data left by a crashed or killed session is cleared at the next start, rotating the phone or changing the font no longer ends the private session, the private browser's menu, dialogs and the page's own alert boxes are kept out of screenshots, the keyboard is asked not to learn from private typing, and the browser's own start-page links can no longer be triggered by a web page.
- **Android browser: bookmarks are safer to save.** A failed save now says so instead of showing "Bookmarked", an unreadable bookmarks file is set aside and never replaced by the old list, folder rename/delete/move report a missing folder, and a private tab can only read bookmarks.

- **Android: private tabs in the FluxDM browser.** Browse tab > Open a private tab, the browser's menu > New private tab, or long press a bookmark > Open in private tab. A private tab has a purple toolbar and a Private badge, keeps no history, bookmarks, saved tabs, cookies, sign-ins or form data, does not show in Recent apps (and cannot be screenshotted), and everything is erased when you close the last private tab. A download from a private tab still goes to FluxDM, with the private session's cookies and without the page address, and stays there.
- **Android browser: bookmark folders.** Create, rename and delete folders in the Browse tab; long press a bookmark for Open, Open in private tab, Move to folder and Delete (Undo is offered). Your existing bookmarks are kept in the default Bookmarks folder.
- **Android browser: a start page for new tabs** with your most visited sites and bookmark shortcuts, a searchable history with Clear all, and a Downloads list of what the browser sent to FluxDM. The new screens and buttons are in Arabic too.
- **Android browser: landscape fixes.** The empty "Pick a download to see its details" panel no longer covers the Browse tab buttons, a new tab no longer opens the keyboard, and the address field never uses the full-screen keyboard in landscape and stays above the keyboard. The duplicate search field on the start page is gone.
- **Android browser: follows the app's theme.** It uses the app's accent colour and one of five backgrounds (navy, black, graphite, purple, forest) from the settings, falls back to the defaults when those are missing or invalid, and rebuilds when you return after changing the theme. Private tabs keep their purple look and never read the settings file.
- **Videos and torrents finish safely after a crash.** FluxDM records every output before putting it in place and checks the saved files on restart. Playlists keep their installed and unfinished files together in one recovery record; a partial save offers Retry finishing, Keep files and reset, and Remove. Conflicting files are preserved, and a video is not marked finished while an output is missing. Subtitles and other video sidecars are saved with the video. Resume can finish saving staged media even if yt-dlp already recorded it in the download archive; subtitles or unmerged streams alone cannot count as a finished video.
- **Torrent Pause answers within seconds on a slow or stuck drive.** The download keeps ownership of its files until disk work drains, so Resume, moving and rechecking cannot race it. Remove waits visibly for that work to finish. Torrent moves use the same crash recovery as finishing, and selected-file torrents retain the boundary data needed for sharing.
- **Validation of the combined 3.5.4 work (Windows, 2026-11-15):** Rust tests: 524 passed, 0 failed, 10 ignored; desktop UI: 189 passed, 0 failed; phone UI: 927 passed, 0 failed. The Rust library type-checks for Android and the Kotlin code compiles; the browser was checked on an Android 14 emulator (landscape, portrait, Arabic, theme change). Nothing has been run on a real phone, and no live video or torrent download was tested. Further testing limits are recorded in `PROJECT_STATE.md`.
- **A download that cannot be put in place is never stuck.** The save folder is created before the finished file is moved, so a new or deleted folder no longer ends in an error. If FluxDM is closed or crashes while finishing, the item comes back Paused with the unfinished file kept. An item that needs attention now has "Retry finishing" and "Keep files and reset" in its menu (PC and phone), and Remove drops it from the list while leaving every file. The installed file is flushed to disk right after the final rename on Windows. For a single HTTP file, "Keep files and reset" is not offered once the file is installed (only Retry finishing, which can complete it), and Remove on a stuck item tells you exactly which source, temp and destination files were kept.
- **PC: large download lists open and update much faster.** Only downloads near the visible area are drawn; selection, keyboard navigation and grouped headings still work across the whole list.
- **PC: the download list keeps your place as it changes.** Rows with wrapped tags or extra details keep their own heights, adding or removing downloads above the viewport no longer jumps to another download, and Enter/Space still work after the focused download scrolls offscreen.
- **Phone: the "System" language follows Android's language for FluxDM.** Choosing Arabic for FluxDM in the phone's app-language settings (or as the phone's language) now shows FluxDM in Arabic, right to left; changing it while FluxDM is open switches the page at once.
- **A torrent is only marked Completed once its data is safely written to disk.** If the final save fails (a stuck or failing drive), the card shows a plain error and FluxDM tries again instead of reporting a finished download that could lose its progress after a power cut. A save that failed while pausing is also retried when you resume.

- **Range-capable HTTP servers get a final size check.** If a server serves bytes beyond the size it advertised, FluxDM keeps the unfinished file and explains the size mismatch instead of publishing a truncated download. A file that was replaced on the server after you downloaded it is not mistaken for this, and the check waits at most 10 seconds.

- **Pause and Remove answer within seconds even while a finished file is being put in place on a slow or stuck drive.** The card says "Finishing… (the drive is slow)"; a Remove at that moment shows "Removing when finished" and is done as soon as the file is in place. Resume, Restart, Move and similar actions wait until then, and a download you removed no longer announces that it finished or failed.
- **PC: the link box in the Add window keeps the whole link readable.** A long link no longer slides under the link icon when you move to its start, and the playlist range and torrent Watched folder boxes no longer cut their hints off at small window sizes.
- **More download checks before each release:** automatic tests now compare finished files byte for byte after pauses, stalled connections, redirects and expired links.
- **Android: changing the font size, display size or language direction no longer restarts FluxDM's screen** (that could stop the download engine); the page adapts in place.
- **Android: downloads keep full speed with the screen off** (FluxDM keeps Wi-Fi awake while downloading), and the CPU wake lock can no longer stay on forever if something gets stuck.
- **Long file names are shortened safely on Windows and Android.** Names in Arabic, Chinese or with emoji no longer fail on phones and SD cards, and the file type (.zip, .pdf…) is kept when a long name is shortened.
- **PC: a removed drive or disconnected network folder says so** ("The drive or network folder is not available…") and can be retried, instead of showing a raw Windows error.
- **HTTP downloads can recover if FluxDM stops while putting a finished file in place.** After restarting, FluxDM checks the saved file before marking it complete. If a drive is missing or the files cannot be identified safely, it keeps them and shows the paths needing attention. Existing files are kept unless you chose Overwrite.
- **Remove requests made while an HTTP download is finishing survive a restart once saved.** If FluxDM stops before the request reaches disk, you may need to repeat Remove.
- **FluxDM's own list and settings are saved more safely.** A crash or power cut while saving can no longer damage both the list and its backup, and a save that fails is reported instead of being silently lost; a file briefly held by antivirus is retried.
- **Torrent downloads are now checked byte for byte by automatic tests** (single and multi-file torrents, pause and resume, recovery after a crash).
- **Torrents never claim data that is not on the disk yet.** A torrent's saved progress is only updated after its data has been written to the drive, so a power cut, a crash or a pulled drive can at worst make it check some pieces again; it can no longer finish with damaged parts. A slow or stuck drive can no longer pile up saves until the whole app freezes, and idle torrents no longer write to the drive every minute.
- **Safer device link:** a device on your network can no longer flood FluxDM's link port or pop up pairing requests over and over, and files received from your other devices can never overwrite an existing file or be redirected through a folder shortcut.
- **Browser extensions must be approved in FluxDM** before they can connect or start a download; approval is remembered for each exact origin.


- **Android: save to an SD card or a USB drive.** The folder picker (Settings > Downloads > Save to, and "Save to" on the Add page) has a new top level, "Storage", listing the phone's storage, the SD card and any plugged-in USB drive with their free space. FluxDM tests that it can really write to a card or drive before accepting a folder on it, and says so when the phone doesn't allow it or the drive is read only. Folders show as "SD card/Movies" instead of a raw path, and the "Save to" rows show the whole folder on its own line (it was cut short). If the card or drive is taken out, the Add page warns before you start. A refused write says "The phone denied access to the save folder" (it said "Windows").
- **Android: pulling out the SD card or USB drive no longer closes FluxDM.** Android stops any app that keeps a file open on a drive being removed. FluxDM now lets go at once: downloads on the card or drive stop with "The SD card or USB drive was removed. Put it back and press Retry.", what they had downloaded is kept, and downloads on the phone's own storage carry on. A queue that starts on a schedule leaves those downloads alone until the drive is back. With two removable drives plugged in, pulling one stops the downloads on both; press Retry on the ones whose drive is still there.
- **A pulled drive or a power cut can no longer leave a hidden gap in a download.** FluxDM only remembers progress that has really reached the disk, so Retry continues from data that is there instead of leaving a gap of empty data in the finished file. Pause still answers within seconds if the drive hangs. This includes SD cards and USB drives, where the drive's own record of the file is saved too.
- **Android: a torrent on a pulled SD card or USB drive checks all of its data again on Retry.** Pieces written just before the drive was pulled may never have reached it; checking everything makes sure a finished torrent has no damaged parts.
- **Android: finished downloads are put in place at once.** A download finishing on the same drive was copied in full to its final name (minutes for a large file, and twice the space meanwhile); it is now renamed. Any copy that is needed is checked to be complete before the unfinished file is removed.
- **Less is downloaded again after Pause or a pulled drive.** Downloads save their progress to the drive every few seconds without slowing down, and pressing Pause saves the latest progress first.
- **Large downloads and torrents on SD cards and USB drives start reliably.** The card shows "Reserving space" and a percentage. Pause and Remove respond within seconds while space is reserved or a torrent's files are being checked, and removing several downloads no longer waits for a busy one.
- **A download paused while reserving space keeps its place.** The card says "Paused · space reserved N%" instead of "Paused · 0%", and Resume carries on from there.
- **A slow or stuck drive no longer freezes the app.** FluxDM keeps working while a drive is slow: other downloads keep going, and Pause answers within seconds. A download paused just as it finished is no longer left unmarked.
- **A slow or stuck drive no longer freezes the folder picker or free-space line.** After a few seconds they say the drive is busy (or that a new folder may still appear) instead of hanging; other drives keep working. Disk-space warnings no longer use old numbers.
- **Remove answers at once, even on a stuck drive.** Removing a download takes the card away immediately; it no longer waits for the download list to be saved, for the leftover part file to be deleted, or for a finished file to go to the bin.
- **Android: replacing a file is safe.** When a finished download replaces an existing file, the old file stays whole until the new one is complete, so pulling the drive mid-copy no longer leaves you with neither.
- **Files sent from your other PCs or phone no longer wait on a slow or stuck drive** while their name is checked, and two transfers into the same folder never pick the same name.
- **The Save to row names the drive again after it is plugged back in** (it showed /storage/… until the folder picker was opened).
- **Moving a torrent works while it is checking its files or after it stopped on an error.** *Move to folder* (and adding trackers to a running torrent) used to fail with an error in these cases, and adding trackers could leave the torrent paused. The torrent now moves and is checked again in the new folder.
- **The upload limit box only sets the limit while downloading.** The box in the status bar (and the phone's Speed limits) used to overwrite the separate limit for finished torrents as well. That one now stays as you set it in Settings > Torrents.
- **"Restart FluxDM to apply":** after saving a torrent setting that only applies on the next start (µTP, connections per torrent, DHT, local discovery, IPv4 only, the blocklist, the listening port, UPnP, or the proxy when torrents use it (SOCKS5)), FluxDM now says so and names what changed.
- **One clear Remove, on PC and phone.** On the PC the toolbar, the menu and the dialog all say "Remove". One dialog asks, with an "Also delete the downloaded file(s)" box for finished downloads and a warning about partial data for unfinished ones. On the phone, taking a download off the list is called "Remove" everywhere (it was "Delete" in places), and queues say "Remove from the queue".
- **Game banners without the blank colour block.** Some Steam banners come with a flat colour panel on one side (for example Need for Speed Heat), in the big banner and on the download's card. FluxDM now cuts that panel off, but only when it is really empty: a panel with a logo or text on it stays. If a store changes a game's banner, the cut copy is made again. Trimmed PlayStation and GOG banners are no longer thrown away on the next check. Downloads you already have get the fixed banner by themselves.
- **The selected download no longer flashes.** In the card view, the selected card could blink black at random while it was downloading. Its picture is now kept in place when the card updates.
- **Keyboard and screen readers:** the PC download list can be reached with Tab and walked with the arrow keys, with a visible focus outline. In the table view, Tab to a column heading and press Enter or Space to sort by it. Menus, and the phone's bookmark and queue rows, are announced as menus and buttons. An open menu or dropdown takes the keyboard focus, so the highlighted row is read out, and focus goes back to where it was when the menu closes. Home and End jump to the first and last row of a menu. In Settings, Enter on a folded group opens it, Tab no longer skips a folded group, and Enter with a dropdown open picks the row and no longer saves and closes the window. On the phone with a keyboard, Enter or Space opens a submenu row.
- **Easier to read:** no text on the PC is tiny any more (counts in the side rail, day headings, card details, detail chips, menu headings). Menu headings are also easier to read over bright art.
- **The download limit box no longer cuts off "Unlimited"** in the smallest window.
- **Video downloads are easier to find:** the Add window's option now reads "Download as a video or audio file (YouTube and other video sites)". Its "Part" and playlist number boxes also shrink with a narrow window, and the Add window no longer cuts off its buttons at its smallest size.
- **Clearer settings:** plain hints for "Manual downloads at the same time", "Retries per connection", "Reconnect a stalled connection after", the Discord daily time and the global speed limit. The seeding hints now say what 0 means (ratio 0 = don't seed; time 0 = no time limit). "Show the tour again" moved from Updates to Behaviour. Appearance says that Save keeps the changes and Cancel undoes them.
- **Tidier settings:** in Appearance, the six art strength and blur controls sit under "More art options", and the list picture switch has its own row. In Torrents, the expert options (µTP, connections per torrent, DHT, local discovery, IPv4 only, blocklist, .!fx marking) sit under "Advanced torrent options". Searching Settings still finds them and opens the group.
- **Tour fixes:** the phone step now points at Devices (it showed the Speed schedule page), the last step names the right place for "Show the tour again" (Settings > Behaviour), the first step shows only Skip tour and Start, and the Updates page no longer shows an empty bar under Check now. In the Add window, a long link no longer starts under the link icon.
- **The Refresh link hint shows for downloads that failed with error 403 or 410** (the hint never appeared before).
- **Android in Arabic everywhere:** the notifications (including "Waiting for Wi-Fi", "Waiting for the charger" and the battery message), the quick settings tile and the built-in browser now follow the language chosen in FluxDM (they were English only), with a right-to-left layout.
- **Phone: failed downloads show a Retry button and the whole reason.** A failed download's card has a Retry button. The reason was cut short ("The SD…") because it shared a row with the size and the Retry button; it now has its own line under the progress bar, up to two lines.
- **Phone: choose a .torrent file.** The Add page has a "Choose .torrent file" button next to Paste. It opens Android's file picker and adds the torrent you pick; a file that is not a torrent is refused with a message. The Add page also says how to add a .torrent file (open it from the Files app or a browser and choose FluxDM), which still works, and so do magnet links.
- **Phone: Interface size.** Settings > Appearance > Interface size makes everything smaller or larger (70% to 110%), so more downloads fit on the screen.
- **Phone, landscape and tablets: drag the border between the list and the details.** Pull the line between the download list and the open download to make either side wider. Double-tap it to go back to the usual width. FluxDM remembers the width. On screens too small for it, the border stays fixed. The open download's header also no longer shows through Settings and other full pages.
- **Phone, large text:** with Android's font size turned up, the bottom bar, menus, chips and buttons grow with the text and no longer cut it off. The page makes room when the bottom bar gets taller.
- **Phone, selecting:** on narrow phones "Select all" moves into the More menu, so the count ("12 selected") is no longer cut short.
- **Phone, easier to tap:** filter chips, small buttons, the speed boxes and the queue drag handle have bigger tap targets. They look the same.
- **Phone settings:** "Wi-Fi only" moved to Downloads. Torrent and proxy settings have one-line explanations. The Discord test result shows right under its button, and the Discord settings fold into one row when Discord is off. "Left out on Android" is a plain list.
- **Phone: safer deleting.** Deleting a speed rule asks first, and removing a bookmark shows Undo.
- **Phone polish:** animations are off when Android's "Remove animations" is on, and sheets keep clear of the screen's curved or notched sides in landscape.

## 3.5.2 — 2026-11-12

- **Torrents download again.** Since 3.4.0 a new or resumed torrent could stay at 0 peers and 0% forever ("Downloading" with no trackers, DHT or peers), on the PC and on Android. The torrent engine dropped its peer sources when a torrent was started while it was still checking its files, which FluxDM does every time. Torrents now find peers within seconds.
- **Moving a downloading torrent works again.** After *Move to folder* (or the Move… button), the torrent restarted in the new folder with no peers and never continued. It now carries on downloading there.
- **Game icons use the PC art first.** A game found on Steam gets its icon from Steam's own cover, not a console store's box art (Portal 2 showed its Xbox 360 cover). Games Steam doesn't have now try GOG's cover first, then the PlayStation and Microsoft stores. Downloads already in your list get their icon redone once.

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

