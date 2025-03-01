# shipbreaker-racers-ledger
A rehosting of [sariya's original racers-ledger plugin](https://web.archive.org/web/20220520234545/https://git.sariya.dev/sariya/racers-ledger#user-content-racers-ledger) for the game [Hardspace: Shipbreaker](https://store.steampowered.com/app/1161580/Hardspace_Shipbreaker/) with permission from sariya.

The `RACErsLedgerRelease.zip` file in the [Releases tab](https://github.com/dnleek/shipbreaker-racers-ledger/releases/tag/Release) is the original plugin release, but with an updated `RACErsLedger.dll` from the user `piepieonline` from the Shipbreaker discord. This new `.dll` is required as of Shipbreaker version 1.2.1. The original `RACErsLedger.dll` is also included in the `.zip` under the name `RACErsLedger.dll.old`.

If you're interested in data visualization, [tashiww's hardspace_viewer](https://github.com/tashiww/hardspace_viewer) is a webpage that scrapes the ledger plugin and visualizes salvage over time and other useful data.

The original plugin's README is as below, with minor modifications (link fixes, etc.). Note that I have not tested anything other than installing this mod on Windows.

# RACErs Ledger
RACErs Ledger -- a mod for Hardspace: Shipbreaker to save salvage data in real time to enable visualization and analysis of salvaging strategies!

It can:

* Save shift summaries (time started, ended, duration, value you salvaged, value you destroyed, probably more in the future!) after every shift!
* Save salvage ledgers (lists of everything you salvaged and destroyed) after every shift!

# Requirements
Hardspace Shipbreaker.

BepInEx: https://github.com/BepInEx/BepInEx/releases (You want the x64 `.zip`.)

This mod (download the `RACErsLedgerRelease.zip` file from the [Releases tab](https://github.com/dnleek/shipbreaker-racers-ledger/releases/tag/Release) of this repo)

## Installation
# Windows
Extract BepInEx to the root Hardspace Shipbreaker folder so `winhttp.dll` is in the same folder as `Shipbreaker.exe`.

Extract the `.zip` you downloaded. Drag the entire `RACErsLedger` plugin folder into `Hardspace Shipbreaker\BepInEx\plugins\RACErsLedger` -- the folder should stay together.

If the `plugins` directory within `Hardspace Shipbreaker\BepInEx` does not yet exist, you can create it or you can run `Shipbreaker.exe` once.

# Linux
Follow the Windows instructions. Afterwards you need to enable the DLL override.

For this either follow [the official instructions of BepInEx](https://docs.bepinex.dev/articles/advanced/proton_wine.html) or do it manually.

In order to manually enable the override open `steamapps/compatdata/1161580/pfx/user.reg` in a text editor and go to section [Software\\Wine\\DllOverrides]. Add a line to it:

```
[Software\\Wine\\DllOverrides]
…
"winhttp"="native,builtin"
```
Afterwards you can start the game as regular.

# Viewing the BepinEx console to see logging info in realtime, if you’re into that
After following Installation instructions (above), run `Shipbreaker.exe` once. You can close it after you get to the main menu.

After this, navigate to `Hardspace Shipbreaker\BepinEx\config\` and edit `BepinEx.cfg`. Under `Logging.Console`, set `Enabled = true`.

Next time you run `Shipbreaker.exe` (directly or through steam), a console window should pop up too.

# Mod configuration
The mod’s config file will be in `Hardspace Shipbreaker\BepInEx\config\dev.sariya.racersledger.cfg` after you’ve run Shipbreaker.exe with RACErsLedger.dll installed properly at least once.

Config options:

| key	| description	| default |
| -------- | ------- | ------- |
| `DataFolder`	| Where to store the CSVs of your salvage summaries |	`HardspaceShipbreaker\RACErsLedger` | 
| `UseLamprey`	| Enable sidecar process for streaming events to interested clients (i.e. live data visualizers) |	true |
| `LampreyListenPort` |	(Advanced users only) What port does the lamprey process listen on?	| 42069 |
| `WebsocketListenPort` |	(Advanced users only) What port does the mod serve a stream of salvage data on? |	32325 |

# Un-installation
BepInEx uses `winhttp.dll` as an injector/loader. Renaming or deleting this file is enough to disable both this mod and the loader.

Or just remove the `RACErsLedger` folder from the plugins folder.

# Support
This mod is provided on an AS-IS basis, with no implied warranty or guarantee that it will work at all. It might fuck up, it might accidentally delete your save, it might destroy spacetime, it might punch you in the face.

It probably won’t do any of those things, since I test every release myself before giving it to anyone else, but it might, and you should be prepared for that harsh reality. Back up your saves, etc.

# Credits
Thank you to Synthlight for making the [Furnace Performance Improvements mod](https://github.com/Synthlight/Hardspace-Shipbreaker-Furnace-Performance-Improvement-Mod) -- I’ve cribbed the structure and README of this mod heavily from them, so thank you Synthlight for helping get me started on this route! Before this I was binary editing the DLLs with dnSpy and that was no fun whatsoever, and hard to source control :-)
