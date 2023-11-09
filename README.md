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

