# bzr.bz

La web del bazar. Estática, sin build step, sin dependencias.

## Estructura

```
.
├── index.html        Landing con el índice de puestos
├── manifiesto.html   Reglas de casa, filosofía del proyecto
├── styles.css        Estilos compartidos entre páginas
└── README.md
```

## Desarrollo

No hay build. Abre los archivos con cualquier servidor estático:

```sh
python3 -m http.server 8000
# o
npx serve .
```

Y entra a `http://localhost:8000`.

## Despliegue

Pensado para Cloudflare Pages o Netlify, apuntando a la rama `main`. Sin comando de build, directorio de publicación `/`.

Para servir las páginas sin extensión `.html` (p. ej. `bzr.bz/manifiesto` en vez de `bzr.bz/manifiesto.html`), configurar en Cloudflare/Netlify la opción de *pretty URLs* o un `_redirects` equivalente.

## Añadir un puesto nuevo

Por ahora los puestos están hardcoded en `index.html` (sección `.stalls`). Cuando haya más de tres, migrar a un `tools.json` y renderizar desde ahí. Mientras tanto, editar a mano.

Cada puesto tiene:
- Estado: `status--soon` / `status--open` / `status--closed`
- Nombre, tagline, descripción corta
- URL del subdominio

## Convenciones

- Paleta, tipografías y motion en `styles.css` (variables CSS en `:root`).
- Sin frameworks, sin JS (de momento). Si hace falta JS, añadirlo inline o en un solo `main.js`.
- Fuentes de Google Fonts: Fraunces (variable, con ejes `SOFT` y `WONK`) + JetBrains Mono.

## Licencia

El código, MIT. El contenido del manifiesto, CC BY 4.0.
