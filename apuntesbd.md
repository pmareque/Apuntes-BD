# SQL DQL (Data Query Language)

DQL es uno de los sublenguajes SQL utilizado para realizar **consultas** en bases de datos. El ejemplo principal de DQL es la instrucción **SELECT**, la cual nos permite **recuperar datos** almacenados en una base de datos.

Esta es la sintaxis básica de una consulta SELECT:
```
SELECT [ DISTINCT|ALL ] [ * ] / [columna1] AS [expresion], ..., [columnaN]
FROM tabla 
WHERE <condicion_where>
GROUP BY <columna1>,<columna2>, ...
HAVING <condicion_having>
ORDER BY <expr_orderby1> [ ASC / DESC ];
```

`SELECT`, `FROM` y `WHERE` son las partes principales de cualquier consulta. Algo que también es importante destacar es que las sentencias SQL acaban siempre con un punto y coma ( **;** ).


`SELECT`: filtra datos a nivel **columna**. 

`FROM`: indica la **tabla** de la que se van a coger los datos.

`WHERE`: filtra datos a nivel **fila**, devolviendo sólo las que cumplen una o más condiciones.

`ORDER BY`: define el orden ascendente(`ASC`) o descendente(`DESC`) de las filas del conjunto de resultados, separando por comas los campos por los que queremos ordenar.  Si no se indica nada **el ordenamiento por defecto es ascendente (ASC)**, y se puede ordenar ascendentemente en unas expresiones, y descendente en otras. La columna por la que se ordenan las tuplas no tiene que aparecer necesariamente en la cláusula SELECT.

Tanto en el SELECT como en el FROM podemos renombrar columnas y filas con la cláusula **AS**. Es muy útil ya que hace que la consulta y su resultado sea más declarativo.

## La sentencia SELECT

En una consulta, `SELECT` puede ir seguido de los siguientes elementos:
- Un **asterisco** `*` indica que en el resultado se añadan todas las columnas de la tabla.
> SELECT * FROM movie;
- `DISTINCT` se incluye después de SELECT para eliminar filas repetidas, de forma que solo haya valores únicos. En el siguiente ejemplo, si no añadimos el DISTINCT el resultado tendría tantas filas como países haya y se repetirían los continentes.
> SELECT DISTINCT continent FROM world;

➜**Orden de ejecución** de una consulta SELECT: FROM, WHERE, GROUP BY, HAVING, SELECT.

##  La cláusula WHERE

Su función es eliminar las filas que le pasa el FROM que no hacen cierta una o más condiciones. Las condiciones que filtran los datos de las tuplas(o filas) en el `WHERE` son expresiones lógicas que devuelven TRUE o FALSE (valor booleano), dependiendo de si se cumplen o no las condiciones. Para comparar los datos se utilizan los siguientes operadores:  
- `<`
- `>`
- `=`
- `<=`
- `=>`

La sintaxis a seguir es:
```... WHERE <expresion1> <operador> <expresion2>```

Esta estructura es lo que se denomina predicados, porque que permiten especificar una condición.

### Predicados
Es una expresión que se evalúa como TRUE o FALSE. Se pueden usar en `WHERE`y `HAVING`. Existen varios predicados:

- **BETWEEN**

- **IN**

- **LIKE**

- **IS [NOT] NULL**

## La cláusula HAVING

De igual forma que WHERE permite filtrar *filas*, `HAVING` permite filtrar **grupos**. Esta cláusula permite establecer una condición que se evalúa sobre cada grupo de filas, y aquellos grupos que cumplen la condición, pasan a la cláusula `SELECT`.

## El valor nulo NULL

Un `NULL` representa ausencia de información. El valor 0 de un dato numérico o una cadena(char) vacía no es lo mismo que un valor NULL, por lo tanto debe diferenciarse de cualquier otro valor.

Se diferencian 2 casos:

-Desconocemos el dato.
•Ejemplo: no conocemos el número de teléfono de un estudiante.

–Porque no procede/no es aplicable.
•Ejemplo: en una tabla de empleados, un nulo en el atributo comisión de un empleado representa que el empleado no tiene derecho a comisión y que, por tanto, no procede almacenar su valor.

En el caso de que haya varios valores `NULL` en una consulta, `DISTINCT` también elimina las filas repetidas. insertar CAPTURA NULOS Y DISTINCT

En una consulta con un ORDER BY, por convención, los nulos se consideran mayores que cualquier valor.*insertar Captura NULOS Y ORDER BY*








