# SQL

## Estructura basica de una consulta SQL:
    SELECT ColumnaUno, ColumnaDos ...
    FROM Nombre_Tabla 
    WHERE ColumnaUno = 'Condicion'
    ORDER BY ColumnaDos DESC
    ...
    ...;

## Crear una base de datos:
    CREATE DATABASE Nombre_Base_Datos;

## Crear una nueva tabla:
### 1. Seleccionar la base de datos: 
    USE Nombre_Base_Datos; 

### 2. Crear la tabla:
    CREATE TABLE Nombre_Tabla (Nombre_Columna TIPO_DATOS RESTRICCIONES FOREIGN KEY(Nombre_Columna ...));

## Insertar datos en una tabla:
    INSERT INTO Nombre_Tabla VALUES (Valor_ColumnaUno, Valor_ColumnaDos ...);

## Eliminar registros de una tabla:
    DELETE FROM nombre_de_la_tabla
    WHERE condición;

## Actualizar un registro de una tabla:
    UPDATE nombre_de_la_tabla
    SET columna1 = valor1,
    columna2 = valor2,
    ...
    columnaN = valorN
    WHERE condición;

## Operadores lógicos:

### ALL
Se utiliza para comparar un único valor con todos los valores de otro conjunto de valores.

### AND
Permite la existencia de varias condiciones en la cláusula WHERE de una indicación SQL.

### ANY
Se utiliza para comparar un valor con cualquier valor aplicable de la lista según la condición.

### BETWEEN
Se utiliza para buscar valores que estén dentro de un conjunto de valores, dado el valor mínimo y el valor máximo.

### EXISTS
Se utiliza para buscar la presencia de una fila en una tabla específica que cumpla con un criterio determinado.

### IN
Se utiliza para comparar un valor con una lista de valores literales que se hayan especificado.

### LIKE
Se utiliza para comparar un valor con valores similares por medio de operadores comodín.

### NOT
Invierte el significado del operador lógico con el que se utiliza. Por ejemplo: NOT EXISTS, NOT BETWEEN, NOT IN, etc. Este es un operador negativo.

### OR
Se utiliza para combinar varias condiciones en la cláusula WHERE de una indicación SQL.

### IS NULL
Se utiliza para comparar un valor con un valor NULL.

### UNIQUE
Busca la singularidad en cada fila de una tabla determinada (sin duplicados).
