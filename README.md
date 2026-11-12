# ASPHODEL

A browser-based PS1-style fixed-camera horror adventure (prologue build). Everything lives in a single
`index.html`; Three.js is loaded from a CDN, and all models and textures are generated in code.

## Run

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

## Controls

| | Keyboard | Touch |
| --- | --- | --- |
| Move | WASD / arrows | left stick |
| Run | hold Shift | push the stick fully |
| Examine / advance text | E, Enter or Space | ACT, or tap the marker / text box |
| Pause | Esc | II |

Settings offers **Modern** controls (camera-relative, the default) or classic **Tank** controls, plus
volume and a pixelation toggle. Progress is saved at pay phones (localStorage).

## Extending

`index.html` is split into numbered, commented sections (see the file map at the top of the script):

- **Scenes** — `registerScene(id, { env, build })` returns geometry, walkable rects, colliders, camera
  zones and interactables.
- **Chapters** — `registerChapter(id, { scene, spawn, onStart })`; scripts use the `Script` API
  (`say`, `lines`, `choice`, `flag`, `save`, `gotoScene`).
- **Characters** — `CHARACTERS.leta()` / `CHARACTERS.mnema()`. Mnema is built and animated but not
  placed in the prologue.

`index.html?viewer` opens a model viewer for both characters (`&view=front`, `&anim=idle|walk|run`,
`&zoom`; keys 1–4 switch animations).
