# Agencia de viajes: brief de diseño

Plantilla `agencia-viajes` creada el 29/10/2026 a partir de `eventos-bodas` con `php artisan plantillas:nueva` y
rediseñada entera (tanda «ancho completo», fila 15 del brief). Este fichero se queda en el repo: es lo que lee quien
(persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: agencias de viajes de barrio o de ciudad, organizadores de excursiones, guías turísticos y empresas
  de rutas (`agencia-viajes, turismo, excursiones, guia-turistico, rutas`). Quien entra quiere ver qué viajes hay,
  cuándo salen, cuánto cuestan y si puede fiarse de la agencia.
- **Qué tiene que conseguir la web**: que pidan presupuesto (formulario con destino, fechas y viajeros; botón de
  cabecera) o que pregunten por un viaje concreto («Lo quiero» al WhatsApp con el viaje en el mensaje).
- **Tono y estilo** (`aventurero`): enérgico, luminoso, de puerto y aeropuerto. Sí: el panel de salidas de un
  aeropuerto, una tarjeta de embarque, un cartel de viajes de los años sesenta en clave actual. No: el catálogo de
  agencia con cajas blancas centradas y sombras, ni la «caja centrada estrecha con tarjetas».
- **Concepto**: «panel de salidas y billete de embarque». La portada es una foto a sangre a pantalla completa con un
  velo de océano y atardecer y el billete de la próxima salida; una franja naranja con los destinos pasa por debajo
  como un rótulo; los viajes son billetes con talón troquelado (línea de puntos y dos muescas del color de la banda);
  el proceso es una ruta punteada con paradas; los destinos, columnas de fotos de borde a borde; el pie firma con el
  nombre en mayúsculas gigantes.
- **Paleta de ejemplo**: primario `#0b4f6c` (azul océano: bandas oscuras), acento `#f26b38` (naranja atardecer:
  botones, cifras, líneas, sellos), fondo `#f6efe2` (arena), texto `#10232e` (tinta). Derivados con `color-mix`:
  océano hondo (primario + negro), arena tostada, papel de los billetes, naranja legible sobre claro (acento + texto)
  y sobre oscuro (acento + fondo). Texto sobre el naranja: tinta, nunca blanco (contraste AA).
- **Tipografía** (del sistema, sin descargas): títulos en mayúsculas estrechas tipo señalética DIN (Bahnschrift en
  Windows, DIN Alternate / Avenir Next Condensed en Apple, Roboto Condensed o Arial Narrow de respaldo) a 700, de
  2,4-2,85 rem en móvil a 5,4-8,25 rem en escritorio, interlineado 0,88-0,95; texto en system-ui; antetítulos,
  botones, rótulos y etiquetas en la misma DIN en mayúsculas con 0,1-0,2 em de interletrado y una línea naranja.
- **Ritmo de bandas** (ejemplo): portada foto oscura + franja naranja → viajes arena → por qué océano 50/50 con foto
  a sangre → cifras naranja → proceso arena tostada → destinos océano hondo con fotos de borde a borde → cta foto
  panorámica a sangre → opiniones océano → preguntas papel → presupuesto océano hondo 50/50 con foto → contacto arena
  50/50 con foto → pie océano hondo.
- **Apartados** en orden:
  1. `hero`: foto a sangre (88 svh en móvil, 100 svh en escritorio), velo, antetítulo con línea, título enorme,
     texto, dos botones; billete «próxima salida» (viaje destacado) a la derecha en escritorio; franja de destinos.
  2. `viajes` (`viajes: [{titulo, destino, categoria, duracion, fecha, precio, texto, incluye, imagen, destacado}]`):
     billetes en 2/3 columnas (carrusel en móvil), filtro por tipo, sello en el destacado, «Lo quiero».
  3. `ventajas` (`items`: titulo, texto, icono): océano 50/50 con foto a sangre a la izquierda.
  4. `cifras` (`items`: titulo = cifra, texto): banda naranja con cifras gigantes.
  5. `proceso` (`items`: titulo, texto, icono): paradas numeradas unidas por una ruta punteada.
  6. `destinos` (`items`: titulo, texto, imagen, url): columnas de fotos de borde a borde con el nombre encima.
  7. `cta`: foto panorámica a sangre, título enorme centrado y dos botones.
  8. `opiniones` (`testimonios`: texto, autor, nota): cita enorme + tres columnas con línea naranja.
  9. `preguntas`: titular fijo a la izquierda y acordeón con «+» naranja.
  10. `presupuesto` (`items` pasos, `tipos_viaje`, `boton`, `nota`): foto 50/50 + formulario con fechas y viajeros.
  11. `contacto` (`horario: [{dia, horas}]`, `boton`): teléfono grande, botones, datos, horario y foto a sangre.
- **Fotos** (`fotos.json`, 15): costa cantábrica al atardecer para la portada, paisajes de cada viaje (Azores,
  Islandia, Sáhara, Oporto, Japón, Picos de Europa), detalle de mochila en un tren, columnas verticales de destinos
  (costa atlántica, fiordo, medina, bahía asiática), mar de nubes desde un avión, mesa con mapa y brújula, interior de
  la agencia. Sin texto legible, sin logotipos, sin personas reconocibles.
- **Qué no hacer**: tarjetas blancas con sombra en una columna estrecha, serif romántica o cursivas (eso es
  `eventos-bodas`), diagonales industriales (`taller-mecanico`), el negro y oro de `hotel-boutique`, más de un acento.

## Hecho

- [x] `site.yaml` de ejemplo (Marea Alta Viajes, Santander), todo activo, al menos un elemento por lista, precios
  entre comillas, listas planas.
- [x] Secciones nuevas (`viajes`, `ventajas`, `cifras`, `destinos`, `cta`, `presupuesto`) y todas las demás
  rediseñadas, `texto.astro` con el diseño; `index.astro` sin tocar.
- [x] `template.yaml` con sectores `[{id, nombre}]`, secciones, estilo, orden y guion `asistente:` (11 pasos).
- [x] `fotos.json` (15) y placeholders.
- [x] `README.md`, `CLAUDE.md`, `aviso-legal.astro` y `404.astro` con el diseño.
- [ ] Fotos y previews definitivas (`preview/card.jpg`, `preview/full.jpg`): las genera el paso de fotos.

## Páginas propias (fichas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.
