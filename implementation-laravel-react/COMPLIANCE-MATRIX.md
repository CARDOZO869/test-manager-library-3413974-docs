# Matriz de cumplimiento verificado

Auditoría y verificación local: 10–11 de octubre de 2026. Fuentes: `spec-python/` y `spec-.net/`, cuyos contratos son independientes del lenguaje; [informe oficial](https://code-sena.github.io/ADSO-3413974/informes/2026-10-10-prueba-manager-library-7-informes/) y [herramienta oficial](https://github.com/code-sena/test-manager-library-3413974-tool). Se conservaron las especificaciones originales. Este documento describe evidencia local, no una calificación del instructor.

## Historias y criterios de aceptación

| Requisito | Estado inicial / evidencia e incumplimiento | Acción correctiva y archivos | Validación | Estado final |
|---|---|---|---|---|
| HU-01 / CA-01.1–3: JWT 8 h, 401/403 | Respuesta con BOM; sesión React inválida. Servidor HTTP perdía entorno Docker y usaba SQLite. | Bootstrap limpio, `HmacTokenIssuer` firma rol; `AuthenticatedUserResolver`; Compose `--no-reload`; `session.js`, `api.js`, `AuthContext.jsx`, rutas protegidas y vencimiento. | AuthenticationTest, SecurityTest, LibraryContractTest; 4 pruebas frontend; admin entra, recarga, logout, `/books` redirige a `/login`. | Verificado; contraseña intacta. |
| HU-02 / CA-02.1–3: bibliotecarios | Servicios existentes, cobertura HTTP insuficiente, bcrypt. | `LaravelPasswordHasher`: Argon2id para nuevas claves, compatibilidad con bcrypt; `ApiErrorResponse`; Users protegido. | API sintética transaccional: 201, normalización, duplicado 409, rol admin 422, librarian 403; sin clave en respuesta. | Verificado por API; no operador real adicional creado. |
| HU-03 / CA-03.1–5: catálogo, stock, portada, baja | `exists:library.category` interpretaba conexión inexistente; portada faltante en UI. | `LibraryController`: validación pgsql; `BookCatalogService` preserva versión; Books/BookDetails/BookCover; eliminar archivo al reemplazar o quitar portada. | BookCatalogTest, BookCoverTest y contrato: PNG, 3 MB rechazado, stock y baja; creación manual persistente. | Verificado. |
| HU-04 / CA-04.1–3: búsqueda/paginación | React esperaba otra estructura; consulta categoría por cada fila. | Books/useCollection usan q/items/total; categoría cargada por página; Pagination. | Repositorio, contrato y benchmark real. | Funcional verificado; alcance de rendimiento abajo. |
| HU-05 / CA-05.1–3: socios | Listado incompatible y detalle faltante. | Members/useCollection, creación, búsqueda, paginación y detalle; DOCUMENT_TAKEN. | MemberUserTest, PostgresRepositoriesTest, 409 duplicado; socio sintético creado en navegador. | Verificado; sin acción de eliminación. |
| HU-06 / CA-06.1–7: préstamo 1–3, límites, 14 días, snapshots | UI enviaba cuerpo incorrecto; concurrencia sin testigo optimista. | Loans envía items; selección buscable; `PostgresLoanRepository` transaccional, bloqueo socio y versión xmin condicional. | LendBooksTest, contrato, dos procesos y dos HTTP: 201/409; préstamo manual. | Verificado. |
| HU-07 / CA-07.1–4: devolución por línea | Integración incompleta. | Loans usa préstamo/línea; ReturnBookService y persistencia atómicos. | Unitarias, PostgreSQL, doble devolución 409; devolución manual deja disponibilidad 1/1 tras recarga. | Verificado. |
| HU-08 / CA-08.1–3: consultar y filtrar | Filtros incompletos, socio mostrado como UUID. | Loans filtra estado/fecha/socio; useMemberNames consulta nombres reales; Clock para estado. | Contrato y LoanTest; listado y persistencia tras recarga. | Verificado por API y listado; líneas visibles dentro del listado. |
| HU-09 / CA-09.1–2: vencidos | Ruta overdue absorbida por `{id}`. | Orden de rutas; Loans muestra título, socio y días; ListOverdueService. | Unitarias, PostgreSQL y sembrador con reloj aislado; panel muestra 3 líneas preexistentes. | Verificado. |
| HU-10 / CA-10.1–5: reporte histórico | React consultaba sin fechas y esperaba otro conteo; agregado en memoria. | Reports usa rango y times_borrowed; lector agrega SQL por snapshots. | MostBorrowedReportTest y contrato: renombrar no cambia histórico, 422 rango invertido, vacío válido, 403 librarian; reporte manual incluye préstamo devuelto. | Verificado. |

## Tareas oficiales

| Tarea | Evidencia inicial / incumplimiento | Acción y archivos | Prueba final | Estado |
|---|---|---|---|---|
| T-01 esqueleto/health | Laravel existente, BOM | Bootstrap limpio y healthcheck | LibraryHttpWiringTest, Docker healthy | Verificado |
| T-02 seis tablas, FK, índices, sin DEFAULT, 5 categorías | Migraciones existentes | Mantener esquema library, revisar motor | LibraryContractTest, database-tables.txt | Verificado en library; public heredado conservado |
| T-03 objetos de valor | Isbn/Quantity/DateRange existentes | Ejercitar reglas | ValueObjectsTest | Verificado |
| T-04 Book | Entidad existente | Preservar versión al editar | BookTest/BookCatalogTest | Verificado |
| T-05 Loan | Entidad existente | Clock inyectado HTTP | LoanTest/LendBooksTest | Verificado |
| T-06 Member/User | Entidades existentes | Normalización/rol comprobados | MemberUserTest | Verificado |
| T-07 auth con fakes | Servicios existentes | JWT rol y hash | AuthenticationTest | Verificado |
| T-08 libros con fakes | Servicio existente | Portada y versión | BookCatalogTest/BookCoverTest | Verificado |
| T-09 prestar con fakes | Reglas existentes | Integración items/errores | LendBooksTest | Verificado |
| T-10 devolver/vencidos | Servicios existentes | Ruta y Clock | ReturnBookTest e integración | Verificado |
| T-11 reporte | Servicio existente | Agregado SQL histórico | MostBorrowedReportTest/contrato | Verificado |
| T-12 repositorios PostgreSQL | Adaptadores existentes; HTTP elegía SQLite | Mantener entorno servidor | PostgresRepositoriesTest | Verificado |
| T-13 concurrencia optimista | Bloqueos sin testigo | Repositorios Book/Loan usan xmin | ConcurrentLendingTest, HTTP 201/409 | Verificado |
| T-14 hash/JWT | bcrypt y secreto en log histórico | Argon2id nuevo; JWT rol; errores sanitizados; log redactado con respaldo DPAPI | SecurityTest, contrato, log-secret-scan-final.json | Verificado en escaneo; TLS pendiente para exposición pública |
| T-15 portadas disco | Adaptador parcial/UI faltante | CoverStorage, LocalCoverStorage, BookCoverService, BookCover | PNG, eliminación, límite tamaño | Verificado |
| T-16 HTTP | Errores heterogéneos/ruta ambigua | ApiErrorResponse, bootstrap, rutas/controladores | Todas rutas privadas y 14 códigos de negocio | Verificado |
| T-17 composición/admin | Proveedor/comando existentes | Bootstrap conserva admin existente | LibraryHttpWiringTest; DB aislada vacía migrada/admin | Verificado |
| T-18 CHECK total/rol | Migración existente | Quitar BOM/conservar restricciones | SQLSTATE 23514 en ambos casos | Verificado |
| T-19 arquitectura | Cobertura parcial | Tres ArchitectureTest, composición y dependencias | Suite PHP; sin import-linter de Python | Adaptado y verificado |
| T-20 infra | Compose con fallos env/health | Start-Library.ps1, vendor Linux, opcache, proxy | Docker y script de arranque | Instalación existente; clon limpio completo no ensayado |
| T-21 demo API | tool solo README | seed-demo.mjs, checkpoint y verify | 40 libros/10 socios/15 préstamos/3 líneas propias vencidas | Reloj aislado de pruebas; real debe esperar 14 días |
| T-22 app | Duplicados/contratos incompatibles | Consolidación src, páginas integradas | Build/lint/4 tests y recorrido manual completo | Verificado; usuarios/portadas por API |
| T-23 page | Solo README | HTML/CSS estáticos, preview.mjs | Móvil 375 px/escritorio, independiente de API | Verificado local; sin publicación |

## Requisitos no funcionales y evaluación

| Criterio | Evidencia | Alcance y límite |
|---|---|---|
| RNF-1 <300 ms / 5.000 libros | 5.008 activos, 3 calentamientos, 20 HTTP; mediana 117,52 ms, p95 130,27 ms, máximo 156 ms | Fixture grande creado por SQL solo en DB aislada; no es prueba completa de 5.000 creados por tool. No garantiza arranque frío/producción. |
| RNF-2 último ejemplar | Dos procesos y dos HTTP: uno 201 y otro 409 | Servidor de pruebas multiworker; repetir en despliegue. |
| RNF-3 secretos | Hash, respuesta sin clave, log histórico redactado; escaneo final sin claves configuradas ni JWT | HTTP local y .env son configuración de desarrollo. TLS/custodia configuración necesarios para publicación; no certifica logs externos. |
| RNF-4 error único | code/message/details, errores negocio y 500 genérico sin SQL/traza | No se simuló cada fallo del proxy externo. |
| RNF-5 arranque/base vacía | Script aplica migraciones library; nueva DB aislada arrancó vacía | DB habitual conservada con tablas framework public; no se eliminan para aparentar vacío. |
| Commits/plazo histórico | Seis repos auditados, cambios iniciales sin seguimiento | No hubo commit ni push; no se corrige retroactivamente plazo/informe. |
| Docs/congruencia | Matriz, informe, arquitectura real, instrucciones y evidencia | Revisión local; sin recalificación oficial. |
| Page/completitud | Responsive y flujos reales | Sin URL publicada. |
| Extras/inglés | Sin multas/pagos/reservas/renovaciones/atributos extra; identificadores en inglés | Framework y tablas heredadas conservados por seguridad. |

El informe oficial está anonimizado (24 entradas Axx). No hay datos suficientes para atribuir una fila al propietario de estos repositorios; no se inventó correspondencia. No se certifica 100 % de la evaluación histórica ni RNF-1 en su método exacto. El núcleo funcional local tiene evidencia reproducible en `evidence/`.
