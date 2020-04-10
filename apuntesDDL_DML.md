- [SQL DDL (Data Definition Language)](#SQL-DDL-Data-Definition-Language)
  - [La sentencia CREATE](#la-sentencia-create)
  - [La sentencia DROP](#la-sentencia-drop)
  - [La sentencia ALTER](#la-sentencia-alter)
  - [CONSTRAINT o restricciones en SQL](#CONSTRAINT-o-restricciones-en-SQL)
- [SQL DML (Data Manipulation Language)](#SQL-DML-Data-Manipulation-Language)
  - [La sentencia INSERT](#La-sentencia-INSERT)
  - [La sentencia UPDATE](#La-sentencia-UPDATE)
  - [La sentencia DELETE](#La-sentencia-DELETE)
  
# SQL DDL (Data Definition Language)

**DDL** es el sublenguaje SQL que actúa sobre los **objetos** de la base de datos, sobre su **estructura**.

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
**Ejemplo con CREATE:** 
```SQL
CREATE DATABASE instituto;
CREATE TABLE alumnos(
	DNI 	     CHAR(9)   PRIMARY KEY,
	nombre       CHAR(20)  NOT NULL,
	apellidos    CHAR(40)  NOT NULL,
	fecha_nac    DATE      NOT NULL,
	tlf          INTEGER,
	notaMedia    DECIMAL    NOT NULL
);
```

## La sentencia DROP

`DROP` es una sentencia que sirve para eliminar la estructura de una tabla.
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
**Ejemplo con DROP TABLE:** 

```SQL
DROP TABLE alumnos;
DROP SCHEMA instituto;
```

## La sentencia ALTER

`ALTER` se utiliza tanto para modificar columnas como para eliminarlas. Los comandos que permiten estas funciones son **ADD** y **DROP**.

-`ADD` puede añadir nuevos atributos o también nuevas restricciones a la tabla.
-`DROP` puede eliminar atributos o restricciones de la tabla.

✔️Sintaxis: 
```console
ALTER TABLE <nombre-de-la-tabla>
    ADD [COLUMN] <atributo1> <dominio1> [NOT NULL] [DEFAULT(x)]
    DROP [COLUMN] <atributo1> [ CASCADE | RESTRICT]
    ADD [CONSTRAINT <restriccion>] ...
    DROP [CONSTRAINT <restriccion>] ...;
```

**Ejemplo con ALTER TABLE:** 
```SQL
ALTER TABLE instituto
	DROP tlf,
	ADD  curso CHAR(5) NOT NULL;
```


## CONSTRAINT o restricciones en SQL

Los **CONSTRAINT** son restricciones usadas para limitar el tipo de dato que puede ingresarse en una tabla. Pueden especificarse cuando la tabla se crea por primera vez a través de la instrucción `CREATE TABLE`, o después de crear la tabla mediante la instrucción `ALTER TABLE`. Existen varios tipos:

- `PRIMARY KEY`: indica el/los atributo/s que forma/n la clave primaria.
- `FOREIGN KEY`: indica los atributos que forman la clave foránea. Para indicar la tabla de la que depende debemos usar **REFERENCES**.
	- **CASCADE**: elimina los "hijos" de una tabla, es decir, borra los campos de la tabla dependiente cuando se borra el campo de 	la tabla principal.
	- **ON DELETE**: especifica cómo debe actuar el SGBD frente a eliminaciones de las tablas referenciadas en la restricción.
	- **ON UPDATE**: especifica cómo debe actuar el SGBD frente a modificaciones de las tablas referenciadas en la restricción.
	- **SET DEFAULT**: los datos tendrán un valor por defecto si los originales se han eliminado/modificado.
	- **SET NULL**: especifica los datos modificados como NULL.
- `UNIQUE`: evita duplicidad errónea de filas.
- `NULL`: asegura que los valores almacenados en una columna no son NULOS.
- `CHECK`: comprueba si se cumple una condición específica entre atributos.

**Ejemplos usando constraints en una sentencia CREATE TABLE y ALTER TABLE:**
```SQL
CREATE TABLE participa (
    DNI                 CHAR(9),
    codigo_proxecto     INTEGER,
    data_inicio         DATE        NOT NULL,
    data_cese           DATE,
    dedicacion          INTEGER     NOT NULL,
    PRIMARY KEY(DNI, codigo_proxecto),
    CONSTRAINT Check_Dates
        CHECK (data_inicio < data_cese),
    CONSTRAINT FK_participa_profesor
        FOREIGN KEY(DNI)
        REFERENCES profesor(DNI)
        ON DELETE NO ACTION 
        ON UPDATE CASCADE,
    CONSTRAINT FK_proxecto_participa    
        FOREIGN KEY (codigo_proxecto)
        REFERENCES proxecto(codigo_proxecto)
        ON DELETE NO ACTION 
        ON UPDATE CASCADE
);

ALTER TABLE instituto
	CONSTRAINT DNI_valorunico
		UNIQUE (DNI)
;
```


# SQL DML (Data Manipulation Language)

**DML** es el sublenguaje SQL que actúa sobre los **datos** de la base de datos. Como su nombre indica, este lenguaje se usa para manipular datos, lo que permite al usuario introducir(`INSERT`), modificar(`UPDATE`) o eliminar(`DELETE`) todo tipo de datos.

## La sentencia INSERT

`INSERT` permite insertar valores en formato fila en una tabla. Su sintaxis básica es la siguiente:
```SQL
INSERT INTO table_name (list_of_columns)
VALUES (list_of_values);
```
Una sintaxis más visual para entender cómo funciona INSERT podría ser:
```SQL
INSERT INTO <table_name> (
	column1, 
	column2, 
	..., 
	columnN
)
VALUES (
value1,
value2,
...
valueN);
```
## La sentencia UPDATE

`UPDATE` permite modificar los valores de uno o más registros de una tabla. Su sintaxis es la siguiente (la condición WHERE es opcional):

```SQL
UPDATE <table_name>
SET 
    column_name = value [, column_name = value]...
[ WHERE condition ];
```

Una sintaxis más visual para entender cómo funciona UPDATE podría ser:
```SQL
UPDATE <table_name>
SET
   column1_name = value1,
   column2_name = value2,
   ...
   columnN_name = valueN;
```

## La sentencia DELETE

`DELETE` permite eliminar filas de una tabla. Su sintaxis es la siguiente(la condición WHERE es opcional):
```SQL
DELETE FROM table_name [ WHERE condition ];
```
