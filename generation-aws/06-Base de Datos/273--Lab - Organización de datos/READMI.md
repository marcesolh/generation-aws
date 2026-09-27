# Laboratorio / Práctica: Organización de datos

Escenario

El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Ayudará a escribir algunas consultas a los registros de grupo para su análisis usando ambas cláusulas GROUP BY y OVER.




## 🚀 Información general y objetivos del laboratorio
Este laboratorio demuestra cómo usar funciones de base de datos comunes con las cláusulas GROUP BY y OVER.

Después de completar este laboratorio, podrá realizar lo siguiente:

* Usar la cláusula GROUP BY con la función agregada SUM()
* Usar la cláusula OVER con la función de ventana RANK()
*Usar la cláusula OVER con la función agregada SUM() y la función de ventana RANK()

Cuando comience este en laboratorio, los siguientes recursos ya estarán creados para usted:
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap1.png)

Una instancia de Command Host y una base de datos world que contiene tres tablas

Al final de este laboratorio, habrá usado ambas cláusulas GROUP BY y OVER con algunos operadores de base de datos comunes:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap2.png)

Un usuario de laboratorio está conectado a una instancia de base de datos. También muestra algunas cláusulas y funciones de base de datos SQL usadas con frecuencia.

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
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap3.png)

## Tarea 2: Consulte la base de datos world

En esta tarea, consultará la base de datos world usando varias statement SELECT y funciones de la base de datos.
Para mostrar las bases de datos existentes, ingrese el siguiente comando en el terminal.
```sql
SHOW DATABASES;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap4.png)

Verifique que la base de datos llamada world esté disponible. Si la base de datos world no está disponible, póngase en contacto con su instructor.

Para ver el esquema, los datos y la cantidad de filas de la tabla en la tabla country, ejecute la siguiente consulta.
```sql
SELECT * FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap5.png)

Para arrojar una lista de registros donde Region es Australia and New Zealand, ejecute la siguiente consulta. Esta consulta incluye una cláusula ORDER BY (introducida en un laboratorio anterior) que ordena los resultados por Population en orden descendente.

```sql
SELECT Region, Name, Population FROM world.country WHERE Region = 'Australia and New Zealand' ORDER By Population desc;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap6.png)

Puede usar en la cláusula GROUP BY para agrupar registros relacionados. El siguiente ejemplo comienza filtrando los registros que usan una condición en la que la región es igual a Australia and New Zealand. Luego, los resultados se agrupan usando una cláusula GROUP BY. Luego, la función SUM() se aplica a los resultados agrupados para generar una población total para esa región. Ejecute la siguiente consulta en el termin

```sql
SELECT Region, SUM(Population) FROM world.country WHERE Region = 'Australia and New Zealand' GROUP By Region ORDER By SUM(Population) desc;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap7.png)

Esta consulta arroja una SUM() de Population para la región Australia and New Zealand. Ya que la cláusula WHERE está filtrada por Region, solo se agregan los registros de Australia and New Zealand. 

El siguiente ejemplo usó una función de ventana para generar un total continuo al agregar Population de primer registro a Population el segundo registro y los registros posteriores. Esta consulta usa la cláusula OVER() para agrupar los registros por Region y usa la función SUM() para agregar los registros. El resultado muestra la población de un país junto con el total continuo de la región. Ejecute la siguiente consulta en el terminal.

```sql
SELECT Region, Name, Population, SUM(Population) OVER(partition by Region ORDER BY Population) as 'Running Total' FROM world.country WHERE Region = 'Australia and New Zealand';
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap8.png)

La siguiente consulta agrupa los registros por Region y los ordena por Population con la cláusula OVER(). Esta consulta también incluye la función RANK() para generar un número de rango que indica la posición de cada registro en el conjunto de resultados. La función RANK() es útil cuando trabaja con un gran grupo de registros. Ejecute la siguiente consulta en el terminal.

```sql
SELECT Region, Name, Population, SUM(Population) OVER(partition by Region ORDER BY Population) as 'Running Total', RANK() over(partition by region ORDER BY population) as 'Ranked' FROM world.country WHERE region = 'Australia and New Zealand';
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap9.png)

## Desafío

Describa una consulta para calificar los países en cada región por su población de mayor a menor.
Tiene que determinar si usar la cláusula de agrupación GROUP BY o OVER y la función SUM() o RANK().

Resultado:
```sql
SELECT Region, Name, Population, RANK() OVER(partition by Region ORDER BY Population desc) as 'Ranked' FROM world.country order by Region, Ranked;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap10.png)

resultado de filas.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/273--Lab%20-%20Organizaci%C3%B3n%20de%20datos/273/Cap11.png)

## Conclusión

Aprendió a realizar correctamente las siguientes actividades:

* Usar la cláusula GROUP BY con la función agregada SUM()

* Usar la cláusula OVER con la función de ventana RANK()

* Usar la cláusula OVER con la función agregada SUM() y la función de ventana RANK()

Para obtener más información acerca de las funciones y operadores de bases de datos, consulte los siguientes recursos:


[Cláusula GROUP By](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/group-by)

[Clausula OVER](https://mariadb.com/docs/server/reference/sql-functions/special-functions/window-functions/window-functions-overview)

[Función SUM](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/sum)

[Función RANK](https://mariadb.com/docs/server/reference/sql-functions/special-functions/window-functions/rank)

[Statements SELECT](https://mariadb.com/docs?q=select)

[Función COUNT](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/count)
