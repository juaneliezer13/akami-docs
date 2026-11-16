## 🌸 Release v1.1.0 — Reconciliación de Catálogo Oficial, Marca ANUA y Arquitectura Modular

### 📌 Resumen de Cambios
Esta versión consolida la base de datos oficial del catálogo vitrina de **Akami K-Beauty**, reincorpora la marca **ANUA** con sus productos oficiales, establece las normas técnicas obligatorias del proyecto y refactoriza la arquitectura de componentes frontend para máxima legibilidad y modularidad.

---

### 🚀 Novedades y Mejoras Principales

#### 1. Reconciliación del Catálogo Oficial
* **Reincorporación de ANUA**: Se agregaron los productos oficiales de la marca ANUA según la lista de precios oficial.
* **Precios oficiales en USD**: Reconciliados al 100% con `lista-precios-akami-actualizada.pdf` (83 productos oficiales auditados y coincidentes).

#### 2. Política de Imágenes Vacías (Coordinación con Diseñadora)
* Se eliminaron dependencias de bancos de imágenes externas (Unsplash) y no se utilizan imágenes por IA.
* Los productos sin fotografía oficial muestran un contenedor limpio con fondo neutro de marca e identificador tipográfico, listos para recibir las fotos de la diseñadora (proporción 1:1, 800x800px, <150 KB).

#### 3. Refactorización de Arquitectura y Componentes
* Se extrajeron componentes modulares, tipados y autocontenidos:
  * `Navbar.vue`: Búsqueda, logo y botón de acceso a marcas.
  * `HeroBanner.vue`: Banner dinámico responsivo por categoría/piel.
  * `FilterSection.vue`: Selector de descubrimiento y navegación por pills.
  * `ProductCard.vue`: Tarjeta de producto con foto o espacio vacío.
  * `ProductDetailModal.vue`: Ficha técnica modal con acordeones y galería.
  * `BrandsDrawer.vue`: Drawer lateral con las marcas y conteo de productos.
  * `ConsultationBanner.vue`: Banner de asesoría directa por WhatsApp.
  * `Footer.vue`: Pie de página minimalista.

#### 4. Base de Datos Estructurada en CSV y JSON
* Exportación de `catalogo_productos.csv` (UTF-8 con BOM) y `catalogo_productos.json` con el diccionario de datos completo.

#### 5. Respaldo de Docker Compose del Servidor
* Respaldo oficial en `docker-compose.server.yml` documentando la configuración del servidor de producción.

#### 6. Normas Técnicas Instituidas
* Publicación de `NORMAS_TECNICAS.md` blindando la tipografía Vástago Grotesk, la paleta cromática, la política de imágenes y el manejo de activos.
