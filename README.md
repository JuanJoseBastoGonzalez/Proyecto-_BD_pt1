1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.

   ```sql
   SELECT o.id_oficina, c.nombre_ciudad
   FROM oficina o
   JOIN ubicacion u ON o.id_ubicacion = u.id_ubicacion
   JOIN ciudad c ON u.id_ciudad = c.id_ciudad;
   +------------+---------------+
   | id_oficina | nombre_ciudad |
   +------------+---------------+
   |          1 | Madrid        |
   |          2 | París         |
   |          3 | Berlín        |
   +------------+---------------+
   ```

   

2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.

   ```sql
   SELECT ciudad.nombre_ciudad, contacto.telefono
   FROM oficina
   INNER JOIN ubicacion ON oficina.id_ubicacion = ubicacion.id_ubicacion
   INNER JOIN ciudad ON ubicacion.id_ciudad = ciudad.id_ciudad
   INNER JOIN pais ON ubicacion.id_pais = pais.id_pais
   INNER JOIN contacto ON oficina.id_contacto = contacto.id_contacto
   WHERE pais.nombre_pais = 'España';
   +---------------+-----------+
   | nombre_ciudad | telefono  |
   +---------------+-----------+
   | Madrid        | 987654321 |
   +---------------+-----------+
   ```

   

3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo
    jefe tiene un código de jefe igual a 7.

  ```sql
  SELECT per.nombre, per.apellido1, per.apellido2, con.email
  FROM empleado e
  INNER JOIN contacto con on e.id_contacto = con.id_contacto
  INNER JOIN persona per ON e.id_persona = per.id_persona
  WHERE e.id_jefe = 7;
  Program did not output anything!
  ```

  

4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la
    empresa.

  ```sql
  SELECT empleado.puesto, persona.nombre, persona.apellido1, persona.apellido2, contacto.email
  FROM empleado
  INNER JOIN persona ON empleado.id_persona = persona.id_persona
  INNER JOIN contacto ON persona.id_contacto = contacto.id_contacto
  WHERE empleado.id_jefe IS NULL;
  Program did not output anything!
  ```

  

5. Devuelve un listado con el nombre, apellidos y puesto de aquellos
    empleados que no sean representantes de ventas.

  ```sql
  SELECT persona.nombre, persona.apellido1, persona.apellido2, empleado.puesto
  FROM empleado
  INNER JOIN persona ON empleado.id_persona = persona.id_persona
  WHERE empleado.puesto != 'Representante de ventas';
  +--------+-----------+-----------+------------+
  | nombre | apellido1 | apellido2 | puesto     |
  +--------+-----------+-----------+------------+
  | Juan   | Pérez     | García    | Gerente    |
  | María  | López     | Martínez  | Vendedor   |
  | Carlos | González  | Sánchez   | Almacenero |
  +--------+-----------+-----------+------------+
  ```

  

6. Devuelve un listado con el nombre de los todos los clientes españoles.

   ```
   
   ```

   

7. Devuelve un listado con los distintos estados por los que puede pasar un
    pedido.

  ```sql
  SELECT DISTINCT estado
  FROM pedido;
  +------------+
  | estado     |
  +------------+
  | Pendiente  |
  | En Proceso |
  | Entregado  |
  +------------+
  ```

  

8. Devuelve un listado con el código de cliente de aquellos clientes que
    realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar
    aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:
    • Utilizando la función YEAR de MySQL.
    • Utilizando la función DATE_FORMAT de MySQL.
    • Sin utilizar ninguna de las funciones anteriores.

  ```sql
  SELECT DISTINCT id_cliente 
  FROM pago
  INNER JOIN fecha on pago.id_fecha = fecha.id_fecha
  WHERE YEAR(fecha.fecha_pedido) = 2008;
  Program did not output anything!
  
  SELECT DISTINCT id_cliente
  FROM pago
  INNER JOIN fecha on pago.id_fecha = fecha.id_fecha
  WHERE DATE_FORMAT(fecha_pedido, '%Y') = '2008';
  Program did not output anything!
  
  SELECT DISTINCT id_cliente
  FROM pago
  INNER JOIN fecha on pago.id_fecha = fecha.id_fecha
  WHERE fecha_pedido >= '2008-01-01' AND fecha_pedido < '2009-01-01';
  Program did not output anything!
  ```

  

9. Devuelve un listado con el código de pedido, código de cliente, fecha
    esperada y fecha de entrega de los pedidos que no han sido entregados a
    tiempo.

  ```sql
  SELECT pedido.id_pedido, pedido.id_cliente, fecha.fecha_esperada_entrega, fecha.fecha_real_entrega
  FROM pedido
  INNER JOIN fecha ON pedido.id_fecha = fecha.id_fecha
  WHERE fecha.fecha_real_entrega > fecha.fecha_esperada_entrega;
  Program did not output anything!
  ```

  

10. Devuelve un listado con el código de pedido, código de cliente, fecha
    esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al
    menos dos días antes de la fecha esperada.
    • Utilizando la función ADDDATE de MySQL.
    • Utilizando la función DATEDIFF de MySQL.
    • ¿Sería posible resolver esta consulta utilizando el operador de suma + o
    resta -?

    ```sql
    
    SELECT id_pedido, id_cliente, fecha_esperada_entrega, fecha_real_entrega
    FROM pedido
    INNER JOIN fecha ON pedido.id_fecha = fecha.id_fecha
    WHERE fecha_real_entrega < ADDDATE(fecha_esperada_entrega, -2);
    Program did not output anything!
    
    SELECT id_pedido, id_cliente, fecha_esperada_entrega, fecha_real_entrega
    FROM pedido
    INNER JOIN fecha ON pedido.id_fecha = fecha.id_fecha
    WHERE DATEDIFF(fecha_esperada_entrega, fecha_real_entrega) >= 2;
    Program did not output anything!
    
    No es posible resolver esta consulta utilizando el operador de suma + o resta -.
    ```

    

11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.

```sql

SELECT pedido.id_pedido, pedido.id_fecha, id_cliente, estado, comentarios
FROM pedido
INNER JOIN fecha ON pedido.id_fecha = fecha.id_fecha
WHERE estado = 'Rechazado' AND YEAR(fecha.fecha_pedido) = 2009;
Program did not output anything!
```

12. Devuelve un listado de todos los pedidos que han sido entregados en el
    mes de enero de cualquier año.

    ```sql
    SELECT pedido.id_pedido, pedido.id_cliente, pedido.estado, pedido.comentarios
    FROM pedido
    INNER JOIN fecha ON pedido.id_fecha = fecha.id_fecha
    WHERE MONTH(fecha.fecha_real_entrega) = 1;
    
    Program did not output anything!
    ```

    

13. Devuelve un listado con todos los pagos que se realizaron en el
    año 2008 mediante Paypal. Ordene el resultado de mayor a menor.

    ```sql
    SELECT pago.id_pago, pago.id_cliente, pago.id_fecha, monto_total, metodo_pago
    FROM pago
    INNER JOIN fecha ON pago.id_fecha = fecha.id_fecha
    WHERE YEAR(fecha_pedido) = 2008 AND metodo_pago = 'Paypal'
    ORDER BY monto_total DESC;
    Program did not output anything!
    ```

    

14. Devuelve un listado con todas las formas de pago que aparecen en la
    tabla pago. Tenga en cuenta que no deben aparecer formas de pago
    repetidas.

    ```sql
    SELECT DISTINCT metodo_pago
    FROM pago;
    +---------------+
    | metodo_pago   |
    +---------------+
    | Tarjeta       |
    | Transferencia |
    | Efectivo      |
    +---------------+
    ```

    

15. Devuelve un listado con todos los productos que pertenecen a la
    gama Ornamentales y que tienen más de 100 unidades en stock. El listado
    deberá estar ordenado por su precio de venta, mostrando en primer lugar
    los de mayor precio.

    ```sql
    SELECT producto.id_producto, producto.nombre, producto.id_gama, producto.id_dimensiones, producto.id_proveedor, producto.descripcion, producto.id_precio
    FROM producto
    INNER JOIN gama_producto ON producto.id_gama = gama_producto.id_gama
    INNER JOIN stock ON producto.id_producto = stock.id_stock
    WHERE gama_producto.descripcion_texto = 'Ornamentales' AND stock.stock_actual > 100
    ORDER BY producto.id_precio DESC;
    
    Program did not output anything!
    ```

    

16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y
    cuyo representante de ventas tenga el código de empleado 11 o 30.

```sql
SELECT cliente.id_cliente, cliente.id_ubicacion, cliente.id_empleado, cliente.id_ultimo_pedido, cliente.limite_credito
FROM cliente
INNER JOIN ubicacion ON cliente.id_ubicacion = ubicacion.id_ubicacion
INNER JOIN ciudad ON ubicacion.id_ciudad = ciudad.id_ciudad
INNER JOIN empleado ON cliente.id_empleado = empleado.id_empleado
WHERE ciudad.nombre_ciudad = 'Madrid' AND (empleado.id_empleado = 11 OR empleado.id_empleado = 30);
Program did not output anything!
```

Consultas multitabla (Composición interna)
Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2. Las consultas con
sintaxis de SQL2 se deben resolver con INNER JOIN y NATURAL JOIN.
1. Obtén un listado con el nombre de cada cliente y el nombre y apellido de su
    representante de ventas.

  ```sql
  SELECT pcliente.nombre, pempleado.nombre
  FROM persona pcliente
  INNER JOIN cliente c ON pcliente.id_persona = c.id_cliente
  join empleado e on c.id_empleado = e.id_empleado
  join persona pempleado on pempleado.id_persona = e.id_empleado;
  
  SELECT pcliente.nombre AS nombre_cliente, pempleado.nombre AS nombre_empleado
  FROM cliente
  NATURAL JOIN empleado
  JOIN persona AS pcliente ON cliente.id_cliente = pcliente.id_persona
  JOIN persona AS pempleado ON empleado.id_empleado = pempleado.id_persona;
  
  +--------+--------+
  | nombre | nombre |
  +--------+--------+
  | Juan   | Juan   |
  | María  | María  |
  | Carlos | Carlos |
  +--------+--------+
  
  ```

  

2. Muestra el nombre de los clientes que hayan realizado pagos junto con el
    nombre de sus representantes de ventas.

  ```sql
  SELECT persona.nombre, persona.nombre, persona.apellido1
  FROM cliente
  INNER JOIN persona on cliente.id_cliente = persona.id_persona
  INNER JOIN empleado ON cliente.id_empleado = empleado.id_empleado
  INNER JOIN pago ON cliente.id_cliente = pago.id_cliente;
  +--------+--------+-----------+
  | nombre | nombre | apellido1 |
  +--------+--------+-----------+
  | Juan   | Juan   | Pérez     |
  | María  | María  | López     |
  | Carlos | Carlos | González  |
  +--------+--------+-----------+
  
  ```

  

3. Muestra el nombre de los clientes que no hayan realizado pagos junto con
     el nombre de sus representantes de ventas.

     ```sql
     SELECT p.nombre AS cliente, per.nombre AS representante
     FROM cliente c
     JOIN empleado e ON c.id_empleado = e.id_empleado
     JOIN persona per ON e.id_persona = per.id_persona
     JOIN pago pa ON c.id_cliente = pa.id_cliente
     JOIN persona p ON c.id_cliente = p.id_persona
     WHERE pa.id_pago IS NULL;
     Program did not output anything!
     ```

     

4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus
     representantes junto con la ciudad de la oficina a la que pertenece el
       representante.

     ```sql
     
     
     SELECT p.nombre AS cliente, per.nombre AS representante, ci.nombre AS ciudad_oficina
     FROM cliente c
     JOIN empleado e ON c.id_empleado = e.id_empleado
     JOIN persona per ON e.id_persona = per.id_persona
     JOIN pago pa ON c.id_cliente = pa.id_cliente
     JOIN persona p ON c.id_cliente = p.id_persona
     JOIN oficina o ON e.id_oficina = o.id_oficina
     JOIN ubicacion u ON o.id_ubicacion = u.id_ubicacion
     JOIN ciudad ci ON u.id_ciudad = ci.id_ciudad;
     +---------+---------------+----------------+
     | cliente | representante | ciudad_oficina |
     +---------+---------------+----------------+
     | Juan    | Juan          | BUCARAMANGA    |
     | María   | María         | BOGOTA         |
     | Pedro   | Pedro         | CALI           |
     +---------+---------------+----------------+
     ```

     

5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre
     de sus representantes junto con la ciudad de la oficina a la que pertenece el
       representante.

     ```sql
     SELECT p.nombre AS cliente, per.nombre AS representante, ci.nombre AS ciudad_oficina
     FROM cliente c
     JOIN empleado e ON c.id_empleado = e.id_empleado
     JOIN persona per ON e.id_persona = per.id_persona
     LEFT JOIN pago pa ON c.id_cliente = pa.id_cliente
     JOIN persona p ON c.id_cliente = p.id_persona
     JOIN oficina o ON e.id_oficina = o.id_oficina
     JOIN ubicacion u ON o.id_ubicacion = u.id_ubicacion
     JOIN ciudad ci ON u.id_ciudad = ci.id_ciudad
     WHERE pa.id_pago IS NULL;
     Program did not output anything!
     ```

     

6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada.

     ```sql
     
     SELECT u.linea_direccion1, u.linea_direccion2
     FROM ubicacion u
     JOIN oficina o ON u.id_ubicacion = o.id_ubicacion
     JOIN empleado e ON o.id_oficina = e.id_oficina
     JOIN cliente c ON e.id_empleado = c.id_empleado
     JOIN ubicacion u2 ON c.id_ubicacion = u2.id_ubicacion
     JOIN ciudad ci ON u2.id_ciudad = ci.id_ciudad
     WHERE ci.nombre;
     Program did not output anything!
     ```

     

7. Devuelve el nombre de los clientes y el nombre de sus representantes junto
     con la ciudad de la oficina a la que pertenece el representante.

```sql

SELECT p.nombre AS cliente, per.nombre AS representante, ci.nombre AS ciudad_oficina
FROM cliente c
JOIN empleado e ON c.id_empleado = e.id_empleado
JOIN persona per ON e.id_persona = per.id_persona
JOIN persona p ON c.id_cliente = p.id_persona
JOIN oficina o ON e.id_oficina = o.id_oficina
JOIN ubicacion u ON o.id_ubicacion = u.id_ubicacion
JOIN ciudad ci ON u.id_ciudad = ci.id_ciudad;
+---------+---------------+----------------+
| cliente | representante | ciudad_oficina |
+---------+---------------+----------------+
| Juan    | Juan          | BUCARAMANGA    |
| María   | María         | BOGOTA         |
| Pedro   | Pedro         | CALI           |
+---------+---------------+----------------+
```

8. Devuelve un listado con el nombre de los empleados junto con el nombre
    de sus jefes.

  ```sql
  select p.nombre AS nombreE,p.nombre AS nombreJ
  FROM persona p
  JOIN empleado e ON e.id_empleado = p.id_persona
  join  jefe j ON e.id_jefe = j.id_jefe;
   
  STDIN
  Input for the program ( Optional )
  
  Output:
  
  +---------+---------+
  | nombreE | nombreJ |
  +---------+---------+
  | María   | María   |
  | Pedro   | Pedro   |
  +---------+---------+
  ```

  

9. Devuelve un listado que muestre el nombre de cada empleados, el nombre
    de su jefe y el nombre del jefe de sus jefe.

  ```sql
  select p.nombre AS nombreE,p.nombre AS nombreJ, p.nombre AS nombrejj
  FROM persona p
  JOIN empleado e ON e.id_empleado = p.id_persona
  join  jefe j ON e.id_jefe = j.id_jefe
  join jefe j on j.id_jefe = j.id_jefe;
  +---------+---------+----------+
  | nombreE | nombreJ | nombrejj |
  +---------+---------+----------+
  | María   | María   | María    |
  | Pedro   | Pedro   | Pedro    |
  +---------+---------+----------+
  ```

  

10. Devuelve el nombre de los clientes a los que no se les ha entregado a
    tiempo un pedido.

    ```sql
    SELECT p.nombre AS cliente
    FROM pedido ped
    JOIN cliente c ON ped.id_cliente = c.id_cliente
    join fecha on ped.id_fecha = fecha.id_fecha
    JOIN persona p ON c.id_cliente = p.id_persona
    WHERE ped.estado != 'Entregado' AND fecha_espera< fecha_entrega;
    +---------+
    | cliente |
    +---------+
    | Juan    |
    | María   |
    | Pedro   |
    +---------+
    ```

    

11. Devuelve un listado de las diferentes gamas de producto que ha comprado
    cada cliente.

```sql
SELECT p.nombre AS cliente, gp.descripcion_texto AS gama_producto
FROM cliente c
JOIN pedido ped ON c.id_cliente = ped.id_cliente
JOIN detalle_pedido dp ON ped.id_pedido = dp.id_pedido
JOIN producto prod ON dp.id_producto = prod.id_producto
JOIN gama_producto gp ON prod.id_gama = gp.id_gama
JOIN persona p ON c.id_cliente = p.id_persona
GROUP BY p.nombre, gp.descripcion_texto;
Program did not output anything!
```

Consultas multitabla (Composición externa)
Resuelva todas las consultas utilizando las cláusulas LEFT JOIN, RIGHT JOIN, NATURAL
LEFT JOIN y NATURAL RIGHT JOIN.
1. Devuelve un listado que muestre solamente los clientes que no han
    realizado ningún pago.

  ```sql
  SELECT p.nombre AS cliente
  FROM cliente c
  LEFT JOIN pago pa ON c.id_cliente = pa.id_cliente
  JOIN persona p ON c.id_cliente = p.id_persona
  WHERE pa.id_pago IS NULL;
  Program did not output anything!
  ```

  

2. Devuelve un listado que muestre solamente los clientes que no han
    realizado ningún pedido.

  ```sql
  SELECT p.nombre AS cliente
  FROM cliente c
  LEFT JOIN pedido ped ON c.id_cliente = ped.id_cliente
  JOIN persona p ON c.id_cliente = p.id_persona
  WHERE ped.id_pedido IS NULL;
  Program did not output anything!
  ```

  

3. Devuelve un listado que muestre los clientes que no han realizado ningún
    pago y los que no han realizado ningún pedido.

  ```sql
  SELECT p1.nombre AS cliente_sin_pago, p2.nombre AS cliente_sin_pedido
  FROM cliente c
  LEFT JOIN pago pa ON c.id_cliente = pa.id_cliente
  LEFT JOIN pedido ped ON c.id_cliente = ped.id_cliente
  JOIN persona p1 ON c.id_cliente = p1.id_persona
  JOIN persona p2 ON c.id_cliente = p2.id_persona
  WHERE pa.id_pago IS NULL OR ped.id_pedido IS NULL;
  Program did not output anything!
  ```

  

4. Devuelve un listado que muestre solamente los empleados que no tienen
    una oficina asociada.

  ```sql
  SELECT per.nombre AS empleado
  FROM empleado e
  LEFT JOIN oficina o ON e.id_oficina = o.id_oficina
  JOIN persona per ON e.id_persona = per.id_persona
  WHERE o.id_oficina IS NULL;
  Program did not output anything!
  ```

  

5. Devuelve un listado que muestre solamente los empleados que no tienen un
    cliente asociado.

  ```sql
  SELECT per.nombre AS empleado
  FROM empleado e
  LEFT JOIN cliente c ON e.id_empleado = c.id_empleado
  JOIN persona per ON e.id_persona = per.id_persona
  WHERE c.id_empleado IS NULL;
  Program did not output anything!
  ```

  

6. Devuelve un listado que muestre solamente los empleados que no tienen un
    cliente asociado junto con los datos de la oficina donde trabajan.

  ```sql
  SELECT per.nombre AS empleado, ofi.id_oficina, ubi.linea_direccion1, ubi.linea_direccion2
  FROM empleado e
  LEFT JOIN cliente c ON e.id_empleado = c.id_empleado
  LEFT JOIN oficina ofi ON e.id_oficina = ofi.id_oficina
  LEFT JOIN ubicacion ubi ON ofi.id_ubicacion = ubi.id_ubicacion
  JOIN persona per ON e.id_persona = per.id_persona
  WHERE c.id_empleado IS NULL;
  Program did not output anything!
  ```

  

7. Devuelve un listado que muestre los empleados que no tienen una oficina
    asociada y los que no tienen un cliente asociado.

  ```sql
  SELECT per1.nombre AS empleado_sin_oficina, per2.nombre AS empleado_sin_cliente
  FROM empleado e
  LEFT JOIN oficina o ON e.id_oficina = o.id_oficina
  LEFT JOIN cliente c ON e.id_empleado = c.id_empleado
  JOIN persona per1 ON e.id_persona = per1.id_persona
  JOIN persona per2 ON e.id_persona = per2.id_persona
  WHERE o.id_oficina IS NULL OR c.id_empleado IS NULL;
  Program did not output anything!
  ```

  

8. Devuelve un listado de los productos que nunca han aparecido en un
    pedido.

```sql
SELECT prod.nombre AS producto
FROM producto prod
LEFT JOIN detalle_pedido dp ON prod.id_producto = dp.id_producto
WHERE dp.id_detalle IS NULL;
Program did not output anything!
```

9. Devuelve un listado de los productos que nunca han aparecido en un
    pedido. El resultado debe mostrar el nombre, la descripción y la imagen del
    producto.

  ```sql
  SELECT pro.nombre, pro.descripcion, gama.imagen
  FROM producto pro
  JOIN gama_producto gama ON pro.id_gama = gama.id_gama
  LEFT JOIN detalle_pedido dp ON pro.id_producto = dp.id_producto
  WHERE dp.id_detalle IS NULL;
  Program did not output anything!
  ```

  

10. Devuelve las oficinas donde no trabajan ninguno de los empleados que
    hayan sido los representantes de ventas de algún cliente que haya realizado
    la compra de algún producto de la gama Frutales.

    ```
    
    ```

    

11. Devuelve un listado con los clientes que han realizado algún pedido pero no
    han realizado ningún pago.

    ```sql
    SELECT p.nombre 
    FROM persona p
    JOIN cliente cl ON p.id_persona = cl.id_cliente
    LEFT JOIN pago ON cl.id_cliente = pago.id_cliente
    WHERE pago.total IS NULL;
    Program did not output anything!
    ```

    

12. Devuelve un listado con los datos de los empleados que no tienen clientes
    asociados y el nombre de su jefe asociado.

```

```

Consultas resumen
1. ¿Cuántos empleados hay en la compañía?

   ```sql
   SELECT COUNT(id_empleado) AS total_empleados
   FROM empleado;
   +-----------------+
   | total_empleados |
   +-----------------+
   |               3 |
   +-----------------+
   ```

   

2. ¿Cuántos clientes tiene cada país?

   ```sql
   SELECT u.id_pais, p.nombre, COUNT(c.id_cliente) AS total_clientes
   FROM cliente c
   JOIN ubicacion u ON c.id_ubicacion = u.id_ubicacion
   JOIN pais p ON u.id_pais = p.id_pais
   GROUP BY u.id_pais, p.nombre;
   +---------+-----------+----------------+
   | id_pais | nombre    | total_clientes |
   +---------+-----------+----------------+
   |       1 | COLOMBIA  |              1 |
   |       2 | CHILE     |              1 |
   |       3 | ARGENTINA |              1 |
   +---------+-----------+----------------+
   ```

   

3. ¿Cuál fue el pago medio en 2009?

   ```sql
   SELECT AVG(total) AS pago_medio_2009
   FROM pago
   jOin fecha on pago.id_fecha = fecha.id_fecha
   WHERE YEAR(fecha_pedido) = 2009;
   +-----------------+
   | pago_medio_2009 |
   +-----------------+
   |            NULL |
   +-----------------+
   ```

   

4. ¿Cuántos pedidos hay en cada estado? Ordena el resultado de forma
    descendente por el número de pedidos.

  ```sql
  SELECT estado, COUNT(id_pedido) AS total_pedidos
  FROM pedido
  GROUP BY estado
  ORDER BY total_pedidos DESC;
  +------------+---------------+
  | estado     | total_pedidos |
  +------------+---------------+
  | En espera  |             1 |
  | En proceso |             1 |
  | Enviado    |             1 |
  +------------+---------------+
  ```

  

5. Calcula el precio de venta del producto más caro y más barato en una
    misma consulta.

  ```sql
  SELECT MAX(precio_venta) AS precio_mas_caro, MIN(precio_venta) AS precio_mas_barato
  FROM precio;
  +-----------------+-------------------+
  | precio_mas_caro | precio_mas_barato |
  +-----------------+-------------------+
  |           40.00 |             32.00 |
  +-----------------+-------------------+
  ```

  

6. Calcula el número de clientes que tiene la empresa.

   ```sql
   SELECT COUNT(id_cliente) AS total_clientes
   FROM cliente;
   +----------------+
   | total_clientes |
   +----------------+
   |              3 |
   +----------------+
   ```

   

7. ¿Cuántos clientes existen con domicilio en la ciudad de Madrid?

   ```sql
   SELECT COUNT(c.id_cliente) AS total_clientes_madrid
   FROM cliente c
   JOIN ubicacion u ON c.id_ubicacion = u.id_ubicacion
   JOIN ciudad ciu ON u.id_ciudad = ciu.id_ciudad
   WHERE ciu.nombre = 'Madrid';
   +-----------------------+
   | total_clientes_madrid |
   +-----------------------+
   |                     0 |
   +-----------------------+
   ```

   

8. ¿Calcula cuántos clientes tiene cada una de las ciudades que empiezan
    por M?

  ```sql
  SELECT ciu.nombre, COUNT(c.id_cliente) AS total_clientes
  FROM cliente c
  JOIN ubicacion u ON c.id_ubicacion = u.id_ubicacion
  JOIN ciudad ciu ON u.id_ciudad = ciu.id_ciudad
  WHERE ciu.nombre LIKE 'M%'
  GROUP BY ciu.nombre;
  Program did not output anything!
  ```

  

9. Devuelve el nombre de los representantes de ventas y el número de clientes
    al que atiende cada uno.

```sql
SELECT per.nombre AS nombre_representante, COUNT(c.id_cliente) AS clientes_atendidos
FROM empleado e
JOIN cliente c ON e.id_empleado = c.id_empleado
JOIN persona per ON e.id_persona = per.id_persona
WHERE e.puesto = 'Representante de ventas'
GROUP BY per.nombre;
Program did not output anything!
```

10. Calcula el número de clientes que no tiene asignado representante de
    ventas.

    ```sql
    SELECT COUNT(id_cliente) AS clientes_sin_representante
    FROM cliente
    WHERE id_empleado IS NULL;
    +----------------------------+
    | clientes_sin_representante |
    +----------------------------+
    |                          0 |
    +----------------------------+
    ```

    

11. Calcula la fecha del primer y último pago realizado por cada uno de los
    clientes. El listado deberá mostrar el nombre y los apellidos de cada cliente.

```

```

12. Calcula el número de productos diferentes que hay en cada uno de los
    pedidos.

    ```sql
    SELECT id_pedido, COUNT(DISTINCT id_producto) AS productos_diferentes
    FROM detalle_pedido
    GROUP BY id_pedido;
    +-----------+----------------------+
    | id_pedido | productos_diferentes |
    +-----------+----------------------+
    |         1 |                    1 |
    |         2 |                    1 |
    |         3 |                    1 |
    +-----------+----------------------+
    ```

    

13. Calcula la suma de la cantidad total de todos los productos que aparecen en
    cada uno de los pedidos.

    ```sql
    SELECT id_pedido, SUM(cantidad) AS cantidad_total
    FROM detalle_pedido
    GROUP BY id_pedido;
    +-----------+----------------+
    | id_pedido | cantidad_total |
    +-----------+----------------+
    |         1 |              5 |
    |         2 |             10 |
    |         3 |              3 |
    +-----------+----------------+
    ```

    

14. Devuelve un listado de los 20 productos más vendidos y el número total de
    unidades que se han vendido de cada uno. El listado deberá estar ordenado
    por el número total de unidades vendidas.

    ```sql
    SELECT dp.id_producto, p.nombre AS nombre_producto, SUM(dp.cantidad) AS total_unidades_vendidas
    FROM detalle_pedido dp
    JOIN producto p ON dp.id_producto = p.id_producto
    GROUP BY dp.id_producto, p.nombre
    ORDER BY total_unidades_vendidas DESC
    LIMIT 20;
    +-------------+-----------------+-------------------------+
    | id_producto | nombre_producto | total_unidades_vendidas |
    +-------------+-----------------+-------------------------+
    |           2 | Producto B      |                      10 |
    |           1 | Producto A      |                       5 |
    |           3 | Producto C      |                       3 |
    +-------------+-----------------+-------------------------+
    ```

    

15. La facturación que ha tenido la empresa en toda la historia, indicando la
    base imponible, el IVA y el total facturado. La base imponible se calcula
    sumando el coste del producto por el número de unidades vendidas de la
    tabla detalle_pedido. El IVA es el 21 % de la base imponible, y el total la
    suma de los dos campos anteriores.

    ```sql
    SELECT 
        SUM(dp.cantidad * pre.precio_venta) AS base_imponible,
        SUM(dp.cantidad * pre.precio_venta) * 0.21 AS iva,
        SUM(dp.cantidad * pre.precio_venta) + (SUM(dp.cantidad * pre.precio_venta) * 0.21) AS total_facturado
    FROM detalle_pedido dp
    JOIN producto pro ON dp.id_producto = pro.id_producto
    JOIN precio pre ON pro.id_precio = pre.id_precio;
    +----------------+----------+-----------------+
    | base_imponible | iva      | total_facturado |
    +----------------+----------+-----------------+
    |         615.00 | 129.1500 |        744.1500 |
    +----------------+----------+-----------------+
    ```

    

16. La misma información que en la pregunta anterior, pero agrupada por
    código de producto.

    ```sql
    SELECT 
        dp.id_producto,
        SUM(dp.cantidad * pre.precio_venta) AS base_imponible,
        SUM(dp.cantidad * pre.precio_venta) * 0.21 AS iva,
        SUM(dp.cantidad * pre.precio_venta) + (SUM(dp.cantidad * pre.precio_venta) * 0.21) AS total_facturado
    FROM detalle_pedido dp
    JOIN producto pro ON dp.id_producto = pro.id_producto
    JOIN precio pre ON pro.id_precio = pre.id_precio
    GROUP BY dp.id_producto;
    +-------------+----------------+---------+-----------------+
    | id_producto | base_imponible | iva     | total_facturado |
    +-------------+----------------+---------+-----------------+
    |           1 |         175.00 | 36.7500 |        211.7500 |
    |           2 |         320.00 | 67.2000 |        387.2000 |
    |           3 |         120.00 | 25.2000 |        145.2000 |
    +-------------+----------------+---------+-----------------+
    ```

    

17. La misma información que en la pregunta anterior, pero agrupada por
    código de producto filtrada por los códigos que empiecen por OR.

    ```sql
    SELECT 
        dp.id_producto,
        SUM(dp.cantidad * pre.precio_venta) AS base_imponible,
        SUM(dp.cantidad * pre.precio_venta) * 0.21 AS iva,
        SUM(dp.cantidad * pre.precio_venta) + (SUM(dp.cantidad * pre.precio_venta) * 0.21) AS total_facturado
    FROM detalle_pedido dp
    JOIN producto pro ON dp.id_producto = pro.id_producto
    JOIN precio pre ON pro.id_precio = pre.id_precio
    WHERE pro.id_producto LIKE 'OR%'
    GROUP BY dp.id_producto;
    Program did not output anything!
    ```

    

18. Lista las ventas totales de los productos que hayan facturado más de 3000
    euros. Se mostrará el nombre, unidades vendidas, total facturado y total
    facturado con impuestos (21% IVA).

    ```sql
    SELECT 
        pro.nombre AS nombre_producto,
        SUM(dp.cantidad) AS unidades_vendidas,
        SUM(dp.cantidad * pre.precio_venta) AS total_facturado,
        (SUM(dp.cantidad * pre.precio_venta) * 0.21) AS total_facturado_con_IVA
    FROM detalle_pedido dp
    JOIN producto pro ON dp.id_producto = pro.id_producto
    JOIN precio pre ON pro.id_precio = pre.id_precio
    GROUP BY pro.nombre
    HAVING total_facturado > 3000;
    Program did not output anything!
    ```

    

19. Muestre la suma total de todos los pagos que se realizaron para cada uno
    de los años que aparecen en la tabla pagos.

```

```

Subconsultas
Con operadores básicos de comparación
1. Devuelve el nombre del cliente con mayor límite de crédito.

   ```sql
   SELECT per.nombre 
   FROM persona per
   JOIn cliente cl on per.id_persona = cl.id_cliente
   WHERE limite_credito = (SELECT MAX(limite_credito) FROM cliente);
   +--------+
   | nombre |
   +--------+
   | Pedro  |
   +--------+
   ```

   

2. Devuelve el nombre del producto que tenga el precio de venta más caro.

   ```sql
   SELECT nombre
   FROM producto
   WHERE id_producto = (
       SELECT id_producto 
       FROM precio 
       ORDER BY precio_venta DESC 
       LIMIT 1
   );
   +------------+
   | nombre     |
   +------------+
   | Producto A |
   | Producto B |
   | Producto C |
   +------------+
   ```

   

3. Devuelve el nombre del producto del que se han vendido más unidades.
    (Tenga en cuenta que tendrá que calcular cuál es el número total de
    unidades que se han vendido de cada producto a partir de los datos de la
    tabla detalle_pedido)

  ```sql
  SELECT nombre
  FROM producto
  WHERE id_producto = (
      SELECT id_producto 
      FROM detalle_pedido 
      GROUP BY id_producto 
      ORDER BY SUM(cantidad) DESC 
      LIMIT 1
  );
  +------------+
  | nombre     |
  +------------+
  | Producto B |
  +------------+
  ```

  4. Los clientes cuyo límite de crédito sea mayor que los pagos que haya

~~~sql
realizado. (Sin utilizar INNER JOIN).

```sql
SELECT nombre
FROM persona
WHERE id_persona IN (
    SELECT cliente.id_cliente
    FROM cliente
    WHERE limite_credito > (
        SELECT SUM(total) 
        FROM pago 
        WHERE pago.id_cliente = cliente.id_cliente
    )
);
+--------+
| nombre |
+--------+
| Juan   |
| María  |
| Pedro  |
+--------+
```
~~~


​    

  5. Devuelve el producto que más unidades tiene en stock.

     ```sql
     SELECT nombre
     FROM producto
     WHERE id_producto = (SELECT id_stock FROM stock ORDER BY stock_actual DESC LIMIT 1);
     +------------+
     | nombre     |
     +------------+
     | Producto A |
     +------------+
     ```

     

  6. Devuelve el producto que menos unidades tiene en stock.

     ```sql
     SELECT nombre
     FROM producto
     WHERE id_producto = (SELECT id_stock FROM stock ORDER BY stock_actual ASC LIMIT 1);
     +------------+
     | nombre     |
     +------------+
     | Producto C |
     +------------+
     ```

     

  7. Devuelve el nombre, los apellidos y el email de los empleados que están a

    cargo de Alberto Soria.

```sql

SELECT per.nombre, per.apellido1, per.apellido2, cont.email
FROM empleado emp
JOIN persona per ON emp.id_persona = per.id_persona
JOIN jefe j ON emp.id_empleado = j.id_jefe
JOIN persona j_per ON j.id_persona = j_per.id_persona
JOIN contacto cont ON emp.id_contacto = cont.id_contacto
WHERE j_per.nombre = 'Alberto' AND j_per.apellido1 = 'Soria';
Program did not output anything!
```

Subconsultas con ALL y ANY
8. Devuelve el nombre del cliente con mayor límite de crédito.

   ```sql
   SELECT persona.nombre
   FROM persona
   JOIN cliente on persona.id_persona = cliente.id_cliente
   WHERE limite_credito >= ALL (SELECT limite_credito FROM cliente);
   +--------+
   | nombre |
   +--------+
   | Pedro  |
   +--------+
   ```

   

9. Devuelve el nombre del producto que tenga el precio de venta más caro.

   ```sql
   
   SELECT nombre
   FROM producto
   WHERE id_precio = ANY (SELECT id_precio FROM precio WHERE precio_venta >= ALL (SELECT precio_venta FROM precio));
   +------------+
   | nombre     |
   +------------+
   | Producto C |
   +------------+
   ```

   

10. Devuelve el producto que menos unidades tiene en stock.

```sql
SELECT producto.nombre
FROM producto
JOIN stock ON producto.id_producto = stock.id_stock
WHERE id_stock = ANY (SELECT id_stock FROM stock WHERE stock_actual <= ALL (SELECT stock_actual FROM stock));
+------------+
| nombre     |
+------------+
| Producto C |
+------------+
```

Subconsultas con IN y NOT IN
11. Devuelve el nombre, apellido1 y cargo de los empleados que no
    representen a ningún cliente.

    ```sql
    SELECT persona.nombre, persona.apellido1, empleado.puesto
    FROM persona
    jOIN empleado ON persona.id_persona = empleado.id_persona
    WHERE id_empleado NOT IN (SELECT id_empleado FROM cliente);
    Program did not output anything!
    ```

    

12. Devuelve un listado que muestre solamente los clientes que no han
    realizado ningún pago.

    ```sql
    
    SELECT id_cliente, id_ubicacion, id_empleado, id_pedido, limite_credito
    FROM cliente
    WHERE id_cliente NOT IN (SELECT id_cliente FROM pago);
    Program did not output anything!
    ```

    

13. Devuelve un listado que muestre solamente los clientes que sí han realizado
    algún pago.

    ```sql
    SELECT id_cliente, id_ubicacion, id_empleado, id_pedido, limite_credito
    FROM cliente
    WHERE id_cliente IN (SELECT id_cliente FROM pago);
    +------------+--------------+-------------+-----------+----------------+
    | id_cliente | id_ubicacion | id_empleado | id_pedido | limite_credito |
    +------------+--------------+-------------+-----------+----------------+
    |          1 |            1 |           1 |         1 |        1000.00 |
    |          2 |            2 |           2 |         2 |        1500.00 |
    |          3 |            3 |           3 |         3 |        2000.00 |
    +------------+--------------+-------------+-----------+----------------+
    ```

    

14. Devuelve un listado de los productos que nunca han aparecido en un
    pedido.

    ```sql
    SELECT id_producto, nombre, id_gama, id_dimensiones, id_proveedor, descripcion, id_precio
    FROM producto
    WHERE id_producto NOT IN (SELECT id_producto FROM detalle_pedido);
    Program did not output anything!
    ```

    

15. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos
    empleados que no sean representante de ventas de ningún cliente.

    ```sql
    SELECT per.nombre, per.apellido1, e.puesto, con.telefono
    FROM persona per
    JOIN empleado e on per.id_persona = e.id_persona
    JOIN contacto con on e.id_empleado = con.id_contacto
    JOIN oficina o ON e.id_oficina = o.id_oficina
    JOIN cliente c ON e.id_empleado = c.id_empleado
    WHERE e.id_empleado NOT IN (SELECT id_empleado FROM cliente WHERE id_empleado = e.id_empleado);
    Program did not output anything!
    ```

    

16. Devuelve las oficinas donde no trabajan ninguno de los empleados que
    hayan sido los representantes de ventas de algún cliente que haya realizado
    la compra de algún producto de la gama Frutales.

    ```sql
    SELECT id_oficina, id_ubicacion, id_contacto
    FROM oficina
    WHERE id_oficina NOT IN (
        SELECT DISTINCT id_oficina
        FROM empleado
        WHERE id_empleado IN (
            SELECT id_empleado
            FROM cliente
            WHERE id_cliente IN (
                SELECT id_cliente
                FROM detalle_pedido
                WHERE id_producto IN (
                    SELECT id_producto
                    FROM producto
                    WHERE id_gama = 'Frutales'
                )
            )
        )
    );
    +------------+--------------+-------------+
    | id_oficina | id_ubicacion | id_contacto |
    +------------+--------------+-------------+
    |          1 |            1 |           1 |
    |          2 |            2 |           2 |
    |          3 |            3 |           3 |
    +------------+--------------+-------------+
    ```

    

17. Devuelve un listado con los clientes que han realizado algún pedido pero no
    han realizado ningún pago.

```sql
SELECT id_cliente, id_ubicacion, id_empleado, id_pedido, limite_credito
FROM cliente
WHERE id_cliente IN (SELECT id_cliente FROM detalle_pedido)
AND id_cliente NOT IN (SELECT id_cliente FROM pago);
Program did not output anything!
```

Subconsultas con EXISTS y NOT EXISTS
18. Devuelve un listado que muestre solamente los clientes que no han
    realizado ningún pago.

    ```sql
    FROM persona pe
    JOIN cliente c on pe.id_persona = c.id_cliente
    WHERE NOT EXISTS (SELECT 1 FROM pago p WHERE p.id_cliente = c.id_cliente);
    Program did not output anything!
    ```

    

19. Devuelve un listado que muestre solamente los clientes que sí han realizado
    algún pago.

    ```sql
    SELECT pe.nombre, pe.apellido1, pe.apellido2
    FROM persona pe
    JOIN cliente c on pe.id_persona = c.id_cliente
    WHERE  EXISTS (SELECT 1 FROM pago p WHERE p.id_cliente = c.id_cliente);
    +--------+------------+-----------+
    | nombre | apellido1  | apellido2 |
    +--------+------------+-----------+
    | Juan   | García     | López     |
    | María  | Martínez   | Sánchez   |
    | Pedro  | Rodríguez  | Díaz      |
    +--------+------------+-----------+
    ```

    

20. Devuelve un listado de los productos que nunca han aparecido en un
    pedido.

    ```sql
    SELECT nombre
    FROM producto p
    WHERE NOT EXISTS (SELECT 1 FROM detalle_pedido dp WHERE dp.id_producto = p.id_producto);
    Program did not output anything!
    ```

    

21. Devuelve un listado de los productos que han aparecido en un pedido
    alguna vez.

```sql
SELECT nombre
FROM producto p
WHERE EXISTS (SELECT 1 FROM detalle_pedido dp WHERE dp.id_producto = p.id_producto);
+------------+
| nombre     |
+------------+
| Producto A |
| Producto B |
| Producto C |
+------------+
```

Subconsultas correlacionadas
Consultas variadas
1. Devuelve el listado de clientes indicando el nombre del cliente y cuántos
    pedidos ha realizado. Tenga en cuenta que pueden existir clientes que no
    han realizado ningún pedido.

  ```sql
  SELECT per.nombre, COUNT(p.id_pedido) AS pedidos_realizados
  FROM persona per
  JOIN cliente c on  per.id_persona = c.id_cliente
  LEFT JOIN pedido p ON c.id_cliente = p.id_cliente
  GROUP BY c.id_cliente, per.nombre;
  +--------+--------------------+
  | nombre | pedidos_realizados |
  +--------+--------------------+
  | Juan   |                  1 |
  | María  |                  1 |
  | Pedro  |                  1 |
  +--------+--------------------+
  ```

  

2. Devuelve un listado con los nombres de los clientes y el total pagado por
    cada uno de ellos. Tenga en cuenta que pueden existir clientes que no han
    realizado ningún pago.

  ```sql
  SELECT per.nombre, COALESCE(SUM(pa.total), 0) AS total_pagado
  FROM persona per
  JOIN cliente c ON per.id_persona = c.id_cliente
  LEFT JOIN pago pa ON c.id_cliente = pa.id_cliente
  GROUP BY c.id_cliente, per.nombre;
  +--------+--------------+
  | nombre | total_pagado |
  +--------+--------------+
  | Juan   |       500.00 |
  | María  |       750.00 |
  | Pedro  |      1000.00 |
  +--------+--------------+
  ```

  

3. Devuelve el nombre de los clientes que hayan hecho pedidos en 2008
    ordenados alfabéticamente de menor a mayor.

  ```sql
  SELECT per.nombre
  FROM persona per
  JOIN cliente cl ON per.id_persona = cl.id_cliente
  WHERE id_cliente IN (
      SELECT DISTINCT id_cliente
      FROM pedido
      JOIN fecha ON pedido.id_fecha = fecha.id_fecha
      WHERE YEAR(fecha.fecha_pedido) = 2008
  )
  ORDER BY nombre ASC;
  Program did not output anything!
  ```

  

4. Devuelve el nombre del cliente, el nombre y primer apellido de su
    representante de ventas y el número de teléfono de la oficina del
    representante de ventas, de aquellos clientes que no hayan realizado ningún
    pago.

  ```sql
  SELECT per.nombre AS nombre_cliente, p.nombre AS nombre_representante, p.apellido1 AS apellido_representante, cont.telefono AS telefono_oficina
  FROM persona per
  JOIN cliente c on  per.id_persona = c.id_cliente
  LEFT JOIN empleado e ON c.id_empleado = e.id_empleado
  LEFT JOIN persona p ON e.id_persona = p.id_persona
  LEFT JOIN oficina o ON e.id_oficina = o.id_oficina
  JOIN contacto cont ON o.id_contacto = cont.id_contacto
  WHERE c.id_cliente NOT IN (
      SELECT id_cliente
      FROM pago
  );
  Program did not output anything!
  ```

  

5. Devuelve el listado de clientes donde aparezca el nombre del cliente, el
    nombre y primer apellido de su representante de ventas y la ciudad donde
    está su oficina.

  ```sql
  SELECT per.nombre AS nombre_cliente, 
         p.nombre AS nombre_representante, 
         p.apellido1 AS apellido_representante, 
         city.nombre AS ciudad_oficina
  FROM persona per
  JOIN cliente c ON per.id_persona = c.id_cliente
  LEFT JOIN empleado e ON c.id_empleado = e.id_empleado
  LEFT JOIN persona p ON e.id_persona = p.id_persona
  LEFT JOIN oficina o ON e.id_oficina = o.id_oficina
  LEFT JOIN ubicacion u ON o.id_ubicacion = u.id_ubicacion
  LEFT JOIN ciudad city ON u.id_ciudad = city.id_ciudad;
  
  +----------------+----------------------+------------------------+----------------+
  | nombre_cliente | nombre_representante | apellido_representante | ciudad_oficina |
  +----------------+----------------------+------------------------+----------------+
  | Juan           | Juan                 | García                 | BUCARAMANGA    |
  | María          | María                | Martínez               | BOGOTA         |
  | Pedro          | Pedro                | Rodríguez              | CALI           |
  +----------------+----------------------+------------------------+----------------+
  ```

  

6. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos
    empleados que no sean representante de ventas de ningún cliente.

```sql
SELECT p.nombre, p.apellido1, p.apellido2, e.puesto, con.telefono
FROM empleado e
JOIN persona p ON e.id_persona = p.id_persona
JOIN contacto con ON e.id_empleado = con.id_contacto
LEFT JOIN oficina o ON e.id_oficina = o.id_oficina
LEFT JOIN cliente c ON e.id_empleado = c.id_empleado
WHERE e.id_empleado NOT IN (
    SELECT id_empleado
    FROM cliente
);
Program did not output anything!
```

