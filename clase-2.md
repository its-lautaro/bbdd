# Clase 2 - Modelo Conceptual
El diseño conceptual es una etapa crucial del diseño de bases de datos, requiere de la participación de los usuarios y forma parte luego de la documentación de la BD. Este modelo conceptual se sigue utilizando y puede sufrir ampliaciones o modificaciones a lo largo del ciclo de vida de la BD.

Un modelo conceptual tiene 6 cualidades esenciales:
- Debe ser expresivo, permitir una representación amplia de la realidad
- Debe ser simple de comprender (se debe equilibrar la expresividad con la complejidad)
- Cada concepto que representa debe ser único y no debe poder ser definido mediante otros conceptos (minimalidad)
- Cada concepto debe tener una sola interpretación (formalidad)

También es importante considerar que el éxito de un modelo conceptual depende del éxito de su representación gráfica, que debería abarcar todos los conceptos y sus símbolos deberían ser bien distinguibles.

## Modelo Entidad-Relación (ER)

El modelo Entidad-Relación es la herramienta más utilizada para construir el modelo conceptual de una bd. Cuenta de 3 elementos básicos:
- Entidades: Representan clases de objetos del mundo real con identidad. Se representan con rectángulos.
- Interrelaciones: Representa agregaciones entre entidades. Se representan con un rombo. Además, se debe indicar la cardinalidad (1 a 1, 1 a N, 0 a N).

Ejemplo:
[ ALUMNO ]  <CURSA> [ MATERIA ]

<VIVE_EN>

[ LOCALIDAD ]

- Atributos: Los atributos son las propiedades básicas de entidades o interrelaciones. Es el equivalente a los campos de un registro. En cada atributo se debe indicar su cardinalidad mínima y máxima, su dominio (valores que puede tomar). Ejemplo: Alumno -> nroLegajo, nombre, dni, etc. Se representa como un pin que sale de la entidad.

### Jerarquías de Generalización
Es una técnica que permite extraer las características generales de cada entidad e implementarlas en una entidad más general que las incluya. Cada atributo, interrelación o generalización definido para la entidad genérica será heredado por todas las entidades del subconjunto. Cuando se generaliza se debe también especificar la cobertura de la generalización (que puede ser total o parcial, y exclusiva o superpuesta).

Ejemplo: se identifica que Docente y Alumno comparten atributos en común, entonces se crea la *superentidad* Persona que define estos atributos, y en cada *subentidad* se definen los atributos específicos de cada una.

### Atributos compuestos
Los atributos compuestos surgen de la agrupación de atributos que tienen una afinidad común y su objetivo es mejorar la legibilidad de las entidades.

Ejemplo: los 4 atributos simples calle, nro, piso, depto, pueden agruparse en un atributo compuesto llamado *direccion* que contenga esos registros.

Los atributos compuestos también pueden definir cardinalidad.

### Identificadores
Los identificadores son atributos o conjunto de atributos que permiten identificiar a cada entidad de manera unívoca dentro del conjunto de entidades. Estos atributos no pueden tener valores nulos.

Los identificadores ademas pueden ser internos o externos, y simples o compuestos

- Internos: son identificadores de la entidad.
- Externos: son identificadores externos a la entidad
- Simples: son identificadores por sí mismos.
- Compuestos: requieren de otro atributo para identificar univocamente a la entidad.

El identificador de una entidad genérica es heredado por las entidades del subconjunto.

Según el tipo de sus identificadores, una entidad puede clasificarse como
- Entidad fuerte: posee identificadores internos
- Entidad débil: posee solo identificadores externos

**Cada entidad debe ser provista de almenos un identificador**

## Conexión con tema 1 (abstracciones)
Recordando que las abstracciones deben proporcionar mecanismos de clasificación, agregación y generalización, analizamos como el modelo entidad relación las proporciona.

### Clasificación
- Las entidades son clases de objetos del mundo real con propiedades comunes.
- Las interrelaciones son clases de objetos que relacionan dos o más entidades.
- Los atributos son clases de valores que representan propiedades de entidades o interrelaciones.
### Agregación
- Las entidades son agregaciones de atributos
- Los interrelaciones son agregaciones de entidades
- Los atributos compuestos son agregaciones de atributos simples
### Generalización
La generalización se puede conseguir con la herencia de entidades y atributos

### Cualidades del modelo ER
- El modelo ER es muy expresivo, por lo que es potente para describir la realidad
- Es simple, todo puede llevarse a interrelaciones binarias
- Los diagramas estan definidos formalmente y son fáciles de leer
- Es gráficamente completo
- Los problemas pueden resolverse de distintas formas sin afectar la minimalidad

**Sin embargo**
- Su expresividad atenta contra la simplicidad y la minimalidad
- Los conceptos de cardinalidad e identificación pueden ser complejos

En resumen, el modelo ER es un buen termino medio entre poder de expresión, simplicidad y minimalidad.

## Metodología para el diseño conceptual
Inicialmente se comienza con una versión preliminar del esquema y se efectúa una serie de transformaciones de esquemas hasta arribar a la versión definitiva.

Estas transformaciones se pueden clasificar en **ascendentes** (si introducen conceptos y propiedades nuevos, que no aparecen en versiones anteriores del esquema) o **descendentes** (si son refinamientos del esquema inicial para producir una descripción más detallada)

### Primitivas ascendentes
Se usan en el diseño de un esquema siempre que se descubre un nuevo concepto con propiedades específicas que no aparecía en el esquema anterior, y se amplía el esquema agregando nuevas entidades, interrelaciones, atributos o generalizaciones.

### Primitivas descendentes
Estas tienen una estructura simple: el esquema inicial es un concepto único y el resultante se compone de un conjunto pequeño de conceptos.

Los nombres se refinan dando lugar a nuevos nombres que describen el concepto original en un nivel de abstracción más bajo.

Las conexiones lógicas se heredan por un solo concepto del esquema resultante.

#### Ejemplos
1. Generar entidades relacionadas a partir de una entidad. Por ejemplo a partir de la entidad vehículo y todos sus atributos, podrían separarse sus especificaciones técnicas en otra entidad por separado.
2. Crear generalizaciones a partir de una entidad. Por ejemplo, pasar de tener solo Personas a tener Personas, Empleados y Gerentes que comparten la información de Persona y agregan información específica.
3. Crear entidades no relacionadas a partir de una entidad. Por ejemplo a partir de la entidad personal, crear las entidades Contratados y Relacion Dep., que son dos identidades independientes y no existe una relación de jerarquía entre ellas.
4. Crear interrelaciones paralelas a partir de una interrelacion. Ejemplo, el esquema inicial guarda información de donde vive una persona, pero luego se dan cuenta de que es necesario guardar en donde nació. Ambos atributos interrelacionan a una Persona con Localidades.
5. Pasar de una interrelacion a entidades con interrelaciones. Ejemplo pasar de un Empleado que trabaja para un Sector, a un Empleado que trabaja para un Gerente que administra un Sector.
6. Refinar los atributos creando atributos nuevos o agrupandolos en atributos compuestos. Ejemplo, un pedido con fecha podria pasar a ser un pedido con dia, mes y año, o incluir esos atributos en un atributo compuesto llamado fecha.

### Diseño de vistas
Una vista es la percepción de los requerimientos de datos de una aplicación o un usuario. El objetivo del diseño de vistas es crear un esquema conceptual partiendo de una descripción informal de los requerimientos del usuario. Esta técnica se puede aplicar si no tenemos un documento de especificación de requerimientos.

Este tipo de diseño requiere realizar un análisis de los requerimientos para captar el significado de los objetos de interés, su agrupación, propiedades, etc. Para captar los requerimientos existen diversas fuentes, como la descripción en lenguaje natural, los formularios, el software preexistente, reglamentos o leyes, entre otros.

### Perfeccionamiento del esquema conceptual
Una vez que se tiene el esquema conceptual, se debe validar. Para esto se examina y evalúa el sistema según las cualidades deseadas, que son

- **Compleción**: Representa todas las caracteristicas del dominio de la aplicación? (Es completo?). Verificar que el esquema tenga todos los requerimientos, y que no haya cosas que no estan en los requerimientos.
- **Corrección**: Usa con propiedad los conceptos de Entidad-Interrelacion? Corrección sintáctica es cuando los conceptos se usan correctamente, y corrección semántica es cuando se usan de acuerdo a su definición. Algunos errores frecuentes son usar atributos en lugar de entidades, olvidar una generalización, olvidar la propiedad de herencia, usar entidades en lugar de interrelaciones, olvidar un identificador de una entidad y omitir cardinalidad.
- **Minimalidad**: Aparece cada aspecto de los requerimientos una sola vez? Un esquema es minimo si no se puede borrar un concepto sin perder información.
- **Expresividad**: Se entiende con facilidad? Un esquema expresivo no requiere de explicaciones adicionales y representa de manera natural los requerimientos
- **Legibilidad**: Sobre criterios estéticos. PAra el diagrama utilizar hojas cuadriculadas, realizar cuadros y rombos del mismo tamaño y usando estructuras simétricas. Minimizar el numero de cruces, realizar solo conexiones horizontales o verticales. Ubicar las entidades padre sobre las entidades hijo para indicar generalizaciones.
- **Autoexplicación**: Un esquema autoexplicativo no necesita de formalismos ni aclaraciones.
- **Extensibilidad**: Un esquema extensible se adapta facilmente a requerimientos cambiantes, para esto debe poder descomponerse en partes a fin de aplicar los cambios en cada parte.
