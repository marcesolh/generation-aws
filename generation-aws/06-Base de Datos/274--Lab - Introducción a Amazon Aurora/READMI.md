# Laboratorio / Práctica: Introducción a Amazon Aurora

## 📋 Información general
Este laboratorio le presenta Amazon Aurora y le proporciona una comprensión básica de cómo usar Aurora. Seguirá los pasos para crear una instancia de Aurora y luego conectarse a ella.


## 🛠️ Temas tratados

Después de completar este laboratorio, podrá hacer lo siguiente:

* Crear una instancia de Aurora
* Conectarse a una instancia de Amazon Elastic Compute Cloud (Amazon EC2)
* Configurar la instancia de Amazon EC2 para conectarse a Aurora
* Consultar la instancia de Aurora


## 🚀 Presentación de las tecnologías

Amazon Aurora

Aurora es un motor de base de datos relacional completamente administrado, compatible con MySQL que combina el rendimiento y la fiabilidad de las bases de datos comerciales de alto nivel con la simplicidad y la rentabilidad de las bases de datos de código abierto. Brinda hasta cinco veces más rendimiento que MySQL sin requerir cambios a la mayoría de sus aplicaciones insistentes que usan bases de datos MySQL.

Amazon Elastic Compute Cloud (Amazon EC2)

Amazon EC2 es un servicio web que proporciona capacidad de cómputo de tamaño modificable en la nube. Se ha diseñado con el fin de simplificar el uso de la informática en la nube a escala web para los desarrolladores. Amazon EC2 reduce el tiempo necesario para aprovisionar nuevas instancias de servidores a minutos, lo que le permite escalar rápidamente la capacidad, ya sea aumentándola o reduciéndola, según cambien sus requisitos de cómputo.

Amazon Relational Database Service (Amazon RDS)

Amazon RDS facilita las tareas de configuración, utilización y escalado de las bases de datos relacionales en la nube. Proporciona una capacidad rentable y de tamaño modificable y, al mismo tiempo, administra las tediosas tareas de administración de base de datos, lo que le libera para enfocarse en sus aplicaciones y en su negocio. Amazon RDS le ofrece seis motores de base de datos entre los que elegir, incluidos Aurora, Oracle, Microsoft SQL Server, PostgreSQL, MySQL y MariaDB.



## Tarea 1: Crear una instancia de Aurora

Esta tarea, creará una instancia de base de datos (DB) de Aurora.

En la Consola de administración de AWS, seleccione el menú  Services (Servicios). Seleccione Database (Base de datos) y seleccione RDS.

En el menú de navegación izquierdo, seleccione Databases (Bases de datos).

Elija Create database (Crear una base de datos) y configure las siguientes opciones:

* Para Choose a database creation method (Elegir un método de creación de base de datos), seleccione Standard create (Creación estándar).
* Para Engine options (Opciones de motor), seleccione Amazon Aurora.
* En la sección Engine options (Opciones de motor) para Replication features (Características de replicación), seleccione Single-master (Maestro único) (si esta opción no está seleccionada de forma predeterminada).
* En Templates (Plantillas), elija Dev/Test (Desarrollo/pruebas).

En la sección Settings (Configuración), configure las siguientes opciones:

* Cluster Identifier (Identificador del clúster): Ingrese `aurora`
* Master username (Nombre de usuario maestro):Iingrese `admin`
* Master password (Contraseña maestra): Ingrese `admin123`
* Confirm password (Confirmar contraseña): Ingrese `admin123`

En la sección DB instance class (Clase de instancia de base de datos), seleccione Burstable classes (Clases ampliables) y seleccione db.t3.small de la lista desplegable. 

En la sección Availability & durability (Disponibilidad y durabilidad) para la Multi-AZ deployment (Implementación Multi-AZ), seleccione Don”t create an Aurora Replica (No crear una réplica de Aurora).

 
 ```
Las implementaciones Multi-AZ de Amazon RDS proporcionan una disponibilidad y durabilidad mejoradas para las instancias de base de datos, por lo que son la opción ideal para las cargas de trabajo de base de datos de producción. Cuando aprovisiona una instancia de base de datos Multi-AZ, Amazon RDS crea de manera automática una instancia de base de datos primaria y replica de forma sincrónica los datos en una instancia en espera en una zona de disponibilidad diferente.

Ya que este es un entorno de laboratorio, no necesita realizar una implementación Multi-AZ.
 
 ```

En Connectivity (Conectividad), configure las siguientes opciones:

* Para Virtual private cloud (VPC) (Nube privada virtual), seleccione LabVPC.
* Para Subnet group (Grupo de subred), seleccione dbsubnetgroup.
* Para Public access (Acceso público), seleccione No.
* Para VPC security group (Grupo de seguridad de VPC), seleccione Choose existing (Elegir el existente).
* Para Existing VPC security groups (Grupos de seguridad de VPC existentes), elimine el grupo de seguridad predeterminado.
* Desde la lista desplegable Existing VPC security groups (Grupos de seguridad de VPC existentes), seleccione DBSecurityGroup.

 ```
 Las subredes son segmentos del intervalo de direcciones IP de una nube privada virtual (VPC) que designa para agrupar sus recursos de acuerdo con las necesidades operativas y de seguridad. Un grupo de subredes de base de datos es un conjunto de subredes (normalmente privadas) que se crean en una VPC y que luego se designan para las instancias de base de datos. Con un grupo de subred de base de datos, puede especificar un VPC cuando crea instancias de base de datos usando la interfaz de línea de comando (CLI) o interfaz de programación de aplicación (API); si usa la consola, puede seleccionar VPC y las subredes que desea usar.

El grupo de subred de aurora se creó para usted cuando inició el laboratorio usando AWS CloudFormation.

 Puede usar el servicio Amazon Virtual Private Cloud (Amazon VPC) para iniciar recursos de AWS en una red virtual definida por usted. Esta red virtual es prácticamente idéntica a una red tradicional operada en su propio centro de datos, pero con los beneficios de utilizar la infraestructura escalable de AWS.
 
 ```

Expanda  Additional configuration (Configuración adicional) y para Initial database name (Nombre de base de datos inicial), ingrese `world`

En la sección Encryption (Cifrado), cancele la selección de la casilla para Enable encryption (Habilitar cifrado).

 
 ```
Puede habilitar la opción de cifrado en la instancia de base de datos de Amazon RDS para cifrar las instancias e instantáneas de Amazon RDS que se encuentren en reposo. Entre los datos que se cifran en reposo se incluyen el almacenamiento subyacente de una instancia de base de datos, los respaldos automatizados, las réplicas de lectura y las instantáneas.
 
 ```
En Monitoring (Supervisión), borre la selección de la casilla Enable Enhanced monitoring (Habilitar supervisión mejorada).

En la sección Maintenance (Mantenimiento), cancele la selección de la casilla Enable auto minor version upgrade (Habilitar actualización de versión menor automática).

Desplácese hasta la parte inferior de la pantalla y luego elija `Create database` (Crear base de datos)

Su instancia de base de datos de Aurora está en proceso de inicio y puede demorar hasta 5 en iniciarse. Sin embargo, puede continuar con la siguiente tarea.


## Tarea 2: Conectarse a una instancia de Linux de Amazon EC2

En esta tarea, iniciar la sesión en su instancia de Linux de Amazon EC2. Esta instancia se inició para usted cuando inició su laboratorio usando CloudFormation.

En la Consola de administración de AWS, seleccione el menú Services. Seleccione Compute (Cómputo) y luego seleccione EC2.

En el menú de navegación izquierdo, seleccione Instances (Instancias).

Junto a la instancia etiquetada Command Host, seleccione la casilla ** y luego seleccione **Connect (Conectar).

Nota: Si no ve la instancia de Command Host, probablemente el laboratorio aún está siendo aprovisionado, o quizás esté usando otra Región.

Para Connect to instance (Conectarse a instancia), seleccione Session Manager.

Seleccione Connect (Conectar) para abrir una ventana de terminal.

  Nota: Si el botón Connect (Conectar) no está disponible, espere unos minutos y vuelva a intentarlo.

## Tarea 3: Configurar la instancia de Linux de Amazon EC2 para conectarse a Aurora


En esta tarea, configurará la instancia de Linux de Amazon EC2 para conectarse a Aurora.

Para configurar la instancia con el cliente MariaDB, ejecute el siguiente comando. El cliente MariaDB se usa para conectarse a la instancia de Aurora que acaba de crear.

 ```sql
sudo yum install mariadb -y

 ```

 Usando una pestaña distinta del navegador, vuelva a la Consola de administración de AWS. Seleccione el menú  Services (Servicio). Seleccione Database (Base de datos) y luego seleccione RDS.

En el menú de navegación izquierdo, seleccione Volumes (Volúmenes).

Espere que aurora-instance-1 muestre  Available (Disponible).

Seleccione aurora.

Seleccione la pestaña Connectivity & security (Conectividad y seguridad), y en la sección Endpoints (Puntos de enlace), copie el nombre de Endpoint (Punto de enlace) para la instancia de Writer (Escritor) su editor de texto.

El punto de enlace debe ser similar a lo siguiente: aurora.cluster-cabcdefghijklm.us-west-2.rds.amazonaws.com

```
Tipos de puntos de enlace de Aurora
Un puntos de enlace se representa como una URL especifica de Aurora que contiene una dirección de host y un puerto. Los siguientes tipos de puntos de enlace están disponibles desde un clúster de base de datos de Aurora.

Punto de enlace de clúster:
* Un punto de enlace de clúster para un clúster de base de datos de Aurora se conecta a la instancia de base de datos primaria para ese clúster de base de datos. Este punto de enlace es el único que puede realizar operaciones de escritura, como statements DDL. Debido a esto, el punto de enlace de clúster es al que se conecta cuando configura un clúster por primera vez o cuando su clúster contiene solo una instancia de base de datos.

Cada clúster de base de datos de Aurora tiene un punto de enlace de clúster y una instancia de base de datos primaria.

Usa el punto de enlace de clúster para todas las operaciones de escritura en el clúster de base de datos, incluidas las inserciones, actualizaciones, eliminaciones y cambios de DDL. También puede usar el punto de enlace de clúster para operaciones de lectura, como consultas.

El punto de enlace del clúster proporciona soporte para conexiones de lectura/escritura al clúster de base de datos. Si la instancia de base de datos primaria de una base de datos falla, Aurora automáticamente realizada la conmutación por error a una nueva instancia de base de datos primaria. Durante una conmutación por error el clúster de base de datos continúa realizando solicitudes de conexión al punto de enlace del clúster desde la nueva instancia de base de datos primaria.

El siguiente ejemplo ilustra un punto de enlace para un clúster de base de datos de MySQL de Aurora.

mydbcluster.cluster-123456789012.us-west-2.rds.amazonaws.com:3306

* Punto de enlace del lector:
Un punto de enlace del lector para un clúster de base de datos de Aurora se conecta a una de las réplicas de Aurora disponibles para ese clúster de base de datos. Cada clúster de base de datos de Aurora tiene un punto de enlace del lector. Si hay más de una replica de Aurora, el punto de enlace del lector dirige cada solicitud de conexión a una de las réplicas de Aurora.

El punto de enlace del lector proporciona soporte de equilibrio de carga para conexiones de solo lectura al clúster de base de datos. También puede usar el punto de enlace del lector para operaciones de lectura, como consultas. No puede usar el punto de enlace del lector para operaciones de escritura.

El clúster de base de datos distribuye solicitudes de conexión al punto de enlace del lector entre las réplicas de Aurora disponibles. Si el clúster de base de datos contiene solo una instancia de base de datos primaria, el punto de enlace del lector realiza solicitudes de conexión desde la instancia de base de datos primaria. Si se crean una o más replicas de Aurora para ese clúster de base de datos, las conexiones posteriores al punto de enlace del lector usan balanceo de carga entre las réplicas.

El siguiente ejemplo ilustra un punto de enlace del lector de base de datos de MySQL de Aurora.

mydbcluster.cluster-ro-123456789012.us-west-2.rds.amazonaws.com:3306
```
En el siguiente comando, reemplace <endpoint_goes_here> con el punto de enlace que copió en su editor de texto. 

```sql
mysql -u admin --password='admin123' -h <endpoint_goes_here>
```

Su comando debe ser similar a lo siguiente:

mysql -u admin --password='admin123' -h mydbcluster.cluster-123456789012.us-west-2.rds.amazonaws.com

El cliente de línea de comandos MySQL es un shell SQL que habilita la interacción con los motores de base de datos. Puede encontrar información útil [aquí](https://dev.mysql.com/doc/refman/8.0/en/mysql.html)

![]()

Copie el comando al portapapeles.

Vuela a la pestaña del navegador de Session Manager que se usó para conectarse a Command Host. Para conectarse a la instancia de Aurora, ejecute el comando que había copiado en el paso anterior.

## Tarea 4: Crer una tabla e insertar registros de consulta

En esta tarea, aprenderá cómo crear una tabla en una base de datos, cargar datos y ejecutar una tarea.

Para mostrar una lista de las bases de datos disponibles, ejecute el siguiente comando.

```sql
SHOW DATABASES;
```
Para cambiar a la base de datos world que creó en la Tarea 1 cuando aprovisionó la instancia de Aurora, ejecute el siguiente comando.

```sql
USE world;
```
Para crear una nueva tabla en la base de datos world, ejecute el siguiente comando.

```sql
CREATE TABLE `country` (
`Code` CHAR(3) NOT NULL DEFAULT '',
`Name` CHAR(52) NOT NULL DEFAULT '',
`Continent` enum('Asia','Europe','North America','Africa','Oceania','Antarctica','South America') NOT NULL DEFAULT 'Asia',
`Region` CHAR(26) NOT NULL DEFAULT '',
`SurfaceArea` FLOAT(10,2) NOT NULL DEFAULT '0.00',
`IndepYear` SMALLINT(6) DEFAULT NULL,
`Population` INT(11) NOT NULL DEFAULT '0',
`LifeExpectancy` FLOAT(3,1) DEFAULT NULL,
`GNP` FLOAT(10,2) DEFAULT NULL,
`GNPOld` FLOAT(10,2) DEFAULT NULL,
`LocalName` CHAR(45) NOT NULL DEFAULT '',
`GovernmentForm` CHAR(45) NOT NULL DEFAULT '',
`Capital` INT(11) DEFAULT NULL,
`Code2` CHAR(2) NOT NULL DEFAULT '',
PRIMARY KEY (`Code`)
);

```

Para insertar nuevos registros en la tabla country que acaba de crear, ejecute los siguientes comandos.

```sql
INSERT INTO `country` VALUES ('GAB','Gabon','Africa','Central Africa',267668.00,1960,1226000,50.1,5493.00,5279.00,'Le Gabon','Republic',902,'GA');

INSERT INTO `country` VALUES ('IRL','Ireland','Europe','British Islands',70273.00,1921,3775100,76.8,75921.00,73132.00,'Ireland/Éire','Republic',1447,'IE');

INSERT INTO `country` VALUES ('THA','Thailand','Asia','Southeast Asia',513115.00,1350,61399000,68.6,116416.00,153907.00,'Prathet Thai','Constitutional Monarchy',3320,'TH');

INSERT INTO `country` VALUES ('CRI','Costa Rica','North America','Central America',51100.00,1821,4023000,75.8,10226.00,9757.00,'Costa Rica','Republic',584,'CR');

INSERT INTO `country` VALUES ('AUS','Australia','Oceania','Australia and New Zealand',7741220.00,1901,18886000,79.8,351182.00,392911.00,'Australia','Constitutional Monarchy, Federation',135,'AU');
```

Para consultar la tabla, ejecute la siguiente statement SELECT.

```sql
SELECT * FROM country WHERE GNP > 35000 and Population > 10000000;
```
La consulta debería arrojar dos registros.

Conclusión

Aprendió a realizar correctamente las siguientes actividades:

* Crear una instancia de Aurora
* Conectarse a una instancia de Amazon Elastic Compute Cloud (Amazon EC2) creada previamente
* Configurar la instancia de Amazon EC2 para conectarse a Aurora
* Consultar la instancia de Aurora


## Recursos adicionales

[Implementaciones Multi-AZ de Amazon RDS]()
[Trabajar con una instancia de base de datos de Amazon RDS en una VPC]()
[¿Qué es Amazon VPC?]()
[Cifrar recursos de Amazon RDS]()
[Seguimiento mejorado]()
[Pares de claves de Amazon EC2]()





