# Tío Pollo — App de Recetario y Costeo

App web de una sola página (HTML/CSS/JS puro) para gestionar recetas, ingredientes, proveedores y el costeo (escandallo) de Tío Pollo, un negocio de pollo frito. Corre como artefacto de Claude.ai y guarda sus datos a través de la API de almacenamiento persistente de Claude (`window.storage`).

**Versión actual:** v1.13
**Archivo principal:** `app.html` (autocontenido: HTML + CSS + JS en un solo archivo)

---

## ¿Qué hace la app?

- **Recetas** — catálogo de fichas técnicas (código, categoría, tipo, ingredientes, pasos), con escalado x1/x2/x4/x8 y cálculo automático de costo.
- **Ingredientes** — catálogo maestro de precios (por gramo, litro o unidad).
- **Proveedores** — directorio de proveedores y qué ingredientes provee cada uno.
- **Escandallo** — costeo detallado por receta y vista general de costos de todo el catálogo.
- **Libro de recetas** — genera un libro imprimible/PDF con portada, índice y una receta por página.
- **Impresión** — fichas técnicas individuales, listado de ingredientes, listado de proveedores, todo con encabezado de marca.
- **Modo oscuro** — tema claro/oscuro, con preferencia guardada por dispositivo.
- **Datos compartidos** — todos los que abren la app ven y editan la misma información (pensado para uso del equipo, no solo un usuario).

## Estructura de datos

Toda la información vive en un único objeto `DATA` con tres listas: `ingredients`, `recipes`, `suppliers`. Se guarda serializado como JSON bajo la clave `tio_pollo_data` en el almacenamiento compartido del artefacto. El detalle completo del modelo de datos está en el **Manual Técnico**.

## Convenciones del negocio

- Cantidades en **gramos**, salvo leche/agua/vinagre (litros) y huevo (unidades).
- Salsas Dulce Tentación, Secreta y Verde → terrinas de 60 g. Salsa Picante (Ají) → terrinas de 20 g. El rendimiento en terrinas siempre se redondea hacia abajo.
- Sub-recetas (FT-03, FT-08, FT-11) se usan como ingredientes dentro de otras recetas y su costo se calcula en cascada.

## Documentación

| Documento | Para quién | Contenido |
|---|---|---|
| `Manual_Usuario_Tio_Pollo.docx` | Equipo de cocina / administración | Cómo usar la app día a día: crear recetas, actualizar precios, imprimir, etc. |
| `Manual_Tecnico_Tio_Pollo.docx` | Quien mantenga o extienda la app | Arquitectura, modelo de datos, funciones, almacenamiento, cómo agregar funciones nuevas |
| Este README | Cualquiera | Visión general rápida |

## Historial de versiones (resumen)

- **v1.0 – v1.5**: primera versión funcional — recetas, ingredientes, proveedores, escandallo, impresión, libro de recetas.
- **v1.6 – v1.9**: rediseño de botones y menú lateral (tarjeta blanca flotante sobre rojo), iconos de línea propios, corrección de la barra de navegación móvil (antes se apilaba en vez de quedar en fila), corrección del salto de página en el libro de recetas (antes la primera receta quedaba pegada al índice).
- **v1.10 – v1.11**: encabezados de impresión rediseñados (fondo blanco + línea dorada + tinta oscura) para que impriman bien en cualquier impresora.
- **v1.12**: datos compartidos entre todos los usuarios de la app + modo oscuro completo.
- **v1.13**: quick wins de pulido — transición suave entre vistas, skeleton loader al cargar, estados vacíos de búsqueda con mensaje amable, toasts de guardado diferenciados (éxito en verde / error en rojo).

## Próximos pasos posibles

Ideas evaluadas y no implementadas aún (ver Manual Técnico para detalle de cómo abordarlas):
buscador global (Cmd/Ctrl+K), dashboard de inicio con KPIs, historial de precios de ingredientes, alertas de margen, foto por receta, módulos de inventario y compras.
