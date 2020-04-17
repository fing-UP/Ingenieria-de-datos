# DML: Data Manipulation Language
Permite introducir datos para realizar tareas de consultas o modificación de los datos que contienen las Bases de Datos: insert, select, update y delete.

### 1.	Insertar valores

•	Los datos que ingresemos deben mantener la estructura en que fueron ordenados los atributos (en las sentencias de las tablas), y deben obedecer a los tipos de datos indicados. La sentencia correspondiente para añadir una tupla es la que sigue:





```sql
insert into [nombreTabla] values (valor1,valor2,valor3,…);
```


•	Si requerimos añadir varias tuplas, podemos repetir la misma sentencia.

   <img src="fotos/42.PNG" style="width:600px;" > 

•	También podemos separar una tupla de otra con comas:

   <img src="fotos/43.PNG" style="width:600px;" >

•	Si se efectuó con éxito entonces veremos este mensaje en la consola:

   <img src="fotos/44.PNG" style="width:300px;" >

 
### 2.	Select

•	Para mostrar todos los registros, con datos que corresponden a una columna o varias, de una determinada tabla:




```sql
select [nombreColumna1], [nombreColumna2], …
from [nombreTabla]
```


```sql
select codCliente, edad
from cliente
```

   <img src="fotos/45.PNG" style="width:400px;" >


```sql
select [* = todas las columnas]
from [nombre Tabla]
```


```sql
select * from cliente
select * from libro
select * from compra
```

   <img src="fotos/46.PNG" style="width:600px;" >
   
### 2. 	Select Distinct

•	Respecto al caso, si quisiéramos saber cuáles son todas las universidades cuyos alumnos han comprado en la librería, necesitamos quitar duplicados de los registros, pues varios alumnos pueden provenir de la misma universidad. A continuación, agregaremos 3 registros más, cuyos estudiantes sean de la ‘UBA’.




```sql
insert into cliente values (6, 'Ana Luna', 17 , 'UBA');
insert into cliente values (7, 'Ana Luna', 25 , 'UBA');
insert into cliente values (8, 'Javier Wam', 20 , 'UBA');
```

•	Verificamos que se hayan agregado los nuevos registrados son select.


```sql
select * from cliente
```

<img src="fotos/48.PNG" style="width:600px;" >

•	Para mostrar todos los registros  sin duplicados, con datos que corresponden a una columna o varias, de una determinada tabla:



```sql

select distinct [nombreColumna1], [nombreColumna2], …
from [nombreTabla]

```

```sql
select district universidad 
from cliente
```
### 3.	Update

•	Para modificar datos ya existentes en una tabla:

   <img src="fotos/49.PNG" style="width:400px;" >



```sql
update [nombreTabla],
set [nombreAtributo1]=[valor1], [nombreAtributo2]=[valor2], …
where [condición]

```

•	En este caso, modificaremos el registro 5.

   <img src="fotos/50.PNG" style="width:600px;" > 

•	Modificaremos el nombre, la edad y la universidad del codCliente 5, y ejecutamos.

   





```sql
update cliente
set nombre='Juan Lazo', edad, universidad='USA'
where codCliente=5;
```

•	Consultamos con select los registros de la tabla cliente, y vemos que se actualizó exitosamente.


```sql
select * from cliente
```

   <img src="fotos/52.PNG" style="width:600px;" >


### 4.	Delete
## Herramientas Tecnlógicas
<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/LV.html">I.   Laboratorio Virtual</a>

## Contenido:

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/Introduccion.html">I.	Introducción a SQL</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/DDL.html">II.	DDL: Data Definition Language</a>

III.	DML: Data Manipulation Language

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CD.html">IV.	Consultas Condicionales</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CB.html">V.	Consultas Básicas</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CA.html">VII.	Consultas Agrupada</a>



