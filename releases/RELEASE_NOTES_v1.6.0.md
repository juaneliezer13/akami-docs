## 🌸 Akami K-Beauty — Release v1.6.0

### ✨ Nuevas Secciones Institucionales ("Quiénes Somos", "Valor de Marca" y "Contacto") + Mejoras de Carga Multimedia

Esta versión introduce la experiencia institucional completa de marca en Akami K-Beauty, incorporando las secciones exclusivas de **Quiénes Somos**, **Valor Fundamental de la Marca** y **Contacto**, junto con optimizaciones de reproducción de video y carga de imágenes de alta resolución en el Mini CMS.

---

### 🌟 Novedades y Características Principales

#### 1. 🔘 Navegación Institucional en Barra Superior y Footer
* Botones **Quiénes somos** y **Contacto** integrados en la barra superior (`Navbar.vue`) y en el pie de página (`Footer.vue`), estratégicamente posicionados junto al selector de **Marcas**.
* Totalmente responsivos en dispositivos móviles y de escritorio, con estados visuales activos y soporte para navegación directa (`#quienes-somos`, `#contacto`).
* El logotipo de Akami permite regresar en cualquier momento a la vitrina principal de productos.

#### 2. 🖼️ Banners Institucionales Oficiales Limpios
* Al ingresar a cada sección institucional, el banner superior se actualiza dinámicamente:
  * **Quiénes Somos:** `quienes-somos-desktop.webp` y `quienes-somos-mobile.webp`.
  * **Valor de Marca:** `valor-marca-desktop.webp` y `valor-marca-mobile.webp`.
  * **Contacto:** `contacto-desktop.webp` y `contacto-mobile.webp`.
* Se removieron subtextos superpuestos en los banners de *Quiénes somos* y *Contacto* para preservar la limpieza visual del arte fotográfico y el logotipo blanco de Akami.

#### 3. 🎬 Experiencia Multimedia: Videos con `faststart` y Autoplay Robusto
* **Layout Editorial Dividido (`AboutSection.vue`):**
  * **Columna Izquierda:** Historia, propósito de marca y pilares de autenticidad.
  * **Columna Derecha:** Video `ritual-skincare.mp4` en reproducción continua (`autoplay loop muted playsinline`), sin cajas flotantes superpuestas.
* **Sección Independiente "Valor Fundamental de la Marca":**
  * Segundo video exclusivo `glass-skin.mp4` centrado en el ritual *Glass Skin*.
  * **Los 3 Pilares Filosóficos Oficiales:** **01 / La Sabiduría**, **02 / La Virtud** y **03 / La Salud**.
* **Optimización de Video:** Codificación MP4 con átomo `moov` al inicio (`faststart`) y posters de carga inmediata (`ritual-skincare-poster.jpg/.webp` y `glass-skin-poster.jpg/.webp`).

#### 4. 📞 Nueva Sección Oficial de Contacto (`ContactSection.vue`)
* Canales de atención directa con tarjetas interactivas hacia WhatsApp Business, Instagram oficial (`@akami.kbeauty`), correo electrónico, horario de atención y preguntas frecuentes de compra y envíos.

#### 5. 📤 Mejoras en Carga de Imágenes (Mini CMS, Nginx y PHP API)
* **Nginx (`/uploads/`):** Prioridad explícita `location ^~ /uploads/` sobre bloques regex de archivos estáticos para evitar bloqueos 404 en imágenes subidas dinámicamente.
* **Mini CMS (`ProductsAdmin.vue`):** Soporte completo de **Drag-and-Drop** (arrastrar y soltar) para carga de fotografías de productos y fallback automático en caso de error de carga en `ProductCard.vue` y `ProductDetailModal.vue`.
* **Backend (`akami-api`):** Ampliación de límites `upload_max_filesize` y `post_max_size` a **25 MB** en `php.ini` dentro del Dockerfile para admitir fotografías de estudio en alta resolución.

---

### 🐳 Imágenes Docker
* `juaneliezer13/akamikbeauty:v1.6.0` / `juaneliezer13/akamikbeauty:latest`
* `juaneliezer13/akami-api:latest`
