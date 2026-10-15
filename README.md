# reserva-salas

Aplicación web para reservar salas de reuniones: gestión de salas y reservas sin solapamientos.

Este repositorio es el punto de entrada del proyecto. Contiene el **contrato de la API** que comparten backend y frontend; el código de cada parte vive en su propio repositorio.

## Repositorios

| Repo | Contenido | Stack |
|---|---|---|
| [`reserva-salas`](https://github.com/v1kz25/reserva-salas) | Contrato de la API (`contrato/openapi.yaml`) y documentación | OpenAPI 3.1 |
| [`reserva-salas-back`](https://github.com/v1kz25/reserva-salas-back) | API REST | Java 21, Spring Boot 4, H2 |
| [`reserva-salas-front`](https://github.com/v1kz25/reserva-salas-front) | Aplicación web | Angular 19 |

## Dominio

- **Sala**: nombre, capacidad y planta.
- **Reserva**: sala, fecha, hora de inicio, hora de fin, responsable y motivo.
- Reglas:
  - No puede haber reservas solapadas en la misma sala.
  - La hora de fin debe ser posterior a la de inicio.
  - No se puede reservar en el pasado.

## Puesta en marcha

Clona los tres repositorios con esta estructura. `back/` y `front/` están ignorados en este repo:

```bash
git clone https://github.com/v1kz25/reserva-salas.git
cd reserva-salas
git clone https://github.com/v1kz25/reserva-salas-back.git back
git clone https://github.com/v1kz25/reserva-salas-front.git front
```

Arranque en local:

```bash
# Backend: http://localhost:8080
cd back && ./mvnw spring-boot:run -Dspring-boot.run.profiles=dev

# Frontend: http://localhost:4200 (redirige /api al backend)
cd front && npm ci && npm start
```

Requisitos: JDK 21, Node LTS y Chrome o Chromium para los tests del frontend.

## Contrato de la API

`contrato/openapi.yaml` es la fuente de verdad de la API. Cualquier cambio en los endpoints empieza actualizando el contrato; después se implementa en el backend y en el frontend.

## Flujo de trabajo

Los tres repos siguen Git Flow:

- `develop` es la rama de integración y la rama por defecto.
- `main` solo recibe releases (`release/X.Y.Z`) y hotfixes. Cada merge a `main` lleva un tag `vX.Y.Z`.
- Cada funcionalidad se desarrolla en una rama `feature/<n>-<slug>` a partir de una issue y entra en `develop` por PR con squash.
- Commits con [Conventional Commits](https://www.conventionalcommits.org/) y versionado [SemVer](https://semver.org/).

Flujo de una funcionalidad:

1. Crear la issue en el repo afectado (una en back y otra en front si afecta a ambos, enlazadas entre sí).
2. Si cambia la API, actualizar el contrato.
3. Implementar backend y frontend en paralelo a partir del contrato.
4. Revisar el código y añadir tests.
5. Abrir la PR a `develop`. El CI tiene que pasar para poder fusionarla.

## Licencia

[MIT](LICENSE)
