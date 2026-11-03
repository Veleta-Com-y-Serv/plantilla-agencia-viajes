# Plantilla «Agencia de viajes» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **aventurero**
(«panel de salidas y billete de embarque»: bandas a todo el ancho que alternan océano hondo, arena y naranja
atardecer; fotos a sangre; títulos en mayúsculas estrechas tipo señalética de aeropuerto; viajes como billetes con
talón troquelado; ruta punteada en el proceso). Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (también la lista `viajes`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = azul océano de las bandas oscuras, acento = naranja atardecer de botones, cifras y líneas, fondo = arena, texto = tinta). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); los derivados (océano hondo, arena tostada, papel de los billetes, naranja legible sobre claro y sobre oscuro) se calculan con `color-mix` en `src/styles/global.css`. El texto sobre el naranja va en el color de texto (tinta), no en blanco.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos`: Bahnschrift / DIN del sistema en estrecha; `--fuente-texto`: system-ui; bandas `.banda--arena|arena2|papel|oceano|hondo|sol`; botones `.btn`/`.btn-sec`/`.btn-claro`; billetes `.billete`, `.billete-corte`; ruta `.ruta`; destinos `.destino`; cabecera `.cabecera--viajes`; pie `.pie--viajes`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (se generan aparte a partir de `fotos.json`); las de respaldo en `public/placeholders/` (`Imagen.astro` cambia a la de respaldo si la foto falta). En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Paisajes y detalles de viaje sin personas reconocibles.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = brújula naranja + nombre en mayúsculas.
- **Cabecera**: fija, transparente sobre la portada y sólida (océano hondo) al bajar; menú completo desde 1180 px, plegable por debajo; `boton_cabecera` como botón naranja (desde 640 px y dentro del menú plegable).
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Un apartado nuevo puede reutilizar un diseño con `tipo: <id>`.
- `hero` → `hero.astro`: foto a sangre a pantalla completa con velo de océano y atardecer, `antetitulo`, `titulo` enorme, `texto`, `cta`, `cta_secundario`. En escritorio, el billete de la «próxima salida» (el primer viaje con `destacado: true`); debajo, la franja naranja con los destinos de los viajes. Sin imagen, océano con sol naranja.
- `viajes` → `viajes.astro`: `viajes` como billetes en 2-3 columnas (en móvil, carrusel horizontal), filtro por `categoria`, botón «Lo quiero» al WhatsApp del negocio con el viaje en el mensaje (o a `cta.url`), `cta` debajo, `etiqueta_destacado` para el sello.
- `ventajas` → `ventajas.astro`: banda océano; con `imagen`, fila 50/50 a sangre con `items` (titulo, texto, icono) en 2 columnas; sin imagen, 4 columnas.
- `cifras` → `cifras.astro`: banda naranja con `items` (titulo = la cifra, texto). Sin cifras no se pinta.
- `proceso` → `proceso.astro`: `items` (titulo, texto, icono) como paradas de una ruta punteada (vertical en móvil, horizontal desde 900 px).
- `destinos` → `destinos.astro`: banda océano hondo con `items` (titulo, texto, imagen, url opcional) en columnas de fotos de borde a borde.
- `cta` → `cta.astro`: foto panorámica a sangre con velo, título enorme y dos botones; sin foto, banda naranja.
- `opiniones` → `opiniones.astro`: `testimonios` (texto, autor, nota); el primero como cita enorme, el resto en 3 columnas. Sin testimonios no se pinta.
- `preguntas` → `preguntas.astro`: titular fijo a la izquierda y acordeón a la derecha. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: banda océano hondo 50/50 con foto a sangre, pasos (`items`: titulo, texto) y formulario con destino, tipo de viaje (`tipos_viaje`), fechas de ida y vuelta, adultos y niños; `boton`, `nota`, `cta` opcional.
- `contacto` → `contacto.astro`: teléfono en grande, botones de llamar y WhatsApp, email, dirección con «Cómo llegar», `horario` (lista de esta sección o `contacto.horario`) y foto a sangre a la derecha. Si no hay apartado de presupuesto activo, lleva aquí el formulario.
- `texto` → `texto.astro`: apartado genérico (`tipo: texto`) con `imagen` 50/50 opcional, `items` y `cta`.

## Campos propios de esta plantilla (además del esquema común)
- `viajes.viajes`: `[{titulo, destino, categoria, duracion, fecha, precio, texto, incluye, imagen, destacado}]`. Todo cadena; `precio` siempre entre comillas («desde 1.390 €», «Consultar»), vacío = no se muestra. `incluye` es UNA cadena separada por «;», nunca una lista. `categoria` = tipo de viaje (el filtro). `destacado: true` en uno: sale en la portada. Máximo 24.
- `viajes.etiqueta_destacado`: texto del sello del viaje destacado («Plazas limitadas»).
- `presupuesto.tipos_viaje`: cadena separada por «;» con las opciones del desplegable. `presupuesto.boton`, `presupuesto.nota`.
- `contacto.horario`: `[{dia, horas}]` (si falta, se usa `contacto.horario` de arriba). `contacto.boton`.
- `testimonios[].nota`: detalle bajo el nombre («Azores, mayo de 2026»).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista (ni en `incluye`).
5. **No inventes** precios, fechas, cifras, opiniones ni datos: si el cliente no los da, deja `precio: ""`, `fecha: ""`, `items: []` o `testimonios: []`; el componente lo oculta.
6. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro` (la primera banda deja sitio a la cabecera fija sola).
7. **Sección nueva**: mejor un id nuevo con `tipo:` (`texto`, `viajes`, `destinos`…). Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)`, `Seccion` (con su `banda`) y `Titular`. `src/pages/index.astro` la recoge sola.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio —`TravelAgency`— y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida y respaldo), JavaScript mínimo (cabecera, filtro de viajes), 16 px de margen lateral (`.contenedor`), sin scroll horizontal en móvil (la franja de destinos y el carrusel de viajes se desplazan solo dentro de sí mismos), ids `hero` y `contacto`. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

Fotos: `fotos.json` describe las fotos de `public/fotos/` (se generan aparte, sin personas reconocibles); los SVG de `public/placeholders/` quedan de respaldo.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.viajes.viajes` → `/viajes/<slug>/` (viaje).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/viajes/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
