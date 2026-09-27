# Laboratorio / Práctica: Realización de una búsqueda condicional

## 📋 Escenario
El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Para ayudar al equipo, escribirá algunas consultas para buscar registros en la tabla country usando la statement SELECT y una cláusula WHERE.


## 🚀 Información general y objetivos del laboratorio
Este laboratorio muestra cómo usar la statement SELECT y una cláusula WHERE para filtrar los registros con una búsqueda condicional.

Después de completar este laboratorio, podrá realizar lo siguiente:

Escribir una condición de búsqueda usando la cláusula WHERE
* Usar el operador BETWEEN
* Usar el operador LIKE con caracteres de comodín
* Usar el operador AS para crear un alias de columna
* Usar funciones en una statement SELECT
* Usar funciones en una cláusula WHERE
* Cuando comience este en laboratorio, los siguientes recursos ya estarán creados para usted:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap01.png)

La instancia de Command Host tiene un cliente de base de datos instalado. Usará el Command Host para consultar la base de datos world, que contiene tres tablas.

Al final de este laboratorio, habrá aprendido a usar la cláusula WHERE, el operador BETWEEN y la función LIKE para filtrar registros:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap02.png)

Un usuario de laboratorio se conecta a una instancia de Command Host para consultar las tablas en la base de datos world.

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
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap2.png)

## Tarea 2: Consulte la base de datos world

En esta tarea, consultará la base de datos world usando varias statement SELECT y funciones de la base de datos.
Para mostrar las bases de datos existentes, ingrese el siguiente comando en el terminal.
```sql
SHOW DATABASES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap3.png)

Verifique que la base de datos llamada world esté disponible. Si la base de datos world no está disponible, póngase en contacto con su instructor.

Para ver el esquema, los datos y la cantidad de filas de la tabla en la tabla country, ejecute la siguiente consulta.
```sql
SELECT * FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap4.png)

Al reducir la cantidad de registros, el conjunto resultados será más pequeño y más fácil para trabajar. Para limitar la cantidad de registros que se arrojan, puede usar una cláusula WHEREPara definir las condiciones con las que deben coincidir los registros.

Use el operador AND para combinar dos condiciones. Cada registro se comprueba contra ambas condiciones antes de incluirlo en el conjunto de resultados. Puede usar el operador > y el operador = para consultar los valores que son mayores o iguales a un valor terminado. De manera similar, puede combinar el operador ** <** y el operador = para consultar los valores que son mayores o iguales a un valor terminado.
Para reducir la cantidad de registros en el conjunto de resultados utilizando una cláusula WHERE y el operador AND, ejecute la siguiente consulta.
```sql
SELECT Name, Capital, Region, SurfaceArea, Population FROM world.country WHERE Population >= 50000000 AND Population <= 100000000;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap5.png)

Cuando busque registros usando una condición de rango, puede usar el operador BETWEEN en lugar del operador >= y el operador <=. Al usar el operador BETWEEN, la consulta es más fácil de leer. Tengan cuenta que el operador es inclusivo, lo que significa que los valores iniciales y finales están incluidos.
Por una lista de todas las columnas en la tabla country, ejecute la siguiente consulta. Esta consulta se ejecuta para comprender el esquema de la tabla.

Para arrojar los mismos registros que el conjunto de resultados anterior usando el operador BETWEEN, ejecute la siguiente consulta.

```sql
SELECT Name, Capital, Region, SurfaceArea, Population FROM world.country WHERE Population BETWEEN 50000000 AND 100000000;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap6.png)

Puede usar la función LIKE para buscar un patrón de cadenas. La siguiente consulta arrojara registros que incluyen la cadena Europe en la columna Region. El símbolo de porcentaje (%) es un carácter de comodín que representa una variedad de caracteres antes o después de la palabra Europe. La consulta agregará la población de todos los países europeos usando la función SUM.

Para arrojar la población de todos los países europeos usando la función LIKE y la función SUM, ejecute la siguiente consulta.

```sql
SELECT sum(Population) from world.country WHERE Region LIKE "%Europe%";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap7.png)

En la consulta anterior, la cláusula SELECT incluyó una función SUM. En la siguiente consulta, la función SUM todavía se usa para calcular la población total de Europa. A consulta también incluye un alias de columna, que hace que el resultado sea más fácil de leer. Para definir el alias de columna, se usa el comando AS en la statement SELECT.

Para arrojar la misma información que la consulta anterior con el alias de columna, ejecute la siguiente consulta.

```sql
SELECT sum(population) as "Europe Population Total" from world.country WHERE region LIKE "%Europe%";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap8.png)

Tenga en cuenta que SQL no es un idioma que distinga entre mayúsculas y minúsculas. Puede usar SELECT o select cuando escriba una consulta. Sin embargo, las bases de datos que consulte pueden estar configuradas con una compaginación que distinga entre mayúsculas y minúsculas. Si la base de datos distingue entre mayúsculas y minúsculas, no podrá consultar una columna llamada Population usando la siguiente: select population from world.country

Aunque la base de datos que se usa en este laboratorio no distingue entre mayúsculas y minúsculas, recomendamos que sus consultas sean consistentes con la nomenclatura utilizada en la base de datos.

El siguiente ejemplo demuestra cómo realizar una consulta que distinga entre mayúsculas y minúsculas. Según la configuración de la base de datos, cuando compare Central con central, el resultado puede ser falso, porque las cadenas no usa las mismas mayúsculas. Para resolver este problema, puede usar la función LOWER en la cláusula WHERE para comparar ambas cadenas en minúscula..

Para realizar una consulta que distinga entre mayúsculas y minúsculas usando la función LOWER, ejecute la siguiente consulta.

```sql
SELECT Name, Capital, Region, SurfaceArea, Population from world.country WHERE LOWER(Region) LIKE "%central%";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap9.png)

## 🛠️ Desafio:
Escriba una consulta para arrojar la suma del área de superficie y de la población de Norteamérica.
Resultado:
```sql
SELECT SUM(SurfaceArea) as "N. America Surface Area", SUM(Population) as "N. America Population" FROM world.country WHERE Region = "North America";
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/271--Lab%20-%20Realizaci%C3%B3n%20de%20una%20b%C3%BAsqueda%20condicional/271/Cap10.png)

Para obtener más información acerca de las funciones y operadores de bases de datos, consulte los siguientes recursos:


[Cláusula WHERE](https://mariadb.com/docs?q=select)

[Operador BETWEEN](https://mariadb.com/docs/server/reference/sql-structure/operators/comparison-operators/between-and)

[Función LIKE](https://mariadb.com/docs/server/reference/sql-functions/string-functions/like)

[Función SUM](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/sum)

[Función LOWER](https://mariadb.com/docs/server/reference/sql-functions/string-functions/lower)




