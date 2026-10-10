# Plan de implementación — Manager Library

## Metodología
SDD: primero interpretar el spec; después implementar sin alterar historias, reglas, modelo ni contrato. Cada tarea termina con evidencia reproducible. Trabajar en los seis forks y subir los resultados antes de la presentación.

## Fases
| Fase | Entregable | Repositorios | Evidencia |
|---|---|---|---|
| P1 | Forks, clones, arquitectura y trazabilidad | docs | Documentos versionados |
| P2 | Laravel health, Docker, PostgreSQL vacío y migraciones | api, infra | Arranque y migraciones |
| P3 | Dominio, puertos y casos de uso | api | Unit tests y fakes |
| P4 | Adaptadores, JWT, HTTP y autorización | api | Pruebas de contrato |
| P5 | Préstamos, devoluciones, vencidos, reporte, concurrencia | api | Integración PostgreSQL |
| P6 | Login, libros, socios, préstamos, reportes | app | Recorrido completo React |
| P7 | Datos demo y página pública | tool, page | Sembrador HTTP y sitio responsive |
| P8 | Pruebas, documentación y feria | todos | Demo desde GitHub |

## Mapeo de tareas originales
| Tarea | Adaptación | Fase |
|---|---|---|
| T-01 | Laravel y GET /health | P2 |
| T-02 | Seis tablas, FK, índices y categorías en migraciones | P2 |
| T-03 | Value objects Isbn, Quantity, DateRange | P3 |
| T-04 | Dominio Book, stock y baja lógica | P3 |
| T-05 | Loan, LoanItem, estados calculados | P3 |
| T-06 | Member, User y normalización | P3 |
| T-07 | Login y alta de bibliotecarios con fakes | P3–P4 |
| T-08 | Libros y portadas con fakes | P3–P4 |
| T-09 | LendBooksService con fakes | P3–P5 |
| T-10 | Devolver y vencidos | P5 |
| T-11 | Reporte agregado congelado | P5 |
| T-12 | Repositorios reales PostgreSQL | P4 |
| T-13 | Préstamos concurrentes último ejemplar | P5 |
| T-14 | Hash y JWT | P4 |
| T-15 | Almacenamiento de portadas | P4 |
| T-16 | Contrato HTTP, errores y roles | P4–P5 |
| T-17 | Composición y admin desde entorno | P4 |
| T-18 | CHECK total positivo y rol | P5 |
| T-19 | Pruebas de arquitectura | P5 |
| T-20 | Docker Compose DB/API/frontend | P2–P8 |
| T-21 | Sembrador API >=40 libros, 10 socios, 15 préstamos, 3 vencidos | P7 |
| T-22 | React: login, catálogo, socios, prestar, devolver, vencidos, reporte | P6 |
| T-23 | Sitio estático independiente | P7 |

## Criterios de entrega
- Un comando documentado levanta contenedores; la base parte sin tablas y Laravel aplica migraciones.
- Health responde status ok; login y permisos cumplen 401/403.
- Contrato `/api/v1` y cuerpo de error uniforme.
- Las seis tablas, categorías, índices y restricciones se comprueban con consultas del spec.
- Los préstamos son atómicos, respetan 14 días y máximo tres abiertos.
- Concurrencia último ejemplar: uno 201 y otro 409.
- Devolución repetida: 409 y stock inalterado.
- Reporte mantiene título/categoría congelados tras edición.
- Frontend demuestra las historias; page funciona sin API; tool siembra por HTTP.

## Priorización
T-01 a T-17 forman el núcleo funcional. T-18 a T-23 elevan el resultado. Es preferible una tarea probada que varias a medias. No inventar multas, reservas, renovaciones ni notificaciones.

## Registro de evidencias
| Tarea | Estado | Prueba | Resultado | Commit |
|---|---|---|---|---|
| T-01 | Pendiente | GET /api/v1/health | Sin ejecutar | — |
| T-02 | Pendiente | Migraciones + SQL §10 | Sin ejecutar | — |
| T-09 | Pendiente | Prueba de préstamo | Sin ejecutar | — |
| T-13 | Pendiente | Concurrencia real | Sin ejecutar | — |
| T-22 | Pendiente | Demo React | Sin ejecutar | — |

Para la feria: mostrar lo construido, pruebas, lo pendiente y por qué, y enlaces a los seis forks.
