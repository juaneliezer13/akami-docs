## 🌸 Akami K-Beauty — Release v1.5.2

### 🛍️ Actualización de Call to Action (CTA): "Comprar"

Esta versión actualiza el texto de los botones principales de llamada a la acción en las tarjetas de productos del catálogo y en la ficha de detalle, cambiando el texto de **"Consultar"** a **"Comprar"** para una intención de compra más directa y clara hacia WhatsApp.

---

### ✨ Cambios Principales

#### 1. 🛒 Tarjetas de Productos (`ProductCard.vue`)
* Texto del botón principal actualizado de `<span>Consultar</span>` a `<span>Comprar</span>`.
* Atributo `title` y accesibilidad actualizados a `Comprar [Producto] por WhatsApp`.

#### 2. 🔍 Modal de Detalle de Producto (`ProductDetailModal.vue`)
* Botón de acción principal actualizado de `Consultar disponibilidad en WhatsApp` a `Comprar por WhatsApp`.
* Consistencia en la experiencia de usuario entre la vista de cuadrícula y el modal extendido.

#### 3. 📦 Empaquetado y Distribución
* Build de producción optimizado con Vite (`index-bJDvMx0C.js`).
* Publicación en Docker Hub de las imágenes:
  * `juaneliezer13/akamikbeauty:1.5.2`
  * `juaneliezer13/akamikbeauty:latest`
