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
