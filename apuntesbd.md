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

`WHERE`: filtra datos a nivel fila.

`FROM`: indica la tabla de la que se van a coger los datos.

