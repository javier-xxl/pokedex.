# Despliegue de **poke-dex-lab** en Azure

## Descripción
Se realizó el despliegue de la aplicación **poke-dex-lab** en la plataforma de Azure, asegurando que todos los servicios necesarios estuvieran correctamente configurados y operativos.

### Pasos para el Despliegue

1. **Descarga y Preparación:**
   - Descarga el archivo ZIP del proyecto desde el enlace de GitHub.
   - Instala **Node.js** y **Angular** de forma local.

2. **Ejecutar la Aplicación Localmente:**
   - Navega a la carpeta del proyecto en tu terminal y ejecuta:
     ```bash
     npm install
     npm start
     ```
   - Valida que la aplicación esté funcionando accediendo a `http://localhost:4200/`.

3. **Construir la Aplicación para Producción:**
   - Una vez confirmada la funcionalidad local, ejecuta el siguiente comando para construir la aplicación:
     ```bash
     npm run build
     ```
   - Esto creará una carpeta llamada **dist** con una subcarpeta **pokedex-angular**. Comprime todos los archivos de esta subcarpeta en un archivo ZIP llamado **pokedex-angular.zip**.

4. **Despliegue en Azure:**
   - Accede a la App Service creada en Azure.
   - Dirígete a **Herramientas de desarrollo** → **Herramientas avanzadas** → **Ir**.
   - Haz clic en **Debug Console** y selecciona **CMD**.
   - Navega a la ruta **site/wwwroot** y arrastra el archivo **pokedex-angular.zip** al servidor para descomprimirlo.

### Configuración de Seguridad

Crea un archivo **web.config** en la raíz del proyecto con los siguientes parámetros de seguridad:

## Explicación del archivo web.config

### Descripción General
El archivo `web.config` es un documento XML que configura un servidor web IIS (Internet Information Services). Este archivo establece diversas configuraciones de seguridad y comportamiento para la aplicación web.

### Componentes Principales

#### 1. Redirección HTTPS 🔒
- **Propósito**: Garantizar conexiones seguras.
- **Tipo**: Redirección permanente (301).
- **Alcance**: Todas las URLs del sitio.

#### 2. Encabezados de Seguridad 🛡️

| Encabezado                     | Propósito                        | Configuración                   |
|---------------------------------|----------------------------------|---------------------------------|
| Strict-Transport-Security       | Forzar HTTPS                    | max-age=31536000               |
| Content-Security-Policy         | Controlar fuentes de recursos    | default-src 'self'             |
| X-Frame-Options                 | Prevenir clickjacking            | DENY                            |
| X-Content-Type-Options          | Prevenir MIME-sniffing           | nosniff                         |
| Referrer-Policy                 | Controlar info de referente      | no-referrer-when-downgrade     |
| Permissions-Policy              | Gestionar permisos               | geolocation=(self), microphone=() |

#### 3. Configuración SPA 📱
- Soporte para archivos JSON.
- Manejo de rutas personalizado.
- Configuración de archivos estáticos.

#### 4. Gestión de Errores
- **404**: Redirección a la página principal.

### Implementación

1. Coloca el archivo **web.config** en la raíz del proyecto.
2. Verifica la configuración del servidor IIS.
3. Prueba todas las redirecciones y encabezados.

### Consideraciones Importantes

- **Nota**: Revisa y ajusta los encabezados de seguridad según tus necesidades específicas.

### Checklist de Implementación
- Verificar compatibilidad con IIS.
- Probar redirecciones HTTPS.
- Validar funcionamiento de la SPA.
- Comprobar encabezados de seguridad.

Para más información, consulta la documentación oficial de Microsoft IIS.
