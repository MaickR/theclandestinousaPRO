# Sistema visual de The Clandestino

Este documento define la dirección visual para las interfaces del proyecto. Describe decisiones de diseño; Tailwind CSS las implementa y los componentes locales de shadcn/ui proporcionan primitives accesibles y editables.

## Dirección de marca

La interfaz extiende la experiencia física de The Clandestino: cultura española del vino y la gastronomía, intimidad, calidez, autenticidad y sofisticación hospitalaria. Su carácter es premium y editorial, con fotografía expresiva, buena legibilidad y espacio para disfrutar del contenido.

Evitar la apariencia de SaaS o ecommerce genérico, el lujo frío, la ornamentación excesiva, los acentos dorados dominantes y las composiciones recargadas.

## Color

| Token de marca      | Valor     | Rol                                                        |
| ------------------- | --------- | ---------------------------------------------------------- |
| Fondo               | `#161616` | Fondo principal oscuro.                                    |
| Superficie profunda | `#0E0D0B` | Contraste profundo y zonas de énfasis oscuro.              |
| Superficie          | `#121111` | Superficies secundarias sobre el fondo.                    |
| Superficie elevada  | `#1B1C1D` | Contenido agrupado y elementos elevados.                   |
| Superficie alta     | `#212121` | Variación de superficie para separar niveles.              |
| Oro de marca        | `#DDDABA` | Identidad, detalles editoriales y acentos discretos.       |
| Oro comercial       | `#D4AF37` | Llamadas a la acción o énfasis comercial puntual.          |
| Bronce              | `#CD7F32` | Acento cálido secundario cuando el contexto lo justifique. |
| Texto principal     | `#FFFFFF` | Texto sobre superficies oscuras.                           |
| Texto secundario    | `#A6A6A6` | Información de menor jerarquía que siga siendo legible.    |

El oro de marca y el oro comercial tienen funciones distintas: no son intercambiables por defecto. Reserva oro y bronce para acentos; no los uses como fondos dominantes ni para decorar cada control. Los bordes deben separar contenido con discreción y no convertir cada elemento en una caja.

Los estados funcionales (error, advertencia, éxito e información) deben reconocerse con texto, iconografía o forma además del color. No se fijan aquí valores cromáticos nuevos: su paleta queda pendiente de definir al implementar estados reales y verificar contraste.

## Tipografía

- **Libre Bodoni:** headings, titulares display y momentos editoriales con impacto.
- **Playfair Display:** acentos de branding, citas y detalles editoriales; no usarla para toda la interfaz funcional.
- **Sans-serif de interfaz:** navegación, botones, formularios, labels, datos y lectura densa. El proyecto carga actualmente Instrument Sans como sans-serif funcional.

Jerarquía recomendada:

1. **Display:** mensaje editorial principal, breve y con presencia.
2. **H1:** título único y claro de la página o sección principal.
3. **H2 / H3:** estructura de secciones, con tamaño y peso descendentes.
4. **Body:** lectura cómoda para descripciones y contenido.
5. **Secondary:** metadatos y explicaciones complementarias, sin perder legibilidad.
6. **Label / Caption:** texto funcional breve; priorizar claridad sobre ornamento.

Usa tamaños responsivos y una jerarquía consistente. Los tamaños exactos se ajustarán con el sistema visual y el contenido real; evita escalas tipográficas nuevas sin necesidad.

## Composición y responsive

- Prioriza jerarquía, legibilidad y ritmo editorial. Alterna contenido, fotografía y espacio negativo con intención.
- Usa contenedores de ancho controlado, alineaciones claras y grids que respondan al contenido.
- Mantén párrafos y líneas de lectura en longitudes cómodas; en pantallas amplias no estires el contenido sin límite.
- En móvil, prioriza lectura, navegación sencilla y acciones identificables. En tablet, adapta grids y proporciones. En desktop, permite composiciones editoriales más ricas sin perder foco.
- Da espacio suficiente entre secciones y grupos relacionados. La densidad debe responder a la tarea, no a llenar el viewport.
- Usa los breakpoints responsive disponibles en Tailwind; introduce otros solo ante una necesidad comprobada.

## Fotografía y contenido visual

Usa imágenes auténticas de vino, tapas, gastronomía, personas compartiendo la mesa, manos y momentos sociales. Prefiere luz cálida e íntima, textura y contexto real. Cuando la historia lo pida, transmite la experiencia del restaurante además de mostrar el producto.

Evita fotografías genéricas de stock, imágenes artificiales o sobreprocesadas, saturación excesiva y fotografías de producto aisladas cuando no sirvan al contexto.

## Componentes y composición

- `resources/js/components/ui/` contiene primitives locales basados en shadcn/ui: accesibles, reutilizables y relativamente independientes del negocio. Extiéndelos cuando la variante sea genérica; compónlos desde fuera para necesidades específicas de una feature.
- No dupliques un primitive ni conviertas `components/ui/` en un catálogo de componentes de negocio.
- Crea `resources/js/components/marca/` solo cuando exista una necesidad repetida de identidad propia. No mantengas esa carpeta vacía.
- Las páginas componen componentes y presentan datos de Laravel/Inertia. Evita bloques monolíticos de JSX y clases Tailwind difíciles de mantener; divide la composición cuando mejore la comprensión o reutilización.
- Tailwind CSS es el sistema principal de estilos. No mezcles Bootstrap, SCSS 7-1 ni otro framework CSS. Mantén los estilos globales en `resources/css/app.css`; añade CSS específico solo si una necesidad técnica real no se expresa adecuadamente con Tailwind o composición.

## Estados, accesibilidad y movimiento

Los estados default, hover, active, disabled, loading, error y success deben comunicar su función con claridad. Usa `focus-visible` perceptible y no dependas únicamente del color para transmitir estado. Los controles deben conservar labels y semántica adecuados.

La accesibilidad tiene prioridad sobre la ornamentación: objetivo WCAG 2.1 AA, contraste suficiente, teclado funcional, foco visible, HTML semántico y objetivos táctiles razonables. Añade ARIA cuando la semántica nativa no baste.

El movimiento debe ser breve y funcional, normalmente alrededor de 180–250 ms para microinteracciones. Evita animaciones decorativas dominantes y respeta `prefers-reduced-motion`.

## Criterios de diseño

**Hacer:** dar prioridad a la tipografía y la fotografía, usar acentos de marca con mesura, preservar contraste y espacio negativo, y mantener consistencia entre páginas.

**Evitar:** saturar la interfaz de dorado, usar gradientes o sombras llamativas sin motivo, añadir tarjetas y bordes a cada bloque, incorporar tipografías decorativas sin decisión de marca, llenar la interfaz de animaciones, duplicar componentes o sacrificar accesibilidad.

Estos principios deben servir a futuras áreas del producto sin definir sus páginas ni sus componentes antes de que existan.

## Relación con las fuentes del proyecto

`AGENTS.md` rige el proceso y las decisiones de ingeniería; este documento rige el lenguaje visual. La configuración CSS actual todavía contiene el tema genérico del starter y carga Instrument Sans. Al implementar el sistema visual, alinea los tokens CSS/Tailwind con los valores de marca definidos aquí y conserva esta correspondencia como fuente visual única.
