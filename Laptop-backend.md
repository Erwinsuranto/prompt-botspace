





# 
```



```
# 
```



```
# 
```



```
# Prompt berikutnya — B-021
```
PROMPT B-021 — AUTHENTICATION API

Lanjutkan /root/botspace-backend pada task B-021 sesuai ROADMAP_V2.

Tujuan:
Implementasikan Authentication API production-grade sebagai fondasi untuk Workspace dan BotSpace.

Scope WAJIB:
1. Implement signup, login, logout, dan current-session.
2. Gunakan contract dari packages/contracts yang sudah ada.
3. Implement credential/password mechanism dengan aman:
   - password tidak boleh disimpan plaintext
   - gunakan Argon2id/bcrypt yang sesuai dependency existing
   - jangan menambahkan dependency baru jika dependency yang ada sudah mencukupi.
4. Integrasikan dengan SessionRepository dan repository/database adapter yang sudah dibuat.
5. Session harus:
   - memiliki token/session identifier yang aman
   - memiliki expiry
   - dapat direvoke saat logout
   - current-session hanya mengembalikan session yang valid.
6. Buat API error envelope yang konsisten dengan B-014.
7. Jangan mencampur authentication dengan business logic Workspace/Bot.
8. Struktur kode harus modular:
   - auth domain
   - auth service/use-case
   - auth repository
   - HTTP/API handler
   - schema/validation
   Pisahkan tanggung jawab dengan jelas agar perubahan auth nantinya tidak mengharuskan audit seluruh backend.
9. Tambahkan test untuk:
   - signup berhasil
   - duplicate email/identity ditolak
   - login berhasil
   - password salah ditolak
   - current-session berhasil
   - session expired/revoked ditolak
   - logout berhasil
   - logout/session invalid tidak menyebabkan crash.
10. Pastikan tidak ada credential/token/password yang masuk ke log.
11. Pertahankan boundary:
   apps -> services -> domain/repository
   dan contracts tetap menjadi boundary publik.
12. Jangan mengubah ROADMAP.md / ROADMAP_V2.md.
13. Jangan menyentuh frontend kecuali benar-benar diperlukan oleh contract.
14. Jangan melakukan refactor besar di luar scope B-021.

VALIDATION WAJIB:
- lint
- typecheck
- import-check
- secret scan
- format check
- build
- test
- frozen install
- cek git diff/status
- pastikan working tree bersih setelah commit
  (kecuali file yang memang sengaja dikecualikan oleh governance).

Jika ada dependency atau kontrak yang belum tersedia:
- jangan membuat workaround sembarangan
- identifikasi blocker secara jelas
- jangan mengubah scope task berikutnya.

COMMIT:
Buat commit hanya untuk perubahan B-021.
JANGAN PUSH.

OUTPUT AKHIR WAJIB:
- files changed
- API endpoint yang dibuat
- authentication flow
- security decisions
- test/validation result
- commit hash
- remaining risks
- next recommended task

Jika semua validation GREEN, nyatakan:
B-021 COMPLETE — WAIT FOR NEXT INSTRUCTION.


```
# Prompt 17 — B-020 User + Session Schema
```
PROMPT 17: BOTSPACE B-020 — USER + SESSION SCHEMA & MIGRATION

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

ROLE:
Kimi utama — Senior Backend Architect + Database Engineer.

PREVIOUS:
B-010 Contracts           COMPLETE
B-011 Config Loader       COMPLETE
B-012 Observability       COMPLETE
B-013 Database Foundation COMPLETE
B-014 API Server Skeleton COMPLETE
B-015 Domain/Repository   COMPLETE

OBJECTIVE:
Implement B-020 — User + Session schema and migration.

IMPORTANT:
- JANGAN PUSH.
- JANGAN ubah main.
- Jangan mengerjakan frontend.
- Jangan mengimplementasikan login UI.
- Jangan membuat authentication flow lengkap.
- Fokus pada database/domain foundation untuk User + Session.
- Jangan mengubah schema yang sudah stabil tanpa alasan.
- Jangan mengarang entity yang belum dibutuhkan.

==================================================
1. AUDIT
==================================================

Baca:

- ROADMAP_V2.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- AI_RULES.md
- PROJECT_STATUS.md
- B-013 database implementation
- B-014 API skeleton
- B-015 domain/repository ports
- packages/contracts
- packages/config
- database schema/migrations

Tentukan terlebih dahulu:
- existing User model
- existing session-related fields
- ID strategy
- timestamp strategy
- uniqueness rules
- deletion strategy
- migration conventions

Jangan langsung coding sebelum dependency map jelas.

==================================================
2. USER SCHEMA
==================================================

Implementasikan User schema sesuai architecture.

Pastikan:

- primary key konsisten dengan B-013/B-015
- identifier uniqueness jelas
- createdAt
- updatedAt
- nullable fields benar
- indexes hanya yang memang diperlukan
- no plaintext secrets
- tidak ada credential leakage

Jangan menambahkan profil user yang belum dibutuhkan.

==================================================
3. SESSION SCHEMA
==================================================

Buat Session schema yang aman.

Minimal evaluasi:

- session ID
- user relation
- expiration
- createdAt
- updatedAt jika diperlukan
- revoked/invalidated state jika architecture membutuhkan
- indexes untuk lookup dan expiry

Session secret/token:

- jangan disimpan plaintext jika architecture membutuhkan
  hashed token representation
- jangan log token
- jangan expose token melalui repository/domain error

Gunakan pendekatan yang aman dan sederhana.

==================================================
4. RELATIONSHIP
==================================================

Pastikan:

User
  ↓
Session

relationship memiliki:

- foreign key
- delete behavior yang aman
- index pada foreign key
- referential integrity

Jangan merusak relation existing:

Workspace
WorkspaceMember
Bot
Account

==================================================
5. MIGRATION
==================================================

Buat migration baru mengikuti format migration B-013.

Migration harus:

- deterministic
- reversible jika tooling mendukung
- tidak destructive terhadap existing data
- memiliki constraint yang benar
- memiliki index yang diperlukan

Jangan menggunakan destructive migration
untuk data existing tanpa explicit requirement.

==================================================
6. DOMAIN ALIGNMENT
==================================================

Sesuaikan domain primitives/repository ports B-015
dengan User + Session jika memang diperlukan.

Jangan memasukkan database implementation
ke domain layer.

Dependency:

domain
 ↓
repository port
 ↓
database adapter

Tetap pertahankan boundary.

==================================================
7. CONTRACTS
==================================================

Audit packages/contracts.

Jika contract User/Session memang sudah tersedia:
gunakan dan align.

Jika belum tersedia:
jangan membuat public API contract besar.

Buat hanya type internal yang diperlukan.

==================================================
8. SECURITY AUDIT
==================================================

Audit khusus:

- session token storage
- credential exposure
- logging
- serialization
- database errors
- session expiration
- revoked sessions
- brute-force related indexing/lookup concerns

Jangan implementasikan rate limiting di B-020
kecuali architecture secara eksplisit meminta.

==================================================
9. TESTS
==================================================

Tambahkan test untuk:

- User creation constraints
- User uniqueness
- Session → User relation
- Session expiration
- session lookup
- revoked/invalid state jika ada
- foreign-key behavior
- migration correctness
- duplicate constraints
- repository behavior jika repository implementation
  memang termasuk scope

Gunakan test database/container sesuai tooling repository.

==================================================
10. VALIDATION
==================================================

Jalankan:

- migration validation
- database schema validation
- format
- lint
- typecheck
- import-check
- secret scan
- ownership check
- doc-link check
- build
- test

Jika PostgreSQL client tidak tersedia:
gunakan mekanisme Docker yang sudah berhasil dipakai
pada B-013.

Jangan bypass migration test.

==================================================
11. ARCHITECTURE
==================================================

Jangan mengubah:

- API server architecture B-014
- contracts tanpa kebutuhan
- observability
- config
- frontend
- bot modules

B-020 harus menjadi foundation yang bisa dipakai
authentication/session layer berikutnya.

==================================================
12. GIT
==================================================

Jika semua validation GREEN:

commit:

feat: add user and session schema

Working tree harus CLEAN.

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

B-020 RESULT

Status:
User Schema:
Session Schema:
Relations:
Indexes:
Constraints:
Migration:
Security:
Domain Alignment:
Contract Alignment:

Migration Test:
Lint:
Typecheck:
Import Check:
Build:
Tests:

Changed Files:
Commit:
Working Tree:
Push: NO

Problems Found:
- ...

Architecture Decisions:
- ...

Remaining Risks:
- ...

Next Recommended Task:
- ...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```

# Prompt 16 — B-014 API Server Skeleton
```
PROMPT 16: BOTSPACE B-014 — API SERVER SKELETON

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

ROLE:
Kimi utama — Senior TypeScript Backend Architect.

PREVIOUS TASKS:
B-010 Contracts           COMPLETE
B-011 Config Loader       COMPLETE
B-012 Observability       COMPLETE
B-013 Database Foundation COMPLETE
B-015 Domain/Repository   COMPLETE

NEXT TASK:
B-014 — API SERVER SKELETON

IMPORTANT:
- Jangan push.
- Jangan mengubah main.
- Jangan mengerjakan frontend.
- Jangan mengerjakan Telegram bot implementation.
- Jangan mengimplementasikan business logic besar.
- Pertahankan architecture boundary yang sudah dibuat B-015.

==================================================
OBJECTIVE
==================================================

Bangun skeleton API server production-quality yang menjadi
entry point backend BotSpace.

Server harus memiliki foundation:

1. HTTP framework/server
2. bootstrap lifecycle
3. health endpoint
4. readiness endpoint jika architecture membutuhkan
5. centralized error handling
6. error envelope
7. request correlation/request ID
8. graceful shutdown
9. config integration dari B-011
10. observability integration dari B-012
11. domain/error boundary dari B-015
12. typed route structure yang mudah diperluas

Jangan membuat fitur bisnis palsu.

==================================================
1. AUDIT SEBELUM CODING
==================================================

Baca:

- ROADMAP_V2.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- AI_RULES.md
- AI_WORKFLOW.md
- PROJECT_STATUS.md
- packages/config
- packages/observability
- packages/contracts
- B-015 domain/repository code
- package.json
- pnpm-workspace.yaml

Tentukan framework HTTP berdasarkan architecture/repository.

Jangan mengganti framework hanya karena preferensi pribadi.

Jika sudah ada framework yang dipilih:
gunakan framework tersebut.

==================================================
2. SERVER BOUNDARY
==================================================

Buat boundary yang jelas:

bootstrap
  ↓
HTTP server
  ↓
routes
  ↓
application/domain
  ↓
repository ports

HTTP layer tidak boleh mengetahui detail database.

HTTP layer tidak boleh langsung menggunakan ORM.

HTTP DTO tidak boleh menjadi domain entity.

==================================================
3. CONFIG
==================================================

Gunakan config loader B-011.

Jangan membaca process.env tersebar di seluruh aplikasi.

Server harus mengambil configuration dari config boundary.

Minimal konfigurasi yang perlu dievaluasi:

- host
- port
- environment
- shutdown timeout
- logging/observability settings

Jangan menambahkan env variables yang tidak diperlukan.

==================================================
4. HEALTH
==================================================

Implementasikan endpoint health yang sederhana dan cepat.

Contoh:

GET /health

Response harus:

- deterministic
- JSON
- tidak membocorkan secret
- tidak melakukan query database berat

Jika architecture membutuhkan readiness:

GET /ready

Bedakan:

liveness
vs
readiness

Jangan menyebut service READY jika dependency wajib
belum siap.

==================================================
5. ERROR ENVELOPE
==================================================

Buat centralized error response.

Format harus konsisten.

Minimal memiliki:

- error/code
- message
- request/correlation ID

Detail internal hanya boleh muncul sesuai environment.

Jangan mengirim:

- stack trace production
- database credentials
- SQL
- environment secrets
- internal filesystem paths

Domain errors dari B-015 harus dapat dipetakan
ke HTTP response tanpa memasukkan HTTP concern
ke domain layer.

==================================================
6. REQUEST ID / CORRELATION
==================================================

Setiap request harus memiliki correlation/request ID.

Jika client mengirim ID yang valid:
gunakan sesuai security policy.

Jika tidak:
generate ID baru.

ID harus tersedia untuk:

- response header
- structured logs
- error response

Jangan log secret atau authorization credential.

==================================================
7. OBSERVABILITY
==================================================

Gunakan package observability B-012.

Integrasikan:

- request lifecycle
- error logging
- startup
- shutdown

Jangan membuat logger kedua jika B-012 sudah menyediakan
abstraction yang benar.

Log harus ringkas dan terstruktur.

==================================================
8. GRACEFUL SHUTDOWN
==================================================

Implementasikan lifecycle:

startup
→ server listening
→ request handling
→ shutdown signal
→ stop accepting requests
→ cleanup resources
→ exit

Handle setidaknya:

SIGTERM
SIGINT

Gunakan timeout agar shutdown tidak menggantung selamanya.

Jangan menggunakan process.exit secara brutal
sebelum cleanup selesai kecuali sebagai last-resort timeout.

==================================================
9. ROUTER STRUCTURE
==================================================

Pisahkan:

- server bootstrap
- router registration
- health routes
- error handler
- middleware/plugin setup

Jangan membuat satu file server raksasa.

Namun jangan over-engineer.

Target:
struktur kecil, jelas, mudah dipelihara.

==================================================
10. CONTRACTS
==================================================

Gunakan contracts package bila endpoint sudah memiliki
public contract.

Jangan membuat API contract baru yang bertentangan
dengan B-010.

Jika endpoint health belum memiliki public contract,
gunakan response internal sederhana dan dokumentasikan
keputusan tersebut.

==================================================
11. TESTS
==================================================

Buat test untuk:

- server bootstrap
- health endpoint
- readiness jika ada
- JSON response
- request ID
- error envelope
- unknown route
- graceful shutdown jika feasible
- no secret leakage
- config failure behavior

Gunakan test environment yang deterministik.

Jangan membuat test yang membutuhkan production database
untuk health endpoint kecuali architecture memang
mewajibkannya.

==================================================
12. SECURITY
==================================================

Audit:

- malformed request
- oversized request jika framework mendukung
- header handling
- error leakage
- secret leakage
- request ID injection
- unsafe logging

Jangan menambahkan authentication implementation
di B-014.

==================================================
13. PERFORMANCE
==================================================

Server foundation harus ringan.

Hindari:

- dependency besar tanpa kebutuhan
- synchronous blocking work
- database access pada liveness
- duplicate serialization
- unnecessary middleware
- unnecessary abstraction

==================================================
14. VALIDATION
==================================================

Setelah implementasi jalankan seluruh validation:

- git status
- git diff --stat
- format check
- lint
- typecheck
- import-check
- secret scan
- ownership check
- doc-link check
- build
- test

Jika ada failure:
diagnosis root cause dan perbaiki.

Jangan sekadar bypass test.

==================================================
15. GIT
==================================================

Jika semua green:

commit:

feat: establish api server skeleton

Working tree harus CLEAN.

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

B-014 RESULT

Status:
Framework:
Server Entry:
Health:
Readiness:
Error Envelope:
Request ID:
Observability:
Graceful Shutdown:
Config:
Contract Integration:
Security:
Tests:
Lint:
Typecheck:
Import Check:
Build:

Changed Files:
Commit:
Working Tree:
Push: NO

Architecture Decisions:
- ...

Problems Found:
- ...

Remaining Risks:
- ...

Next Recommended Task:
- ...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# BOTSPACE B-015
```
PROMPT: BOTSPACE B-015 — DOMAIN PRIMITIVES + REPOSITORY PORTS

ROLE:
Kimi utama — Senior Backend Architect / TypeScript Engineer.

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

IMPORTANT:
B-013 DATABASE FOUNDATION SUDAH COMPLETE.
B-010 CONTRACTS SUDAH COMPLETE.
B-011 CONFIG LOADER SUDAH COMPLETE.
B-012 OBSERVABILITY SUDAH COMPLETE.

JANGAN PUSH.
JANGAN mengerjakan B-014.
Fokus penuh B-015.

==================================================
OBJECTIVE
==================================================

Implementasikan B-015:
DOMAIN PRIMITIVES + REPOSITORY PORTS.

Tujuan task ini adalah membuat boundary domain/backend
yang kuat sebelum API server dan business use-case dibangun.

Jangan sekadar membuat interface kosong.
Audit architecture terlebih dahulu lalu implementasikan
primitive dan repository port yang benar-benar konsisten
dengan schema, contracts, roadmap, dan struktur repository.

==================================================
1. ARCHITECTURE AUDIT
==================================================

Baca terlebih dahulu:

- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- MODULES.md
- PROJECT_STATUS.md
- packages/contracts
- packages/config
- packages/observability
- packages/database / schema / migrations
- services/*
- apps/*
- package.json
- pnpm-workspace.yaml

Cari dan petakan:

- domain entities yang sudah ditentukan
- database entities B-013
- shared contracts
- existing repository interfaces
- service boundaries
- dependency direction
- ID strategy
- timestamp strategy
- error strategy
- pagination/filter conventions
- ownership rules

JANGAN mengarang domain baru jika tidak ada dasar
di architecture/roadmap/contracts.

==================================================
2. DOMAIN PRIMITIVES
==================================================

Buat primitive/value object yang memang diperlukan oleh
domain yang sudah didefinisikan.

Contoh kategori yang boleh dipertimbangkan hanya jika
didukung architecture:

- UserId
- WorkspaceId
- BotId
- AccountId
- WorkspaceMemberId
- JobId
- ApiKeyId
- ProviderId
- Status types
- pagination primitives
- timestamp/date primitives
- validated string identifiers

Primitive harus:

- type-safe
- runtime-safe jika diperlukan
- tidak bergantung pada database ORM
- tidak bergantung pada HTTP framework
- tidak bergantung pada Express/Fastify/Hono
- mudah digunakan oleh application layer
- memiliki validation yang jelas
- memiliki test

Jangan membuat value object hanya untuk menambah jumlah file.

==================================================
3. ID STRATEGY
==================================================

Ikuti keputusan architecture.

Jangan membuat UUID/random ID baru secara sembarangan.

Jika UUID/ULID adalah application concern,
implementasikan di domain/application boundary.

Database tidak boleh menjadi alasan domain
bergantung langsung pada ORM.

Pastikan ID type tidak mudah tertukar.

Contoh:

UserId tidak boleh interchangeable secara sembarangan
dengan WorkspaceId jika architecture mengharuskan
strong typing.

==================================================
4. DOMAIN TYPES
==================================================

Definisikan domain types berdasarkan entity yang benar-benar
sudah ada.

Minimal evaluasi:

- User
- Workspace
- WorkspaceMember
- Bot
- Account
- Job

Hanya implementasikan entity yang memang sudah menjadi
bagian architecture/roadmap.

Jangan membuat business logic lengkap.
B-015 fokus pada primitives dan boundary.

==================================================
5. REPOSITORY PORTS
==================================================

Buat repository ports/interface untuk domain yang relevan.

Repository port harus:

- berada pada layer domain/application yang benar
- tidak mengimpor ORM
- tidak mengimpor database client
- tidak mengimpor HTTP framework
- tidak mengetahui PostgreSQL implementation detail
- memiliki input/output type yang jelas
- memiliki error semantics yang jelas

Gunakan interface/type yang dapat diimplementasikan
oleh database adapter pada tahap berikutnya.

Jangan implementasikan PostgreSQL repository penuh
kecuali architecture memang memintanya untuk B-015.

==================================================
6. QUERY / PAGINATION CONTRACT
==================================================

Jika repository membutuhkan list/query:

buat primitive yang konsisten untuk:

- limit
- cursor/offset sesuai architecture
- sorting jika memang diperlukan
- filtering jika sudah ditentukan

Hindari membuat query DSL besar.

Prioritaskan API sederhana dan type-safe.

==================================================
7. ERROR MODEL
==================================================

Buat atau gunakan error model yang sudah ada.

Minimal bedakan secara jelas jika architecture membutuhkan:

- not found
- conflict
- validation error
- persistence error
- invalid input

Jangan expose database error mentah ke domain.

Jangan memasukkan HTTP status code ke domain layer.

==================================================
8. DEPENDENCY RULE
==================================================

WAJIB:

domain/application
        ↓
repository port
        ↓
infrastructure/database adapter

BUKAN:

domain
  ↓
Prisma/Drizzle/pg/ORM

dan bukan:

domain
  ↓
HTTP framework

Pastikan import graph sesuai architecture.

Gunakan import-check untuk membuktikannya.

==================================================
9. DATABASE ALIGNMENT
==================================================

Bandingkan hasil B-015 dengan schema B-013.

Pastikan:

- naming konsisten
- ID semantics konsisten
- nullable fields konsisten
- enum/status semantics konsisten
- timestamps konsisten
- relation semantics konsisten

Jika ada mismatch:

JANGAN langsung mengubah B-013.

Identifikasi mismatch terlebih dahulu.

Jika memang membutuhkan perubahan,
jelaskan dalam final report sebelum melakukan perubahan
yang berada di luar scope.

==================================================
10. CONTRACT ALIGNMENT
==================================================

Bandingkan dengan:

packages/contracts

Pastikan domain types tidak bertentangan dengan public/API
contracts.

Domain model dan transport contract tidak harus identik.

Jangan memaksa domain memakai DTO HTTP.

Gunakan mapper/boundary jika memang diperlukan.

==================================================
11. TESTING
==================================================

Buat test yang benar-benar menguji behavior.

Minimal:

- valid primitive diterima
- invalid primitive ditolak
- ID types tidak mudah tertukar
- repository port memiliki contract yang jelas
- validation behavior konsisten
- error semantics konsisten
- pagination primitive tervalidasi
- domain types tidak mengimpor infrastructure

Tambahkan compile-time checks jika berguna.

Jangan membuat test yang hanya memeriksa
"object exists".

==================================================
12. STATIC ARCHITECTURE CHECK
==================================================

Buat/verifikasi architecture boundary.

Cari import ilegal seperti:

- domain -> database
- domain -> ORM
- domain -> HTTP
- domain -> process.env
- domain -> infrastructure

Jika ada violation dari sebelum B-015:

jangan sembunyikan.

Audit dan perbaiki hanya jika memang bagian scope
atau dokumentasikan blocker.

==================================================
13. PERFORMANCE
==================================================

Gunakan TypeScript code yang sederhana dan cepat.

Hindari:

- dependency besar tanpa kebutuhan
- runtime reflection
- decorator-heavy architecture
- unnecessary abstraction
- generic framework layer
- duplicate validation library

Prioritaskan compile-time safety.

==================================================
14. SECURITY
==================================================

Audit:

- secret leakage
- credential types
- logging
- error serialization
- unsafe coercion
- arbitrary object input
- prototype pollution risk
- database error leakage

Domain layer tidak boleh mengetahui secret value.

==================================================
15. VALIDATION PENUH
==================================================

Setelah coding jalankan:

- git status
- git diff --stat
- format check
- lint
- typecheck
- import-check
- secret scan
- ownership check
- doc-link check
- build
- test
- frozen install validation jika tersedia

Jika ada error:
perbaiki sampai GREEN.

Jangan berhenti pada first failure.

==================================================
16. SCOPE CONTROL
==================================================

JANGAN mengerjakan:

- B-014 API server selection
- API routes
- HTTP controllers
- Telegram bot implementation
- frontend
- authentication implementation
- production deployment
- provider integration
- business workflow lengkap

B-015 hanya:

DOMAIN PRIMITIVES
+
DOMAIN TYPES
+
REPOSITORY PORTS
+
VALIDATION
+
TESTS
+
ARCHITECTURE BOUNDARY

==================================================
17. GIT
==================================================

Jika semua validation GREEN:

Working tree harus CLEAN.

Commit:

feat: establish domain primitives and repository ports

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

B-015 RESULT

Status:
Architecture Audit:
Domain Primitives:
Domain Types:
Repository Ports:
ID Strategy:
Error Model:
Pagination:
Database Alignment:
Contract Alignment:
Dependency Boundary:
Tests:
Lint:
Typecheck:
Import Check:
Build:
Security:
Changed Files:
Working Tree:
Commit:
Push: NO

Architecture Decisions:
- ...

Assumptions:
- ...

Problems Found:
- ...

Remaining Risks:
- ...

Next Recommended Task:
- ...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```

# BOTSPACE B-013 
```
PROMPT: BOTSPACE B-013 — DATABASE FOUNDATION / SCHEMA + MIGRATIONS

ROLE:
Kimi utama — BotSpace Backend Engineer.

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

CURRENT STATE:
B-012 sudah COMPLETE dan GREEN.
Working tree CLEAN.
Jangan push.

==================================================
TASK
==================================================

Kerjakan B-013:
Database schema + migrations baseline.

Ini adalah FOUNDATION TASK.
Jangan hanya membuat placeholder kosong.
Audit repository terlebih dahulu lalu implementasikan baseline
database yang benar-benar siap menjadi fondasi Phase berikutnya.

==================================================
1. AUDIT SEBELUM CODING
==================================================

Baca dan pahami:

- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- MODULES.md
- PROJECT_STATUS.md
- packages/contracts
- packages/config
- services
- apps
- package.json
- pnpm-workspace.yaml

Cari apakah repository sudah menentukan:
- database engine
- ORM/query builder
- migration tool
- schema convention
- ID strategy
- timestamp convention
- naming convention
- repository pattern

JANGAN mengganti keputusan architecture yang sudah ada.

Jika database technology belum ditentukan secara eksplisit,
pilih solusi paling minimal dan konsisten dengan repository,
bukan menambahkan stack database besar tanpa alasan.

==================================================
2. DATABASE SCHEMA
==================================================

Implementasikan schema baseline sesuai domain BotSpace.

Minimal audit kebutuhan entity yang sudah didefinisikan
di roadmap/contracts/architecture.

Jangan mengarang domain baru.

Jika entity belum cukup jelas:
- gunakan entity yang memang sudah ditentukan repository
- jangan membuat fitur bisnis baru
- dokumentasikan asumsi

Schema harus memiliki:
- primary key yang konsisten
- createdAt / updatedAt jika memang diperlukan
- foreign key yang benar
- unique constraint yang diperlukan
- index untuk lookup penting
- nullable/non-nullable yang masuk akal
- referential integrity

Hindari over-engineering.

==================================================
3. MIGRATION SYSTEM
==================================================

Buat baseline migration yang repeatable.

Pastikan:
- migration dapat dijalankan dari database kosong
- migration tidak bergantung pada data manual
- migration order deterministic
- schema dapat direproduksi
- migration test dapat dijalankan di CI/local
- tidak ada migration yang merusak source existing

Jika migration tool sudah ada, gunakan tool tersebut.

Jangan mengganti migration framework hanya demi task ini.

==================================================
4. DATABASE ACCESS LAYER
==================================================

Buat boundary database yang bersih.

Pisahkan:
- schema
- migration
- database client/connection
- repository interface/port
- implementation

Jangan membuat business logic masuk ke database layer.

Ikuti architecture:
domain/application tidak boleh bergantung langsung
pada detail database jika architecture repository
sudah menentukan dependency inversion.

Jika repository port belum waktunya dibuat,
buat hanya yang diperlukan untuk B-013.

==================================================
5. CONFIG INTEGRATION
==================================================

Gunakan config loader B-011.

Database connection/config:
- jangan membaca process.env langsung di banyak tempat
- gunakan centralized config
- validasi konfigurasi database
- jangan pernah log password/credential

Pastikan config database tetap aman.

==================================================
6. TEST
==================================================

Tambahkan test yang bermakna.

Minimal verifikasi:

1. schema dapat di-load
2. migration dapat dijalankan dari database kosong
3. migration menghasilkan schema yang diharapkan
4. constraint penting bekerja
5. repository/database boundary dapat diinisialisasi
6. invalid configuration ditolak
7. database secret tidak masuk log

Jika integration database membutuhkan service eksternal
dan repository belum memiliki test infrastructure,
gunakan test strategy yang konsisten dengan architecture.

JANGAN membuat fake test yang hanya PASS tanpa menguji behavior.

==================================================
7. PACKAGE / DEPENDENCY GOVERNANCE
==================================================

Sebelum menambah dependency:
- cek package yang sudah tersedia
- gunakan dependency existing jika memungkinkan
- jangan install duplicate ORM/database library

Jika dependency baru benar-benar diperlukan:
jelaskan alasan dan dampaknya.

Jangan mengedit pnpm-lock.yaml secara manual.

Gunakan package manager repository.

==================================================
8. DOCUMENTATION
==================================================

Update dokumentasi hanya jika diperlukan oleh B-013.

Dokumentasikan:
- database technology
- schema location
- migration command
- test command
- environment/config requirement

Jangan mengubah:
- ROADMAP.md
- ROADMAP_V2.md

kecuali task secara eksplisit membutuhkan perubahan dokumentasi
dan perubahan tersebut benar-benar diperlukan.

==================================================
9. SECURITY
==================================================

WAJIB audit:

- SQL injection boundary
- credential exposure
- database URL/password leakage
- logs
- error messages
- migration secrets
- test fixtures

Tidak boleh ada:
- password nyata
- API key
- token
- credential
- secret
di source code atau test fixture.

==================================================
10. VALIDATION
==================================================

Setelah implementasi jalankan validasi repository secara penuh:

- git status
- git diff --stat
- format check
- lint
- typecheck
- import-check
- secret scan
- ownership check
- doc-link check
- build
- test
- migration validation
- frozen install jika tersedia

Jika ada failure:
DEBUG dan perbaiki sampai GREEN.

Jangan berhenti hanya karena satu command gagal.

==================================================
11. SCOPE CONTROL
==================================================

JANGAN mengerjakan:
- B-014
- B-015
- B-016
- F-012
- frontend
- production deployment
- Docker production setup
- authentication feature
- Telegram bot feature

Tetap fokus B-013.

Namun jika dependency B-013 memang membutuhkan
perubahan kecil pada shared infrastructure,
boleh dilakukan hanya jika benar-benar diperlukan.

==================================================
12. GIT
==================================================

Jika semua validation GREEN:

git status harus CLEAN.

Commit:

feat: add database schema and migrations baseline

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

B-013 RESULT

Status:
Database Technology:
Schema:
Migration:
Database Boundary:
Repositories/Ports:
Config Integration:
Tests:
Migration Validation:
Lint:
Typecheck:
Import Check:
Build:
Security:
Changed Files:
Working Tree:
Commit:
Push: NO

Architecture Decisions:
- ...

Assumptions:
- ...

Problems Found:
- ...

Next Task:
- ...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# Laptop — B-012
```
PROMPT: BOTSPACE B-012 — OBSERVABILITY BASELINE

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
/root/botspace-backend

BRANCH:
backend-dev

B-011 sudah COMPLETE dan GREEN.

Latest commit:
2c3b633 — feat: add backend config loader

TASK:
B-012 — Observability baseline — real logger + redaction

Baca:
- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- packages/config
- existing services/apps
- existing scripts

Implementasikan observability baseline sesuai architecture yang sudah ada.

TUJUAN:
- logger terpusat
- structured logging yang ringan
- level log yang jelas
- aman untuk production
- secret/token/password/API key wajib diredaсt
- tidak boleh membocorkan environment variable
- error logging tetap informatif tanpa secret
- jangan menyebarkan console.log secara sembarangan

Jangan membuat framework logging baru jika repository sudah memiliki pilihan yang sesuai.

Hindari dependency baru jika tidak benar-benar diperlukan.

SECURITY:
Jangan pernah mencetak:
- API key
- BOT token
- password
- secret
- authorization header
- credential
- nilai environment variable sensitif

Tambahkan redaction test untuk memastikan secret tidak muncul
dalam output logger.

Jangan mengubah frontend.

Jangan mengubah:
- ROADMAP.md
- ROADMAP_V2.md
- pnpm-lock.yaml secara manual
- packages/contracts kecuali benar-benar diperlukan oleh B-012

VALIDATION:
Jalankan:
- git status
- git diff --stat
- format check
- lint
- typecheck
- import-check
- build
- test

Pastikan workspace tetap GREEN.

Jika ada dependency baru, jelaskan alasannya.

Jika requirement B-012 tidak jelas, STOP dan laporkan.

GIT:
Jika berhasil:
- commit perubahan B-012
- gunakan commit message:
  feat: add observability baseline

JANGAN PUSH.

FINAL REPORT:
B-012 RESULT
Status:
Changed Files:
Logger:
Redaction:
Tests:
Lint:
Typecheck:
Import Check:
Build:
Working Tree:
Commit:
Push: NO
Next Task:

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# Laptop — B-011
```

PROMPT: BOTSPACE B-011 — CONFIG LOADER + ENV VALIDATION

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
/root/botspace-backend

BRANCH:
backend-dev

CURRENT STATUS:
B-001 ✅
B-002 ✅
B-003 ✅ locally verified
B-004 ✅
B-005 ✅
B-010 ✅

Latest commit:
3df80d0 — feat: establish backend contracts

B-010:
- Contract Boundary: PASS
- Frontend Consumption Ready: YES
- Working Tree: CLEAN
- Push: NO

==================================================
TASK
==================================================

B-011 — Config Loader with ENV Validation.

Baca terlebih dahulu:

- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- package.json
- existing config/environment files
- existing scripts
- services/apps structure

Jangan langsung coding.

Audit konfigurasi yang sudah ada dan tentukan acceptance criteria
B-011 dari ROADMAP_V2.md.

==================================================
TUJUAN
==================================================

Implementasikan config loader backend yang:

- typed
- terpusat
- deterministic
- memvalidasi environment variables
- fail-fast untuk konfigurasi wajib
- tidak membocorkan secret
- mudah digunakan oleh service backend
- tidak bergantung pada frontend
- tidak mengandung business logic

Ikuti architecture repository yang sudah ada.

Jangan membuat konfigurasi baru jika mekanisme yang benar sudah ada.

==================================================
SECURITY
==================================================

Sangat penting:

Jangan pernah:
- print API key
- print BOT_TOKEN
- print password
- print secret
- commit .env
- memasukkan secret ke test fixture
- memasukkan secret ke README
- memasukkan secret ke source code

Error validation boleh menyebut NAMA environment variable,
tetapi jangan pernah menampilkan NILAINYA.

Gunakan .env.example jika memang sudah tersedia.

==================================================
VALIDATION RULES
==================================================

Audit environment variables yang memang diperlukan repository.

Pisahkan:

REQUIRED
OPTIONAL
DEFAULT

Jangan mengarang environment variable.

Jika requirement B-011 tidak jelas:
STOP dan laporkan.

Config harus gagal dengan pesan yang jelas jika REQUIRED env
tidak tersedia.

Config harus tetap aman ketika OPTIONAL env tidak tersedia
jika memang diperbolehkan oleh architecture.

==================================================
IMPLEMENTATION
==================================================

Gunakan TypeScript dengan strict typing.

Hindari:
- any
- duplicate config parsing
- process.env tersebar di seluruh business logic
- silent fallback untuk required secret
- hardcoded secret
- dependency baru tanpa alasan

Jika repository sudah memiliki validation library:
gunakan yang sudah ada.

Jangan menambahkan library baru hanya untuk validasi sederhana
jika repository sudah mempunyai mekanisme yang sesuai.

==================================================
TESTING
==================================================

Tambahkan test untuk behavior config yang memang diperlukan.

Minimal pertimbangkan:

1. required env tersedia → PASS
2. required env hilang → FAIL
3. optional env → sesuai default/optional rule
4. secret tidak bocor dalam error
5. type hasil config benar

Gunakan environment test yang aman.

Jangan menggunakan secret asli.

==================================================
WORKTREE SAFETY
==================================================

Hanya bekerja di:

/root/botspace-backend

Jangan menyentuh frontend.

Jangan mengubah:

- ROADMAP.md
- ROADMAP_V2.md
- pnpm-lock.yaml secara manual
- packages/contracts/ kecuali B-011 benar-benar membutuhkan perubahan
- business logic yang bukan dependency B-011

Jika shared contract harus berubah:
STOP dan laporkan sebelum melakukan perubahan.

==================================================
VALIDATION
==================================================

Setelah implementasi jalankan:

git status
git diff --stat
git diff

Kemudian:

pnpm install --frozen-lockfile

format check
lint
typecheck
import-check
build
test

Pastikan seluruh workspace tetap green.

==================================================
GIT
==================================================

Jika B-011 berhasil:

git add <B-011 files>

git commit -m "feat: add backend config loader"

JANGAN PUSH.

Jika blocked karena requirement tidak jelas:
jangan commit.

==================================================
FINAL REPORT
==================================================

BOTSPACE B-011 RESULT

Task:
B-011

Status:
COMPLETE / PARTIAL / BLOCKED

Config Variables Audited:
...

Required:
...

Optional:
...

Defaults:
...

Implementation:
...

Security:
...

Tests:
...

Validation:
- Frozen Install:
- Format:
- Lint:
- Typecheck:
- Import Check:
- Build:
- Test:

Changed Files:
- ...

Commit:
...

Working Tree:
CLEAN / DIRTY

Push:
NO

Next Task:
...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.

```

# Prompt B-010
```
PROMPT: BOTSPACE B-010 — BACKEND CONTRACTS FOUNDATION

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
/root/botspace-backend

BRANCH:
backend-dev

==================================================
CURRENT STATUS
==================================================

Phase 0 foundation:
B-001 ✅
B-002 ✅
B-003 ✅ locally verified
B-004 ✅
B-005 ✅

Latest commit:
11953bf — chore: resolve modules path governance

B-005 validation:
- Typecheck PASS
- Import-check PASS
- Secret scan PASS
- Ownership check PASS
- Doc-link check PASS
- Build PASS
- Test PASS — 28 tests
- Workspace resolution PASS

Working Tree:
CLEAN

Push:
NO

==================================================
TASK
==================================================

B-010 — Backend Contracts.

Baca terlebih dahulu:

- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- packages/contracts/
- MODULES.md
- FINAL_ARCHITECTURE.md
- FINAL_STRUCTURE.md
- IMPLEMENTATION_SEQUENCE.md

Jangan langsung coding.

Pertama audit kondisi packages/contracts/ saat ini.

Tentukan:
- contract apa yang sudah ada
- contract apa yang belum ada
- consumer yang sudah menggunakan contract
- dependency B-010 yang sebenarnya
- acceptance criteria B-010 dari ROADMAP_V2.md

Gunakan ROADMAP_V2.md sebagai source of truth.

==================================================
TUJUAN B-010
==================================================

Implementasikan B-010 sesuai definisi repository.

Contract harus menjadi boundary resmi antara backend dan frontend.

Jangan membuat contract berdasarkan tebakan fitur.

Jika roadmap menyebut contract tertentu, implementasikan contract tersebut.

Jika ada contract yang sudah tersedia dan valid:
JANGAN membuat duplicate.

==================================================
ATURAN ARSITEKTUR
==================================================

packages/contracts/ adalah shared contract boundary.

Contract harus:
- typed
- reusable
- jelas
- stabil
- tidak bergantung pada implementation detail backend
- tidak bergantung pada UI frontend
- tidak mengandung secret
- tidak mengandung database implementation detail

Jangan menaruh business logic backend di packages/contracts/.

Jangan membuat API client production di contracts.

Jangan membuat mock production sebagai pengganti backend.

==================================================
SHARED FILE SAFETY
==================================================

Boleh menyentuh:

packages/contracts/

dan file lain hanya jika B-010 memang membutuhkannya.

Jangan mengubah:

- ROADMAP.md
- ROADMAP_V2.md
- pnpm-lock.yaml secara manual
- frontend worktree
- apps/web UI
- business logic backend yang bukan dependency B-010

Jika membutuhkan perubahan shared file di luar scope:
STOP dan laporkan.

==================================================
QUALITY
==================================================

Gunakan TypeScript yang paling jelas dan maintainable.

Hindari:
- any
- duplicate types
- string literal yang tersebar
- circular dependency
- backend-specific imports di contracts
- frontend-specific imports di contracts

Periksa apakah repository sudah mempunyai convention untuk:
- request types
- response types
- error types
- pagination
- IDs
- enums/status
- API envelope

Ikuti convention yang sudah ada.

Jangan menciptakan convention baru jika repository sudah memiliki satu.

==================================================
VALIDATION
==================================================

Setelah implementasi:

git status
git diff --stat
git diff

Kemudian jalankan validation:

pnpm install --frozen-lockfile

format check
lint
typecheck
import-check
build
test

Pastikan seluruh workspace tetap valid.

Pastikan packages/contracts dapat dikonsumsi oleh frontend tanpa
membuat dependency cycle.

Jika ada test khusus contracts, jalankan juga.

==================================================
GIT
==================================================

Jika B-010 berhasil:

git add <B-010 files>

git commit -m "feat: establish backend contracts"

JANGAN PUSH.

Jika tidak ada perubahan karena B-010 ternyata sudah terpenuhi:
jangan membuat commit kosong.

Jika B-010 BLOCKED karena requirement roadmap tidak jelas:
STOP dan laporkan, jangan menebak.

==================================================
FINAL REPORT
==================================================

BOTSPACE B-010 RESULT

Task:
B-010

Status:
COMPLETE / PARTIAL / BLOCKED

Roadmap Definition:
...

Existing Contracts:
...

New Contracts:
...

Architecture Decision:
...

Changed Files:
- ...

Validation:
- Frozen Install:
- Format:
- Lint:
- Typecheck:
- Import Check:
- Build:
- Test:

Contract Boundary:
PASS / FAIL

Frontend Consumption Ready:
YES / NO

Backend Files Changed:
...

Shared Files Changed:
...

ROADMAP.md:
NOT MODIFIED

ROADMAP_V2.md:
NOT MODIFIED

Commit:
...

Working Tree:
CLEAN / DIRTY

Push:
NO

Next Task:
...

IMPORTANT:
B-010 adalah dependency untuk F-012.
Jangan mengerjakan F-012 di backend.
Jangan membuat API endpoint production kecuali memang termasuk
scope B-010.

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
#B-005
```
PROMPT: BOTSPACE B-005 — RESOLVE MODULES PATH GOVERNANCE

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
/root/botspace-backend

BRANCH:
backend-dev

CURRENT STATUS:

B-001 ✅
B-002 ✅
B-003 ✅ locally verified
B-004 ✅

Latest commit:
282d49c — chore: improve governance scripts

Working Tree:
CLEAN

Push:
NO

==================================================
TASK
==================================================

B-005 — Resolve modules/path governance discrepancy.

Baca terlebih dahulu:

- ROADMAP_V2.md
- AI_TASKS.md
- MODULES.md
- pnpm-workspace.yaml
- struktur repository aktual
- FINAL_STRUCTURE.md
- FINAL_ARCHITECTURE.md
- CONTRIBUTING.md
- scripts/README.md

Jangan langsung membuat folder modules/.

==================================================
PROBLEM
==================================================

Saat audit ditemukan:

pnpm-workspace.yaml memasukkan:

modules/*

tetapi folder:

modules/

tidak ada di repository.

Ini menyebabkan discrepancy antara workspace configuration dan struktur
repository aktual.

==================================================
TUJUAN
==================================================

Tentukan berdasarkan dokumentasi dan repository:

APAKAH:

A. modules/ memang merupakan bagian resmi arsitektur dan harus dibuat,

ATAU

B. modules/* adalah konfigurasi lama/tidak digunakan dan harus
dihapus/diperbaiki,

ATAU

C. ada aturan lain yang sudah ditentukan di MODULES.md / architecture
yang harus diikuti.

Jangan mengambil keputusan berdasarkan asumsi.

Gunakan dokumentasi repository sebagai source of truth.

==================================================
ATURAN KETAT
==================================================

- Jangan mengubah business logic.
- Jangan membuat feature baru.
- Jangan membuat module dummy hanya agar check hijau.
- Jangan membuat folder kosong sebagai workaround.
- Jangan menghapus konfigurasi tanpa bukti bahwa konfigurasi tersebut
  obsolete.
- Jangan mengubah ROADMAP.md.
- Jangan mengubah ROADMAP_V2.md.
- Jangan mengubah pnpm-lock.yaml secara manual.
- Jangan menyentuh frontend.
- Jangan push.

Jika keputusan membutuhkan klarifikasi arsitektur:
STOP dan laporkan, jangan menebak.

==================================================
AUDIT
==================================================

Periksa:

1. pnpm-workspace.yaml
2. MODULES.md
3. FINAL_STRUCTURE.md
4. FINAL_ARCHITECTURE.md
5. package.json
6. semua workspace/package yang benar-benar ada
7. apakah ada referensi "modules/*" di repository
8. apakah CI/governance script mengharapkan modules/
9. apakah modules/ pernah direncanakan tetapi belum dibuat

Gunakan pencarian repository untuk menemukan semua referensi
"modules/" dan "modules/*".

==================================================
IMPLEMENTATION
==================================================

Setelah bukti cukup:

Jika modules/* memang salah:
perbaiki konfigurasi secara minimal.

Jika modules/ memang resmi:
ikuti struktur yang sudah ditentukan dokumentasi.
Jangan membuat implementasi bisnis.

Jika hanya dokumentasi yang salah:
perbaiki dokumentasi yang memang menjadi scope B-005.

Jika ada konflik antar dokumen:
JANGAN memilih secara diam-diam.
Laporkan konflik tersebut.

==================================================
VALIDATION
==================================================

Setelah perubahan, jalankan validation yang relevan.

Minimal:

pnpm install --frozen-lockfile

Kemudian:

format check
lint
typecheck
import-check
build
test

Pastikan workspace resolution tidak lagi menghasilkan discrepancy.

Periksa:

git status
git diff --stat
git diff

Pastikan tidak ada perubahan tidak sengaja.

==================================================
GIT
==================================================

Jika B-005 berhasil diselesaikan:

commit:

chore: resolve modules path governance

JANGAN PUSH.

Jika tidak ada perubahan yang diperlukan:
jangan membuat commit kosong.

Jika B-005 BLOCKED karena konflik dokumentasi:
jangan commit dan jangan push.

==================================================
FINAL REPORT
==================================================

BOTSPACE B-005 RESULT

Task:
B-005

Status:
COMPLETE / BLOCKED

Root Cause:
...

Evidence:
...

Decision:
KEEP modules/*
atau
REMOVE/CHANGE modules/*
atau
DOCUMENTATION ISSUE
atau
NEEDS CLARIFICATION

Implementation:
...

Changed Files:
- ...

Validation:
- Frozen Install:
- Format:
- Lint:
- Typecheck:
- Import Check:
- Build:
- Test:
- Workspace Resolution:

Commit:
...

Working Tree:
CLEAN / DIRTY

Push:
NO

Next Recommended Task:
...

IMPORTANT:
Jangan membuat folder modules/ hanya untuk menghilangkan error.
Keputusan harus berdasarkan architecture dan governance repository.

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# PROMPT: BOTSPACE B-004 — GOVERNANCE SCRIPTS
```
PROMPT: BOTSPACE B-004 — GOVERNANCE SCRIPTS

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
/root/botspace-backend

BRANCH:
backend-dev

TASK:
B-004 — Governance Scripts

STATUS SEBELUMNYA:
B-001 ✅
B-002 ✅
B-003 ✅ locally verified

Commit terakhir B-003:
a650147

Baca ROADMAP_V2.md dan AI_TASKS.md sebelum bekerja.

==================================================
ATURAN
==================================================

- Hanya bekerja di /root/botspace-backend.
- Jangan menyentuh /root/botspace-frontend.
- Jangan bekerja di /root/botspace/main.
- Jangan push.
- Jangan mengubah ROADMAP.md.
- Jangan mengubah ROADMAP_V2.md.
- Jangan mengubah pnpm-lock.yaml secara manual.
- Jangan mengubah business logic.
- Jangan membuat feature produk.
- Jangan melakukan refactor di luar scope B-004.

==================================================
TUJUAN
==================================================

Selesaikan B-004 sesuai requirements ROADMAP_V2.md.

Audit terlebih dahulu governance/validation scripts yang sudah ada.

Identifikasi:
- script yang sudah tersedia
- script yang belum tersedia
- script yang duplicate
- script yang tidak konsisten
- command yang digunakan CI
- command yang digunakan local validation

Jangan mengarang requirement.

Gunakan repository aktual sebagai source of truth.

==================================================
IMPLEMENTATION
==================================================

Jika B-004 memang membutuhkan perubahan script:

- lakukan perubahan seminimal mungkin
- pertahankan command yang sudah bekerja
- jangan mengubah business logic
- jangan mengubah dependency jika tidak diperlukan
- jangan merusak B-001/B-002/B-003

Pastikan governance scripts dapat digunakan secara reproducible.

==================================================
VALIDATION
==================================================

Setelah perubahan:

git status

Kemudian jalankan validation yang relevan dengan B-004.

Minimal pastikan command yang disentuh:
- dapat dijalankan
- exit code benar
- tidak menghasilkan perubahan tidak sengaja

Jika memungkinkan jalankan kembali:
- format check
- lint
- typecheck
- import-check
- build
- test

Jangan melakukan prettier write repo-wide tanpa scope yang sudah ditentukan.

==================================================
GIT
==================================================

Periksa:

git diff --stat
git diff

Pastikan hanya perubahan B-004.

Jika valid:

git add <files>
git commit -m "chore: improve governance scripts"

JANGAN PUSH.

==================================================
FINAL OUTPUT
==================================================

BOTSPACE B-004 RESULT

Branch:
backend-dev

Audit:
...

Implemented:
...

Validation:
...

Changed Files:
- ...

Commit:
...

Working Tree:
...

Errors:
...

Next Task:
...

Push:
NO

WAIT FOR NEXT INSTRUCTION.


```
#
```
PROMPT: BOTSPACE B-003 — FIRST GREEN CI VERIFICATION

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

TASK:
B-003 — Verify First Green CI Run.

B-001 dan B-002 sudah selesai:

B-001:
- pnpm-lock.yaml generated
- commit: f4c3f95

B-002:
- validation gates PASS
- commit: a8b194e
- prettier governance resolved
- working tree clean

Sekarang lanjut B-003 sesuai ROADMAP_V2.md.

==================================================
TUJUAN
==================================================

Memastikan GitHub Actions CI benar-benar menjalankan validation foundation yang sama dengan local validation.

CI harus mencakup, sesuai repository aktual:

1. install
2. format check
3. lint
4. typecheck
5. import-check
6. build
7. test

Jangan mengarang command. Gunakan scripts/config yang benar-benar ada.

==================================================
ATURAN
==================================================

- Hanya bekerja di /root/botspace-backend.
- Branch harus backend-dev.
- Jangan menyentuh /root/botspace-frontend.
- Jangan bekerja di /root/botspace/main.
- Jangan mengubah business logic.
- Jangan mengerjakan P2 Core Backend.
- Jangan mengubah ROADMAP.md.
- Jangan mengubah ROADMAP_V2.md.
- Jangan mengubah pnpm-lock.yaml secara manual.
- Jangan melakukan dependency upgrade.
- Jangan membuat workaround untuk membuat CI hijau.
- Jangan push tanpa instruksi eksplisit dari user.

==================================================
LANGKAH 1 — AUDIT CI
==================================================

Periksa:

.github/workflows/ci.yml

Periksa juga:

package.json
pnpm-workspace.yaml
scripts
turbo.json
tsconfig
Prettier configuration
.prettierignore

Pastikan workflow menggunakan lockfile secara reproducible.

Pastikan CI tidak diam-diam melakukan hal yang berbeda dari local validation.

==================================================
LANGKAH 2 — VALIDASI WORKFLOW
==================================================

Periksa:

- trigger
- permissions
- Node version
- pnpm version
- install mode
- frozen-lockfile
- cache
- working directory
- format check
- lint
- typecheck
- import-check
- build
- test

Pastikan urutannya masuk akal.

==================================================
LANGKAH 3 — JANGAN MERUSAK GOVERNANCE
==================================================

Jangan menjalankan:

prettier --write .

secara membabi buta.

Jangan memformat:

- ROADMAP.md
- ROADMAP_V2.md
- generated files
- frozen artifacts
- pnpm-lock.yaml

Gunakan scope format yang sudah diselesaikan pada B-002.

==================================================
LANGKAH 4 — LOCAL CI EQUIVALENCE
==================================================

Jika memungkinkan, jalankan command yang sama/ekuivalen dengan CI secara lokal.

Pastikan:

pnpm install --frozen-lockfile

dan seluruh gate:

format-check
lint
typecheck
import-check
build
test

PASS.

Jika semua sudah PASS, jangan mengubah source code hanya untuk B-003.

==================================================
LANGKAH 5 — CI TRIGGER
==================================================

Periksa apakah first green CI dapat diverifikasi tanpa push.

Jika repository/environment menyediakan cara lokal untuk menjalankan workflow, gunakan cara tersebut.

Jika GitHub Actions hanya dapat diverifikasi setelah push:

JANGAN PUSH.

Berhenti setelah audit dan tampilkan:

"CI trigger requires remote push; push not performed."

Jangan membuat asumsi bahwa CI sudah hijau hanya karena local validation hijau.

==================================================
LANGKAH 6 — CHANGES
==================================================

Jika ci.yml memang salah dan perlu diperbaiki:

- ubah hanya bagian yang benar-benar diperlukan
- jangan mengubah business logic
- jalankan validation ulang
- tampilkan git diff

Jika ci.yml sudah benar:

JANGAN mengubahnya.

==================================================
GIT
==================================================

Setelah selesai:

git status
git diff --stat
git log -3 --oneline

Jika tidak ada perubahan:
jangan commit.

Jika ada perubahan CI yang memang diperlukan:
commit dengan pesan:

ci: verify foundation validation workflow

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

BOTSPACE B-003 RESULT

Branch:
backend-dev

CI Workflow:
PASS/FAIL

Trigger:
...

Node:
...

pnpm:
...

Frozen Install:
PASS/FAIL

Format Check:
PASS/FAIL

Lint:
PASS/FAIL

Typecheck:
PASS/FAIL

Import Check:
PASS/FAIL

Build:
PASS/FAIL

Test:
PASS/FAIL

Local CI Equivalent:
PASS/FAIL

Remote GitHub Actions:
VERIFIED / NOT VERIFIED

Push:
NO

Changed Files:
- ...

Commit:
- ...

P1.003:
COMPLETE / BLOCKED

Reason:
...

Next Recommended Task:
...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
#
```
PROMPT: BOTSPACE B-002 — RESOLVE PRETTIER GOVERNANCE BLOCKER

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

B-002 sebelumnya gagal hanya pada:
prettier --check

Hasil:
- 116 files memiliki formatting mismatch
- tidak ada source code yang berubah
- working tree tetap clean
- B-001 lockfile sudah benar
- jangan push

TUGAS SEKARANG:
Audit dan selesaikan masalah GOVERNANCE/FORMAT CHECK agar B-002 dapat berjalan dengan benar.

ATURAN SANGAT PENTING:

1. Jangan mengubah business logic.
2. Jangan melakukan refactor source code.
3. Jangan mengubah ROADMAP.md.
4. Jangan mengubah ROADMAP_V2.md.
5. Jangan mengubah pnpm-lock.yaml secara manual.
6. Jangan menyentuh frontend worktree.
7. Jangan melakukan push.
8. Jangan menjalankan prettier --write ke seluruh repository secara membabi buta.

Audit terlebih dahulu:

- prettier config
- .prettierignore
- package.json scripts
- workspace configuration
- generated files
- frozen documentation
- files yang memang seharusnya diformat
- files yang memang harus dikecualikan

Tujuan:
Tentukan SCOPE FORMAT yang benar berdasarkan repository dan governance yang sudah ada.

Jika perlu membuat atau memperbaiki .prettierignore/config/script, lakukan hanya jika benar-benar sesuai governance repository.

Setelah scope benar:

1. jalankan prettier check pada scope yang benar
2. jalankan format check
3. jalankan lint
4. jalankan typecheck
5. jalankan import-check jika tersedia
6. jalankan build
7. jalankan test

Jangan memformat:
- ROADMAP.md
- generated/frozen artifacts
- pnpm-lock.yaml
- file yang memang dikecualikan oleh governance

Jika source files memang wajib diformat, hanya format file yang masuk scope resmi.

Setelah selesai:

git status
git diff --stat
git diff

Pastikan perubahan hanya governance/formatting yang memang diperlukan.

Jika semua PASS, commit perubahan B-002 dengan pesan yang sesuai.

JANGAN PUSH.

FINAL OUTPUT:

B-002 RESULT
Prettier Scope:
Format Check:
Lint:
Typecheck:
Import Check:
Build:
Test:
P1.003:
Changed Files:
Commit:
Working Tree:
Errors:
Next Task:

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# LAPTOP — Kimi utama — B-002
```
PROMPT: BOTSPACE B-002 — FULL FOUNDATION VALIDATION

Kamu adalah Kimi utama untuk BotSpace BACKEND.

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

TASK:
B-002 — Full local validation suite untuk menutup gate P1.003.

Baca ROADMAP_V2.md dan PROJECT_STATUS.md terlebih dahulu.

==================================================
ATURAN
==================================================

- Hanya bekerja di /root/botspace-backend.
- Jangan menyentuh /root/botspace-frontend.
- Jangan bekerja di /root/botspace/main.
- Jangan mengerjakan business feature.
- Jangan melakukan refactor source code.
- Jangan mengubah frontend.
- Jangan mengubah ROADMAP.md lama.
- Jangan mengubah pnpm-lock.yaml secara manual.
- Jangan mengubah dependency kecuali validation membuktikan ada masalah dependency yang memang menjadi blocker.
- Jangan melakukan push.
- Jangan melakukan perubahan di luar scope B-002.

B-001 sudah selesai dan pnpm-lock.yaml sudah di-commit.

==================================================
TUJUAN
==================================================

Menjalankan validation lengkap untuk memastikan foundation repository benar-benar siap menuju P2 Core Backend.

Jalankan validation berdasarkan script dan konfigurasi repository AKTUAL.

Jangan mengarang command yang tidak tersedia.

==================================================
VALIDATION ORDER
==================================================

Mulai dari:

1. git status
2. git branch --show-current
3. pastikan branch = backend-dev
4. pastikan working tree bersih

Kemudian periksa scripts package.json/workspace.

Jalankan validation yang memang tersedia:

- pnpm install --frozen-lockfile
- pnpm format:check / equivalent jika tersedia
- pnpm lint
- pnpm typecheck
- import-check jika tersedia
- pnpm build
- pnpm test

Jika repository memiliki command berbeda, gunakan command aktual repository.

Jalankan secara berurutan agar root cause mudah diketahui.

==================================================
ERROR HANDLING
==================================================

Jika suatu validation gagal:

1. Catat command.
2. Catat error.
3. Tentukan apakah:
   - environment issue
   - dependency issue
   - configuration issue
   - existing code issue
   - test issue
   - unrelated issue

JANGAN langsung memperbaiki source code.

B-002 adalah validation task.

Jika error merupakan blocker nyata yang memang termasuk scope B-002 dan dapat diperbaiki tanpa menyentuh business logic, jelaskan terlebih dahulu dalam hasil.

Jangan melakukan perubahan besar hanya agar test menjadi hijau.

==================================================
P1.003 GATE
==================================================

Periksa apakah hasil validation cukup untuk menyatakan:

P1.003 = COMPLETE

Jangan menyatakan COMPLETE jika masih ada gate yang gagal.

Khusus:

- frozen lockfile
- lint
- typecheck
- import-check
- build
- test

harus dibandingkan dengan requirement repository aktual.

==================================================
GIT SAFETY
==================================================

Setelah validation:

git status
git diff --stat

Jika validation tidak mengubah file:
working tree harus tetap clean.

Jika command menghasilkan generated files:
identifikasi dan jangan commit file sementara tanpa alasan.

Jangan membuat commit jika tidak ada perubahan yang diperlukan.

Jika ada perubahan yang memang diperlukan dalam scope B-002, tampilkan dulu detailnya sebelum commit.

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

Tampilkan:

BOTSPACE B-002 RESULT

Branch:
backend-dev

B-001:
PASS

Frozen Install:
PASS/FAIL

Format Check:
PASS/FAIL/N/A

Lint:
PASS/FAIL/N/A

Typecheck:
PASS/FAIL/N/A

Import Check:
PASS/FAIL/N/A

Build:
PASS/FAIL/N/A

Test:
PASS/FAIL/N/A

P1.003 Gate:
PASS/FAIL

Working Tree:
CLEAN/DIRTY

Changed Files:
- ...

Errors:
- ...

Root Causes:
- ...

Recommended Next Task:
- ...

JANGAN PUSH.
WAIT FOR NEXT INSTRUCTION.


```
#
```

PROMPT: BOTSPACE B-001 — GENERATE PNPM LOCKFILE

Kamu bekerja sebagai Kimi utama untuk BotSpace BACKEND.

WORKTREE:
 /root/botspace-backend

BRANCH:
 backend-dev

TASK:
 B-001 — Generate & commit pnpm-lock.yaml

Baca ROADMAP_V2.md terlebih dahulu dan ikuti assignment B-001.

TUJUAN:
Menyelesaikan blocker P1.003 dengan menghasilkan pnpm-lock.yaml yang valid dan reproducible.

ATURAN:
- Hanya bekerja di /root/botspace-backend.
- Jangan berpindah ke /root/botspace.
- Jangan menyentuh /root/botspace-frontend.
- Jangan mengubah ROADMAP.md lama.
- Jangan mengerjakan feature/backend lain.
- Jangan melakukan refactor business logic.
- Jangan mengubah dependency version kecuali benar-benar diperlukan untuk menghasilkan lockfile.
- Jangan menghapus file.
- Jangan mengubah source code.
- Jangan mengubah frontend.
- Jangan mengubah shared files selain yang memang diperlukan untuk B-001.
- Jika menemukan masalah di luar scope B-001, catat saja dan jangan memperbaikinya.

LANGKAH:

1. Pastikan lokasi:
   pwd

2. Pastikan branch:
   git branch --show-current

Harus:
backend-dev

3. Periksa kondisi:
   git status

Working tree harus bersih sebelum mulai.

4. Baca:
   - ROADMAP_V2.md
   - package.json
   - pnpm-workspace.yaml
   - konfigurasi package/workspace yang relevan

5. Gunakan package manager yang sesuai dengan repository.

6. Jalankan proses install/resolution yang diperlukan untuk menghasilkan:
   pnpm-lock.yaml

7. Pastikan lockfile mencakup workspace/package yang benar.

8. Jalankan validasi yang relevan untuk B-001.

Minimal pastikan:
   pnpm install --frozen-lockfile

dapat digunakan setelah lockfile tersedia.

Jika frozen install pertama membutuhkan kondisi khusus, jelaskan penyebabnya dan jangan mengakali dependency.

9. Periksa git diff.

Pastikan perubahan B-001 tidak menyentuh source code secara tidak sengaja.

10. Jalankan pemeriksaan akhir:
   git status
   git diff --stat
   git diff -- pnpm-lock.yaml

11. Jika hasil valid dan hanya perubahan B-001 yang benar, commit:

   git add pnpm-lock.yaml
   git commit -m "chore: generate pnpm lockfile"

12. Setelah commit, verifikasi:

   git status
   git log -1 --oneline

EXPECTED RESULT:

- pnpm-lock.yaml berhasil dibuat.
- lockfile valid.
- repository tetap konsisten.
- tidak ada perubahan business logic.
- tidak ada perubahan frontend.
- commit B-001 berhasil.
- working tree clean.

JANGAN PUSH.

Jika ada error yang membuat B-001 tidak dapat diselesaikan, jangan melakukan workaround berbahaya. Tampilkan error asli, root cause, dan tindakan yang diperlukan.

FINAL OUTPUT:

================================
BOTSPACE B-001 RESULT
================================

Branch:
Status:
Lockfile:
Validation:
Commit:
Working Tree:

Changed Files:
- ...

Errors:
- ...

Next Recommended Task:
- ...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.

```
