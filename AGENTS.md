# 🤖 Contexto e Instrucciones para Agentes y Modelos de IA — Akami K-Beauty

Este archivo define el contexto arquitectónico, las reglas de negocio y las restricciones técnicas obligatorias para cualquier modelo o agente de Inteligencia Artificial (Gemini / Antigravity, Claude Code, Cursor, GitHub Copilot, Codex) que opere sobre el proyecto **Akami K-Beauty**.

---

## 1. 🗺️ Mapa del Ecosistema (Estado Actual v1.6.0+)

El workspace `akami/` se divide en módulos desacoplados:

1. **`akamikbeauty/` (Frontend Web SPA — Puerto `16001`):**
   * **Stack:** Vue 3 (`<script setup>`, Composition API), TypeScript, Vite, Tailwind CSS, Lucide Icons, servido en producción por `nginx:alpine`.
   * **Vistas y Secciones:**
     * **Vitrina de Catálogo:** Filtros reactivos por Categoría (8), Tipo de Piel (5), Marca (Drawer lateral con 19/20 marcas) y buscador en tiempo real.
     * **Quiénes Somos y Valor de Marca (`src/components/AboutSection.vue`):** Ruta `#quienes-somos`. Incluye banners dedicados sin subtexto, historia de marca, videos `ritual-skincare.mp4` y `glass-skin.mp4` (codificados con `faststart` y posters JPEG/WebP, sin cajas de texto flotantes sobre los videos) y los 3 pilares filosóficos (*01 La Sabiduría*, *02 La Virtud*, *03 La Salud*).
     * **Contacto (`src/components/ContactSection.vue`):** Ruta `#contacto`. Banner dedicado sin subtexto y canales directos (WhatsApp Business `+58 414-9025118`, Instagram `@akami.kbeauty`, correo, ubicación, horario y FAQ).
     * **Mini CMS Administrativo (`src/components/admin/`):** Ruta `#admin`. Login con token Bearer (`akami` / `akami2026`). Gestión CRUD de productos, marcas y categorías, con carga de imágenes por clic o **Drag-and-Drop** y fallback automático de imágenes en tarjetas y modal.
   * **Conversión:** Todos los botones de acción de producto utilizan el texto **"Comprar"** (en `ProductCard.vue`) y **"Comprar por WhatsApp"** (en `ProductDetailModal.vue`).

2. **`akami-api/` (Backend RESTful API — Puerto `15001`):**
   * **Stack:** PHP 8.2 (`php:8.2-cli-alpine`) + PDO SQLite en modo WAL.
   * **Configuración Clave:**
     * Límite de carga en `php.ini` ampliado a **`25M`** (`upload_max_filesize = 25M`, `post_max_size = 25M`) en `Dockerfile` para permitir fotografías de alta resolución.
     * Auto-seeding (`src/Seeder.php`) desde `src/data/productos.json` (83 productos oficiales) cuando la base de datos se inicializa desde cero.

3. **`database/` (Persistencia SQLite):**
   * Contiene **únicamente** la base de datos activa `akami.sqlite` (y sus archivos de control WAL/SHM).
   * **PROHIBIDO** agregar scripts de prueba o archivos redundantes en `database/`, y **PROHIBIDO** eliminar o sobrescribir `akami.sqlite`.

4. **`uploads/products/` (Medios Desacoplados):**
   * Almacena las imágenes de productos subidas o servidas dinámicamente.
   * En `akamikbeauty/nginx.conf`, la ubicación `location ^~ /uploads/` tiene prioridad explícita sobre los bloques regex de extensiones estáticas para evitar bloqueos 404.

5. **`akami-docs/` (Repositorio de Documentación y Activos Estandarizados):**
   * Contiene toda la documentación funcional (`business/`), guías DevOps (`deploy/`), notas de versión (`releases/RELEASE_NOTES_v1.1.0.md` a `v1.6.0.md`), normas (`NORMAS_TECNICAS.md`) y activos optimizados en formato WebP y nomenclatura `kebab-case` dentro de `assets/` (`audio/`, `banners/`, `brand/`, `documents/`, `fonts/`, `products/`, `videos/`).

---

## 2. 🔒 Reglas Estrictas de Desarrollo para Agentes de IA

1. **Inviolabilidad de Precios y Catálogo:**
   * Los precios en USD y nombres de productos provienen exclusivamente de `akami-docs/assets/documents/lista-precios-akami-actualizada.pdf` y la base de datos `database/akami.sqlite`. Nunca inventar precios ni productos.
2. **Política de Imágenes (Cero Imágenes Falsas):**
   * Prohibido usar URLs de Unsplash, Pexels o imágenes generadas por IA para productos. Si un producto no tiene foto o falla su carga, el componente debe renderizar el estado vacío/fallback oficial de marca.
3. **Tipografía y Paleta Intocables:**
   * Mantener siempre la fuente oficial `Vastago Grotesk` y la paleta editorial (`#FCFBF7` Ivory, `#1A1918` Ink, `#F5EBE6` Blush, `#C27A72` Accent Rose, `#2F4D40` Verde Bosque Akami).
4. **Higiene del Workspace:**
   * No recrear carpetas eliminadas como `scripts/` o `recordings/` en la raíz del proyecto ni dejar archivos temporales en `database/`.
5. **Flujo Git y Docker:**
   * Ramas estándar: `main` (producción), `develop` (integración) y `release/vX.Y.Z`.
   * Imágenes Docker Hub: `juaneliezer13/akamikbeauty:latest` y `juaneliezer13/akami-api:latest`.
