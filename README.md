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
