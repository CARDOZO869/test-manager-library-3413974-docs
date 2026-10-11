# Estado final e inventario Git

Los seis repositorios contienen cambios locales sin commit ni push. Algunos archivos ya estaban sin seguimiento al iniciar; este inventario describe el estado final, no atribuye todos los archivos a esta sesión. Los duplicados React ausentes de su ruta original están en respaldo recuperable.

## test-manager-library-3413974-api  HEAD: 265e8c7. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M .dockerignore
 M Dockerfile
 M README.md
 M app/Application/Ports/CoverStorage.php
 M app/Application/Ports/MostBorrowedReportReader.php
 M app/Application/Services/BookCatalogService.php
 M app/Application/Services/BookCoverService.php
 M app/Application/Services/MostBorrowedReportService.php
 M app/Domain/Entities/Book.php
 M app/Http/Controllers/Api/V1/CatalogManagementController.php
 M app/Http/Controllers/Api/V1/LibraryController.php
 M app/Http/Controllers/Api/V1/LoanCoverController.php
 M app/Infrastructure/Persistence/PostgresBookRepository.php
 M app/Infrastructure/Persistence/PostgresLoanRepository.php
 M app/Infrastructure/Persistence/PostgresMostBorrowedReportReader.php
 M app/Infrastructure/Security/AuthenticatedUserResolver.php
 M app/Infrastructure/Security/HmacTokenIssuer.php
 M app/Infrastructure/Security/LaravelPasswordHasher.php
 M app/Infrastructure/Storage/LocalCoverStorage.php
 M app/Providers/LibraryServiceProvider.php
 M bootstrap/providers.php
 M routes/api.php
 M tests/Feature/PostgresLoanRepositoryTest.php
 M tests/Unit/Application/BookCoverTest.php
 M tests/Unit/Infrastructure/SecurityTest.php
?? .editorconfig
?? .env.example
?? .gitattributes
?? .gitignore
?? app/Application/Ports/Clock.php
?? app/Http/ApiErrorResponse.php
?? app/Http/Controllers/Controller.php
?? app/Infrastructure/Time/SystemClock.php
?? app/Models/User.php
?? app/Providers/AppServiceProvider.php
?? artisan
?? bootstrap/app.php
?? bootstrap/cache/.gitignore
?? composer.json
?? composer.lock
?? config/app.php
?? config/auth.php
?? config/cache.php
?? config/cors.php
?? config/database.php
?? config/filesystems.php
?? config/library.php
?? config/logging.php
?? config/mail.php
?? config/queue.php
?? config/services.php
?? config/session.php
?? database/.gitignore
?? database/factories/UserFactory.php
?? database/migrations/0001_01_01_000000_create_users_table.php
?? database/migrations/0001_01_01_000001_create_cache_table.php
?? database/migrations/0001_01_01_000002_create_jobs_table.php
?? database/migrations/2026_10_10_190508_add_domain_check_constraints_to_library_tables.php
?? database/seeders/DatabaseSeeder.php
?? database/seeders/LibraryDemoSeeder.php
?? package.json
?? phpunit.xml
?? public/.htaccess
?? public/favicon.ico
?? public/index.php
?? public/robots.txt
?? resources/css/app.css
?? resources/js/app.js
?? resources/js/bootstrap.js
?? resources/views/welcome.blade.php
?? routes/api.php.backup
?? routes/console.php
?? routes/web.php
?? storage/app/.gitignore
?? storage/app/private/.gitignore
?? storage/app/public/.gitignore
?? storage/framework/.gitignore
?? storage/framework/cache/.gitignore
?? storage/framework/cache/data/.gitignore
?? storage/framework/sessions/.gitignore
?? storage/framework/testing/.gitignore
?? storage/framework/views/.gitignore
?? storage/logs/.gitignore
?? tests/Architecture/ArchitectureTest.php
?? tests/Feature/ConcurrentLendingTest.php
?? tests/Feature/ExampleTest.php
?? tests/Feature/LibraryContractTest.php
?? tests/Support/benchmark-search.php
?? tests/Support/concurrent-http-worker.php
?? tests/Support/concurrent-loan-worker.php
?? tests/TestCase.php
?? tests/Unit/ExampleTest.php
?? tests/login-diagnostic.php
?? tests/session-probe.php
?? vite.config.js
```

## test-manager-library-3413974-app  HEAD: 92b6eb8. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M README.md
?? .gitignore
?? .oxlintrc.json
?? index.html
?? package-lock.json
?? package.json
?? public/favicon.svg
?? public/icons.svg
?? src/App.css
?? src/App.jsx
?? src/assets/hero.png
?? src/assets/react.svg
?? src/assets/vite.svg
?? src/components/BookCover.jsx
?? src/components/Layout.jsx
?? src/components/Pagination.jsx
?? src/components/ProtectedRoute.jsx
?? src/components/ResourceStatus.jsx
?? src/contexts/AuthContext.jsx
?? src/contexts/useAuth.js
?? src/index.css
?? src/main.jsx
?? src/pages/Books.jsx
?? src/pages/Dashboard.jsx
?? src/pages/Loans.jsx
?? src/pages/Login.jsx
?? src/pages/Members.jsx
?? src/pages/Reports.jsx
?? src/pages/Users.jsx
?? src/services/api.js
?? src/services/session.js
?? src/services/useCollection.js
?? src/services/useMemberNames.js
?? tests/session.test.mjs
?? vite.config.js
```

## test-manager-library-3413974-docs  HEAD: f4e5e88. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M README.md
 M implementation-laravel-react/architecture.md
 M implementation-laravel-react/requirements-mapping.md
?? ersjuansManager-Librarytest-manager-library-3413974-docs
?? implementation-laravel-react/ACTUAL-ARCHITECTURE.md
?? implementation-laravel-react/COMPLIANCE-MATRIX.md
?? implementation-laravel-react/FILE-INVENTORY.md
?? implementation-laravel-react/FINAL-REPORT.md
?? implementation-laravel-react/README.md
?? implementation-laravel-react/evidence/backend-tests.txt
?? implementation-laravel-react/evidence/browser-flow.md
?? implementation-laravel-react/evidence/dashboard.jpg
?? implementation-laravel-react/evidence/database-tables.txt
?? implementation-laravel-react/evidence/demo-seeder.json
?? implementation-laravel-react/evidence/docker-status.txt
?? implementation-laravel-react/evidence/frontend-build.txt
?? implementation-laravel-react/evidence/frontend-lint.txt
?? implementation-laravel-react/evidence/frontend-tests.txt
?? implementation-laravel-react/evidence/instructor-report.html
?? implementation-laravel-react/evidence/log-secret-scan-final.json
?? implementation-laravel-react/evidence/log-secret-scan.json
?? implementation-laravel-react/evidence/page-mobile.jpg
?? implementation-laravel-react/evidence/report.jpg
?? implementation-laravel-react/evidence/repository-status-final.json
?? implementation-laravel-react/evidence/repository-status.json
?? implementation-laravel-react/evidence/search-benchmark.json
?? implementation-laravel-react/evidence/startup.json
```

## test-manager-library-3413974-infra  HEAD: 7891fd7. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M LOCAL-SETUP.md
 M README.md
 M docker-compose.yml
?? RUNBOOK.md
?? Start-Library.ps1
?? php-performance.ini
?? test.sql
```

## test-manager-library-3413974-page  HEAD: dbc9ad6. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M README.md
?? LOCAL-PREVIEW.md
?? index.html
?? preview.mjs
?? styles.css
```

## test-manager-library-3413974-tool  HEAD: 68da4d2. Secretos configurados seguidos por Git: 0. diff --check: 0.  ```text
 M README.md
?? .gitignore
?? DEMO-GUIDE.md
?? seed-demo.mjs
```
