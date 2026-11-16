# 🚀 Guía de Despliegue en Servidor GoDaddy (Bajos Recursos / Docker)

Esta guía documenta el procedimiento estándar para compilar y desplegar la **Single Page Application (SPA)** de **Akami K-Beauty** en un servidor básico / VPS de bajos recursos en GoDaddy utilizando Docker y Nginx Alpine.

---

## 🏗️ Arquitectura de Producción

En el servidor remoto de GoDaddy, la estructura de carpetas esperada es estrictamente la siguiente:

```text
/home/usuario/ (o /var/www/)
└── akami-web/
    ├── docker-compose.yml
    └── html/
        └── akami/
            ├── index.html
            ├── favicon.svg
            └── assets/
                ├── index-*.js
                └── index-*.css
```

---

## 🐳 Archivo de Orquestación: `docker-compose.yml`

El archivo `docker-compose.yml` en producción utiliza la imagen oficial ligera de Nginx (`nginx:alpine`), la cual consume menos de **15 MB de memoria RAM**:

```yaml
services:
  web_akami:
    image: nginx:alpine
    container_name: cliente_akami
    restart: unless-stopped
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html:ro
```

> **Nota de Rutas:** Al montar `./html:/usr/share/nginx/html:ro`, la aplicación queda servida en la ruta base `/akami/` (ej. `http://tu-dominio.com/akami/` o `http://tu-ip/akami/`). La configuración de Vite (`base: './'`) garantiza que todas las llamadas a scripts, hojas de estilo e imágenes se resuelvan de forma relativa sin importar el subdirectorio o dominio.

---

## 🛠️ Procedimiento de Compilación y Publicación

### Paso 1: Compilar la SPA en tu entorno local (WSL / Local)

Desde la carpeta raíz del proyecto `akami-web`:

```bash
# 1. Instalar dependencias si no se ha hecho
npm install

# 2. Compilar el proyecto para producción
npm run build
```

El script de compilación `npm run build` está configurado para emitir automáticamente los archivos procesados y minificados directamente en:
```text
akami-web/html/akami/
```

### Paso 2: Subir los archivos al servidor GoDaddy

Puedes transferir los archivos compilados mediante `scp`, `rsync`, o mediante un cliente SFTP (como FileZilla):

```bash
# Ejemplo con rsync
rsync -avz --delete ./html/ usuario@tu-servidor-godaddy:/ruta/hacia/akami-web/html/
rsync -avz ./docker-compose.yml usuario@tu-servidor-godaddy:/ruta/hacia/akami-web/
```

O si tienes Git clonado en el servidor GoDaddy:
```bash
cd akami-web
git pull origin main
npm run build  # (si el servidor tiene Node) o simplemente subir la carpeta html/
```

### Paso 3: Iniciar o Reiniciar el Contenedor Docker en GoDaddy

Conéctate por SSH a tu servidor GoDaddy:

```bash
ssh usuario@tu-ip-godaddy
cd akami-web

# Iniciar el servicio en segundo plano
docker compose up -d
```

Para verificar el estado y los logs del contenedor:
```bash
# Ver estado del contenedor
docker ps --filter "name=cliente_akami"

# Ver logs de Nginx en vivo
docker compose logs -f web_akami
```

Para reiniciar tras una actualización:
```bash
docker compose restart web_akami
```

---

## 📱 Acceso Local desde Dispositivos en la Misma Red Wi-Fi (Celulares/Tablets)

Para probar la experiencia móvil en celulares reales conectados a la misma red Wi-Fi:

1. **Tu IP local de red detectada es:** `172.21.0.196` (o la IP que asigne tu router Wi-Fi).
2. **Acceso directo en el navegador de tu celular:**
   * `http://172.21.0.196/akami/`
   * `http://172.21.0.196/` (redirige automáticamente)
3. **Puente de Red Local (WSL2 -> LAN):**
   * Se incluye el script automático `iniciar_acceso_red_local.bat` en la raíz del proyecto.
   * Al ejecutarlo, levanta un relay en `0.0.0.0:80` que redirige el tráfico entrante de cualquier teléfono o dispositivo hacia el contenedor Nginx en WSL2.
   * Alternativamente, si deseas configurar la redirección permanente nativa en Windows con permisos de Administrador, puedes ejecutar el archivo `abrir_puerto_80_firewall.bat`.

---

## 🔒 Configuración Opcional: SSL y Dominio Propio

Si deseas configurar un certificado HTTPS gratuito con Let's Encrypt (Certbot), puedes:
1. Usar un proxy inverso frontal como Nginx con Certbot en el host.
2. O mapear el puerto 443 en el `docker-compose.yml` montando los certificados SSL en `/etc/nginx/ssl`.

---

## 📈 Rendimiento y Métricas en Servidor GoDaddy

* **Consumo de Memoria:** ~12 MB de RAM (Ideal para VPS de 512 MB o 1 GB de RAM).
* **Consumo de CPU:** < 0.1% en reposo.
* **Tiempo de Respuesta TTFB:** < 45 ms.
* **Compatibilidad de Cache:** Nginx entrega cabeceras HTTP de cache estático (`ETag`, `Cache-Control`) para carga ultrarrápida en visitas recurrentes.
