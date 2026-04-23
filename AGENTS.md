# AGENTS.md — bzr.bz

Instrucciones para agentes de código (Claude Code, etc.) que trabajen en este repo.

## Qué es este repo

La web del bazar: landing de herramientas + manifiesto. **Sitio estático, sin build step, sin dependencias.** HTML + CSS a pelo. Si alguna vez hace falta JS, añádelo inline o en un único `main.js`; no introduzcas bundler.

Lee también `README.md` para contexto y `manifiesto.html` para entender la filosofía del proyecto. Los principios del bazar aplican también a este repo: publicar pronto, iterar feo, no sobre-ingenierizar.

## Ejecución local

```sh
python3 -m http.server 8000
# o
npx serve .
```

No hay `package.json`, no hay `node_modules`, no hay `dist/`. Despliegue en Cloudflare Pages apuntando a `main`, sin build command, directorio de publicación `/`.

## Convenciones

- **CSS**: todo en `styles.css`. Variables de diseño en `:root` (paleta, tipografías, tamaños). No dupliques valores literales — usa las variables.
- **Tipografías**: Fraunces (variable, con ejes `SOFT` y `WONK` — esos glifos raros son intencionales) + JetBrains Mono. Se cargan de Google Fonts.
- **Paleta**: papel manila + tinta + sello rojo. Nunca añadas un color sin pasar por una variable CSS.
- **Accesibilidad**: respetar `prefers-reduced-motion`; los `aria-disabled="true"` en puestos "próximamente" son intencionales.
- **HTML**: semántico, sin divs innecesarios. Los puestos son `<a class="stall">` para que todo el bloque sea clicable.

## Añadir un puesto nuevo

Por ahora los puestos están hardcoded en `index.html` dentro de `.stalls`. Cuando pasen de tres, migrar a un `tools.json` servido estático y renderizado con JS mínimo. No antes — YAGNI.

Cada puesto declara:
- `status`: `status--soon` (mostaza) / `status--open` (rojo) / `status--closed` (tachado)
- nombre, tagline corto (una línea en mono color stamp), descripción de 1-3 frases
- URL del subdominio (ej. `https://jrnl.bzr.bz`)

Si cambia el estado de un puesto, actualiza también el contador en `.section-head .count`.

## Cosas que NO hay que hacer

- No añadir React, Vue, frameworks, ni bundlers.
- No añadir trackers (Google Analytics, Meta pixel, Hotjar…). Si hace falta analítica, será Plausible o Umami self-hosted.
- No importar fuentes ni assets de CDNs que no sean Google Fonts (la única excepción, por pragmatismo).
- No meter imágenes grandes. Preferir SVG inline o texturas CSS (como el grano actual del `body`).
- No romper las URLs existentes: `/` y `/manifiesto.html` (o `/manifiesto` con pretty URLs).

## Commits

Estilo conventional commits cuando vaya bien (`feat:`, `fix:`, `chore:`, `docs:`, `style:`), pero sin religión. Mensajes en español o inglés, consistentes dentro del mismo commit.
