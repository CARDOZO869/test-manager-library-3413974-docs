# Matriz de trazabilidad — Manager Library

Fuente de verdad: `spec-python/spec.md`, `api-contract.md`, `data-model.md`, `tasks.md`; contrastar con `spec-.net/`. Estado de implementación: pendiente.

## Historias de usuario
| HU | Función | Laravel | React | Evidencia |
|---|---|---|---|---|
| HU-01 | Login y roles | JWT 8h, 401/403 | Login, rutas protegidas | CA-01.1 a 01.3 |
| HU-02 | Alta bibliotecarios | POST /users solo admin; normalizar usuario | Formulario admin | CA-02.1 a 02.3; 409/422 |
| HU-03 | Libros | Crear, editar, baja lógica, portada, stock | Catálogo admin | CA-03.1 a 03.5 |
| HU-04 | Buscar libros | Texto, categoría, paginación y 404 | Buscador | CA-04.1 a 04.3 |
| HU-05 | Socios | Crear, buscar, listar; documento único | Formulario y listado | CA-05.1 a 05.3 |
| HU-06 | Préstamos | Transacción, límites, vencidos, snapshots | Registrar préstamo | CA-06.1 a 06.7 |
| HU-07 | Devoluciones | Retorno por línea, 409 doble | Devolver línea | CA-07.1 a 07.4 |
| HU-08 | Consultar préstamos | Listado, filtros, estado calculado | Lista y detalle | CA-08.1 a 08.3 |
| HU-09 | Vencidos | Líneas pendientes y días atraso | Tabla vencidos | CA-09.1 a 09.2 |
| HU-10 | Más prestados | Agregado por snapshots, solo admin | Reporte | CA-10.1 a 10.5 |

## Rutas bajo /api/v1
| Método | Ruta | Permiso |
|---|---|---|
| POST | /auth/login | público |
| GET | /health | público |
| POST | /users | admin |
| GET | /categories | autenticado |
| GET | /books | autenticado |
| GET | /books/{id} | autenticado |
| POST | /books | admin |
| PUT | /books/{id} | admin |
| DELETE | /books/{id} | admin |
| PUT | /books/{id}/cover | admin |
| GET | /books/{id}/cover | autenticado |
| DELETE | /books/{id}/cover | admin |
| GET | /members | admin/librarian |
| GET | /members/{id} | admin/librarian |
| POST | /members | admin/librarian |
| POST | /loans | admin/librarian |
| GET | /loans | admin/librarian |
| GET | /loans/{id} | admin/librarian |
| POST | /loans/{loan_id}/items/{item_id}/return | admin/librarian |
| GET | /loans/overdue | admin/librarian |
| GET | /reports/most-borrowed | admin |

Nota: GET /books/{id}/cover está indicado en la explicación de portadas del contrato aunque no figura como fila separada en su tabla. Implementarlo y registrar la diferencia documental.

## Reglas de negocio y no funcionales
| Regla | Criterio verificable |
|---|---|
| RN-1 | 0 <= disponibles <= total, CHECK en PostgreSQL |
| RN-2 | Vencimiento a 14 días; máximo 3 libros sin devolver |
| RN-3 | Socio con vencidos recibe 409 |
| RN-4 | Título, ISBN y categoría congelados en loan_item |
| RN-5 | Préstamos no se borran; libros baja lógica |
| RN-6 | Fechas UTC; mensajes español; campos y código inglés |
| RNF-1 | Búsqueda <300 ms con 5000 libros |
| RNF-2 | Último ejemplar concurrente: 201 + 409 |
| RNF-3 | Sin contraseñas claras en DB, logs o respuestas |
| RNF-4 | Errores con cuerpo {code,message,details} |
| RNF-5 | Arranque con un comando y base inicialmente vacía |

## Códigos de negocio
- 401: INVALID_CREDENTIALS.
- 403: FORBIDDEN_ROLE.
- 404: NOT_FOUND.
- 409: USERNAME_TAKEN, ISBN_TAKEN, DOCUMENT_TAKEN, BOOK_HAS_OPEN_LOANS, BOOK_NOT_AVAILABLE, MEMBER_HAS_OVERDUE, ITEM_ALREADY_RETURNED.
- 422: MEMBER_LIMIT_EXCEEDED, DUPLICATE_BOOK_IN_LOAN, VALIDATION_ERROR, INVALID_DATE_RANGE.

## Modelo y alcance
Seis tablas: category, book, member, loan, loan_item, user; PostgreSQL 16, esquema library, UUID v4, fechas UTC. Cinco categorías fijas: Novela, Ciencia, Tecnología, Historia, Infantil. Admin inicial por entorno. Excluidos: multas, pagos, reservas, renovaciones, SMS/correo, importación masiva, préstamos entre sedes, editorial, año e idioma.

## Seguimiento
| HU | Estado | Evidencia | Commit |
|---|---|---|---|
| HU-01 | Pendiente | — | — |
| HU-02 | Pendiente | — | — |
| HU-03 | Pendiente | — | — |
| HU-04 | Pendiente | — | — |
| HU-05 | Pendiente | — | — |
| HU-06 | Pendiente | — | — |
| HU-07 | Pendiente | — | — |
| HU-08 | Pendiente | — | — |
| HU-09 | Pendiente | — | — |
| HU-10 | Pendiente | — | — |

No marcar completado sin ejecutar la evidencia.
