# SQL DQL (Data Query Language)

DQL es uno de los sublenguajes SQL utilizado para realizar **consultas** en bases de datos. El ejemplo principal de DQL es la instrucción **SELECT**, la cual nos permite **recuperar datos** almacenados de una base de datos.

Esta es la sintaxis básica de una consulta SELECT:
```
SELECT [ DISTINCT ] [ * ] / [nombre_columna] AS [expresion]
FROM nombre_tabla 
WHERE condicion
ORDER BY nombre_columna [ ASC / DESC ]
```
`SELECT`, `FROM` y `WHERE` son las partes principales de cualquier consulta. 

`SELECT`: filtra datos a nivel columna. 

`FROM`: indica la tabla de la que se van a coger los datos.

`WHERE`: filtra datos a nivel fila, devolviendo sólo las que cumplen una o más condiciones.

`ORDER BY`: define el orden de las filas del conjunto de resultados, separando por comas los campos por los que queremos ordenar.

Tanto en el SELECT como en el FROM podemos renombrar columnas y filas (respectivamente) con la cláusula **AS**. Es muy útil ya que hace que la consulta y su resultado sea más declarativo y por lo tanto más sencillo de entender.

###  La cláusula WHERE

Las condiciones que filtran los datos de las tuplas(o filas) en el `WHERE` son expresiones lógicas que devuelven TRUE o FALSE, dependiendo de si se cumplen o no las condiciones. Para comparar los datos se utilizan los siguientes operadores:  
