# Objetivo
- El objetivo de este proeycto es desarrollar una base de datos con consultad SQL para un sistema de ventas en las cafeterías de la Universidad Javeriana. Para lograr esto, se crearon distintas tablas las cuales están relacionadas con sus llaves primarias y foráneas (como edificios, pisos, cafeterías, colaboradores, metas de ventas, etc)

# Diseño entidad-atributos
- Edificio: identificación, nombre
- Piso: identificación, numero, identificación del edificio
- Cafeteria: identificación, identificación del piso
- Colaborador: identificación, nombre, tipo de documento, vinculación, comisión
- Meta: identificación, identificación del colaborador, identificación de la cafetria, fecha meta, valor meta, valor real.
Link modelo:

# Diseño relacional
- Edificio: id(PK), nombre
- Piso: id(PK), numeropiso, idEdificio (FK)
- Cafetería: id(PK), nombre, idPiso(FK)
- Colaborador: id(PK), tipodocumento, numerodocumento, nombre, vinculacion
- Meta: id(PK), idColaborador(FK), idCafeteria(FK), fechameta, valor_meta, valor_real
Link modelo:

# Creación tablas
- La tabla edificio es la encargada de la información básica de los edificios, id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita y el nombre corresponde al nombre del edificio el cual no puede ser nulo y es un valor único para que no hayan confusiones con edificios con el mismo nombre.
CREATE TABLE Edificio (
    id NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    nombre VARCHAR2(255) NOT NULL UNIQUE
);

- La tabla piso relaciona la jerarquia entre los pisos y los edificios mediante una llave foranea, el id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, numeropiso representa el número del piso el cual no puede ser nulo, idEdificio es una llave foránea de la tabla edificio que no puede ser nula y lo que hace el unique se encarga de que no existan dos pisos con el mismo número de edificio.
CREATE TABLE Piso (
    id NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    numeropiso NUMBER NOT NULL,
    idEdificio NUMBER NOT NULL,
    FOREIGN KEY (idEdificio) REFERENCES Edificio(id) ON DELETE CASCADE,
    UNIQUE (numeropiso, idEdificio)
);

- La tabla cafeteria guarda la información de las cafeterías y la ubicación de los pisos, el id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, el nombre corresponde al de la cafetería el cual no puede ser nullo y tiene que ser único y el idPiso es una llave foránea de la tabla piso. El on delete cascade sirve para eliminar las cafeterías en caso de que se elimine el piso asociado.
CREATE TABLE Cafeteria (
    id NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    nombre VARCHAR2(255) NOT NULL UNIQUE,
    idPiso NUMBER NOT NULL,
    FOREIGN KEY (idPiso) REFERENCES Piso(id) ON DELETE CASCADE
);

- La tabla colaborador guarda los datos de los colaboradores, el  id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, el tipodocumento y el numerodocumento deben tener un valor único, vinculacion permite y guarda los valores PLANTA o TEMPORAL y comision tiene un valor por defecto del 10% en un rango de 0 a 100.
CREATE TABLE Colaborador (
    id NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    tipodocumento VARCHAR2(255) NOT NULL,
    numerodocumento NUMBER NOT NULL,
    nombre VARCHAR2(255) NOT NULL,
    vinculacion VARCHAR2(255) CHECK (vinculacion IN ('PLANTA', 'TEMPORAL')) NOT NULL,
    comision NUMBER DEFAULT 10 CHECK (comision BETWEEN 0 AND 100),
    UNIQUE (tipodocumento, numerodocumento)
);

- La tabla meta guarda los objetivos y resultados de los colaboradores en las cafeterías, el  id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, idColaborador es una llave foránea de la tabla colaborador, en caso de que un colaborador se elimine, también se eliminará de las metas, idCafeteria es la llave foránea el cual no puede ser nulo, la fechameta asigna la meta, valor_meta y valor_real son los valores de la meta y los resultados obtenidos, el unique es una restricción para que no hayan duplicados en una fecha en específico.
CREATE TABLE Meta (
    id NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    idColaborador NUMBER NOT NULL,
    idCafeteria NUMBER NOT NULL,
    fechameta DATE NOT NULL,
    valor_meta NUMBER DEFAULT 0 NOT NULL,
    valor_real NUMBER DEFAULT 0 NOT NULL,
    FOREIGN KEY (idColaborador) REFERENCES Colaborador(id) ON DELETE CASCADE,
    FOREIGN KEY (idCafeteria) REFERENCES Cafeteria(id) ON DELETE CASCADE,
    UNIQUE (idColaborador, idCafeteria, fechameta)
);

# Inserción de Tuplas
- Inserción datos edificio: Se insertan los nombres de los edificios con sus respectivos ID.
INSERT INTO Edificio (id, nombre) VALUES (1,'Edificio Bar�n');
INSERT INTO Edificio (id, nombre) VALUES (2,'Edificio Giraldo');
INSERT INTO Edificio (id, nombre) VALUES (3,'Edificio Central');
INSERT INTO Edificio (id, nombre) VALUES (4,'Edificio Jos� del Carmen Acosta S.J.');
INSERT INTO Edificio (id, nombre) VALUES (5,'Edificio Fernando Bar�n S.J.');
INSERT INTO Edificio (id, nombre) VALUES (6,'Edificio Gabriel Giraldo S.J.');
INSERT INTO Edificio (id, nombre) VALUES (7,'Edificio Carlos Ort�z');
INSERT INTO Edificio (id, nombre) VALUES (8,'Edificio Manuel Brice�o S.J.');
INSERT INTO Edificio (id, nombre) VALUES (9,'Edificio Luis Carlos Gal�n Sarmiento');
INSERT INTO Edificio (id, nombre) VALUES (10,'Edificio Pedro Arrupe S.J.');
INSERT INTO Edificio (id, nombre) VALUES (11,'Edificio Jorge Hoyos V�squez S.J.');
INSERT INTO Edificio (id, nombre) VALUES (12,'Edificio Jos� Gabriel Maldonado S.J.');
INSERT INTO Edificio (id, nombre) VALUES (13,'Edificio F�lix Restrepo S.J.');

- Inserción datos alergias: Se insertan los números de piso y su referencia al edificio correspondiente.
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (1, 1, 1); -- Edificio Bar�n, Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (2, 1, 2); -- Edificio Giraldo, Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (3, 1, 3); -- Edificio Central, Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (4, 1, 4); -- Edificio Jos� del Carmen Acosta S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (5, 1, 5); -- Edificio Fernando Bar�n S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (6, 1, 6); -- Edificio Gabriel Giraldo S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (7, 1, 7); -- Edificio Carlos Ort�z, Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (8, 1, 8); -- Edificio Manuel Brice�o S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (9, 1, 9); -- Edificio Luis Carlos Gal�n Sarmiento, Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (10, 1, 10); -- Edificio Emilio Arango S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (11, 1, 11); -- Edificio Jorge Hoyos V�squez S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (12, 1, 12); -- Edificio Jos� Gabriel Maldonado S.J., Piso 1
INSERT INTO Piso (id, numeropiso, idEdificio) VALUES (13, 1, 13); -- Edificio F�lix Restrepo S.J., Piso 1

- Inserción datos cafetería: Se insertan los nombres de las cafeter�as y su referencia al piso correspondiente.
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (1, 'Cafeter�a Central', 3); -- Edificio Central, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (2, 'Cafeter�a Norte', 2); -- Edificio Giraldo, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (3, 'Cafeter�a Sur', 1); -- Edificio Bar�n, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (4, 'Cafeter�a Occidente', 4); -- Edificio Occidental, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (5, 'Cafeter�a Este', 7); -- Edificio Carlos Ort�z, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (6, 'Cafeter�a Las Palmas', 5); -- Edificio Fernando Bar�n S.J., Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (7, 'Cafeter�a El �gora', 9); -- Edificio Luis Carlos Gal�n Sarmiento, Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (8, 'Cafeter�a Los Almendros', 10); -- Edificio Emilio Arango S.J., Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (9, 'Cafeter�a Jard�n', 11); -- Edificio Jorge Hoyos V�squez S.J., Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (10, 'Cafeter�a K', 12); -- Edificio Jos� Gabriel Maldonado S.J., Piso 1
INSERT INTO Cafeteria (id, nombre, idPiso) VALUES (11, 'Cafeter�a O', 13); -- Edificio F�lix Restrepo S.J., Piso 1

Inserción datos colaborador: Se insertan los datos de los colaboradores, cada uno con su documento �nico.
INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (1, 'Laura Hern�ndez', 'CC', 1234567890, 'PLANTA', 10); -- Cafeter�a Central
INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (2, 'Carlos P�rez', 'CC', 9876543210, 'TEMPORAL', 12); -- Cafeter�a Central

INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (3, 'Mar�a G�mez', 'CC', 1122334455, 'PLANTA', 15); -- Cafeter�a Norte
INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (4, 'Juan Ram�rez', 'CC', 5566778899, 'TEMPORAL', 10); -- Cafeter�a Norte

INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (5, 'Ana Rodr�guez', 'CC', 9988776655, 'PLANTA', 8); -- Cafeter�a Sur
INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (6, 'Luis G�mez', 'CC', 5544332211, 'TEMPORAL', 10); -- Cafeter�a Sur

INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (7, 'Pedro Mart�nez', 'CC', 1122446688, 'PLANTA', 12); -- Cafeter�a Occidente
INSERT INTO Colaborador (id, nombre, tipodocumento, numerodocumento, vinculacion, comision) 
VALUES (8, 'Sof�a Torres', 'CC', 7788990011, 'TEMPORAL', 14); -- Cafeter�a Occidente

Inserción datos meta: Se insertan las metas para cada colaborador en su respectiva cafeter�a y fecha.
INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (1, 1, 1, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 500000, 450000); -- Meta para Laura Hern�ndez en Cafeter�a Central
INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (2, 2, 1, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 600000, 580000); -- Meta para Carlos P�rez en Cafeter�a Central

INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (3, 3, 2, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 550000, 530000); -- Meta para Mar�a G�mez en Cafeter�a Norte
INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (4, 4, 2, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 480000, 470000); -- Meta para Juan Ram�rez en Cafeter�a Norte

INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (5, 5, 3, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 600000, 590000); -- Meta para Ana Rodr�guez en Cafeter�a Sur
INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (6, 6, 3, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 450000, 440000); -- Meta para Luis G�mez en Cafeter�a Sur

INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (7, 7, 4, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 620000, 610000); -- Meta para Pedro Mart�nez en Cafeter�a Occidente
INSERT INTO Meta (id, idColaborador, idCafeteria, fechameta, valor_meta, valor_real) 
VALUES (8, 8, 4, TO_DATE('2024-08-26', 'YYYY-MM-DD'), 480000, 475000); -- Meta para Sof�a Torres en Cafeter�a Occidente

# Consultas solicitadas
![image](https://github.com/user-attachments/assets/2c8ee2d4-c8d5-415e-a947-a0a1a04b3366)

