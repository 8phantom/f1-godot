# AUDIT — F1

**Audit status:** Conditional technical candidate; **not eligible for distribution in its current asset/branding state**.

## Executive decision

F1 is a strong **Godot Web compatibility probe** because its published WebGL demo runs in a modern browser. It is not yet a validated catalogue game: the upstream project describes multiplayer as in development, and its present branding, UI provenance and audio provenance prevent a clean redistribution without replacement work.

## Evidence register

| Claim | Evidence | Confidence |
|---|---|---|
| The project uses Godot 3.5 | Upstream README | High |
| A WebGL 1.0 browser demo is published | Upstream README; manually tested by platform owner | High |
| Repository code is Unlicense | Repository licence declaration | High |
| Multiplayer exists as a finished feature | README says “In development” | Negative / not demonstrated |
| Kenney assets are used | Upstream README | High, but exact files unknown |
| Flaticon UI assets are used | Upstream README | High |
| Pixabay audio and third-party music are used | Upstream README | High |
| F1 branding/fonts are third-party trademarks | Upstream README | High |

| Élément	| Constat |
| Point d'input humain |	race_car.gd, fonctions _get_action_steering_angle() et _input_process() |
| Mécanisme actuel |	Actions Godot globales ui_left/right/up/down, aucune notion de device ou playerId |
| Distinction joueur/IA |	Une seule voiture humaine par partie, sélectionnée via Global.my_race_car_idx dans circuit.gd |
| Slots disponibles	| 4 positions fixes ($P1-$P4) déjà présentes dans les scènes de circuit |
| Mode multijoueur UI |	Placeholder non implémenté (print_debug("MULTIPLAYER not implemented, yet")) |
| Verdict |	Isolation nécessite une réécriture ciblée du point d'input, pas une simple activation de fonctionnalité existante |

## Technical fit

| Criterion | Status | Notes |
|---|---|---|
| Web target | **Pass, preliminary** | Existing browser demo is a meaningful proof. Rebuild locally and test iframe loading. |
| Godot runtime | **Pass, preliminary** | Godot 3.5 is older but still appropriate for a compatibility spike. |
| Build reproducibility | **Unknown** | Open in the exact Godot 3.5.x version and export locally. |
| Local-first operation | **Unknown** | Confirm that no external network/API requests are required after local export. |
| 2–4 local players | **Fail / not implemented** | Multiplayer is listed as in development upstream. |
| Platform input API | **Unknown** | Locate vehicle input polling and replace it with player-scoped actions. |
| Hub state and results | **Unknown** | Identify race start, lap/finish and ranking scripts. |
| `postMessage` integration | **Unproven** | Godot 3 requires a custom JavaScript bridge/export template strategy; validate before committing to this version. |
| Input latency tolerance | **Medium risk** | Racing/drift is continuous input; validate on real iOS Safari and Android Chrome over LAN. |
| Visual quality | **Promising base** | Must be evaluated after removal of Formula 1 trade dress and replacement UI/audio. |

## Legal and editorial blockers

1. **Formula 1 marks and fonts:** remove them completely. Use a new title, wordmark, typeface, vehicle livery and UI language with no likelihood of confusion.
2. **Flaticon UI:** create an inventory or replace every imported icon/button. A generic source attribution is not sufficient for a clean package audit.
3. **Pixabay and channel-sourced audio:** identify source URLs and author conditions for each file; otherwise replace all SFX/music.
4. **Kenney assets:** match actual files to the relevant Kenney packs and include their licence/attribution statement.
5. **No multiplayer claim:** do not list this as 2–4 players in the platform catalogue until a working local implementation exists.

## Spike plan

### Gate 1 — Open and build

- [ ] Record the exact Godot version that opens without scene/script migration.
- [ ] Run the project locally from the editor.
- [ ] Export Web locally, serve it over HTTPS, and measure compressed build size.
- [ ] Load the local build in a sandboxed hub iframe.
- [ ] Inspect DevTools for remote assets, failed requests and browser-console errors.

### Gate 2 — Input seam

- [ ] Locate the vehicle controller script and enumerate current actions: steering, acceleration, braking/reverse, restart/menu.
- [ ] Define `platform_input(player_id, action, pressed_or_value)` at the gameplay boundary.
- [ ] Prove one remote platform action can accelerate/steer a vehicle without `KeyboardEvent` synthesis.
- [ ] Determine whether the steering model accepts digital d-pad input; do not introduce an analogue joystick before mobile playtesting.

### Gate 3 — Multi-car local adaptation

- [ ] Establish whether the existing scene supports multiple vehicle instances.
- [ ] Add stable `playerId` ownership to each vehicle.
- [ ] Test a shared top-down camera or a track layout that keeps all cars readable; avoid inherited split-screen by default.
- [ ] Implement a 2-player proof before attempting 3–4 players.
- [ ] Implement start grid, lap counting, finish trigger and deterministic ranking.

### Gate 4 — Hub contract

- [ ] Receive `platform:init` with player IDs, names and colours.
- [ ] Emit `game:ready` with the selected input profile.
- [ ] Emit `game:state` for waiting, playing, paused and results.
- [ ] Emit `game:score` only if lap/position information is stable and useful.
- [ ] Emit `game:ended` with the final ranking.
- [ ] Handle pause, resume and destroy without lingering audio, timers or inputs.

### Gate 5 — Rights replacement

- [ ] Delete Formula 1 branding and replace it with original branding.
- [ ] Replace or clear every Flaticon-derived UI element.
- [ ] Replace or clear all non-traceable music/SFX.
- [ ] Produce `ASSET_INVENTORY.md` and final `NOTICE.md`.

## Candidate manifest — deliberately incomplete

```json
{
  "id": "f1-racing-prototype",
  "name": "WORKING TITLE — replace upstream F1 branding",
  "version": "0.0.1",
  "status": "experimental",
  "engine": "godot",
  "runtime": "web-wasm",
  "minPlayers": 2,
  "maxPlayers": 4,
  "inputProfile": "dpad-2buttons",
  "capabilities": ["pause", "score", "round-end"],
  "license": {
    "code": "Unlicense",
    "assets": "PENDING_REPLACEMENT_OR_AUDIT",
    "noticePath": "/games/f1-racing-prototype/NOTICE.md"
  }
}
```

The player limits, runtime label and input profile above are platform targets, not statements about the upstream game. They become valid only after the spike gates pass.

## Exit criteria

Retain F1 as the pilot only if all conditions below are met:

- a reproducible local Web export works inside the hub iframe;
- platform-originated input directly controls two independently owned vehicles;
- a short two-player race returns an unambiguous ranking to the hub;
- the game remains enjoyable with phone controls over LAN;
- all Formula 1 marks, unclear UI and unclear audio are removed or documented under compatible terms;
- the rework remains a targeted fork rather than a full replacement of rules, rendering and assets.
