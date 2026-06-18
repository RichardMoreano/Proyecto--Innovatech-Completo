# Innovatech Solutions - Plataforma Integral de Gestión y Monitoreo

Este repositorio actúa como el orquestador central del ecosistema distribuido **Innovatech Solutions**. Utiliza Docker Compose para configurar, enlazar y desplegar la infraestructura completa que abarca la interfaz de usuario, la capa intermedia de agregación (BFF), una puerta de entrada unificada (API Gateway), los microservicios del núcleo operativo y la persistencia de datos.

## Arquitectura del Ecosistema

El sistema implementa una arquitectura orientada a microservicios con persistencia compartida en una base de datos relacional, comunicados internamente mediante resolución de nombres nativa de Docker y expuestos de manera segura a través de un Gateway perimetral.

### Componentes de Software Principales

- **Frontend UI:** Desarrollado en React, empaquetado estáticamente para el navegador. Consume endpoints apuntando exclusivamente al API Gateway.
- **Capa BFF (Backend-for-Frontend):** Actúa como agregador y formateador de datos provenientes de los microservicios core para optimizar la carga del cliente.
- **API Gateway:** Único punto de entrada perimetral que enruta las peticiones externas hacia el BFF o hacia el módulo de identidad según el contexto de la solicitud.

---

## Mapeo de Servicios y Puertos Operacionales

Al levantar la infraestructura, los servicios se exponen en el host local a través de los siguientes puertos de red:

| Nombre del Contenedor | Puerto Host | Tecnología / Framework | Propósito en el Ecosistema |
|----------------------|------------|------------------------|----------------------------|
| **innovatech-frontend** | `3000` | React / Next.js / Vite | Interfaz de usuario para la interacción con la plataforma. |
| **innovatech-bff** | `8080` | Java / Node.js / Python | Agregador intermedio de los microservicios de negocio. |
| **ms-gestion-proyectos** | `8081` | Java / Spring Boot | Núcleo de lógica de ciclos de vida y estados de proyectos. |
| **ms-auth** | `8082` | Java / Spring Boot | Proveedor de identidad, emisión y validación de firmas JWT. |
| **api-gateway** | `8083` | Java / Spring Cloud | Proxy inverso perimetral y guardián de rutas de la API. |
| **ms-monitoreo-analitica** | `8084` | Java / Spring Boot | Procesamiento de métricas y analítica de telemetría. |
| **ms-gestion-recursos** | `8086` | Java / Spring Boot | Control de capital humano, roles y disponibilidad. |
| **innovatech-db** | `5432` | PostgreSQL 15 Alpine | Almacenamiento relacional centralizado del ecosistema. |

---

## Requisitos Mínimos del Entorno

- **Docker Engine** v24.0.0 o superior.
- **Docker Compose** v2.0.0 o superior.
- Conectividad de red local libre en los puertos especificados en la tabla anterior.

---

## Variables de Entorno de Red Críticas

La comunicación inter-contenedor aprovecha el DNS interno de Docker. Los servicios se vinculan mediante las siguientes configuraciones clave:

- El **Frontend** dirige sus peticiones al API Gateway del host mediante:

```env
NEXT_PUBLIC_API_URL=http://localhost:8083
```

- El **API Gateway** distribuye tráfico internamente usando alias de contenedor:

```text
http://ms-auth:8082
http://innovatech-bff:8080
```

- El **BFF** consolida datos consultando directamente a los microservicios:

```text
http://ms-gestion-proyectos:8081
http://ms-gestion-recursos:8086
http://ms-monitoreo-analitica:8084
```

- Todos los **Microservicios Core Spring Boot** se conectan a PostgreSQL mediante:

```text
jdbc:postgresql://postgres-db:5432/innovatech_db
```

---

# Despliegue de la Infraestructura

## 1. Construcción y Arranque Inicial

Para descargar las imágenes base necesarias, compilar el código fuente de cada microservicio en su respectivo contenedor y levantar la malla completa de servicios:

```bash
docker compose up --build
```

## 2. Monitoreo de Contenedores

Para validar que todos los contenedores se encuentren operativos y verificar el mapeo de puertos:

```bash
docker compose ps
```

## 3. Visualización de Logs en Tiempo Real

Para inspeccionar la inicialización, migraciones o errores de un servicio específico:

```bash
docker compose logs -f ms-gestion-proyectos
```

## 4. Apagar y Limpiar el Entorno

Para detener todos los servicios y eliminar las redes creadas por Docker:

```bash
docker compose down
```

### Nota sobre Persistencia

Los datos almacenados en PostgreSQL permanecen disponibles después de ejecutar `docker compose down`, ya que están asociados al volumen persistente `pgdata`.

Si se requiere eliminar completamente la base de datos y realizar una instalación limpia:

```bash
docker compose down -v
```