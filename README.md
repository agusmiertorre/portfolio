# Portfolio — Agustín Mier Torre

Web personal interactiva en **un único archivo autocontenido**: [`index.html`](index.html)
(HTML semántico + CSS + Vanilla JS + [Lucide Icons](https://lucide.dev) vía CDN).

## Uso

Abrí `index.html` en cualquier navegador. No requiere build ni dependencias.
Para publicarlo alcanza con subir el archivo a GitHub Pages, Vercel, Netlify o cualquier hosting estático.

## Qué incluye

| Sección | Detalle |
|---|---|
| Hero | Badges de especialidad, CTAs, **tarjeta de perfil** (foto + datos reales) y contador animado |
| Perfil | Bio extendida + ficha rápida de contacto |
| Proyectos | Grilla con filtro por categoría (tabs accesibles con teclado), sin conteos a la vista |
| Trayectoria | Timeline de experiencia laboral y formación académica |
| Galería | 3 tarjetas con *placeholders* listos para reemplazar por fotos reales |
| Stack | 4 grupos: Hardware/Maker, Programación, IA & Datos, Pedagogía PBL |
| Footer | Contacto + botón "Imprimir / Guardar PDF" |

## Paleta de comandos (⌘K)

Se abre con <kbd>⌘ K</kbd> / <kbd>Ctrl K</kbd> o desde el botón "Buscar" del header.
Permite saltar a cualquier sección, buscar un proyecto por nombre o tag, aplicar un filtro,
copiar el email, abrir LinkedIn/GitHub, cambiar el tema o imprimir.

El índice **se arma solo leyendo el DOM**: si agregás un proyecto nuevo o una sección al nav,
aparece en la paleta sin tocar el JavaScript. La búsqueda ignora acentos (`robotica` encuentra
`Robótica`) y acepta subsecuencias (`adi` encuentra `Álbum Digital Interactivo`).

## Características técnicas

- **Responsive** verificado de 320 px a 1440 px, sin scroll horizontal.
- **Tema claro / oscuro** con detección de `prefers-color-scheme` y persistencia en `localStorage`.
- **Accesibilidad**: HTML semántico, skip link, roles ARIA en el filtro (`tablist`/`tab`/`tabpanel`)
  con navegación por flechas, `aria-expanded` en el menú mobile, foco visible.
- **Microinteracciones**: reveal on scroll, spotlight en tarjetas, marquee, contadores.
  Todo se desactiva con `prefers-reduced-motion: reduce`.
- **Impresión**: `@media print` optimizado para A4 (~4,5 páginas). Funciona como CV completo:
  incluye la foto, la ficha de contacto y la trayectoria. Imprime todos los proyectos aunque
  haya un filtro activo y expande las URLs de los enlaces relevantes.
- **Foto de perfil embebida** como `data:` URI, así el archivo sigue siendo autocontenido.
- **Logos de GitHub y LinkedIn como SVG inline** (`<symbol>` + `<use>`): Lucide retiró los
  íconos de marca de su set, así que no se pueden pedir por `data-lucide`. Si un nombre de
  ícono no existe, el JS borra el `<i>` vacío para que no quede un hueco en el `gap`.

## Datos personales

Los datos del hero (rol, experiencia, formación, método, idiomas) están en la
`.badge-card`, y la trayectoria en la sección `#trayectoria`.
Los cuatro recuadros de abajo (`.stat`) son deliberadamente cualitativos —
`4+`, `PBL`, `STEAM`, `IA` — para no exponer conteos de proyectos. Si querés un portfolio
más corto, en la timeline de experiencia hay un comentario marcando los dos empleos no técnicos
que se pueden borrar.

## Cómo agregar las fotos reales

En la sección `#taller` cada tarjeta tiene un placeholder. Reemplazá el bloque:

```html
<div class="shot__ph">
  <span class="ph-ico" aria-hidden="true"><i data-lucide="image-plus"></i></span>
  <span>Foto 01 · Arduino</span>
</div>
```

por la imagen (el CSS ya aplica `object-fit: cover` y el zoom en hover):

```html
<img src="img/taller-arduino.jpg"
     alt="Estudiantes programando una placa Arduino en el taller"
     loading="lazy" width="1200" height="900">
```

Las fotos van en una carpeta `img/` junto al HTML. Relación de aspecto recomendada: **4:3**.
Si preferís mantener el archivo 100 % autocontenido, se pueden embeber como `data:` URI en base64.

## Personalización rápida

Los colores, tipografías y radios están centralizados como *design tokens* en `:root`
(y su contraparte en `html[data-theme="light"]`), al inicio del `<style>`:

```css
--brand:   #7C5CFF;  /* violeta principal   */
--maker:   #FF6B35;  /* naranja maker       */
--circuit: #14E0B0;  /* verde circuito      */
--spark:   #FFC53D;  /* amarillo acento     */
```

Cada tarjeta de proyecto define su acento con `style="--accent: var(--maker)"`.
