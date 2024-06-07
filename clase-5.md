# Clase 5 - Algebra Relacional

El Álgebra Relacional (AR) es un lenguaje de consulta procedural diseñado para manejar y manipular datos en sistemas de gestión de bases de datos relacionales. Fue propuesto originalmente por Edgar F. Codd en 1970. Codd introdujo este concepto como parte de su teoría de bases de datos relacionales para proporcionar una base teórica y formal para realizar consultas y manipular datos de manera estructurada y eficiente.

El AR sirve como base teórica para los lenguajes de consulta utilizados en sistemas de bases de datos relacionales, como SQL. Proporciona un conjunto de operaciones que permiten realizar consultas complejas y manipulaciones de datos de manera sistemática y eficiente. Gracias al AR, se pueden definir, ejecutar y optimizar consultas de manera formal, lo que mejora la eficiencia y la precisión en la gestión de datos.

## Operaciones básicas del Álgebra Relacional
Las operaciones del AR trabajan sobre las relaciones (tablas), que son conjuntos de tuplas (filas). Utiliza operaciones de una o dos relaciones de entrada para generar una nueva relación como resultado. Las operaciones fundamentales se dividen en unarias y binarias:

### Operaciones Unarias (Trabajan sobre una sola tabla o relacion)
* Selección: Filtra las tuplas de una relación que cumplen con una condición específica.
* Proyección: Extrae un subconjunto de columnas de una relación.
* Renombre: Cambia el nombre de una relación o de sus atributos.
  
### Operaciones Binarias (Trabajan sobre dos tablas o relaciones)
* Producto Cartesiano: Combina cada tupla de una relación con cada tupla de otra relación.
* Unión: Combina las tuplas de dos relaciones en una sola, eliminando duplicados.
* Diferencia: Devuelve las tuplas que están en una relación pero no en la otra.

## Operaciones adicionales del AR
Las operaciones adicionales no añaden potencia, sino que sólo simplifican las consultan realizadas con las operaciones básicas.

En el Álgebra Relacional (AR), además de las operaciones fundamentales, existen otras operaciones adicionales que amplían la capacidad de manipulación y consulta de datos. Estas operaciones son:

### Intersección

La **Intersección** devuelve las tuplas que son comunes a dos relaciones. Es una operación binaria y se denota como \( R \cap S \), donde \( R \) y \( S \) son las dos relaciones de entrada.

- **Sintaxis**: \( R \cap S \)
- **Ejemplo**: Si \( R \) y \( S \) son dos relaciones de empleados de dos departamentos diferentes, la intersección \( R \cap S \) devolverá los empleados que trabajan en ambos departamentos.

### Producto Theta (θ-Join)

El **Producto Theta** o **θ-Join** es una operación que combina las tuplas de dos relaciones en función de una condición de unión arbitraria (θ). Es una forma generalizada del producto cartesiano donde solo se mantienen las tuplas que cumplen con la condición especificada.

- **Sintaxis**: \( R \bowtie_{\theta} S \)
- **Ejemplo**: \( R \bowtie_{R.A = S.B} S \), donde \( R \) y \( S \) son dos relaciones y \( R.A \) y \( S.B \) son atributos en \( R \) y \( S \), respectivamente. La operación devolverá todas las combinaciones de tuplas de \( R \) y \( S \) donde \( R.A = S.B \).

### Producto Natural (Natural Join)

El **Producto Natural** es una operación especial de unión que combina las tuplas de dos relaciones eliminando los atributos duplicados en la relación resultante. Solo se mantienen las tuplas que tienen el mismo valor en los atributos comunes.

- **Sintaxis**: \( R \bowtie S \)
- **Ejemplo**: Si \( R \) y \( S \) son relaciones con un atributo común \( id \), \( R \bowtie S \) devolverá todas las combinaciones de tuplas de \( R \) y \( S \) donde los valores de \( id \) son iguales, eliminando uno de los atributos duplicados \( id \).

### División

La **División** es una operación que devuelve aquellas tuplas de una relación \( R \) que están asociadas con todas las tuplas de otra relación \( S \). Es útil para consultas del tipo "para todos".

- **Sintaxis**: \( R \div S \)
- **Ejemplo**: Si \( R \) es una relación de "Estudiantes y Cursos" y \( S \) es una relación de "Cursos", la operación \( R \div S \) devolverá todos los estudiantes que están inscritos en todos los cursos listados en \( S \).

### Asignación

La **Asignación** se utiliza para almacenar el resultado de una expresión de consulta en una relación temporal para su uso posterior. Permite dividir una consulta compleja en partes más manejables.

- **Sintaxis**: \( T \leftarrow E \)
- **Ejemplo**: Si \( E \) es una expresión de consulta y \( T \) es una relación temporal, la operación \( T \leftarrow E \) almacena el resultado de \( E \) en \( T \). Esto facilita la reutilización de resultados intermedios en consultas más complejas.

Estas operaciones adicionales del Álgebra Relacional permiten una mayor flexibilidad y potencia en la manipulación y consulta de datos, proporcionando herramientas adicionales para gestionar relaciones complejas y consultas sofisticadas en bases de datos relacionales.
