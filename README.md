# Dremio en Docker Compose

Este repositorio contiene la configuración necesaria para levantar Dremio OSS en tu máquina local utilizando Docker Compose. La imagen se fija a la versión **25.2.0** de Dremio OSS.

## Requisitos

- Docker (https://docs.docker.com/get-docker/) instalado en tu sistema.
- Docker Compose (https://docs.docker.com/compose/install/) (generalmente incluido en Docker Desktop).

## Archivos incluidos

- docker-compose.yml: Archivo de configuración para levantar el contenedor de Dremio.
- .env: Archivo de variables de entorno (debes crear o modificar este archivo según tus necesidades).

## Configuración

El archivo docker-compose.yml define el servicio "dremio" utilizando la imagen "dremio/dremio-oss:25.2.0". Se exponen los siguientes puertos:

- 9047: Interfaz web de Dremio.
- 31010: Conexiones JDBC/ODBC y otras.
- 45678: Servicio de coordinación entre nodos.

Se configuran dos volúmenes para la persistencia de datos:
- dremio_data: Almacena los datos y configuraciones de Dremio.
- local_files: Mapea un directorio para archivos locales adicionales.

El archivo .env debe contener las variables de entorno necesarias, por ejemplo:

DREMIO_MAX_DIRECT_MEMORY=4G
DREMIO_JAVA_OPTS=-XX:MaxDirectMemorySize=4G

## Uso

### 1. Preparación
- Clona o descarga este repositorio en tu máquina local.
- Asegúrate de tener en el mismo directorio el archivo docker-compose.yml y el archivo .env con la configuración deseada.

### 2. Levantar el servicio
Abre una terminal en el directorio del repositorio y ejecuta:

    docker-compose up -d

Este comando descargará la imagen "dremio/dremio-oss:25.2.0" (si aún no la tienes), creará el contenedor y lo iniciará en segundo plano.

### 3. Acceder a la interfaz web
Una vez que el contenedor esté en ejecución, abre tu navegador y visita:

    http://localhost:9047

Desde allí podrás configurar y administrar Dremio.

### 4. Administrar el servicio
- Ver logs del contenedor:

      docker-compose logs -f dremio

- Detener el servicio:

      docker-compose down

## Notas adicionales

- Persistencia de datos:
  Los volúmenes "dremio_data" y "local_files" aseguran que los datos y configuraciones se mantengan entre reinicios del contenedor.

- Variables de entorno:
  Ajusta las variables en el archivo .env según la memoria y recursos disponibles en tu máquina.

## Contribuciones

Las contribuciones son bienvenidas. Si deseas mejorar la configuración o agregar nuevas funcionalidades, por favor envía un pull request o abre un issue.

## Licencia

Este proyecto se distribuye bajo la licencia Apache-2.0.
