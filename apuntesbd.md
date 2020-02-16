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

`SELECT` y `FROM` son las partes principales de una consulta, pero a pesar de que muchas consultan usen `WHERE` no es una cláusula obligatoria. Algo que también es importante destacar es que las sentencias SQL acaban siempre con un punto y coma ( **;** ).

`SELECT`: filtra datos a nivel **columna**. 

`FROM`: indica la **tabla** de la que se van a coger los datos.

`WHERE`: filtra datos a nivel **fila**, devolviendo sólo las que cumplen una o más condiciones.

`ORDER BY`: define el orden ascendente(`ASC`) o descendente(`DESC`) de las **filas** del conjunto de resultados, separando por comas los campos por los que queremos ordenar.  Si no se indica nada **el ordenamiento por defecto es ascendente (ASC)**, y se puede ordenar ascendentemente en unas expresiones, y descendente en otras. La columna por la que se ordenan las tuplas no tiene que aparecer necesariamente en la cláusula SELECT.

Tanto en el SELECT como en el FROM podemos renombrar columnas y filas con la cláusula `AS`. Es muy útil ya que hace que la consulta y su resultado sea más declarativo.

## La instrucción SELECT

En una consulta, `SELECT` puede ir seguido de los siguientes elementos:
- Un **asterisco** `*` indica que en el resultado se añadan todas las columnas de la tabla. Ejemplo:
> SELECT * FROM movie;
- `DISTINCT` se incluye después de SELECT para eliminar filas repetidas, de forma que solo haya valores únicos. En el siguiente ejemplo, si no añadimos DISTINCT el resultado tendría tantas filas como países haya y se repetirían los continentes. Ejemplo(El resultado será una columna con siete filas, una por cada continente.):
> SELECT DISTINCT continent FROM world;

➜❗ **Orden de ejecución** de una consulta SELECT: FROM, WHERE, GROUP BY, HAVING, SELECT.

##  La instrucción WHERE

Su función es eliminar las filas que le pasa el FROM que no hacen cierta una o más condiciones. Las condiciones que filtran los datos de las tuplas(o filas) en el `WHERE` son expresiones lógicas que devuelven TRUE o FALSE (valor booleano), dependiendo de si se cumplen o no las condiciones. Para comparar los datos se utilizan los siguientes operadores:  
- `<`  (estrictamente menor)
- `>`  (estrictamente mayor)
- `=`  (igual) 
- `<=` (menor o igual)
- `>=` (mayor o igual)
- `<>` (distinto)

La sintaxis a seguir es:
```... WHERE <expresion1> <operador> <expresion2>```

Esta estructura es lo que se denomina predicados, porque que permiten especificar una condición.

### Predicados
Es una expresión que se evalúa como TRUE o FALSE. Se pueden usar en `WHERE`y `HAVING`. Existen varios predicados:

- **BETWEEN** : selecciona valores dentro de un rango dado, donde los valores extremos del rango también se incluyen. Los valores pueden ser números, texto o fechas. Ejemplo:
```
SELECT title 
FROM movie
WHERE year BETWEEN 1980 AND 1990;
```

- **IN** : permite especificar múltiples valores. `IN` funciona como un conjunto en el que, por definición, no tiene valores repetidos. Además, es  una abreviatura de **múltiples condiciones OR**. Ejemplo:
```
SELECT title
FROM movie
WHERE year IN('1960', '1962', '1964');
```

- **LIKE** : se utiliza para buscar un patrón/expresión regular específico en una columna. Hay dos elementos que se utilizan a menudo en conjunto con el operador LIKE:

- `%` : representa 0, 1 o varios caracteres.

- `_`: representa un único caracter.

Ejemplo:
```
SELECT actor
FROM movie
WHERE name LIKE 'S%';
```
## La cláusula GROUP BY

`GROUP BY` agrupa las filas que tienen los mismos valores en grupos de filas. En lugar de aplicar las funciones colectivas sobre todas las filas, éstas se pueden agrupar, formando más de un grupo de filas, y entonces aplicar las funciones sobre cada uno de esos grupos. En el resultado habrá una fila por cada uno de los grupos. Ejemplo:
```
SELECT continent, COUNT(name) 
FROM world
GROUP BY continent;
```
## La cláusula HAVING

De igual forma que WHERE permite filtrar **filas**, `HAVING` permite filtrar **grupos**. Esta cláusula permite establecer una condición que se evalúa sobre cada grupo de filas, y aquellos grupos que cumplen la condición, pasan a la cláusula `SELECT`. Ejemplo:
```
SELECT continent, SUM(population)
FROM world
GROUP BY continent
HAVING SUM(population) > 500000000;
```

## La instrucción JOIN

`JOIN` se utiliza para recuperar datos de múltiples tablas en una base de datos.  La combinación básica se hace mediante dos tablas, como este ejemplo:
```
SELECT actor.name 
FROM casting JOIN actor ON (actor.id = casting.actorid)
 WHERE casting.movieid= 11768 ;
```
En esta consulta, la columna *id* de la tabla *actor* y la columna *actorid* de la tabla *casting* son las que hacen posible la unión de las tablas. *casting.actorid* es la clave foránea que hace referencia a *actor.id*, la clave primaria de la tabla *actor*. De este modo, podremos obtener el nombre de todos los actores que actuaron en la película con el identificador(*id*) 11768.

Hay 4 tipos de `JOIN`:
- `INNER JOIN` (`JOIN`):
- `LEFT JOIN`:
- `RIGHT JOIN`:
- `FULL JOIN`:

## El valor nulo NULL

`NULL` representa ausencia de información. El valor 0 de un dato numérico o una cadena(char) vacía no es lo mismo que un valor NULL, por lo tanto debe diferenciarse de cualquier otro valor.

Se diferencian 2 casos:

-Desconocemos el dato.
•Ejemplo: no conocemos el número de teléfono de un estudiante.

–Porque no procede/no es aplicable.
•Ejemplo: en una tabla de empleados, un nulo en el atributo comisión de un empleado representa que el empleado no tiene derecho a comisión y que, por tanto, no procede almacenar su valor.

En el caso de que haya varios `NULL` en una consulta, `DISTINCT` también elimina las filas repetidas. 

En una consulta con un **ORDER BY**, por convención, los **nulos** se consideran **mayores** que cualquier valor.

➜ ❗ Debemos tener en cuenta que no se puede comparar un valor y un NULL con un operador, pues sería decir que un valor es igual a un valor desconocido (*por ejemplo, actor.name = NULL es INCORRECTO*). La forma correcta de usarlo es añadiendo **IS NULL** o **IS NOT NULL**:
```
SELECT [columna1], ..., [columnaN]
FROM tabla
WHERE <condicion_where> IS [NOT] NULL;
```

## Funciones de agregado

Un función de agregado realiza un cálculo sobre un conjunto de valores y devuelve un solo valor. Estas funciones ignoran los valores NULL excepto `COUNT`, y suelen ser usadas con `GROUP BY`.







