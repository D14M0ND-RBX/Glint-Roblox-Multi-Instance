# Glint

A small, local-only Roblox launcher with multi-account swapping, one-click join, and optional FPS tools.
Made by Diamond.

**Your accounts never leave your PC.** There is no server, no analytics and no update check. See "Privacy" below.

**It is one file.** `Glint.bat` contains the launcher, the program and the icon. Nothing else is needed.

---

## Quick start

1. Put `Glint.bat` anywhere (a folder of its own is nicest) and **double-click it**.
   - First run: it installs Python (if you don't have it) and one small library. This takes a minute.
2. Click **Configure**, then **Add account (sign in)** and log in on the Roblox page that pops up.
   Repeat for every account you want. They are saved, so you only do this once.
3. Press **Back to launcher** (or Esc). Paste a **game link or private server link** into the box on the launch screen.
4. Pick an account in the list and press **Launch**.

Next time you open it, picking an account and pressing **Launch** is all you need.

## The launch screen

| Control | What it does |
|---|---|
| **Accounts list** | Click an account to pick it. Ctrl/Shift-click to pick several. **Double-click** an account to launch it right away. |
| **Launch** | Joins the saved game/private server with the picked account(s). The button shows who it will launch. |
| **Launch all** | Starts every saved account, one after another. |
| **Configure** | Accounts and all settings. |
| **Game or private server link** | What to join. Shows a green tick when the link is understood. |
| **Allow multiple Roblox instances** | Your choice, see below. |

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
- The only network traffic is to Roblox (sign-in and joining), plus these optional one-time downloads that always ask first: `handle64.exe` (Microsoft) and `PresentMon.exe` (Intel, from GitHub).
- Source is a single readable file: open `Glint.bat` in Notepad - the code is below the launcher part. The embedded icon data is kept at the very bottom.

## Upgrading from Diamond Launcher

Glint is the new name of Diamond Launcher. Your saved accounts and settings carry over automatically (the data folder is still called `DiamondLauncher`, on purpose). Just delete the old `.bat` and use `Glint.bat`. If you made a desktop shortcut before, delete the old "Diamond Launcher" shortcut and press **Desktop shortcut** in Settings again.

## Troubleshooting

**Windows says "Unknown publisher" / SmartScreen warning.**
That text comes from a paid code-signing certificate, which this free tool doesn't have, so Windows can't show a name there. Click *More info -> Run anyway* (only for files you got from someone you trust). Properly showing "Diamond" would need an `.exe` signed with a real certificate.

**The sign-in window doesn't open.** Use **Add by cookie** instead, or install Python 3.12 and Microsoft Edge WebView2.

**Private server doesn't join.** Roblox changes these internal links now and then. Try the share link or the plain game link, and report what the log box in Settings says.

**FPS unlocker says close Roblox.** Close every Roblox window, then press Launch again.

**Nothing changed after FPS boost.** Flags are read when Roblox starts - restart any open Roblox windows.

**Roblox says it is already running / won't open a second window.** Make sure *Allow multiple Roblox instances* is ticked, and if Roblox was already open before this app, close it first. If it still fails, run Glint as administrator.

**The second account doesn't open when I launch quickly.** Raise *Seconds between launches* in Settings (try 10). The first client needs a moment to start before the next one can.

If the app ever crashes, details are saved in `%APPDATA%\DiamondLauncher\crash.log`.

## Optional (advanced): make an .exe with the diamond icon

1. Run `Glint.bat --export-icon` from a command prompt in the folder with the file. Nothing visible happens, but it writes `diamond.ico` next to the file (the icon is stored inside the .bat, so you never need to keep a separate icon file).
2. Copy `Glint.bat` to `Glint.py`.
3. Open it in Notepad and delete everything from the top down to (and including) the line that is just `"""` right above the `# ====` banner. What remains is pure Python.
4. Run:
```
py -m pip install pyinstaller pywebview
pyinstaller --onefile --noconsole --icon diamond.ico --name "Glint" Glint.py
```
An unsigned .exe will still show "Unknown publisher" in Windows.

## Removing it

Untick *FPS boost* and *FPS unlocker* (this restores your settings), press *Wipe all data*, then delete the folder `%APPDATA%\DiamondLauncher` and the `.bat`.

---

Not affiliated with Roblox Corporation. Running several clients at once is not officially supported by Roblox - use at your own risk.
