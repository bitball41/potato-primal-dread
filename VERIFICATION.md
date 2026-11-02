# Browser verification — 2026-11-02

## Build

- Supplied native executable: `3.7.dev.custom_build`.
- PCK header: Godot 3.7.0, pack format 1; 12,044 original entries.
- Game: Brotato 1.2.0.0.
- Web engine: official Godot 3.7 dev1, source revision `a117d512b00f1646db174e703e7e888519b64608`, release / single-threaded template.
- All 596 compiled scripts were recoverable for inspection. Gameplay scripts and original imported assets remain supplied bytecode/resources. Browser changes replace configuration, skip desktop crash-log inspection, workshop loader callbacks/log-file writes, and the cross-origin announcement request. A read-only QA autoload reports measurements only with `?qa=1`.
- Desktop game files were not modified.

| File | Bytes | Chunks | SHA-256 |
| --- | ---: | ---: | --- |
| game.pck | 281347063 | 15 | `52b22324abe25142f56557e644e4505ed3e0050023dbf13b66319b2416157498` |
| game.wasm | 20112283 | 2 | `fcb37d18e3bdab7ef845cc580a01ff6b6d5dec4cb75fc20d16db21f1f855bd43` |

Maximum chunk size: 19,000,000 bytes. Asset commit: `c6abb85825660f426aa791f40135c635cca56701`.

## Observed in browser

The local preview initially loaded the main pack directly. The final launcher was then tested at `http://127.0.0.1:8143/Brotato-Primal-Dread.html?qa=1`; its game/runtime bytes came from pinned public jsDelivr URLs, not local game files.

- jsDelivr returned 200, correct JavaScript/binary MIME types, wildcard CORS, and immutable caching for checked pinned files.
- The browser downloaded all 17 chunks and reported exact whole-file hashes matching the table above.
- Original menu, character, weapon, difficulty, gameplay, shop, and pause scenes rendered and responded to input.
- Veteran played through Crash Zone wave one and entered wave two; shop purchases deducted the correct currency and added weapons.
- Archaeologist entered The Jungle (`zone=2`, `dlc_id=primal_dread`) with a whip; moving enemies, combat, and dig sites were observed. Measured active gameplay samples were 59–60 FPS in the first preview.
- The final CDN launcher played Variant in The Jungle through wave one and into wave two. Enemy counts and player positions changed; damage, material pickups, and an evolution value of 1 were observed. Its measured active samples included 30 FPS; background/automation throttling also occurred. No broader late-game performance claim is made.
- Browser AudioContext reported `running`; active game audio bus samples included -18.27 and -17.93 dB in the first preview and -18.05 and -20.91 dB in the final launcher. This verifies active audio generation/output routing; it is not a human listening review.
- WASD movement, keyboard menu confirmation, mouse purchases, Esc pause/resume, and camera movement worked.
- A direct-pack preview restored a run after page reload and displayed Resume, restoring the saved shop checkpoint.
- In the final CDN build, a second SMG cost 23 of 31 materials, leaving 8 materials and two weapons. Starting wave two wrote the native progress/run checkpoint files. The tab was closed and a new tab opened on the same origin. The restarted game logged successful loading of `user://user/save_v3_0.json` and `user://user/run_v3_0.json`.
- The canvas filled the browser viewport. Browser fullscreen requests made through background browser automation returned `not granted`.

## Remaining verification limits

- Browser automation blocked direct `file://` navigation, so opening the downloadable HTML by double-click was not visually tested. The HTTP-origin standalone launcher and its remote dependency path were tested.
- Computer Use subsequently stopped because it could not determine the current Windows browser URL with sufficient confidence. The final visual Resume check for the two-SMG/8-material checkpoint and a foreground fullscreen-button click could not be completed in this turn. Save-file reload itself was observed in browser logs.
- No full 20-wave completion, late-game boss run, controller hardware test, or second-browser/device compatibility claim is made.

## Bare launcher update

The current launcher has an empty initial document title, a gray background, and one gray loading bar. It starts Godot automatically after verification and initialization. The launcher has no visible text or buttons; its canvas still fills the viewport. Audio resumes on the first keyboard/pointer interaction if the browser initially suspends it. Asset pins, game bytes, chunk hashes, and save storage paths are unchanged. The revised entry point passed JavaScript syntax and markup checks; the browser session had already stopped, so this appearance/automatic-start revision was not visually retested. The gameplay observations above describe the preceding entry-point presentation using the same runtime and game assets.
