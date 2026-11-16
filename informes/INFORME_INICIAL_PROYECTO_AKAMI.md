# 📊 Informe Técnico y Ejecutivo — Proyecto Akami K-Beauty

**Proyecto:** Akami K-Beauty (Vitrina Web, Catálogo Digital SPA & Mini CMS)  
**Cliente:** Akami C.A.  
**Estado Actual:** Producción Estable (`v1.6.0` — Frontend Puerto `16001` / Backend API Puerto `15001`)  

---

## 1. 🎯 Objetivos y Alcance del Proyecto

El proyecto dota a la marca **Akami K-Beauty** de una plataforma web de cosmética coreana con diseño editorial de alta gama (*clean skincare*), optimizada para tráfico proveniente de dispositivos móviles e Instagram (`@akami.kbeauty`), con gestión autónoma mediante un **Mini CMS** integrado y cierre de ventas asistido por **WhatsApp Business**.

### 📌 Decisiones Clave de Negocio:
1. **Catálogo Vitrina con Cierre en WhatsApp Business:**
   Cada producto cuenta con acción directa (**"Comprar"** / **"Comprar por WhatsApp"**) que envía el pedido preconfigurado con marca, nombre y precio en USD para concretar la venta de forma personalizada.
2. **Navegación Dual + Secciones Institucionales:**
   Organización reactiva por **Categoría de Producto** (8 categorías) y por **Tipo de Piel** (5 necesidades), selector lateral de **Marcas** (19 marcas oficiales) y secciones dedicadas de **Quiénes somos**, **Valor de marca** y **Contacto**.

---

## 2. 🎨 Diseño UI/UX y Activos Multimedia

* **Prototipo Base Validado:** Figma Make ([https://bottom-rapid-26566161.figma.site/](https://bottom-rapid-26566161.figma.site/)).
* **Tipografía Oficial:** Familia completa `Vastago Grotesk` (`.otf`).
* **Banners Oficiales:** 17 pares de banners responsivos (`desktop` + `mobile` en WebP) con logotipo corporativo blanco y copys editoriales por categoría y tipo de piel.
* **Videos Institucionales:** `ritual-skincare.mp4` y `glass-skin.mp4` codificados con `faststart` (`moov` atom al inicio) y posters de carga inmediata.

---

## 3. 🏗️ Arquitectura Técnica de Producción

* **Frontend (`akamikbeauty` — Puerto `16001`):** Vue 3 (Composition API, `<script setup>`), TypeScript, Vite, Tailwind CSS y contenedor `nginx:alpine` con bloque prioritario `^~ /uploads/` y proxy inverso hacia `/api/`.
* **Backend (`akami-api` — Puerto `15001`):** Microservicio RESTful en PHP 8.2 (`php:8.2-cli-alpine`) con PDO SQLite en modo WAL (`database/akami.sqlite`), autenticación Bearer (`akami` / `akami2026`), auto-seeding y subida de imágenes de hasta 25 MB.
* **Almacenamiento Persistente:**
  * `database/akami.sqlite`: Base de datos relacional activa con 83 productos oficiales, marcas, categorías y usuarios.
  * `uploads/products/`: Almacenamiento desacoplado de fotografías de productos con soporte Drag-and-Drop desde el Mini CMS (`#admin`).

---

## 4. 📋 Matriz de Entregables Consolidados en `akami-docs`

| Entregable | Ubicación en `akami-docs` | Estado |
| :--- | :--- | :---: |
| Índice General y Arquitectura del Ecosistema | `README.md` | ✅ **Completado** |
| Normas Técnicas y Directrices para IA/Desarrollo | `NORMAS_TECNICAS.md` | ✅ **Completado** |
| Especificación de Requerimientos y Audios | `business/requerimientos_cliente.md` | ✅ **Completado** |
| Especificación de Diseño y Tokens UI/UX | `business/diseno_figma.md` | ✅ **Completado** |
| Catálogo Maestro Reconciliado (MD, JSON y CSV) | `business/catalogo_productos.*` | ✅ **Completado** |
| Guías de Despliegue AWS EC2, Docker y Staging | `deploy/` | ✅ **Completado** |
| Historial de Versiones (`v1.1.0` a `v1.6.0`) | `releases/` | ✅ **Completado** |
| Activos Fuente Optimizados y Estandarizados | `assets/` | ✅ **Completado** |
