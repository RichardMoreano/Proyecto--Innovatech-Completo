\# Innovatech Solutions - Entrega Evaluación Parcial 2

\*\*Asignatura:\*\* DSY1106 - Desarrollo Fullstack III



\## Integrantes

\- Richard Moreano



\## Repositorios



\- \*\*Frontend\*\*: https://github.com/RichardMoreano/innovatech-frontend.git

\- \*\*BFF\*\*: https://github.com/RichardMoreano/innovatech-bff.git

\- \*\*Project Service\*\*: https://github.com/TU-USUARIO/innovatech-project-service

\- \*\*Resource Service\*\*: https://github.com/TU-USUARIO/innovatech-resource-service

\- \*\*Arquetipo Base\*\*: https://github.com/TU-USUARIO/innovatech-microservice-base



\## Tecnologías y Patrones Implementados



\*\*Backend:\*\*

\- Microservicios con Spring Boot 3.3 + Java 17

\- Patrón \*\*Database-per-Service\*\*

\- \*\*Repository Pattern\*\*

\- \*\*Factory Method\*\*

\- \*\*DTO Pattern\*\*

\- \*\*Circuit Breaker\*\* (Resilience4j)

\- \*\*JWT Authentication\*\*



\*\*BFF:\*\*

\- Backend For Frontend

\- Orquestación de servicios

\- Agregación de datos (`/proyectos-con-recursos`)



\*\*Frontend:\*\*

\- React + Vite

\- \*\*Componente reutilizable\*\* (`ProjectCard`) listo para NPM

\- Consumo del BFF con Axios



\## Cómo Probar el Sistema (Paso a Paso)



\### Requisitos previos

- PostgreSQL instalado y en ejecución
- Node.js instalado (para frontend)
- Java 25 instalado:

&#x20; ```sql

&#x20; CREATE DATABASE innovatech\_projects\_db;

&#x20; CREATE DATABASE innovatech\_resources\_db;



\# Terminal 1 - Project Service

cd innovatech-project-service

./mvnw spring-boot:run



\# Terminal 2 - Resource Service

cd innovatech-resource-service

./mvnw spring-boot:run



\# Terminal 3 - BFF

cd innovatech-bff

./mvnw spring-boot:run



\# Terminal 4 - BFF

cd innovatech-frontend

npm run dev

