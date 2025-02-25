<h1 align="center">Bases de Datos SQL</h1>
SQL, que significa "Structured Query Language" (Lenguaje de Consulta Estructurado), es un lenguaje de programación utilizado para gestionar y manipular bases de datos relacionales.
Es el estándar de facto para interectuar con sistemas de gestión de bases de datos (DBMS) como MySQL, PostgreSQL, Oracle y SQL server.
Desde su creación, SQL ha sido fundamental en el desarrollo de aplicaciones que requieren almacenamiento y recuperación eficiente de datos.


## Origenes de SQL
La historia de SQL comienza en la década de 1970 en los laboratorios de IBM. Edgar F. Codd, un cientifico de la computación británico, propuso el modelo relacional para bases de dados en su documento de 1970
titulado "A relational Model of Data for Large Shared Data Banks". Este modelo revolucionó la 
manera en que los datos podían ser organizados y 

## Tipos de datos en SQL

### ¿Qué son los tipos de datos?
Los tipos de datos normalmente los utilizamos en columnas, variables y parametros y estos nos funcionan para especificar cual es la clase de información que vamos a insertar en los atributos del objeto que estamos creando.
Por ejemplo cuál es el tipo de contenido que puede tener esa columna en la tabla que estamos creando o el parametro o una variable.

#### Datos númericos

##### INTEGER
    INT (capacidad de 4 bytes)
    SMALLINT (capacidad de 2 bytes)
    BIGINIT (capacidad de 8 bytes)

    DECIMAL (valor1, valor2)

#### Datos de Texto

##### CHAR
    CHAR(longitud del texto que se desea almacenar)

##### VARCHAR
    VARCHAR(longitud del texto que se desea almacenar)

##### TEXT 
    No requiere una limitación de la longitud

#### Datos de fecha

##### TIME
    Para especificar la hora

##### DATE
Para especificar la fecha

##### DATETIME 
Para especificar la fecha y la hora


### Crear base de datos
```sql
CREATE DATABASE NOMBREDB
```
### Crear tablas

```sql
CREATE TABLE STUDENTS (
    STUDENTID INT PRIMARY KEY,
    FIRSTNAME VARCHAR(50),
    LASTNAME VARCHAR(50),
    AGE INT,
    EMAIL VARCHAR(100),
    LOADDATE TIMESTAMP DEFAULT CURRENT_TIMETAMP,
    UPDATEDATE TIMESTAMP DEFAULT CURRENT_TIMETAMP,
    FOREIGN (INSTRUCTORID) REFERENCES INSTRUCTORS(INTRUCTORID)
);
```

```sql
CREATE TABLE INSTRUCTORS (
    STUDENTID INT PRIMARY KEY,
    FIRSTNAME VARCHAR(50),
    LASTNAME VARCHAR(50),
    AGE INT,
    EMAIL VARCHAR(100),
    LOADDATE TIMESTAMP DEFAULT CURRENT_TIMETAMP,
    UPDATEDATE TIMESTAMP DEFAULT CURRENT_TIMETAMP,
);
```

### INSERT
La instrucción INSERT en SQL se utiliza para agregar nuevosdatos a una tabla. Funciona como si insertaras un nuevo registro en una hija de cálculo.

Sintaxis básica:  

```sql
INSERT INTO nombre_tabla (columna1, columna2, ...)
VALUES (valor1, valor2, ...)

```

Explicación de la sintaxis:   
INSERT INTO: Indica que se trata de una instrucción INSERT.  
nombre_tabla: Especifica el nombre de la tabla en la que deseas insertar los datos.   
(columna1, columna2, ...): Define las columnas en las que se insertarán los datos. Puedes incluir todas las columnas de la tabla o solo algunas específicas.   
VALUES: Indica el inicio de la lista de valores que se insertarán.
(valor1, valor2, ...): Son los valores que se insertarán en cada una de las columnas correspondientes. El orden de los valores debe coincidir con el orden de las columnas especificado anteriormente.


### SELECT 
La instrucción SELECT en SQL se utiliza para extraer y recuperar datos de una o más tablas en una base de datos. Es como si buscaras información específica en una hoja de cálculo. 
Sintaxis básica:
```
SELECT columna1, columna2, ...
FROM nombre_tabla
[WHERE condición]
```

Explicación de la sintaxis:  
**SELECT**: Indica que se trata de una instrucción SELECT.
**columna1, columna2, ...**: Especifica las columnas de las que deseas obtener datos.  
Puedes incluir todas las columnas de la tabla o solo algunas específicas.  
**FROM**: Indica el origen de los datos. Debe ir seguido del nombre de la tabla de la que deseas extraer la información.  
**[WHERE condición]**: Es opcional. Se utiliza para filtrar los resultados según una condición específica. Por ejemplo, puedes mostrar solo los clientes de un determinado país o los productos con un precio superior a cierto valor.

### UPDATE

### DELETE

### Operadores Lógicos

Operador lógico =
```sql
SELECT * FROM INSTRUCTORS
WHERE INSTRUCTORID = 3
```

Operador lógico IN
```sql
SELECT * FROM INSTRUCTORS
WHERE INSTRUCTORID IN (3,6,8)
```

Operador lógico !=
```sql
SELECT * FROM INSTRUCTORS
WHERE INSTRUCTORID != 3
```

Operaador lógico tipo string
```sql
SELECT * FROM INSTRUCTORS
WHERE FIRSTNAME = 'Kathy'
```

Operaador lógico < >
```sql
SELECT * FROM INSTRUCTORS
WHERE SALARY > 5000
```

Operador between
```sql
SELECT * FROM INSTRUCTORS
WHERE SALARY between 5000 and 9000
```

### Cláusulas de comparación textual en SQL, (AND, NULL, IN, NOT)

#### AND
```sql
SELECT * FROM INSTRUCTORS
WHERE SALARY >50000 AND FIRSTNAME LIKE 'J%'
```
Muestra la tabla de INSTRUCTORS con resultados donde el salario es mayor o igual a 50000 y su nombre empiece por la letra J.

#### OR
```sql
SELECT * FROM INSTRUCTORS
WHERE SALARY >50000 OR FIRSTNAME LIKE 'J%'
```
```sql
SELECT * FROM INSTRUCTORS
WHERE SALARY >50000 OR FIRSTNAME LIKE 'J%' OR FIRSTNAME LIKE 'D%'
```
Muestra la tabla de INSTRUCTORS con resultados donde el salario es mayor o igual a 50000 o donde el nombre de la persona empiece por la letra J O D.

### Funciones de aritmética básica (MIN, MAX)

**MIN**: Se utiliza para obtener el valor mínimo de una columna específica en un conjunto de resultados. Esta función es útil para identificar el valor más bajo entre un grupo de datos. 

```sql
SELECT MIN(AGE) FROM STUDENTS;
```
Muestra la edad minima de la tabla de estudiantes

Es importante destacar que la función MIN ignora los valores NULL al calcular el valor mínimo. Si la columna contiene valores NULL, la función MIN no devolverá el valor no NULL más bajo.

**MAX**: Se utiliza para obtener el valor máximo de una columna especifica en un conjunto de resultados. Esta función es útil para identificar el valor más alto entre un grupo de datos.

```sql
SELECT MAX(AMOUNT) FROM ORDERS;
```

MIN y MAX: Las funciones MIN y MAX se pueden utilizar juntas en consultas más complejas para obtener un rango de valores dentro de un conjunto de datos. 

```sql
SELECT MIN(AGE) AS min_age, MAX(AGE) AS max_age, MAX(AGE) AS age_range FROM STUDENTS;
```

Nota:   
Las funciones MIN y MAX solo se pueden usar con columnas de tipo de datos numérico. Si la columna contiene valores no numéricos, como cadenas de texto, las funciones devolverán un error.
 
### Agrupación de datos en SQL: GROUP BY, HAVING y CASE

#### GROUP BY
Esta cláusula es una herramienta fundamental para agrupar y organizar datos en conjuntos relacionados, permitiendo realizar cálculos y análisis estadísticos más precisos y significativos.

#### HAVING
