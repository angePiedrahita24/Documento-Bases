# Objetivo
- El objetivo de este proeycto es desarrollar una base de datos con consultad SQL para un sistema de ventas en las cafeterías de la Universidad Javeriana. Para lograr esto, se crearon distintas tablas las cuales están relacionadas con sus llaves primarias y foráneas (como edificios, pisos, cafeterías, colaboradores, metas de ventas, etc)

# Diseño entidad-relación
- Edificio: identificación, nombre
- Piso: identificación, numero, identificación del edificio
- Cafeteria: identificación, identificación del piso
- Colaborador: identificación, nombre, tipo de documento, vinculación, comisión
- Meta: identificación, identificación del colaborador, identificación de la cafetria, fecha meta, valor meta, valor real.

# Diseño relacional
- Edificio: id(PK)
