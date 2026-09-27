# Laboratorio / Práctica: Trabajar con funciones

## 📋 Escenario
El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Según los casos prácticos específicos definidos en el ejercicio de laboratorio, escribirá algunas consultas usando funciones de base de datos con la statement SELECT y la cláusula WHERE.


## 🚀 Información general y objetivos del laboratorio
Este laboratorio demuestra cómo usar funciones de base de datos comunes con la statement SELECT y la cláusula WHERE.

Después de completar este laboratorio, podrá realizar lo siguiente:

* Use las funciones agregadas SUM(), MIN(), MAX() y AVG() para resumir datos.
* Use la función SUBSTRING_INDEX() para dividir las cadenas.
* Use las funciones LENGTH() y TRIM() para determinar la longitud de una cadena
* Use la función DISTINCT() para filtrar los registros duplicados
* Use las funciones en la statement SELECT y la cláusula WHERE
  
Cuando comience este en laboratorio, los siguientes recursos ya estarán creados para usted:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap01.png)

Una instancia de Command Host y una base de datos world que contiene tres tablas

Al final de este laboratorio, habrá usado la statement SELECT y la cláusula WHERE con algunas funciones de base de datos comunes:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap02.png)

Un usuario de laboratorio está conectado a una instancia de base de datos. También muestra algunas funciones de base de datos SQL usadas con frecuencia.

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
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap1.png)

## Tarea 2: Consulte la base de datos world

En esta tarea, consultará la base de datos world usando varias statements SELECT y funciones de la base de datos. Usará una función para procesar y manipular los datos en una consulta. Hay una amplia variedad de funciones SQL y este laboratorio revisa un subconjunto de funciones utilizadas con frecuencia.

```sql
SHOW DATABASES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap2.png)

Verfique que la base de datos world esté disponible. Si la base de datos world no está disponible, póngase en contacto con su instructor.

Para mostrar una lista de todas las columnas y sus propiedades en la tabla country, ejecute la siguiente consulta.
```sql
SELECT * FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap3.png)

La siguiente consulta demuestra cómo usar las funciones agregadas SUM(), MIN(), MAX() y AVG() para resumir datos. Ya que la consulta no incluye una condición WHERE, la función agrega datos de todos los registros en la tabla country. Ejecute la siguiente consulta.
```sql
SELECT sum(Population), avg(Population), max(Population), min(Population), count(Population) FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap4.png)

* SUM() suma todos los valores de población juntos.
* AVG() genera un promedio de todos los valores de población.
* MAX() encuentra la fila con el valor de población más alto.
* MIN() encuentra la fila con el valor de población más bajo.
* COUNT() encuentra la cantidad de filas con un valor de población.
  
En algunos casos, es posible que necesite dividir una cadena. La siguiente consulta usa SUBSTRING_FUNCTION() para dividir una cadena en la que ocurre un espacio. Ejecute la siguiente consulta.

```sql
SELECT Region, substring_index(Region, " ", 1) FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap5.png)

Después de ejecutar la consulta, notará que la segunda columna incluye el comienzo del nombre de cada región.  
A veces puede necesitar buscar filas usando un fragmento de cadena. La siguiente consulta incluye SUBSTRING_FUNCTION() como parte de una condición en la cláusula WHERE para filtrar registros que incluyen Southern en la primera parte del nombre de la región. Ejecute la siguiente consulta.

```sql
SELECT Name, Region from world.country WHERE substring_index(Region, " ", 1) = "Southern";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap6.png)
Puede usar las funciones LENGTH() y TRIM() para determinar cuántos caracteres tiene una cadena. TRIM() borra los espacios en blanco iniciales y finales y la función LENGTH() arroja un conteo de los caracteres resultantes. Siguiente ejemplo arroja las regiones que tienen menos de diez caracteres en sus nombres. Ejecute la siguiente consulta.
```sql
SELECT Region FROM world.country WHERE LENGTH(TRIM(Region)) < 10;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap7.png)

Es posible que haya notado registros duplicados en el ejemplo anterior. Puede usar la función DISTINCT() para filtrar los duplicados. Ejecute la siguiente consulta.

```sql
SELECT DISTINCT(Region) FROM world.country WHERE LENGTH(TRIM(Region)) < 10;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap8.png)

## Desafío
Consulte la tabla country para arrojar un conjunto de registros basado en el siguiente requisito.
```sql
SELECT Name, substring_index(Region, "/", 1) as "Region Name 1",substring_index(region, "/", -1) as "Region Name 2" FROM world.country WHERE Region = "Micronesia/Caribbean";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/272--Lab%20-%20Trabajar%20con%20funciones/272/Cap9.png)

## Conclusión
* Usar las funciones agregadas SUM(), MIN(), MAX() y AVG() para resumir datos.
* Usar la función SUBSTRING_INDEX() para dividir las cadenas.
* Usar las funciones LENGTH() y TRIM() para determinar la longitud de una cadena
* Usar la función DISTINCT() para filtrar los registros duplicados
* Usar las funciones en la statement SELECT y la cláusula WHERE

Para obtener más información acerca de las funciones y operadores de bases de datos, consulte los siguientes recursos:

[Statements SELECT](https://mariadb.com/docs?q=select)

[Función Count](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/count)

[Función SUM](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/sum)

[Función AVG](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/avg)

[Función MIN](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/min)

[Función MAX](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/max)

[Función SUBSTRING_INDEX](https://mariadb.com/docs/server/reference/sql-functions/string-functions/substring_index)

[Función LENGTH](https://mariadb.com/docs/server/reference/sql-functions/string-functions/length)

[Función TRIM](https://mariadb.com/docs/server/reference/sql-functions/string-functions/length)



