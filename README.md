# Glint

A small, local-only Roblox launcher with multi-account swapping, one-click join, and optional FPS tools.
Made by Diamond.

**GitHub:** https://github.com/D14M0ND-RBX/roblox-multi-instance  |  **Report a bug:** https://github.com/D14M0ND-RBX/roblox-multi-instance/issues

**Your accounts never leave your PC.** There is no server and no analytics. The only extra thing it does is an optional update check against GitHub (you can turn it off). See "Privacy" below.

**It is one file.** `Glint.bat` contains the launcher, the program and the icon. Nothing else is needed. You can also turn it into a real `Glint.exe` that pins to the taskbar - see "Make Glint.exe" below.

---

## Quick start

1. Put `Glint.bat` anywhere (a folder of its own is nicest) and **double-click it**.
   - First run: it installs Python (if you don't have it) and one small library. This takes a minute.
2. Click **Configure**, then **Add account (sign in)** and log in on the Roblox page that pops up.
   Repeat for every account you want. They are saved, so you only do this once.
3. Press **Back to launcher** (or Esc). Paste a **game link or private server link** into the box on the launch screen.
4. Pick an account in the list and press **Launch**.

Next time you open it, picking an account and pressing **Launch** is all you need.

Want it on your taskbar? Build `Glint.exe` once (see "Make Glint.exe" below), open it, then right-click its taskbar icon and choose **Pin to taskbar**.

## The launch screen

| Control | What it does |
|---|---|
| **Accounts list** | Click an account to pick it. Ctrl/Shift-click to pick several. **Double-click** an account to launch it right away. |
| **Launch** | Joins the saved game/private server with the picked account(s). The button shows who it will launch. |
| **Launch all** | Starts every saved account, one after another. |
| **Configure** | Accounts and all settings. |
| **Game or private server link** | What to join. Shows a green tick when the link is understood. |
| **Allow multiple Roblox instances** | Your choice, see below. |
| **Report a bug** (bottom left) | Opens the bug reporter, see below. |
| **GitHub page** (bottom right) | Opens the project page. |

## Opening several accounts fast (pick, launch, swap, launch)

The launcher **stays open** after you press Launch, so you can keep going:

1. Pick an account and press **Launch** (or just double-click it).
2. The list **automatically moves to the next account**, so the next press of **Launch** is the next account. That is the swap.
3. Press **Launch** again. Repeat as often as you like. Accounts that have been started this session show a green tick.

You never have to wait: if you press Launch again before the previous client has finished starting, the launch is **queued** and runs automatically after a short gap (default 7 seconds, change it in Settings under *Seconds between launches*). The status line under the buttons shows what is happening.

You can also pick a different account yourself at any time. Turn off the automatic move to the next account in Settings if you prefer.

Want the old behaviour where the app closes after launching? Tick **Close this app after launching** in Settings.

## Multiple Roblox instances: your choice

Roblox normally lets only one window run at a time. **Allow multiple Roblox instances** removes that limit.

- It is a checkbox on the launch screen (and in Settings). Both are the same switch.
- **It is off by default on a fresh install.** Tick it when you want several accounts running at once.
- On first use it asks before downloading Microsoft's free `handle64.exe`. If you say no, the box un-ticks itself.
- If it is off and you press **Launch all** (or pick several accounts), the app asks whether to turn it on. Saying no launches just the first account.
- If you used an earlier version, your previous choice is kept.

## Links you can paste

- A normal game link: `https://www.roblox.com/games/123456789/Game-Name`
- Just the place ID: `123456789`
- A private server link: `https://www.roblox.com/games/123456789/Name?privateServerLinkCode=...`
- A share link: `https://www.roblox.com/share?code=...&type=Server`
- A link containing `gameInstanceId=...` joins that exact server.

## Settings (press Configure)

**Accounts** (left side)
- **Add account (sign in)** - opens Roblox's own login page. **Add by cookie** is the fallback if that window can't open.
- **Remove selected**, **Check all** (tests that every saved login still works; expired ones turn red).

**Launching**
- **Allow multiple Roblox instances** - see above.
- **Auto-select the next account after Launch** - the swap behaviour described above. On by default.
- **Close this app after launching** - off by default.
- **Skip the launch screen next time** - the app launches straight into your game with the account(s) you used last. Hold **Shift** while opening to bring the screen back.
- **Check for updates on launch** - on by default. Asks GitHub once per launch whether a newer Glint exists and **always asks you before installing**. Untick it to never check.
- **Seconds between launches** - the gap between two clients starting. Lower is faster, but a slow PC may need more.

**Performance**
- **FPS boost (optimized graphics flags)** - writes Roblox's allowed graphics flags (no grass, lower detail distance, grey sky, lowest render quality). Only flags on Roblox's official allowlist are used. Re-applied on every launch because Roblox updates reset them. Untick to restore your own flags. Works with Bloxstrap installs too.
- **FPS unlocker (uncap FPS)** - sets Roblox's own *Maximum Frame Rate* value (default 9999, you can type another number). It can only be changed while **no Roblox window is open**, so it applies on your next launch from here.
- **FPS tracker overlay** - a draggable box showing real FPS for each Roblox window. Uses Intel's free PresentMon (one-time download, asks first). Windows shows a permission prompt each time it starts. Needs borderless/windowed Roblox to be visible on top. While it is on and the app is set to close after launching (or skips the launch screen), it stays in the background so the overlay keeps updating, and closes itself once Roblox is closed.

**Data**
- **Desktop shortcut** - creates a Glint icon on your desktop.
- **Wipe all data** - deletes every saved account from this PC.

## Privacy

- Accounts are stored in `%APPDATA%\DiamondLauncher\accounts.dat`, encrypted with Windows DPAPI. Only the same Windows user on the same PC can open it - copying the file elsewhere is useless.
- You type your password only on Roblox's own login page, never into this app.
- The only network traffic is to Roblox (sign-in and joining), the optional update check (a read-only request to `api.github.com` for the latest release - nothing about you is sent; switch it off in Settings), plus these optional one-time downloads that always ask first: `handle64.exe` (Microsoft) and `PresentMon.exe` (Intel, from GitHub).
- Source is a single readable file: open `Glint.bat` in Notepad - the code is below the launcher part. The embedded icon data is kept at the very bottom.

## Auto-update (setup for the publisher)

Glint can check your GitHub for a newer version each time it opens, and offer to install it.

**Already set up:** `UPDATE_REPO` in `Glint.bat` points to `D14M0ND-RBX/roblox-multi-instance`. The repository must stay **public** (the updater can't read private ones).

**Releasing a new version**
1. Raise the version in `Glint.bat`: `APP_NAME, APP_VERSION = "Glint", "1.2"`.
2. On GitHub: **Releases -> Draft a new release**. Make the tag `v1.2` (it must be higher than the old one).
3. Attach `Glint.bat`. If you also publish the exe, run `Build-Glint-Exe.bat` and attach `Glint.exe` too. (The attached file names must start with `Glint`.)
4. Write a short description - it is shown to users in the update prompt. Publish.

**What users see:** the next time they open Glint it says "Glint v1.2 is available - update now?". Yes downloads the file, replaces the old one and restarts. No does nothing (it asks again next launch).

**Safety:** it only downloads from github.com, refuses a file that isn't a valid Glint, and keeps the old exe as `Glint.exe.old` until the next start. For extra safety, attach a file named `Glint.bat.sha256` (or `Glint.exe.sha256`) containing the file's SHA-256 hash and the updater will verify it. To make the hash, run `certutil -hashfile Glint.bat SHA256` and paste the long hex line into that file.

## Reporting a bug

Press **Report a bug** (bottom left of the launch screen, or in Settings under *Data*).

1. Write what went wrong at the top (the "What went wrong" part).
2. Press **Copy & open GitHub**. This copies the report and opens a new issue on https://github.com/D14M0ND-RBX/roblox-multi-instance/issues/new
3. Paste it into the issue (Ctrl+V) and submit. You need a free GitHub account.

By default the report contains **no personal or technical details** - only what you type plus the Glint version. If you want to help the developer fix it faster, tick *Also include technical details* to add your Windows version, settings and recent log. Even then, login cookies, private-server codes and your Windows username are removed, and account names become `account#1`, `account#2`...

Nothing is sent by Glint itself - you decide what gets posted. The window also has links to the GitHub page and the issues list.

## Upgrading from Diamond Launcher

Glint is the new name of Diamond Launcher. Your saved accounts and settings carry over automatically (the data folder is still called `DiamondLauncher`, on purpose). Just delete the old `.bat` and use `Glint.bat`. If you made a desktop shortcut before, delete the old "Diamond Launcher" shortcut and press **Desktop shortcut** in Settings again.

## Troubleshooting

**Windows says "Unknown publisher" / SmartScreen warning.**
That text comes from a paid code-signing certificate, which this free tool doesn't have, so Windows can't show a name there. Click *More info -> Run anyway* (only for files you got from someone you trust). Properly showing "Diamond" would need an `.exe` signed with a real certificate.

**Antivirus flags Glint.exe, or it is blocked.**
Unsigned programs built with PyInstaller are often flagged by mistake. If you built it yourself from the readable source in this file, add an exception for `Glint.exe`. Only run exes you built or got from someone you trust.

**No update prompt appears.**
Check the repo is public, the release tag is higher than the current version, and *Check for updates on launch* is ticked. It also stays silent if you have no internet or GitHub is down.

**The sign-in window doesn't open.** Use **Add by cookie** instead, or install Python 3.12 and Microsoft Edge WebView2.

**Private server doesn't join.** Roblox changes these internal links now and then. Try the share link or the plain game link, and report what the log box in Settings says.

**FPS unlocker says close Roblox.** Close every Roblox window, then press Launch again.

**Nothing changed after FPS boost.** Flags are read when Roblox starts - restart any open Roblox windows.

**Roblox says it is already running / won't open a second window.** Make sure *Allow multiple Roblox instances* is ticked, and if Roblox was already open before this app, close it first. If it still fails, run Glint as administrator.

**The second account doesn't open when I launch quickly.** Raise *Seconds between launches* in Settings (try 10). The first client needs a moment to start before the next one can.

If the app ever crashes, details are saved in `%APPDATA%\DiamondLauncher\crash.log`.

Everything shown in the log box is also saved to `%APPDATA%\DiamondLauncher\glint.log`. When that file reaches 1 MB it is cleared automatically and starts fresh, so it never grows big. Every new log starts with a header line showing the Glint version and your Windows username, for example `=== Glint v1.1 | user: YourName ===`. It stays on your PC and is never uploaded.

## Make Glint.exe (pin it to the taskbar)

A real `.exe` can be pinned to the taskbar and Start menu, and people you share it with don't need Python.

1. Put `Build-Glint-Exe.bat` in the **same folder** as `Glint.bat`.
2. Double-click `Build-Glint-Exe.bat`. It installs everything it needs by itself: Python 3.12 (if missing), PyInstaller, pywebview and Microsoft Edge WebView2 (if missing). This takes a few minutes the first time.
3. When it says "Done", `Glint.exe` is in the same folder (with the diamond icon built in).
4. Open `Glint.exe`, right-click its icon on the taskbar and choose **Pin to taskbar**. You can move `Glint.exe` anywhere first (for example a Programs folder) and pin it from there.

Notes:
- The exe is a copy made at build time. If you edit `Glint.bat`, run `Build-Glint-Exe.bat` again.
- Your saved accounts and settings are shared between `Glint.bat` and `Glint.exe` (same data folder).
- The exe starts a little slower than the .bat because it unpacks itself on every launch.
- Because it is unsigned, Windows SmartScreen and some antivirus programs may warn about it. See Troubleshooting.
- `handle64.exe` and `PresentMon.exe` are still downloaded on demand (and only after asking) - they are not inside the exe.

<details>
<summary>Doing it by hand instead</summary>

1. Run `Glint.bat --export-icon` from a command prompt in the folder with the file. It writes `diamond.ico` next to it.
2. Copy `Glint.bat` to `Glint.py`, open it in Notepad and delete everything from the top down to (and including) the line that is just `"""` right above the `# ====` banner.
3. Run:
```
py -m pip install pyinstaller pywebview
pyinstaller --onefile --noconsole --icon diamond.ico --name "Glint" --collect-all webview Glint.py
```
The exe appears in the `dist` folder.
</details>

## Removing it

Untick *FPS boost* and *FPS unlocker* (this restores your settings), press *Wipe all data*, then delete the folder `%APPDATA%\DiamondLauncher`, the `.bat` and `Glint.exe` (unpin it from the taskbar first).

---

Not affiliated with Roblox Corporation. Running several clients at once is not officially supported by Roblox - use at your own risk.
