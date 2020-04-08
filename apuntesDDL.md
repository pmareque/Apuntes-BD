- [SQL DDL (Data Definition Language)](#SQL-DQL-Data-Definition-Language)
  - [La sentencia CREATE](#la-sentencia-create)
  - [La sentencia DROP](#la-sentencia-drop)
  - [La sentencia ALTER](#la-sentencia-alter)
  
# SQL DDL (Data Definition Language)

DQL es la parte del lenguaje SQL que actúa sobre los **objetos** de la base de datos.

### ❕❕

A pesar de que existen mucho más tipos de datos SQL, en estos apuntes se limitarán a los siguientes:

-**Numéricos**:
  - INTEGER 
  - DECIMAL 
  - FLOAT
  - REAL

-**Texto**:
  - CHAR 	
  - VARCHAR 	
  - STRING

-**Booleanos**:
  - TRUE	
  - FALSE	
  - NULL
  
-**Fechas**:
  - DATE (DD-MM-YYYY)
  - TIME (H, MIN, zona horaria)
  - TIMESTAMP (DATE+TIME)

-**Otros**:
  - CIDR (Classless Inter-Domain Routing, identificar direcciones IP con el formato x.x.x.x/x Ej 192.168.0.1/24)
  - MONEY (identificar cantidades monetarias)
  - UUID (Universally Unique IDentifier)
  - JSON (JavaScript Object Notation)
  - XML (almacenar fragmentos y documentos XML en una base de datos)

## La sentencia CREATE

Sintaxis ✔️: 
```console
CREATE TABLE <nombre-de-tabla> (
	<atributo1> <dominio1> [NOT NULL] [DEFAULT(x)] ,   
        ...
	<atributoN> <dominioN> [NOT NULL] [DEFAULT(x)],
	[restriccion1],
	...
	[restriccionN]
);
```
/*explicar:  
CONSTRAINT= Puede colocar restricciones para limitar el tipo de dato que puede ingresarse en una tabla. Dichas restricciones pueden especificarse cuando la tabla se crea por primera vez a través de la instrucción CREATE TABLE, o luego de crear la tabla a través de la instrucción ALTER TABLE-> clave primaria(evitar insertar valores nulos en determinados atributos de la tabla), unicidad(evitar duplicidad errónea de filas), comprobación(CHECK).*/

*explicar: 
 PRIMARY KEY indica el/los atributo/s que forma/n la clave primaria.
 FOREIGN KEY indica los atributos que forma/n la clave foránea.
 NOT NULL(asegura que los valores almacenados en una columna no son NULOS.), DEFAULT(x)*/

/*ejemplos con CREATE TABLE*/

/*Caso CREATE DOMAIN = útil para crear un nuevo tipo de dato*/
## La sentencia DROP

Sintaxis ✔️:
```console
DROP TABLE                                     
    [IF EXISTS] <nombre-de-la-tabla>
    [CASCADE | RESTRICT];   
```
/*explicar >> CASCADE -> elimina los hijos. RESTRICT -> para en esta tabla*/ /*todo lo que va entre [] es un dato opcional*/

/*ejemplos con DROP TABLE*/

```console
DROP SCHEMA
    [IF EXISTS] <nombre-de-la-bd>
    [ CASCADE | RESTRICT ];                 
 ```
/*CASCADE->borra aunque esté llena. RESTRICT-> protege si la BD no está vacía*/

## La sentencia ALTER

Sintaxis ✔️: 
```console
ALTER TABLE <nombre-de-la-tabla>
    ADD [COLUMN] <atributo1> <dominio1> [NOT NULL] [DEFAULT(x)]
    DROP [COLUMN] <atributo1> [ CASCADE | RESTRICT]
    ADD [CONSTRAINT <restriccion>] ...
    DROP [CONSTRAINT <restriccion>] ...;
```
/*Explicar CASCADE, RESTRICT, NOT NULL(asegura que los valores almacenados en una columna no son NULOS.)*/

/*ejemplos con ALTER TABLE*/

/*emojis útiles ✔️ ✅*/
