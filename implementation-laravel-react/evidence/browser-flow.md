# Recorrido manual del navegador

Entorno: app http://localhost:5173, API PostgreSQL habitual; operador admin existente. Contraseña y token no se capturaron.

1. Login correcto: panel con 40 libros, 10 socios, 15 préstamos y 3 líneas vencidas.
2. Crear libro Validación integral 20261010, Autor de validación, ISBN 9799998887770, Ciencia, una copia.
3. Crear Socio de validación integral, documento sintético E2E-20261010. Recargar y comprobar persistencia.
4. Buscar ambos en selectores y registrar préstamo de una línea. Recargar lista y comprobar que persiste.
5. Devolver únicamente esa línea. El catálogo tras recarga muestra total 1 y disponibles 1.
6. Consultar reporte 2026-10-11 UTC: título de validación, categoría Ciencia, veces prestado 1. Captura report.jpg.
7. Panel final: 41 libros, 11 socios, 16 préstamos, 3 vencidos. Captura dashboard.jpg.
8. Cerrar sesión; abrir /books: redirección a http://localhost:5173/login sin acceso al catálogo.

Los datos sintéticos se conservan; los préstamos vencidos preexistentes no se devolvieron ni alteraron. Una captura preliminar del reporte antes de consultar se archivó fuera del repositorio en backups/session-scripts/report-before-query.jpg; no se considera prueba de devolución. La devolución se comprobó por vista de detalle y por integración automatizada.

Sitio público: http://127.0.0.1:4178, independiente de la API. Verificado a 375 × 812; ancho de contenido 360 y ancho de viewport 375, sin overflow. Captura page-mobile.jpg. También inspeccionado en escritorio.
