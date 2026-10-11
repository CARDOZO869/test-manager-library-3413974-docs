# Arquitectura implementada

Los seis repositorios siguen separados: docs especifica y documenta, api implementa HTTP/reglas/persistencia, app ofrece UI de operadores, infra inicia Docker, tool siembra por HTTP y page presenta el producto sin API.

API: `app/Domain/Entities` y `ValueObjects` contienen reglas sin Laravel; `app/Application/Ports` declara Clock, BookRepository, LendingRepository, ReturnsRepository, UserRepository, PasswordHasher, TokenIssuer, CoverStorage y MostBorrowedReportReader. `Application/Services` contiene los casos de uso. `Infrastructure/{Persistence,Security,Storage,Time}` implementa adaptadores. `Providers/LibraryServiceProvider.php` compone dependencias; `bootstrap/providers.php` registra el proveedor. `Http/Controllers/Api/V1` valida y serializa, `Http/ApiErrorResponse.php` unifica errores, `routes/api.php` define el contrato.

El adaptador de socios existe como PostgresMemberRepository; el controlador también realiza consultas sencillas de socios/categorías/listados a través de DB. No se presenta como una implementación absolutamente pura de puertos para cada lectura: dominio y aplicación sí mantienen independencia y las pruebas comprueban sus dependencias. No se agregaron abstracciones para cada consulta de presentación.

PostgreSQL: seis tablas singulares en esquema library, UUID v4, sin DEFAULT ni columnas genéricas de auditoría; categorías fijas. Migraciones Laravel propietarias del esquema. Tablas public heredadas y registro de migraciones se conservaron. El stock es transaccional con testigo xmin; este es metadato MVCC del motor, no una columna de negocio extra. Socio bloqueado para límites de préstamos; dos solicitudes con versión anterior compiten y solo una actualiza stock. Las líneas guardan título/ISBN/categoría congelados; reporte agrega esos snapshots y no datos actuales del catálogo.

Auth: JWT HMAC con sub/role/iat/exp, 8 horas, verificación de firma/expiración y coincidencia rol de usuario persistido. Secreto desde JWT_SECRET opcional o APP_KEY existente, nunca se reemplazó. Nuevos hashes Argon2id; password_verify conserva acceso con bcrypt existente. Sin creación de admin por HTTP; provisionamiento desde entorno.

Frontend real: `src/main.jsx`, `src/App.jsx`; `contexts/{AuthContext,useAuth}`, `services/{api,session}`, `hooks/{useCollection,useMemberNames}`, `components`, `pages`. Axios usa /api/v1 mediante proxy Vite y añade Bearer con sesión vigente. localStorage almacena token/rol/expiración; validación no crea valores faltantes. Rutas y roles controlan presentación, mientras API aplica autorización real. El storage de tokens presupone entorno de desarrollo y requiere protección frente a XSS en despliegue.

Compose: db postgres16/volumen existente, api PHP8.4 Laravel12 con vendor Linux/opcache y --no-reload, app Node22/Vite con polling Windows y proxy interno. Un único comando Start-Library.ps1 inicia y migra; secretos locales no se publican. El servidor artisan/Vite es desarrollo. Page usa HTML/CSS local sin auth/red API.

Clock real UTC por defecto. El Clock fijo exige simultáneamente APP_ENV=testing y DB manager_library_verification; solo sirve para verificar vencidos sin tocar fechas de la instalación habitual. No se modifica el reloj del sistema. Las pruebas de arquitectura comprueban dependencias dominio/aplicación y que la instanciación de infraestructura ocurre en composición.
