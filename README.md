# 🌸 Akami K-Beauty — Repositorio Central de Documentación y Activos (`akami-docs`)

Bienvenido al repositorio central de **documentación técnica, reglas de negocio, historial de versiones, guías de despliegue y activos oficiales optimizados** del ecosistema **Akami K-Beauty** (Catálogo Digital Web SPA, Mini CMS Administrativo y API RESTful con cierre de ventas por WhatsApp Business).

---

## 🗂️ Estructura Estandarizada del Repositorio `akami-docs`

```text
akami-docs/
├── 📄 README.md                                  # Índice maestro del repositorio y arquitectura general
├── 📜 NORMAS_TECNICAS.md                         # Normas técnicas, reglas de negocio y directrices para IA
├── 🤖 AGENTS.md                                  # Contexto e instrucciones operativas para Agentes de IA
├── 🤖 CLAUDE.md                                  # Contexto técnico para Claude Code / Anthropic
├── 🤖 GEMINI.md                                  # Contexto técnico para Gemini / Antigravity
│
├── 💼 business/                                  # Reglas de negocio, catálogo maestro y diseño UI/UX
│   ├── requerimientos_cliente.md                 # Requerimientos funcionales, transcripción de audios y flujos
│   ├── diseno_figma.md                           # Especificación UI/UX, paleta de colores, fuentes y secciones
│   ├── catalogo_productos.md                     # Catálogo maestro documentado (83 productos y 19 marcas)
│   ├── catalogo_productos.json                   # Matriz JSON estructurada de los 83 productos oficiales
│   └── catalogo_productos.csv                    # Exportación CSV (UTF-8 con BOM) para hojas de cálculo
│
├── 🚀 deploy/                                    # Guías DevOps, Docker Compose y configuración de servidores
│   ├── GUIA_DESPLIEGUE_AWS_DESDE_CERO.md         # Guía paso a paso para AWS EC2 (Frontend 16001 | Backend 15001)
│   ├── DEPLOY_GODADDY_DOCKER.md                  # Guía de contenedorización ligera
│   ├── STAGING.md                                # Guía de entorno Staging
│   ├── docker-compose.server.yml                 # Compose de referencia para servidor de producción
│   ├── docker-compose.staging.yml                # Compose de referencia para entorno staging
│   └── nginx.conf.example                        # Configuración base de Nginx con compresión Gzip y caché
│
├── 🏷️ releases/                                  # Historial completo de versiones y notas de lanzamiento
│   ├── RELEASE_NOTES_v1.1.0.md                   # Reconciliación inicial de catálogo y arquitectura modular
│   ├── RELEASE_NOTES_v1.2.0.md                   # Optimización de banners y experiencia móvil
│   ├── RELEASE_NOTES_v1.2.2.md                   # Sincronización de inventario y precios oficiales
│   ├── RELEASE_NOTES_v1.2.3.md                   # Ajustes de catálogo y normalización de activos
│   ├── RELEASE_NOTES_v1.3.0.md                   # Mini CMS integrado, Backend PHP 8.2 + SQLite y /uploads/
│   ├── RELEASE_NOTES_v1.4.0.md                   # Desacoplamiento de infraestructura (Puertos 16001 y 15001)
│   ├── RELEASE_NOTES_v1.5.0.md                   # Renovación completa de banners WebP por categoría y piel
│   ├── RELEASE_NOTES_v1.5.1.md                   # Nuevos copys editoriales y logotipo blanco en banners
│   ├── RELEASE_NOTES_v1.5.2.md                   # Actualización de CTA principal a "Comprar"
│   └── RELEASE_NOTES_v1.6.0.md                   # Secciones Quiénes Somos, Valor de Marca, Contacto y Drag & Drop
│
├── 📊 informes/                                  # Informes ejecutivos y estado del proyecto
│   └── INFORME_INICIAL_PROYECTO_AKAMI.md         # Informe ejecutivo y matriz de entregables consolidados
│
├── 🖼️ prototypes-and-screenshots/                # Enlaces a prototipo Figma Make, Instagram y referencias
│   └── README.md
│
└── 📦 assets/                                    # Activos oficiales de la marca optimizados y estandarizados
    ├── audio/                                    # Notas de voz originales con requerimientos de la clienta (.ogg)
    ├── banners/                                  # Banners WebP organizados en institucional/, categorias/ y tipos-de-piel/
    ├── brand/                                    # Isologo SVG, logotipos PNG y manual de paleta de colores (.webp)
    ├── documents/                                # PDFs maestros de lista de precios y estructura por categorías
    ├── fonts/                                    # Familia tipográfica oficial Vastago Grotesk (9 pesos .otf)
    ├── products/                                 # Fotografías base en WebP organizadas por marca (16 carpetas)
    └── videos/                                   # Videos institucionales MP4 (faststart) y posters WebP
```

---

## 🏗️ Arquitectura General del Proyecto Akami K-Beauty

El ecosistema completo en el entorno de trabajo (`akami/`) opera bajo una arquitectura de microservicios desacoplados con contenedores Docker:

```text
akami/
├── 💻 akamikbeauty/          # Frontend SPA (Vue 3 + TS + Vite + Tailwind + Nginx Alpine) -> Puerto 16001
├── 🛠️ akami-api/             # Backend RESTful API (PHP 8.2 + PDO SQLite WAL)            -> Puerto 15001
├── 📚 akami-docs/            # Repositorio central de documentación y activos (este repo)
├── 🗄️ database/              # Persistencia SQLite (contiene únicamente akami.sqlite)
└── 🖼️ uploads/products/      # Almacenamiento persistente de imágenes subidas desde el Mini CMS
```

---

## 🏷️ Estándar de Versionado Semántico y Ramas

* **Ramas y Tags de Lanzamiento:** `release/vX.Y.Z` y tags `vX.Y.Z` (última versión: `v1.6.0`).
* **Rama de Desarrollo Activo:** `develop`.
* **Rama de Producción Estable:** `main`.
* **Imágenes Oficiales en Docker Hub:**
  * Frontend: `juaneliezer13/akamikbeauty:latest` (`v1.6.0`)
  * Backend: `juaneliezer13/akami-api:latest` (`v1.1.0+`)
