# Parte B: Reservaciones de restaurante

Asignación 1 - Mapeo de dominios a Prisma. MySQL 8 y Prisma 6.19.0.

## Modelo

- `Cliente`: nombre, teléfono y correo único.
- `Mesa`: número único y capacidad.
- `Turno`: nombre, hora de inicio y hora de fin, almacenadas como `TIME(0)`.
- `Reservacion`: fecha (`DATE`), estado y relaciones obligatorias con cliente, mesa y turno.

Relaciones: Cliente 1:N Reservacion, Mesa 1:N Reservacion y Turno 1:N Reservacion. El enum `EstadoReservacion` admite `confirmada`, `cancelada` y `completada`.

## Respuesta

**¿Por qué esa combinación única evita reservar la misma mesa dos veces en el mismo turno?**

`@@unique([mesaId, turnoId])` genera el índice único compuesto `Reservacion_mesaId_turnoId_key`. MySQL rechaza insertar o modificar una reservación si otra fila ya tiene los mismos valores de mesa y turno. Por ejemplo, si existe `(mesaId=1, turnoId=2)`, no se admite otra fila con `(1,2)`, aunque el cliente sea diferente. Sí pueden existir `(1,3)` o `(2,2)` si sus relaciones son válidas.

La fecha y el estado no participan en esa restricción: también se bloquea la combinación en fechas distintas o cuando la reservación anterior está cancelada. Se conserva exactamente lo solicitado por la tarea. En un sistema que permitiera reutilizar mesas cada día, se podría definir `@@unique([mesaId, turnoId, fecha])` y diseñar aparte la política de cancelaciones.

## Comprobación en MySQL Workbench

Después de aplicar la migración, ejecutar:

```sql
USE asignacion01_restaurante_00000252274;
SHOW TABLES;
SHOW CREATE TABLE Reservacion;
```

Deben aparecer las cuatro tablas del dominio: `Cliente`, `Mesa`, `Turno` y `Reservacion`. Prisma también crea la tabla técnica `_prisma_migrations`.
