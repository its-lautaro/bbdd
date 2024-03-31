# Clase 4 - Normalización de bases de datos
La normalización es una técnica de verificación de diseño de base de datos, permite conseguir la eliminación de las dependencias entre atributos no deseada.

Consiste en un proceso de analisis de los esquemas de tablas dados basado en sus dependencias funcionales y claves primarias. Se busca minimizar la dependencia de datos y las anomalías de actualización.

Los esquemas de tablas que no cumplan con las condiciones de las *pruebas normales* se descomponen en esquemas mas pequeños que satisagan las pruebas, para llevar a la base de datos a la forma normal.

Los objetivos son controlar la redundancia, evitar perdidas de informacion y mantener la consistencia de los datos.

Es un proceso deseado pero no es estrictamente necesario. Puede afectar los tiempos de acceso a los datos en las ablas en donde se producen cambios. Se puede optar por dejar de lado la normalización y priorizar la performance final de la BD.

## Dependencias funcionales
Una dependencia funcional (DF) representa una restricción entre atributos de una tabla de la base de datos. Dados X, Y atributos, se dice que Y depende funcionalmente de X cuando para un valor dado de X siempre se encuentra el mismo valor para el atributo Y. X e Y pueden representar también un conjunto de atributos.

Ejemplo:
Para la entidad DOCENTE = (_DNI, nombre, direccion, tel, idTitulo)

La dependencia funcional es de DNI para con nombre, direccion, tel e idTitulo

### Tipos de dependencia funcional: Parcial
Una DF X->Y es parcial cuando existe otra DF Z->Y, siendo Z subconjunto de X. Es decir, un atributo B (que no es clave) depende de un subconjunto de A (clave).

Ejemplo:

PEDIDOS = (_idPedido, _idProducto, descProducto, fechaPedido, cantidad)

fechaPedido depende solo de idPedido, y descProducto depende de _idProducto. Esto produce repetición, por ejemplo para cada producto de un determinado pedido se repite la fecha de pedido.

La solución es partir el esquema en dos entidades teniendo en cuenta estas dependencias. Quedarian en este caso una tabala pedido y una tabla producto. 

Cuando esto sucede se presenta repetición de información y puede generaranomalías de inserción, borrado o modificación.

### Tipos de dependencia funcional: Transitiva
Una DF X->Y es transitiva cuando existe un atributo Z tal que X->Z y Z->Y. O sea se da cuando un atributo que no es clave depende de otro que tampoco es clave

Ejemplo:

ALUMNO = (_idAlumno, nombre, direccion, idCarrera, nombreCarrera)

nombreCarrera depende de idCarrera, por lo que la dependencia idAlumno -> nombreCarrera es transitiva

### Tipos de dependencia funcional: de Boyce-Codd
Una DF X->Y es de Boyce-Codd cuando X no es una clave principal o candidate e Y sí es una clave principal o candidata (o parte de ella).

Ejemplo: Se registran materias que cursan los alumnos y el docente a cargo de 
