# Laboratorio / Práctica: Operaciones de tabla de base de datos

## 📋 Información general y objetivos del laboratorio

Este laboratorio muestra cómo usar algunas operaciones de bases de datos y tablas comunes.

Después de completar este laboratorio, podrá realizar lo siguiente:

* Usar la statement CREATE para crear bases de datos y tablas
* Usar la statement SHOW para ver las bases de datos y tablas disponibles
* Usar la statement ALTER para alterar la estructura de una tabla
* Usar la statement DROP para eliminar bases de datos y tablas
  
Cuando comience este en laboratorio, los siguientes recursos ya estarán creados para usted:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap1.png)

Un cliente de base de datos está instalado en una instancia.

Al final de este laboratorio, habrá completado algunas de las operaciones de base de datos y tablas comunes:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap2.png)



## 🛠️ Tecnologías y Herramientas Utilizadas
* **Base de Datos / Motor:** (Ej. PostgreSQL, MySQL, Amazon RDS, etc.)
* **Herramienta de Consulta (IDE):** (Ej. DBeaver, pgAdmin, MySQL Workbench, etc.)
* **Conceptos aplicados:** (Ej. INNER JOIN, GROUP BY, Subconsultas, Índices, etc.)

## 🚀 Escenario
El equipo de operaciones de base de datos para una organización configuró una instancia de base de datos relacional. El equipo le pidió que practique crear y descartar (eliminar) bases de datos y tablas.


## 🚀 Desarrollo y Solución

## Tarea 1: Conectarse a Command Host

En esta tarea, se conectará a una instancia de EC2 configurada con un cliente de base de datos. El cliente se usa para ejecutar las consultas de idioma de consulta estructurada (SQL) contra una base de datos relacional. Esta instancia se conoce como Command Host.


En la Consola de administración de AWS, seleccione el menú  Services (Servicios). Selccione Compute (Cómputo) y luego seleccione EC2.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap3.png)

En el menú de navegación izquierdo, seleccione Instances (Instancias).

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap4.png)

Junto a la instancia etiquetada Command Host, seleccione la casilla  y luego seleccione Connect (Conectar).
Nota: Si no ve Command Host, probablemente en laboratorio aún está siendo aprovisionado, o quizás esté usando otra Región.
En Connect to instance (Conexión a instancia), elija la pestaña Session Manager.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap5.png)
Elija Connect (Conectar) para abrir una ventana de terminal.

Nota: Si el botón Connect (Conectar) no está disponible, espere unos minutos y vuelva a intentarlo.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap6.png)



Para configurar la terminal para acceder a todas las herramientas y recursos necesarios, ejecute el siguiente comando:

```sql
sudo su
cd /home/ec2-user/
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap7.png)

Recuperar comandos de Linux

* El comando sudo (SuperUser DO) se usa para ejecutar un comando de Linux con los privilegios de otro usuario.
* El comando su (cambiar usuario) se usa para cambiara a otro usuario. De forma predeterminada, usa al usuario raíz si no se especifica un usuario.
* El comando cd (cambiar directorio) se usa para cambiar del directorio actual a una nueva ruta.

Para conectarse a la instancia de base de datos relacional, ejecute el siguiente comando en el terminal. Se configuró una contraseña cuando se instaló la base de datos.
```sql
mysql -u root --password='re:St@rt!9'
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap8.png)

El cliente de línea de comandos MySQL es un shell SQL que puede usar para interactuar con los motores de base de datos.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap9.png)


## Tarea 2: Crear una base de datos y una tabla
En esta tarea, creará una base de datos llamada world y una tabla llamada country. Luego, alterará la tabla country.

Para mostrar las bases de datos existentes, ejecute la siguiente consulta. 
```sql
SHOW DATABASES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap10.png)

Para determinar la base de datos disponible y asegurar que está trabajando con la instancia de base de datos correcta, use el comando SHOW DATABASES;(MOSTRAR BASES DE DATOS). 

Para crear una nueva base de datos llamada world, ejecute en el siguiente comando.
```sql
CREATE DATABASE world;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap11.png)

Para verificar que la base de datos world se haya creado, ejecute la siguiente consulta. 
```sql
SHOW DATABASES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap12.png)

Para almacenar datos en una base de datos, la base de datos debe contener una o más tablas. En una base de datos SQL, una tabla debe tener una estructura bien definida, conocida como el esquema de tabla Para crear una tabla llamada country, ejecute el siguiente comando.  
```sql
CREATE TABLE world.country (
  `Code` CHAR(3) NOT NULL DEFAULT '',
  `Name` CHAR(52) NOT NULL DEFAULT '',
  `Conitinent` enum('Asia','Europe','North America','Africa','Oceania','Antarctica','South  America') NOT NULL DEFAULT 'Asia',
  `Region` CHAR(26) NOT NULL DEFAULT '',
  `SurfaceArea` FLOAT(10,2) NOT NULL DEFAULT '0.00',
  `IndepYear` SMALLINT(6) DEFAULT NULL,
  `Population` INT(11) NOT NULL DEFAULT '0',
  `LifeExpectancy` FLOAT(3,1) DEFAULT NULL,
  `GNP` FLOAT(10,2) DEFAULT NULL,
  `GNPOld` FLOAT(10,2) DEFAULT NULL,
  `LocalName` CHAR(45) NOT NULL DEFAULT '',
  `GovernmentForm` CHAR(45) NOT NULL DEFAULT '',
  `HeadOfState` CHAR(60) DEFAULT NULL,
  `Capital` INT(11) DEFAULT NULL,
  `Code2` CHAR(2) NOT NULL DEFAULT '',
  PRIMARY KEY (`Code`)
);
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap13.png)

Para verificar que se haya creado la tabla country, use el comando SHOW TABLES; (MOSTRAR TABLAS) para mostrar una lista de las tablas en la base de datos. El comando USE (USAR) se usa para especificar contra cuál base de datos se debe ejecutar una consulta. Ejecute los siguientes comandos en el terminal. 
```sql
USE world;
SHOW TABLES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap14.png)

Use la consulta SHOW COLUMNS (MOSTRAR COLUMNAS) para mostrar una lista de todas las columnas en una tabla. Ejecute la siguiente consulta para mostrar una lista de todas las columnas y sus propiedades en la tabla country.
```sql
SHOW COLUMNS FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap15.png)

Nota: Tenga en cuenta que la columna Continent está mal escrita como Conitinent. 

El comando ALTER TABLE (ALTERAR TABLA) se usa para alterar el esquema de la tabla. Para corregir el error tipográfico de la columna Continent, ejecute el siguiente comando.
```sql
ALTER TABLE world.country RENAME COLUMN Conitinent TO Continent;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap16.png)

Para verificar que se corrigió el nombre de la columna Continent en la tabla country, ejecute la siguiente consulta.
```sql
SHOW COLUMNS FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap17.png)

## Desafío 1
Cree una tabla llamada city y agregue dos columnas llamadas Name y Region. Ambas columnas deben usar el tipo de datos CHAR.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap18.png)

resultado: 
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap19.png)

## Tarea 3: Eliminar una base de datos y tabla
En esta tarea, eliminará la base de datos world y la tabla country. 

El comando DROP TABLE se usa para eliminar (descartar) una tabla en una base de datos. Una vez que se descarta una tabla, no se puede recuperar a menos que haya un respaldo disponiible. Para descartar la tabla city, ejecute el siguiente comando.
```sql
DROP TABLE world.city;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap20.png)

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap21.png)

## Desafío 2
Escribe una consulta y descarte la tabla country.
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap22.png)

Resultado:
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/268--Lab-Operaciones%20de%20Tabla%20de%20base/268/Cap23.png)

Para verificar que ambas tablas se hayan descartado, ejecute la siguiente consulta.
```sql
SHOW TABLES;
```
Para descartar la base de datos world, ejecute el siguiente comando.
```sql
DROP DATABASE world;
```
Para verificar que la base de datos world se haya eliminado, ejecute la siguiente consulta.
```sql
SHOW DATABASES;
```







