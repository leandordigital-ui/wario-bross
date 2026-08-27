# 🍔 Wario Bross — Web Oficial

Sitio web de una sola página (MVP) para **Wario Bross**, restaurante de comida
rápida en El Caney, Cali, Colombia. Construido en HTML + CSS + JavaScript
Vanilla (sin frameworks, sin build step), listo para desplegar en **Vercel**.

El objetivo del sitio es un único flujo de conversión:

**Explorar el menú → Elegir un producto → "Pedir ahora" → FUDO (plataforma oficial de pedidos)**

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
    ├── products/         ← Fotografías reales del menú
    └── reviews/           ← Capturas de reseñas de Google Maps (ver abajo)
```

> **Nota:** `404.html`, `robots.txt`, `sitemap.xml` y `llms.txt` se generaron
> en una entrega anterior del proyecto. Si no los tienes a la mano, pídeme
> que te los vuelva a generar.

---

## 🖥️ Ver el sitio en tu computador (sin instalar nada)

1. Haz doble clic sobre `index.html`.
2. Se abre en tu navegador. Así de simple — no necesitas servidor ni instalar nada.

Si quieres verlo exactamente como se vería en internet (recomendado antes de
publicar cambios grandes), puedes usar la extensión **Live Server** de VS Code,
o simplemente confiar en las **Vista Previas automáticas de Vercel** (ver la
guía de despliegue).

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

### Agregar, quitar o editar un producto del menú

Busca el bloque `const MENU = [ ... ];` dentro de `index.html`. Es una lista
de categorías, cada una con su lista de productos:

```javascript
{ nombre: "Nombre del producto", desc: "Descripción real.", imagen: "img/products/archivo.png", precio: 25900 }
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

### Agregar una foto nueva de producto

1. Guarda la foto (idealmente en formato `.webp` o `.png`, optimizada) dentro
   de `img/products/`.
2. En el array `MENU`, en el producto correspondiente, escribe la ruta:
   `imagen: "img/products/nombre-del-archivo.webp"`.

---

## ⭐ Sobre las reseñas de Google Maps

Las 5 capturas de pantalla de reseñas deben guardarse en:

```
img/reviews/
```

**Importante:** una captura de pantalla por sí sola no es ideal para el sitio
final, porque el texto dentro de una imagen no lo pueden leer los buscadores
ni las personas que usan lector de pantalla (mala práctica de SEO/accesibilidad).

Para construir la sección de reseñas correctamente, se necesita transcribir
de cada captura:

- Nombre del autor de la reseña
- Calificación (número de estrellas)
- Texto de la reseña
- Fecha aproximada

Con esos datos (reales, no inventados) se construye una sección de reseñas en
HTML real, con el texto legible y un enlace "Ver reseña en Google Maps" —
mucho mejor para SEO/GEO/AEO que una imagen. Si compartes las capturas o me
transcribes esos datos, armo la sección.

---

## 🚀 Publicar el sitio (Git + Vercel)

Ver el archivo **`GUIA-VERCEL-GITHUB.md`** — instrucciones explicadas paso a
paso, pensadas para alguien que nunca ha usado GitHub ni Vercel.

Flujo recomendado una vez publicado por primera vez:

```
Editas index.html
      ↓
Subes el cambio a GitHub ("commit")
      ↓
Vercel detecta el cambio y publica solo automáticamente
      ↓
El sitio en internet se actualiza en menos de un minuto
```

No necesitas volver a "subir" el sitio manualmente cada vez — una vez
conectado, Vercel publica cada cambio que subas a GitHub.

---

## ✅ Antes de dar por cerrada una actualización, verificar

- El botón **"Pedir ahora"** sigue llevando a FUDO en todos los lugares.
- El sitio se ve bien en un celular (la mayoría del tráfico es móvil).
- No hay errores en la consola del navegador (clic derecho → Inspeccionar → Console).
- Las imágenes nuevas cargan correctamente (rutas escritas bien, sin espacios).
- Los precios y descripciones son reales, no inventados.

---

## 🎨 Identidad de marca

Colores extraídos directamente del logo real de Wario Bross:

| Color | Uso |
|---|---|
| `#12121D` Negro-azulado | Footer, textos principales |
| `#F6B73C` Dorado | Acentos sobre fondo oscuro |
| `#F07C3E` Naranja | Acento decorativo (pan del logo) |
| `#1E606F` Teal | Acentos/eyebrows sobre fondo claro |
| `#D8303F` Rojo (tomate del logo) | **Reservado exclusivamente** para el botón "Pedir ahora" y acciones de conversión |

---

Proyecto desarrollado por **Leandor Digital** para Wario Bross · Cali, Colombia 🇨🇴
