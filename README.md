# JARDINERIA 


1. Obtener un listado con el nombre de cada cliente y el nombre y apellido de su representante de ventas.

select c.nombre_cliente as Nombre_Cliente,
concat(e.nombre,' ',e.apellido1,' ',apellido2) as Nombre_Representante_Ventas
from cliente c
JOIN empleado e on c.codigo_empleado_rep_ventas = e.codigo_empleado;
 

2. Muestra el nombre de los clientes que hayan realizado pago junto con el nombre de sus representantes de ventas.

select distinct c.codigo_cliente, c.nombre_cliente as Cliente_hizo_pago, concat(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas  
from pago p 
join cliente c on p.codigo_cliente = c.codigo_cliente 
join empleado e on c.codigo_empleado_rep_ventas = e.codigo_empleado;



3. Muestra el nombre de los clientes que NO hayan realizado pago junto con el nombre de sus representantes de ventas.


SELECT c.codigo_cliente, c.nombre_cliente as Cliente_sin_pago, 
CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas
FROM cliente c
LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente
JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
WHERE p.codigo_cliente IS NULL;


4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus representantes junto con la ciudad de la
oficina a la que pertenece el representante.   

select distinct c.codigo_cliente, c.nombre_cliente as Cliente_hizo_pago, concat(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas, o.ciudad as Oficina
from pago p join cliente c on p.codigo_cliente = c.codigo_cliente 
join empleado e on c.codigo_empleado_rep_ventas = e.codigo_empleado 
JOIN oficina o ON e.codigo_oficina = o.codigo_oficina;

5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.


SELECT c.codigo_cliente, c.nombre_cliente as Cliente_sin_pago,
CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) as Nombre_representante_ventas, o.ciudad as Oficina
FROM cliente c
LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente
JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
join oficina o ON e.codigo_oficina = o.codigo_oficina
WHERE p.codigo_cliente IS NULL;

6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada 

select cliente.linea_direccion1 as direccion , cliente.region as nombre
from empleado 
inner join cliente
on empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
inner join oficina
on empleado.codigo_oficina = oficina.codigo_oficina
where cliente.region = 'Fuenlabrada';


