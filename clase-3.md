# Clase 3 - Diseño lógico y físico
## Diseño lógico
En la etapa de diseño lógico se toma el esquema conceptual realizado en la primer etapa y se modifica para que sea más eficiente su utilización. En esta etapa se definirá el sistema de gestión de base de datos (SGBD).

El primer paso es la simplificación del esquema conceptual, poniendo énfasis en los datos derivados, las relaciones cíclicas y la eliminación de atributos polivalentes, compuestos y jerarquías de generalización.

### Datos derivados
Los datos derivados son información que puede obtenerse de otra forma a partir del mismo esquema. La ventaja de mantener su existencia es que elimina la necesidad de calcular su valor, pero requieren más espacio de almacenamiento y procesamiento adicional para mantener estos datos derivados.

Generalmente para decidir dejarlo o eliminarlo se debe tener en cuenta la cantidad de veces que es usado vs la cantidad de veces que debe ser recalculado. Este tipo de atributos deben tener documentado el cálculo a partir del cual son obtenidos.

Un ejemplo podría ser mantener la edad junto la fecha de nacimiento, la edad podría calcularse solo con la fecha de nacimiento.

### Ciclos de relaciones
En algunos casos, un ciclo puede generar repetición de información. En este caso, se debe identificar las relaciones responsables de la redundancia y analizar si representa una ventaja o una desventaja.

![image](https://github.com/its-lautaro/bbdd/assets/67167458/6c0c0b45-93b6-430b-b538-a4e472b44686)

### Eliminación de atributos polivalentes
Los SGBD no permiten atributos con múltiples valores (vectores) cuya dimensión sea determinada dinámicamente. Todos los atributos de valores múltiples deben tener determinada su dimensión de forma estática.

La solución más simple es asignar un tamaño estático adecuado, pero esto ocasiona que para algunas entidades no sea suficiente, y para otras se desperdicie espacio. Otro enfoque mejor implica **quitar el atributo**, **generar una nueva entidad** con ese atributo y **establecer una relación** con la entidad a la que pertenecía.

### Eliminación de atributos compuestos
Suponiendo un atributo compuesto domicilio que tiene calle, numero, piso y depto. Se podría reemplazar estos atributos por una única cadena de caracteres, sin embargo esto dificulta el procesamiento de la información si se requiriera en el futuro por ejemplo ofrecer promociones a clientes que vivan en determinados barrios.

Tambien se podrian considerar cada uno de los componentes del atributo complejo como atributos simples.

Otra alternativa involucra una vez más la transformación del atributo compuesto en una entidad y la creación de una relación de esta nueva entidad con la entidad anterior.

### Eliminación de jerarquías de generalización
Los modelos lógicos relacionales no permiten representar jerarquías de generalización, se deben representar usando solo entidades e interrelaciones, por lo que la herencia de atributos que antes era implícita ahora debe ser explícita

- La solución más simple es integrar la jerarquía, haciendo que la superentidad también contenga los atributos de todas las subentidades. Esta solucion genera valores nulos de atributos, pero se puede aplicar a cualquier caso.

- Otra solución consiste, de manera inversa, en eliminar a la superentidad y retener a las subentidades. Sin embargo, genera repetición de atributos y operaciones de la superentidad, y crea redundancia. Solo es aplicable en caso de cobertura **total exclusiva**.

- También pueden retenerse todas las entidades, estableciendo explícitamente las interrelaciones entre las superentidades y las subentidades. Proporciona redundancia inherente al representar la relación *ES_UN* en la jerarquía a través de una interrelación explícita.

### Partición de entidades
Esta es una modificación no obligatoria, que se realiza sobre el esquema conceptual a fin de mejorar la performance o la seguridad.

La partición de entidades puede ser horizontal cuando se utiliza para descomponer una entidad en un conjunto de entidades, o vertical cuando se utiliza para descomponer atributos.

- Partición horizontal: Puede decidirse partir la tabla Personas en Clientes y Proveedores ya que si bien tienen la misma información, se realizan procesos diferentes con cada entidad.

- Partición vertical: Se separan los atributos más utilizados y los menos utilizados en dos entidades diferentes.

### Partición de relaciones
Ejemplo: Relación *cursa* entre Alumno y Materia. Podría dividirse en *cursa_pri_sem* y *cursa_seg_sem* para procesarlas más facilmente.

### Fusión de entidades y relaciones
Operación contraria a la partición.

## Diseño Físico
El modelo relacional es un modelo basado en registros ampliamente difundido y tuilizado Es simple, potente y formal. Representa a la BD como una coleccion de archivos (tablas).

Para convertir el esquema lógico a un esquema físico, se debe llevar a cabo la eliminación de identificadores externos, la selección de claves, y la conversión de entidades y relaciones a tablas.

### Eliminación de identificadores externos
Cada una de las entidades que conforman el esquema lógico, ahora debe poseer sus identificadores definidos en forma interna.

En el modelo físico los identificadores se llaman claves. Las claves son un atributo o conjunto de atributos de una tabla que identifica de manera unívoca cada tupla de la misma. El modelo relacional solo acepta identificación interna.

Una tabla tiene como mínimo una clave, pero puede tener más de una. Estas se denominan claves candidatas. Dentro de las candidatas, se debe elegir la primaria (la que efectivamente identifica a las tuplas).

Las claves foráneas, son el atributo o atributos de una tabla que son clave primaria en otra tabla.

En el elección de la clave primaria, por una cuestion de performance, se debe tratar de que sea un identificador simple, del menor tamaño posible. Cuanto mas chica sea la clave, mas eficiente sera el acceso a los elementos de la tabla. La clave elegida se subraya. Por una cuestion de seguridad, deben elegirse campos de dominio autoincremental (no modificables por el usuario, o de modificación minima para evitar el impacto de actualizar otros indices que apunten a este).

Las claves primarias luego se utilizan como indices primarios, y el resto de las claves candidatas, como indices secundarios.

### Integridad Referencial
La integridad referencial es una propiedad deseable de las bases de datos relacionales. Plantea restriccionesentre tablas, y sirve para mantener la consistencia entre las tuplas de dicha tabla.

Ejemplo, si se tiene que en la tabla facturas se guardan numeros de cliente, es decir que cada factura esta relacionada a un cliente, algunas restricciones que garantizan la integridad referencial son:
- No se puede crear una factura para un cliente que no existe
- Todas las facturas deben tener un numero de cliente (no puede ser null)
- Al borrar un cliente, deberian borrarse *en cascada* todas sus facturas

### Conversion de entidades
Para el modelo fisico, todas las entidades deben convertirse en tablas. Se pueden agregar campos para indices autoincrementales.

En las relaciones 1 a 1, no es necesario crear dos tablas, se puede crear a una y agregarle los datos de la otra.
