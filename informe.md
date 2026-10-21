## 1. Título

**Creación de volúmenes para persistir una base de datos PostgreSQL utilizando Docker**

## 2. Tiempo de duración

2 horas 

## 3. Fundamentos

### Docker y contenedores

Docker es una plataforma que permite crear y ejecutar aplicaciones dentro de contenedores. Estos entornos incluyen los componentes necesarios para que una aplicación funcione y comparten el núcleo del sistema operativo que los ejecuta. Una imagen contiene la base para crear un contenedor, mientras que el contenedor es una instancia de esa imagen que puede iniciarse, detenerse y eliminarse.

En esta práctica se trabajó con la imagen oficial de PostgreSQL para comparar dos formas de almacenar la información. Se utilizaron los contenedores `server_db1` y `server_db2`, con el propósito de comprobar qué ocurre con una base de datos cuando se elimina y se vuelve a crear el contenedor.

### Base de datos PostgreSQL

PostgreSQL es un sistema de gestión de bases de datos relacionales que permite organizar información en tablas y manipularla mediante instrucciones SQL. Una tabla está formada por columnas, que definen los campos, y filas, que contienen los registros almacenados.

Para desarrollar la actividad se utilizó una base de datos llamada `test` y una tabla denominada `customer`, con los campos `id`, `fullname` y `status`. La conexión mediante un administrador de bases de datos permitió crear estos elementos, insertar información y consultar los registros antes y después de recrear los contenedores.

### Volúmenes de Docker

Un volumen es un recurso de almacenamiento administrado por Docker que tiene un ciclo de vida independiente del contenedor. Al utilizar un volumen con nombre, como `pgdata`, se puede identificar y asociar nuevamente a otro contenedor. Esto permite conservar la base de datos, las tablas y los registros, siempre que el volumen siga estando disponible y se monte en la ubicación correcta.

## 4. Conocimientos previos

- Conceptos básicos de imágenes y contenedores.
- Instalación y uso básico de Docker.
- Manejo de comandos en una terminal.
- Comprensión de puertos y conexiones locales.
- Conocimientos básicos de bases de datos relacionales y SQL.
- Uso de un administrador de bases de datos.

## 5. Objetivos a alcanzar

- Crear un contenedor PostgreSQL sin asociar explícitamente un volumen con nombre.
- Conectar un administrador de bases de datos al servidor PostgreSQL.
- Crear la base de datos `test` y la tabla `customer` con los campos solicitados.
- Insertar y consultar al menos un registro.
- Comprobar que recrear un contenedor con el mismo nombre no recupera automáticamente los datos anteriores.
- Crear el volumen `pgdata` y asociarlo a un contenedor PostgreSQL.
- Verificar la persistencia de los datos al eliminar y recrear el contenedor reutilizando el mismo volumen.

## 6. Equipo necesario

- Laptop o computadora con Docker instalado y en ejecución.
- Terminal de comandos.
- Administrador de bases de datos compatible con PostgreSQL.

## 7. Material de apoyo

- Guía de la práctica No. 3.
- Video explicativo en la plataforma EVA

## 8. Procedimiento

### Parte 1: Base de datos sin volumen con nombre

**Paso 1: Creación del contenedor `server_db1`.**

Se creó un contenedor a partir de la imagen de PostgreSQL con el nombre `server_db1`, configurando los datos de acceso y la publicación del puerto para permitir la conexión desde el administrador de bases de datos.

<img width="1917" height="167" alt="Captura de pantalla 2026-10-20 205320" src="https://github.com/user-attachments/assets/a4b80a69-e1d3-4ad3-8f0b-818b69b9bb67" />


**Paso 2: Creación de la base de datos y de la tabla.**

Se creó una base de datos denominada `test`. Dentro de ella se creó la tabla `customer`, con los campos `id`, `fullname` y `status`, para almacenar la información solicitada en la práctica.

<img width="1115" height="590" alt="image" src="https://github.com/user-attachments/assets/65f2348b-d265-4202-8f6b-6b63c4bb16a7" />


**Paso 3: Inserción y consulta de registros.**

Se insertó al menos un registro en la tabla `customer`. Luego se consultó su contenido para comprobar que la información estuviera almacenada antes de eliminar el contenedor.

<img width="1310" height="855" alt="Captura de pantalla 2026-10-20 202556" src="https://github.com/user-attachments/assets/cceaf08d-eea6-4081-8918-f64d555b4aa0" />


**Paso 4: Detención y eliminación del contenedor.**

Se detuvo y eliminó el contenedor `server_db1` utilizando los comandos:

<img width="1917" height="215" alt="Captura de pantalla 2026-10-20 205505" src="https://github.com/user-attachments/assets/6f5dfd2a-639c-431c-a003-20a71dbeabe8" />


**Paso 5: Recreación del contenedor y verificación.**

Se volvió a crear el contenedor PostgreSQL con el mismo nombre `server_db1`, sin asociar el almacenamiento utilizado anteriormente. Después se estableció nuevamente la conexión desde el administrador y se comprobó que la base de datos `test` ya no estuviera disponible en esta nueva instancia.

<img width="1917" height="170" alt="Captura de pantalla 2026-10-20 205835" src="https://github.com/user-attachments/assets/85e52efa-3a62-439a-b463-ade85f44899d" />

 <img width="1107" height="553" alt="image" src="https://github.com/user-attachments/assets/ccd0b6a8-8780-4611-8da2-051acf62f261" />

### Parte 2: Base de datos con volumen

**Paso 6: Creación del volumen `pgdata`.**

<img width="1345" height="320" alt="image" src="https://github.com/user-attachments/assets/1fbe396b-7aa7-4035-9590-3075b2821f52" />


**Paso 7: Creación del contenedor `server_db2` con el volumen.**

Se creó un segundo contenedor denominado `server_db2`, asociando el volumen `pgdata` a la ubicación de almacenamiento correspondiente a la versión de PostgreSQL utilizada. También se configuraron las credenciales y el puerto de conexión.

De esta manera, los archivos de la base de datos quedaron almacenados en el volumen que se reutilizaría después de eliminar el contenedor.

<img width="1917" height="117" alt="Captura de pantalla 2026-10-20 210848" src="https://github.com/user-attachments/assets/be185105-0bd9-4ab1-a420-4651f1bee303" />


**Paso 8: Conexión y creación de los datos de prueba.**

Se creó la base `test` y, dentro de ella, la tabla `customer` con los campos `id`, `fullname` y `status`. Se insertó al menos un registro y se consultó la tabla para verificar su almacenamiento.

<img width="1173" height="570" alt="Captura de pantalla 2026-10-20 211329" src="https://github.com/user-attachments/assets/d6b3f019-731d-4bf1-a06c-16db4eab0848" />


**Paso 9: Detención y eliminación de `server_db2`.**

Se detuvo y eliminó el segundo contenedor, conservando el volumen `pgdata`:

<img width="1917" height="282" alt="Captura de pantalla 2026-10-20 211440" src="https://github.com/user-attachments/assets/8f0c68c2-fb7b-4e95-b678-5d7977968da0" />


**Paso 10: Recreación de `server_db2` utilizando el mismo volumen.**

Se volvió a crear el contenedor `server_db2`, asociándolo nuevamente al volumen `pgdata` y utilizando la misma versión principal de PostgreSQL y la misma ubicación de montaje. Esto permitió que el servidor accediera a los archivos de la base de datos guardados en la primera ejecución.

<img width="1917" height="193" alt="Captura de pantalla 2026-10-20 211908" src="https://github.com/user-attachments/assets/92e04bf3-d3a9-42f7-89b8-91c245f02df6" />


**Paso 12: Verificación de la persistencia de los datos.**

Se verificó que la base `test` y la tabla `customer` siguen estando disponibles. Mediante la consulta de la tabla se vio que los registros insertados antes de eliminar el contenedor se conservaron

<img width="1050" height="562" alt="Captura de pantalla 2026-10-21 170036" src="https://github.com/user-attachments/assets/aa8abd29-fdf1-42e9-9d1d-eb05b76c285e" />


## 9. Resultados esperados

- Un contenedor `server_db1` creado sin asociar explícitamente un volumen con nombre.
- Una base `test` y una tabla `customer` con al menos un registro en la primera instancia.
- Una nueva instancia de `server_db1` en la que no aparezca la base `test`, al no reutilizar el almacenamiento anterior.
- Un volumen `pgdata` creado y asociado al contenedor `server_db2`.
- Una base `test`, una tabla `customer` y sus registros disponibles después de eliminar y recrear `server_db2` utilizando el mismo volumen.

## 10. Bibliografía

Docker, Inc. (s. f.). *Volumes*. Docker Docs. https://docs.docker.com/engine/storage/volumes/

Docker, Inc. (s. f.). *Postgres: Docker Official Image*. Docker Hub. https://hub.docker.com/_/postgres

Docker, Inc. (s. f.). *docker container rm*. Docker Docs. https://docs.docker.com/reference/cli/docker/container/rm/

PostgreSQL Global Development Group. (s. f.). *PostgreSQL documentation*. https://www.postgresql.org/docs/
