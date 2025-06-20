# tabla_mecanica
usuario:
alter session set "_ORACLE_SCRIPT"=true;

-- USER SQL
CREATE USER adm_taller IDENTIFIED BY 123456
DEFAULT TABLESPACE "USERS"
TEMPORARY TABLESPACE "TEMP";

-- QUOTAS
ALTER USER adm_taller QUOTA UNLIMITED ON "USERS";

-- ROLES
GRANT "CONNECT" TO adm_taller;
GRANT "RESOURCE" TO adm_taller;
ALTER USER adm_taller DEFAULT ROLE "CONNECT","RESOURCE";

CREATE TABLE adm_taller.cliente
(
    id_cliente   NUMBER(6) PRIMARY KEY,
    nom_cliente  VARCHAR2(30 CHAR),
    rut   NUMBER(9) UNIQUE,
    telefono_cliente NUMBER(12),
    email VARCHAR2(30 CHAR),
    direccion VARCHAR2(30 CHAR)
);

alter table cliente MODIFY (nom_cliente VARCHAR2 (100 CHAR) NOT NULL, 
rut VARCHAR2 (12 CHAR)  NOT NULL,
telefono_cliente VARCHAR2 (15 CHAR),
email VARCHAR2 (100 CHAR),
direccion VARCHAR2 (200 CHAR))

CREATE TABLE marca
(
    id_marca   NUMBER(10) PRIMARY KEY,
    nom_marca  VARCHAR2(50 CHAR) UNIQUE
);

CREATE TABLE modelo
(
    id_modelo   NUMBER(10) PRIMARY KEY,
    nom_modelo  VARCHAR2(50 CHAR),
    id_marca NUMBER(10),
    CONSTRAINT fk_modelo_marca FOREIGN KEY (id_marca) REFERENCES marca(id_marca)
);








//tabla cliente
CREATE TABLE cliente
(
    id_cliente NUMBER(10) PRIMARY KEY,
    nombre VARCHAR2(100 CHAR) NOT NULL,
    rut VARCHAR2(12 CHAR) UNIQUE,
    telefono  VARCHAR2(15 CHAR),
    email  VARCHAR2(100 CHAR),
    direccion  VARCHAR2(200 CHAR)
);

//tabla marca
CREATE TABLE marca
(
    id_marca NUMBER(10) PRIMARY KEY,
    nombre VARCHAR2(50 CHAR) UNIQUE
);

//tabla servicio
CREATE TABLE servicio
(
    id_servicio NUMBER(10) PRIMARY KEY,
    nombre_servicio VARCHAR2(100 CHAR) NOT NULL,
    descripcion CLOB,
    costo_estimado NUMBER(10,2)
);

// tabla especialidad
CREATE TABLE especialidad
(
    id_especialidad NUMBER(10) PRIMARY KEY,
    nombre VARCHAR2(100 CHAR) UNIQUE
);

//tabla modelo
CREATE TABLE modelo
(
    id_modelo NUMBER(10) PRIMARY KEY,
    nombre VARCHAR2(50 CHAR) NOT NULL,
    id_marca NUMBER(10),
    CONSTRAINT fk_modelo_marca FOREIGN KEY (id_marca) REFERENCES marca(id_marca)
);

//tabla vehiculo
CREATE TABLE vehiculo
(
    id_vehiculo NUMBER(10) PRIMARY KEY,
    patente VARCHAR2(10 CHAR) UNIQUE,
    anio NUMBER(4),
    id_cliente NUMBER(10),
    CONSTRAINT fk_vehiculo_cliente FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente),
    id_modelo NUMBER(10),
    CONSTRAINT fk_vehiculo_modelo FOREIGN KEY (id_modelo) REFERENCES modelo(id_modelo)
);

//tabla ordentrabajo
CREATE TABLE ordentrabajo
(
    id_orden NUMBER(10) PRIMARY KEY,
    id_vehiculo NUMBER(10),
    fecha_ingreso DATE NOT NULL,
    fecha_salida DATE,
    estado VARCHAR2(20 CHAR),
    observaciones CLOB,
    CONSTRAINT fk_ordentrabajo_vehiculo FOREIGN KEY (id_vehiculo) REFERENCES vehiculo(id_vehiculo)
);

//tabla mecanico_especialidad
CREATE TABLE mecanicoespecialidad
(
    id_mecanico NUMBER(10),
    id_especialidad NUMBER(10),
    CONSTRAINT pk_mecanicoespecialidad PRIMARY KEY (id_mecanico),
    CONSTRAINT fk_mecanicoespecialidad_especialidad FOREIGN KEY (id_especialidad) REFERENCES especialidad(id_especialidad),
    CONSTRAINT fk_mecanicoespecialidad_mecanico FOREIGN KEY (id_mecanico) REFERENCES mecanico(id_mecanico)
);

//tabla mecanico
CREATE TABLE mecanico
(
    id_mecanico NUMBER(10), PRIMARY KEY,
    nombre VARCHAR2(100 CHAR) NOT NULL,
    rut VARCHAR2(12 CHAR) UNIQUE
);

//tabla detalleservicio
CREATE TABLE detalleservicio
(
    id_detalle NUMBER(10) PRIMARY KEY,
    id_orden NUMBER(10),
    id_servicio NUMBER(10),
    id_mecanico NUMBER(10),
    fecha_servicio DATE,
    costo_final NUMBER(10,2),
    CONSTRAINT fk_detalleservicio_ordentrabajo FOREIGN KEY (id_orden) REFERENCES ordentrabajo(id_orden),
    CONSTRAINT fk_detalleservicio_servicio FOREIGN KEY (id_servicio) REFERENCES servicio(id_servicio),
    CONSTRAINT fk_detalleservicio_mecanico FOREIGN KEY (id_mecanico) REFERENCES mecanico(id_mecanico)
);










MODIFICACION
//tabla cliente 
CREATE TABLE cliente 
( 
    id_cliente NUMBER(10) PRIMARY KEY, 
    nombre VARCHAR2(100 CHAR) NOT NULL, 
    rut VARCHAR2(12 CHAR) UNIQUE, 
    telefono VARCHAR2(15 CHAR), 
    email VARCHAR2(100 CHAR), 
    direccion VARCHAR2(200 CHAR) 
);

//tabla marca 
CREATE TABLE marca 
( 
    id_marca NUMBER(10) PRIMARY KEY, 
    nombre VARCHAR2(50 CHAR) UNIQUE 
);

//tabla servicio 
CREATE TABLE servicio 
( 
    id_servicio NUMBER(10) PRIMARY KEY, 
    nombre_servicio VARCHAR2(100 CHAR) NOT NULL, 
    descripcion CLOB, 
    costo_estimado NUMBER(10,2) 
);

// tabla especialidad 
CREATE TABLE especialidad 
( 
    id_especialidad NUMBER(10) PRIMARY KEY, 
    nombre VARCHAR2(100 CHAR) UNIQUE 
);

//tabla modelo 
CREATE TABLE modelo 
( 
    id_modelo NUMBER(10) PRIMARY KEY, 
    nombre VARCHAR2(50 CHAR) NOT NULL, 
    id_marca NUMBER(10), 
    CONSTRAINT fk_modelo_marca FOREIGN KEY (id_marca) REFERENCES marca(id_marca) 
);

//tabla vehiculo 
CREATE TABLE vehiculo 
( 
    id_vehiculo NUMBER(10) PRIMARY KEY, 
    patente VARCHAR2(10 CHAR) UNIQUE, 
    anio NUMBER(4), 
    id_cliente NUMBER(10), 
    CONSTRAINT fk_vehiculo_cliente FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente), 
    id_modelo NUMBER(10), 
    CONSTRAINT fk_vehiculo_modelo FOREIGN KEY (id_modelo) REFERENCES modelo(id_modelo) 
);

//tabla ordentrabajo 
CREATE TABLE ordentrabajo 
( 
    id_orden NUMBER(10) PRIMARY KEY, 
    id_vehiculo NUMBER(10), 
    fecha_ingreso DATE NOT NULL, 
    fecha_salida DATE, 
    estado VARCHAR2(20 CHAR), 
    observaciones CLOB, 
    CONSTRAINT fk_ordentrabajo_vehiculo FOREIGN KEY (id_vehiculo) REFERENCES vehiculo(id_vehiculo) 
);

//tabla mecanico_especialidad 
CREATE TABLE mecanicoespecialidad 
( 
    id_mecanico NUMBER(10), 
    id_especialidad NUMBER(10), 
    CONSTRAINT pk_mecanicoespecialidad PRIMARY KEY (id_mecanico), 
    CONSTRAINT fk_mecanicoespecialidad_especialidad FOREIGN KEY (id_especialidad) REFERENCES especialidad(id_especialidad), 
    CONSTRAINT fk_mecanicoespecialidad_mecanico FOREIGN KEY (id_mecanico) REFERENCES mecanico(id_mecanico) 
);

//tabla mecanico 
CREATE TABLE mecanico
(
    id_mecanico NUMBER(10) PRIMARY KEY,
    nombre VARCHAR2(100 CHAR) NOT NULL,
    rut VARCHAR2(12 CHAR) UNIQUE
);

//tabla detalleservicio 
CREATE TABLE detalleservicio 
( 
    id_detalle NUMBER(10) PRIMARY KEY, 
    id_orden NUMBER(10), 
    id_servicio NUMBER(10), 
    id_mecanico NUMBER(10), 
    fecha_servicio DATE, 
    costo_final NUMBER(10,2), 
    CONSTRAINT fk_detalleservicio_ordentrabajo FOREIGN KEY (id_orden) REFERENCES ordentrabajo(id_orden), 
    CONSTRAINT fk_detalleservicio_servicio FOREIGN KEY (id_servicio) REFERENCES servicio(id_servicio), 
    CONSTRAINT fk_detalleservicio_mecanico FOREIGN KEY (id_mecanico) REFERENCES mecanico(id_mecanico) 
);

//Insertar datos:

//Datos Clientes
INSERT INTO cliente VALUES (11111, 'Juan', '22.345.678-0', '987654321', 'juan@gmail.com', 'santa cruz #30 maipu');
INSERT INTO cliente VALUES (11112, 'Pedro', '12.098.765-1', '912345678', 'pedro@gmail.com', 'san fernando #987 maipu');
INSERT INTO cliente VALUES (11113, 'Diego', '10.567.987-2', '983746574', 'diego@gmail.com', 'santiago #34517 maipu');
INSERT INTO cliente VALUES (11114, 'Luis', '19.987.123-6', '984351987', 'luis@gmail.com', 'san miguel #342 maipu');
INSERT INTO cliente VALUES (11115, 'Tomas', '21.876.123-4', '965412354', 'tomas@gmail.com', 'san antonio #222 maipu');


//Datos Marca
INSERT INTO marca (id_marca, nombre) VALUES (1, 'Samsung');
INSERT INTO marca (id_marca, nombre) VALUES (2, 'Apple');
INSERT INTO marca (id_marca, nombre) VALUES (3, 'Sony');
INSERT INTO marca (id_marca, nombre) VALUES (4, 'Huawei');
INSERT INTO marca (id_marca, nombre) VALUES (5, 'Xiaomi');


//Datos Servicio
INSERT INTO servicio (id_servicio, nombre_servicio, descripcion, costo_estimado) VALUES (1, 'Revisión y Diagnóstico', 'Servicio completo de revisión para identificar problemas y diagnosticar fallas en equipos electrónicos o vehículos.', 50.00);
INSERT INTO servicio (id_servicio, nombre_servicio, descripcion, costo_estimado) VALUES (2, 'Mantenimiento Preventivo', 'Rutina de mantenimiento diseñada para prevenir futuras averías y prolongar la vida útil de los sistemas.', 120.50);
INSERT INTO servicio (id_servicio, nombre_servicio, descripcion, costo_estimado) VALUES (3, 'Reparación de Software', 'Servicio especializado en la corrección de errores de software, reinstalación de sistemas operativos y eliminación de virus.', 85.75);
INSERT INTO servicio (id_servicio, nombre_servicio, descripcion, costo_estimado) VALUES (4, 'Instalación de Componentes', 'Instalación de hardware o software, incluyendo configuración inicial y pruebas de funcionamiento.', 70.00);
INSERT INTO servicio (id_servicio, nombre_servicio, descripcion, costo_estimado) VALUES (5, 'Asesoría Técnica Remota', 'Soporte técnico y consultoría a distancia para resolver problemas menores y proporcionar orientación.', 35.00);


//Datos Especialidad
INSERT INTO especialidad (id_especialidad, nombre) VALUES (1, 'Electrónica de Consumo');
INSERT INTO especialidad (id_especialidad, nombre) VALUES (2, 'Telefonía Móvil');
INSERT INTO especialidad (id_especialidad, nombre) VALUES (3, 'Informática y Redes');
INSERT INTO especialidad (id_especialidad, nombre) VALUES (4, 'Reparación de Electrodomésticos');
INSERT INTO especialidad (id_especialidad, nombre) VALUES (5, 'Soporte de Software');


//Datos Modelo
INSERT INTO modelo (id_modelo, nombre, id_marca) VALUES (101, 'Galaxy S23', 1); 
INSERT INTO modelo (id_modelo, nombre, id_marca) VALUES (102, 'iPhone 15 Pro', 2); 
INSERT INTO modelo (id_modelo, nombre, id_marca) VALUES (103, 'Bravia XR A80K', 3); 
INSERT INTO modelo (id_modelo, nombre, id_marca) VALUES (104, 'MateBook X Pro', 4);
INSERT INTO modelo (id_modelo, nombre, id_marca) VALUES (105, 'Redmi Note 12', 5); 


//Datos Vehoculo
INSERT INTO vehiculo (id_vehiculo, patente, anio, id_cliente, id_modelo) VALUES (1, 'ABCD-12', 2020, 11111, 101); 
INSERT INTO vehiculo (id_vehiculo, patente, anio, id_cliente, id_modelo) VALUES (2, 'EFGH-34', 2022, 11112, 102); 
INSERT INTO vehiculo (id_vehiculo, patente, anio, id_cliente, id_modelo) VALUES (3, 'IJKL-56', 2019, 11113, 103); 
INSERT INTO vehiculo (id_vehiculo, patente, anio, id_cliente, id_modelo) VALUES (4, 'MNÑO-78', 2021, 11114, 104); 
INSERT INTO vehiculo (id_vehiculo, patente, anio, id_cliente, id_modelo) VALUES (5, 'PQRS-90', 2023, 11111, 105); 


//Datos Ordentrabajo
INSERT INTO ordentrabajo (id_orden, id_vehiculo, fecha_ingreso, fecha_salida, estado, observaciones) VALUES (1, 1, TO_DATE('2024-05-10', 'YYYY-MM-DD'), TO_DATE('2024-05-15', 'YYYY-MM-DD'), 'Completado', 'Revisión general y reemplazo de batería. Dispositivo en óptimas condiciones.');
INSERT INTO ordentrabajo (id_orden, id_vehiculo, fecha_ingreso, fecha_salida, estado, observaciones) VALUES (2, 2, TO_DATE('2024-06-01', 'YYYY-MM-DD'), NULL, 'En Proceso', 'Pantalla rota, se está esperando el repuesto original.');
INSERT INTO ordentrabajo (id_orden, id_vehiculo, fecha_ingreso, fecha_salida, estado, observaciones) VALUES (3, 3, TO_DATE('2024-06-15', 'YYYY-MM-DD'), TO_DATE('2024-06-18', 'YYYY-MM-DD'), 'Completado', 'Actualización de firmware y limpieza interna. Mejora en el rendimiento.');
INSERT INTO ordentrabajo (id_orden, id_vehiculo, fecha_ingreso, fecha_salida, estado, observaciones) VALUES (4, 4, TO_DATE('2024-06-19', 'YYYY-MM-DD'), NULL, 'Pendiente', 'Problemas con la carga, se requiere diagnóstico eléctrico.');
INSERT INTO ordentrabajo (id_orden, id_vehiculo, fecha_ingreso, fecha_salida, estado, observaciones) VALUES (5, 5, TO_DATE('2024-05-20', 'YYYY-MM-DD'), TO_DATE('2024-05-22', 'YYYY-MM-DD'), 'Completado', 'Optimización de software y eliminación de aplicaciones no deseadas.');


//Datos Mecanico
INSERT INTO mecanico (id_mecanico, nombre, rut) VALUES (1, 'Carlos Ramirez', '15.123.456-7');
INSERT INTO mecanico (id_mecanico, nombre, rut) VALUES (2, 'Maria Soto', '16.987.654-3');
INSERT INTO mecanico (id_mecanico, nombre, rut) VALUES (3, 'Juan Perez', '17.345.876-K');
INSERT INTO mecanico (id_mecanico, nombre, rut) VALUES (4, 'Ana Diaz', '18.765.432-1');
INSERT INTO mecanico (id_mecanico, nombre, rut) VALUES (5, 'Roberto Vega', '19.012.345-9');


//Datos Mecanicoespecialidad
INSERT INTO mecanicoespecialidad (id_mecanico, id_especialidad) VALUES (1, 1);
INSERT INTO mecanicoespecialidad (id_mecanico, id_especialidad) VALUES (2, 2);
INSERT INTO mecanicoespecialidad (id_mecanico, id_especialidad) VALUES (3, 3);
INSERT INTO mecanicoespecialidad (id_mecanico, id_especialidad) VALUES (4, 4);
INSERT INTO mecanicoespecialidad (id_mecanico, id_especialidad) VALUES (5, 5);


//Datos detalleservivio
INSERT INTO detalleservicio (id_detalle, id_orden, id_servicio, id_mecanico, fecha_servicio, costo_final) VALUES (1, 1, 1, 1, TO_DATE('2024-05-10', 'YYYY-MM-DD'), 50.00);
INSERT INTO detalleservicio (id_detalle, id_orden, id_servicio, id_mecanico, fecha_servicio, costo_final) VALUES (2, 5, 5, 5, TO_DATE('2024-05-19', 'YYYY-MM-DD'), 345.00);
INSERT INTO detalleservicio (id_detalle, id_orden, id_servicio, id_mecanico, fecha_servicio, costo_final) VALUES (3, 3, 2, 3, TO_DATE('2024-06-16', 'YYYY-MM-DD'), 120.50);
INSERT INTO detalleservicio (id_detalle, id_orden, id_servicio, id_mecanico, fecha_servicio, costo_final) VALUES (4, 4, 1, 4, TO_DATE('2024-06-19', 'YYYY-MM-DD'), 55.00);
INSERT INTO detalleservicio (id_detalle, id_orden, id_servicio, id_mecanico, fecha_servicio, costo_final) VALUES (5, 5, 5, 5, TO_DATE('2024-05-21', 'YYYY-MM-DD'), 35.00);




//Actualizar tabla mecanicoespecialidad

UPDATE mecanicoespecialidad
    SET id_especialidad = 2
    WHERE id_mecanico = 1;

UPDATE mecanicoespecialidad
    SET id_especialidad = 4
    WHERE id_mecanico = 2;

UPDATE mecanicoespecialidad
    SET id_especialidad = 1
    WHERE id_mecanico = 3;
    

//Actualizar tabla cliente
UPDATE cliente
    SET telefono = '912345678',
        email = 'juan.nuevo@example.com'
    WHERE id_cliente = 11111;

UPDATE cliente
    SET direccion = 'Av. Libertador #555, Las Condes'
    WHERE id_cliente = 11112;

UPDATE cliente
    SET nombre = 'Diego Armijo',
        rut = '20.123.456-0' 
    WHERE id_cliente = 11113;
    
//Actualizar tabla modelo
UPDATE modelo
    SET nombre = 'Galaxy S24 Ultra'
    WHERE id_modelo = 101;

UPDATE modelo
    SET id_marca = 5 
    WHERE id_modelo = 102;

UPDATE modelo
    SET nombre = 'Bravia OLED A95L',
        id_marca = 1 
    WHERE id_modelo = 103;




//Cambios en tabla cliente
//columna nombre
ALTER TABLE cliente
RENAME COLUMN nombre TO nombre_cliente;

//Cambios en tabla especialidad
//Columna nombre
ALTER TABLE especialidad
RENAME COLUMN nombre TO nombre_especialidad;

//Cambios en tabla vehiculo
//Columna anio
ALTER TABLE vehiculo
RENAME COLUMN anio TO año_fabricacion;





//Cambiar tipos de datos en tabla cliente
//aumentar el tamaño del email
ALTER TABLE cliente
MODIFY (email VARCHAR2(150 CHAR)); 

//Cambiar tipos de datos en la tabla detalleservivio
//modificar costo final
ALTER TABLE detalleservicio
MODIFY (costo_final NUMBER(12,2));

//cambiar tipo de datos en la tabla vehiculo
//modificar patente
ALTER TABLE vehiculo
MODIFY (patente VARCHAR2(15 CHAR));




//Agregar restricion CHECK a costo_estimado en la tabla servicio
ALTER TABLE servicio
ADD CONSTRAINT chk_costo_positivo CHECK (costo_estimado >= 0);





//Borrar fila en tabla marca
