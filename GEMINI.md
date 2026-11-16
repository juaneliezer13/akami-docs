# 🤖 GEMINI.md — Contexto para Gemini / Antigravity (Akami K-Beauty)

Este proyecto sigue las especificaciones detalladas en [`AGENTS.md`](./AGENTS.md) y [`NORMAS_TECNICAS.md`](./NORMAS_TECNICAS.md).

## Puntos Críticos a Recordar (v1.6.0+)

1. **Estructura Limpia del Workspace (`akami/`):**
   * `akamikbeauty/`: Frontend SPA en Vue 3 + TypeScript + Vite + Tailwind CSS + Nginx Alpine (Puerto `17001`).
   * `akami-api/`: Backend RESTful en PHP 8.2 + SQLite WAL (Puerto `16001`, subida hasta `25 MB`).
   * `akami-docs/`: Repositorio central de documentación y activos optimizados en WebP (`kebab-case`).
   * `database/`: Solo contiene `akami.sqlite`.
   * `uploads/products/`: Imágenes de productos desacopladas servidas mediante `location ^~ /uploads/` en Nginx.
   * Las carpetas antiguas `scripts/` y `recordings/` fueron eliminadas permanentemente por estandarización.

2. **Últimos Cambios Implementados:**
   * Incorporación de secciones **Quiénes somos**, **Valor Fundamental de la Marca** (con videos MP4 `faststart` y posters JPEG/WebP sin cajas flotantes) y **Contacto** (con banner dedicado sin subtexto y canales directos).
   * Soporte **Drag-and-Drop** en el Mini CMS (`#admin`) para subida de fotos de productos, límite de 25 MB en PHP y fallback visual automático en tarjetas y modal cuando una imagen no está disponible.
   * CTA unificado a **"Comprar"** y **"Comprar por WhatsApp"**.
