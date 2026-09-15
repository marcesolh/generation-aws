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
En Connect to instance (Conexión a instancia), elija la pestaña Session Manager.
Elija Connect (Conectar) para abrir una ventana de terminal.
Nota: Si el botón Connect (Conectar) no está disponible, espere unos minutos y vuelva a intentarlo.



Aquí puedes documentar los pasos lógicos que seguiste para resolverlo:
1. Análisis del diagrama de entidad-relación (ER).
2. Construcción de las consultas SQL paso a paso.

### Código Destacado
Inserta los fragmentos de código más importantes o complejos que hayas escrito. Usar bloques de código ayuda a que se vea profesional:

```sql
-- Ejemplo de consulta desarrollada en el laboratorio
SELECT 
    c.nombre_cliente,
    SUM(f.total_venta) AS total_gastado
FROM 
    clientes c
INNER JOIN 
    facturas f ON c.id_cliente = f.id_cliente
GROUP BY 
    c.nombre_cliente
ORDER BY 
    total_gastado DESC;

