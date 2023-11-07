# JARDINERIA 


1. Obtener un listado con el nombre de cada cliente y el nombre y apellido de su representante de ventas.

select c.nombre_cliente as Nombre_Cliente,
concat(e.nombre,' ',e.apellido1,' ',apellido2) as Nombre_Representante_Ventas
from cliente c
JOIN empleado e on c.codigo_empleado_rep_ventas = e.codigo_empleado;
 

2. Muestra el nombre de los clientes que hayan realizado pago junto con el nombre de sus representantes de ventas.

select distinct c.codigo_cliente, c.nombre_cliente as Cliente_hizo_pago, concat(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas  from pago p join cliente c on p.codigo_cliente = c.codigo_cliente join empleado e on c.codigo_empleado_rep_ventas = e.codigo_empleado;



3. Muestra el nombre de los clientes que NO hayan realizado pago junto con el nombre de sus representantes de ventas.


SELECT c.codigo_cliente, c.nombre_cliente as Cliente_sin_pago, 
CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas
FROM cliente c
LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente
JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
WHERE p.codigo_cliente IS NULL;


