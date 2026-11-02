# Plantilla NoExpertise · Agencia de viajes

Web aventurera a todo el ancho para agencias de viajes, turismo, excursiones, guías y rutas: portada a pantalla
completa con la próxima salida, viajes como billetes de embarque con filtro por tipo, por qué con nosotros, cifras,
proceso en ruta punteada, destinos de borde a borde, llamada a la acción con foto panorámica, opiniones con cita
grande, preguntas frecuentes, presupuesto con fechas y viajeros, y contacto con horario.

- Sectores: agencia-viajes, turismo, excursiones, guia-turistico, rutas. Estilo: aventurero. Plan mínimo: presencia.
- Secciones: hero, viajes, ventajas, cifras, proceso, destinos, cta, opiniones, preguntas, presupuesto, contacto
  (+ `texto` genérico).
- Campos propios: `viajes.viajes[]` {titulo, destino, categoria, duracion, fecha, precio, texto, incluye, imagen,
  destacado}, `viajes.etiqueta_destacado`, `presupuesto.tipos_viaje`, `presupuesto.boton`, `presupuesto.nota`,
  `contacto.horario[]` {dia, horas}, `contacto.boton`, `testimonios[].nota`.
- Diseño: océano + arena + naranja atardecer, bandas a sangre, títulos en mayúsculas estrechas (DIN del sistema),
  billetes con talón troquelado, ruta punteada, franja de destinos, pie oscuro con el nombre gigante. Detalle en
  `DISEÑO.md`.
- Ejemplo: «Marea Alta Viajes», agencia ficticia de Santander.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD `TravelAgency` y de las preguntas frecuentes,
  `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en
  `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`).
Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.viajes.viajes` con `detalle` tiene su página en `/viajes/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
