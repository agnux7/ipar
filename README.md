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
├── docs/           # PDF que se descargan desde la sección Recursos
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
- **Inicio de sesión simulado** (sin validación): al "entrar" se desbloquea visualmente la sección **Diezmos** y aparece el panel de administrador de eventos.
- **CRES** ya no es sección del sitio: el menú abre el sitio del seminario, https://seminariocres.com/, en una pestaña nueva.
- Modal "Crear nuevo evento" (panel de administrador, sin guardar datos reales).
- **Fechador:** la barra superior muestra la fecha actual en español y se repinta al cruzar la medianoche.
- **Contador de visitas** en el pie. En esta fase se guarda en `localStorage`, así que cuenta las visitas **de cada navegador**, no el total global del sitio; para un total real hace falta backend (fase 2).
- Scroll suave, conteo animado de estadísticas y revelado al hacer scroll.
- Accesibilidad: navegación por teclado, `aria-label` en controles, foco visible y soporte de `prefers-reduced-motion`.

---

## Contenido por reemplazar antes de publicar

Estos valores son **de muestra** y deben sustituirse por datos oficiales:

- **Estadísticas de Comunidad:** Sínodos y Presbiterios ya son oficiales (2 y 8). Faltan **Iglesias** y **Miembros activos** (atributo `data-count`).
- **Contacto del footer:** dirección, correo y teléfono.
- **Línea de tiempo (sección IPAR):** las cuatro fechas ya son oficiales (1879 inicio de la IPAR, 2023 plan estratégico, 2024 fundación del Sínodo General, 2029 aniversario). Falta afinar la redacción con el archivo histórico.
- **Eventos:** el calendario solo trae la *III Reunión ordinaria de Sínodo General* (17–19 sep 2026, Río Verde, SLP). Se retiraron las tarjetas de ejemplo; falta cargar el resto de las actividades oficiales.
- **Recursos:** ocho documentos ya se descargan desde `docs/`. Cuatro categorías siguen sin archivo y aparecen marcadas como *Pendiente de carga*: Reglas Parlamentarias, Libro de Culto y Liturgia, Devocionales y En defensa de la fe.
- **Derechos de los PDF:** las confesiones históricas son de dominio público, pero algunas ediciones y los tres cuadernos de *El Credo Apostólico* (Humberto Casanova y Jeff Stam, Libros Desafío) son publicaciones con autor y editorial. Conviene confirmar el permiso de distribución antes de difundir el sitio.
- **Fotografías del carrusel:** cada diapositiva es un placeholder. Para usar fotos reales, sustituye el degradado de `.bg` por una imagen:
  ```css
  .slide[data-i="0"] .bg{ background:url('img/adoracion.jpg') center/cover; }
  ```
- **Estructura de gobierno:** un Sínodo General (fundado en 2024) que reúne a **2 sínodos** y **8 presbiterios**.

---

## Lo que NO incluye esta fase

Base de datos, backend/API, autenticación real, calendario funcional ni carga de archivos. Todo eso corresponde a la **fase 2**, una vez aprobado el diseño visual.

---

© 2026 Sínodo General IPAR — Todos los derechos reservados.
