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



