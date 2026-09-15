# Laboratorio / Práctica: Insertar, actualizar y eliminar datos en una base de datos

## 📋 Descripción del Reto
Breve descripción con tus propias palabras de qué problema resolvía este laboratorio o qué objetivo de negocio simulaba la práctica. 
* *Ejemplo:* Consulta de base de datos relacional para obtener métricas de ventas y comportamiento de clientes utilizando funciones de agregación y uniones (JOINs).

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

