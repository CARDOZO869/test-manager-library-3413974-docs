# Manager Library — Implementación Laravel y React

## Objetivo
Desarrollar un sistema de gestión de biblioteca siguiendo las especificaciones oficiales del reto ADSO 3413974.

## Tecnologías
- Backend: PHP con Laravel.
- Frontend: React.
- Base de datos: PostgreSQL 16.
- Infraestructura: Docker Compose.
- API: REST con JSON.

## Funcionalidades
1. Autenticación y autorización por roles.
2. Gestión de bibliotecarios.
3. Gestión y búsqueda de libros.
4. Registro y consulta de socios.
5. Préstamos y devoluciones.
6. Consulta de préstamos vencidos.
7. Reporte de libros más prestados.

## Reglas principales
- Préstamos de 14 días.
- Máximo 3 libros sin devolver por socio.
- Bloqueo de nuevos préstamos si existen vencidos.
- Control de ejemplares disponibles.
- Conservación del historial de préstamos.

## Organización
- docs: especificaciones y documentación.
- api: backend Laravel.
- app: frontend React.
- page: sitio público.
- infra: infraestructura Docker.
- tool: sembrador de demostración mediante la API.

## Metodología
Desarrollo guiado por especificaciones (SDD). Cada tarea se considera terminada cuando cuenta con evidencia verificable.

## Estado
P1: preparación del entorno y adaptación documental en progreso.