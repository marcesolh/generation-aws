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



## Escenario
* El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Tiene que validar la configuración de la base de datos al ejecutar los statements INSERT, UPDATE y DELETE en la tabla country.  

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Base de Datos / Motor:** (Ej. PostgreSQL, MySQL, Amazon RDS, etc.)
* **Herramienta de Consulta (IDE):** (Ej. DBeaver, pgAdmin, MySQL Workbench, etc.)
* **Conceptos aplicados:** (Ej. INNER JOIN, GROUP BY, Subconsultas, Índices, etc.)

## 🚀 Desarrollo y Solución
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

