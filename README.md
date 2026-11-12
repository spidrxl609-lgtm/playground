# ASPHODEL

A browser-based PS1-style third-person horror adventure (prologue + Chapter 1). Everything lives in a
single `index.html`; Three.js is loaded from a CDN, and all models and textures are generated in code.

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
| Sprint | hold Shift | B / RT / L3 | push the stick fully |
| Interact / advance text | E, Space or Enter | A / X | ACT button, or tap the marker / text box |
| Pause | Esc | Start | II |

The camera follows over Leta's shoulder and shortens its boom rather than pass through walls. Settings
has volume, camera speed, invert Y and a pixelation toggle. Progress is saved at pay phones and at the
end of a chapter (localStorage).

## Extending

`index.html` is split into numbered, commented sections (see the file map at the top of the script):

- **Scenes** — `registerScene(id, { env, build })` returns geometry, walkable rects, colliders,
  interactables, `triggers` (story beats and companion barks) and an optional `mirror` plane.
- **Chapters** — `registerChapter(id, { scene, spawn, onStart })`. Story beats are async functions using
  the `Script` API: `talk`, `choice`, `cam` (cinematic shots), `walkTo`, `pose`, `look`, `join`, flags,
  and `attach(n)` for the hidden attachment counter.
- **Characters** — `CHARACTERS.leta()`, `.mnema()`, `.hollow()`; poses live in `POSES`.

`index.html?viewer` opens a model viewer (`&view=front|side`, `&anim=idle|walk|run|cry|scared|laugh|reach|cry_sit`,
`&zoom`; keys 1–9 switch animations).
