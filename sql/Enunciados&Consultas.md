# Enunciados y Consultas

Actualizar el stock indicando el código del producto y la nueva cantidad.


```sql
create procedure cambiarStock
@codigo int,
@valor int
as
	select *
	from Products
	where ProductID=@codigo

	update Products
	set UnitsInStock=@valor
	where ProductID=@codigo

	select *
	from Products
	where ProductID=@codigo

exec cambiarStock 1,38
```


Mostrar los nombres de los productos más vendidos  y sus montos. Indicar la cantidad de registros a mostrar y el año correspondiente.



```sql
create proc montoVendido
@anio int,
@num int
as
	select top (@num) p.ProductName, SUM(Quantity*od.UnitPrice) as Monto
	from Products as p
	inner join [Order Details] as od on od.ProductID=p.ProductID
	inner join Orders as o on o.OrderID=od.OrderID
	where year(OrderDate)=@anio
	group by p.ProductName
	order by Monto

exec montoVendido 1996,4
```

Mostrar los nombres de los productos que no fueron vendidos en el año escogido.


```sql
create proc productoNoVendido
@anio int
as
	select p.ProductName
	from Products as p
	where ProductID not in (
		select ProductID
		from [Order Details] as od
		inner join Orders as o on o.OrderID=od.OrderID
		where YEAR(o.OrderDate)=@anio
		)

exec productoNoVendido 1992
```




Función que devuelva el precio de un producto al indicar su código.



```sql
CREATE FUNCTION dbo.clienteProducto(@cliente varchar(50)) RETURNS table
as
return (
	select p.ProductID, p.ProductName
	from Customers as c
	inner join Orders as o on c.CustomerID=o.CustomerID
	inner join [Order Details] as od on o.OrderID=od.OrderID
	inner join Products as p on od.ProductID=p.ProductID
	where @cliente = c.CompanyName
	)
go


select * from dbo.clienteProducto('Alfreds Futterkiste')

```

Función que devuelva la cantidad de órdenes realizadas por un empleado, al indicar su nombre,


```sql
CREATE FUNCTION dbo.empleadoOrdenes(@empleado varchar(50)) RETURNS table
as
return(
	select COUNT(*) as Cantidad
	from Employees as e
	inner join Orders as o on e.EmployeeID=o.EmployeeID
	where @empleado=e.FirstName
	group by e.FirstName
	)
go


select * from dbo.empleadoOrdenes('Laura')
```


Mostrar ‘La suma de los números impares es:’ con el resultado de la suma de los 100 primeros números impares.



```sql
declare @contador int
declare @total int
set @contador = 0
set @total = 0

while (@contador <= 100)
	begin
		if (@contador % 2) <> 0
			set @total = @total + @contador
		set @contador = @contador + 1
	end
print 'La suma de los números impares es:'+str(@total)
```

Se sabe que el stock es suficiente cuando es mayor a 35, insuficiente cuando es menor a 35 y que cuando no hay disponible se debe colocar una orden de reposición. Mostrar un mensaje indicando el estado y el stock actual. Escoger nombres de diversos productos.



```sql
DECLARE @NUMERO INT
SET  @NUMERO = (
				select UnitsInStock
				from Products
				where ProductName='Chai')
IF @NUMERO > 35
	print 'Stock suficiente. Productos en almacén: '+ str(@NUMERO)
ELSE IF @NUMERO <=35
	print 'Stock insuficiente. Productos en almacén: '+ str(@NUMERO)
ELSE 
	print 'Colocar orden de reposición de stock. Porductos en almacén: 0'
```

Se tiene una tabla que se llama clienteTrigger el cual tiene los atributos id, fechaNacimiento y edad. Se desea que en el momento que se inserte el id y la fechaNacimiento se calcule automáticamente con un trigger la edad.


```sql
Create table clienteTrigger (
id  varchar(3),
fechaNacimiento Date,
edad int,
 
)
 
create trigger clacularedades
on clienteTrigger for insert
as
begin
declare @age int
declare @id varchar
select @id=id , @age=DATEDIFF(year,fechaNacimiento,GETDATE()) from inserted
update clienteTrigger set edad=@age from inserted
 
end

```


Se tiene la tabla productostrigger la cual tiene los atributos id, actualizados, precio y nombre. El atributo actualizado hace referencia a cuantas veces se ha actualizado el producto.Se desea que se cree un trigger que en el momento que se actualice el producto el contados de actualizadas incremente en uno y además al terminar de actualizar sql haga un select de los productos actualizados.




```sql
create table productostrigger (
id varchar(5),
actualizadas int default 0,
precio float,
nombre varchar
)


alter trigger actualizarproducto
on productostrigger for update
as
begin
declare @ac int
declare @id varchar(5)
select @ac=actualizadas, @id=id from inserted
set @ac=@ac+1
update productostrigger set actualizadas=@ac from inserted 

select * from productostrigger where id=@id

end

```

Se tiene una pagina web donde almacena en su base de datos cuantas personas dieron click en el producto en venta. Teniendo en cuanta que se conoce la cantidad de personas que comprar el producto calcule el ratio de clicks vs ventas. Asegurase que funcione para todos los casos y utilice try and catch


```sql
declare @clicks int
declare @ventas int
set @ventas =0
set @clicks = 0
BEGIN TRY  
     select @ventas/@clicks
END TRY  
BEGIN CATCH  
     select 0
END CATCH  

```

Se esta integrando una base de datos con una interfaz grafica y los empleados son los que se encargar de utilizar dicha interfaz. Últimamente los trabajadores están tratando de ingresar los datos de los clientes, pero aparentemente lo hacen mal pero no están siendo notificados. Así que usted deberá crea un programa que cuando se inserte los datos mal se retorne el tipo de error con un select. La tabla cliente contiene id:int, nombre:varchar(10), apellid:varchar(10) y sexo:bit not null.


```sql
create table Cliente (
id int,
nombre varchar(10),
apellido varchar(10),
sexo bit not null,
)


BEGIN TRY  
     insert into Cliente values(2,'Stivi','Suenaga','masculino')
END TRY  
BEGIN CATCH  
     select ERROR_MESSAGE()
END CATCH  

```

## Herramientas Tecnlógicas
<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/LV.html">I.   Laboratorio Virtual</a>

## Contenido:

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/Introduccion.html">I.	Introducción a SQL</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/GenerarDiagramas.html">II.	Generar Diagramas</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/DLL.html">III.	DDL: Data Definition Language </a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/DML.html">IV.	DML: Data Manipulation Language</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CD.html">V.	Consultas Condicionales</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CB.html">VI.	Consultas Básicas</a>

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/CA.html">VII.	Consultas Agrupada</a>

## Consultas y Enuncidaos

<a href="https://fing-up.github.io/Ingenieria-de-datos/sql/Enunciados&Consultas.html">Consultas y Enunciados</a>

