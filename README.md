# Sínodo General IPAR — Sitio web (Fase 1: maqueta visual)

Sitio oficial del **Sínodo General de la Iglesia Presbiteriana Asociada Reformada de México A.R. (IPAR)**.

> «La luz en las tinieblas resplandece» — Juan 1:5

Esta es la **fase 1**: una maqueta visual estática e interactiva, sin backend ni autenticación real. Sirve para aprobar el diseño antes de construir la funcionalidad de la fase 2.

---

## Estructura del repositorio

```
sinodo-ipar/
├── index.html      # Sitio completo y autocontenido (HTML + CSS + JS)
├── img/
│   ├── sello-ipar.png       # Sello oficial del Sínodo (fondo transparente)
│   ├── favicon-32.png       # Ícono de pestaña
│   └── apple-touch-icon.png # Ícono para iOS
└── README.md       # Este archivo
```

Todo el sitio vive en un solo archivo `index.html`: el CSS está embebido en `<style>` y el JavaScript en `<script>` al final del documento. No hay paso de compilación.

---

## Tecnología

- HTML, CSS y JavaScript vanilla (sin frameworks ni librerías de JS).
- **Tipografía:** Playfair Display + Inter (Google Fonts, vía CDN).
- **Íconos:** Tabler Icons webfont (vía CDN).
- **Imágenes:** el sello oficial vive en `img/`; el resto de los placeholders son SVG inline y degradados CSS.

---

## Cómo verlo en local

Al ser estático, basta con abrir el archivo. Para evitar restricciones del navegador con `file://`, conviene servirlo:

```bash
# con Python
python3 -m http.server 8000
# luego abre http://localhost:8000

# o con Node
npx serve .
```

---

## Despliegue en Vercel

No requiere configuración (`vercel.json` no es necesario). Es un sitio estático.

**Opción A — sin terminal**
1. Sube el repositorio a GitHub.
2. En Vercel: **Add New → Project → Import** el repo.
3. *Framework Preset:* **Other**. Sin *build command* ni *output directory*.
4. **Deploy**. Cada `push` redepliega automáticamente.

**Opción B — Vercel CLI**
```bash
npm i -g vercel
vercel --prod
```

Para dominio propio: **Project → Settings → Domains** en Vercel.

---

## Funcionalidades de la maqueta

- Mega-menú por hover en escritorio; menú hamburguesa con acordeón en móvil (colapsa en ≤1199px).
- Carrusel del hero con autoplay, flechas, puntos, navegación por teclado (← →) y swipe táctil.
- Modal de búsqueda a pantalla completa (resultados simulados).
- **Inicio de sesión simulado** (sin validación): al "entrar" se desbloquean visualmente las secciones **CRES** y **Diezmos** y aparece el panel de administrador de eventos.
- Modal "Crear nuevo evento" (panel de administrador, sin guardar datos reales).
- **Fechador:** la barra superior muestra la fecha actual en español y se repinta al cruzar la medianoche.
- **Contador de visitas** en el pie. En esta fase se guarda en `localStorage`, así que cuenta las visitas **de cada navegador**, no el total global del sitio; para un total real hace falta backend (fase 2).
- Scroll suave, conteo animado de estadísticas y revelado al hacer scroll.
- Accesibilidad: navegación por teclado, `aria-label` en controles, foco visible y soporte de `prefers-reduced-motion`.

---

## Contenido por reemplazar antes de publicar

Estos valores son **de muestra** y deben sustituirse por datos oficiales:

- **Estadísticas de Comunidad:** Sínodos / Presbiterios / Iglesias / Miembros (atributo `data-count`).
- **Contacto del footer:** dirección, correo y teléfono.
- **Línea de tiempo (sección IPAR):** confirmar fechas y redacción con el archivo histórico.
- **Eventos:** el calendario solo trae la *III Reunión ordinaria de Sínodo General* (17–19 sep 2026, Río Verde, SLP). Se retiraron las tarjetas de ejemplo; falta cargar el resto de las actividades oficiales.
- **Fotografías del carrusel:** cada diapositiva es un placeholder. Para usar fotos reales, sustituye el degradado de `.bg` por una imagen:
  ```css
  .slide[data-i="0"] .bg{ background:url('img/adoracion.jpg') center/cover; }
  ```
- **Fechas históricas:** la IPAR inicia en **1879** y cumple **150 años en 2029**; el resto de los hitos de la línea de tiempo (1901, 2028) sigue siendo de muestra.

---

## Lo que NO incluye esta fase

Base de datos, backend/API, autenticación real, calendario funcional ni carga de archivos. Todo eso corresponde a la **fase 2**, una vez aprobado el diseño visual.

---

© 2026 Sínodo General IPAR — Todos los derechos reservados.
