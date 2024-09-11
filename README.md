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

Este repositorio contiene un entorno Docker configurado para el proyecto **OLS**, facilitando la ejecución y el desarrollo de las aplicaciones. A continuación, se muestran los comandos más importantes para levantar los contenedores Docker, junto con una breve descripción de las versiones utilizadas en `docker-compose.yml`.

## Requisitos

- **Docker** y **Docker Compose** instalados en tu sistema.

## Comandos principales

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
      - APP_ENV=${APP_ENV}
      - DB_HOST=${DB_HOST}
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

## Versiones de los servicios Docker
En el archivo docker-compose.yml, se especifican versiones específicas para los servicios necesarios del entorno. Aquí está una breve descripción:

- **mariadb:latest**: Base de datos relacional utilizada para almacenar y gestionar los datos de la aplicación, compatible con MySQL pero con un enfoque más abierto y flexible.
- **litespeedtech/openlitespeed:latest**: Servidor web de alto rendimiento que maneja las peticiones hacia la aplicación, optimizado para trabajar con **OpenLiteSpeed** y compatible con WordPress y otros CMS.
- **bitnami/laravel:latest**: Imagen optimizada de **Laravel** que incluye el entorno completo para ejecutar aplicaciones basadas en este framework PHP, facilitando la configuración y despliegue.
- **bitnami/phpmyadmin:latest**: Herramienta web utilizada para gestionar bases de datos MariaDB/MySQL a través de una interfaz gráfica, facilitando la administración de tablas, consultas, y configuraciones de bases de datos.
- **redis:alpine**: Almacenamiento en caché de alta velocidad utilizado para mejorar el rendimiento y la escalabilidad de la aplicación, permitiendo una rápida recuperación de datos.


Asegúrate de que las versiones de estos servicios sean compatibles con tus necesidades de desarrollo.

Notas adicionales
Puedes personalizar las variables en el archivo .env para ajustar la configuración a tu entorno de desarrollo.

Si necesitas reconstruir los contenedores después de realizar cambios en el archivo docker-compose.yml, ejecuta:

```
docker-compose up --build
```

## Licencia y Uso

Este proyecto está licenciado bajo la **Licencia Apache 2.0**. Puedes revisarla [aquí](https://www.apache.org/licenses/LICENSE-2.0).

Este repositorio es un proyecto abierto para la comunidad y está diseñado con el propósito de apoyar a otros desarrolladores en la creación de entornos de desarrollo. **No me hago responsable** de cualquier uso indebido o problemas que puedan surgir del uso de este código. 

El **usuario es completamente responsable** de adaptar y mantener el entorno de acuerdo a sus necesidades, y no se ofrece garantía alguna sobre su funcionalidad o seguridad en un entorno productivo. **No se realiza ningún lucro** con este repositorio y su uso es libre, bajo las condiciones de la licencia.

El propósito de este repositorio es exclusivamente de apoyo para facilitar entornos de desarrollo Docker. **No asumiré ninguna responsabilidad** por posibles daños o problemas técnicos que puedan ocurrir en el futuro.
