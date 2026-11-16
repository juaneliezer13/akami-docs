# 🤖 CLAUDE.md — Guía de Contexto y Reglas para Claude Code (Akami K-Beauty)

Por favor, lee y respeta íntegramente las directrices establecidas en:
* [`AGENTS.md`](./AGENTS.md)
* [`NORMAS_TECNICAS.md`](./NORMAS_TECNICAS.md)

## Resumen Rápido de Comandos y Arquitectura (v1.6.0+)

* **Frontend (`akamikbeauty/` — Puerto `17001`):**
  * Desarrollo: `cd akamikbeauty && npm run dev`
  * Build de producción (genera `html/`): `cd akamikbeauty && npm run build`
  * Contenedor Docker: `cd akamikbeauty && docker compose up -d`
* **Backend (`akami-api/` — Puerto `16001`):**
  * Contenedor Docker: `cd akami-api && docker compose up -d`
  * Healthcheck: `curl -s http://localhost:16001/api/health`
* **Base de Datos (`database/akami.sqlite`):**
  * Base de datos SQLite en modo WAL con 83 productos oficiales, 20 marcas y 8 categorías. No modificar ni borrar `akami.sqlite`, ni añadir archivos extra en `database/`.
* **Reglas Clave de UI y Servidor:**
  * Secciones activas: Catálogo principal, **Quiénes somos** (`#quienes-somos` con videos `ritual-skincare.mp4` y `glass-skin.mp4` sin texto flotante), **Contacto** (`#contacto` con banner propio y canales directos) y **Mini CMS** (`#admin` con subida Drag-and-Drop de hasta 25 MB).
  * Botones CTA de producto: **"Comprar"** / **"Comprar por WhatsApp"**.
  * Nginx sirve `/uploads/` con prioridad `location ^~ /uploads/` hacia `/usr/share/nginx/uploads/`.
