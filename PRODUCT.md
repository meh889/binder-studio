# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

One creator of a Spanish-language (rioplatense) Pokémon TCG YouTube channel who records *master list* videos: every card of one species, shown one by one in a virtual binder, narrated live. Works alone, at a desk, on a large monitor, in Chrome or Edge on a computer. Card data usually arrives already prepared by Claude (from TCGdex) in `binder.json`, and the video plan arrives as `video.json`; inside the app the creator mostly reviews, reorders and corrects cards, crops images, marks zooms, retouches scenes, sets the channel brand, rehearses and records.

## Product Purpose

Binder Studio turns a folder of card scans into a master-list video plan that plays in the browser: intro burst, kinetic title cards, big-card moments with zooms, and a binder filmed on the desk where each card is shown up close, slides into its pocket and gets ticked on the page's checklist (its pocket stays empty when the creator does not own it). Since November 2026 the app no longer records: the creator previews the video full screen (Ver video), Claude renders each scene as a 4K 60 fps clip with its effects track, and the final video is edited in DaVinci Resolve. The team's script and notes live on a separate shared page (`guion.html`, saved to the repo through each person's GitHub token).

## Positioning

The preview is performed: the creator advances the binder card by card while reading the script column, to rehearse and check the pacing. The edit happens later, in DaVinci, with the rendered clips.

## Operating Context

- One folder per species on the creator's computer: `binder.json` (cards and brand), `video.json` (scenes), card images named by card number, `media/` (GIFs, clips, images for bursts and scenes), `musica/`, `_editadas/` (crops made in the app), `videos/` (recordings).
- The creator writes the script with Claude in chat, iterating until approved; Claude then writes `video.json` into the folder and the app picks it up when the tab regains focus.
- Ver video runs full screen: the 16:9 stage on the left, the script column on the right. Keyboard drives it: → / Space / Enter advance, ← back, Z zoom, Esc ends.
- Collections range from a few dozen cards (Bulbasaur Cameos, 47) to several hundred (Bulbasaur, 409), many of them the same art in several languages grouped together.

## Capabilities and Constraints

- Single `index.html`, vanilla HTML/CSS/JS in one IIFE, no build step, deployed on GitHub Pages (`meh889.github.io/binder-studio`). No Node, npm or bundler on the creator's machine.
- Folder read/write uses the File System Access API (Chrome/Edge desktop). Other browsers open a folder read-only and must export `binder.json`.
- Rendering is a 1920×1080 `<canvas>`; music, clips and synthesized sound effects play through Web Audio. 4K clips are rendered frame by frame on a virtual clock (see CLAUDE.md).
- Card editing: per-card fields (set, year, number, series label, rarity, variants, illustrator, language, same-art group, on-screen note, teleprompter script, missing flag), image crop/straighten/brightness editor, up to six zooms per card, drag to reorder, paste from spreadsheet, undo/redo.
- Scene types: ráfaga, portada, cartel cinético (golpe, barrido, máquina, contador), binder (card range), carta en grande, imagen o clip, lista, cierre. Chapters are set per scene in the plan.
- Brand/overlay: theme presets, accent colors, title typeface, logo, channel handle, subscribe button, background image, toggles for what the binder shows.
- All interface copy is Spanish (rioplatense, voseo).

## Brand Commitments

- The recorded video keeps the channel's editing energy documented in `CLAUDE.md` (kinetic type cards in the spirit of Casey Neistat, the Check The Box master-list format of filing every card of a species).
- The video must look filmed, not generated (creator's request, 2026-10-16): a real binder on a dark playmat seen from above, one page in frame with the card's sheet beside it, natural lamp light, a camera that barely moves. The generated-graphics look (purple gradients, glows, tracked monospace labels, grids of squares, synthetic pings) is out.
- Missing cards stay as an empty pocket in the binder, with no red X.
- The creator gave full freedom over the tool's interface and the video's look, as long as every current function keeps working.

## Evidence on Hand

- Real collections: `~/Desktop/Bulbasaur/` (409 cards) and `~/Desktop/Bulbasaur Cameos/` (47 cards), each with `binder.json` and card scans.
- Example plan: `ejemplos/Ponyta/binder.json` and `ejemplos/Ponyta/video.json`.
- The channel brand (Mafia TCG: logo, avatar, banner, stickers) is in `marca/`; the app uses it by default. No music or media files are in the repo.

## Product Principles

1. The stage is the product: whatever the creator edits, the result is visible on the stage at the same time.
2. Review beats data entry: data arrives prepared, so the interface is built to scan hundreds of cards, spot what is missing and fix it fast.
3. The preview is calm: while it plays, nothing can surprise, block or distract; the creator always knows where they are in the video and what comes next.
4. The folder is the source of truth: everything saves back to the species folder automatically and visibly.
