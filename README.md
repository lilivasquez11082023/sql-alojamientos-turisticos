# Gestión de Alojamientos Turísticos — Consultas SQL Avanzadas

Actividad evaluada de Bases de Datos: script SQL con 20 consultas CRUD y JOIN
funcionales sobre una base de datos de gestión de alojamientos turísticos.

## Motor de base de datos

**PostgreSQL** (probado en PostgreSQL 14+; compatible con pgAdmin, DBeaver o psql).

## Archivos del repositorio

| Archivo | Contenido |
|---|---|
| `01_schema_alojamientos_turisticos.sql` | Creación de la base de datos, las 6 tablas y los datos semilla (propietarios, alojamientos, huéspedes, reservas, pagos, reseñas). |
| `02_consultas_sql.sql` | Las 20 consultas SQL solicitadas: INSERT, SELECT, UPDATE, DELETE, INNER JOIN, LEFT JOIN, funciones de agregación (SUM, AVG, COUNT), GROUP BY / HAVING y subconsulta. |
| `capturas.pdf` | Evidencia en PDF con una captura de pantalla por cada una de las 20 consultas ejecutadas. |

## Esquema de la base de datos

La base `gestion_alojamientos` tiene 6 tablas relacionadas:

```
propietarios (1) ───< alojamientos (1) ───< reservas (1) ───< pagos
                            │                    │
                            │                    │
                            └──────< resenas >───┘
```

### Tablas

- **propietarios** — `id_propietario` (PK), nombre, apellido, email (único), teléfono, fecha_registro.
- **alojamientos** — `id_alojamiento` (PK), `id_propietario` (FK), nombre, descripción, tipo, dirección, ciudad, país, precio_noche, capacidad_personas, num_habitaciones, num_banos, activo.
- **huespedes** — `id_huesped` (PK), nombre, apellido, email (único), teléfono, nacionalidad.
- **reservas** — `id_reserva` (PK), `id_alojamiento` (FK), `id_huesped` (FK), fecha_entrada, fecha_salida, num_personas, precio_total, estado.
- **pagos** — `id_pago` (PK), `id_reserva` (FK), monto, metodo_pago, estado_pago.
- **resenas** — `id_resena` (PK), `id_alojamiento` (FK), `id_huesped` (FK), `id_reserva` (FK), calificacion (1-5), comentario.

Todas las claves foráneas usan `ON DELETE CASCADE`.

## Cómo ejecutar

```bash
psql -U postgres -f 01_schema_alojamientos_turisticos.sql
psql -U postgres -d gestion_alojamientos -f 02_consultas_sql.sql
```

O bien, en pgAdmin/DBeaver: abrir `01_schema_alojamientos_turisticos.sql`, ejecutarlo completo,
luego abrir `02_consultas_sql.sql` conectado a la base `gestion_alojamientos` y ejecutar
cada consulta por separado para capturar su resultado.

## Autor

_(Completar con tu nombre)_
