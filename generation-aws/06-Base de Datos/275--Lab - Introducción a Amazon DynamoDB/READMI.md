# Laboratorio / Práctica: Introducción a Amazon DynamoDB

## 📋 Escenario
El equipo de operaciones de base de datos creó una base de datos relacional llamada world que contiene tres tablas: city, country y countrylanguage. Según los casos prácticos específicos definidos en el ejercicio de laboratorio, escribirá algunas consultas usando operadores de base de datos y la statement SELECT.


## 🚀 Información general sobre el laboratorio
Amazon DynamoDB es un servicio de base de datos NoSQL ágil y flexible para todas las aplicaciones que necesiten una latencia constante en milisegundos de un solo dígito a cualquier escala. Se trata de una base de datos completamente administrada que soporta modelos de clave-valor y de documentos. Su modelo de datos flexible y su desempeño de confianza lo convierten en un complemento perfecto para aplicaciones móviles, web, de juegos, de tecnología publicitaria y de Internet de las cosas (IoT), entre otras.

En este laboratorio, creará una tabla en DynamoDB para almacenar información sobre una biblioteca de música. Después, consultará la biblioteca de música y luego eliminará la tabla de DynamoDB.

## Temas tratados
En este laboratorio, deberá realizar lo siguiente:

* crear una tabla de Amazon DynamoDB

* ingresar datos en una tabla de Amazon DynamoDB

* consultar una tabla de Amazon DynamoDB

* eliminar una tabla de Amazon DynamoDB



## Tarea 1: Crear una nueva tabla
En esta tarea, creará una nueva tabla en DynamoDB llamada Música. Cada tabla requiere una clave de partición (o clave principal) que se utiliza para dividir datos de partición en los servidores de DynamoDB. Una tabla también puede tener una clave de ordenación. La combinación de una clave de partición y una clave de ordenación identifica de forma única cada elemento de una tabla de DynamoDB.

* En la Consola de administración de AWS, seleccione el menú  Services (Servicios). En Base de datos, elija DynamoDB.

* Elija Create table (Crear tabla).

* En Table name (Nombre de la tabla), ingrese Music

* Para Partition key (Clave de partición), ingrese Artist y deje String (Cadena) seleccionado en la lista desplegable.

* En Sort key - optional (Clave de ordenación [opcional]), ingrese Song y deje seleccionado String (Cadena).

* La tabla utilizará la configuración predeterminada para los índices y la capacidad de aprovisionamiento.

* Desplácese hacia abajo y elija Create alarm (Crear una alarma).

* La tabla se creará en menos de 1 minuto. Espere que la tabla Music (Música) esté Active (Activa) antes de pasar a la siguiente tarea.

 
## Tarea 2: Agregar datos

En esta tarea, agregará datos a la tabla Music (Música). Una tabla es una colección de datos sobre un tema determinado.

Cada tabla contiene varios elementos. Un elemento es un grupo de atributos que se identifica de forma única entre todos los demás elementos. Los elementos de DynamoDB son similares en muchos sentidos a las filas de otros sistemas de base de datos. En DynamoDB, no existen límites con respecto a la cantidad de elementos que puede almacenar en una tabla.

Cada elemento se compone de uno o más atributos. Un atributo es un componente fundamental de los datos que no es necesario seguir dividiendo. Por ejemplo, un elemento en una tabla de Música contiene atributos como Canción y Artista. Los atributos de DynamoDB son similares a las columnas de otros sistemas de bases de datos, pero cada elemento (fila) puede tener atributos diferentes (columnas).

Cuando escribe un elemento en una tabla de DynamoDB, solo se requieren la clave de partición y la clave de ordenación, si se utiliza. Además de estos campos, la tabla no necesita un esquema. Esto significa que se pueden agregar atributos a un elemento que pueden ser diferentes a aquellos de otros elementos.

* Seleccione la tabla Music (Música).

* Elija Actions (Acciones) y, a continuación, elija Create item (Eliminar elemento).

* Para el valor Artist (Artista), ingrese Pink Floyd

* Para el valor Song (Canción), Ingrese Money

* Estos son los únicos atributos que se requieren, pero ahora podrá agregar atributos adicionales.

* Para agregar atributos adicionales, elija Add new attribute (Agregar nuevo atributo).

* En la lista desplegable, seleccione String (Cadena).

Se agregará una nueva fila de atributos.

Para el nuevo atributo, escriba lo siguiente:

  * FIELD: `Album`

  * VALUE: `The Dark Side of the Moon`

gregue otro nuevo atributo mediante el botón Add new attribute (Agregar nuevo atributo).

En la lista desplegable, elija Number (Número).

Se agregará un nuevo atributo de número.

Para el nuevo atributo, escriba lo siguiente:
  * FIELD: Year

  * VALUE: 1973

Seleccione Create item (Crear elemento).

El elemento ahora se agregó a la tabla Music (Música).

De manera similar, para crear un tercer elemento, use los siguientes atributos:

![]()

Observe que este elemento tiene un atributo adicional llamado Genre (Género). Este es un ejemplo de que cada elemento es capaz de tener diferentes atributos sin necesidad de predefinir un esquema de tablas.

Para crear un tercer elemento, use los siguientes atributos.
![]()

Una vez más, este elemento tiene un nuevo atributo, Lengthseconds, que identifica la longitud de la canción. Esto demuestra la flexibilidad de una base de datos NoSQL.

También hay formas más rápidas de cargar datos en DynamoDB, como el uso de AWS Command Line Interface, la carga de datos mediante programación o el uso de una de las herramientas gratuitas disponibles en Internet.

## Tarea 3: Modificar un elemento existente

Ahora observa que hay un error en sus datos. En esta tarea, modificará un elemento existente.

En el panel DynamoDB, en Tables (Tablas), seleccione Explore Items (Explorar elementos).

Seleccione el botón  Music (Música).

Elija Psy.

Cambie el atributo Year (Año) de 2011 a 2012.

Seleccione Save changes (Guardar los cambios).

El elemento está actualizado.

## Tarea 4: Consultar la tabla

Hay dos formas de consultar una tabla de DynamoDB: consulta y análisis.

Una operación de consulta busca elementos basados en la clave primaria y, de forma opcional, en la clave de ordenación. Está completamente indexada, por lo que funciona muy rápido.

Expanda Scan/Query items (Analizar/consultar elementos) y seleccione Query (Consultar).

Ahora se muestran los campos Artist (Artista) (clave de partición) y Song (Canción) (clave de ordenación).

Ingrese los siguientes detalles:
* Artista (clave de partición): Psy

* Canción (clave de ordenación): Gangnam Style

Elija Run (Ejecutar). 

La canción aparece rápidamente en la lista. Es posible que tenga que desplazarse hacia abajo para ver este resultado.

Una consulta es la forma más eficiente de recuperar datos de una tabla de DynamoDB. 

Como alternativa, puede analizar un elemento. Esta opción implica buscar entre todos los elementos de una tabla, por lo que es menos eficiente y puede llevar mucho tiempo para tablas más grandes.

esplácese hacia arriba en la página y seleccione Scan (Analizar).

Expanda Filters (Filtros) e ingrese los siguientes valores:

En Attribute Name (Nombre del atributo), ingrese: Year

* En Type (Tipo), elija Number (Número).

* En Value (Valor), ingrese 1971.

Seleccione Run (Ejecutar).

Solo se muestra la canción que se lanzó en 1971.

## Tarea 5: Eliminar la tabla

En esta tarea, eliminará la tabla Music (Música), lo que también eliminará todos los datos de la tabla.

En el panel DynamoDB, en Tables (Tablas), seleccione Update settings (Actualizar configuración).

Seleccione la tabla Music (Música) si todavía no está seleccionada.

Elija Actions (Acciones) y, a continuación, elija Delete table (Eliminar tabla). 

En el panel de confirmación, ingrese delete y seleccione Delete table (Eliminar tabla).

Se eliminará la tabla.

## Conclusión

Aprendió a realizar correctamente las siguientes tareas:

* Crear una tabla de Amazon DynamoDB

* Ingresar datos en una tabla de Amazon DynamoDB

* Consultar una tabla de Amazon DynamoDB

* Eliminar una tabla de Amazon DynamoDB

Para obtener información acerca de DynamoDB, consulte la [documentación de DynamoDB](https://docs.aws.amazon.com/dynamodb/)

