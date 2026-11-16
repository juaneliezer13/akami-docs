# 📋 Requerimientos del Cliente y Reglas de Negocio — Akami K-Beauty

Este documento consolida y formaliza todos los requerimientos funcionales, directrices estéticas, reglas de interacción y evoluciones funcionales implementadas para la plataforma **Akami K-Beauty**.

---

## 🎙️ Transcripción y Análisis de Requerimientos Iniciales

Los audios originales se encuentran estandarizados en `assets/audio/`:
* `requerimiento-01-vision-general.ogg`
* `requerimiento-02-navegacion-categorias.ogg`

### 1. Mensaje de Visión General del Negocio (`requerimiento-01-vision-general.ogg`)
> *"Mari, Para la página de Akami no quiero un e-commerce complejo con pasarela de pago ni procesamiento de tarjetas online por ahora. Queremos un Catálogo Web estilo vitrina, que sea súper estético, limpio y fácil de navegar desde el celular. Lo que necesitamos es que la gente pueda ver los productos con sus fotos, precios y descripciones, y que al hacer clic en 'Comprar' o 'Consultar', los redirija automáticamente a nuestro WhatsApp Business con el pedido listo para cerrar la venta directamente por ahí."*

### 2. Mensaje de Jerarquía y Arquitectura de Navegación (`requerimiento-02-navegacion-categorias.ogg`)
> *"Bueno Mari, me gusta la idea de tener las Marcas súper visibles en el menú desplegable para las que buscan una en específico, pero necesito que la barra principal organice los productos por Tipo de Producto ejemplo protectores Solares, Sérums, Limpiadores etc.. y también por Tipo de Piel. Así las clientas que no conocen las marcas coreanas pueden comprar según lo que su piel necesita."*

---

## 💎 Directrices del Modelo de Negocio (K-Beauty Vitrina + Mini CMS)

### Por qué un Catálogo Vitrina con Cierre en WhatsApp Business
1. **Cero Fricción de Pago en Venezuela / LATAM:** Evita comisiones bancarias, rechazos de tarjetas internacionales y abandono de carrito.
2. **Naturaleza Consultiva del Skincare Coreano:** Permite asesorar al cliente sobre compatibilidad de activos (ej. retinoides, vitamina C, ácidos exfoliantes y doble limpieza).
3. **Cierre de Ventas Asistido en WhatsApp Business (`+58 414-9025118`):**
   * El cliente llega desde el botón **"Comprar"** con el producto exacto, marca y precio en USD pre-cargados en el mensaje.
   * La asesora de Akami confirma disponibilidad, sugiere productos complementarios (*upselling*), coordina métodos de pago flexibles (Zelle, Pago Móvil, Efectivo USD, Binance USDT) y gestiona el envío o retiro.

---

## 📱 Reglas Funcionales y de Interacción

### RF-01: Experiencia Mobile-First y Navegación Institucional
* Optimizada para tráfico móvil proveniente de Instagram (`@akami.kbeauty`).
* **Barra de Navegación Superior (`Navbar.vue`):**
  * Enlaces directos a **Quiénes somos** (`#quienes-somos`), **Contacto** (`#contacto`) y **Marcas** (Drawer lateral).
  * Buscador instantáneo en tiempo real por nombre, marca, categoría o ingrediente activo.
  * Logotipo oficial de Akami con retorno directo a la vitrina principal.

### RF-02: Filtros Reactivos Simultáneos y Banners Dinámicos
El usuario puede explorar los **83 productos oficiales y 19 marcas** de 3 formas complementarias sin recargar la página:
1. **Por Tipo de Producto (8 categorías + Todos):** `Todos`, `Limpiadores`, `Tónicos & Esencias`, `Sérums`, `Hidratantes`, `Protector Solar`, `Mascarillas`, `Ojos & Labios`, `Dispositivos & Sets`.
2. **Por Tipo de Piel (5 necesidades + Todos):** `Todos`, `Tendencia al Acné`, `Piel Grasa/Mixta`, `Piel Seca`, `Piel Sensible/Rojeces`, `Antimanchas`.
3. **Por Marca:** Drawer deslizable con listado de marcas coreanas y contador dinámico de productos.
* Cada categoría, tipo de piel y sección institucional actualiza dinámicamente el **Hero Banner** (en formato WebP responsivo para Desktop y Mobile) con el logotipo blanco de Akami en la esquina superior derecha.

### RF-03: Ficha Detallada de Producto (`ProductDetailModal.vue`)
* Galería fotográfica con soporte de fallback automático en caso de imagen ausente o en proceso de carga.
* Insignias de compatibilidad, marca, título oficial y precio en USD (`$`).
* Acordeones informativos desplegables: **Beneficios**, **Ingredientes Clave** y **Modo de Uso**.
* Botón de acción principal (*CTA*): **"Comprar"** en tarjetas de catálogo y **"Comprar por WhatsApp"** en el modal de detalle.

### RF-04: Secciones Institucionales ("Quiénes Somos", "Valor de Marca" y "Contacto")
* **Quiénes Somos (`AboutSection.vue`):**
  * Banner oficial dedicado (`quienes-somos-desktop.webp` / `quienes-somos-mobile.webp`) limpio sin subtexto superpuesto.
  * Layout editorial dividido con historia de marca y video en bucle continuo (`ritual-skincare.mp4` codificado con `faststart` y poster JPEG, sin cajas de texto flotantes sobre el video).
* **Valor Fundamental de la Marca:**
  * Segundo video exclusivo (`glass-skin.mp4`) enfocado en el ritual *Glass Skin*.
  * Presentación de los 3 pilares filosóficos: **01 / La Sabiduría**, **02 / La Virtud** y **03 / La Salud**.
* **Contacto (`ContactSection.vue`):**
  * Banner oficial dedicado (`contacto-desktop.webp` / `contacto-mobile.webp`) limpio sin subtexto.
  * Tarjetas de contacto directo a WhatsApp Business, Instagram (`@akami.kbeauty`), correo electrónico, ubicación, horario de atención y preguntas frecuentes.

### RF-05: Mini CMS Administrativo Integrado (`#admin`)
* Acceso protegido mediante login con token Bearer (`akami` / `akami2026`).
* **Gestión de Productos (`ProductsAdmin.vue`):**
  * Crear, editar, activar/ocultar (`is_active`) y eliminar productos en tiempo real.
  * Subida de imágenes mediante selector de archivos o **Drag-and-Drop** (arrastrar y soltar), con soporte de archivos de alta resolución de hasta **25 MB** en el backend PHP y almacenamiento desacoplado en `/uploads/products/`.
* **Gestión de Marcas y Categorías:** CRUD completo sincronizado con la base de datos SQLite.

---

## ⚡ Requerimientos No Funcionales y Arquitectura Desacoplada

1. **Frontend SPA (`akamikbeauty` — Puerto `16001`):**
   * Construido en Vue 3 + TypeScript + Vite + Tailwind CSS, servido mediante `nginx:alpine` con compresión Gzip, caché de activos y bloque prioritario `location ^~ /uploads/` para servir fotografías dinámicas sin conflictos de regex.
2. **Backend RESTful API (`akami-api` — Puerto `15001`):**
   * Microservicio en PHP 8.2 (`php:8.2-cli-alpine`) con PDO SQLite en modo WAL (`database/akami.sqlite`), auto-seeding inicial de los 83 productos oficiales y límite de carga de 25 MB.
