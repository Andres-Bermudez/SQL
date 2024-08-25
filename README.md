# SQL

# Indice

- [ER-D Entity Relationalship diagram](#er-d-entity-relationalship-diagram)
- [Estructura basica de una consulta SQL](#estructura-basica-de-una-consulta-sql)
  - [Crear una base de datos](#crear-una-base-de-datos)
  - [Crear una nueva tabla](#crear-una-nueva-tabla)
  - [Insertar datos en una tabla](#insertar-datos-en-una-tabla)
  - [Eliminar registros de una tabla](#eliminar-registros-de-una-tabla)
  - [Actualizar un registro de una tabla](#actualizar-un-registro-de-una-tabla)
- [Operadores logicos](#operadores-lógicos)
- [Esquema de bases de datos](#esquema-de-bases-de-datos)
- [Normalizacion de bases de datos](#normalizacion-de-bases-de-datos)
  - [Primera forma normal](#primera-forma-normal) 
  - [Segunda forma normal](#segunda-forma-normal)
  - [Tercera forma normal](#tercera-forma-normal)

## ER-D Entity Relationalship Diagram:
![ER-D](./images/ER-D.png)

Un diagrama entidad relación (también conocido como diagrama ER o diagrama ERD o 
simplemente ERD) muestra cómo interactúan las entidades (personas, objetos y conceptos). 
Estos modelos conceptuales de datos ayudan a desarrolladores y diseñadores a visualizar 
las relaciones entre elementos clave del software.

El diagrama en sí es un tipo de diagrama de flujo. Es un modelo lógico que muestra cómo 
fluyen los datos de una entidad a otra. Con este formato fácil de seguir, los desarrolladores 
y diseñadores de software pueden visualizar claramente la estructura de un sistema.

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

# Esquema de bases de datos:
![Esquema conceptual DB](./images/ConceptualSchema.png)

Para crear la base de datos de un restaurante, la sintaxis SQL es la siguiente:

    CREATE DATABASE restaurant;

La primera tabla “tbl” representa una mesa del restaurante. Cuenta con un ID único y 
una ubicación, donde se ubica en el restaurante. El ID único es la clave principal de esta tabla.

    CREATE TABLE tbl (
        table_id INT,
        location VARCHAR(255),
        PRIMARY KEY (table_id) 
    ); 

La siguiente tabla contiene datos sobre los camareros que trabajan en el restaurante. Tienen un 
ID único, un nombre, su número de contacto y en qué turno suelen trabajar. La clave principal de 
la tabla es el ID único asignado al camarero.

    CREATE TABLE waiter(
        waiter_id INT,
        name VARCHAR(150),
        contact_no VARCHAR(10),
        shift VARCHAR(10),
        PRIMARY KEY (waiter_id)
    ); 

La siguiente sintaxis crea la tabla que almacena datos sobre pedidos para cada tabla. Tiene los 
campos ID del pedido y ID de la tabla. Además de un campo date_time para registrar la fecha y 
hora del pedido y el ID del camarero que se supone que debe servir esa mesa para ese pedido.

    CREATE TABLE table_order(
        order_id INT,
        date_time DATETIME,
        table_id INT,
        waiter_id INT,
        PRIMARY KEY (order_id),
        FOREIGN KEY (table_id) REFERENCES tbl(table_id),
        FOREIGN KEY (waiter_id) REFERENCES waiter(waiter_id)
    );

Esta tabla almacena datos sobre los clientes. Tiene un ID del cliente, nombre, número NIC para 
almacenar el número del documento nacional de identidad y los campos de número de contacto. La 
clave principal es el campo único ID del cliente.

    CREATE TABLE customer(
        customer_id INT,
        name VARCHAR(100),
        NIC_no VARCHAR(12),
        contact_no VARCHAR(10),
        PRIMARY KEY (customer_id)
    ); 

La tabla de reservas asocia un pedido con un cliente. Tiene un ID único, una fecha y hora, el 
número de invitados o pasajeros esperados, el order_id, table_id y el customer_id. Su clave 
principal es el ID de reserva único. Esta tabla se vincula con las tablas tbl, table_order y cliente.

    CREATE TABLE reservation(
        reservation_id INT,
        date_time DATETIME,
        no_of_pax INT,
        order_id INT,
        table_id INT,
        customer_id INT,
        PRIMARY KEY (reservation_id),
        FOREIGN KEY (order_id) REFERENCES table_order(table_id),
        FOREIGN KEY (table_id) REFERENCES tbl(table_id),
        FOREIGN KEY (customer_id) REFERENCES customer(customer_id)
    ); 

Esta tabla de menú almacena todos los menús del restaurante. Tiene un menu_id que es el campo único 
que contiene descripciones del menú y su disponibilidad.

    CREATE TABLE menu(
        menu_id INT,
        description VARCHAR(255),
        availability INT,
        PRIMARY KEY (menu_id)
    ); 

Cada menú puede tener elementos de menú únicos, y estos elementos se almacenan en el menú, en la tabla
menu_item. Los elementos del menú también tienen campos de descripción, precio y disponibilidad. Esta
tabla se vincula con la tabla de menú.

    CREATE TABLE menu_item(
        menu_item_id INT,
        description VARCHAR(255),
        price FLOAT,
        availability INT,
        menu_id INT,
        PRIMARY KEY (menu_item_id),
        FOREIGN KEY (menu_id) REFERENCES menu(menu_id)
    );

Esta última tabla recoge los elementos de menú solicitados para un pedido concreto. Tiene el order_id, 
menu_item_id y la cantidad solicitada. Tiene una clave principal compuesta de la combinación del campo 
id_pedido e id_elemento_menú, y está vinculada con las tablas pedido_mesa y elemento_menú.

    CREATE TABLE order_menu_item(
        order_id INT,
        menu_item_id INT,
        quantity INT,
        PRIMARY KEY (order_id,menu_item_id),
        FOREIGN KEY (order_id) REFERENCES table_order(order_id),
        FOREIGN KEY (menu_item_id) REFERENCES menu_item(menu_item_id)
    ); 

Estas sentencias CREATE TABLE elaboran todas las tablas de la base de datos de reservas. Es importante 
tener en cuenta la manera en la que se establecen las relaciones entre las tablas. Cada tabla se define 
con una clave principal y, a su vez, se convierte en la clave externa de la tabla relacionada.

# Normalizacion de bases de datos

El proceso de normalización pretende minimizar las duplicaciones de datos, evitar errores durante las 
modificaciones de datos y simplificar las consultas de datos desde la base de datos. Las tres formas 
fundamentales de normalización se conocen como:

    Primera forma normal (1NF)
    Segunda forma normal (2NF)
    Tercera forma normal (3NF)

## Primera forma normal:
#### Regla de atomicidad de los datos: 
La regla de atomicidad de datos significa que solo puede haber un único valor 
de instancia del atributo de columna en cualquier celda de la tabla.

## Segunda forma normal:
En la segunda forma normal, debe evitar cualquier relación de dependencia parcial entre datos. La 
dependencia parcial se refiere a tablas con una clave principal compuesta. Es decir, una clave que 
consta de una combinación de dos o más columnas, donde un valor de atributo no clave depende solo de 
una parte de la clave compuesta.

## Tercera forma normal:
Para que una relación en una base de datos esté en la tercera forma normal, ya debe estar en la segunda 
forma normal (2NF). 

Además, no debe tener dependencia transitiva. Esto significa que cualquier atributo
que no sea clave de la tabla de cirugía puede no depender funcionalmente de otro atributo no clave en la 
misma tabla. 




