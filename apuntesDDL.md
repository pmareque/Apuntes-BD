- [SQL DDL (Data Definition Language)](#SQL-DQL-Data-Definition-Language)
  - [La sentencia CREATE](#la-sentencia-create)
  - [La sentencia DROP](#la-sentencia-drop)
  - [La sentencia ALTER](#la-sentencia-alter)
  - [CONSTRAINT o restricciones en SQL](#CONSTRAINT-o-restricciones-en-SQL)
  
# SQL DDL (Data Definition Language)

**DQL** es el sublenguaje SQL que actúa sobre los **objetos** de la base de datos.

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

`CREATE` sirve para crear bases de datos enteras o tablas concretas de una base de datos.

✔️Sintaxis: 
```console
CREATE DATABASE <nombre-BD>;

CREATE TABLE <nombre-tabla> (
	<atributo1> <dominio1> [NOT NULL] [DEFAULT(x)] ,   
        ...
	<atributoN> <dominioN> [NOT NULL] [DEFAULT(x)],
	[restriction1],
	...
	[restrictionN]
);
``` 
**Ejemplos con CREATE TABLE:** <<<<<<<<<<<<<<<<<<<<<<<<
```SQL
CREATE TABLE Alumnos(
	numeroLista INTEGER PRIMARY KEY,
	nombre CHAR(20),
	apellidos CHAR(40),
	tlf INTEGER,
	notaMedia DECIMAL
);
```

## La sentencia DROP

`DROP` es una sentencia que no sirve sólo para eliminar datos y restricciones de una tabla (o base de datos), sino que también elimina la estructura de dicha tabla. Podríamos decir que no posee ningún tipo de vuelta atrás.

✔️Sintaxis:
```console
DROP TABLE                                     
    [IF EXISTS] <nombre-de-la-tabla>
    [CASCADE | RESTRICT];   
```

```console
DROP SCHEMA
    [IF EXISTS] <nombre-de-la-bd>
    [ CASCADE | RESTRICT ];                 
 ```
**Ejemplos con DROP TABLE:** <<<<<<<<<<<<

## La sentencia ALTER

`ALTER` se utiliza tanto para modificar columnas como para eliminarlas. Los comandos que permiten estas funciones son **ADD** y **DROP**.

-`ADD` <<<<<<<<<<<<
-`DROP` <<<<<<<<<<<<

✔️Sintaxis: 
```console
ALTER TABLE <nombre-de-la-tabla>
    ADD [COLUMN] <atributo1> <dominio1> [NOT NULL] [DEFAULT(x)]
    DROP [COLUMN] <atributo1> [ CASCADE | RESTRICT]
    ADD [CONSTRAINT <restriccion>] ...
    DROP [CONSTRAINT <restriccion>] ...;
```

**Ejemplos con ALTER TABLE:** <<<<<<<<<<<<


## CONSTRAINT o restricciones en SQL

Las **CONSTRAINT** son restricciones usadas para limitar el tipo de dato que puede ingresarse en una tabla. Pueden especificarse cuando la tabla se crea por primera vez a través de la instrucción `CREATE TABLE`, o después de crear la tabla mediante la instrucción `ALTER TABLE`. Existen varios tipos:

- `PRIMARY KEY`: indica el/los atributo/s que forma/n la clave primaria.
- `FOREIGN KEY`: indica los atributos que forma/n la clave foránea. Para indicar la tabla de la que depende debemos usar **REFERENCES**.
	- **CASCADE**: elimina los "hijos" de una tabla, es decir, borra los campos de la tabla dependiente cuando se borra el campo de 	la tabla principal.
	- **ON DELETE**: <<<<<<<<<<<<
	- **ON UPDATE**: <<<<<<<<<<<<
	- **SET DEFAULT**: los datos tendrán un valor por defecto si los originales se han eliminado/modificado.
	- **SET NULL**: especifica los datos modificados como NULL.
- `UNIQUE`: evita duplicidad errónea de filas.
- `NULL`: asegura que los valores almacenados en una columna no son NULOS.
- `CHECK` <<<<<<<<<<<<

**Ejemplo usando CONSTRAINTS en una sentencia ALTER TABLE:** <<<<<<<<<<<<


