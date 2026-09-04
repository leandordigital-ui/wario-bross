# 🍔 Wario Bross — Web Oficial

Sitio web de una sola página (MVP) para **Wario Bross**, restaurante de comida
rápida en El Caney, Cali, Colombia. Construido en HTML + CSS + JavaScript
Vanilla (sin frameworks, sin build step), listo para desplegar en **Vercel**.

El objetivo del sitio es un único flujo de conversión:

**Explorar el menú → Elegir un producto → "Pedir ahora" → FUDO (plataforma oficial de pedidos)**

Sitio en vivo: **https://wario-bross.vercel.app/**

---

## 📁 Estructura del proyecto

```
wario-bross/
│
├── index.html          ← Toda la web: HTML + CSS + JS en un solo archivo
├── 404.html             ← Página de error personalizada
├── robots.txt            ← Instrucciones para buscadores
├── sitemap.xml            ← Mapa del sitio para indexación
├── llms.txt                ← Info factual complementaria para IA (GEO)
├── README.md                ← Este archivo
├── .gitignore                 ← Archivos que Git debe ignorar
│
└── img/
    ├── brand/           ← Logo y favicons oficiales
    ├── hero/             ← Imagen principal del Hero
    └── products/          ← Fotografías reales del menú
```

> **Nota:** las reseñas de Google Maps ya no se guardan como capturas de
> pantalla. Están transcritas como texto real dentro del array `RESENAS` en
> `index.html`, junto con el resto del contenido data-driven del sitio (ver
> sección de reseñas más abajo).

---

## 🖥️ Ver el sitio en tu computador (sin instalar nada)

1. Haz doble clic sobre `index.html`.
2. Se abre en tu navegador. Así de simple — no necesitas servidor ni instalar nada.

Si quieres verlo exactamente como se vería en internet (recomendado antes de
publicar cambios grandes), puedes usar la extensión **Live Server** de VS Code,
o simplemente confiar en las **Vista Previas automáticas de Vercel**.

---

## 🛠️ Cómo actualizar el contenido

Todo el sitio está pensado para que **no tengas que tocar el diseño** al
actualizar información. Los datos viven centralizados dentro de `index.html`:

### Cambiar el link de pedidos, teléfono, WhatsApp, Instagram, dirección u horarios

Busca dentro de `index.html` el bloque:

```javascript
const CONFIG = Object.freeze({
  fudoUrl: "...",
  whatsappNumber: "...",
  address: "...",
  mapsUrl: "...",
  phoneDisplay: "...",
  phoneHref: "...",
  hours: [ ... ]
});
```

Cambia el valor ahí — se actualiza automáticamente en **todos** los botones,
enlaces y tablas del sitio que lo usan. No necesitas buscar y reemplazar en
varios lugares.

> ⚠️ Si cambias `fudoUrl`, `address`, `mapsUrl`, `phoneDisplay` o `hours`,
> avísale a quien mantenga el Schema.org (JSON-LD en el `<head>`) para que
> también se actualice ahí — esos datos se generan a partir del mismo `CONFIG`
> y `MENU`, pero viven como texto estático en el `<head>`, así que no se
> sincronizan automáticamente.

### Agregar, quitar o editar un producto del menú

Busca el bloque `const MENU = [ ... ];` dentro de `index.html`. Es una lista
de categorías, cada una con su lista de productos:

```javascript
{ nombre: "Nombre del producto", desc: "Descripción real.", imagen: "img/products/archivo.webp", precio: 25900 }
```

- Para **agregar** un producto nuevo, copia una línea parecida dentro de la
  categoría correcta y cambia los datos.
- Para **quitar** un producto, borra su línea completa.
- Para **cambiar un precio**, solo edita el número (sin puntos ni comas).
- El campo `personas` es opcional (solo si aplica, ej. `personas: 2`).
- Si el producto no tiene foto todavía, deja `imagen: ""` — el sitio muestra
  automáticamente el ícono de la categoría en su lugar.

**No dupliques información en otras partes del HTML** — el menú visual se
genera automáticamente a partir de este único array.

> ⚠️ Igual que con `CONFIG`: el bloque `hasMenu` del Schema.org (JSON-LD) es
> una copia estática de este array en el momento en que se generó. Si agregas,
> quitas o cambias precios de productos, pide que se regenere ese bloque para
> que no quede desactualizado.

### Agregar una foto nueva de producto

1. Guarda la foto (idealmente en formato `.webp`, optimizada) dentro de
   `img/products/`.
2. En el array `MENU`, en el producto correspondiente, escribe la ruta:
   `imagen: "img/products/nombre-del-archivo.webp"`.

---

## ⭐ Reseñas de Google Maps

Las reseñas están transcritas como texto real (no imágenes) dentro del array
`RESENAS` en `index.html`. Cada una incluye nombre del autor, calificación,
texto, tiempo relativo y un enlace directo "Ver reseña en Google Maps".

Para agregar una reseña nueva:

1. Copia el texto real de la reseña desde Google Maps (nunca inventar).
2. Agrega un objeto nuevo al array `RESENAS`, siguiendo el mismo formato de
   los existentes.
3. El carrusel se actualiza automáticamente — no hay que tocar el HTML del
   carrusel ni las tarjetas manualmente.

---

## 🚀 Publicar el sitio (Git + Vercel)

Flujo recomendado una vez publicado por primera vez:

```
Editas index.html (u otro archivo)
      ↓
Subes el cambio a GitHub ("commit" + "push")
      ↓
Vercel detecta el cambio y publica automáticamente
      ↓
El sitio en internet se actualiza en 1-2 minutos
```

No necesitas volver a "subir" el sitio manualmente cada vez — una vez
conectado, Vercel publica cada cambio que subas a GitHub.

**Antes de dar por cerrada una actualización**, verifica el archivo
directamente en GitHub (no solo en tu carpeta local) para confirmar que el
cambio realmente llegó al repositorio antes de asumir que ya está en vivo.

---

## ✅ Antes de dar por cerrada una actualización, verificar

- El botón **"Pedir ahora"** sigue llevando a FUDO en todos los lugares.
- El sitio se ve bien en un celular (la mayoría del tráfico es móvil).
- No hay errores en la consola del navegador (clic derecho → Inspeccionar → Console).
- Las imágenes nuevas cargan correctamente (rutas escritas bien, sin espacios, mismas mayúsculas/minúsculas).
- Los precios y descripciones son reales, no inventados.
- El archivo cambiado aparece actualizado en GitHub, no solo en tu carpeta local.

---

## 🎨 Identidad de marca

Colores extraídos directamente del logo real de Wario Bross:

| Color                            | Uso                                                                               |
| --------------------------------- | ----------------------------------------------------------------------------------- |
| `#12121D` Negro-azulado          | Footer, textos principales                                                        |
| `#F6B73C` Dorado                 | Acentos sobre fondo oscuro                                                        |
| `#F07C3E` Naranja                | Acento decorativo (pan del logo)                                                  |
| `#1E606F` Teal                   | Acentos/eyebrows sobre fondo claro                                                |
| `#D8303F` Rojo (tomate del logo) | **Reservado exclusivamente** para el botón "Pedir ahora" y acciones de conversión |

---

Proyecto desarrollado por **Leandor Digital** para Wario Bross · Cali, Colombia 🇨🇴
