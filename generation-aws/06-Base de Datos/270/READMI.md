# Laboratorio / Práctica: Selección de datos de una base de datos

## 📋 Escenario
El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Según los casos prácticos específicos definidos en el ejercicio de laboratorio, escribirá algunas consultas usando operadores de base de datos y la statement SELECT.


Breve descripción con tus propias palabras de qué problema resolvía este laboratorio o qué objetivo de negocio simulaba la práctica. 
* *Ejemplo:* Consulta de base de datos relacional para obtener métricas de ventas y comportamiento de clientes utilizando funciones de agregación y uniones (JOINs).

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Base de Datos / Motor:** (Ej. PostgreSQL, MySQL, Amazon RDS, etc.)
* **Herramienta de Consulta (IDE):** (Ej. DBeaver, pgAdmin, MySQL Workbench, etc.)
* **Conceptos aplicados:** (Ej. INNER JOIN, GROUP BY, Subconsultas, Índices, etc.)

## 🚀 Información general y objetivos del laboratorio
Este laboratorio muestra cómo usar algunas operaciones de bases de datos comunes y la statement SELECT.
Después de completar este laboratorio, podrá realizar lo siguiente:

* Usar la statement SELECT para consultar una base de datos

* Usar la función COUNT ()

## Use las siguientes operaciones para consultar una base de datos:
```sql
  <
  >
  =
  WHERE
  ORDER BY
  AND
```
Cuando comience este en laboratorio, los siguientes recursos ya estarán creados para usted:
![]()

Una instancia de Command Host y una base de datos world que contiene tres tablas
Al final de este laboratorio, habrá usado la statement SELECT y algunas operaciones de base de datos comunes:

![]()

Un usuario de laboratorio está conectado a una instancia de base de datos. También muestra algunas operaciones de base de datos que se usan con frecuencia.

Los datos de muestra en este curso se obtuvieron de Statistics Finland, estadísticas regionales generales, 4 de febrero de 2022.

## Tarea 1: Conectarse a Command Host

En esta tarea, se conecta a una instancia que contiene un cliente de base de datos, que se usa para conectarse a una base de datos. Esta instancia se conoce como Command Host.

En la Consola de administración de AWS, seleccione el menú  Services (Servicios). Seleccione Compute (Cómputo) y luego seleccione EC2.

En el menú de navegación izquierdo, seleccione Instances (Instancias).

Junto a la instancia etiquetada Command Host, seleccione la casilla  y luego seleccione Connect (Conectar).

Nota: Si no ve Command Host, probablemente el laboratorio aún está siendo aprovisionado, o quizás esté usando otra Región.

Para Connect to instance (Conectarse a instancia), seleccione la pestaña Session Manager.

Seleccione Connect (Conectar) para abrir una ventana de terminal.

Nota: Si el botón Connect (Conectar) no está disponible, espere unos minutos y vuelva a intentarlo.


Para configurar la terminal para acceder a todas las herramientas y recursos necesarios, ejecute el siguiente comando:

```sql
sudo su
cd /home/ec2-user/
```
Para conectarse al servicio de base de datos, ejecute el siguiente comando en el terminal. Se configuró una contraseña cuando se instaló la base de datos.

```sql
mysql -u root --password='re:St@rt!9'
```

## Tarea 2: Consulte la base de datos world

En esta tarea, consultará la base de datos world usando varias statement SELECT y funciones de la base de datos.
Para mostrar las bases de datos existentes, ingrese el siguiente comando en el terminal.
```sql
SHOW DATABASES;
```
Verifique que la base de datos llamada world esté disponible. Si la base de datos world no está disponible, póngase en contacto con su instructor.

Para mostrar una lista de todas las columnas y sus propiedades en la tabla country, ejecute la siguiente consulta.
```sql
SELECT * FROM world.country;
```
Para consultar la cantidad de filas en una tabla, puede usar la función COUNT() en una statement SELECT. Para contar todas las filas en la tabla, puede usar COUNT(*). Para contar la cantidad de filas que tienen un valor en una columna específica, incluya nombre de la columna como un parámetro en la función COUNT(): por ejemplo, COUNT(Population). Para una lista de la cantidad de filas en la tabla country, ejecute la siguiente consulta.
```sql
SELECT COUNT(*) FROM world.country;
```

Por una lista de todas las columnas en la tabla country, ejecute la siguiente consulta. Esta consulta se ejecuta para comprender el esquema de la tabla.
```sql
SHOW COLUMNS FROM world.country;
```
Para consultar columnas específicas en la tabla world, ejecute la siguiente consulta para arrojar un conjunto de resultados que incluya las columnas Name, Capital, Region, SurfaceArea y Population.
```sql
SELECT Name, Capital, Region, SurfaceArea, Population FROM world.country;
```
Los nombres de columnas de la base de datos en ocasiones no son fáciles de usar para los usuarios. Para agregar un nombre de columna más descriptivo al resultado de la consulta, puede usar la opción AS. Ejecute la siguiente consulta que incluya esta opción.
```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country;
```
De ser necesario, desplazarse hasta la parte superior de los resultados de la consulta y observe que la columna SurfaceArea se muestre como Surface Area.

Los conjuntos de resultados ordenados son más fáciles de ver y trabajar con ellos. Si quiere ordenar el resultado según una columna, puede usar la opción ORDER BY. En este ejemplo,ordenará los resultados según la población.
```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country ORDER BY Population;
```
La opción ORDER BY ordena los datos en orden ascendente.

Para ordenar los datos en orden descendente, use la opción DESC con ORDER BY. Ejecute el siguiente comando con esta opción.  
```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country ORDER BY Population DESC;
```
Puede agregar condiciones a las statements SELECT usando la cláusula WHERE. Por ejemplo, para listar todas las filas con una población mayor de 50.000.000, ejecute la siguiente consulta.
```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country WHERE Population > 50000000 ORDER BY Population DESC;
```
Usó el operador de comparación >. De forma similar, puede usar otros operadores de comparación para comparar valores.

Puede construir una cláusula WHERE usando una serie de condiciones y operadores. 

La siguiente consulta usa dos condiciones: todas las filas con una población mayor de 50.000.000 y todas las filas que una población menor de 100.000.000. La consulta incluye el operador AND para indicar que ambas condiciones deben ser verdaderas. Ejecute la siguiente consulta en el terminal.
```sql
SELECT Name, Capital, Region, SurfaceArea AS "Surface Area", Population FROM world.country WHERE Population > 50000000 AND Population < 100000000 ORDER BY Population DESC;
```
Para obtener más información acerca de los operadores de comparación, consulte la sección Recursos adicionales al final del laboratorio.

![operadores de comparación](https://mariadb.com/docs/server/reference/sql-structure/operators/comparison-operators)


