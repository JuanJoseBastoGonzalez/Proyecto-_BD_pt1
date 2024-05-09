

tabla  gama_producto

```sql
CREATE TABLE gama_producto(
    id_gama varchar(20) PRIMARY KEY,
    descripcion_texto text,
    descripcion_html text,
    imagen varchar(256)
);

```

tabla producto

```sql
CREATE TABLE producto(
id_producto INT(10) AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(70),
id_gama varchar(20),
id_dimenciones INT(20),
id_proveedor INT(20),
descripcion TEXT,
id_precio INT(20)
);
```

tabla detalle_pedido

```sql
CREATE TABLE detalle_pedido(
id_detalle INT(20) AUTO_INCREMENT PRIMARY KEY,
id_pedido INT(20),
id_producto INT(20),
cantidad INT(11),
id_precio INT(20),
numero_linea SMALLINT
);
```

tabla pedido

```sql
CREATE TABLE pedido(
id_pedido INT(20) AUTO_INCREMENT PRIMARY KEY,
id_fecha INT(20),
id_cliente INT(20),
estado VARCHAR(15),
comentarios TEXT
);
```

tabla oficina

```sql
CREATE TABLE oficina(
id_oficina INT(20)AUTO_INCREMENT PRIMARY KEY,
id_ubicacion INT(20),
id_contacto INT(20)
);
```

tabla cliente 

```sql
CREATE TABLE cliente(
id_cliente INT(20) AUTO_INCREMENT PRIMARY KEY,
id_ubicacion INT(20),
id_empleado INT(20),
id_pedido INT(20),
limite_credito DECIMAL(15,2)
);
```

tabla pago

```sql
CREATE TABLE pago(
id_pago INT(20) AUTO_INCREMENT PRIMARY KEY,
id_cliente INT(20),
id_fecha INT(20),
total DECIMAL(15,2),
metodo_pago VARCHAR(50)
);
```

tabla empleado

```sql
CREATE TABLE empleado(
id_empleado INT(20) AUTO_INCREMENT PRIMARY KEY,
id_jefe INT(20),
id_oficina INT(20),
puesto VARCHAR(50),
id_contacto INT(20),
id_persona INT(20)
);
```

tabla stock

```sql
CREATE TABLE stock(
id_stock INT(20) AUTO_INCREMENT PRIMARY KEY,
stock_acutal INT(10),
stock_maximo INT(10),
stock_minimo INT(10)
);
```

tabla dimensiones

```sql
CREATE TABLE dimenciones(
id_dimenciones INT(20) AUTO_INCREMENT PRIMARY KEY,
largo DECIMAL(15,2),
ancho DECIMAL(15,2),
peso DECIMAL(15,2)
);
```

tabla precio

```sql
CREATE TABLE precio(
id_precio INT(20) AUTO_INCREMENT PRIMARY KEY,
precio_compra DECIMAL(15,2),
precio_venta DECIMAL(15,2)
);
```

tabla proveedor

```sql
CREATE TABLE proovedor(
id_provedor INT(20) AUTO_INCREMENT PRIMARY KEY,
id_persona INT(20),
id_ubicacion INT(20)
);
```

tabla persona

```sql
CREATE TABLE persona (
id_persona INT(20) AUTO_INCREMENT PRIMARY KEY,
id_contacto INT(20),
tipo VARCHAR(50),
nombre VARCHAR(50),
apellido1 VARCHAR(50),
apellido2 VARCHAR(50)
);
```

tabla jefe 

```sql
CREATE TABLE jefe(
id_jefe INT(20) AUTO_INCREMENT PRIMARY KEY,
id_persona INT(20),
id_oficina INT(20)
);
```

tabla ubicacion

```sql
CREATE TABLE ubicacion (
id_ubicacion INT(20) AUTO_INCREMENT PRIMARY KEY,
id:_cuidad INT(20),
id_pais INT(20),
id_ciudad INT(20),
linea_direccion1 VARCHAR(50),
linea_direccion2 VARCHAR(50)
);
```

tabla fecha

```sql
CREATE TABLE fecha (
id_fecha INT(20) AUTO_INCREMENT PRIMARY KEY,
fecha_pedido DATE,
fecha_esperada DATE,
fecha_entrega DATE
);
```

tabla pais

```sql
CREATE TABLE pais (
id_pais INT(50) AUTO_INCREMENT PRIMARY KEY,
nombre_pais VARCHAR(50)
);
```

tabla region 

```sql
CREATE TABLE region(
id_region INT(20) AUTO_INCREMENT PRIMARY KEY,
nombre_region VARCHAR(50)
);
```

tabla ciudad

```sql
CREATE TABLE ciudad (
id_ciudad INT(20) AUTO_INCREMENT PRIMARY KEY,
nombre_ciudad VARCHAR(50),
codigo_postal INT(8)
);
```















```sql
CREATE TABLE gama_producto(
    id_gama VARCHAR(20) PRIMARY KEY,
    descripcion_texto TEXT,
    descripcion_html TEXT,
    imagen VARCHAR(256)
);

CREATE TABLE producto(
    id_producto INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(70),
    id_gama VARCHAR(20),
    id_dimensiones INT(20),
    id_proveedor INT(20),
    descripcion TEXT,
    id_precio INT(20)
);

CREATE TABLE detalle_pedido(
    id_detalle INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_pedido INT(20),
    id_producto INT(20),
    cantidad INT(11),
    id_precio INT(20),
    numero_linea SMALLINT
);

CREATE TABLE pedido(
    id_pedido INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_fecha INT(20),
    id_cliente INT(20),
    estado VARCHAR(15),
    comentarios TEXT
);

CREATE TABLE oficina(
    id_oficina INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_ubicacion INT(20),
    id_contacto INT(20)
);

CREATE TABLE cliente(
    id_cliente INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_ubicacion INT(20),
    id_empleado INT(20),
    id_ultimo_pedido INT(20),
    limite_credito DECIMAL(15,2)
);

CREATE TABLE pago(
    id_pago INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT(20),
    id_fecha INT(20),
    monto_total DECIMAL(15,2),
    metodo_pago VARCHAR(50)
);

CREATE TABLE empleado(
    id_empleado INT(10) AUTO_INCREMENT PRIMARY KEY,
    id_jefe INT(20),
    id_oficina INT(20),
    puesto VARCHAR(50),
    id_contacto INT(20),
    id_persona INT(20)
);

CREATE TABLE stock(
    id_stock INT(20) AUTO_INCREMENT PRIMARY KEY,
    stock_actual INT(10),
    stock_maximo INT(10),
    stock_minimo INT(10)
);

CREATE TABLE dimensiones(
    id_dimensiones INT(20) AUTO_INCREMENT PRIMARY KEY,
    largo DECIMAL(15,2),
    ancho DECIMAL(15,2),
    peso DECIMAL(15,2)
);

CREATE TABLE precio(
    id_precio INT(20) AUTO_INCREMENT PRIMARY KEY,
    precio_compra DECIMAL(15,2),
    precio_venta DECIMAL(15,2)
);

CREATE TABLE proveedor(
    id_proveedor INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_persona INT(20),
    id_ubicacion INT(20)
);

CREATE TABLE persona (
    id_persona INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_contacto INT(20),
    tipo VARCHAR(50),
    nombre VARCHAR(50),
    apellido1 VARCHAR(50),
    apellido2 VARCHAR(50)
);

CREATE TABLE jefe(
    id_jefe INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_persona INT(20),
    id_oficina INT(20)
);

CREATE TABLE ubicacion (
    id_ubicacion INT(20) AUTO_INCREMENT PRIMARY KEY,
    id_ciudad INT(20),
    id_pais INT(20),
    linea_direccion1 VARCHAR(50),
    linea_direccion2 VARCHAR(50)
);

CREATE TABLE fecha (
    id_fecha INT(20) AUTO_INCREMENT PRIMARY KEY,
    fecha_pedido DATE,
    fecha_esperada_entrega DATE,
    fecha_real_entrega DATE
);

CREATE TABLE pais (
    id_pais INT(50) AUTO_INCREMENT PRIMARY KEY,
    nombre_pais VARCHAR(50)
);

CREATE TABLE region(
    id_region INT(20) AUTO_INCREMENT PRIMARY KEY,
    nombre_region VARCHAR(50)
);

CREATE TABLE ciudad (
    id_ciudad INT(20) AUTO_INCREMENT PRIMARY KEY,
    nombre_ciudad VARCHAR(50),
    codigo_postal VARCHAR(10)
);
CREATE TABLE contacto(
id_contacto INT(20) AUTO_INCREMENT PRIMARY KEY,
fax INT(10),
telefono INT(10),
email VARCHAR(50),
extencion INT(10)
);
```

query relacional

```
-- Relación entre producto y gama_producto
ALTER TABLE producto
ADD CONSTRAINT fk_producto_gama
FOREIGN KEY (id_gama)
REFERENCES gama_producto(id_gama);

-- Relación entre producto y dimensiones
ALTER TABLE producto
ADD CONSTRAINT fk_producto_dimensiones
FOREIGN KEY (id_dimensiones)
REFERENCES dimensiones(id_dimensiones);

-- Relación entre producto y proveedor
ALTER TABLE producto
ADD CONSTRAINT fk_producto_proveedor
FOREIGN KEY (id_proveedor)
REFERENCES proveedor(id_proveedor);

-- Relación entre detalle_pedido y pedido
ALTER TABLE detalle_pedido
ADD CONSTRAINT fk_detalle_pedido_pedido
FOREIGN KEY (id_pedido)
REFERENCES pedido(id_pedido);

-- Relación entre detalle_pedido y producto
ALTER TABLE detalle_pedido
ADD CONSTRAINT fk_detalle_pedido_producto
FOREIGN KEY (id_producto)
REFERENCES producto(id_producto);

-- Relación entre detalle_pedido y precio
ALTER TABLE detalle_pedido
ADD CONSTRAINT fk_detalle_pedido_precio
FOREIGN KEY (id_precio)
REFERENCES precio(id_precio);

-- Relación entre pedido y cliente
ALTER TABLE pedido
ADD CONSTRAINT fk_pedido_cliente
FOREIGN KEY (id_cliente)
REFERENCES cliente(id_cliente);

-- Relación entre oficina y ubicación
ALTER TABLE oficina
ADD CONSTRAINT fk_oficina_ubicacion
FOREIGN KEY (id_ubicacion)
REFERENCES ubicacion(id_ubicacion);

-- Relación entre cliente y empleado
ALTER TABLE cliente
ADD CONSTRAINT fk_cliente_empleado
FOREIGN KEY (id_empleado)
REFERENCES empleado(id_empleado);

-- Relación entre cliente y último pedido
ALTER TABLE cliente
ADD CONSTRAINT fk_cliente_ultimo_pedido
FOREIGN KEY (id_ultimo_pedido)
REFERENCES pedido(id_pedido);

-- Relación entre pago y cliente
ALTER TABLE pago
ADD CONSTRAINT fk_pago_cliente
FOREIGN KEY (id_cliente)
REFERENCES cliente(id_cliente);

-- Relación entre pago y fecha
ALTER TABLE pago
ADD CONSTRAINT fk_pago_fecha
FOREIGN KEY (id_fecha)
REFERENCES fecha(id_fecha);

-- Relación entre empleado y jefe
ALTER TABLE empleado
ADD CONSTRAINT fk_empleado_jefe
FOREIGN KEY (id_jefe)
REFERENCES jefe(id_jefe);

-- Relación entre empleado y oficina
ALTER TABLE empleado
ADD CONSTRAINT fk_empleado_oficina
FOREIGN KEY (id_oficina)
REFERENCES oficina(id_oficina);

-- Relación entre empleado y persona
ALTER TABLE empleado
ADD CONSTRAINT fk_empleado_persona
FOREIGN KEY (id_persona)
REFERENCES persona(id_persona);

-- Relación entre proveedor y persona
ALTER TABLE proveedor
ADD CONSTRAINT fk_proveedor_persona
FOREIGN KEY (id_persona)
REFERENCES persona(id_persona);

-- Relación entre proveedor y ubicación
ALTER TABLE proveedor
ADD CONSTRAINT fk_proveedor_ubicacion
FOREIGN KEY (id_ubicacion)
REFERENCES ubicacion(id_ubicacion);

-- Relación entre ubicación y ciudad
ALTER TABLE ubicacion
ADD CONSTRAINT fk_ubicacion_ciudad
FOREIGN KEY (id_ciudad)
REFERENCES ciudad(id_ciudad);

-- Relación entre ubicación y país
ALTER TABLE ubicacion
ADD CONSTRAINT fk_ubicacion_pais
FOREIGN KEY (id_pais)
REFERENCES pais(id_pais);

```



llenar datos 

```
-- Inserción de datos en la tabla gama_producto
INSERT INTO gama_producto (id_gama, descripcion_texto, descripcion_html, imagen)
VALUES 
('GP1', 'Gama 1 - Descripción de ejemplo', '<p>Gama 1 - Descripción de ejemplo</p>', 'imagen1.jpg'),
('GP2', 'Gama 2 - Descripción de ejemplo', '<p>Gama 2 - Descripción de ejemplo</p>', 'imagen2.jpg'),
('GP3', 'Gama 3 - Descripción de ejemplo', '<p>Gama 3 - Descripción de ejemplo</p>', 'imagen3.jpg');


-- Inserción de datos en la tabla detalle_pedido
INSERT INTO detalle_pedido (id_pedido, id_producto, cantidad, id_precio, numero_linea)
VALUES 
(1, 1, 5, 1, 1),
(2, 2, 3, 2, 2),
(3, 3, 2, 3, 3);

-- Inserción de datos en la tabla pedido
INSERT INTO pedido (id_fecha, id_cliente, estado, comentarios)
VALUES 
(1, 1, 'Pendiente', 'Comentario 1'),
(2, 2, 'En Proceso', 'Comentario 2'),
(3, 3, 'Entregado', 'Comentario 3');

-- Inserción de datos en la tabla oficina
INSERT INTO oficina (id_ubicacion, id_contacto)
VALUES 
(1, 1),
(2, 2),
(3, 3);

-- Inserción de datos en la tabla cliente
INSERT INTO cliente (id_ubicacion, id_empleado, id_ultimo_pedido, limite_credito)
VALUES 
(1, 1, 1, 1000.00),
(2, 2, 2, 1500.00),
(3, 3, 3, 2000.00);

-- Inserción de datos en la tabla pago
INSERT INTO pago (id_cliente, id_fecha, monto_total, metodo_pago)
VALUES 
(1, 1, 500.00, 'Tarjeta'),
(2, 2, 750.00, 'Transferencia'),
(3, 3, 1000.00, 'Efectivo');

-- Inserción de datos en la tabla empleado
INSERT INTO empleado (id_jefe, id_oficina, puesto, id_contacto, id_persona)
VALUES 
(1, 1, 'Gerente', 1, 1),
(2, 2, 'Vendedor', 2, 2),
(3, 3, 'Almacenero', 3, 3);

-- Inserción de datos en la tabla stock
INSERT INTO stock (stock_actual, stock_maximo, stock_minimo)
VALUES 
(100, 200, 50),
(150, 250, 75),
(200, 300, 100);


-- Inserción de datos en la tabla precio
INSERT INTO precio (precio_compra, precio_venta)
VALUES 
(50.00, 100.00),
(75.00, 150.00),
(100.00, 200.00);

-- Inserción de datos en la tabla proveedor
INSERT INTO proveedor (id_persona, id_ubicacion)
VALUES 
(1, 1),
(2, 2),
(3, 3);

-- Inserción de datos en la tabla persona
INSERT INTO persona (id_contacto, tipo, nombre, apellido1, apellido2)
VALUES 
(1, 'Empleado', 'Juan', 'Pérez', 'García'),
(2, 'Empleado', 'María', 'López', 'Martínez'),
(3, 'Empleado', 'Carlos', 'González', 'Sánchez');

-- Inserción de datos en la tabla jefe
INSERT INTO jefe (id_persona, id_oficina)
VALUES 
(1, 1),
(2, 2),
(3, 3);

-- Inserción de datos en la tabla ubicacion
INSERT INTO ubicacion (id_ciudad, id_pais, linea_direccion1, linea_direccion2)
VALUES 
(1, 1, 'Calle Principal 123', 'Piso 1'),
(2, 2, 'Avenida Central 456', 'Local 2'),
(3, 3, 'Plaza Mayor 789', 'Edificio A');

-- Inserción de datos en la tabla fecha
INSERT INTO fecha (fecha_pedido, fecha_esperada_entrega, fecha_real_entrega)
VALUES 
('2024-05-01', '2024-05-08', '2024-05-07'),
('2024-05-02', '2024-05-09', '2024-05-08'),
('2024-05-03', '2024-05-10', '2024-05-09');

-- Inserción de datos en la tabla pais
INSERT INTO pais (nombre_pais)
VALUES 
('España'),
('Francia'),
('Alemania');

-- Inserción de datos en la tabla region
INSERT INTO region (nombre_region)
VALUES 
('Norte'),
('Sur'),
('Este');

-- Inserción de datos en la tabla ciudad
INSERT INTO ciudad (nombre_ciudad, codigo_postal)
VALUES 
('Madrid', '28001'),
('París', '75001'),
('Berlín', '10115');

-- Insertar dimensiones primero
INSERT INTO dimensiones (largo, ancho, peso)
VALUES 
(10.0, 5.0, 2.0),
(15.0, 7.0, 3.0),
(20.0, 10.0, 4.0);

-- Insertar productos con referencias a las dimensiones existentes
INSERT INTO producto (nombre, id_gama, id_dimensiones, id_proveedor, descripcion, id_precio)
VALUES 
('Producto 1', 'GP1', 1, 1, 'Descripción del Producto 1', 1),
('Producto 2', 'GP2', 2, 2, 'Descripción del Producto 2', 2),
('Producto 3', 'GP3', 3, 3, 'Descripción del Producto 3', 3);

INSERT INTO contacto (fax, telefono, email, extension)
VALUES 
(123456789, 987654321, 'ejemplo1@example.com', 100),
(987654321, 123456789, 'ejemplo2@example.com', 200),
(555555555, 444444444, 'ejemplo3@example.com', 300);


```

```

```

