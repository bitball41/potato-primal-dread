# Brotato browser build

Download [`index.html`](https://github.com/bitball41/potato-primal-dread/raw/refs/heads/main/index.html) and open it in a modern desktop browser, or serve it over HTTPS/localhost. Click **Play** after loading. The canvas fills the browser window; the top-right button requests browser fullscreen.

Includes the supplied Brotato 1.2.0.0 content, Primal Dread, and Abyssal Terrors. Uses Godot 3.7 dev1's official single-threaded Web export runtime, matching the supplied game's Godot 3.7 development version family. The native executable identifies itself as a custom 3.7 development build; the Web runtime is not that native custom executable.

The standalone HTML contains its build manifest and fetches every runtime/game dependency from immutable jsDelivr URLs pinned to asset commit `c6abb85825660f426aa791f40135c635cca56701`. No adjacent local assets are needed. Each chunk is at most **19,000,000 bytes**. The loader checks SHA-256 on every chunk and on both assembled files before starting Godot.

WASD/arrow keys move; Esc pauses. Gamepad support remains supplied by Godot/the original game and was not hardware-tested. Audio starts with Play or interaction with the game. Native workshop mod loading and remote announcements are skipped in Web builds.

Saves use browser IndexedDB and the original game checkpoint format/behavior. Use the same browser and origin to continue a run; changing the domain, port, or launch origin creates separate browser storage. Cached chunks are separate from saves. Do not clear site data if you want to retain progress.

See [VERIFICATION.md](VERIFICATION.md) for the actual tested scope and outstanding visual checks. The original game and content retain their original ownership; the Godot engine's license and third-party notices are included separately.
