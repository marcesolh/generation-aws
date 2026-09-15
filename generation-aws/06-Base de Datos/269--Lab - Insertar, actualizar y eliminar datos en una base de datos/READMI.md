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
Junto a la instancia etiquetada Command Host, seleccione la casilla  y luego seleccione Connect (Conectar).
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

Para mostrar las bases de datos existentes, ingrese el siguiente comando en el terminal. Tome nota delas bases de datos actualmente disponibles.
```sql
SHOW DATABASES;
```
resultado:
![](https://github.com/marcesolh/generation-aws/blob/main/generation-aws/06-Base%20de%20Datos/img/C1.png)


