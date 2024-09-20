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

![image](https://github.com/user-attachments/assets/feb441dc-8d57-45a8-84b5-542cc2bfc576)

- La tabla piso relaciona la jerarquia entre los pisos y los edificios mediante una llave foranea, el id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, numeropiso representa el número del piso el cual no puede ser nulo, idEdificio es una llave foránea de la tabla edificio que no puede ser nula y lo que hace el unique se encarga de que no existan dos pisos con el mismo número de edificio.

![image](https://github.com/user-attachments/assets/89dea13a-9422-4a35-9310-ba2b624c83ba)

- La tabla cafeteria guarda la información de las cafeterías y la ubicación de los pisos, el id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, el nombre corresponde al de la cafetería el cual no puede ser nullo y tiene que ser único y el idPiso es una llave foránea de la tabla piso. El on delete cascade sirve para eliminar las cafeterías en caso de que se elimine el piso asociado.

![image](https://github.com/user-attachments/assets/c38a5c31-70a9-4307-bdef-f023d78ea765)

- La tabla colaborador guarda los datos de los colaboradores, el  id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, el tipodocumento y el numerodocumento deben tener un valor único, vinculacion permite y guarda los valores PLANTA o TEMPORAL y comision tiene un valor por defecto del 10% en un rango de 0 a 100.
![image](https://github.com/user-attachments/assets/21116fb0-ddc3-493e-9323-2c00451ebefb)

- La tabla meta guarda los objetivos y resultados de los colaboradores en las cafeterías, el  id es la llave primaria generada automaticamente por identity para crear un identificador que no se repita, idColaborador es una llave foránea de la tabla colaborador, en caso de que un colaborador se elimine, también se eliminará de las metas, idCafeteria es la llave foránea el cual no puede ser nulo, la fechameta asigna la meta, valor_meta y valor_real son los valores de la meta y los resultados obtenidos, el unique es una restricción para que no hayan duplicados en una fecha en específico.
![image](https://github.com/user-attachments/assets/ed0a9c96-6721-46b7-8048-e61c5561bc34)

# Inserción de Tuplas
- Inserción datos edificio: Se insertan los nombres de los edificios con sus respectivos ID.
![image](https://github.com/user-attachments/assets/ac63366a-cbb8-4590-952b-28aa7bb42abf)

- Inserción datos alergias: Se insertan los números de piso y su referencia al edificio correspondiente.
![image](https://github.com/user-attachments/assets/78721e45-6f97-4d39-8770-12ad7fd7af41)

- Inserción datos cafetería: Se insertan los nombres de las cafeter�as y su referencia al piso correspondiente.
![image](https://github.com/user-attachments/assets/ef6c8e10-141a-4a9e-a165-161d3bf2270c)

Inserción datos colaborador: Se insertan los datos de los colaboradores, cada uno con su documento único.
![image](https://github.com/user-attachments/assets/1eadbf90-7bfb-422d-a2ab-19b8c2d9b6f6)

Inserción datos meta: Se insertan las metas para cada colaborador en su respectiva cafeter�a y fecha.
![image](https://github.com/user-attachments/assets/7cb2000d-7756-4754-8ca9-b86b05053dca)

# Consultas solicitadas
- Proporciona un listado detallado de colaboradores, cafeterías, metas y el porcentaje de diferencia entre el valor real y la meta establecida. Esta vista es fundamental para el análisis de rendimiento de los colaboradores en cada cafetería y su impacto frente a las metas asignadas:
![image](https://github.com/user-attachments/assets/2c8ee2d4-c8d5-415e-a947-a0a1a04b3366)

- Muestra el total de ventas por cafetería, incluyendo las que no tienen ventas:
![image](https://github.com/user-attachments/assets/8a0c28c3-27b3-43f6-a441-643469369fd2)

- Determina cuánto debe pagarse a cada colaborador mensualmente según las ventas y su comisión , permitiendo ver el pago mensual por colaborador y el total general de pagos a realizar:

![image](https://github.com/user-attachments/assets/096bad2f-4b2d-460b-bd87-af485c25f3b2)

- Calcula los totales de metas y ventas reales por mes y año, incluyendo la diferencia entre ambas y  observa la evolución de las metas frente a las ventas reales y evaluar si se cumplieron los objetivos a lo largo del tiempo:
![image](https://github.com/user-attachments/assets/63773527-33dd-4ba5-a2e4-f54c517fb803)

- Muestra el porcentaje de participación de cada colaborador en relación al total de ventas de todas las cafeterías:
![image](https://github.com/user-attachments/assets/85101aa3-a90e-490f-bfac-d58b4f6260b3)

- Identifica a los colaboradores que tienen metas asignadas en todas las cafeterías:
![image](https://github.com/user-attachments/assets/412a7c85-2476-460b-ac7d-af934d4d18fd)

- Muestra la cantidad de colaboradores de planta y temporales por edificio, junto con un total general:
![image](https://github.com/user-attachments/assets/14e02d71-67eb-4774-98b2-356f6e0d665d)
