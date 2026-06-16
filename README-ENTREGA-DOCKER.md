# Innovatech Solutions - Entrega Parcial 2 (Docker)

Este documento explica cómo levantar todo el ecosistema Innovatech usando Docker y docker-compose.

## Repositorios

- Frontend: https://github.com/RichardMoreano/innovatech-frontend.git
- BFF: https://github.com/RichardMoreano/innovatech-bff.git
- Backend: monorepo con los microservicios y gateway (este repositorio)

## Levantar con docker-compose

Desde la raíz del repositorio ejecutar:

```bash
docker compose up --build
```

Servicios y puertos aproximados:

- innovatech-api-gateway: 9000
- innovatech-bff: 8080
- ms-gestion-proyectos: 8081
- ms-gestion-recursos: 8082
- ms-autenticacion: 8083
- ms-monitoreo-analitica: 8084
- frontend: 5173 (servido por nginx en el contenedor)

