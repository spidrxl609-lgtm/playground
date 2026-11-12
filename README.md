# ASPHODEL

A browser-based PS1-style third-person horror adventure (prologue, Chapter 1 and the start of Chapter 2).
Everything lives in a single `index.html`; Three.js is loaded from a CDN, and all models and textures are
generated in code.

## Run

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

## Controls

| | Keyboard + mouse | Gamepad | Touch |
| --- | --- | --- | --- |
| Move | WASD | left stick | left stick |
| Look | mouse (click the picture to capture it) or arrow keys | right stick | drag anywhere |
| Sprint | hold Shift | RT / L3 | push the stick fully |
| Interact / advance text | E or Enter | A | ACT button, or tap the marker / text box |
| Swing the plank | J or left click | X | ATK |
| Heavy swing | K or right click | Y | hold ATK |
| Dodge | Space | B | DODGE |
| Inventory | I or Tab | Back | ITEM |
| Flashlight | F | LB | — |
| Pause | Esc | Start | II |

Health is shown as a heart trace (Fine / Caution / Danger) with a stamina bar under it. Bandages, pale
flowers and first aid kits are used from the inventory. Progress is saved at pay phones, at checkpoints and
on every chapter transition (localStorage); dying offers a retry from the last save.

## Extending

`index.html` is split into numbered, commented sections (see the file map at the top of the script):

- **Scenes** — `registerScene(id, { env, build })` returns geometry, walkable rects, colliders,
  interactables, `triggers` (story beats, barks, checkpoints), `monsters`, `pickups` and an optional
  `mirror` plane. `env.lamps` lists street lamps (`steady: true` ones do not flicker).
- **Chapters** — `registerChapter(id, { title, subtitle, scene, spawn, onStart })`. Story beats are async
  functions using the `Script` API: `talk`, `choice`, `cam`, `walkTo`, `pose`, `join`, flags, `attach(n)`
  for the hidden attachment counter, `checkpoint()` and `transition('chapterN')`.
- **Characters** — `CHARACTERS` (Leta, Mnema and the monster bodies); emotes in `POSES`, action clips in
  `CLIPS`.
- **Combat** — `ACT` (Leta's actions), `MON` (monster kinds) and `ITEMS` in section 14b.

`index.html?viewer` opens a model viewer (`&view=front|side`, `&anim=idle|walk|run|light|heavy|dodge|hurt|death|cry|scared`,
`&zoom`; keys 1–0 switch animations).
