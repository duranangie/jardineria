# JARDINERIA

1. Obtén un listado con el nombre de cada cliente y el nombre y apellido de su representante de ventas.

```sql
    SELECT c.nombre_cliente AS Nombre_cliente, e.nombre AS Nombre_rep_ventas, e.apellido1 AS Apellido_rep_ventas FROM cliente c INNER JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado;
```

```sql
    SELECT c.nombre_cliente AS Nombre_cliente,e.nombre AS Nombre_rep_ventas,e.apellido1 AS Apellido_rep_ventas FROM cliente c,empleado e WHERE c.codigo_empleado_rep_ventas = e.codigo_empleado;

```

2. Muestra el nombre de los clientes que hayan realizado pagos junto con el nombre de sus representantes de ventas.

```sql
    SELECT DISTINCT c.codigo_cliente AS COD_Cliente, c.nombre_cliente AS Nombre_cliente, CONCAT( e.nombre,' ',e.apellido1,' ',e.apellido2) AS Representante_ventas FROM cliente c INNER JOIN empleado e  ON c.codigo_empleado_rep_ventas = e.codigo_empleado INNER JOIN pago p ON c.codigo_cliente = p.codigo_cliente ;

```

3. Muestra el nombre de los clientes que no hayan realizado pagos junto con el nombre de sus representantes de ventas.

```sql
    SELECT c.codigo_cliente, c.nombre_cliente ,e.codigo_empleado, CONCAT(e.nombre,' ',e.apellido1,' ',e.apellido2 ) AS REPRESENTANTE_VENTAS FROM cliente c LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente INNER JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado WHERE p.codigo_cliente IS NULL;
```


4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

```sql
     SELECT DISTINCT c.codigo_cliente , c.nombre_cliente AS Cliente , e.codigo_empleado, CONCAT (e.nombre,' ',e.apellido1) AS empleado , o.ciudad AS ciudad_Representante_Ventas  FROM cliente c INNER
JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado INNER JOIN pago p ON c.codigo_cliente = p.codigo_cliente INNER JOIN oficina o ON e.codigo_oficina = o.codigo_oficina;
```

5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

```sql
    SELECT c.nombre_cliente , CONCAT (e.nombre,' ',e.apellido1,' ',e.apellido2)AS representante_ventas , o.ciudad FROM cliente c LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente INNER JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado INNER JOIN oficina o ON e.codigo_oficina = o.codigo_oficina WHERE p.codigo_cliente IS NULL;
```

6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada.

```sql
     SELECT DISTINCT o.linea_direccion1 AS OFICINA_DIRECCIÓN FROM oficina o INNER JOIN empleado e ON o.codigo_oficina = e.codigo_oficina INNER JOIN cliente c ON e.codigo_empleado = c.codigo_empleado_rep_ventas WHERE c.ciudad = 'Fuenlabrada';
```

7. Devuelve el nombre de los clientes y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

```sql
    SELECT c.nombre_cliente , CONCAT (e.nombre,' ',e.apellido1,' ',e.apellido2)AS representante_ventas , o.ciudad AS Ciudad_Representante FROM cliente c INNER JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado INNER JOIN oficina o ON e.codigo_oficina = o.codigo_oficina ;
```

8. Devuelve un listado con el nombre de los empleados junto con el nombre de sus jefes.

```sql
    SELECT e.nombre AS EMPLEADO, ej.nombre AS JEFE FROM empleado e INNER JOIN empleado ej ON e.codigo_jefe = ej.codigo_empleado;
```

9. Devuelve un listado que muestre el nombre de cada empleados, el nombre de su jefe y el nombre del jefe de sus jefe.

```sql
    SELECT e.nombre AS EMPLEADO, ej.nombre AS JEFE ,ejj.nombre AS JEFE_DEL_JEFE FROM empleado e INNER JOIN empleado ej ON e.codigo_jefe = ej.codigo_empleado LEFT JOIN empleado ejj ON ej.codigo_jefe = ejj.codigo_empleado; 
```

10. Devuelve el nombre de los clientes a los que no se les ha entregado a tiempo un pedido.

```sql
    SELECT p.fecha_esperada,p.fecha_entrega, c.nombre_cliente FROM cliente c INNER JOIN pedido p ON c.codigo_cliente = p.codigo_cliente WHERE p.fecha_entrega > p.fecha_esperada OR p.fecha_entrega IS NULL ;
```

11. Devuelve un listado de las diferentes gamas de producto que ha comprado cada cliente.

```sql
    SELECT DISTINCT c.nombre_cliente , g.gama FROM gama_producto g INNER JOIN producto p ON g.gama = p.gama INNER JOIN detalle_pedido d ON p.codigo_producto = d.codigo_producto INNER JOIN pedido pd ON d.codigo_pedido = pd.codigo_pedido INNER JOIN cliente c ON pd.codigo_cliente = c.codigo_cliente; 
```




## segunda consulta


Resuelva todas las consultas utilizando las cláusulas LEFT JOIN, RIGHT JOIN, NATURAL LEFT JOIN Y NATURAL RIGHT JOIN.

1.   Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago

```sql
SELECT DISTINCT nombre_cliente 
from cliente 
LEFT JOIN pago on cliente.codigo_cliente = pago.codigo_cliente
where pago.codigo_cliente is null;
```
2.   Devuelve un listado que muestre solamente los clientes que no han realizado ningún pedido.

```sql
SELECT DISTINCT nombre_cliente 
from cliente 
LEFT JOIN pedido on cliente.codigo_cliente = pedido.codigo_cliente
where pedido.codigo_cliente is null;
```

3.   Devuelve un listado que muestre los clientes que no han realizado ningún pago y los que no han realizado ningún pedido.

```sql

SELECT DISTINCT nombre_cliente 
from cliente 
LEFT JOIN pago on cliente.codigo_cliente = pago.codigo_cliente
LEFT JOIN pedido on cliente.codigo_cliente = pedido.codigo_cliente
where pedido.codigo_cliente IS NULL and pago.codigo_cliente is null; 

```


4.   Devuelve un listado que muestre solamente los empleados que no tienen una oficina asociada.

```sql

SELECT DISTINCT nombre 
from empleado 
LEFT JOIN oficina on empleado.codigo_oficina = oficina.codigo_oficina
where empleado.codigo_oficina IS NULL ;

```

5.   Devuelve un listado que muestre solamente los empleados que no tienen un cliente asociado.

```sql

SELECT DISTINCT nombre 
from empleado 
LEFT JOIN cliente on empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
where cliente.codigo_empleado_rep_ventas IS NULL;

```

6.   Devuelve un listado que muestre solamente los empleados que no tienen un cliente asociado junto con los datos de la
oficina donde trabajan.


```sql

SELECT DISTINCT nombre, oficina.codigo_oficina as oficina,oficina.ciudad ,oficina.pais ,oficina.region ,oficina.codigo_postal ,oficina.telefono, oficina.linea_direccion1, oficina.linea_direccion2 
from empleado 
LEFT JOIN oficina on empleado.codigo_oficina = oficina.codigo_oficina
LEFT JOIN cliente on empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
where cliente.codigo_empleado_rep_ventas IS NULL ;

```




7.   Devuelve un listado que muestre los empleados que no tienen una oficina asociada y los que no tienen un cliente asociado.



```sql

SELECT DISTINCT nombre, oficina.codigo_oficina
from empleado 
LEFT JOIN cliente on empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
LEFT JOIN oficina on empleado.codigo_oficina = oficina.codigo_oficina
where empleado.codigo_oficina IS NULL or cliente.codigo_empleado_rep_ventas IS NULL ;

```


8.   Devuelve un listado de los productos que nunca han aparecido en un pedido. 

```sql

SELECT pr.nombre 
FROM producto pr 
LEFT JOIN detalle_pedido d ON pr.codigo_producto = d.codigo_producto  
WHERE d.codigo_producto is null;
```

9.   Devuelve un listado de los productos que nunca han aparecido en un pedido. El resultado debe mostrar el nombre, la
descripción y la imagen del producto.

```sql

SELECT pr.nombre , pr.descripcion , pr.gama
FROM producto pr 
LEFT JOIN detalle_pedido d ON pr.codigo_producto = d.codigo_producto  
WHERE d.codigo_producto is null;
```


10.   Devuelve las oficinas donde no trabajan ninguno de los empleados que hayan sido los representantes de ventas de algún cliente que haya realizado la compra de algún producto de la gama Frutales.

```sql

select distinct o.codigo_oficina, e.nombre
from oficina o
left join empleado e on o.codigo_oficina = e.codigo_oficina
left join cliente c on e.codigo_empleado = c.codigo_empleado_rep_ventas
left join pedido p on c.codigo_cliente = p.codigo_cliente
left join detalle_pedido dp on p.codigo_pedido = dp.codigo_pedido
left join producto pr ON dp.codigo_producto = pr.codigo_producto
where pr.gama = 'Frutales' and c.codigo_empleado_rep_ventas is not null
and e.codigo_empleado is not null
and c.codigo_cliente is not null
and p.codigo_pedido is not null
and dp.codigo_pedido is not null
and pr.codigo_producto is not null
and o.codigo_oficina is not null;

    

    
    
```


11.  Devuelve un listado con los clientes que han realizado algún pedido pero no han realizado ningún pago.


```sql

 SELECT c.codigo_cliente AS CODIGO,c.nombre_cliente AS CLIENTE
    FROM cliente c
    INNER JOIN pedido p ON c.codigo_cliente = p.codigo_cliente
    LEFT JOIN pago pg ON c.codigo_cliente = pg.codigo_cliente
    WHERE pg.codigo_cliente IS NULL;

        
```

12.   Devuelve un listado con los datos de los empleados que no tienen clientes asociados y el nombre de su jefe asociado.º

```sql

SELECT DISTINCT e.*, ej.nombre as Nombre_del_jefe 
FROM empleado e 
LEFT JOIN cliente c ON e.codigo_empleado = c.codigo_empleado_rep_ventas 
LEFT JOIN empleado ej ON e.codigo_jefe = ej.codigo_empleado 
WHERE c.codigo_empleado_rep_ventas IS NULL;

        
```


## tercer consulta





1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.
```sql
select o.codigo_oficina , o.ciudad from oficina o;    
```


2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.
```sql
select o.telefono , o.ciudad from oficina o where pais='España' ;  
```
3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo jefe tiene un código de jefe igual a 7.
```SQL

select nombre,apellido1,apellido2,email from empleado where codigo_jefe = 7;
```

4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la empresa.
```SQL
select puesto,nombre,apellido1,apellido2, email from empleado where codigo_jefe is NULL ;

```

5. Devuelve un listado con el nombre, apellidos y puesto de aquellos empleados que no sean representantes de ventas.
```SQL

select nombre,apellido1,apellido2, puesto from empleado where puesto != 'Representante Ventas';
```
6. Devuelve un listado con el nombre de los todos los clientes españoles.
```SQL

select nombre_cliente from cliente where pais ='spain';

```

7. Devuelve un listado con los distintos estados por los que puede pasar un pedido.
```SQL

select distinct estado from pedido;
    

```

8. Devuelve un listado con el código de cliente de aquellos clientes que realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:

Utilizando la función YEAR de MySQL.

- Utilizando la función DATE_FORMAT de MySQL.
- Sin utilizar ninguna de las funciones anteriores.

```SQL

select distinct codigo_cliente, fecha_pago from pago  where year(fecha_pago) = 2008;


```

9. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos que no han sido entregados a tiempo.
```SQL

   select codigo_pedido , codigo_cliente, fecha_esperada, fecha_entrega from pedido where fecha_esperada < fecha_entrega ;


```
10. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al menos dos días antes de la fecha esperada.

Utilizando la función ADDDATE de MySQL.

- Utilizando la función DATEDIFF de MySQL.
- ¿Sería posible resolver esta consulta utilizando el operador de suma + o resta - ?
```SQL

   select codigo_pedido , codigo_cliente, fecha_esperada, fecha_entrega from pedido where fecha_entrega <= ADDDATE(fecha_esperada, -2) ;

```

11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.

```SQL
select * from pedido where estado='rechazado' and year(fecha_pedido)=2009;

```

12. Devuelve un listado de todos los pedidos que han sido entregados en el mes de enero de cualquier año.
```SQL
select * from pedido where month(fecha_entrega)=1;

```

13. Devuelve un listado con todos los pagos que se realizaron en el año 2008 mediante Paypal. Ordene el resultado de mayor a menor.
```SQL
select * from pago  where year(fecha_pago) = 2008 and forma_pago = 'Paypal' order by fecha_pago DESC;
```

14. Devuelve un listado con todas las formas de pago que aparecen en la tabla pago. Tenga en cuenta que no deben aparecer formas de pago repetidas.
```SQL
select distinct forma_pago from pago;
```

15. Devuelve un listado con todos los productos que pertenecen a la gama Ornamentales y que tienen más de 100 unidades en stock. El listado deberá estar ordenado por su precio de venta, mostrando en primer lugar los de mayor precio.
```SQL
select codigo_producto, nombre, precio_venta from producto where gama = 'Ornamentales' and cantidad_en_stock > 100 order by precio_venta DESC;
```

16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y cuyo representante de ventas tenga el código de empleado 11 o 30.
```SQL
select * from cliente where ciudad = 'Madrid' and codigo_empleado_rep_ventas = 11 or codigo_empleado_rep_ventas = 30;

```


### 1.4.8 Subconsultas

#### 1.4.8.1 Con operadores básicos de comparación

1. Devuelve el nombre del cliente con mayor límite de crédito.
```SQL
select nombre_cliente from cliente order by limite_credito desc limit 1; 
 
```

2. Devuelve el nombre del producto que tenga el precio de venta más caro.
```SQL
select nombre from producto order by precio_venta desc limit 1;

```

3. Devuelve el nombre del producto del que se han vendido más unidades. (Tenga en cuenta que tendrá que calcular cuál es el número total de unidades que se han vendido de cada producto a partir de los datos de la tabla `detalle_pedido`)

```SQL
SELECT p.nombre
FROM detalle_pedido d
JOIN producto p ON d.codigo_producto = p.codigo_producto
GROUP BY d.codigo_producto, p.nombre
ORDER BY SUM(d.cantidad) DESC
LIMIT 1;
```

4. Los clientes cuyo límite de crédito sea mayor que los pagos que haya realizado. (Sin utilizar `INNER JOIN`).

```SQL
select * from cliente
where limite_credito > (select sum(total) from pago where codigo_cliente = cliente.codigo_cliente);
```
5. Devuelve el producto que más unidades tiene en stock.

```SQL
select nombre from producto where cantidad_en_stock = (select max(cantidad_en_stock) from producto);
```

6. Devuelve el producto que menos unidades tiene en stock.

```SQL
select nombre from producto where cantidad_en_stock = (select min(cantidad_en_stock) from producto);
```

7. Devuelve el nombre, los apellidos y el email de los empleados que están a cargo de **Alberto Soria**.

```SQL
select concat(nombre, ' ', apellido1, ' ', apellido2), email from empleado where codigo_jefe in ( select distinct jefe.codigo_empleado from empleado em      join empleado jefe on em.codigo_jefe = jefe.codigo_empleado where jefe.nombre like 'al%' );
```

#### 1.4.8.2 Subconsultas con ALL y ANY

1. Devuelve el nombre del cliente con mayor límite de crédito.

```SQL
select nombre_cliente,limite_credito
from cliente
where limite_credito >= ALL
(select limite_credito from cliente);

```

2. Devuelve el nombre del producto que tenga el precio de venta más caro.

```SQL
select nombre 
from producto 
where precio_venta >= ALL
(select precio_venta from producto);

```

3. Devuelve el producto que menos unidades tiene en stock.

```SQL
select nombre 
from producto 
where cantidad_en_stock <= ALL
(select cantidad_en_stock from producto);

```



#### 1.4.8.3 Subconsultas con IN y NOT IN

1. Devuelve el nombre, apellido1 y cargo de los empleados que no representen a ningún cliente.

```SQL

select nombre,apellido1,puesto  from empleado where codigo_empleado not in (select codigo_empleado_rep_ventas from cliente);  

```


2. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago.

```SQL

select *  from cliente where codigo_cliente not in (select codigo_cliente from pago);  


```


3. Devuelve un listado que muestre solamente los clientes que sí han realizado algún pago.

```SQL

select *  from cliente where codigo_cliente in (select codigo_cliente from pago);  



```

4. Devuelve un listado de los productos que nunca han aparecido en un pedido.

```SQL
select codigo_producto,nombre from producto where codigo_producto not in (select  codigo_producto from detalle_pedido); 


```


5. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos empleados que no sean representante de ventas de ningún cliente.


```SQL

select empleado.nombre, empleado.apellido1, empleado.apellido2, oficina.telefono from empleado, oficina where codigo_empleado not in (select codigo_empleado_rep_ventas from cliente)
AND empleado.codigo_oficina = oficina.codigo_oficina;

```
6. Devuelve las oficinas donde **no trabajan** ninguno de los empleados que hayan sido los representantes de ventas de algún cliente que haya realizado la compra de algún producto de la gama `Frutales`.

```SQL

select * from oficina where codigo_oficina not in (select codigo_oficina from empleado where codigo_empleado in (select codigo_empleado_rep_ventas from cliente where codigo_cliente in (select codigo_cliente from pedido where codigo_pedido in (select codigo_pedido from detalle_pedido where codigo_producto in ( select codigo_producto from producto where gama = 'Frutales'))))) ;


```
7. Devuelve un listado con los clientes que han realizado algún pedido pero no han realizado ningún pago.
```SQL

select * from cliente where codigo_cliente not in (select codigo_cliente from pago where codigo_cliente ) and codigo_cliente in (select codigo_cliente from pedido ) ;




```
#### 1.4.8.4 Subconsultas con EXISTS y NOT EXISTS

1. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago.
```SQL


select * from cliente where not exists ( select codigo_cliente from pago where pago.codigo_cliente= cliente.codigo_cliente);

```


2. Devuelve un listado que muestre solamente los clientes que sí han realizado algún pago.
```SQL


select * from cliente where exists ( select codigo_cliente from pago where pago.codigo_cliente= cliente.codigo_cliente);

```

3. Devuelve un listado de los productos que nunca han aparecido en un pedido.
```SQL

select * from producto where not exists ( select codigo_pedido from detalle_pedido where producto.codigo_producto = detalle_pedido.codigo_producto);



```


4. Devuelve un listado de los productos que han aparecido en un pedido alguna vez.

```SQL

select * from producto where exists ( select codigo_pedido from detalle_pedido where producto.codigo_producto = detalle_pedido.codigo_producto);


```


# Tips de los videos 

1. Multiple grouping 

- List how many units each range has in stock.

    ```
    SELECT g.gama, p.precio_venta, COUNT(*) cantidad_en_stock 
    FROM producto p
    INNER JOIN gama_producto g ON g.gama = p.gama 
    GROUP BY g.gama, p.precio_venta;
    ```

2. Filter by added features

- Show the range and the units in stock greater than 100 of each of them.

    ```
    SELECT g.gama, COUNT(*) cantidad_en_stock 
    FROM producto 
    INNER JOIN gama_producto g ON g.gama = producto.gama 
    GROUP BY g.gama 
    HAVING COUNT(*) > 100;
    ```

- Show the range and the quantity in stock of the range that begins with the letter 'F', also the minimum quantity in stock must be greater than 10.

    ```
    SELECT g.gama, min(cantidad_en_stock) cantidad_en_stock 
    FROM producto 
    INNER JOIN gama_producto g ON g.gama = producto.gama 
    WHERE SUBSTRING(g.gama, 1, 1) = 'F' 
    GROUP BY g.gama 
    HAVING MIN(cantidad_en_stock) > 10;
    ```

3. Grouped by scalar functions

- Show the first letters of all the ranges there are and the units in stock of each of them.

    ```
    SELECT SUBSTRING(g.gama, 1,1) AS letraGama, COUNT(*) cantidad_en_stock 
    FROM producto 
    INNER JOIN gama_producto g ON g.gama = producto.gama 
    GROUP BY SUBSTRING(g.gama, 1,1);
    ```


4. Grouped with UNION ALL

- List the ranges and sales prices, in addition to showing the total number of ranges in products and the amount of price that is repeated.

    ```
    SELECT todo, COUNT(*) AS Total 
    FROM (SELECT concat('Gama: ', g.gama) AS todo FROM producto INNER JOIN gama_producto g ON g.gama = producto.gama UNION ALL SELECT CONCAT('Precios de Ventas: ', CAST(producto.precio_venta as char)) AS todo FROM producto) AS Tabla 
    GROUP BY todo;
    ```


5. Concatenate clustering results

- List the types of ranges and the products that belong to it.

    ```
    SELECT g.gama, GROUP_CONCAT(producto.nombre ORDER BY producto.nombre DESC SEPARATOR '/ ') AS producto
    FROM producto
    INNER JOIN gama_producto g ON g.gama = producto.gama
    GROUP BY g.gama;
    ```

6. Extra: Totals by grouping

- List the range, sales price and total units of those fields.

    ```
    SELECT IFNULL(g.gama, 'TOTAL') AS gama, IFNULL(CAST(producto.precio_venta AS CHAR), 'TOTAL') AS precio, COUNT(*) AS total
    FROM producto
    INNER JOIN gama_producto g ON g.gama = producto.gama
    GROUP BY g.gama, producto.precio_venta WITH ROLLUP;
    ```

--------------------------------------------------------------------------------------------------------------

# TIPS WHERE

1. NOT IN

- List products where their id isn't 'AR-001' and 'FR-1'.

    ```
    SELECT codigo_producto 
    FROM producto 
    WHERE codigo_producto NOT IN('AR-001', 'FR-1');
    ```

2. Subquery

- List the ranges that are in the product and that are greater than zero.

    ```
    SELECT * 
    FROM gama_producto g 
    WHERE (SELECT count(*) FROM producto  WHERE producto.gama = g.gama) > 0;
    ```

3. REGEX

- Product's name where they contain a 'y' or a 'z'.

    ```
    SELECT * 
    FROM producto 
    WHERE nombre REGEXP "[y-z]";
    ```
    
- Range's name where they start with H.

    ```
    SELECT * 
    FROM producto 
    WHERE gama REGEXP '^H';
    ```

- Product's name where they end with a.

    ```
    SELECT * 
    FROM producto 
    WHERE nombre REGEXP 'a$';
    ```

- Product's name where it contains a blank space.

    ```
    SELECT * 
    FROM producto 
    WHERE nombre REGEXP '([A-Za-z]+[\s][A-Za-z]+)';
    ```

4. IN and Subquery

- Product's name where its range starts with A.

    ```
    SELECT * 
    FROM producto 
    WHERE gama IN(SELECT gama FROM gama_producto WHERE gama REGEXP '^A');
    ```


5. Functions

- Product's name where its range begins with F.

    ```
    SELECT * 
    FROM producto 
    WHERE SUBSTRING(gama,1,1) = 'F';
    ```
---------------------------------------------------------------------------------------------------------------

# TIPS UPDATE  

1. Edit using already saved value

- Update the sale price by adding 10.00.

    ```
    UPDATE producto 
    SET precio_venta = precio_venta +10.00;
    ```

2. Multiple grouping

-  Update the sales price using a default value.

    ```
    UPDATE producto 
    SET precio_venta = DEFAULT;
    ```
Note: It doesn't have a default value, but if it did it would give a result.

3. Edit getting value by subquery

- Update the product's description with the name of the range and the name of the respective product.

    ```
    UPDATE producto 
    SET descripcion = (SELECT CONCAT(g.gama, ' ', producto.nombre) FROM gama_producto g WHERE g.gama = producto.gama);
    ```

4. Subqueries in WHERE

- Update the word 'pato' where the first letter of the selected field starts with H.

    ```
    UPDATE producto 
    SET prueba = 'pato' 
    WHERE producto.prueba LIKE 'H%';
    ```
Note: The following query can be done, but this database fails in a constraint.
    ```
    UPDATE producto 
    SET gama = 'pato' WHERE producto.gama IN(SELECT gama FROM gama_producto g WHERE g.gama LIKE 'H%');
    ```

5. UPDATE con JOIN

- Update to transcribe product ranges by 'gama_producto' ranges.

    ```
    UPDATE producto
    INNER JOIN gama_producto ON gama_producto.gama = producto.gama
    SET producto.gama = gama_producto.gama;
    ```

---------------------------------------------------------------------------------------------------------------

# TIPS SELECT

1. Fixed values

- Add a column and assign a value to it if it isn't in the original table.

    ```
    SELECT codigo_producto, nombre, gama, 1 AS ghost 
    FROM producto;
    ```

2. Operations with columns

-  Know the total of two columns that are related, but are different tables.

    ```
    SELECT DISTINCT d.precio_unidad, producto.precio_venta, (d.precio_unidad + producto.precio_venta) AS Suma FROM producto 
    INNER JOIN detalle_pedido d ON d.codigo_producto = producto.codigo_producto;
    ```

-  Know the total of two columns that are related, but are from different tables and know the product's name with the quantity they have of it.

    ```
    SELECT DISTINCT d.precio_unidad, producto.precio_venta, (d.precio_unidad + producto.precio_venta) AS Suma, CONCAT(producto.nombre, ' - ', d.cantidad) AS Almacenado_producto_cantidad 
    FROM producto 
    INNER JOIN detalle_pedido d ON d.codigo_producto = producto.codigo_producto;
    ```

3. Conditions

- List products and list in 'Retornar' when they are equal to 'Membrillero' a 1 appears, but if it's 'Higuera' a 2 and if it's not in the previous condition it returns a 3.

    ```
    SELECT nombre, CASE WHEN nombre = 'Membrillero' THEN 1 WHEN nombre = 'Higuera' THEN 2 ELSE 3 END AS Retornar 
    FROM producto;
    ```

4. Subqueries

- List the ranges and the total ranges there are for each product.

    ```
    SELECT gama, (SELECT COUNT(producto.gama) FROM producto WHERE producto.gama = gama_producto.gama) AS Total_gamas_productos 
    FROM gama_producto;
    ```

5. Query on Subquery

- List the ranges and the total number of ranges for each product, but greater than 4.

    ```
    SELECT gama, Total_gama 
    FROM (SELECT g.gama, COUNT(g.gama) AS Total_gama FROM producto INNER JOIN gama_producto g ON g.gama = producto.gama GROUP BY g.gama) AS MiTabla 
    WHERE MiTabla.Total_gama > 4;
    ```

6. Extra: Autoincremental virtual column

- List an autoincremental id, the product code in relation to the autoincremental and list the product's name.

    ```
    SELECT ROW_NUMBER() OVER (ORDER BY (SELECT 1)) AS MiId, codigo_producto, nombre
    FROM producto ORDER BY nombre;
    ```




 
