# UPSTREAM — F1

## Identification

- **Game ID:** `f1`
- **Upstream repository:** https://github.com/kuba--/f1
- **Author / owner:** `kuba--`
- **Repository visibility:** Public
- **Fork date:** 2026-07-11
- **Upstream commit:** `T1d7a7870293f6b72524b6d1e01b961474e1d9b06`
- **Original release observed:** `f1 0.1.1`, published 2024-01-23

## Description and runtime

- **Description:** Simple car racing game.
- **Engine:** Godot 3.5.
- **Primary language:** GDScript.
- **Original web demonstration:** https://kuba--.github.io/f1/
- **Verified by project owner during initial review:** the existing web demo runs correctly in a current browser.
- **Original graphics API stated by upstream:** WebGL 1.0.
- **Other stated target:** Android / OpenGL ES 3.0.

## Multiplayer status

The upstream README labels multiplayer as **“In development”**. This must not be represented as existing local multiplayer. The initial platform fork must therefore treat the game as a **single-player racing base requiring a local 2–4 player adaptation**, unless source inspection demonstrates otherwise.

## Licensing

### Code

- **Upstream declaration:** Unlicense.
- **Interpretation:** permissive dedication for the repository code, subject to retaining the upstream notice and documenting the fork.

### Third-party content — not cleared for redistribution yet

The upstream README credits several external sources but does not identify the exact files nor include their individual licence records:

| Category | Upstream attribution | Audit state | Required action |
|---|---|---|---|
| 3D game assets / materials | Kenney | Source family is generally well documented, but each imported pack/file must be matched to its licence | Inventory files and record source pack + licence per asset group |
| UI icons and buttons | Flaticon | **Blocked**: Flaticon assets may require attribution and can have usage restrictions depending on asset/licence | Identify every icon; replace with self-made, Kenney, Lucide, or other explicitly compatible assets if uncertain |
| Sound effects / music | Pixabay | **Blocked pending asset-by-asset audit** | Identify original URLs, authors and licence terms; preferably replace all audio with traceable sources |
| Main music | “Slow Rain”, Alejandro Magaña, via a royalty-free music channel | **Blocked**: provenance and reuse rights are insufficiently documented | Remove/replace before any distribution |
| F1 logo and fonts | Formula One Licensing BV trademarks | **Incompatible** with a distributable fork | Remove all Formula 1 names, logo marks, trade dress and associated fonts; rename the game and redesign the branding |

## Known fork modifications

- `TODO — add changes as they are made.`

## Local build / Web export

```text
TODO — record exact Godot 3.5.x version after opening the project.
TODO — record import/build commands.
TODO — record local web export preset, output size and server command.
```

## Attribution and notices

- Preserve the upstream Unlicense text in `LICENSE`.
- Preserve this file and add the exact pinned upstream commit.
- Create a final `NOTICE.md` only after the third-party asset inventory is complete.
- Do not ship the current upstream visual identity or audio until every item is cleared or replaced.
