# RPE v10 UX/UI Handoff

## Current deployed artifact

- GitHub Pages repo: `https://github.com/luismescobar/rpe-compilacion`
- Branch: `main`
- Deployed file: `index.html`
- Source HTML copied from: `/Users/amluis/Downloads/RPE_PROYECTO/versions/v10/rpe_compilacion_v10.html`
- Generator: `/Users/amluis/Downloads/RPE_PROYECTO/rpe_gen_v10.py`

## What changed in v10

v10 keeps the same 107 existing RPE criteria and changes the UX/UI only.

- Added a default `Biblioteca` view.
- Replaced the old text-heavy hero with a modern Apple Books / Kindle-style shelf.
- Added four SVG pictogram cards:
  - `Leer criterios`
  - `Temas`
  - `Años`
  - `Leyes`
- Added a horizontal row of SCJN ponentes using existing base64 photos from `PHOTOS`.
- Clicking a minister photo filters by that ponente through the existing search input.
- Added frequent topic cards generated from existing `temas`.
- Added year bars as direct filters.
- Added reader modes inside the detail panel:
  - Normal
  - Texto grande
  - Compacto
  - Contraste
- Added a direct `Fundamento legal` action in the detail panel.

## Sidebar behavior

The sidebar is intentionally responsive and should not be simplified back to a static panel.

### Desktop >= 1024px

- Sidebar is in document flow.
- The top sidebar button runs `toggleSidebarMode()`.
- Expanded width uses `--sbw`.
- Compact mode adds `.sb-mini` to `#appBody` and collapses the sidebar to a 64px icon rail.
- Compact preference is persisted in `localStorage` key `rpeSidebarMini`.

### Compact rail interaction

Do not make all compact icons behave as a generic expand button.

`toggleSec(id)` must:

1. Detect `.sb-mini` on `#appBody`.
2. Remove `.sb-mini`.
3. Persist `rpeSidebarMini = 0`.
4. Close every `.sb-sec` except the requested `id`.
5. Scroll the requested section into view.

This makes each pictogram open its own filter:

- Fuente
- Tipo de criterio
- Sala / Órgano
- Año
- Tema clave

### Tablet and mobile < 1024px

- Header hamburger opens the sidebar drawer.
- Sidebar internal button closes the drawer.
- Do not apply compact rail behavior on tablet/mobile.

## Files to edit for future changes

- Generator/template: `/Users/amluis/Downloads/RPE_PROYECTO/rpe_gen_v10.py`
- Generated HTML: `/Users/amluis/Downloads/RPE_PROYECTO/versions/v10/rpe_compilacion_v10.html`
- GitHub Pages deploy target: `/private/tmp/rpe_site/index.html`

## Regeneration and deploy flow

```bash
cd /Users/amluis/Downloads/RPE_PROYECTO
python3 rpe_gen_v10.py
cp /tmp/rpe_compilacion_v10.html /Users/amluis/Downloads/RPE_PROYECTO/versions/v10/rpe_compilacion_v10.html
cp /Users/amluis/Downloads/RPE_PROYECTO/versions/v10/rpe_compilacion_v10.html /private/tmp/rpe_site/index.html
cd /private/tmp/rpe_site
git add index.html CLAUDE_HANDOFF.md
git commit -m "v10: modernize RPE library UX"
git push origin main
```

## Verification already used

```bash
python3 /Users/amluis/Downloads/RPE_PROYECTO/rpe_gen_v10.py
node -e "const fs=require('fs'); const html=fs.readFileSync('/Users/amluis/Downloads/RPE_PROYECTO/versions/v10/rpe_compilacion_v10.html','utf8'); const m=html.match(/<script>([\s\S]*)<\/script>/); new Function(m[1]); console.log('JS syntax OK');"
```

Expected:

- `Total:107 SCJN:99 TFJA:8 J:36 P:0 TA:71`
- `JS syntax OK`

