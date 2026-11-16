# 🎨 Especificación de Diseño UI/UX y Sistema Visual — Akami K-Beauty

* **Prototipo Interactivo Base (Figma Make):** [https://bottom-rapid-26566161.figma.site/](https://bottom-rapid-26566161.figma.site/)
* **Nombre de la Plataforma:** *Akami K-Beauty — Catálogo Digital & Vitrina Web*
* **Estilo Visual:** Minimalismo Coreano Editorial (*Clean K-Beauty*), tonos marfil/blush y tipografía corporativa **Vastago Grotesk**.

---

## 🌸 1. Sistema de Diseño y Tokens Visuales

### Paleta Cromática Oficial (Manual de Identidad y UI Web)

Los manuales originales de paleta de colores se encuentran estandarizados en `assets/brand/manual-paleta-colores-01.webp` al `06.webp`.

| Token / Variable | Código HEX | Nombre / Descripción | Uso Principal |
| :--- | :--- | :--- | :--- |
| `--ivory` / Fondo | `#FCFBF7` / `#FAF8F5` | **Marfil Base** | Fondo principal general del catálogo |
| `--surface` | `#FFFFFF` | **Blanco Superficie** | Tarjetas de producto, modales y paneles del CMS |
| `--ink` | `#1A1918` | **Tinta Principal** | Tipografía principal y botones de acción primarios |
| `--blush` | `#F5EBE6` | **Rubor Suave** | Fondos suaves, badges y estados activos |
| `--blush-border` | `#EAD8D0` | **Borde Rubor** | Bordes delicados de componentes destacados |
| `--line` | `#EAE6DF` | **Línea Divisoria** | Divisores y bordes sutiles de tarjetas |
| `--muted` | `#8C827A` | **Texto Secundario** | Subtítulos, metadatos y textos de apoyo |
| `--accent-rose` | `#C27A72` | **Terracota / Rose** | Acentos K-Beauty e indicadores interactivos |
| `--brand-primary` | `#2F4D40` | **Verde Bosque Akami** | Identidad corporativa en manual de marca |
| `--brand-sage` | `#A7B095` | **Verde Salvia Suave** | Acento botánico secundario de identidad |
| `--whatsapp` | `#25D366` | **Verde WhatsApp** | Botones de compra y contacto directo |

### Tipografía Oficial: Vastago Grotesk (`assets/fonts/*.otf`)

La aplicación integra los 9 pesos vectoriales originales de **Vastago Grotesk**:
* `VastagoGrotesk-Thin.otf` (100)
* `VastagoGrotesk-ExtraLight.otf` (200)
* `VastagoGrotesk-Light.otf` (300)
* `VastagoGrotesk-Regular.otf` (400)
* `VastagoGrotesk-Medium.otf` (500)
* `VastagoGrotesk-SemiBold.otf` (600)
* `VastagoGrotesk-Bold.otf` (700)
* `VastagoGrotesk-Heavy.otf` (800)
* `VastagoGrotesk-Black.otf` (900)

---

## 📐 2. Arquitectura de Componentes y Pantallas

### 1. Cabecera y Navegación (`Navbar.vue`)
* **Logo Corporativo:** Logotipo oficial de Akami con regreso instantáneo a la vitrina de catálogo.
* **Enlaces de Navegación:**
  * **Quiénes somos** (`#quienes-somos`)
  * **Contacto** (`#contacto`)
  * **Marcas** (abre el `BrandsDrawer.vue` con las marcas activas y conteo de productos)
* **Buscador Reactivo:** Filtrado instantáneo por título, marca, categoría o ingrediente.

### 2. Hero Editorial Dinámico (`HeroBanner.vue` y `src/data/banners.ts`)
* **17 Pares de Banners Oficiales en WebP (`desktop` + `mobile`):**
  * **Institucionales (`assets/banners/institucional/`):**
    * `principal` (*Todos*): *"Tu piel, más luminosa"* — *"Descubre el ritual coreano que habla el idioma de tu piel."*
    * `quienes-somos`: Título *"Quiénes somos"* (sin subtexto superpuesto).
    * `valor-de-marca`: Título *"Valor de marca"*.
    * `contacto`: Título *"Contacto"* (sin subtexto superpuesto).
  * **Por Categoría (`assets/banners/categorias/`):**
    * `limpiadores`: *"Pureza y calma"*
    * `tonicos`: *"Gotas de equilibrio"*
    * `serums`: *"Concentrados de luz"*
    * `hidratantes`: *"Glass skin diaria"*
    * `protectores`: *"Tu velo protector"*
    * `mascarillas`: *"Ritual de desconexión"*
    * `ojos-y-labios`: *"Cuidado delicado"*
    * `dispositivos-y-sets`: *"Sets y accesorios"*
  * **Por Tipo de Piel (`assets/banners/tipos-de-piel/`):**
    * `acne`: *"Claridad y paciencia"*
    * `grasa-mixta`: *"Armonía y confort"*
    * `piel-seca`: *"Abrazo de nutrición"*
    * `piel-sensible`: *"Caricia reconfortante"*
    * `antimanchas` (en `categorias/antimanchas`): *"Tono uniforme y glow"*
* **Identidad en Banner:** Logotipo oficial en blanco (`akami-logo-blanco.png`) ubicado en la esquina superior derecha con `drop-shadow` suave y superposición `.catalog-hero-overlay` para contraste óptimo.

### 3. Secciones Institucionales
* **Quiénes Somos y Valor de Marca (`AboutSection.vue`):**
  * Diseño editorial dividido con historia de marca y reproducción fluida del video `ritual-skincare.mp4` (`autoplay loop muted playsinline`, con `faststart` y poster JPEG, sin cajas de texto flotantes sobre el video).
  * Bloque **Valor Fundamental de la Marca** con el segundo video `glass-skin.mp4` y los 3 pilares: *01 La Sabiduría*, *02 La Virtud* y *03 La Salud*.
* **Contacto (`ContactSection.vue`):**
  * Tarjetas interactivas para WhatsApp Business, Instagram (`@akami.kbeauty`), correo electrónico, ubicación, horario de atención y preguntas frecuentes.

### 4. Cuadrícula y Ficha de Producto (`ProductCard.vue` & `ProductDetailModal.vue`)
* **Tarjetas de Producto:** Proporción 1:1, fallback visual elegante cuando un producto no tiene imagen o falla la carga, precio en USD y botón CTA **"Comprar"**.
* **Modal de Detalle:** Hoja deslizable en móvil (*Bottom Sheet*) y modal centrado en desktop, con acordeones de Beneficios, Ingredientes y Modo de Uso, y botón principal **"Comprar por WhatsApp"**.

### 5. Panel Administrativo Mini CMS (`#admin`)
* Gestión integral de productos, marcas y categorías.
* Zona de carga de imágenes con soporte **Drag-and-Drop** y previsualización instantánea.
