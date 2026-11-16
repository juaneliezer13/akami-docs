# 🚀 Release Notes — `v1.6.1` (Reasignación de Puertos de Contenedores: 16001 API / 17001 Web)

* **Rama Git / Tag:** `release/v1.6.1` / `v1.6.1` (`akami-api`: `release/v1.1.1` / `v1.1.1`)
* **Fecha:** 16 de noviembre de 2026

## ✨ Novedades Principales
1. **Reasignación de Puertos en Entorno Docker:**
   * **Backend REST API (`akami-api`):** Pasa al puerto **`16001`** (`BACK_PORT=16001`).
   * **Frontend Web SPA (`akamikbeauty`):** Pasa al puerto **`17001`** (`FRONT_PORT=17001`).
   * Permite la convivencia simultánea en el host junto al ecosistema **BaiFa Power Tracking** (`14001` API / `14002` DB / `15001` UI) sin colisión de puertos.
2. **Actualización Documental (`akami-docs`):**
   * Sincronización de referencias de puertos en `README.md`, `NORMAS_TECNICAS.md`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` y guías de despliegue.
