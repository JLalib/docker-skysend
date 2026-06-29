# Docker SkySend ☁️

SkySend es una plataforma de compartición de archivos encriptada y autohospedada que permite compartir archivos de forma segura sin depender de servicios en la nube como WeTransfer, Google Drive o Dropbox. Gracias a la encriptación end-to-end, los archivos se cifran en el navegador del emisor antes de subirse, asegurando que ni siquiera el administrador del servidor pueda acceder a su contenido.

## 🚀 Características Principales

- **Encriptación End-to-End:** Privacidad absoluta; el cifrado y descifrado ocurren exclusivamente en el navegador del cliente.
- **Sin Límites de Tamaño:** La capacidad depende únicamente del espacio en disco disponible en tu servidor.
- **Enlaces Únicos y Seguros:** Genera URLs con claves secretas imposibles de adivinar.
- **Descarga Directa y Anónima:** No requiere registro de cuentas ni suscripciones.
- **CLI Profesional:** Herramienta de línea de comandos para automatización y scripting de subidas y descargas.
- **Control de Acceso y Expiración:** Configura el número máximo de descargas y la fecha de auto-eliminación de los archivos.
- **API REST:** Facilidad de integración en otras aplicaciones propias.

## 🛠️ Requisitos del Sistema

- **Hardware:** Compatible con cualquier servidor x86 o ARM.
- **RAM:** 512 MB - 1 GB.
- **Espacio en Disco:** Configurable según la cantidad de archivos a compartir.
- **Puerto:** 3000 (configurable).
- **Software:** Docker y Docker Compose instalados.

## 📦 Instalación con Docker Compose

### 1. Preparar el entorno
Crea la carpeta del proyecto y entra en ella:
```bash
mkdir skysend && cd skysend
```

### 2. Crear el archivo `docker-compose.yml`
Copia el contenido del archivo `docker-compose.yml` incluido en este repositorio.

### 3. Desplegar el servicio
```bash
docker compose up -d
```

### 4. Acceder a SkySend
Abre tu navegador y entra en: `http://localhost:3000`

## ⚙️ Primeros Pasos

1. **Subir un archivo:** Arrastra el archivo a la interfaz web. SkySend lo encriptará localmente y te dará un enlace único.
2. **Compartir:** Envía el enlace generado (incluida la parte `#secret`). El receptor podrá descargar y desencriptar el archivo automáticamente.
3. **Uso de la CLI:**
   - Instala la CLI: `curl -fsSL https://skysend.ch/install.sh | sh`
   - Configura el servidor: `skysend config set-server http://localhost:3000`
   - Sube un archivo: `skysend upload ./archivo.pdf`
4. **Opciones Avanzadas:** Antes de subir, ajusta la expiración y el límite de descargas en el panel de opciones.

## 🛡️ Seguridad y Mantenimiento

- **HTTPS (Recomendado):** Para acceso remoto seguro, utiliza un proxy inverso como **Caddy** o **Nginx**. Recuerda actualizar la variable `BASE_URL` en el `docker-compose.yml` con tu dominio HTTPS.
- **Gestión de Almacenamiento:** Monitorea el espacio usado en el volumen de subidas:
  ```bash
  du -sh ./skysend-uploads/
  ```
- **Actualización:** `docker compose pull && docker compose up -d`
- **Backup de Datos:**
  ```bash
  docker run --rm -v skysend-data:/data -v $(pwd):/backup alpine tar czf /backup/skysend-backup-$(date +%Y%m%d).tar.gz -C /data .
  ```

---
*Basado en el tutorial de [Genbyte](https://genbyte.blogspot.com/)*
