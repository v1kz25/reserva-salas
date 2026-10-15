# Changelog

Todos los cambios relevantes del contrato de la API (`contrato/openapi.yaml`) se documentan en este fichero.

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y el proyecto usa [Versionado Semántico](https://semver.org/lang/es/).

## [0.1.0] - 2026-10-15

### Añadido

- Contrato inicial de la API, con errores en formato `ProblemDetail`:
  - Salas: listar, consultar, crear, modificar y eliminar (`/api/salas`). `409` si el nombre está repetido o si se elimina una sala con reservas futuras.
  - Reservas: listar, crear, consultar y cancelar (`/api/reservas`). `409` si la reserva se solapa con otra de la misma sala.
- Filtro de reservas por sala y por rango de fechas (`fechaDesde`, `fechaHasta`); las reservas solo se admiten a partir de mañana (#2).

[0.1.0]: https://github.com/v1kz25/reserva-salas/releases/tag/v0.1.0
