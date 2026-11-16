# 📜 NORMAS TÉCNICAS, REGLAS DE NEGOCIO Y CONTEXTO PARA IA — AKAMI K-BEAUTY

Este documento reúne las directrices técnicas, arquitectónicas y de negocio obligatorias para el mantenimiento, actualización e iteración de la plataforma **Akami K-Beauty**. Tanto los desarrolladores como los agentes y modelos de Inteligencia Artificial deben seguir estrictamente estas normas.

---

## 1. 🏗️ Arquitectura Actual del Ecosistema (v1.6.0+)

El workspace de **Akami K-Beauty** está compuesto por tres repositorios principales y dos directorios de persistencia desacoplada:

| Componente | Ruta en Workspace | Tecnología / Propósito | Puerto Host |
| :--- | :--- | :--- | :---: |
| **Frontend Web SPA** | `akamikbeauty/` | Vue 3 + TypeScript + Vite + Tailwind CSS + Nginx Alpine (`juaneliezer13/akamikbeauty:latest`) | `17001` |
| **Backend REST API** | `akami-api/` | PHP 8.2 CLI Alpine + PDO SQLite WAL (`juaneliezer13/akami-api:latest`) | `16001` |
| **Documentación y Activos** | `akami-docs/` | Documentación técnica, reglas de negocio, releases y activos optimizados | N/A |
| **Base de Datos Activa** | `database/` | Contiene **únicamente** `akami.sqlite` (83 productos, 20 marcas, 8 categorías) | Volumen Docker |
| **Medios Desacoplados** | `uploads/products/` | Fotografías de productos servidas por Nginx (`^~ /uploads/`) y gestionadas por el CMS | Volumen Docker |

### Reglas de Infraestructura y Contenedores
1. **Puertos Estándar:** Frontend en **`17001`** (`FRONT_PORT`) y Backend en **`16001`** (`BACK_PORT`), conectados mediante la red bridge `akami_network`.
2. **Servido de Imágenes en Nginx (`akamikbeauty/nginx.conf`):** El bloque `location ^~ /uploads/` utiliza el modificador `^~` para tener prioridad absoluta sobre la expresión regular de archivos estáticos (`.jpg`, `.webp`, `.png`), garantizando que las imágenes subidas al volumen `/usr/share/nginx/uploads/` nunca devuelvan error 404.
3. **Límite de Subida en PHP (`akami-api/Dockerfile`):** Configurado en `25M` (`upload_max_filesize = 25M` y `post_max_size = 25M`) para soportar fotografías de estudio en alta resolución subidas mediante clic o Drag-and-Drop en el Mini CMS (`#admin`).
4. **Limpieza de `database/`:** En la carpeta `/database` solo debe residir el archivo `akami.sqlite` (y sus archivos temporales de transacciones `-wal` / `-shm` generados por SQLite). Las exportaciones documentales (`catalogo_productos.json` y `catalogo_productos.csv`) viven en `akami-docs/business/`, y la semilla del backend vive en `akami-api/src/data/productos.json`.

---

## 2. 📑 Fuentes Oficiales de Verdad del Catálogo y Precios

### Documentos Maestros (`akami-docs/assets/documents/`)
1. **Lista de Precios Oficial (Referencia Principal):**
   * **Archivo:** `lista-precios-akami-actualizada.pdf` (en `akami-docs/assets/documents/`).
   * **Propósito:** Es la **fuente de verdad principal y obligatoria** para nombres de producto, marcas, variantes (caja e individual) y precios de venta al público en USD (`$`).
   * **Obligatoriedad:** Ningún precio puede inventarse ni alterarse fuera de lo estipulado por la cliente o el Mini CMS oficial.
2. **Estructura Web por Categorías (Referencia de Taxonomía):**
   * **Archivo:** `estructura-web-categorias-inventario.pdf` (en `akami-docs/assets/documents/`).
   * **Propósito:** Define la asignación de las **8 categorías de producto** (*Limpiadores, Tónicos & Esencias, Sérums, Hidratantes, Protector Solar, Mascarillas, Ojos & Labios, Dispositivos & Sets*) y los **5 tipos/necesidades de piel** (*Tendencia al Acné, Piel Grasa/Mixta, Piel Seca, Piel Sensible/Rojeces, Antimanchas*).

### Regla de Inclusión Obligatoria
* **Disponibilidad:** La falta temporal de stock físico de un producto **NO** es motivo para eliminarlo del catálogo base; su visibilidad pública se controla dinámicamente mediante el campo `is_active` (`1` = visible, `0` = oculto) en el Mini CMS (`#admin`).

---

## 3. 🖼️ Política de Imágenes, Videos y Activos Estandarizados

### Regla del Espacio Vacío y Fallback Visual (Sin Imágenes Falsas)
* Si no se dispone de la fotografía oficial de un producto o ocurre un error de carga, los componentes `ProductCard.vue` y `ProductDetailModal.vue` muestran automáticamente el **fallback visual limpio de marca** con fondo neutro suave e identificador tipográfico.
* **Queda terminantemente prohibido:**
  1. ❌ Colocar imágenes que no correspondan al producto exacto.
  2. ❌ Generar fotografías de productos con Inteligencia Artificial.
  3. ❌ Usar imágenes de bancos externos (Unsplash, Pexels, etc.).

### Estándar de Activos en `akami-docs/assets/`
Todos los activos iniciales compartidos por la cliente han sido optimizados a formato **WebP** y estandarizados bajo nomenclatura `kebab-case` (sin espacios, tildes ni nombres genéricos):
* **`assets/products/<marca>/<marca>-<producto>.webp`:** Fotografías base organizadas en 16 carpetas de marca (`anua`, `celimax`, `cosrx`, `dr-althea`, `dr-melaxin`, `haruharu-wonder`, `heimish`, `medicube`, `mixsoon`, `numbuzin`, `purito`, `round-lab`, `skin1004`, `stage`, `tocobo`, `vt-cosmetics`), máx. 800x800 px (relación 1:1).
* **`assets/banners/`:** Organizados en:
  * `institucional/` (`principal`, `quienes-somos`, `valor-de-marca`, `contacto`)
  * `categorias/` (`limpiadores`, `tonicos`, `serums`, `hidratantes`, `protectores`, `mascarillas`, `ojos-y-labios`, `dispositivos-y-sets`, `antimanchas`)
  * `tipos-de-piel/` (`acne`, `grasa-mixta`, `piel-seca`, `piel-sensible`)
  Cada carpeta contiene las variantes limpias (`<slug>-desktop.webp` y `<slug>-mobile.webp`) y sus mockups de referencia tipográfica (`<slug>-mockup-16x9.webp` y `<slug>-mockup-1x1.webp`).
* **`assets/videos/`:** Videos editoriales `ritual-skincare.mp4` y `glass-skin.mp4` codificados con `faststart` (`moov` atom al inicio para reproducción instantánea en móviles) y sus respectivos posters `.webp`.
* **`assets/brand/`:** Isologo vectorial (`akami-isologo.svg`), logotipos (`akami-logo-principal.png`, `akami-logo-blanco.png`, variantes `01` y `02`), láminas del manual de paleta cromática (`manual-paleta-colores-01.webp` a `06.webp`) y artes de referencia institucional.

---

## 4. ✍️ Inviolabilidad de la Tipografía (Vastago Grotesk)

* **Prohibición de Cambio de Fuentes:** No sustituir la tipografía corporativa configurada en el proyecto.
* **Fuente Oficial:** `Vastago Grotesk` (`akami-docs/assets/fonts/VastagoGrotesk-*.otf`, 9 pesos de `Thin` 100 a `Black` 900).
* **Implementación:** Las reglas `@font-face` en `akamikbeauty/src/style.css` y la configuración en `akamikbeauty/tailwind.config.js` son definitivas.

---

## 5. 🎨 Línea de Diseño, Secciones y Paleta Cromática

* **Paleta Oficial UI Web:**
  * **Ivory (Fondo Principal):** `#FCFBF7` / `#FAF8F5`
  * **Surface (Contenedores / Blanco Puro):** `#FFFFFF`
  * **Ink (Tipografía Principal y Botones):** `#1A1918`
  * **Blush (Fondos Suaves y Badges):** `#F5EBE6`
  * **Blush Border:** `#EAD8D0`
  * **Line (Divisores):** `#EAE6DF`
  * **Muted (Textos Secundarios):** `#8C827A` / `#5C554E`
  * **Accent Rose:** `#C27A72`
  * **Verde Bosque Corporativo (Manual de Marca):** `#2F4D40` | **Salvia:** `#A7B095`
  * **WhatsApp Oficial:** `#25D366`
* **Reglas de Interfaz Vigentes:**
  1. Los botones de conversión en tarjetas y modal de producto utilizan el texto **"Comprar"** / **"Comprar por WhatsApp"** (nunca *"Consultar"*).
  2. Los banners de **Quiénes somos** y **Contacto** no llevan subtexto superpuesto.
  3. Los videos en **Quiénes somos** (`AboutSection.vue`) se reproducen limpios sin cajas de texto flotantes encima.

---

*Documento oficial actualizado y en vigencia técnica para todo el desarrollo y asistencia por IA de Akami K-Beauty.*
