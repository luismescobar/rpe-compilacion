# CLAUDE.md — rpe-compilacion (repo desplegado)

SPA de jurisprudencia RPE desplegada en GitHub Pages. Rama `main` → auto-deploy.

Documentación completa del proceso:
`/Users/amluis/Downloads/RPE_PROYECTO/CLAUDE.md`

---

## Archivos en este repo

| Archivo | Descripción |
|---|---|
| `index.html` | SPA completa (~1.2 MB, autocontenida). `const DATA=[...]` embebido. |
| `infografia.html` | Infografía cronológica (~29 KB, autocontenida). Cargada como iframe. |
| `CLAUDE_HANDOFF.md` | Notas de handoff de v10 (UX/UI). |

## Para editar UI/CSS/JS (sin cambiar datos)

Editar directamente `index.html` con `Edit`. Luego:
```bash
cd /tmp/rpe-compilacion-clone
git add index.html
git commit -m "fix: descripción"
git push origin main
```

## Para actualizar con nuevos datos

Ver sección "Pipeline de generación" en el CLAUDE.md del proyecto.
El generador produce `versions/v10/rpe_compilacion_v10.html` → copiar aquí como `index.html`.

## Estado actual (2026-06-05)

- 107 criterios: 99 SCJN + 8 TFJA
- Vistas: Biblioteca, Lista, Por temas, Cronología, Orientación, Infografía, Leyes
- Responsive: desktop ≥1024px · tablet ≤1023px · móvil ≤639px
- Paginación: 10 items/página, "Página X de Y"
- Orientación jurídica: pro-ciudadano en 2013-15, neutro 2016-18, pro-estado 2019-21,
  pro-ciudadano 2022-26

## Constantes críticas en index.html

```javascript
const PG = 10;          // items por página
const BH = 78;          // altura máxima de barras en px (NO usar % en nested grid)
const ALL_TEMAS = [...]; // orden canónico de los 13 temas
const OKW_C = [...];    // 24 keywords pro-ciudadano para oScore()
const OKW_E = [...];    // 20 keywords pro-estado para oScore()
```

## Reglas CSS móvil (≤639px)

```css
.toolbar    { display: none }      /* ocultar barra superior */
.bottom-nav { display: flex }      /* mostrar nav inferior */
.temas-grid { grid-template-columns: 1fr 1fr; gap: 8px } /* 2 col exactas */
.tc-card    { min-width: 0; overflow: hidden }            /* evitar blowout */
.pager      { flex-wrap: wrap }                           /* botones no se cortan */
```
