# Laboratorio / Práctica: Insertar, actualizar y eliminar datos en una base de datos

## 📋 Descripción del Reto
Este laboratorio muestra cómo insertar, actualizar, eliminar e importar filas de datos usando el Lenguaje de consulta estructurada (SQL).

Después de completar este laboratorio, podrá hacer lo siguiente:

Insertar filas en una tabla
Actualizar filas de una tabla
Eliminar filas de una tabla
Importar filas de un archivo de respaldo de base de datos
Cuando comience este laboratorio, los siguientes recursos ya estarán creados para usted:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/recursos1.jpg)

Una instancia de Command Host y una base de datos world que contiene tres tablas
Al finalizar este laboratorio, la arquitectura se verá como en el siguiente ejemplo:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/recursos2.jpg)

Un usuario de laboratorio está conectado a una instancia de base de datos. Se muestran las operaciones Insertar, Actualizar y Eliminar.
Los datos de muestra en este curso se obtuvieron de Statistics Finland, estadísticas regionales generales, 4 de febrero de 2022.


## Escenario
* El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Tiene que validar la configuración de la base de datos al ejecutar los statements INSERT, UPDATE y DELETE en la tabla country.  

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Base de Datos / Motor:** (Ej. PostgreSQL, MySQL, Amazon RDS, etc.)
* **Herramienta de Consulta (IDE):** (Ej. DBeaver, pgAdmin, MySQL Workbench, etc.)
* **Conceptos aplicados:** (Ej. INNER JOIN, GROUP BY, Subconsultas, Índices, etc.)




## 🚀 Desarrollo y Solución
Tarea 1: Conectar a una base de datos

En esta tarea, se conecta a una instancia que contiene un cliente de base de datos, que se usa para conectarse a una base de datos. Esta instancia se conoce como Command Host.
En la Consola de administración de AWS, seleccione el menú  Services (Servicios). En Compute (Cómputo), seleccione EC2.
En el panel de navegación izquierdo, elija Instances (Instancias).
Junto a la instancia etiquetada Command Host, seleccione la casilla  y luego seleccione Connect (Conectar)(referido en la siguiente imagen).
Nota: Si no ve Command Host, probablemente el laboratorio aún está siendo aprovisionado, o quizás esté usando otra Región.

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/instancia%20Ec2.jpg)
En Connect to instance (Conexión a instancia), elija la pestaña Session Manager.
Elija Connect (Conectar) para abrir una ventana de terminal.
Nota: Si el botón Connect (Conectar) no está disponible, espere unos minutos y vuelva a intentarlo.
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/entrar%20a%20la%20consola.png)
consola.
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Consola.png)



```sql
-- 1.-Para configurar la terminal para acceder a todas las herramientas y recursos necesarios, ejecutando el siguiente comando:

sh-4.2$ sudo su
[root@ip-10-1-11-220 bin]# cd /home/ec2-user/

-- 2.-Para conectarse a la instancia de base de datos, se ejecuta el siguiente comando en el terminal. Se configuró una contraseña cuando se instaló la base de datos.

[root@ip-10-1-11-220 ec2-user]# mysql -u root --password='re:St@rt!9'

```
 El cliente de línea de comandos MySQL es un shell SQL que puede usar para interactuar con los motores de base de datos.
 
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Descripci%C3%B3n1.png)

resultado:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/C1.png)

Para mostrar las bases de datos existentes, ingrese el siguiente comando en el terminal. Tome nota delas bases de datos actualmente disponibles.
```sql
SHOW DATABASES;
```

resultado:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/C2.png)


Tarea 2: Insertar datos en una tabla
En esta tarea, insertará datos de muestra en la tabla country.

1-Para verificar que la tabla country este vacía, ejecute el siguiente comando. La statement SELECT se usa para identificar las columnas que se deben incluir en el conjunto de resultados. El uso de * indica todas las columnas. La cláusula FROM se usa en el siguiente ejemplo para especificar la base de datos y la tabla que se está consultando.

```sql
SELECT * FROM world.country;
```
La tabla debe estar vacía porque se acaba de crear.

2-Para insertar filas en la tabla country, ejecute los siguientes comandos. Los valores en la cláusula VALUES deben estar en el mismo oren que se definió en el esquema de tabla. 

```sql
INSERT INTO world.country VALUES ('IRL','Ireland','Europe','British Islands',70273.00,1921,3775100,76.8,75921.00,73132.00,'Ireland/Éire','Republic',1447,'IE');

INSERT INTO world.country VALUES ('AUS','Australia','Oceania','Australia and New Zealand',7741220.00,1901,18886000,79.8,351182.00,392911.00,'Australia','Constitutional Monarchy, Federation',135,'AU');
```
resultado: 
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Insert1.png)

3-Para verificar que se insertaron dos filas correctamente en la tabla country, ejecute la siguiente consulta.

```sql
SELECT * FROM world.country;
```
La tabla ahora debe contener dos filas y debe aparecer como se muestra a continuación:

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Descripci%C3%B3n2.png)

![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/tabla%20country.png)





Tarea 3: Actualizar filas en una tabla
En esta tarea, actualizará ambas filas en la tabla country usand una statement UPDATE.
Para establecer el valor en la columna Population en 0 para ambas filas en la tabla country, ejecute la siguiente statement UPDATE. 

```sql
UPDATE world.country SET Population = 0;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Cap1.png)

Todas las filas se actualizan porque la statement UPDATE no incluye una condición WHERE. Una cláusula WHERE usa condiciones para filtrar filas arrojadas por una consulta. El siguiente laboratorio introduce la cláusula WHERE.

Para verificar que la columna Population en la tabla country se actualizó, ejecute el siguiente comando.

```sql
SELECT * FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Cap2.png)

Para establecer el valor en la columna Population en 0 para ambas filas en la tabla country, ejecute la siguiente statement UPDATE.

```sql
UPDATE world.country SET Population = 100, SurfaceArea = 100;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Cap3.png)

Para verificar que la columna Population y SurfaceArea en la tabla country se actualizaron, ejecute el siguiente comando.

```sql
SELECT * FROM world.country;
```
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/Cap4.png)





Tarea 4: Eliminar filas de una tabla
En esta tarea, actualizará ambas filas en la tabla country usando una statement DELETE. 

Tenga cuidado cuando use statements de manipulación de datos como UPDATE y DELETE ya que estos cambios pueden no ser reversibles. 

Para eliminar las filas ALL desde la tabla country, ejecute el siguiente comando. 
```sql
DELETE FROM world.country;
```
Ya que la statement DELETE no incluye una condición WHERE, se eliminan todas las filas.

Para verificar que todas las filas se eliminaron de la tabla country, ejecute el siguiente comando.
```sql
SELECT * FROM world.country;
```


