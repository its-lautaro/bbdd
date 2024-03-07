# Clase 1

# Conceptos Básicos
Una base de datos es cualquier información dispuesta de manera adecuada (de forma que permita el rápido acceso) para su tratamiento por una computadora.

Esta información, que se organiza en archivos que permiten el acceso concurrente, esta interrelacionada con un propósito específico vinculado a la resolución de un problema.

En este sentido, hay dos procesos esenciales a la hora de construir una base de datos. En primer lugar, realizar una abstracción que permita identificar los datos relevantes al dominio del problema (y los que no lo son) (**selección**). En segundo lugar, el esquema de representación que se utilizara para esos datos (**diseño**)

## Sistema de gestión
Toda base de datos es acompañada por un sistema de gestión, llamado DBMS (Database Management System) o SGBD en español. Este sistema es el que permite **crear**, **mantener** y **utilizar** la base de datos. Sus objetivos principales son:
- Evitar las repeticiones (controlar redundancia)
- Garantizar el acceso en todo momento (contrario al antiguo método maestro detalle que no permite el acceso durante una actualización)
- Brindar acceso concurrente
- Realizar un control de acceso (por ejemplo, con usuarios y roles)
- Gestionar copias de seguridad
- Imponer restricciones para asegurar la integridad
- Brindar mecanismos de persistencia ante fallos

Los sistemas de gestión ofrecen por lo general 2 componentes, un **lenguaje de definición de datos** que permite especificar el esquema de la base de datos y obtener un diccionario de datos, y un **lenguaje de manipulación de datos** para realizar la recuperación de la información y su manipulación (alta, baja y modificación).

Este ultimo puede ser procedimental y no procedimental.Los lenguajes de datos procedimentales requieren que se indique qué datos se quieren obtener y como obtenerlos. Un ejemplo de este tipo de lenguaje es SQL.

## Sistema de base de datos vs Sistema de archivos
Los sistemas de base de datos contienen la base de datos junto con la definición de su esquema y sus restricciones, por lo que se dice que son **autodescriptivos**, contrario a los sistemas de archivos donde la descripción de cada archivo se encontraba en la aplicación que lo utilizaba.

Otra diferencia notable de los sistemas de base de datos en comparación a los sistemas de archivos es la **independencia de datos**, que permite realizar modificaciones sobre la estructura de los archivos sin tener que modificar la estructura de los programas que lo utilizan.

Además, los sistemas de base de datos soportan **vistas**, que permite ocultar información sensible o inapropiada para ciertas aplicaciones, revelando solo la información necesaria del esquema.

Finalemente, soportan el **acceso compartido** por múltiples usuarios.

## Actores involucrados

- Database Administrator (DBA): Es quien administra todos los recursos, autoriza accesos y vigila el uso de los recursos. Es responsable por la seguridad y performance de la base de datos.
- Diseñador de BD: Diseña la estructura de la BD, genera las vistas para cada grupo de usuarios y las integra para formar un esquema final integral (esquema conceptual)
- Analista de sistemas: Determina los requerimientos de los usuarios finales
- Programadores: Desarrollan las aplicaciones finales para satisfacer las necesidades de los usuarios, deben conocer las capacidades del SGBD.
- Usuarios: Interactuan con la base de datos mediante aplicaciones o consultas.

# Modelado de datos y diseño de base de datos
Un modelo de datos es una colección de herramientas conceptuales que permite describir los datos, las relaciones entre ellos, la semántica asociada y las restricciones de consistencia. Debe permitir obtener la perspectiva de los *stakeholders* (clientes, usuarios) sobre el problema, visibilizando la necesidad de cada dato que se guarda y como se utilizan. Permite describir y sintetizar la realidad del problema y facilitar la comprensión de los datos de una organización.

Los modelos de datos de **alto nivel** son conceptuales, de estructura flexible y basados en objetos del mundo real (por ejemplo, el modelo *Entidad-Relación*). Se utilizan al inicio del proceso de diseño.

Por otro lado, los modelos de **bajo nivel** tienen una estructura basada en registros de formato fijo y traen un lenguaje asociada para expresar consultas sobre los datos (por ejemplo, el modelo **Relacional**)

El diseño de bases de datos se encuentra dividido en tres etapas:
- Conceptual
- Lógico
- Físico

## Diseño conceptual
El diseño conceptual toma como entrada la **especificación de requerimientos** y genera un **esquema conceptual**. Esta etapa de diseño se encarga de describir el contenido de información de la base de datos, se debe captar y representar las necesidades del usuario definidas en la especificación de requerimientos.

Este esquema conceptual, que es una descripción de alto nivel, es independiente del SGBD que manipula a la base de datos.

## Diseño lógico
El diseño lógico toma como entrada el **esquema conceptual** y genera como resultado un **esquema lógico**. 

En esta etapa se debe tener en cuenta el tiempo de respuesta que debe tener la base de datos (rendimiento), la evolución que tendrá la información de la base de datos (información de carga, velocidad de crecimiento) y la **clase de modelo de datos** que utilizará el SGBD (relacional, jerárquico o de redes).

## Diseño físico
Esta etapa toma como entrada el **esquema lógico** y produce un **esquema físico** de la base de datos.

Describe como se guarda (implantación) la información en el disco (memoria secundaria). Ya no es un esquema gráfico como las etapas anteriores, es código y por lo tanto **debe adaptarse a un SGBD específico** (sintáxis específica para cada producto).

Presenta una descripción detallada de las estructuras de almacenamiento y de los métodos de acceso que se van a utilizar para tener un acceso eficiente a los datos.

Las decisiones tomadas en el diseño físico para mejorar el rendimiento pueden afectar el esquema lógico (por ejemplo, se puede requerir redundancia, lo que ocasiona que se deba modificar la estructura).

## Mecanismos de abstracción

La abstracción es el proceso mental que se aplica al seleccionar características del problema para representarlas, y excluir otras que no son de interés para la solución del problema. Para realizar este proceso de abstracción existen 3 mecanismos que se pueden utilizar.

El primero es la **clasificación**. Este proceso consiste en identificar objetos en un concepto y establecer entre ellos propiedades comunes y relaciones del tipo "es miembro de", por ejemplo: enero es miembro del concepto mes, (licuadora, lavadora, batidora) son miembros de la clase producto.

El segundo es la **agregación**, que define una nueva clase a partir de otras que representan sus partes componentes, utilizando la relación "es parte de", por ejemplo patente y motor son parte de vehículo.
- La agregación puede ser **binaria** o **N-aria** segun la cantidad de clases entre las que haya correspondencia.
- En una agregación binaria, una entidad se agrega a otra entidad individualmente. Esto significa que una instancia de una entidad está relacionada con una única instancia de otra entidad a través de la agregación. Por ejemplo, en un modelo de datos de una biblioteca, un libro (entidad agregada) está asociado con una única biblioteca (entidad principal).
- En una agregación N-aria, una entidad puede agregarse a múltiples instancias de otra entidad. Esto implica que una instancia de una entidad puede estar relacionada con varias instancias de otra entidad a través de la agregación. Por ejemplo, en un modelo de datos de una tienda en línea, un producto (entidad agregada) puede estar asociado con múltiples pedidos (entidad principal).


Por último, la **generalización** define una relación de subconjunto entre los elementos de dos o más clases, utilizando la relación "es un". Por ejemplo, clientes y proveedores son personas.

Estos 3 mecanismos son independientes entre sí, lo que quiere decir que ninguno de ellos puede describirse en función de los otros. Son un mecanismo diferenciado en el proceso de estructuración de la información.

### Relaciones de correspondencia
La **agregación** y la **generalización** generan una *relación de correspondencia* entre las clases que las conforman. En el caso de la agregación se habla de *cardinalidad* y en el caso de la generalización se habla de *cobertura*.

#### Cardinalidad
La cardinalidad se refiere a la cantidad de instancias de una clase que pueden estar asociadas con una instancia de otra clase a través de una relación. Cuando la cardinalidad mínima es mayor a cero, la participación es obligatoria, cuando no, es opcional.

Por ejemplo, en una relación de uno a uno (1 a 1), cada instancia de una clase está asociada con exactamente una instancia de otra clase, y viceversa.

En una relación de uno a muchos (1 a N), una instancia de una clase está asociada con una o más instancias de otra clase, pero cada instancia de la segunda clase está asociada con solo una instancia de la primera clase (N a 1).

En una relación de muchos a muchos (N a N), muchas instancias de una clase están asociadas con muchas instancias de otra clase.
#### Cobertura

Ejemplo: Docentes <- Persona -> Alumnos

En la generalización, la cobertura puede ser

- Total: si cada elemento de la clase genérica corresponde al menos a un elemento de las clases subconjunto (las personas serán alumnos o docentes, alguna de las dos sin excepción)
- Parcial: si existe algún elemento de la clase genérica que no corresponde a ningún elemento de las clases subconjunto. (puede haber personas que no sean alumnos ni docentes)

- Exclusiva: si cada elemento de la clase genérica corresponde a lo sumo a un elemento de las clases subconjunto. (una persona solo puede ser alumno o docente a la vez)
- Superpuesta: si existe algún elemento de la clase genérica que corresponde a los elementos de dos o más clases subconjunto diferentes. (una persona puede ser alumno y docente a la vez)

