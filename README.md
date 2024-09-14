<p align="center">
  <a href="https://www.docker.com/" target="_blank">
    <img src="https://raw.githubusercontent.com/docker/compose/main/logo.png" width="200" alt="Docker Logo">
  </a>
</p>

<p align="center">
  <a href="https://github.com/litespeedtech/ols-docker-env/actions/">
    <img src="https://github.com/litespeedtech/ols-docker-env/workflows/docker-build/badge.svg" alt="Build Status">
  </a>
  <a href="https://hub.docker.com/r/litespeedtech/openlitespeed">
    <img src="https://img.shields.io/docker/pulls/litespeedtech/openlitespeed?style=flat&color=blue" alt="Docker Pulls">
  </a>
  <a href="https://litespeedtech.com/slack">
    <img src="https://img.shields.io/badge/slack-LiteSpeed-blue.svg?logo=slack" alt="Slack">
  </a>
  <a href="https://twitter.com/litespeedtech">
    <img src="https://img.shields.io/twitter/follow/litespeedtech.svg?label=Follow&style=social" alt="Follow on Twitter">
  </a>
</p>

# OLS Docker Setup

Este repositorio es una copia idéntica del proyecto original de GitHub [litespeedtech/ols-docker-env](https://github.com/litespeedtech/ols-docker-env) de la cuenta **litespeedtech**, modificado para un uso más nativo y amigable en cualquier sistema operativo, pero especialmente dirigido a usuarios de Windows. Este entorno Docker facilita la ejecución y el desarrollo de las aplicaciones. A continuación, se muestran los comandos más importantes para levantar los contenedores Docker, junto con una breve descripción de las versiones utilizadas en `docker-compose.yml`.


## Requisitos

- **[Docker](https://www.docker.com/)** y **[Docker Compose](https://docs.docker.com/compose/)** instalados en tu sistema.

## Componentes

La imagen Docker instala los siguientes paquetes en tu sistema, asegurando que cada uno esté en su última versión estable para ofrecer un entorno de desarrollo completo y actualizado:

|Componente|Versión|
| :-------------: | :-------------: |
|MySQL|[Última versión](https://hub.docker.com/_/mysql)|
|OpenLiteSpeed|[Última versión](https://hub.docker.com/r/litespeedtech/openlitespeed)|
|Laravel|[Última versión](https://hub.docker.com/r/bitnami/laravel/)|
|phpMyAdmin|[Última versión](https://hub.docker.com/r/bitnami/phpmyadmin/)|
|Redis|[Última versión](https://hub.docker.com/_/redis/)|

### Uso en producción
Cuando el proyecto se despliega en un entorno de producción, o si necesitas un entorno de desarrollo más controlado, es altamente recomendable fijar las versiones de las imágenes de Docker para evitar problemas de compatibilidad o actualizaciones inesperadas. Esto garantiza que el entorno se mantenga estable y evita cualquier comportamiento inesperado al actualizarse las imágenes a versiones más recientes de forma automática, se pueden usar versiones especificas usando variables de entorno, el `.env.example` incluye `OLS_VERSION` y `PHP_VERSION` para uso de versiones especificas.

Para especificar una versión de imagen en el archivo `docker-compose.yml`, puedes hacerlo de la siguiente manera:

```yaml
services:
  laravel:
    image: bitnami/laravel:11.1.5
    environment:
      LARAVEL_DATABASE_PORT_NUMBER: ${MYSQL_PORT}
      LARAVEL_DATABASE_NAME: ${MYSQL_DATABASE}
  mysql:
    image: mysql:8.4
  litespeed:
    image: litespeedtech/openlitespeed:${OLS_VERSION}-${PHP_VERSION}
```

### Explicación de los Componentes

En el archivo `docker-compose.yml`, se especifican versiones específicas para los servicios necesarios del entorno. Aquí está una breve descripción:

- **MariaDB**: Un sistema de gestión de bases de datos relacional que es una alternativa mejorada y de código abierto a MySQL.
- **OpenLiteSpeed**: Un servidor web ligero y de alto rendimiento, que ofrece soporte para tecnologías modernas como HTTP/3, PHP y más.
- **Laravel**: Un framework de desarrollo web en PHP, diseñado para facilitar la creación de aplicaciones web con una arquitectura limpia y modular.
- **phpMyAdmin**: Una herramienta gráfica para gestionar bases de datos MariaDB/MySQL, lo que facilita la administración de bases de datos sin necesidad de comandos SQL.
- **Redis**: Un almacén de datos en memoria que mejora la velocidad del acceso a datos y es útil para almacenamiento en caché y sesiones.

Este entorno completo te permite trabajar con todas las herramientas necesarias para desarrollar y gestionar aplicaciones web modernas de manera eficiente.

Asegúrate de que las versiones de estos servicios sean compatibles con tus necesidades de desarrollo.

Notas adicionales
Puedes personalizar las variables en el archivo .env para ajustar la configuración a tu entorno de desarrollo.

Si necesitas reconstruir los contenedores después de realizar cambios en el archivo docker-compose.yml, ejecuta:

```
docker-compose up --build
```

## Estructura de Datos

Proyecto clonado

```bash
├── acme
│   └── .gitignore
├── logs
│   └── .gitignore
├── lsws
│   └── .gitignore
├── sites
│   ├── JS
│   │   └── .gitignore
│   ├── localhost
│   │   ├── html
│   │   │   └── .gitignore
│   │   └── logs
│   │       └── .gitignore
│   └── PHP
│       └── .gitignore
├── .env.example
├── docker-compose.yml
├── LICENSE
└── README.md
```

  * `acme` contiene todos los certificados aplicados de Let's Encrypt.

  * `logs` contiene todos los registros del servidor web y los registros de acceso de los hosts virtuales.

  * `lsws` contiene todos los archivos de configuración del servidor web.

  * `sites` contiene los directorios raíz de los sitios (aquí se instalará la aplicación de Laravel/PHP, localhost para OpenLiteSpeed y node para proyectos de NodeJS).
  
  * `.gitignore` archvivo para ignorar todo contenido de esas carpetas, en caso de querer subir proyectos personales, eliminar el .gitignore correspondiente de cada carpeta.

## Comandos principales y uso

### 1. Clonar el repositorio

Antes de empezar, debes clonar el repositorio de OLS Docker en tu máquina local para poder configurar el entorno correctamente. Ejecuta el siguiente comando en tu terminal:

```
git clone https://github.com/9paul20/ols-docker-9paul2.git
```

Este comando descargará el repositorio completo en tu directorio actual. Una vez clonado, navega al directorio del proyecto:

```
cd ols-docker-9paul2
```

Con esto tendrás el código fuente del proyecto listo para los siguientes pasos de configuración, como copiar el archivo de entorno y ejecutar los contenedores Docker.

### 2. Copiar el archivo de entorno

El archivo `.env` se utiliza para configurar variables de entorno específicas del proyecto, como las credenciales de la base de datos, las rutas de almacenamiento, o las claves API. Antes de ejecutar los contenedores, es necesario copiar el archivo de ejemplo y renombrarlo a `.env`, que será leído automáticamente por el sistema:

```
cp .env.example .env
```

Este archivo permite que el proyecto se ejecute en diferentes entornos (desarrollo, pruebas, producción) sin necesidad de cambiar el código fuente. Puedes modificar el archivo `.env` para incluir nuevas variables o eliminar aquellas que no sean necesarias.

Si estás trabajando con **Docker Compose**, también puedes agregar o ajustar variables de entorno que serán utilizadas por los servicios definidos en el archivo `docker-compose.yml`. Por ejemplo, puedes definir puertos, bases de datos, o configuraciones específicas de tu aplicación en el `.env`, y luego referenciarlas en el `docker-compose.yml` de esta forma:

```yaml
services:
  app:
    image: bitnami/laravel:latest
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```

### 3. Iniciar los contenedores

Para levantar los contenedores con Docker Compose, usa el siguiente comando:

```
docker-compose up
```

Este comando iniciará los contenedores definidos en el archivo docker-compose.yml.

### 4. Apagar los contenedores

Si necesitas detener los contenedores, usa:

```
docker-compose down
```

## Soporte

Si aún tienes preguntas después de usar OpenLiteSpeed Docker, tienes algunas opciones:

* Unete a la comunidad de [GoLiteSpeed Slack community](https://litespeedtech.com/slack) para discusiones en tiempo real.
* Publica en los foros de [OpenLiteSpeed Forums](https://forum.openlitespeed.org/) para obtener soporte de la comunidad.
* Reporta cualquier problema en el proyecto de [Github ols-docker-env](https://github.com/litespeedtech/ols-docker-env/issues).

## Licencia y Uso

Este proyecto está licenciado bajo la **Licencia Apache 2.0**. Puedes revisarla [aquí](https://www.apache.org/licenses/LICENSE-2.0).

Este repositorio es un proyecto abierto para la comunidad y está diseñado con el propósito de apoyar a otros desarrolladores en la creación de entornos de desarrollo. **No me hago responsable** de cualquier uso indebido o problemas que puedan surgir del uso de este código. 

El **usuario es completamente responsable** de adaptar y mantener el entorno de acuerdo a sus necesidades, y no se ofrece garantía alguna sobre su funcionalidad o seguridad en un entorno productivo. **No se realiza ningún lucro** con este repositorio y su uso es libre, bajo las condiciones de la licencia.

El propósito de este repositorio es exclusivamente de apoyo para facilitar entornos de desarrollo Docker. **No asumiré ninguna responsabilidad** por posibles daños o problemas técnicos que puedan ocurrir en el futuro.
