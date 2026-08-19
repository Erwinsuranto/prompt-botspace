

# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# Prompt: B-040 — Prepare Complete Approval Package, Then Re-Audit
```

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

Repository saat ini sudah diaudit dan validation terakhir PASS.

Status:

- B-030 Workspace API/Contract: DONE
- B-070 Storage Adapter: DONE
- B-071 File/Share contract: DONE
- B-071 File/Share API: DONE
- B-071 production wiring: DONE
- SecretResolver application boundary: DONE
- Infrastructure verification yang dapat dilakukan dari environment: DONE
- Security review terakhir: PASS
- Working tree: CLEAN
- Local SHA == remote SHA
- Tidak ada perubahan source implementation baru yang menunggu commit.

Current blocker:

B-040 Telegram Account Connection
= BLOCKED

ADR-011 sudah dibuat.

==================================================
ATURAN PALING PENTING
==================================================

JANGAN IMPLEMENTASIKAN B-040 SECARA SPECULATIVE.

JANGAN:

- memilih authentication mechanism tanpa approval,
- membuat Telegram polling,
- membuat Telegram webhook,
- membuat Telegram connector,
- membuat session persistence,
- membuat credential storage,
- mengubah BotInstallation.status,
- membuat provider runtime,
- mengarang Telegram API contract,
- mengarang lifecycle state machine,
- mengarang revoke/disconnect behavior,
- mengarang API version,
- mengarang runtime handoff boundary.

JANGAN menganggap keputusan arsitektur sudah disetujui hanya karena
implementation tersebut terlihat masuk akal.

B-040 hanya boleh berubah menjadi READY setelah keputusan manusia
benar-benar tersedia.

==================================================
TUJUAN RUN INI
==================================================

Karena B-040 masih membutuhkan human approval, gunakan run ini untuk
menyiapkan APPROVAL PACKAGE B-040/ADR-011 secara lengkap.

Tujuan:

1. Audit seluruh evidence repository.
2. Tentukan keputusan apa saja yang benar-benar diperlukan.
3. Jangan membuat keputusan atas nama owner.
4. Susun opsi yang tersedia.
5. Jelaskan konsekuensi setiap opsi.
6. Tunjukkan dependency terhadap existing architecture.
7. Tunjukkan bagian mana yang sudah fixed oleh repository.
8. Tunjukkan bagian mana yang masih membutuhkan keputusan manusia.
9. Buat dokumen approval yang bisa langsung diberikan kepada:
   - Architecture owner
   - Telegram/provider owner
   - Security owner
   - Deployment owner
10. Setelah package selesai, lakukan re-audit roadmap untuk memastikan
    tidak ada task independen lain yang ternyata READY.

==================================================
BAGIAN 1 — AUDIT ADR-011
==================================================

Baca:

- ADR-011
- ADR terkait authentication
- ADR terkait provider/runtime
- `docs/architecture/DECISIONS.md`
- `AI_CONTEXT.md`
- `AI_TASKS.md`
- `PROJECT_STATUS.md`
- `ROADMAP_V2.md`
- `CHANGELOG.md`

Cari semua reference yang berhubungan dengan:

- Telegram account
- provider account
- authentication
- credentials
- session
- connection state
- disconnect
- revoke
- runtime handoff
- BotInstallation
- provider lifecycle
- deployment secret boundary.

Jangan hanya membaca ADR-011.

Pastikan keputusan yang diminta benar-benar konsisten
dengan architecture yang sudah ada.

==================================================
BAGIAN 2 — EXISTING ARCHITECTURE
==================================================

Petakan architecture yang SUDAH FIXED.

Minimal audit:

- account/user model
- workspace model
- BotInstallation
- provider abstraction
- SecretResolver
- storage boundary
- runtime composition
- API layer
- authorization
- persistence
- background worker/job architecture jika ada
- frontend assumptions
- deployment boundary.

Untuk setiap komponen tulis:

- existing contract,
- existing implementation,
- dependency terhadap B-040,
- apakah boleh diubah,
- apakah harus dipertahankan.

JANGAN membuat implementation baru.

==================================================
BAGIAN 3 — AUTHENTICATION DECISION
==================================================

Identifikasi authentication mechanism yang benar-benar diperlukan
untuk Telegram account connection.

Jangan memilih sendiri.

Jika ada beberapa opsi yang masuk akal, dokumentasikan opsi tersebut,
misalnya berdasarkan evidence repository:

- API credential,
- OAuth-like flow,
- device/login flow,
- browser/session flow,
- provider-specific authentication.

Untuk setiap opsi jelaskan:

- bagaimana authentication terjadi,
- credential apa yang dihasilkan,
- di mana credential disimpan,
- bagaimana refresh dilakukan,
- bagaimana revoke dilakukan,
- bagaimana disconnect dilakukan,
- bagaimana runtime memperoleh credential,
- security implications,
- deployment implications,
- frontend implications,
- backend implications.

Tandai:

`REQUIRES HUMAN DECISION`

untuk keputusan yang belum approved.

==================================================
BAGIAN 4 — ACCOUNT / SESSION MODEL
==================================================

Susun decision package untuk:

- Telegram account identity
- provider account identity
- connection identity
- session identity
- credential identity
- workspace ownership
- apakah satu account dapat digunakan beberapa bot
- apakah satu account dapat berada di beberapa workspace
- hubungan account → workspace → bot
- lifecycle connection.

Jangan membuat schema baru.

Hanya dokumentasikan model yang diperlukan untuk keputusan.

Tandai bagian yang membutuhkan approval.

==================================================
BAGIAN 5 — CREDENTIAL STORAGE
==================================================

Audit SecretResolver yang sudah ada.

Tentukan secara dokumentatif:

- credential apa yang kemungkinan dibutuhkan,
- mana yang boleh disimpan,
- mana yang tidak boleh disimpan,
- siapa yang boleh resolve,
- kapan credential boleh diberikan ke runtime,
- bagaimana credential dicabut,
- bagaimana credential rotation dilakukan.

JANGAN menyimpan credential.

JANGAN membuat fake credential.

JANGAN mengubah SecretResolver implementation hanya untuk
menyelesaikan approval package.

==================================================
BAGIAN 6 — LIFECYCLE STATE MACHINE
==================================================

Buat proposal state machine untuk B-040 berdasarkan architecture
yang sudah ada.

Contoh state hanya sebagai bahan analisis, BUKAN keputusan:

- disconnected
- connecting
- connected
- degraded
- disconnecting
- revoked
- error

Jangan langsung memasukkannya ke production code.

Untuk setiap state jelaskan:

- arti state,
- siapa yang mengubah state,
- event yang menyebabkan perubahan,
- apakah state persistent,
- apakah state berbeda dari runtime process state,
- bagaimana recovery dilakukan.

Sangat penting:

JANGAN mengubah:

`BotInstallation.status`

menjadi runtime process state.

Jika connection lifecycle membutuhkan model baru,
dokumentasikan sebagai keputusan yang harus disetujui terlebih dahulu.

==================================================
BAGIAN 7 — DISCONNECT / REVOKE
==================================================

Siapkan decision matrix:

Disconnect:

- apa yang terjadi?
- credential dihapus atau tetap?
- session invalidated?
- bot berhenti?
- runtime handoff bagaimana?

Revoke:

- apa yang terjadi?
- apakah credential langsung invalid?
- apakah runtime harus dihentikan?
- apakah user harus login ulang?
- apakah semua bot menggunakan account tersebut ikut terpengaruh?

Account removal:

- apa yang terjadi terhadap bot?
- workspace?
- credential?
- session?
- runtime?

Jangan implementasikan behavior.

==================================================
BAGIAN 8 — RUNTIME HANDOFF
==================================================

Audit bagaimana B-040 nantinya menyerahkan connection/account
ke runtime.

Dokumentasikan boundary:

Account Connection
        ↓
Credential/Session
        ↓
Provider Adapter
        ↓
Bot Runtime

Tentukan pertanyaan:

- siapa owner credential?
- siapa yang dapat meminta credential?
- apakah runtime menerima raw credential?
- apakah runtime menerima opaque handle?
- bagaimana revoke diinformasikan?
- bagaimana disconnect diinformasikan?
- bagaimana runtime recovery?

Jangan membuat runtime implementation.

==================================================
BAGIAN 9 — API CONTRACT DECISION PACKAGE
==================================================

Daftarkan endpoint/API behavior yang mungkin dibutuhkan B-040.

Jangan langsung membuat endpoint.

Kelompokkan:

### Connection
- connect
- status
- disconnect
- reconnect

### Authentication
- start authentication
- submit authentication result
- callback/device completion jika memang diperlukan

### Credential/session
- refresh
- revoke
- rotate jika diperlukan

### Runtime
- handoff
- runtime status
- recovery

Untuk setiap API tulis:

- purpose,
- input,
- output,
- authorization,
- error cases,
- persistence,
- owner,
- dependency.

Semua yang belum disetujui diberi:

`PROPOSED — REQUIRES APPROVAL`

==================================================
BAGIAN 10 — SECURITY REVIEW PACKAGE
==================================================

Minta Security owner memberikan keputusan eksplisit untuk:

- credential storage,
- secret resolution,
- session persistence,
- token exposure,
- authentication callback security,
- replay protection,
- CSRF/state protection jika browser flow,
- encryption requirements,
- revoke semantics,
- audit requirements,
- logging restrictions.

Jangan membuat security policy sendiri.

Dokumentasikan:

`SECURITY APPROVAL REQUIRED`

untuk keputusan yang belum tersedia.

==================================================
BAGIAN 11 — DEPLOYMENT DECISION PACKAGE
==================================================

Deployment owner harus menentukan:

- secret manager,
- runtime environment,
- required environment references,
- network requirements,
- callback/webhook exposure jika diperlukan,
- persistent session requirements,
- restart behavior,
- rolling deployment behavior,
- credential rotation behavior.

Jangan memilih infrastructure vendor tanpa evidence repository.

==================================================
BAGIAN 12 — TELEGRAM/PROVIDER OWNER DECISIONS
==================================================

Buat daftar pertanyaan yang harus dijawab provider owner.

Minimal:

1. Authentication mechanism resmi apa?
2. Credential/session apa yang dihasilkan?
3. Berapa lama session valid?
4. Bagaimana refresh?
5. Bagaimana revoke?
6. Bagaimana disconnect?
7. Apakah satu account bisa menjalankan beberapa bot?
8. Apakah credential dapat digunakan concurrent?
9. Apakah ada rate limit?
10. Bagaimana reconnect?
11. Apa failure mode?
12. Apakah provider menyediakan webhook/polling/device flow?
13. Apa API contract resminya?
14. Apa batasan deployment?

Jangan mengarang jawabannya.

==================================================
BAGIAN 13 — APPROVAL MATRIX
==================================================

Buat matrix seperti:

| Decision | Architecture | Telegram | Security | Deployment | Status |
|----------|--------------|----------|----------|------------|--------|

Masukkan minimal:

- authentication mechanism
- account model
- session model
- credential persistence
- SecretResolver usage
- lifecycle state machine
- disconnect
- revoke
- API contract
- runtime handoff
- deployment requirements

Status harus salah satu:

- APPROVED
- PENDING
- BLOCKED
- NOT REQUIRED

Jangan menulis APPROVED tanpa evidence.

==================================================
BAGIAN 14 — IMPLEMENTATION READINESS
==================================================

Setelah approval matrix selesai, tentukan:

B-040 status:

READY

hanya jika SEMUA keputusan wajib sudah approved.

Jika belum:

`BLOCKED — HUMAN APPROVAL REQUIRED`

Kemudian buat daftar implementation sequence setelah approval.

Contoh:

1. domain/account connection model
2. persistence
3. authentication adapter
4. SecretResolver integration
5. connection lifecycle
6. API
7. runtime handoff
8. security tests
9. integration tests
10. deployment verification

Urutkan berdasarkan dependency nyata.

==================================================
BAGIAN 15 — RE-AUDIT ROADMAP
==================================================

Setelah approval package selesai:

audit ulang seluruh roadmap.

Cari apakah ada task selain B-040 yang sekarang benar-benar READY.

Jika ada task independent:

JANGAN langsung mengimplementasikan jika tujuan run ini hanya
approval package.

Cukup laporkan:

- task ID
- dependency
- reason READY

Jika tidak ada:

jelaskan bahwa B-040 adalah blocker utama.

==================================================
BAGIAN 16 — DOKUMENTASI
==================================================

Update documentation ONLY jika memang diperlukan.

Jika repository menggunakan:

- `AI_TASKS.md`
- `PROJECT_STATUS.md`
- `ROADMAP_V2.md`
- `CHANGELOG.md`
- `docs/architecture/DECISIONS.md`

update status secara konsisten.

Jangan membuat banyak README.

Jangan membuat dokumen duplikat.

Jika ADR-011 perlu diperbarui untuk memperjelas decision checklist,
update ADR-011 secara minimal.

Jangan memasukkan keputusan yang belum disetujui sebagai keputusan final.

==================================================
BAGIAN 17 — VALIDATION
==================================================

Karena run ini terutama documentation/decision package,
jangan melakukan source refactor yang tidak diperlukan.

Jika documentation berubah, jalankan:

- `pnpm test`
- `pnpm build`
- `pnpm typecheck`
- `pnpm lint`
- `pnpm format:check`
- `node scripts/check-imports.mjs`
- `node scripts/check-ownership.mjs`
- `node scripts/check-doc-links.mjs`
- `git diff --check`

Jangan membuat:

`scripts/check-symlinks.mjs`

karena file tersebut memang tidak tersedia.

Jangan menjalankan integration test Gorouter.app.

NVIDIA dan TokenHarbor tidak perlu disentuh.

==================================================
BAGIAN 18 — GIT
==================================================

Jika ada perubahan dokumentasi/ADR yang valid:

1. review diff,
2. pastikan tidak ada source implementation speculative,
3. commit satu kali,
4. push:

`git push origin backend-dev-recovery`

Verifikasi:

- local SHA
- remote SHA
- working tree clean

Jika tidak ada perubahan valid:

JANGAN membuat empty commit.

==================================================
FINAL REPORT
==================================================

Tampilkan:

### B-040 STATUS

`BLOCKED — HUMAN APPROVAL REQUIRED`

atau READY jika dan hanya jika evidence approval benar-benar tersedia.

### APPROVALS REQUIRED

Buat daftar keputusan yang harus dijawab manusia.

### APPROVAL MATRIX

Tampilkan matrix Architecture / Telegram / Security / Deployment.

### PROPOSED IMPLEMENTATION ORDER

Urutan implementasi setelah approval.

### DOCUMENTATION

Dokumen yang diperbarui.

### VALIDATION

Semua hasil validation.

### GIT

- commit:
- push:
- local SHA:
- remote SHA:
- working tree:

### OTHER READY TASKS

Jika ada.

### NEXT SINGLE ACTION

Harus berupa:

`Obtain human approval for B-040/ADR-011`

jika B-040 masih blocked.

JANGAN mengatakan project selesai total jika B-040 belum approved.

JANGAN mengimplementasikan B-040 hanya untuk menghilangkan blocker.

Kerjakan langsung pada `/root/botspace`.

```
# Prompt: Continue All Unblocked Work While B-040 Awaits Approval
```

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR — JANGAN DIULANG
==================================================

Audit terakhir SUDAH selesai.

B-030 Workspace API/Contract:
DONE

B-070 Storage Adapter:
DONE

B-071 File/Share Contract:
DONE

B-071 File/Share API:
DONE

B-071 Production Wiring:
DONE

Production SecretResolver boundary:
SUDAH dikerjakan sejauh yang aman dari repository.

B-040 Telegram Account Connection:
BLOCKED

ADR-011:
SUDAH dibuat dan sudah dipush.

Commit terakhir:
`cdf489cdba7aed599f4deb69fe0248bfa7e782f9`

Remote:
`origin/backend-dev-recovery`

Local SHA == Remote SHA:
YA

Working tree:
CLEAN

Tidak ada source implementation Telegram yang boleh dibuat secara
speculative.

==================================================
BLOCKER RESMI
==================================================

B-040 / ADR-011 membutuhkan keputusan manusia dari:

- Architecture owner
- Telegram/provider owner
- Security owner
- Deployment owner

Keputusan yang masih dibutuhkan mencakup:

1. Telegram authentication mechanism
2. account/session model
3. credential persistence boundary
4. lifecycle state machine
5. disconnect/revoke semantics
6. versioned API/provider contract
7. runtime handoff boundary

JANGAN:

- mengarang approval,
- memilih authentication mechanism sendiri,
- membuat Telegram connector speculative,
- membuat polling/webhook,
- membuat session storage speculative,
- mengubah BotInstallation.status,
- menutup B-040 hanya agar roadmap terlihat maju.

B-040 tetap:

`BLOCKED — HUMAN APPROVAL REQUIRED`

==================================================
TUJUAN RUN INI
==================================================

Karena B-040 blocked, JANGAN berhenti.

Sekarang audit SELURUH ROADMAP dan kerjakan SEMUA pekerjaan yang:

- tidak bergantung B-040,
- contract-nya sudah tersedia,
- architecture sudah cukup jelas,
- aman diimplementasikan,
- dan dapat divalidasi dari repository/environment saat ini.

Prinsip:

AUDIT
→ FIND UNBLOCKED TASK
→ IMPLEMENT
→ TEST
→ REVIEW
→ COMMIT
→ PUSH
→ RE-AUDIT ROADMAP
→ CONTINUE

Teruskan sampai tidak ada task aman yang tersisa.

==================================================
FASE 1 — AUDIT ROADMAP
==================================================

Baca ulang:

- `AI_CONTEXT.md`
- `AI_TASKS.md`
- `PROJECT_STATUS.md`
- `ROADMAP_V2.md`
- `CHANGELOG.md`
- `docs/architecture/`
- `docs/architecture/DECISIONS.md`
- ADR yang relevan.

Audit task:

B-040
B-041
B-050
B-051
B-052
B-080
B-090
B-091
B-092
B-100
B-110
B-111
B-120
B-130
B-131
B-140
B-141
B-150
B-151

dan frontend:

F-002
F-010
F-011
F-012
F-020
F-021
F-030
F-031
F-070
F-080
F-090
F-100
F-110
F-120
F-130
F-140
F-150

Untuk masing-masing tentukan:

- DONE
- READY
- BLOCKED
- DEFERRED

JANGAN hanya mengikuti tulisan roadmap lama.

Validasi dependency berdasarkan CODE + CONTRACT + ADR aktual.

==================================================
FASE 2 — PRIORITAS TASK YANG TIDAK BERGANTUNG B-040
==================================================

Cari task yang bisa dikerjakan TANPA Telegram account connection.

Jika ada:

IMPLEMENTASIKAN.

Jangan menunggu B-040 jika task tersebut memang independen.

Contoh kandidat:

- frontend yang contract/API-nya sudah tersedia,
- typed API client,
- frontend shell,
- UI primitives,
- authentication state yang contract-nya sudah ada,
- workspace dashboard yang endpoint-nya sudah tersedia,
- documentation/architecture cleanup,
- validation tooling,
- test coverage,
- production hardening,
- storage/file/share improvements yang memang sudah contract-backed.

Tetapi jangan mengerjakan task hanya karena namanya terlihat independen.

Pastikan dependency nyata.

==================================================
FASE 3 — FRONTEND
==================================================

Audit dependency frontend secara khusus.

Screenshot/status sebelumnya menunjukkan:

F-002:
frontend framework/styling approach

F-010:
web application shell

F-011:
UI primitives

F-012:
typed API client

F-020/F-021:
authentication + route guards

F-030:
workspace dashboard/context

F-031:
workspace settings/members UI

F-070:
real File/Share UI

Jika F-002/F-010/F-011/F-012 sudah dapat dikerjakan tanpa API contract yang belum tersedia:

KERJAKAN BERURUTAN.

Jangan membuat speculative API.

Untuk frontend:

- gunakan typed client,
- jangan hardcode endpoint yang belum ada,
- jangan membuat fake backend,
- jangan membuat mock data sebagai production behavior,
- jangan membuat membership behavior jika contract belum tersedia,
- jangan membuat Telegram account UI jika B-040 belum approved.

Jika F-031 masih bergantung pada B-031 membership/invitation contract:

TETAP BLOCKED.

Jangan mengarang membership API.

==================================================
FASE 4 — FILE/SHARE FRONTEND
==================================================

Audit B-071 API yang SUDAH ADA.

Jika endpoint dan typed client sudah cukup:

implementasikan F-070 File/Share UI.

UI harus menggunakan API nyata.

Minimal bila contract mendukung:

- file listing,
- upload,
- download,
- share,
- revoke share,
- public share access,
- loading state,
- error state,
- empty state.

Jangan menambahkan:

- expiry,
- rate limiting UI,
- audit UI,

jika backend contract belum mendukungnya.

Gunakan workspace authorization yang sudah tersedia.

==================================================
FASE 5 — BACKEND TASK INDEPENDEN
==================================================

Audit semua backend task yang tidak bergantung Telegram.

Khusus:

B-080
B-090
B-091
B-092
B-100
B-110
B-111
B-120
B-130
B-131
B-140
B-141
B-150
B-151

Untuk setiap task:

1. Cari contract.
2. Cari dependency.
3. Cari ADR.
4. Cari existing implementation.
5. Tentukan apakah benar-benar READY.

Jika contract belum ada:

BLOCKED.

Jika contract tersedia:

IMPLEMENTASIKAN.

Jangan membuat architecture baru hanya karena task tersebut belum dikerjakan.

==================================================
FASE 6 — QUEUE/JOB/SCHEDULER
==================================================

Untuk:

B-090
B-091
B-092
F-090

Audit apakah sudah ada contract untuk:

- JobEnvelope
- queue adapter
- retry
- DLQ
- replay
- execution semantics
- scheduler
- job monitoring.

Jika contract tersedia:

implementasikan sesuai contract.

Jika belum:

JANGAN memilih Redis/BullMQ/SQS/etc secara sepihak.

Status:

BLOCKED — queue/job architecture decision required

==================================================
FASE 7 — OPERATOR / BILLING
==================================================

Untuk:

B-100
B-110
B-111
F-100
F-110

Audit contract yang tersedia.

Jangan membuat:

- billing provider,
- entitlement model,
- operator authorization,

secara speculative.

Jika contract sudah ada:

implementasikan.

Jika belum:

BLOCKED.

==================================================
FASE 8 — SECURITY / ABUSE
==================================================

Untuk:

B-130
B-131
F-130

Audit:

- abuse-control contract,
- webhook validation,
- security settings,
- authorization boundary.

Jika contract sudah tersedia:

implementasikan.

Jika belum:

BLOCKED.

Jangan membuat security architecture baru tanpa ADR.

==================================================
FASE 9 — TELEMETRY / SLO
==================================================

Untuk:

B-140
B-141
F-140

Audit:

- telemetry provider,
- metrics,
- tracing,
- SLO,
- alert,
- runbook.

Jika contract/provider tersedia:

implementasikan.

Jika belum:

BLOCKED.

Jangan memilih observability provider secara sepihak.

==================================================
FASE 10 — RELEASE / DEPLOYMENT
==================================================

Untuk:

B-150
B-151
F-150

Audit:

- release contract,
- staging,
- backup,
- restore,
- rollback,
- production approval.

Jika environment dan contract tersedia:

kerjakan.

Jika membutuhkan infrastructure/approval yang tidak tersedia:

BLOCKED.

Jangan mengklaim production verification PASS tanpa evidence nyata.

==================================================
FASE 11 — INFRASTRUCTURE VERIFICATION
==================================================

PostgreSQL:

Jika:

`PERSISTENCE_TEST_DATABASE_URL`

tersedia:

jalankan integration test yang memang sudah ada.

Jika tidak:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan membuat database palsu.

MinIO/S3:

Jika endpoint + test credentials tersedia:

jalankan:

upload
→ verify
→ download
→ verify content
→ delete
→ verify deletion.

Jika tidak:

`SKIPPED — MinIO/S3 test environment unavailable`

Managed Secret Manager:

Jika environment nyata tersedia:

jalankan verification.

Jika tidak:

jangan membuat fake production secret manager.

==================================================
FASE 12 — SECURITY AUDIT
==================================================

Sebelum commit setiap perubahan:

audit:

- workspace isolation,
- authorization,
- secret leakage,
- credential handling,
- token leakage,
- path traversal,
- object storage key leakage,
- error sanitization,
- log sanitization.

Jangan pernah commit:

- API key,
- token,
- password,
- session,
- credential,
- production secret.

==================================================
FASE 13 — TEST
==================================================

Setelah setiap kelompok implementation:

jalankan validation yang relevan.

Kemudian full validation:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

Untuk:

`node scripts/check-symlinks.mjs`

jangan membuat file tersebut.

Jika tidak tersedia:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

Jangan mengubah test agar PASS.

==================================================
FASE 14 — GIT
==================================================

Sebelum commit:

`git status`

`git diff --stat`

`git diff`

Pastikan tidak ada perubahan unrelated.

Jika ada implementation valid:

buat SATU commit untuk pekerjaan run ini.

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Local SHA harus sama dengan remote SHA.

Jika tidak ada perubahan valid:

JANGAN membuat empty commit.

==================================================
FASE 15 — RE-EVALUATE
==================================================

SETELAH COMMIT/PUSH:

Jangan langsung berhenti.

Audit roadmap lagi.

Jika task baru menjadi READY akibat pekerjaan tadi:

KERJAKAN.

Ulangi:

AUDIT
→ IMPLEMENT
→ TEST
→ COMMIT
→ PUSH
→ RE-AUDIT

sampai tidak ada task READY yang aman untuk dikerjakan.

==================================================
STOP CONDITION
==================================================

Berhenti hanya jika:

1. semua task yang benar-benar READY sudah selesai,
2. semua task berikutnya BLOCKED/DEFERRED,
3. atau membutuhkan approval manusia/infrastructure yang memang belum tersedia.

B-040/ADR-011 harus tetap dicatat:

`BLOCKED — HUMAN APPROVAL REQUIRED`

Jangan memalsukan approval.

==================================================
FINAL REPORT
==================================================

Tampilkan:

### B-040
BLOCKED — HUMAN APPROVAL REQUIRED

Jelaskan decision yang masih dibutuhkan.

### TASK YANG DIKERJAKAN RUN INI
- task:
- implementation:
- tests:
- commit:

### TASK YANG SEKARANG DONE
Daftar task yang benar-benar selesai.

### TASK YANG BLOCKED
Untuk setiap task:
- task ID
- dependency
- alasan blocked

### TASK DEFERRED
Hanya dependency nyata.

### VALIDATION
- test
- build
- typecheck
- lint
- format
- imports
- ownership
- docs
- diff

### GIT
- commit SHA
- remote SHA
- push status
- working tree

### NEXT SINGLE ACTION
Berikan SATU task paling tepat berikutnya.

PENTING:

JANGAN membuat pekerjaan palsu hanya untuk menghindari blocker B-040.

JANGAN mengarang contract.

JANGAN mengarang approval.

JANGAN membuat Telegram connector.

JANGAN membuat Telegram polling/webhook.

JANGAN mengubah BotInstallation.status.

JANGAN menyentuh Gorouter.app.

NVIDIA dan TokenHarbor hanya disentuh jika memang diperlukan oleh perubahan yang sedang dikerjakan.

Kerjakan semua pekerjaan lain yang benar-benar UNBLOCKED.

Kerjakan langsung pada `/root/botspace`.

```
# Prompt: B-040 → B-041 → Bot Runtime Dependency Chain
```
Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

B-030 Workspace API/Contract:
DONE

B-070 Storage Adapter:
DONE

B-071 File/Share Contract:
DONE

B-071 File/Share API:
DONE

B-071 Production Wiring:
DONE

Production SecretResolver application boundary:
DONE sejauh yang dapat dilakukan dari repository

Deferred infrastructure verification:
SUDAH DIAUDIT

B-040 Telegram Account Connection:
BELUM IMPLEMENTASI

Audit terakhir sudah menghasilkan:

`docs/architecture/ADR-011-telegram-account-connection.md`

dan update documentation/status terkait.

Repository terakhir menunjukkan:

- HEAD dan origin/backend-dev-recovery sudah sinkron.
- Tidak ada source implementation Telegram yang dibuat secara speculative.
- B-040 masih menunggu approval contract/architecture decision.
- B-041 bergantung pada B-040.
- B-050/B-051/B-052 bergantung pada bot/provider/runtime contract.
- B-090/B-091/B-092 bergantung pada queue/job/scheduler architecture.
- B-100 bergantung pada operator/admin contract.
- B-110/B-111 bergantung pada entitlement/billing contract.
- B-130/B-131 bergantung pada abuse-control/webhook/security contract.
- B-140/B-141 bergantung pada telemetry/SLO/alert/runbook contract.
- B-150/B-151 bergantung pada deployment/release/backup/rollback infrastructure.
- B-080 AI requirements belum tersedia.
- B-120 marketplace requirements belum tersedia.
- share expiry masih deferred.
- public-share rate limiting masih deferred.
- public-share audit event masih deferred.
- PostgreSQL integration masih membutuhkan environment.
- MinIO/S3 smoke test masih membutuhkan environment.
- `scripts/check-symlinks.mjs` memang tidak tersedia.

==================================================
TUJUAN RUN INI
==================================================

Jangan berhenti hanya karena screenshot/status sebelumnya mengatakan
"approval required".

Sekarang lakukan audit penuh untuk menentukan apakah approval B-040/ADR-011
memang benar-benar membutuhkan input eksternal, atau repository sudah memiliki
cukup informasi untuk menyelesaikan decision tersebut.

Jika approval dapat diselesaikan berdasarkan contract/ADR/deployment decision
yang SUDAH ada di repository:

→ selesaikan approval secara repository-backed,
→ implementasikan B-040,
→ lanjutkan otomatis ke B-041,
→ lanjutkan ke task berikutnya yang benar-benar UNBLOCKED.

Jika approval memang membutuhkan keputusan manusia/deployment owner yang belum
tersedia:

→ JANGAN mengarang approval,
→ JANGAN memilih authentication mechanism secara sembarangan,
→ JANGAN membuat Telegram implementation speculative.

Tetapi audit SEMUA task lain yang mungkin sudah UNBLOCKED dan kerjakan yang
bisa dilakukan.

==================================================
FASE 1 — AUDIT ADR-011
==================================================

Baca:

- `docs/architecture/ADR-011-telegram-account-connection.md`
- `docs/architecture/DECISIONS.md`
- roadmap terbaru,
- `AI_CONTEXT.md`,
- `AI_TASKS.md`,
- `PROJECT_STATUS.md`,
- `ROADMAP_V2.md`,
- seluruh contract Telegram/account/provider/runtime yang sudah ada.

Cari:

- status ADR,
- decision owner,
- approval mechanism,
- accepted/rejected status,
- superseding ADR,
- existing authentication decision,
- existing credential/session decision,
- existing Telegram provider decision,
- existing deployment decision.

Jangan hanya grep `B-040`.

Cari juga istilah:

- Telegram account
- account connection
- Telegram authentication
- Bot API
- bot token
- MTProto
- session
- credential
- SecretResolver
- connection state
- account lifecycle
- provider adapter
- runtime
- BotInstallation
- workspace account
- account ownership
- revoke
- disconnect
- reconnect
- health.

==================================================
FASE 2 — TENTUKAN APAKAH B-040 BISA DIBUKA
==================================================

Klasifikasikan hasil menjadi:

A. APPROVED
B. APPROVABLE FROM EXISTING CONTRACT
C. REQUIRES HUMAN/DEPLOYMENT OWNER DECISION
D. BLOCKED BY MISSING INFRASTRUCTURE

Jangan mengubah status menjadi APPROVED hanya karena implementation
terlihat mudah.

Untuk status APPROVED atau APPROVABLE:

jelaskan evidence file/contract yang mendukung.

Jika C:

jelaskan EXACT decision yang masih diperlukan.

Minimal:

1. Telegram authentication mechanism
2. account identity
3. credential/session persistence boundary
4. lifecycle state machine
5. disconnect/revoke semantics
6. workspace ownership
7. runtime handoff boundary

==================================================
FASE 3 — JIKA B-040 SUDAH APPROVED
==================================================

Implementasikan B-040 secara modular.

Pisahkan dengan jelas:

- domain model,
- connection contract,
- account repository contract,
- connection service,
- credential/session boundary,
- provider adapter,
- API boundary.

Jangan membuat satu file besar.

Pastikan:

### Account Identity

Telegram account harus memiliki identity yang deterministic.

Pastikan hubungan:

workspace
→ Telegram account
→ connection

tidak memungkinkan cross-workspace access.

### Credential Boundary

Gunakan `SecretResolver` yang sudah ada.

Jangan:

- hardcode token,
- menyimpan raw credential di source,
- mencetak credential,
- mengembalikan credential melalui API,
- memasukkan credential ke error.

### Lifecycle

Implementasikan hanya state yang memang disetujui ADR/contract.

Jangan membuat state tambahan tanpa alasan.

### Disconnect

Disconnect harus memiliki behavior yang jelas.

Pastikan account yang disconnected tidak dapat digunakan oleh runtime sebagai
connected account.

### Revoke

Jika contract mendukung revoke:

- invalidate credential/session reference,
- update connection state,
- pastikan runtime tidak menggunakan credential yang sudah direvoke.

==================================================
FASE 4 — B-041 CONNECTION HEALTH / STATE MACHINE
==================================================

SETELAH B-040 selesai dan validation PASS:

Audit B-041.

Implementasikan hanya jika contract B-040 sekarang cukup.

B-041 harus menangani:

- connection health,
- current state,
- transition validity,
- failure state,
- disconnect state,
- reconnect semantics jika contract mendukungnya.

Jangan membuat network polling permanen hanya untuk health check jika runtime
contract belum tersedia.

Pisahkan:

ACCOUNT LIFECYCLE STATE

dari:

RUNTIME PROCESS STATE.

JANGAN mengubah:

`BotInstallation.status`

menjadi process state.

==================================================
FASE 5 — B-050 / B-051 / B-052
==================================================

Setelah B-041:

Audit dependency:

- B-050
- B-051
- B-052

Jangan mengerjakan semuanya secara membabi buta.

Tentukan:

B-050 membutuhkan apa?
B-051 membutuhkan apa?
B-052 membutuhkan apa?

Jika contract/provider/runtime sudah tersedia:

IMPLEMENTASIKAN.

Jika belum:

STOP di dependency tersebut.

Jangan membuat provider contract speculative.

==================================================
FASE 6 — BOT RUNTIME
==================================================

Jika B-050/B-051/B-052 ternyata sudah cukup untuk membuka runtime:

audit runtime architecture.

Pisahkan:

1. account connection
2. bot installation
3. provider
4. runtime process
5. lifecycle
6. health
7. restart/reconnect.

Jangan membuat Telegram polling/webhook hanya karena ingin "melanjutkan".

Gunakan adapter/provider boundary yang memang sudah ada.

Jika provider contract belum ada:

jangan implementasikan runtime.

==================================================
FASE 7 — CARI SEMUA TASK UNBLOCKED
==================================================

Setelah B-040/B-041 atau blocker ditemukan, jangan berhenti.

Audit roadmap secara keseluruhan.

Untuk setiap task:

B-050
B-051
B-052
B-080
B-090
B-091
B-092
B-100
B-110
B-111
B-120
B-130
B-131
B-140
B-141
B-150
B-151
F-080
F-090
F-100
F-110
F-120
F-130
F-140
F-150

tentukan:

- DONE
- READY
- BLOCKED
- DEFERRED

Jika READY dan contract tersedia:

KERJAKAN.

Jika BLOCKED:

jangan membuat speculative implementation.

==================================================
FASE 8 — QUEUE / JOB / SCHEDULER
==================================================

Jika ternyata B-090 atau dependency-nya sudah memiliki contract yang cukup:

audit:

- JobEnvelope,
- queue adapter,
- retry,
- DLQ,
- replay,
- execution semantics,
- scheduler.

Jangan membuat queue system baru jika repository sudah memiliki abstraction.

Jangan memilih Redis/BullMQ/SQS/etc. tanpa architecture decision.

Jika contract belum ada:

tetap BLOCKED.

==================================================
FASE 9 — OPERATOR / BILLING / SECURITY
==================================================

Jangan membuat:

- operator system,
- billing system,
- entitlement system,
- abuse system,
- telemetry system,

secara speculative.

Tetapi jika contract sudah tersedia:

kerjakan implementation yang memang sudah unblocked.

==================================================
FASE 10 — INFRASTRUCTURE VERIFICATION
==================================================

Periksa environment.

### PostgreSQL

Cari:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan integration test yang memang sudah ada.

Jika tidak:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan membuat database palsu.

### MinIO/S3

Cari environment endpoint/credential TEST ONLY.

Jika tersedia:

jalankan smoke test:

upload
→ verify
→ download
→ verify content
→ delete
→ verify deletion

Jika tidak:

`SKIPPED — MinIO/S3 test environment unavailable`

Jangan install infrastructure permanen hanya untuk membuat PASS.

### Secret Manager

Jika managed secret manager nyata tersedia:

jalankan startup/integration verification sesuai architecture.

Jika tidak:

tetap deferred.

==================================================
FASE 11 — SECURITY
==================================================

Audit semua perubahan.

Pastikan:

- workspace isolation,
- account ownership,
- authorization,
- credential boundary,
- SecretResolver,
- session handling,
- revoke behavior,
- error sanitization,
- log sanitization,
- no secret leakage.

Cari secara aktif:

- API keys,
- tokens,
- passwords,
- private credentials,
- session strings.

Jangan mencetak nilainya.

==================================================
FASE 12 — TEST
==================================================

Tambahkan test hanya untuk behavior yang benar-benar diimplementasikan.

Minimal bila B-040/B-041 berhasil:

- account ownership,
- workspace isolation,
- connect,
- duplicate connect,
- disconnect,
- revoke,
- invalid state transition,
- connection failure,
- health state,
- unauthorized access,
- credential failure,
- secret non-leakage.

Jika runtime dibuka:

tambahkan test runtime lifecycle sesuai contract.

Jangan membuat mock palsu hanya agar test PASS.

==================================================
FASE 13 — VALIDATION
==================================================

Jalankan semua command yang benar-benar tersedia:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check
node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat file baru.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jika command tertentu tidak tersedia, laporkan secara jujur.

Jangan mengubah package.json hanya untuk membuat command terlihat tersedia.

==================================================
FASE 14 — REVIEW DIFF
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan tidak ada:

- credential,
- secret,
- temporary file,
- generated junk,
- unrelated refactor,
- speculative provider,
- speculative Telegram runtime,
- perubahan Gorouter.app,
- perubahan NVIDIA/TokenHarbor yang tidak diperlukan.

==================================================
FASE 15 — COMMIT + PUSH
==================================================

Jika ada implementation valid:

buat SATU commit untuk perubahan yang benar-benar dikerjakan dalam run ini.

Gunakan commit message yang sesuai dengan actual scope.

Contoh:

`feat: implement telegram account connection`

atau:

`feat: add telegram connection health state`

atau message lain yang lebih tepat.

Kemudian:

git push origin backend-dev-recovery

Verifikasi:

git rev-parse HEAD
git rev-parse origin/backend-dev-recovery
git status

Pastikan:

LOCAL SHA == REMOTE SHA

Jika hanya audit/documentation dan tidak ada source change:

JANGAN membuat empty commit.

Jika push gagal:

jangan mengubah credential sembarangan,
jangan menghapus commit,
laporkan error.

==================================================
FASE 16 — UPDATE DOCUMENTATION
==================================================

Jika implementation benar-benar selesai:

update status roadmap/documentation yang memang digunakan repository.

Jangan membuat README baru.

Gunakan documentation yang sudah ada:

- AI_CONTEXT.md
- AI_TASKS.md
- PROJECT_STATUS.md
- ROADMAP_V2.md
- docs/architecture/ADR-011-telegram-account-connection.md
- docs/architecture/DECISIONS.md

Jangan menghapus history.

Status harus mencerminkan keadaan repository sebenarnya.

==================================================
FINAL REPORT
==================================================

Tampilkan:

# B-040

Status:
DONE / APPROVED / BLOCKED / DECISION REQUIRED

Evidence:
- contract:
- ADR:
- implementation:

# B-041

Status:
DONE / READY / BLOCKED

# B-050/B-051/B-052

Status masing-masing.

# OTHER READY TASKS

Tampilkan task lain yang ternyata sudah UNBLOCKED dan dikerjakan.

# BLOCKED TASKS

Tampilkan hanya dependency nyata.

# DEFERRED

Tampilkan:
- AI requirements
- marketplace requirements
- rate limiting
- audit event
- expiry
- infrastructure yang memang belum tersedia

# TEST / VALIDATION

Tampilkan hasil setiap command.

# GIT

- commit SHA
- remote SHA
- push status
- working tree

# NEXT ACTION

Berikan SATU task berikutnya yang paling tepat berdasarkan dependency nyata.

==================================================
STOP CONDITION
==================================================

Jangan berhenti hanya karena menemukan satu blocker.

Teruskan pekerjaan selama masih ada task yang:

- contract-nya tersedia,
- dependency-nya selesai,
- aman diimplementasikan,
- dan tidak membutuhkan keputusan eksternal.

STOP hanya jika:

1. semua task yang currently READY sudah dikerjakan,
2. semua task berikutnya benar-benar blocked/deferred,
3. atau membutuhkan approval/decision/infrastructure yang belum tersedia.

Jangan membuat fitur speculative hanya supaya terlihat progress.

Kerjakan langsung pada `/root/botspace`.

PRINSIP UTAMA:

AUDIT → UNBLOCK → IMPLEMENT → TEST → REVIEW → COMMIT → PUSH → REEVALUATE ROADMAP.

Ulangi siklus tersebut sampai tidak ada pekerjaan aman yang tersisa.


```
# Prompt: B-040 Telegram Account Connection — Full Contract Discovery, Decision Package & Implementation
```

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

Repository sudah diaudit secara menyeluruh.

Status yang sudah selesai dan JANGAN diulang:

- B-030 Workspace API/Contract — DONE
- B-070 Storage Adapter — DONE
- B-071 File/Share Contract — DONE
- B-071 File/Share API — DONE
- B-071 Production Wiring — DONE
- SecretResolver production boundary — DONE sejauh yang dapat dilakukan
- Workspace isolation — verified
- File/share security — verified
- Git branch sudah sinkron
- Working tree terakhir CLEAN

Remaining roadmap saat ini menunjukkan:

- B-040 Telegram account connection — BLOCKED
- B-041 connection health/state machine — menunggu B-040
- B-050/B-051/B-052 — menunggu bot/provider/runtime contract
- B-090/B-091/B-092 — menunggu JobEnvelope/queue/scheduler contract
- B-100 — menunggu operator/admin contract
- B-110/B-111 — menunggu entitlement/billing contract
- B-130/B-131 — menunggu abuse-control/webhook/security contract
- B-140/B-141 — menunggu telemetry/SLO/alert/runbook contract
- B-150/B-151 — menunggu release/staging/backup/rollback infrastructure
- B-080 — AI requirements unavailable
- B-120 — marketplace requirements unavailable
- public-share rate limiting — deferred
- public-share audit event — deferred
- share expiry — deferred

Audit terakhir menyatakan:

"the next actionable step is not code. It is approval and delivery of the missing Telegram account connection contract, after which B-041 and the dependent bot/runtime chain can be reevaluated."

==================================================
TUJUAN RUN INI
==================================================

Sekarang fokus hanya pada:

# B-040 TELEGRAM ACCOUNT CONNECTION

Tujuan utama:

1. Pastikan apakah Telegram account connection contract benar-benar belum ada.
2. Cari seluruh repository untuk kemungkinan contract/ADR/model/configuration yang sebenarnya sudah tersedia tetapi belum ditemukan oleh audit sebelumnya.
3. Jika contract sudah ada secara nyata:
   - gunakan contract tersebut,
   - implementasikan B-040,
   - tambahkan test,
   - validation,
   - commit,
   - push.
4. Jika contract memang BELUM ADA:
   - jangan langsung membuat implementation Telegram speculative,
   - jangan membuat polling/webhook,
   - jangan membuat authentication flow berdasarkan asumsi,
   - jangan memilih architecture tanpa dasar.
5. Namun jangan berhenti hanya dengan kalimat "blocked".
   Buat decision package yang lengkap agar dependency B-040 dapat diselesaikan dengan satu keputusan yang jelas.

==================================================
FASE 1 — AUDIT TOTAL B-040
==================================================

Cari seluruh repository untuk:

- B-040
- Telegram
- Telegram account
- account connection
- connection contract
- account lifecycle
- authentication
- session
- credentials
- login
- authorization
- bot account
- BotInstallation
- provider
- runtime
- webhook
- polling
- MTProto
- Bot API
- token
- secret
- account state
- connection state
- health state
- ADR
- architecture decision
- TODO
- deferred
- blocked
- roadmap

Jangan hanya mencari nama file.

Periksa juga:

- database schema,
- migrations,
- domain models,
- interfaces,
- ports,
- adapters,
- API routes,
- configuration,
- documentation,
- ADR,
- README,
- test fixtures,
- existing Telegram-related code.

==================================================
FASE 2 — CEK APAKAH CONTRACT TERSEMBUNYI
==================================================

Sebelum menyimpulkan B-040 blocked:

Cari apakah sudah ada contract yang secara tidak langsung menentukan:

- bagaimana Telegram account direpresentasikan,
- bagaimana account dihubungkan,
- bagaimana credential/session disimpan,
- bagaimana connection dibuat,
- bagaimana connection diputus,
- bagaimana connection state ditentukan,
- bagaimana health ditentukan,
- bagaimana reconnect dilakukan,
- bagaimana account ownership ditentukan,
- bagaimana workspace memiliki account,
- bagaimana authentication dilakukan.

Jika ada:

JANGAN membuat contract baru.

Gunakan contract yang sudah ada.

==================================================
FASE 3 — TENTUKAN DEPENDENCY MINIMUM
==================================================

Jika contract belum tersedia, tentukan dependency minimum yang BENAR-BENAR dibutuhkan B-040.

Minimal audit:

1. Account identity
2. Workspace ownership
3. Connection lifecycle
4. Authentication mechanism
5. Credential/session storage boundary
6. Connection state
7. Disconnect/revoke semantics
8. Health semantics
9. Secret handling
10. Runtime handoff boundary

Jangan implementasikan runtime sebelum boundary ini jelas.

==================================================
FASE 4 — JANGAN MEMILIH AUTHENTICATION SECARA SEMBARANGAN
==================================================

JANGAN otomatis memilih:

- Telegram Bot API token,
- MTProto,
- phone login,
- QR login,
- OAuth,
- device code,
- browser session,
- polling,
- webhook.

Cari dulu apakah architecture repository sudah menetapkan salah satunya.

Jika tidak ada:

tandai sebagai ARCHITECTURE DECISION REQUIRED.

Jangan mengarang keputusan.

==================================================
FASE 5 — DECISION PACKAGE
==================================================

Jika B-040 benar-benar belum memiliki contract, buat satu decision package yang bisa digunakan maintainer/deployment owner untuk menyetujui contract tersebut.

Decision package harus menjelaskan:

### A. Account Model

Apa identitas Telegram account?

Contoh pertanyaan:

- internal account ID?
- Telegram user/account ID?
- workspace ID?
- display name?
- username?

Jangan mengisi nilai berdasarkan asumsi. Bedakan:

CONFIRMED

vs

DECISION REQUIRED.

### B. Connection Lifecycle

Tentukan contract yang dibutuhkan untuk:

- connect
- connecting
- connected
- degraded
- disconnected
- disconnecting
- failed
- revoked

Jika state belum disetujui:

jangan membuat implementation.

### C. Authentication

Jelaskan pilihan yang mungkin berdasarkan kebutuhan repository.

Tetapi JANGAN memilih satu tanpa approval.

### D. Credential Boundary

Tentukan:

- apa yang dianggap secret,
- siapa yang menyimpan,
- bagaimana SecretResolver digunakan,
- bagaimana credential/session direvoke,
- apa yang tidak boleh masuk database/log.

### E. Workspace Ownership

Pastikan satu Telegram account tidak dapat diakses oleh workspace lain.

### F. Disconnect/Revoke

Tentukan behavior:

- disconnect account,
- revoke credential,
- invalidate session,
- remove workspace association.

### G. Runtime Boundary

B-040 hanya mendefinisikan account connection.

JANGAN memasukkan:

- bot polling,
- webhook runtime,
- worker runtime,
- queue,
- scheduler.

Runtime harus tetap menjadi dependency berikutnya.

==================================================
FASE 6 — ADR / DOCUMENTATION
==================================================

Cari mekanisme ADR/documentation yang SUDAH digunakan repository.

Jika repository memang memiliki ADR mechanism:

buat/update decision document hanya jika itu memang bagian workflow repository.

Jika repository tidak memiliki ADR mechanism:

JANGAN membuat sistem dokumentasi baru hanya untuk ini.

Dalam laporan, tampilkan decision package sebagai output audit.

Jangan mengubah README besar-besaran.

==================================================
FASE 7 — IMPLEMENTASI JIKA CONTRACT SUDAH TERSEDIA
==================================================

Jika selama audit ditemukan contract yang benar-benar sudah tersedia:

IMPLEMENTASIKAN B-040.

Implementation harus modular.

Pisahkan:

- domain contract,
- account repository,
- connection service,
- credential boundary,
- provider adapter,
- API boundary.

Jangan membuat satu file besar.

Pastikan:

- workspace ownership,
- authorization,
- secret handling,
- lifecycle,
- error handling.

Tambahkan test untuk:

- connect,
- duplicate connection,
- wrong workspace,
- disconnect,
- revoke,
- invalid state,
- credential failure,
- unauthorized access,
- secret leakage.

==================================================
FASE 8 — JIKA CONTRACT BELUM ADA
==================================================

Jika contract benar-benar belum ada:

JANGAN membuat fake implementation.

JANGAN membuat Telegram runtime.

JANGAN membuat database migration speculative.

JANGAN membuat provider adapter speculative.

JANGAN membuat endpoint palsu.

Sebaliknya:

hasilkan:

# B-040 BLOCKED

dengan:

- exact missing contract,
- exact architecture decision,
- exact dependency,
- files inspected,
- evidence dari repository,
- apa yang bisa langsung dikerjakan setelah approval.

==================================================
FASE 9 — RE-EVALUASI DEPENDENCY CHAIN
==================================================

Setelah audit B-040, reevaluasi:

B-040
↓
B-041
↓
B-050
↓
B-051
↓
B-052
↓
B-090
↓
B-091/B-092
↓
F-090
↓
B-100
↓
B-110/B-111
↓
B-130/B-131
↓
B-140/B-141
↓
B-150/B-151

Jangan menganggap dependency chain otomatis benar.

Gunakan repository sebagai source of truth.

Jika ada task yang ternyata tidak bergantung B-040 dan sudah UNBLOCKED:

KERJAKAN task tersebut.

Jika semuanya tetap blocked:

jelaskan alasannya.

==================================================
FASE 10 — VALIDATION
==================================================

Jika ada code yang berubah:

jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check
node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan membuat:

scripts/check-symlinks.mjs

Jika file tidak tersedia:

SKIPPED — unavailable.

Jangan mengubah test agar PASS.

==================================================
FASE 11 — SECURITY REVIEW
==================================================

Audit:

- workspace isolation,
- account ownership,
- credential storage,
- SecretResolver usage,
- session handling,
- authorization,
- error sanitization,
- log sanitization.

Pastikan:

- tidak ada secret di source,
- tidak ada token di log,
- tidak ada credential di response,
- tidak ada cross-workspace account access.

==================================================
FASE 12 — GIT
==================================================

Jika ada implementation valid:

review:

git status
git diff --stat
git diff

Jika valid:

buat SATU commit.

Push:

git push origin backend-dev-recovery

Verifikasi:

git rev-parse HEAD
git rev-parse origin/backend-dev-recovery
git status

Pastikan:

LOCAL SHA == REMOTE SHA
WORKING TREE CLEAN

Jika hanya audit/documentation tanpa repository change:

JANGAN membuat empty commit.

==================================================
FINAL REPORT
==================================================

Tampilkan:

# B-040 STATUS

DONE / BLOCKED / DECISION REQUIRED

# CONTRACT DISCOVERY

- contract ditemukan:
- file:
- evidence:

# MISSING DECISIONS

Jika ada, tampilkan exact decision yang diperlukan.

# IMPLEMENTATION

Jika ada:
- file changed
- behavior
- tests

Jika tidak:
- jelaskan mengapa implementation tidak aman dilakukan.

# DEPENDENCY CHAIN

B-040 → B-041 → B-050/B-051/B-052 → ...

# VALIDATION

Semua hasil test/build/typecheck/lint/etc.

# GIT

- SHA
- push
- working tree

# NEXT ACTION

Hanya satu next action paling tepat.

Jangan membuat fitur acak.

==================================================
STOP CONDITION
==================================================

STOP setelah:

1. seluruh repository sudah dicari,
2. B-040 contract sudah ditemukan ATAU dipastikan benar-benar belum ada,
3. semua task yang tidak bergantung B-040 sudah diperiksa,
4. implementation dilakukan jika contract benar-benar tersedia,
5. jika contract tidak tersedia, decision package sudah lengkap,
6. tidak ada speculative Telegram implementation.

PENTING:

Jangan hanya menjawab "B-040 blocked".

Lakukan audit mendalam terlebih dahulu.

Jika ada code yang aman dikerjakan → KERJAKAN.

Jika tidak ada → siapkan dependency/decision yang benar.

Kerjakan langsung pada `/root/botspace`.

```
# Prompt: Final Roadmap Closure & Dependency Resolution Audit
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
STATUS TERAKHIR
==================================================

Repository saat ini sudah melalui:

- B-030 Workspace API/Contract — DONE
- B-070 Storage Adapter — DONE
- B-071 File/Share Contract — DONE
- B-071 File/Share API — DONE
- B-071 Production Wiring — DONE
- SecretResolver application boundary — DONE
- Infrastructure verification yang dapat dilakukan dari repository — DONE
- File/share security regression — DONE
- Workspace isolation — DONE
- Local SHA dan remote SHA — SAMA
- Working tree — CLEAN

Status terakhir menunjukkan:

Remaining Roadmap:

1. B-040 Telegram account connection
   - contract dan implementation belum tersedia.
2. B-041 connection health/state machine
   - bergantung pada B-040.
3. B-050/B-051/B-052
   - masih menunggu bot/provider/runtime contracts.
4. B-090
   - membutuhkan JobEnvelope, queue adapter, retry/DLQ/replay policy,
     scheduler persistence contract.
5. Operator/billing/telemetry/release
   - contract belum tersedia.
6. Share expiry
   - menunggu approved contract/schema/migration.
7. Public-share rate limiting
   - menunggu approved policy/middleware boundary.
8. Public-share audit event
   - menunggu approved event/service/repository boundary.
9. PostgreSQL integration verification
   - hanya dapat dijalankan jika `PERSISTENCE_TEST_DATABASE_URL` tersedia.
10. MinIO/S3 smoke test
   - hanya dapat dijalankan jika test environment tersedia.
11. `scripts/check-symlinks.mjs`
   - memang tidak tersedia dan JANGAN dibuat hanya untuk validation.

==================================================
TUJUAN PROMPT INI
==================================================

Lakukan FINAL ROADMAP CLOSURE AUDIT.

Tujuannya bukan membuat code secara paksa.

Tujuannya:

1. memastikan tidak ada task repository yang sebenarnya sudah UNBLOCKED,
2. memastikan tidak ada dependency yang terlewat,
3. memastikan semua completed task benar-benar valid,
4. memastikan semua deferred task memiliki alasan dependency yang nyata,
5. mengidentifikasi EXACTLY apa yang dibutuhkan agar project bisa lanjut,
6. melakukan implementation hanya jika dependency benar-benar tersedia,
7. melakukan documentation/ADR update hanya jika repository memang sudah memiliki mekanisme dokumentasi/ADR untuk keputusan tersebut.

JANGAN membuat architecture speculative.

==================================================
ATURAN MUTLAK
==================================================

JANGAN:

- membuat Telegram account connection contract berdasarkan asumsi,
- memilih Telegram authentication method sendiri,
- membuat Telegram polling,
- membuat Telegram webhook,
- membuat MTProto implementation,
- membuat QR login,
- membuat phone login,
- membuat session system,
- membuat fake Telegram connection,
- membuat provider abstraction baru jika belum ada contract,
- membuat BotInstallation runtime,
- mengubah `BotInstallation.status`,
- membuat queue architecture speculative,
- membuat JobEnvelope speculative,
- membuat billing architecture speculative,
- membuat telemetry architecture speculative,
- membuat release architecture speculative,
- membuat share expiry tanpa contract/schema,
- membuat rate limiter tanpa approved policy,
- membuat audit event system baru tanpa approved boundary,
- membuat fake PostgreSQL,
- menggunakan SQLite sebagai pengganti PostgreSQL,
- membuat fake MinIO,
- membuat credential production palsu,
- membuat `scripts/check-symlinks.mjs`.

Jangan mengubah code hanya supaya jumlah "remaining task" berkurang.

==================================================
FASE 1 — AUDIT ROADMAP AKTUAL
==================================================

Audit repository langsung.

Jalankan:

`cd /root/botspace`

`git status`

`git branch --show-current`

`git log --oneline -30`

Kemudian cari seluruh roadmap/task:

- B-*
- F-*
- Phase *
- V2
- TODO
- FIXME
- deferred
- blocked
- dependency
- ADR

Jangan hanya menggunakan laporan AI sebelumnya.

Source of truth adalah repository.

==================================================
FASE 2 — DEPENDENCY GRAPH
==================================================

Bangun dependency graph aktual untuk SEMUA task yang belum selesai.

Untuk setiap task:

- Task ID
- Nama
- Status
- Existing contract?
- Existing implementation?
- Existing tests?
- Dependency
- External dependency?
- Environment dependency?
- Architecture decision dependency?
- UNBLOCKED / BLOCKED

Kategori:

A. DONE
B. UNBLOCKED — BOLEH DIKERJAKAN
C. ENVIRONMENT BLOCKED
D. CONTRACT BLOCKED
E. ARCHITECTURE DECISION BLOCKED
F. EXTERNAL INFRASTRUCTURE BLOCKED

==================================================
FASE 3 — CARI TASK UNBLOCKED
==================================================

Ini sangat penting.

Jangan menganggap semua task setelah B-040 otomatis blocked.

Cari seluruh repository dan pastikan apakah ada task lain yang:

- tidak bergantung B-040,
- contract-nya sudah tersedia,
- implementation boundary-nya sudah jelas,
- dapat dikerjakan tanpa speculative architecture.

Jika ada:

KERJAKAN SEKARANG.

Lakukan:

IMPLEMENT
→ TEST
→ BUILD
→ TYPECHECK
→ LINT
→ REVIEW
→ COMMIT

Jangan berhenti pada audit jika task benar-benar UNBLOCKED.

==================================================
FASE 4 — B-040 TELEGRAM ACCOUNT CONNECTION
==================================================

Audit B-040 secara menyeluruh.

Cari apakah repository memiliki:

- Telegram account model,
- connection contract,
- authentication contract,
- credential/session contract,
- provider contract,
- account lifecycle contract,
- secret storage boundary,
- OAuth/device-code/browser-login mechanism,
- ADR yang menentukan authentication method.

Jika SEMUA tersedia:

implementasikan B-040 secara nyata.

Jika contract belum tersedia:

JANGAN mengarang implementation.

Cari dan dokumentasikan EXACT dependency yang hilang.

Contoh output internal:

B-040 BLOCKED
Reason:
Telegram account connection contract unavailable.

Missing decisions:
- authentication mechanism
- account/session lifecycle
- credential storage
- connection/disconnection semantics
- health semantics

Jangan membuat contract sendiri hanya untuk menghilangkan blocker.

==================================================
FASE 5 — B-041
==================================================

Audit B-041.

Jika B-040 belum tersedia:

JANGAN implementasikan B-041.

Tetapkan:

B-041 BLOCKED → B-040.

Jika B-040 sudah tersedia secara nyata:

implementasikan connection health/state machine berdasarkan contract B-040.

Jangan membuat state machine yang tidak memiliki source of truth.

==================================================
FASE 6 — B-050/B-051/B-052
==================================================

Audit dependency chain.

Cari:

- bot contract,
- provider contract,
- runtime contract,
- installation lifecycle,
- execution model.

Jika semua tersedia:

kerjakan task yang UNBLOCKED.

Jika belum:

jangan membuat runtime architecture.

Tampilkan dependency chain secara eksplisit:

B-050 → missing X
B-051 → depends on B-050/X
B-052 → depends on B-051/provider/runtime contract

==================================================
FASE 7 — JOB/QUEUE/B-090
==================================================

Audit B-090 dan seluruh dependency.

Cari apakah repository sudah memiliki:

- JobEnvelope contract,
- queue abstraction,
- queue adapter,
- retry policy,
- DLQ policy,
- replay policy,
- scheduler contract,
- persistence contract,
- worker execution contract.

Jika tersedia:

implementasikan task yang memang sudah unblocked.

Jika belum:

JANGAN membuat queue architecture sendiri.

JANGAN memilih:

- Redis,
- BullMQ,
- RabbitMQ,
- SQS,
- database queue,
- custom queue

secara sepihak.

Semua itu membutuhkan architecture decision jika repository belum menetapkannya.

==================================================
FASE 8 — OPERATOR / BILLING / TELEMETRY / RELEASE
==================================================

Audit seluruh roadmap untuk:

- operator controls,
- billing,
- usage,
- telemetry,
- release/deployment lifecycle.

Cari contract yang sudah ada.

Jika tersedia:

kerjakan.

Jika tidak:

jangan membuat speculative system.

Pisahkan:

CONTRACT BLOCKED

dari:

IMPLEMENTATION BLOCKED.

==================================================
FASE 9 — POSTGRESQL
==================================================

Periksa environment:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan PostgreSQL integration tests yang memang sudah ada.

Jangan membuat test baru hanya untuk mengklaim PostgreSQL selesai.

Jika unavailable:

SKIPPED.

Jangan membuat fake database.

==================================================
FASE 10 — MINIO/S3
==================================================

Periksa environment.

Jika test-only MinIO/S3 tersedia:

jalankan smoke test.

Verifikasi:

- upload
- read/download
- metadata
- delete
- cleanup

Jika unavailable:

SKIPPED.

Jangan install infrastructure permanen.

==================================================
FASE 11 — DEFERRED PUBLIC SHARE
==================================================

Audit ulang:

- rate limiting
- audit event
- share expiry

Jika contract sudah tersedia:

implementasikan.

Jika belum:

tetap deferred.

Jangan membuat architecture baru.

==================================================
FASE 12 — SECURITY AUDIT
==================================================

Pastikan pekerjaan sebelumnya tidak rusak.

Audit:

- workspace isolation,
- authorization,
- file ownership,
- share authorization,
- token handling,
- object storage access,
- secret handling,
- path traversal,
- error sanitization.

Jika menemukan BUG nyata:

perbaiki.

Jika tidak:

jangan melakukan refactor hanya untuk membuat diff.

==================================================
FASE 13 — VALIDATION
==================================================

Jalankan validation yang tersedia:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

JANGAN membuat:

`node scripts/check-symlinks.mjs`

jika memang tidak tersedia.

Jangan mengubah test untuk membuat PASS.

==================================================
FASE 14 — GIT
==================================================

Jika ada perubahan valid:

review:

`git diff --stat`

`git diff`

Hapus semua:

- temporary files,
- credentials,
- secrets,
- generated junk,
- unrelated changes,
- speculative implementation.

Jika perubahan valid:

buat SATU commit yang sesuai.

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

WORKING TREE CLEAN

Jika tidak ada perubahan:

JANGAN membuat empty commit.

==================================================
FASE 15 — FINAL DEPENDENCY REPORT
==================================================

Setelah seluruh audit dan implementation selesai, tampilkan:

# COMPLETED

Daftar task yang benar-benar selesai.

# IMPLEMENTED THIS RUN

Hanya task yang benar-benar berubah pada run ini.

# BLOCKED BY CONTRACT

Tampilkan:

- task,
- contract yang hilang,
- keputusan yang harus dibuat.

# BLOCKED BY INFRASTRUCTURE

Tampilkan:

- task,
- infrastructure yang hilang.

# BLOCKED BY ENVIRONMENT

Tampilkan:

- PostgreSQL,
- MinIO/S3,
- secret manager,
- environment lain.

# SECURITY STATUS

Tampilkan:

- workspace isolation
- authorization
- file/share security
- secret handling
- storage security

# VALIDATION

Tampilkan:

- test
- build
- typecheck
- lint
- format
- imports
- ownership
- docs
- diff check
- PostgreSQL
- MinIO/S3
- symlink check

# GIT

Tampilkan:

- branch
- commit SHA
- remote SHA
- push status
- working tree

# FINAL ROADMAP

Urutkan task berdasarkan dependency.

Gunakan format:

1. B-040 — BLOCKED
   Missing: ...

2. B-041 — BLOCKED BY B-040

3. B-050 — BLOCKED
   Missing: ...

dst.

Jangan membuat task baru.

==================================================
FINAL STOP CONDITION
==================================================

STOP hanya jika:

1. semua task UNBLOCKED sudah dikerjakan,

DAN

2. semua task tersisa sudah dikategorikan secara jelas sebagai:
   - contract blocked,
   - architecture decision blocked,
   - infrastructure blocked,
   - environment blocked,

DAN

3. tidak ada implementation aman yang tersisa di repository.

Jika kondisi tersebut tercapai, JANGAN membuat code speculative.

Berikan laporan bahwa repository sudah mencapai:

`NO SAFE CONTRACT-BACKED IMPLEMENTATION REMAINS`

dan jelaskan EXACTLY keputusan/dependency eksternal yang diperlukan untuk membuka roadmap berikutnya.

PENTING:

Jangan hanya mengatakan "blocked" tanpa melakukan audit.

Cari seluruh repository terlebih dahulu.

Jika ada pekerjaan yang bisa dilakukan dengan aman → KERJAKAN.

Jika tidak ada → jangan mengarang.

Kerjakan langsung pada:

`/root/botspace`

```
# Prompt — Full Roadmap Completion / Dependency-Aware
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
STATUS TERAKHIR
==================================================

Repository saat ini sudah melalui:

- B-030 Workspace API/Contract — DONE
- B-070 Storage Adapter — DONE
- B-071 File/Share Contract — DONE
- B-071 File/Share API — DONE
- B-071 Production Wiring — DONE
- SecretResolver application boundary — DONE
- Infrastructure verification yang dapat dilakukan dari repository — DONE
- File/share security regression — DONE
- Workspace isolation — DONE
- Local SHA dan remote SHA — SAMA
- Working tree — CLEAN

Status terakhir menunjukkan:

Remaining Roadmap:

1. B-040 Telegram account connection
   - contract dan implementation belum tersedia.
2. B-041 connection health/state machine
   - bergantung pada B-040.
3. B-050/B-051/B-052
   - masih menunggu bot/provider/runtime contracts.
4. B-090
   - membutuhkan JobEnvelope, queue adapter, retry/DLQ/replay policy,
     scheduler persistence contract.
5. Operator/billing/telemetry/release
   - contract belum tersedia.
6. Share expiry
   - menunggu approved contract/schema/migration.
7. Public-share rate limiting
   - menunggu approved policy/middleware boundary.
8. Public-share audit event
   - menunggu approved event/service/repository boundary.
9. PostgreSQL integration verification
   - hanya dapat dijalankan jika `PERSISTENCE_TEST_DATABASE_URL` tersedia.
10. MinIO/S3 smoke test
   - hanya dapat dijalankan jika test environment tersedia.
11. `scripts/check-symlinks.mjs`
   - memang tidak tersedia dan JANGAN dibuat hanya untuk validation.

==================================================
TUJUAN PROMPT INI
==================================================

Lakukan FINAL ROADMAP CLOSURE AUDIT.

Tujuannya bukan membuat code secara paksa.

Tujuannya:

1. memastikan tidak ada task repository yang sebenarnya sudah UNBLOCKED,
2. memastikan tidak ada dependency yang terlewat,
3. memastikan semua completed task benar-benar valid,
4. memastikan semua deferred task memiliki alasan dependency yang nyata,
5. mengidentifikasi EXACTLY apa yang dibutuhkan agar project bisa lanjut,
6. melakukan implementation hanya jika dependency benar-benar tersedia,
7. melakukan documentation/ADR update hanya jika repository memang sudah memiliki mekanisme dokumentasi/ADR untuk keputusan tersebut.

JANGAN membuat architecture speculative.

==================================================
ATURAN MUTLAK
==================================================

JANGAN:

- membuat Telegram account connection contract berdasarkan asumsi,
- memilih Telegram authentication method sendiri,
- membuat Telegram polling,
- membuat Telegram webhook,
- membuat MTProto implementation,
- membuat QR login,
- membuat phone login,
- membuat session system,
- membuat fake Telegram connection,
- membuat provider abstraction baru jika belum ada contract,
- membuat BotInstallation runtime,
- mengubah `BotInstallation.status`,
- membuat queue architecture speculative,
- membuat JobEnvelope speculative,
- membuat billing architecture speculative,
- membuat telemetry architecture speculative,
- membuat release architecture speculative,
- membuat share expiry tanpa contract/schema,
- membuat rate limiter tanpa approved policy,
- membuat audit event system baru tanpa approved boundary,
- membuat fake PostgreSQL,
- menggunakan SQLite sebagai pengganti PostgreSQL,
- membuat fake MinIO,
- membuat credential production palsu,
- membuat `scripts/check-symlinks.mjs`.

Jangan mengubah code hanya supaya jumlah "remaining task" berkurang.

==================================================
FASE 1 — AUDIT ROADMAP AKTUAL
==================================================

Audit repository langsung.

Jalankan:

`cd /root/botspace`

`git status`

`git branch --show-current`

`git log --oneline -30`

Kemudian cari seluruh roadmap/task:

- B-*
- F-*
- Phase *
- V2
- TODO
- FIXME
- deferred
- blocked
- dependency
- ADR

Jangan hanya menggunakan laporan AI sebelumnya.

Source of truth adalah repository.

==================================================
FASE 2 — DEPENDENCY GRAPH
==================================================

Bangun dependency graph aktual untuk SEMUA task yang belum selesai.

Untuk setiap task:

- Task ID
- Nama
- Status
- Existing contract?
- Existing implementation?
- Existing tests?
- Dependency
- External dependency?
- Environment dependency?
- Architecture decision dependency?
- UNBLOCKED / BLOCKED

Kategori:

A. DONE
B. UNBLOCKED — BOLEH DIKERJAKAN
C. ENVIRONMENT BLOCKED
D. CONTRACT BLOCKED
E. ARCHITECTURE DECISION BLOCKED
F. EXTERNAL INFRASTRUCTURE BLOCKED

==================================================
FASE 3 — CARI TASK UNBLOCKED
==================================================

Ini sangat penting.

Jangan menganggap semua task setelah B-040 otomatis blocked.

Cari seluruh repository dan pastikan apakah ada task lain yang:

- tidak bergantung B-040,
- contract-nya sudah tersedia,
- implementation boundary-nya sudah jelas,
- dapat dikerjakan tanpa speculative architecture.

Jika ada:

KERJAKAN SEKARANG.

Lakukan:

IMPLEMENT
→ TEST
→ BUILD
→ TYPECHECK
→ LINT
→ REVIEW
→ COMMIT

Jangan berhenti pada audit jika task benar-benar UNBLOCKED.

==================================================
FASE 4 — B-040 TELEGRAM ACCOUNT CONNECTION
==================================================

Audit B-040 secara menyeluruh.

Cari apakah repository memiliki:

- Telegram account model,
- connection contract,
- authentication contract,
- credential/session contract,
- provider contract,
- account lifecycle contract,
- secret storage boundary,
- OAuth/device-code/browser-login mechanism,
- ADR yang menentukan authentication method.

Jika SEMUA tersedia:

implementasikan B-040 secara nyata.

Jika contract belum tersedia:

JANGAN mengarang implementation.

Cari dan dokumentasikan EXACT dependency yang hilang.

Contoh output internal:

B-040 BLOCKED
Reason:
Telegram account connection contract unavailable.

Missing decisions:
- authentication mechanism
- account/session lifecycle
- credential storage
- connection/disconnection semantics
- health semantics

Jangan membuat contract sendiri hanya untuk menghilangkan blocker.

==================================================
FASE 5 — B-041
==================================================

Audit B-041.

Jika B-040 belum tersedia:

JANGAN implementasikan B-041.

Tetapkan:

B-041 BLOCKED → B-040.

Jika B-040 sudah tersedia secara nyata:

implementasikan connection health/state machine berdasarkan contract B-040.

Jangan membuat state machine yang tidak memiliki source of truth.

==================================================
FASE 6 — B-050/B-051/B-052
==================================================

Audit dependency chain.

Cari:

- bot contract,
- provider contract,
- runtime contract,
- installation lifecycle,
- execution model.

Jika semua tersedia:

kerjakan task yang UNBLOCKED.

Jika belum:

jangan membuat runtime architecture.

Tampilkan dependency chain secara eksplisit:

B-050 → missing X
B-051 → depends on B-050/X
B-052 → depends on B-051/provider/runtime contract

==================================================
FASE 7 — JOB/QUEUE/B-090
==================================================

Audit B-090 dan seluruh dependency.

Cari apakah repository sudah memiliki:

- JobEnvelope contract,
- queue abstraction,
- queue adapter,
- retry policy,
- DLQ policy,
- replay policy,
- scheduler contract,
- persistence contract,
- worker execution contract.

Jika tersedia:

implementasikan task yang memang sudah unblocked.

Jika belum:

JANGAN membuat queue architecture sendiri.

JANGAN memilih:

- Redis,
- BullMQ,
- RabbitMQ,
- SQS,
- database queue,
- custom queue

secara sepihak.

Semua itu membutuhkan architecture decision jika repository belum menetapkannya.

==================================================
FASE 8 — OPERATOR / BILLING / TELEMETRY / RELEASE
==================================================

Audit seluruh roadmap untuk:

- operator controls,
- billing,
- usage,
- telemetry,
- release/deployment lifecycle.

Cari contract yang sudah ada.

Jika tersedia:

kerjakan.

Jika tidak:

jangan membuat speculative system.

Pisahkan:

CONTRACT BLOCKED

dari:

IMPLEMENTATION BLOCKED.

==================================================
FASE 9 — POSTGRESQL
==================================================

Periksa environment:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan PostgreSQL integration tests yang memang sudah ada.

Jangan membuat test baru hanya untuk mengklaim PostgreSQL selesai.

Jika unavailable:

SKIPPED.

Jangan membuat fake database.

==================================================
FASE 10 — MINIO/S3
==================================================

Periksa environment.

Jika test-only MinIO/S3 tersedia:

jalankan smoke test.

Verifikasi:

- upload
- read/download
- metadata
- delete
- cleanup

Jika unavailable:

SKIPPED.

Jangan install infrastructure permanen.

==================================================
FASE 11 — DEFERRED PUBLIC SHARE
==================================================

Audit ulang:

- rate limiting
- audit event
- share expiry

Jika contract sudah tersedia:

implementasikan.

Jika belum:

tetap deferred.

Jangan membuat architecture baru.

==================================================
FASE 12 — SECURITY AUDIT
==================================================

Pastikan pekerjaan sebelumnya tidak rusak.

Audit:

- workspace isolation,
- authorization,
- file ownership,
- share authorization,
- token handling,
- object storage access,
- secret handling,
- path traversal,
- error sanitization.

Jika menemukan BUG nyata:

perbaiki.

Jika tidak:

jangan melakukan refactor hanya untuk membuat diff.

==================================================
FASE 13 — VALIDATION
==================================================

Jalankan validation yang tersedia:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

JANGAN membuat:

`node scripts/check-symlinks.mjs`

jika memang tidak tersedia.

Jangan mengubah test untuk membuat PASS.

==================================================
FASE 14 — GIT
==================================================

Jika ada perubahan valid:

review:

`git diff --stat`

`git diff`

Hapus semua:

- temporary files,
- credentials,
- secrets,
- generated junk,
- unrelated changes,
- speculative implementation.

Jika perubahan valid:

buat SATU commit yang sesuai.

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

WORKING TREE CLEAN

Jika tidak ada perubahan:

JANGAN membuat empty commit.

==================================================
FASE 15 — FINAL DEPENDENCY REPORT
==================================================

Setelah seluruh audit dan implementation selesai, tampilkan:

# COMPLETED

Daftar task yang benar-benar selesai.

# IMPLEMENTED THIS RUN

Hanya task yang benar-benar berubah pada run ini.

# BLOCKED BY CONTRACT

Tampilkan:

- task,
- contract yang hilang,
- keputusan yang harus dibuat.

# BLOCKED BY INFRASTRUCTURE

Tampilkan:

- task,
- infrastructure yang hilang.

# BLOCKED BY ENVIRONMENT

Tampilkan:

- PostgreSQL,
- MinIO/S3,
- secret manager,
- environment lain.

# SECURITY STATUS

Tampilkan:

- workspace isolation
- authorization
- file/share security
- secret handling
- storage security

# VALIDATION

Tampilkan:

- test
- build
- typecheck
- lint
- format
- imports
- ownership
- docs
- diff check
- PostgreSQL
- MinIO/S3
- symlink check

# GIT

Tampilkan:

- branch
- commit SHA
- remote SHA
- push status
- working tree

# FINAL ROADMAP

Urutkan task berdasarkan dependency.

Gunakan format:

1. B-040 — BLOCKED
   Missing: ...

2. B-041 — BLOCKED BY B-040

3. B-050 — BLOCKED
   Missing: ...

dst.

Jangan membuat task baru.

==================================================
FINAL STOP CONDITION
==================================================

STOP hanya jika:

1. semua task UNBLOCKED sudah dikerjakan,

DAN

2. semua task tersisa sudah dikategorikan secara jelas sebagai:
   - contract blocked,
   - architecture decision blocked,
   - infrastructure blocked,
   - environment blocked,

DAN

3. tidak ada implementation aman yang tersisa di repository.

Jika kondisi tersebut tercapai, JANGAN membuat code speculative.

Berikan laporan bahwa repository sudah mencapai:

`NO SAFE CONTRACT-BACKED IMPLEMENTATION REMAINS`

dan jelaskan EXACTLY keputusan/dependency eksternal yang diperlukan untuk membuka roadmap berikutnya.

PENTING:

Jangan hanya mengatakan "blocked" tanpa melakukan audit.

Cari seluruh repository terlebih dahulu.

Jika ada pekerjaan yang bisa dilakukan dengan aman → KERJAKAN.

Jika tidak ada → jangan mengarang.

Kerjakan langsung pada:

`/root/botspace`

```
# Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
STATUS TERAKHIR
==================================================

Repository saat ini sudah melalui:

- B-030 Workspace API/Contract — DONE
- B-070 Storage Adapter — DONE
- B-071 File/Share Contract — DONE
- B-071 File/Share API — DONE
- B-071 Production Wiring — DONE
- SecretResolver application boundary — DONE
- Infrastructure verification yang dapat dilakukan dari repository — DONE
- File/share security regression — DONE
- Workspace isolation — DONE
- Local SHA dan remote SHA — SAMA
- Working tree — CLEAN

Status terakhir menunjukkan:

Remaining Roadmap:

1. B-040 Telegram account connection
   - contract dan implementation belum tersedia.
2. B-041 connection health/state machine
   - bergantung pada B-040.
3. B-050/B-051/B-052
   - masih menunggu bot/provider/runtime contracts.
4. B-090
   - membutuhkan JobEnvelope, queue adapter, retry/DLQ/replay policy,
     scheduler persistence contract.
5. Operator/billing/telemetry/release
   - contract belum tersedia.
6. Share expiry
   - menunggu approved contract/schema/migration.
7. Public-share rate limiting
   - menunggu approved policy/middleware boundary.
8. Public-share audit event
   - menunggu approved event/service/repository boundary.
9. PostgreSQL integration verification
   - hanya dapat dijalankan jika `PERSISTENCE_TEST_DATABASE_URL` tersedia.
10. MinIO/S3 smoke test
   - hanya dapat dijalankan jika test environment tersedia.
11. `scripts/check-symlinks.mjs`
   - memang tidak tersedia dan JANGAN dibuat hanya untuk validation.

==================================================
TUJUAN PROMPT INI
==================================================

Lakukan FINAL ROADMAP CLOSURE AUDIT.

Tujuannya bukan membuat code secara paksa.

Tujuannya:

1. memastikan tidak ada task repository yang sebenarnya sudah UNBLOCKED,
2. memastikan tidak ada dependency yang terlewat,
3. memastikan semua completed task benar-benar valid,
4. memastikan semua deferred task memiliki alasan dependency yang nyata,
5. mengidentifikasi EXACTLY apa yang dibutuhkan agar project bisa lanjut,
6. melakukan implementation hanya jika dependency benar-benar tersedia,
7. melakukan documentation/ADR update hanya jika repository memang sudah memiliki mekanisme dokumentasi/ADR untuk keputusan tersebut.

JANGAN membuat architecture speculative.

==================================================
ATURAN MUTLAK
==================================================

JANGAN:

- membuat Telegram account connection contract berdasarkan asumsi,
- memilih Telegram authentication method sendiri,
- membuat Telegram polling,
- membuat Telegram webhook,
- membuat MTProto implementation,
- membuat QR login,
- membuat phone login,
- membuat session system,
- membuat fake Telegram connection,
- membuat provider abstraction baru jika belum ada contract,
- membuat BotInstallation runtime,
- mengubah `BotInstallation.status`,
- membuat queue architecture speculative,
- membuat JobEnvelope speculative,
- membuat billing architecture speculative,
- membuat telemetry architecture speculative,
- membuat release architecture speculative,
- membuat share expiry tanpa contract/schema,
- membuat rate limiter tanpa approved policy,
- membuat audit event system baru tanpa approved boundary,
- membuat fake PostgreSQL,
- menggunakan SQLite sebagai pengganti PostgreSQL,
- membuat fake MinIO,
- membuat credential production palsu,
- membuat `scripts/check-symlinks.mjs`.

Jangan mengubah code hanya supaya jumlah "remaining task" berkurang.

==================================================
FASE 1 — AUDIT ROADMAP AKTUAL
==================================================

Audit repository langsung.

Jalankan:

`cd /root/botspace`

`git status`

`git branch --show-current`

`git log --oneline -30`

Kemudian cari seluruh roadmap/task:

- B-*
- F-*
- Phase *
- V2
- TODO
- FIXME
- deferred
- blocked
- dependency
- ADR

Jangan hanya menggunakan laporan AI sebelumnya.

Source of truth adalah repository.

==================================================
FASE 2 — DEPENDENCY GRAPH
==================================================

Bangun dependency graph aktual untuk SEMUA task yang belum selesai.

Untuk setiap task:

- Task ID
- Nama
- Status
- Existing contract?
- Existing implementation?
- Existing tests?
- Dependency
- External dependency?
- Environment dependency?
- Architecture decision dependency?
- UNBLOCKED / BLOCKED

Kategori:

A. DONE
B. UNBLOCKED — BOLEH DIKERJAKAN
C. ENVIRONMENT BLOCKED
D. CONTRACT BLOCKED
E. ARCHITECTURE DECISION BLOCKED
F. EXTERNAL INFRASTRUCTURE BLOCKED

==================================================
FASE 3 — CARI TASK UNBLOCKED
==================================================

Ini sangat penting.

Jangan menganggap semua task setelah B-040 otomatis blocked.

Cari seluruh repository dan pastikan apakah ada task lain yang:

- tidak bergantung B-040,
- contract-nya sudah tersedia,
- implementation boundary-nya sudah jelas,
- dapat dikerjakan tanpa speculative architecture.

Jika ada:

KERJAKAN SEKARANG.

Lakukan:

IMPLEMENT
→ TEST
→ BUILD
→ TYPECHECK
→ LINT
→ REVIEW
→ COMMIT

Jangan berhenti pada audit jika task benar-benar UNBLOCKED.

==================================================
FASE 4 — B-040 TELEGRAM ACCOUNT CONNECTION
==================================================

Audit B-040 secara menyeluruh.

Cari apakah repository memiliki:

- Telegram account model,
- connection contract,
- authentication contract,
- credential/session contract,
- provider contract,
- account lifecycle contract,
- secret storage boundary,
- OAuth/device-code/browser-login mechanism,
- ADR yang menentukan authentication method.

Jika SEMUA tersedia:

implementasikan B-040 secara nyata.

Jika contract belum tersedia:

JANGAN mengarang implementation.

Cari dan dokumentasikan EXACT dependency yang hilang.

Contoh output internal:

B-040 BLOCKED
Reason:
Telegram account connection contract unavailable.

Missing decisions:
- authentication mechanism
- account/session lifecycle
- credential storage
- connection/disconnection semantics
- health semantics

Jangan membuat contract sendiri hanya untuk menghilangkan blocker.

==================================================
FASE 5 — B-041
==================================================

Audit B-041.

Jika B-040 belum tersedia:

JANGAN implementasikan B-041.

Tetapkan:

B-041 BLOCKED → B-040.

Jika B-040 sudah tersedia secara nyata:

implementasikan connection health/state machine berdasarkan contract B-040.

Jangan membuat state machine yang tidak memiliki source of truth.

==================================================
FASE 6 — B-050/B-051/B-052
==================================================

Audit dependency chain.

Cari:

- bot contract,
- provider contract,
- runtime contract,
- installation lifecycle,
- execution model.

Jika semua tersedia:

kerjakan task yang UNBLOCKED.

Jika belum:

jangan membuat runtime architecture.

Tampilkan dependency chain secara eksplisit:

B-050 → missing X
B-051 → depends on B-050/X
B-052 → depends on B-051/provider/runtime contract

==================================================
FASE 7 — JOB/QUEUE/B-090
==================================================

Audit B-090 dan seluruh dependency.

Cari apakah repository sudah memiliki:

- JobEnvelope contract,
- queue abstraction,
- queue adapter,
- retry policy,
- DLQ policy,
- replay policy,
- scheduler contract,
- persistence contract,
- worker execution contract.

Jika tersedia:

implementasikan task yang memang sudah unblocked.

Jika belum:

JANGAN membuat queue architecture sendiri.

JANGAN memilih:

- Redis,
- BullMQ,
- RabbitMQ,
- SQS,
- database queue,
- custom queue

secara sepihak.

Semua itu membutuhkan architecture decision jika repository belum menetapkannya.

==================================================
FASE 8 — OPERATOR / BILLING / TELEMETRY / RELEASE
==================================================

Audit seluruh roadmap untuk:

- operator controls,
- billing,
- usage,
- telemetry,
- release/deployment lifecycle.

Cari contract yang sudah ada.

Jika tersedia:

kerjakan.

Jika tidak:

jangan membuat speculative system.

Pisahkan:

CONTRACT BLOCKED

dari:

IMPLEMENTATION BLOCKED.

==================================================
FASE 9 — POSTGRESQL
==================================================

Periksa environment:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan PostgreSQL integration tests yang memang sudah ada.

Jangan membuat test baru hanya untuk mengklaim PostgreSQL selesai.

Jika unavailable:

SKIPPED.

Jangan membuat fake database.

==================================================
FASE 10 — MINIO/S3
==================================================

Periksa environment.

Jika test-only MinIO/S3 tersedia:

jalankan smoke test.

Verifikasi:

- upload
- read/download
- metadata
- delete
- cleanup

Jika unavailable:

SKIPPED.

Jangan install infrastructure permanen.

==================================================
FASE 11 — DEFERRED PUBLIC SHARE
==================================================

Audit ulang:

- rate limiting
- audit event
- share expiry

Jika contract sudah tersedia:

implementasikan.

Jika belum:

tetap deferred.

Jangan membuat architecture baru.

==================================================
FASE 12 — SECURITY AUDIT
==================================================

Pastikan pekerjaan sebelumnya tidak rusak.

Audit:

- workspace isolation,
- authorization,
- file ownership,
- share authorization,
- token handling,
- object storage access,
- secret handling,
- path traversal,
- error sanitization.

Jika menemukan BUG nyata:

perbaiki.

Jika tidak:

jangan melakukan refactor hanya untuk membuat diff.

==================================================
FASE 13 — VALIDATION
==================================================

Jalankan validation yang tersedia:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

JANGAN membuat:

`node scripts/check-symlinks.mjs`

jika memang tidak tersedia.

Jangan mengubah test untuk membuat PASS.

==================================================
FASE 14 — GIT
==================================================

Jika ada perubahan valid:

review:

`git diff --stat`

`git diff`

Hapus semua:

- temporary files,
- credentials,
- secrets,
- generated junk,
- unrelated changes,
- speculative implementation.

Jika perubahan valid:

buat SATU commit yang sesuai.

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

WORKING TREE CLEAN

Jika tidak ada perubahan:

JANGAN membuat empty commit.

==================================================
FASE 15 — FINAL DEPENDENCY REPORT
==================================================

Setelah seluruh audit dan implementation selesai, tampilkan:

# COMPLETED

Daftar task yang benar-benar selesai.

# IMPLEMENTED THIS RUN

Hanya task yang benar-benar berubah pada run ini.

# BLOCKED BY CONTRACT

Tampilkan:

- task,
- contract yang hilang,
- keputusan yang harus dibuat.

# BLOCKED BY INFRASTRUCTURE

Tampilkan:

- task,
- infrastructure yang hilang.

# BLOCKED BY ENVIRONMENT

Tampilkan:

- PostgreSQL,
- MinIO/S3,
- secret manager,
- environment lain.

# SECURITY STATUS

Tampilkan:

- workspace isolation
- authorization
- file/share security
- secret handling
- storage security

# VALIDATION

Tampilkan:

- test
- build
- typecheck
- lint
- format
- imports
- ownership
- docs
- diff check
- PostgreSQL
- MinIO/S3
- symlink check

# GIT

Tampilkan:

- branch
- commit SHA
- remote SHA
- push status
- working tree

# FINAL ROADMAP

Urutkan task berdasarkan dependency.

Gunakan format:

1. B-040 — BLOCKED
   Missing: ...

2. B-041 — BLOCKED BY B-040

3. B-050 — BLOCKED
   Missing: ...

dst.

Jangan membuat task baru.

==================================================
FINAL STOP CONDITION
==================================================

STOP hanya jika:

1. semua task UNBLOCKED sudah dikerjakan,

DAN

2. semua task tersisa sudah dikategorikan secara jelas sebagai:
   - contract blocked,
   - architecture decision blocked,
   - infrastructure blocked,
   - environment blocked,

DAN

3. tidak ada implementation aman yang tersisa di repository.

Jika kondisi tersebut tercapai, JANGAN membuat code speculative.

Berikan laporan bahwa repository sudah mencapai:

`NO SAFE CONTRACT-BACKED IMPLEMENTATION REMAINS`

dan jelaskan EXACTLY keputusan/dependency eksternal yang diperlukan untuk membuka roadmap berikutnya.

PENTING:

Jangan hanya mengatakan "blocked" tanpa melakukan audit.

Cari seluruh repository terlebih dahulu.

Jika ada pekerjaan yang bisa dilakukan dengan aman → KERJAKAN.

Jika tidak ada → jangan mengarang.

Kerjakan langsung pada:

`/root/botspace`1
```



```
# Prompt — Full Roadmap Completion / Dependency-Aware
```

# Prompt: BotSpace — Full Dependency-Aware Roadmap Completion

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

Dari pekerjaan sebelumnya:

- B-030 Workspace API/Contract SUDAH selesai.
- B-031 Membership/Invitation backend SUDAH selesai.
- F-031 Workspace Settings/Members UI SUDAH selesai.
- B-032 SUDAH selesai sesuai roadmap terakhir.
- B-070 Storage Adapter SUDAH selesai.
- B-071 File/Share contract SUDAH selesai.
- B-071 File/Share API SUDAH selesai.
- B-071 production wiring SUDAH selesai.
- SecretResolver production boundary SUDAH dikerjakan sejauh yang dapat dilakukan dari repository/environment.
- Local SHA dan remote SHA terakhir SUDAH sama.
- Working tree terakhir CLEAN.

Screenshot/status terakhir menunjukkan:

Remaining Deferred:

1. B-040 Telegram account connection:
   - contract dan implementation belum tersedia.
   - B-040 tidak boleh dibuat secara speculative.
   - jangan membuat Telegram polling/runtime hanya untuk menganggap B-040 selesai.

2. B-041 connection health/state machine:
   - bergantung pada B-040.

3. B-050/B-051/B-052:
   - roadmap V2 masih menunjukkan TODO/dependency chain yang belum ditutup.
   - jangan mengarang implementation jika dependency belum ada.

4. PostgreSQL runtime integration:
   - membutuhkan `PERSISTENCE_TEST_DATABASE_URL`.

5. `scripts/check-symlinks.mjs`:
   - tidak tersedia di repository.
   - jangan membuat script palsu hanya untuk membuat validation PASS.

6. Public-share rate limiting:
   - hanya boleh dikerjakan jika approved policy/middleware boundary tersedia.

7. Public-share audit event:
   - hanya boleh dikerjakan jika approved event/service/repository boundary tersedia.

8. Share expiry:
   - tetap deferred jika contract/schema/migration belum menyediakannya.

==================================================
TUJUAN UTAMA
==================================================

Jangan hanya mengulang laporan bahwa B-040 blocked.

Lakukan FULL ROADMAP AUDIT dan kerjakan SEMUA TASK yang:

- dependency-nya sudah tersedia,
- contract-nya sudah tersedia,
- architecture-nya sudah jelas,
- dapat diimplementasikan dengan aman dari repository saat ini.

Jika task benar-benar blocked oleh dependency eksternal/contract yang belum tersedia:

- jangan mengarang contract,
- jangan membuat fake implementation,
- jangan membuat TODO palsu hanya agar terlihat selesai,
- lanjutkan mencari task lain yang tidak blocked.

Teruskan sampai tidak ada lagi task yang aman untuk dikerjakan.

==================================================
ATURAN PALING PENTING
==================================================

JANGAN mengulang pekerjaan yang sudah selesai.

JANGAN mengulang:

- B-030
- B-031
- B-032
- B-070
- B-071 contract
- B-071 API
- B-071 production wiring
- F-002
- F-010
- F-011
- F-012
- F-020
- F-021
- F-030
- F-031
- F-070

Jangan membuat implementation duplicate.

Jangan membuat framework frontend kedua.

Jangan membuat storage abstraction kedua.

Jangan membuat SecretResolver abstraction kedua.

Jangan membuat authorization system kedua.

Jangan membuat database abstraction kedua.

Jangan membuat Telegram runtime speculative.

Jangan mengubah:

`BotInstallation.status`

menjadi process/runtime state.

Jangan membuat Telegram polling.

Jangan membuat Telegram webhook runtime.

Jangan menghubungkan akun Telegram menggunakan metode yang belum ditetapkan contract repository.

Jangan membuat credential Telegram palsu.

Jangan menyentuh Gorouter.app integration test.

NVIDIA dan TokenHarbor tidak perlu disentuh kecuali perubahan repository secara langsung mengharuskannya.

==================================================
FASE 1 — REPOSITORY AUDIT
==================================================

Mulai dengan audit repository aktual.

Jalankan:

`cd /root/botspace`

`git status`

`git branch --show-current`

`git log --oneline -20`

Kemudian audit:

- roadmap,
- TODO,
- dependency graph,
- architecture docs,
- ADR,
- backend modules,
- frontend modules,
- API routes,
- service layer,
- repository layer,
- migrations,
- authentication,
- workspace,
- membership,
- storage,
- file/share,
- SecretResolver,
- deployment configuration,
- Telegram-related code,
- frontend roadmap.

Cari semua task identifier:

- B-*
- F-*
- Phase 1
- Phase 2
- Phase 3
- Phase 4
- Phase 5
- V2

Jangan hanya membaca output AI sebelumnya.

Gunakan repository sebagai source of truth.

==================================================
FASE 2 — BUILD DEPENDENCY GRAPH
==================================================

Buat dependency graph aktual.

Untuk setiap task yang belum selesai:

- task ID,
- status,
- dependency,
- contract available?,
- implementation available?,
- environment required?,
- blocked/unblocked.

Contoh:

B-040
→ contract unavailable
→ BLOCKED

B-041
→ depends on B-040
→ BLOCKED

Task lain
→ dependency available
→ UNBLOCKED
→ IMPLEMENT.

Jangan menganggap urutan nomor task otomatis berarti dependency.

==================================================
FASE 3 — KERJAKAN SEMUA UNBLOCKED BACKEND TASK
==================================================

Untuk setiap backend task yang dependency-nya sudah tersedia:

1. audit existing implementation,
2. implementasikan sesuai architecture,
3. tambahkan test,
4. jalankan validation,
5. perbaiki error,
6. review diff.

Jangan berhenti setelah satu task jika task berikutnya juga sudah unblock.

Teruskan otomatis.

==================================================
FASE 4 — TELEGRAM B-040
==================================================

Untuk B-040:

JANGAN langsung implementasikan.

Audit terlebih dahulu apakah repository sudah menyediakan:

- Telegram account model,
- authentication contract,
- connection contract,
- credential/session storage contract,
- OAuth/device-code/browser-login contract,
- account lifecycle contract,
- secret storage mechanism,
- provider abstraction.

Jika contract tersebut BENAR-BENAR tersedia:

implementasikan B-040 berdasarkan contract tersebut.

Jika tidak tersedia:

JANGAN membuat contract Telegram secara speculative.

JANGAN membuat:

- Telegram polling,
- Telegram bot runtime,
- webhook,
- MTProto implementation,
- session persistence,
- QR login,
- phone login,
- fake connection state.

Dalam kondisi tersebut tandai:

`B-040 BLOCKED — Telegram account connection contract/implementation not available`

Kemudian lanjutkan mencari task lain yang tidak bergantung B-040.

==================================================
FASE 5 — B-041
==================================================

B-041 hanya boleh dikerjakan jika B-040 sudah benar-benar tersedia.

B-041 harus memiliki:

- connection state,
- health state,
- transition rules,
- failure handling,
- reconnect behavior,

HANYA jika architecture B-040 memang sudah menetapkan behavior tersebut.

Jika B-040 blocked:

`B-041 BLOCKED — depends on B-040`

Jangan membuat fake state machine.

==================================================
FASE 6 — FRONTEND TASKS
==================================================

Audit semua F-* task.

Untuk setiap frontend task:

- cek backend contract,
- cek typed API,
- cek route,
- cek dependency,
- cek UI architecture.

Jika backend dependency sudah tersedia:

langsung implementasikan frontend.

Gunakan:

- existing frontend framework,
- existing styling system,
- existing UI primitives,
- existing typed API client,
- existing auth/route guards,
- existing workspace context.

Jangan membuat dummy API.

Jangan membuat hardcoded member/user/file data.

Jangan membuat frontend UI untuk endpoint yang belum ada.

Jika frontend task blocked:

catat dependency sebenarnya.

==================================================
FASE 7 — TYPED API CLIENT
==================================================

Audit seluruh typed API client.

Cari:

- endpoint tanpa typed client,
- response type tidak sesuai backend,
- duplicate request helper,
- raw fetch di feature component,
- inconsistent error mapping.

Jika ada task yang memang sudah memiliki backend contract tetapi typed client belum lengkap:

implementasikan.

Jangan mengubah endpoint backend hanya demi frontend.

==================================================
FASE 8 — AUTHORIZATION AUDIT
==================================================

Audit seluruh route yang sudah ada.

Pastikan:

- authentication,
- workspace isolation,
- membership authorization,
- owner protection,
- cross-workspace denial.

Jangan percaya role dari client.

Backend tetap menjadi security boundary.

Jika menemukan security bug nyata:

perbaiki.

Tambahkan regression test.

==================================================
FASE 9 — FILE/SHARE REGRESSION
==================================================

Jangan mengimplementasikan ulang B-071.

Tetapi lakukan regression audit terhadap:

- upload,
- download,
- share,
- revoke,
- workspace isolation,
- object storage,
- token digest,
- path traversal,
- unauthorized access.

Jika menemukan bug nyata:

perbaiki.

Jika tidak ada bug:

jangan mengubah implementation.

==================================================
FASE 10 — SECRETRESOLVER
==================================================

Audit production SecretResolver terakhir.

Pastikan:

- application menggunakan existing SecretResolver,
- deployment boundary benar,
- tidak ada secret hardcoded,
- test resolver injectable,
- error tidak membocorkan secret,
- storage credential tidak bocor.

Jika managed secret manager nyata tidak tersedia:

jangan membuat fake production integration.

Status:

`DEFERRED — managed secret manager unavailable`

==================================================
FASE 11 — POSTGRESQL
==================================================

Periksa:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan PostgreSQL integration test.

Jika tidak tersedia:

jangan membuat database palsu.

Jangan menggunakan SQLite sebagai pengganti.

Catat:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jika test gagal:

diagnosis root cause.

Perbaiki jika masalah memang berasal dari code.

Jangan mematikan test.

==================================================
FASE 12 — MINIO/S3
==================================================

Periksa environment MinIO/S3-compatible.

Jika tersedia:

jalankan smoke test:

1. upload,
2. read,
3. verify,
4. metadata,
5. delete,
6. verify cleanup.

Gunakan test-only credential.

Jangan menggunakan credential production.

Jika unavailable:

`SKIPPED — MinIO/S3 test environment unavailable`

==================================================
FASE 13 — PUBLIC SHARE RATE LIMIT
==================================================

Audit apakah approved boundary sudah tersedia.

Jika tersedia:

implementasikan sesuai policy.

Jika belum:

JANGAN membuat arbitrary rate limiter.

Jangan menentukan angka sendiri.

Status:

`DEFERRED — approved rate-limit boundary unavailable`

==================================================
FASE 14 — PUBLIC SHARE AUDIT
==================================================

Audit apakah audit event boundary tersedia.

Jika tersedia:

implementasikan sesuai contract.

Jika belum:

jangan membuat audit architecture baru.

Status:

`DEFERRED — approved audit-event boundary unavailable`

==================================================
FASE 15 — SHARE EXPIRY
==================================================

Jangan implementasikan expiry jika contract/schema belum mendukung.

Jangan membuat:

- expiresAt,
- migration,
- scheduler,
- cleanup worker,
- expiry token.

Status:

`DEFERRED — approved contract/schema/migration required`

==================================================
FASE 16 — V2 TASKS
==================================================

Audit:

B-050
B-051
B-052

dan seluruh V2 roadmap.

Jangan menganggap TODO berarti harus langsung dibuat.

Untuk setiap task:

1. baca dependency,
2. cari contract,
3. cari ADR,
4. cari implementation prerequisite.

Jika dependency tersedia:

KERJAKAN.

Jika dependency belum tersedia:

BLOCKED.

Jangan mengisi V2 dengan speculative implementation.

==================================================
FASE 17 — TESTING
==================================================

Untuk setiap perubahan yang dibuat:

jalankan test yang relevan.

Kemudian jalankan full validation:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

Untuk:

`node scripts/check-symlinks.mjs`

jika tidak tersedia:

JANGAN membuat file tersebut.

Catat:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

==================================================
FASE 18 — FIX LOOP
==================================================

Jika validation gagal:

Jangan berhenti.

Lakukan:

READ ERROR
→ FIND ROOT CAUSE
→ FIX
→ TEST
→ BUILD
→ TYPECHECK
→ LINT
→ REVIEW.

Jangan:

- disable test,
- disable lint,
- menurunkan TypeScript strictness,
- menghapus assertion,
- fake PASS,
- skip test tanpa alasan environment yang nyata.

==================================================
FASE 19 — TYPESCRIPT/PARSER AUDIT
==================================================

Cari:

`<<<<<<<`

`=======`

`>>>>>>>`

Cari juga:

- malformed JSX,
- duplicate imports,
- duplicate exports,
- broken generics,
- invalid route definitions,
- syntax errors,
- accidental terminal output,
- broken JSON,
- broken migration,
- invalid SQL.

Perbaiki jika nyata.

==================================================
FASE 20 — DOCUMENTATION
==================================================

Update dokumentasi/status hanya jika memang diperlukan.

Jangan membuat README baru.

Gunakan README/documentation yang sudah ada.

Jika roadmap/status perlu diperbarui:

update existing documentation.

Jangan membuat file dokumentasi duplikat.

==================================================
FASE 21 — SECURITY REVIEW
==================================================

Sebelum commit audit:

- secrets,
- credentials,
- API keys,
- tokens,
- Telegram sessions,
- storage keys,
- authorization,
- workspace isolation,
- path traversal,
- error leakage,
- log leakage.

Jangan pernah commit:

`.env`

credentials

private keys

session files

real tokens.

==================================================
FASE 22 — DIFF REVIEW
==================================================

Jalankan:

`git status`

`git diff --stat`

Review seluruh diff.

Hapus perubahan yang:

- unrelated,
- speculative,
- duplicate,
- generated junk,
- temporary,
- debugging.

Jangan memasukkan perubahan yang tidak diperlukan.

==================================================
FASE 23 — COMMIT STRATEGY
==================================================

Jika ada perubahan valid:

buat commit yang logis.

Jika perubahan hanya satu coherent task:

gunakan satu commit.

Jika beberapa task independen sudah dikerjakan:

boleh membuat commit terpisah jika repository workflow memang cocok.

Jangan membuat empty commit.

==================================================
FASE 24 — PUSH
==================================================

Setelah validation PASS:

`git push origin backend-dev-recovery`

Kemudian:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

WORKING TREE CLEAN

Jika push gagal:

- jangan force push,
- jangan reset --hard,
- jangan hapus commit,
- jangan mengubah credential GitHub sembarangan.

==================================================
FASE 25 — NEXT ROADMAP LOOP
==================================================

Setelah push:

AUDIT ROADMAP LAGI.

Cari task berikutnya.

Jika ada task UNBLOCKED:

KERJAKAN LANGSUNG.

Jika task blocked:

lanjut cari task lain.

Jangan berhenti hanya karena B-040 blocked.

Teruskan sampai:

- semua task yang feasible sudah selesai,
- atau semua task tersisa memang memiliki dependency yang belum tersedia.

==================================================
STOP CONDITION
==================================================

Hanya berhenti jika:

A. seluruh task yang feasible sudah selesai,

ATAU

B. semua task yang tersisa benar-benar blocked oleh:

- contract yang belum tersedia,
- infrastructure yang belum tersedia,
- environment yang belum tersedia,
- external architecture decision,
- approved policy yang belum tersedia.

Jangan membuat pekerjaan speculative hanya untuk menghindari stop condition.

==================================================
OUTPUT FINAL
==================================================

Tampilkan:

# Completed This Run

Daftar task yang benar-benar dikerjakan.

Untuk setiap task:

- ID
- implementation
- tests
- status
- commit

# Blocked

Untuk setiap blocked task:

- ID
- alasan
- dependency yang hilang
- apakah dependency internal/external/environment.

# Validation

- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:
- symlink:

# Infrastructure

- PostgreSQL:
- MinIO/S3:
- SecretResolver:

# Security

- workspace isolation:
- authorization:
- secrets:
- token handling:
- storage access:

# Git

- branch:
- commit SHA:
- remote SHA:
- push:
- working tree:

# Remaining Roadmap

Urutkan task berdasarkan dependency nyata.

Jangan membuat task baru hanya agar roadmap terlihat panjang.

==================================================
ATURAN TERAKHIR
==================================================

KERJAKAN LANGSUNG.

Jangan hanya memberikan rekomendasi.

Jangan berhenti pada audit jika ada task yang bisa diimplementasikan.

Jangan mengarang dependency.

Jangan mengarang Telegram contract.

Jangan membuat Telegram runtime speculative.

Jangan membuat fake production infrastructure.

Jangan mengulang task yang sudah selesai.

Jangan menyentuh Gorouter.app.

Jangan mengubah BotInstallation.status.

Jangan menambahkan share expiry tanpa contract.

Jangan membuat `scripts/check-symlinks.mjs`.

Gunakan repository sebagai source of truth.

Kerjakan sampai semua pekerjaan yang feasible benar-benar selesai.

Repository:
`/root/botspace`

```
# Prompt: B-031 → F-031 → Continue Frontend Roadmap
```
Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

Frontend roadmap sebelumnya sudah dikerjakan sampai:

- F-002 frontend framework/styling
- F-010 web application shell
- F-011 UI primitives
- F-012 typed API client
- F-020/F-021 authentication state + route guards
- F-030 workspace dashboard/context
- F-070 real File/Share UI terhadap B-071 API

Dari audit terakhir, repository sekarang menyatakan:

NEXT FRONTEND TASK:

`F-031 Workspace settings and members UI`

Tetapi F-031 BELUM boleh diimplementasikan penuh karena dependency backend:

`B-031 Membership/Invitation HTTP contract + API`

belum tersedia.

Jadi dependency order sekarang adalah:

B-031
→ F-031
→ audit roadmap berikutnya
→ lanjut task yang dependency-nya sudah tersedia.

Jangan membuat speculative F-031 dengan fake member/invitation API.

==================================================
ATURAN PENTING
==================================================

Jangan mengulang:

- B-030 Workspace API/Contract
- B-070 Storage Adapter
- B-071 File/Share contract
- B-071 File/Share API
- B-071 production wiring
- SecretResolver work yang sudah selesai
- F-002
- F-010
- F-011
- F-012
- F-020/F-021
- F-030
- F-070

Gunakan implementasi yang sudah ada sebagai source of truth.

Jangan membuat framework frontend kedua.

Jangan membuat API palsu.

Jangan membuat database schema berdasarkan asumsi.

Jangan mengubah contract B-030/B-071 jika tidak benar-benar diperlukan oleh B-031.

Jangan membuat Telegram polling/webhook runtime.

Jangan mengubah `BotInstallation.status`.

Jangan menyentuh Gorouter.app integration test.

NVIDIA dan TokenHarbor tidak perlu disentuh.

==================================================
FASE 0 — AUDIT REPOSITORY
==================================================

Sebelum mengubah kode:

1. `cd /root/botspace`
2. `git status`
3. `git branch --show-current`
4. `git log --oneline -15`
5. audit roadmap.
6. audit B-030 workspace contract.
7. audit existing user/account model.
8. audit existing authentication/session model.
9. audit workspace ownership.
10. audit existing PostgreSQL schema/migrations.
11. audit existing repository patterns.
12. audit existing service patterns.
13. audit existing HTTP route patterns.
14. audit typed frontend API client.
15. audit frontend workspace context.
16. audit F-030 dashboard implementation.
17. cari apakah B-031 sudah sebagian tersedia.
18. cari semua reference ke:
    - member
    - membership
    - invitation
    - workspace member
    - invite
    - role
    - owner
    - admin
    - member permissions.

Jangan langsung membuat kode.

Tentukan terlebih dahulu dependency B-031 yang benar-benar sudah ada.

==================================================
FASE 1 — B-031 CONTRACT AUDIT
==================================================

Tentukan contract minimum B-031 berdasarkan repository.

Membership system minimal perlu memiliki konsep:

- workspace,
- user/account,
- membership,
- role/permission jika memang sudah menjadi bagian architecture,
- invitation jika roadmap memang memerlukannya.

Tetapi JANGAN mengarang field.

Gunakan model/contract yang sudah ada jika tersedia.

Cari apakah repository sudah memiliki:

- User identity,
- Workspace identity,
- Workspace owner,
- membership relation,
- role enum,
- authorization abstraction,
- invitation token abstraction.

Jika sebagian sudah tersedia:

gunakan kembali.

Jangan membuat duplicate abstraction.

==================================================
FASE 2 — B-031 MEMBERSHIP DOMAIN/CONTRACT
==================================================

Jika contract membership belum tersedia:

implementasikan contract/domain minimum yang memang dibutuhkan F-031.

Membership harus memiliki:

- stable identifier jika memang diperlukan,
- workspace ownership,
- user/account reference,
- role/access information sesuai existing authorization architecture,
- active/inactive state jika memang diperlukan oleh existing contract.

Jangan menambahkan permission system besar.

Gunakan role model paling minimal yang sesuai repository.

Contoh:

OWNER
MEMBER

Tetapi hanya gunakan role tersebut jika memang cocok dengan architecture yang sudah ada.

Jangan membuat ADMIN/MODERATOR/EDITOR dan role lain hanya berdasarkan asumsi.

==================================================
FASE 3 — B-031 INVITATION CONTRACT
==================================================

Audit apakah invitation memang sudah ada di roadmap.

Jika iya, implementasikan contract minimum.

Invitation harus memiliki:

- workspace reference,
- invited identity/email/account reference sesuai architecture,
- invitation state,
- secure invitation identifier/token jika diperlukan,
- created time jika model repository menggunakannya,
- expiration hanya jika contract memang sudah mendukung expiry.

JANGAN menambahkan invitation expiry hanya karena terlihat bagus.

Jika invitation expiry belum ada pada contract:

tetap tanpa expiry.

Jangan membuat scheduler.

Jangan membuat cleanup worker.

Jangan membuat background job hanya untuk invitation.

==================================================
FASE 4 — DATABASE / MIGRATION
==================================================

Jika B-031 membutuhkan persistence:

audit migration architecture terlebih dahulu.

Jika membership/invitation schema belum tersedia dan memang merupakan bagian B-031:

implementasikan migration yang sesuai contract.

Requirements:

- foreign key yang benar,
- workspace ownership,
- user/account relation,
- uniqueness constraint yang memang dibutuhkan,
- safe indexing untuk lookup utama.

Jangan membuat migration destruktif.

Jangan mengubah tabel B-071 secara tidak perlu.

Jangan membuat schema hanya agar test PASS.

Jangan menggunakan SQLite sebagai pengganti PostgreSQL jika repository menggunakan PostgreSQL.

==================================================
FASE 5 — B-031 REPOSITORY
==================================================

Implementasikan repository mengikuti pola repository yang sudah digunakan BotSpace.

Repository hanya menangani persistence.

Jangan memasukkan business logic ke repository.

Minimal jika contract membutuhkannya:

Membership:

- get membership,
- list workspace members,
- create membership,
- update role/state,
- remove membership.

Invitation:

- create invitation,
- find invitation,
- list invitations,
- accept invitation,
- revoke invitation.

Tetapi hanya implementasikan operasi yang memang diperlukan roadmap.

Jangan membuat API CRUD berlebihan.

==================================================
FASE 6 — B-031 SERVICE
==================================================

Implementasikan service layer.

Service bertanggung jawab atas:

- workspace authorization,
- membership rules,
- invitation rules,
- ownership protection,
- duplicate membership handling,
- invitation acceptance,
- revoke behavior.

PENTING:

Workspace owner tidak boleh secara tidak sengaja dihapus jika architecture melarangnya.

User dari workspace A tidak boleh mendapatkan membership workspace B tanpa authorization.

Member biasa tidak boleh melakukan owner-only operation.

Gunakan authorization abstraction yang sudah tersedia.

Jangan membuat authorization system kedua.

==================================================
FASE 7 — INVITATION SECURITY
==================================================

Jika invitation menggunakan token:

- gunakan crypto-safe random generation,
- jangan menyimpan raw token jika repository menggunakan digest pattern,
- jangan mencetak token ke log,
- jangan memasukkan token ke error message,
- jangan memasukkan token ke analytics/logging,
- jangan commit token.

Jika invitation token memang harus dikembalikan ke caller karena email service belum ada:

kembalikan hanya sesuai contract.

Jangan membuat email provider.

Jangan mengirim email sungguhan dari repository jika architecture belum menyediakan email service.

==================================================
FASE 8 — B-031 HTTP API
==================================================

Setelah contract/repository/service stabil:

implementasikan HTTP API B-031.

Endpoint harus mengikuti routing conventions repository.

Jangan membuat endpoint berdasarkan asumsi jika pattern repository sudah tersedia.

Kemungkinan operation yang dibutuhkan:

- list workspace members,
- update member role,
- remove member,
- create invitation,
- list invitations,
- revoke invitation,
- accept invitation.

Hanya implementasikan endpoint yang benar-benar diperlukan roadmap.

Setiap endpoint:

1. authenticate user,
2. resolve workspace,
3. authorize operation,
4. validate request,
5. call service,
6. map response,
7. sanitize error.

Jangan mengembalikan:

- password,
- secret,
- internal database details,
- storage credential,
- raw internal errors.

==================================================
FASE 9 — AUTHORIZATION MATRIX
==================================================

Buat authorization matrix berdasarkan architecture yang benar-benar tersedia.

Minimal review:

OWNER:
- melihat members
- mengelola membership
- mengundang member
- revoke invitation
- remove member sesuai policy

MEMBER:
- melihat data yang memang diizinkan
- tidak boleh mengubah membership jika tidak punya permission

Jangan membuat role baru hanya untuk memenuhi matrix.

Jika repository sudah memiliki role/permission model:

gunakan model tersebut.

Tambahkan test untuk:

- owner allowed,
- member denied,
- cross-workspace denied,
- unknown workspace denied,
- unknown member denied,
- duplicate invitation/membership behavior.

==================================================
FASE 10 — TEST B-031
==================================================

Tambahkan test nyata untuk:

### Membership
- create membership,
- list members,
- workspace isolation,
- authorization,
- duplicate membership,
- remove member,
- owner protection,
- role update jika tersedia.

### Invitation
- create invitation,
- invitation lookup,
- accept invitation,
- revoke invitation,
- invalid invitation,
- unauthorized invitation management,
- duplicate invitation handling.

### HTTP
- 401,
- 403,
- 404,
- 400 validation,
- successful response,
- safe error response.

Jangan membuat mock yang tidak menguji behavior sebenarnya.

Jika PostgreSQL integration environment tersedia:

gunakan:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tidak tersedia:

jangan membuat database palsu.

Catat:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

==================================================
FASE 11 — F-031 WORKSPACE SETTINGS UI
==================================================

Setelah B-031 API benar-benar selesai dan typed API client dapat mengaksesnya:

langsung lanjut implementasi F-031.

Jangan berhenti hanya setelah backend B-031.

Gunakan frontend architecture yang SUDAH ADA.

F-031 minimal menyediakan:

### Workspace Settings

- workspace name/info,
- workspace context,
- settings navigation,
- loading state,
- error state.

### Members

- list members,
- member identity,
- role,
- member state jika tersedia,
- loading,
- empty state,
- error state.

### Member Management

Jika API mendukung:

- change role,
- remove member.

Tampilkan confirmation sebelum destructive action.

### Invitations

Jika API mendukung:

- invite member,
- invitation state,
- pending invitations,
- revoke invitation,
- accept invitation jika flow frontend memang berada di workspace UI.

Jangan membuat UI untuk endpoint yang tidak tersedia.

==================================================
FASE 12 — TYPED FRONTEND API
==================================================

Tambahkan typed API client methods untuk B-031.

Jangan menggunakan raw `fetch()` di component.

Gunakan architecture F-012 yang sudah dibuat.

Contoh conceptual flow:

UI
→ feature hook/service
→ typed API client
→ B-031 HTTP API

Bukan:

UI
→ fetch langsung.

Pastikan request/response types berasal dari actual API contract.

Jangan membuat frontend type yang bertentangan dengan backend.

==================================================
FASE 13 — F-031 UX
==================================================

UI harus:

- responsive,
- mobile friendly,
- clean,
- konsisten dengan F-030,
- menggunakan existing UI primitives F-011.

States:

- loading,
- empty,
- error,
- success,
- disabled,
- confirmation.

Jangan membuat design system baru.

Jangan membuat UI terlalu kompleks.

Jangan menggunakan dummy member.

Jika workspace tidak memiliki member selain owner:

tampilkan empty/appropriate state.

==================================================
FASE 14 — SECURITY REVIEW F-031
==================================================

Audit:

- route guard,
- workspace context,
- cross-workspace access,
- role manipulation,
- invitation token handling,
- unsafe rendering,
- error message.

Frontend route guard bukan security boundary.

Backend authorization tetap wajib.

Jangan mempercayai role yang dikirim client.

==================================================
FASE 15 — VALIDATION
==================================================

Setelah B-031 dan F-031 selesai:

jalankan validation yang tersedia:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

Untuk:

`node scripts/check-symlinks.mjs`

JANGAN membuat script baru jika memang tidak tersedia.

Jika unavailable:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

Jika PostgreSQL test membutuhkan environment yang tidak tersedia:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan mengubah test agar terlihat PASS.

==================================================
FASE 16 — FAILURE HANDLING
==================================================

Jika test/build/typecheck/lint gagal:

jangan berhenti.

1. baca error,
2. cari root cause,
3. perbaiki,
4. test ulang,
5. jalankan validation penuh.

Jangan:

- disable lint,
- disable TypeScript strictness,
- delete test,
- fake PASS,
- bypass authorization,
- membuat dummy API.

==================================================
FASE 17 — TYPESCRIPT/PARSER AUDIT
==================================================

Cari:

`<<<<<<<`

`=======`

`>>>>>>>`

Audit juga:

- duplicate imports,
- duplicate exports,
- malformed JSX,
- invalid generics,
- invalid route definitions,
- broken object literals,
- accidental terminal output,
- syntax corruption.

Perbaiki hanya masalah nyata.

==================================================
FASE 18 — DIFF REVIEW
==================================================

Sebelum commit:

`git status`

`git diff --stat`

Review seluruh diff.

Pastikan tidak ada:

- credential,
- secret,
- `.env`,
- temporary files,
- generated junk,
- unrelated refactor,
- perubahan Gorouter,
- perubahan NVIDIA,
- perubahan TokenHarbor,
- perubahan B-071 yang tidak diperlukan.

==================================================
FASE 19 — COMMIT
==================================================

Jika B-031 menghasilkan perubahan backend dan F-031 menghasilkan perubahan frontend:

buat commit yang logis.

Ideal:

1. B-031 membership/invitation backend
2. F-031 workspace settings/members UI

Tetapi jika repository workflow lebih cocok satu commit:

boleh satu commit.

Jangan membuat empty commit.

==================================================
FASE 20 — PUSH
==================================================

Setelah commit:

`git push origin backend-dev-recovery`

Verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

WORKING TREE CLEAN

Jika push gagal:

- jangan force push,
- jangan reset --hard,
- jangan menghapus commit,
- jangan mengubah credential sembarangan.

==================================================
FASE 21 — LANJUTKAN ROADMAP
==================================================

Setelah B-031 + F-031 selesai:

JANGAN berhenti hanya karena dua task ini selesai.

Audit roadmap kembali.

Cari task berikutnya yang:

- dependency sudah tersedia,
- contract sudah tersedia,
- implementation dapat dilakukan sekarang.

Jika task berikutnya dapat dikerjakan dengan aman:

LANJUTKAN OTOMATIS.

Jika task berikutnya membutuhkan dependency yang belum tersedia:

berhenti pada dependency tersebut dan tampilkan alasannya.

Jangan membuat fitur speculative.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan:

## B-031
- contract:
- migration:
- repository:
- service:
- HTTP API:
- authorization:
- tests:
- status:

## F-031
- workspace settings:
- members:
- invitations:
- member management:
- typed API:
- status:

## Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

## PostgreSQL
- status:

## Git
- branch:
- commit:
- local SHA:
- remote SHA:
- push:
- working tree:

## Remaining Deferred

Hanya tampilkan dependency nyata yang belum tersedia.

## Next Roadmap

Tentukan berdasarkan roadmap repository yang sebenarnya.

==================================================
ATURAN TERAKHIR
==================================================

Jangan hanya membuat rencana.

KERJAKAN LANGSUNG.

AUDIT
→ IMPLEMENT B-031
→ TEST
→ FIX
→ BUILD
→ IMPLEMENT F-031
→ TEST
→ FIX
→ BUILD
→ REVIEW
→ COMMIT
→ PUSH
→ VERIFY
→ AUDIT ROADMAP
→ LANJUT JIKA DEPENDENCY SUDAH TERSEDIA.

Jangan meminta saya memilih task berikutnya selama dependency repository sudah jelas.

Kerjakan langsung pada:

`/root/botspace`


```
# Prompt: F-002 → F-070 — Complete Frontend Roadmap End-to-End
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

WORKING DIRECTORY:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR — JANGAN DIULANG
==================================================

Backend foundation yang sudah selesai:

- B-030 Workspace API/Contract SUDAH selesai.
- B-070 Storage Adapter SUDAH selesai.
- B-071 File/Share contract SUDAH selesai.
- B-071 File/Share API SUDAH selesai.
- B-071 production wiring SUDAH selesai.
- SecretResolver/deployment boundary sudah diaudit dan dikerjakan sejauh yang dapat dilakukan.
- Deferred infrastructure sudah diverifikasi sejauh environment memungkinkan.
- Working tree terakhir CLEAN.
- Local SHA dan remote SHA sudah sinkron.
- Branch tetap `backend-dev-recovery`.

JANGAN mengulang:

- B-030
- B-070
- B-071 contract
- B-071 repository
- B-071 service
- B-071 API
- B-071 production wiring
- SecretResolver infrastructure yang sudah selesai
- backend storage implementation yang sudah selesai

Jangan membuat ulang backend hanya karena frontend membutuhkan API.

Gunakan API B-071 yang SUDAH ADA sebagai source of truth.

==================================================
HASIL AUDIT TERAKHIR
==================================================

Repository menunjukkan bahwa task frontend yang valid sekarang adalah:

1. F-002 — approve frontend framework dan styling approach
2. F-010 — build web application shell
3. F-011 — build UI primitives
4. F-012 — replace API client dengan typed API client
5. F-020/F-021 — authentication state dan route guards
6. F-030 — workspace dashboard/context
7. F-070 — implement real File/Share UI terhadap B-071 API

Dependency order tersebut WAJIB dihormati.

Jangan melompat langsung ke F-070 sebelum foundation frontend tersedia.

==================================================
TUJUAN UTAMA
==================================================

Kerjakan seluruh frontend roadmap yang dapat diselesaikan dari repository/environment saat ini:

F-002
→ F-010
→ F-011
→ F-012
→ F-020/F-021
→ F-030
→ F-070

Kerjakan secara end-to-end.

Jangan hanya audit.

Jangan berhenti setelah satu task.

Setiap task yang dependency-nya sudah tersedia harus langsung dikerjakan.

Setelah satu task selesai:

- test,
- typecheck,
- build,
- lint,
- review diff,

kemudian lanjut ke task berikutnya.

Jika ada dependency yang benar-benar tidak tersedia, jangan membuat fake implementation. Tandai deferred dan lanjutkan bagian lain yang masih dapat dikerjakan.

==================================================
FASE 0 — AUDIT FRONTEND SAAT INI
==================================================

Sebelum mengubah file:

1. `cd /root/botspace`
2. `git status`
3. `git branch --show-current`
4. `git log --oneline -10`
5. audit `package.json`.
6. audit lockfile.
7. audit frontend source.
8. audit routing.
9. audit existing UI.
10. audit existing API client.
11. audit auth/session code.
12. audit workspace context.
13. audit CSS/styling system.
14. audit existing component library.
15. audit build configuration.
16. audit TypeScript configuration.
17. audit frontend roadmap/documentation.

Cari framework yang SUDAH digunakan.

Contoh:

- React
- Next.js
- Vite
- Vue
- Svelte
- atau framework lain.

Jangan mengubah framework jika repository sudah memiliki framework yang valid.

Jangan melakukan rewrite frontend hanya demi preferensi pribadi.

Source of truth:

- existing package.json,
- existing source,
- existing build config,
- roadmap,
- API contract.

==================================================
FASE 1 — F-002
FRONTEND FRAMEWORK + STYLING APPROACH
==================================================

Tentukan dan dokumentasikan framework frontend yang memang paling sesuai dengan repository saat ini.

PRINSIP:

1. Jika framework sudah tersedia dan valid:
   - pertahankan.

2. Jika framework belum jelas:
   - audit dependency dan source terlebih dahulu.
   - pilih pendekatan paling minimal yang kompatibel dengan repository.

3. Jangan menambahkan framework kedua.

4. Jangan menambahkan CSS framework baru jika repository sudah memiliki styling system yang cukup.

5. Jangan menambahkan dependency besar tanpa alasan.

6. Styling harus konsisten.

7. Gunakan TypeScript jika repository frontend sudah menggunakan TypeScript.

8. Jangan membuat architecture frontend yang tidak dibutuhkan.

Dokumentasikan keputusan F-002 di dokumentasi frontend yang SUDAH ADA.

Jangan membuat banyak README.

Jika sudah ada architecture documentation:
- update file tersebut.

Jika memang tidak ada dokumentasi yang sesuai:
- gunakan dokumentasi repository yang paling tepat,
- jangan membuat banyak file dokumentasi.

==================================================
FASE 2 — F-010
WEB APPLICATION SHELL
==================================================

Implementasikan application shell.

Minimal foundation:

- application root,
- routing structure,
- global layout,
- header/navigation,
- main content area,
- responsive behavior,
- loading state,
- error boundary/state,
- not-found state jika routing mendukung,
- authentication-aware layout jika architecture sudah siap.

Jangan membuat dashboard palsu yang tidak terhubung ke state nyata.

Gunakan reusable layout.

Pastikan shell dapat menjadi foundation untuk:

- authentication,
- workspace context,
- dashboard,
- File/Share UI.

Jangan mengimplementasikan file management langsung di tahap ini jika dependency F-012/F-030 belum selesai.

==================================================
FASE 3 — F-011
UI PRIMITIVES
==================================================

Buat UI primitives yang memang diperlukan oleh application shell dan dashboard.

Contoh jika diperlukan:

- Button
- Input
- Select
- Dialog/Modal
- Card
- Badge
- Table/List
- Dropdown
- Tabs
- Toast/notification
- Spinner/loading
- Empty state
- Error state
- Confirm dialog

ATURAN:

1. Jangan membuat component yang sama berkali-kali.
2. Gunakan reusable primitives.
3. Jangan membuat design system raksasa.
4. Hanya implementasikan primitives yang memang dibutuhkan.
5. Props harus typed.
6. Accessibility dasar harus diperhatikan.
7. Keyboard interaction untuk interactive elements.
8. Button harus memiliki disabled/loading behavior bila relevan.
9. Form control harus memiliki label/error state bila relevan.
10. Jangan hardcode business logic ke primitive component.

Styling harus konsisten dengan keputusan F-002.

==================================================
FASE 4 — F-012
TYPED API CLIENT
==================================================

Sekarang implementasikan typed API client berdasarkan API BotSpace yang SUDAH ADA.

Audit backend API B-030 dan B-071.

Jangan mengarang endpoint.

Jangan mengarang response.

Jangan mengarang request field.

Gunakan contract/API implementation repository sebagai source of truth.

API client harus typed.

Minimal support API yang memang sudah tersedia:

- authentication/session jika tersedia,
- workspace/context,
- file list,
- upload,
- download,
- create share,
- revoke share,
- public share access jika frontend memang membutuhkan public route.

Gunakan centralized API client.

Jangan membuat fetch logic tersebar di seluruh component.

Contoh architecture yang diinginkan:

UI
 ->
feature hook/service
 ->
typed API client
 ->
HTTP API

Bukan:

UI
 ->
fetch() acak di setiap component.

Pastikan:

- base URL configuration,
- request headers,
- auth handling,
- JSON parsing,
- error mapping,
- HTTP status handling,
- multipart upload,
- binary/download response.

Jangan memasukkan API secret ke frontend.

Jangan hardcode token production.

==================================================
FASE 5 — F-020/F-021
AUTHENTICATION STATE + ROUTE GUARDS
==================================================

Audit authentication system backend yang SUDAH ADA.

Jangan membuat authentication backend baru.

Frontend harus mengikuti authentication mechanism yang repository sudah gunakan.

Implementasikan:

- authentication state,
- current user/account state,
- loading state,
- unauthenticated state,
- authenticated state,
- logout behavior jika endpoint tersedia,
- route guard,
- protected layout.

Pastikan route protection terjadi pada frontend UX level.

Tetapi JANGAN menganggap frontend route guard sebagai security boundary.

Backend authorization tetap menjadi source of truth.

Jika user belum login:

- jangan menampilkan protected dashboard sebagai authenticated.

Jika session sedang diperiksa:

- tampilkan loading state.

Jika session expired:

- clear auth state,
- arahkan ke login sesuai routing architecture.

Jangan menyimpan credential sensitif secara tidak aman.

Jangan menyimpan password.

Jangan menaruh API secret di localStorage.

Gunakan mekanisme session/token yang memang sesuai backend.

==================================================
FASE 6 — WORKSPACE CONTEXT
==================================================

Sebelum F-030, implementasikan workspace context berdasarkan B-030.

Pastikan frontend memiliki satu source of truth untuk current workspace.

Context/state harus mendukung:

- current workspace,
- workspace list jika API tersedia,
- switching workspace,
- loading,
- error,
- no workspace state.

Workspace context harus digunakan oleh feature yang workspace-scoped.

Jangan membuat workspace ID global hardcoded.

Jangan menggunakan workspace milik user lain.

Jangan mencampurkan workspace ID dengan BotInstallation process state.

==================================================
FASE 7 — F-030
WORKSPACE DASHBOARD
==================================================

Implementasikan dashboard workspace menggunakan foundation yang sudah dibuat.

Dashboard harus menggunakan data API nyata jika endpoint tersedia.

Minimal:

- current workspace,
- workspace information,
- navigation,
- relevant summary,
- file/share area entry point,
- loading state,
- error state,
- empty state.

Jangan membuat statistik palsu.

Jangan menampilkan angka dummy.

Jika API belum menyediakan metric tertentu:

- jangan mengarang metric,
- tampilkan hanya data yang memang tersedia.

Dashboard harus responsive.

Prioritaskan mobile usability tetapi tetap baik di desktop.

==================================================
FASE 8 — F-070
REAL FILE/SHARE UI
==================================================

Sekarang setelah:

F-002
F-010
F-011
F-012
F-020/F-021
F-030

selesai, implementasikan F-070 menggunakan API B-071 yang SUDAH ADA.

JANGAN membuat fake API.

JANGAN membuat mock data sebagai production behavior.

UI File/Share harus menggunakan backend nyata.

Minimal feature:

### File list

Tampilkan:

- file name,
- size jika tersedia,
- metadata yang memang tersedia,
- created/uploaded time jika tersedia,
- share status jika tersedia,
- actions.

State:

- loading,
- empty,
- error,
- success.

### Upload

Implementasikan real multipart upload.

Support:

- file selection,
- upload progress jika architecture mendukung,
- disabled state saat upload,
- success,
- failure,
- retry.

Jangan membuat arbitrary file limit di frontend jika backend contract belum menetapkannya.

Frontend validation boleh mengikuti backend policy jika memang sudah ada.

Jangan membuat policy baru.

### Download

Gunakan endpoint download yang nyata.

Jangan mengekspos internal object storage path/key.

### Create Share

UI harus:

- create share,
- menerima response API,
- menampilkan share link,
- menyediakan copy action.

Jangan membuat share URL sendiri jika backend sudah menghasilkan URL.

### Revoke Share

Gunakan API revoke nyata.

Setelah revoke:

- update UI state,
- jangan hanya menghapus item secara visual jika backend gagal.

Jika revoke gagal:
- tampilkan error,
- jangan menganggap revoke berhasil.

### Public Share

Jika roadmap frontend memang menyediakan public-share route:

implementasikan route berdasarkan API public share yang sudah ada.

Public share UI:

- valid share,
- revoked/invalid state,
- download/access behavior,
- error state.

Jangan implementasikan expiry UI karena backend contract/schema saat ini belum mendukung expiry.

==================================================
FASE 9 — ERROR HANDLING
==================================================

Buat error handling frontend yang konsisten.

Mapping minimal:

- 400 → invalid request
- 401 → authentication required/session expired
- 403 → access denied
- 404 → resource not found
- 409 → conflict jika API menggunakannya
- 413 → payload too large jika backend menggunakannya
- 429 → rate limited jika backend menggunakannya
- 5xx → server error

Jangan menampilkan:

- stack trace,
- database details,
- storage credential,
- secret,
- internal object path,
- internal infrastructure details.

Gunakan safe user-facing error message.

==================================================
FASE 10 — RESPONSIVE + UX
==================================================

Audit seluruh frontend yang dibuat.

Pastikan:

- mobile usable,
- desktop usable,
- buttons tidak terlalu kecil,
- form mudah digunakan,
- loading state jelas,
- error state jelas,
- empty state jelas,
- dialogs dapat ditutup dengan benar,
- keyboard accessibility dasar,
- focus state,
- disabled state,
- upload interaction tidak membingungkan.

Jangan membuat UI terlalu kompleks.

Prioritaskan:

clean,
simple,
responsive,
consistent.

==================================================
FASE 11 — SECURITY REVIEW FRONTEND
==================================================

Audit:

- token handling,
- auth state,
- API base URL,
- XSS risk,
- unsafe HTML rendering,
- share URL handling,
- file name rendering,
- error rendering,
- workspace switching.

Jangan menggunakan:

`dangerouslySetInnerHTML`

kecuali benar-benar diperlukan dan input telah disanitasi.

File name dan metadata harus diperlakukan sebagai untrusted data.

Jangan menaruh:

- API key,
- secret,
- database credential,
- storage credential,

di frontend source.

==================================================
FASE 12 — TESTING
==================================================

Tambahkan test sesuai framework yang repository gunakan.

Prioritas:

### F-010
- shell render,
- navigation,
- loading/error states.

### F-011
- primitive behavior,
- button disabled,
- form behavior,
- accessibility dasar.

### F-012
- typed API behavior,
- error mapping,
- multipart request,
- binary response.

### F-020/F-021
- authenticated state,
- unauthenticated state,
- loading state,
- route guard.

### Workspace
- workspace selection,
- switching,
- isolation behavior.

### F-030
- dashboard loading,
- dashboard success,
- empty/error.

### F-070
- file list,
- upload,
- upload error,
- download,
- create share,
- copy link,
- revoke,
- revoked state,
- unauthorized state.

Jangan membuat fake tests yang hanya memastikan component muncul.

Test behavior yang penting.

==================================================
FASE 13 — VALIDATION
==================================================

Setelah seluruh frontend selesai:

jalankan command yang memang tersedia di repository.

Minimal:

`pnpm test`

`pnpm build`

`pnpm typecheck`

`pnpm lint`

`pnpm format:check`

`node scripts/check-imports.mjs`

`node scripts/check-ownership.mjs`

`node scripts/check-doc-links.mjs`

`git diff --check`

Jika repository memang memiliki command frontend tambahan:

jalankan juga.

Untuk:

`node scripts/check-symlinks.mjs`

JANGAN membuat script baru jika memang tidak tersedia.

Jika tidak ada:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

Jangan mengubah validation agar terlihat PASS.

==================================================
FASE 14 — FIX FAILURE
==================================================

Jika build/test/typecheck/lint gagal:

Jangan berhenti.

Lakukan:

1. baca error lengkap,
2. cari root cause,
3. perbaiki source,
4. jalankan test terkait,
5. jalankan validation penuh kembali.

Jangan:

- menghapus test,
- menurunkan strictness TypeScript hanya agar PASS,
- menonaktifkan lint,
- menonaktifkan build check,
- membuat mock production,
- mengubah backend contract secara sembarangan.

Jika failure berasal dari environment:

- diagnosis,
- jangan membuat fake PASS,
- dokumentasikan sebagai environment limitation.

==================================================
FASE 15 — TYPESCRIPT / PARSER AUDIT
==================================================

Karena repository sebelumnya pernah mengalami TypeScript parser error, lakukan audit khusus:

Cari:

- merge conflict markers,
- malformed TypeScript,
- duplicate imports,
- duplicate exports,
- broken generics,
- invalid JSX,
- malformed object literals,
- accidental pasted terminal output,
- illegal characters,
- broken route definitions.

Cari:

`<<<<<<<`

`=======`

`>>>>>>>`

Hanya hapus jika benar-benar leftover merge conflict.

Jangan mengubah dokumentasi/test fixture yang memang menggunakan string tersebut secara valid.

==================================================
FASE 16 — NO UNRELATED CHANGES
==================================================

Sebelum commit:

Review seluruh diff.

Pastikan TIDAK ADA:

- perubahan Gorouter.app,
- perubahan NVIDIA provider yang tidak diperlukan,
- perubahan TokenHarbor yang tidak diperlukan,
- credential,
- API key,
- password,
- secret,
- `.env`,
- temporary files,
- generated junk,
- unrelated backend refactor,
- schema migration yang tidak diperlukan.

Jika ada:
hapus/revert perubahan tersebut.

==================================================
FASE 17 — DOCUMENTATION
==================================================

Update dokumentasi yang SUDAH ADA jika diperlukan.

Dokumentasikan:

- frontend framework decision,
- application shell,
- UI architecture,
- typed API client,
- authentication flow,
- workspace context,
- dashboard,
- File/Share UI,
- development/run instructions.

Jangan membuat banyak README.

Gunakan dokumentasi utama repository yang sudah ada.

==================================================
FASE 18 — COMMIT PER BATCH
==================================================

Karena pekerjaan cukup besar, gunakan commit yang logis.

Jangan membuat empty commit.

Idealnya:

1. F-002/F-010/F-011
2. F-012/F-020/F-021
3. F-030
4. F-070

Tetapi jika repository lebih cocok dengan satu commit frontend besar, gunakan satu commit.

Yang paling penting:

- setiap commit harus valid,
- test harus dijalankan,
- jangan commit pekerjaan rusak,
- jangan commit secret.

==================================================
FASE 19 — PUSH
==================================================

Setelah commit valid:

`git push origin backend-dev-recovery`

Setelah push:

verifikasi:

`git rev-parse HEAD`

`git rev-parse origin/backend-dev-recovery`

`git status`

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

working tree clean.

Jika push gagal:

- jangan force push,
- jangan reset --hard,
- jangan menghapus commit,
- jangan mengubah credential sembarangan.

Diagnosis error dan tampilkan dengan jelas.

==================================================
FASE 20 — LANJUTKAN SAMPAI BATAS DEPENDENCY
==================================================

Setelah F-070 selesai:

audit roadmap lagi.

Jika masih ada frontend task berikutnya yang dependency-nya sudah tersedia:

LANJUTKAN.

Jangan berhenti hanya karena F-070 selesai.

Tetapi jangan membuat fitur yang belum ada di roadmap.

Jika semua frontend task yang dapat dikerjakan sudah selesai:

berhenti dengan aman.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan:

## F-002
- framework:
- styling:
- status:

## F-010
- shell:
- routing:
- responsive:
- status:

## F-011
- primitives:
- status:

## F-012
- typed API client:
- endpoints integrated:
- status:

## F-020/F-021
- authentication state:
- route guards:
- status:

## Workspace
- workspace context:
- switching:
- isolation:
- status:

## F-030
- dashboard:
- status:

## F-070
- file list:
- upload:
- download:
- create share:
- revoke share:
- public share:
- status:

## Testing
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

## Git
- branch:
- commits:
- latest SHA:
- remote SHA:
- push:
- working tree:

## Remaining Deferred

HANYA tampilkan dependency yang benar-benar belum dapat dikerjakan karena:

- external infrastructure,
- missing environment,
- approved architecture decision,
- backend contract,
- atau dependency nyata lainnya.

## Next Roadmap

Audit repository setelah frontend selesai dan tentukan task berikutnya berdasarkan roadmap NYATA.

Jangan membuat roadmap fiktif.

==================================================
ATURAN KERAS
==================================================

1. Jangan mengulang B-030.
2. Jangan mengulang B-070.
3. Jangan mengulang B-071 backend.
4. Jangan membuat backend API duplikat.
5. Jangan membuat fake API.
6. Jangan membuat fake production authentication.
7. Jangan hardcode secret.
8. Jangan menyimpan password.
9. Jangan menaruh API secret di frontend.
10. Jangan membuat expiry UI sebelum backend contract mendukungnya.
11. Jangan membuat rate-limit UI/policy baru tanpa backend contract.
12. Jangan menyentuh Gorouter.app.
13. Jangan membuat Telegram polling/webhook runtime.
14. Jangan mengubah `BotInstallation.status`.
15. Jangan membuat framework kedua.
16. Jangan melakukan rewrite besar jika tidak diperlukan.
17. Jangan menonaktifkan test/typecheck/lint untuk membuat PASS.
18. Jangan membuat dummy validation.
19. Jangan membuat empty commit.
20. Jangan force push.
21. Jangan berhenti hanya karena satu dependency/environment tidak tersedia.
22. Kerjakan semua task yang dependency-nya sudah tersedia.
23. Gunakan repository sebagai source of truth.
24. Kerjakan langsung di `/root/botspace`.
25. Setelah satu task selesai, lanjut otomatis ke task berikutnya dalam dependency order.
26. Jangan meminta saya memilih task berikutnya selama roadmap repository sudah jelas.

KERJAKAN SEKARANG.
AUDIT -> IMPLEMENT -> TEST -> FIX -> BUILD -> COMMIT -> PUSH -> VERIFY -> LANJUT.
JANGAN HANYA MEMBERIKAN RENCANA.

```
# B-072 — Complete Remaining Roadmap End-to-End
```

# Prompt: B-072 — Complete Remaining BotSpace Roadmap End-to-End

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

KERJAKAN LANGSUNG DI:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR YANG WAJIB DIHORMATI
==================================================

Berdasarkan pekerjaan sebelumnya:

- B-030 Workspace API/Contract SUDAH SELESAI.
- B-070 Storage Adapter SUDAH SELESAI.
- B-071 File/Share Contract SUDAH SELESAI.
- B-071 File/Share API SUDAH SELESAI.
- Production wiring B-071 SUDAH SELESAI.
- SecretResolver application boundary SUDAH ADA.
- Beberapa infrastructure verification SUDAH dilakukan.
- Working tree terakhir CLEAN.
- Branch `backend-dev-recovery`.
- Jangan mengulang pekerjaan yang sudah selesai.
- Jangan membuat ulang contract yang sudah ada.
- Jangan membuat schema/architecture baru hanya berdasarkan asumsi.
- Jangan mengubah behavior yang sudah benar hanya untuk merapikan kode.
- Jangan menyentuh Gorouter.app.
- NVIDIA dan TokenHarbor jangan disentuh kecuali benar-benar terdampak langsung oleh perubahan yang sedang dikerjakan.
- Jangan membuat Telegram polling/webhook runtime jika belum menjadi bagian roadmap yang sedang dikerjakan.
- Jangan mengubah `BotInstallation.status` menjadi process/runtime state.

HASIL TERAKHIR YANG TERLIHAT:

Deferred infrastructure masih mencakup kemungkinan:

1. Pemilihan/provider Secret Manager.
2. Deployment-owned SecretResolver adapter.
3. Workload identity/bootstrap authentication.
4. PostgreSQL integration test membutuhkan:
   `PERSISTENCE_TEST_DATABASE_URL`
5. MinIO/S3 smoke test membutuhkan endpoint dan test credentials.
6. Public-share rate limiting masih menunggu approved boundary.
7. Public-share audit event masih menunggu approved boundary.
8. Share expiry masih menunggu approved contract/schema/migration.
9. `scripts/check-symlinks.mjs` tidak tersedia.
10. Setelah B-071 selesai, roadmap berikutnya mengarah ke file list/upload/share UI/API integration dan task berikutnya yang memang tersedia di repository.

PENTING:

Jangan hanya membaca daftar deferred lalu berhenti.

Tugas utama kamu adalah:
AUDIT -> TENTUKAN DEPENDENCY -> KERJAKAN SEMUA YANG BISA DIKERJAKAN -> TEST -> FIX -> VALIDATE -> COMMIT -> PUSH -> LANJUT KE TASK BERIKUTNYA YANG VALID.

Jangan meminta saya memilih langkah berikutnya jika repository sendiri sudah memberikan dependency/roadmap yang jelas.

==================================================
FASE 0 — AUDIT KONDISI NYATA
==================================================

Sebelum mengubah apa pun:

1. `cd /root/botspace`
2. `git status`
3. `git branch --show-current`
4. `git log --oneline -10`
5. `git remote -v`
6. audit struktur repository.
7. baca roadmap/documentation yang relevan.
8. cari TODO/FIXME/deferred roadmap yang benar-benar masih aktif.
9. audit B-030, B-070, B-071 dan pastikan tidak mengulang pekerjaan yang sudah selesai.

Gunakan kode repository sebagai source of truth.

Jangan menganggap laporan lama selalu benar jika kode sekarang sudah berubah.

Jika ada perbedaan antara dokumentasi dan implementation:

- prioritaskan implementation + contract aktual,
- jangan melakukan rollback,
- dokumentasikan perbedaannya.

==================================================
FASE 1 — SECRETRESOLVER / DEPLOYMENT INFRASTRUCTURE
==================================================

Audit:

- SecretResolver
- production configuration
- composition root
- deployment configuration
- storage credential loading
- object storage adapter
- environment handling
- deployment documentation.

Tujuan:

Menyelesaikan SecretResolver sejauh mungkin tanpa mengarang infrastructure.

ATURAN:

1. Jangan membuat interface SecretResolver kedua.
2. Gunakan interface yang sudah ada.
3. Application/business layer hanya bergantung pada SecretResolver abstraction.
4. Provider-specific detail harus berada di deployment/infrastructure boundary.
5. Jangan hardcode secret.
6. Jangan hardcode password.
7. Jangan hardcode API key.
8. Jangan hardcode access key.
9. Jangan hardcode token.
10. Jangan mencetak secret ke log.
11. Jangan memasukkan secret ke HTTP response.
12. Jangan memasukkan secret ke error message.
13. Jangan menyimpan secret ke repository.

Jika repository sudah menetapkan provider Secret Manager:

- implementasikan adapter konkret untuk provider tersebut.

Jika repository BELUM menetapkan provider:

JANGAN memilih vendor secara sembarangan.

Sebagai gantinya:

- pertahankan provider-neutral boundary,
- gunakan configuration/reference mechanism yang memang sudah tersedia,
- implementasikan deployment adapter hanya sejauh contract benar-benar mendukungnya,
- dokumentasikan dependency yang membutuhkan keputusan deployment owner.

Jika environment VPS saat ini hanya menyediakan environment variables dan tidak ada managed Secret Manager:

- jangan membuat managed service palsu,
- jangan memasukkan fake production credentials,
- jangan menganggap fake resolver sebagai production implementation.

Namun tetap pastikan:

- startup configuration validation benar,
- production dependency boundary benar,
- test resolver bisa diinjeksi,
- storage adapter tidak membaca secret secara langsung dari business layer.

Jika ada implementation yang aman dan valid, kerjakan.

==================================================
FASE 2 — WORKLOAD IDENTITY / BOOTSTRAP
==================================================

Audit apakah repository/deployment contract sudah memiliki:

- workload identity,
- bootstrap authentication,
- secret manager reference,
- deployment identity,
- credential rotation/revocation.

Jika contract sudah ada:

- implementasikan integration sesuai contract.

Jika belum:

- jangan membuat protocol baru,
- jangan mengarang provider-specific authentication,
- jangan menambahkan credential system baru.

Pastikan production code tidak membutuhkan hardcoded credentials.

Jika dependency deployment belum tersedia:

tandai:

`DEFERRED — deployment-owned identity/provider configuration required`

Tetapi lanjutkan ke fase berikutnya.

==================================================
FASE 3 — POSTGRESQL INTEGRATION VERIFICATION
==================================================

Periksa:

`PERSISTENCE_TEST_DATABASE_URL`

Jika tersedia:

jalankan integration test PostgreSQL yang memang tersedia.

Verifikasi:

- migration,
- file metadata,
- workspace ownership,
- workspace isolation,
- share-link persistence,
- create share,
- revoke share,
- repository read/write,
- transaction behavior,
- cleanup/rollback behavior.

Jika test gagal:

1. tentukan apakah failure berasal dari implementation BotSpace atau environment.
2. jika implementation BotSpace salah, FIX.
3. jalankan ulang test.
4. jangan mengubah test agar PASS.
5. jangan mengganti PostgreSQL dengan SQLite.
6. jangan membuat fake PostgreSQL.

Jangan menjalankan migration destruktif pada database yang bukan database test.

Jika variable tidak tersedia:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan membuat variable palsu.

==================================================
FASE 4 — MINIO / S3 VERIFICATION
==================================================

Audit ObjectStoragePort dan adapter B-070.

Cari environment MinIO/S3-compatible yang benar-benar tersedia.

Jika tersedia:

gunakan credential TEST/SYNTHETIC ONLY.

Verifikasi end-to-end:

1. upload object,
2. object exists,
3. read/download,
4. metadata/content,
5. delete,
6. verify deletion.

Semua object test harus dibersihkan.

Jangan:

- menggunakan production credential,
- menyimpan credential ke source,
- commit credential,
- mencetak credential,
- mengubah production secret hanya untuk smoke test.

Jika environment tidak tersedia:

`SKIPPED — MinIO/S3 test environment unavailable`

Jangan install infrastructure permanen hanya untuk membuat test PASS.

==================================================
FASE 5 — PUBLIC SHARE SECURITY
==================================================

Audit public share implementation.

Pastikan:

- revoked share tidak dapat digunakan,
- invalid token ditolak,
- workspace isolation tetap aman,
- object storage internal key tidak bocor,
- raw secret tidak masuk log,
- token handling mengikuti contract,
- unauthorized access ditolak,
- path traversal ditolak,
- unsafe object identifier ditolak.

Jangan mengubah contract yang sudah benar.

==================================================
FASE 6 — PUBLIC SHARE RATE LIMITING
==================================================

Cari apakah repository sekarang sudah memiliki approved:

- rate-limit contract,
- middleware,
- policy,
- request context,
- public-share boundary.

Jika SUDAH ada:

implementasikan rate limiting berdasarkan contract tersebut.

Tambahkan test:

- request allowed,
- request limited,
- reset/window behavior jika memang contract mendukungnya,
- private workspace file operations tidak ikut terkena public-share limit.

Jika BELUM ada:

JANGAN membuat rate limiter speculative.

Jangan:

- memilih angka limit sendiri,
- membuat database table baru,
- menambahkan Redis hanya untuk ini,
- membuat middleware architecture baru tanpa contract.

Tetapkan:

`DEFERRED — approved public-share rate-limit boundary required`

Lalu lanjutkan.

==================================================
FASE 7 — PUBLIC SHARE AUDIT EVENT
==================================================

Audit apakah audit event boundary sudah tersedia.

Jika tersedia:

implementasikan event sesuai contract.

Minimal event hanya jika memang contract mendukung:

- public share accessed,
- access denied/revoked,
- share created/revoked.

Jangan simpan:

- raw share token,
- secret,
- password,
- storage credential.

Gunakan digest/identifier sesuai contract.

Jika boundary belum tersedia:

`DEFERRED — approved audit event boundary required`

Jangan membuat audit architecture baru secara speculative.

==================================================
FASE 8 — SHARE EXPIRY
==================================================

JANGAN menambahkan expiry jika contract/schema belum mendukung.

Jangan membuat:

- expiresAt,
- expiry column,
- expiry migration,
- expiry scheduler,
- expiry token,
- cleanup worker.

Hanya implementasikan expiry jika repository SEKARANG sudah memiliki approved:

- contract,
- schema,
- migration,
- service behavior,
- test expectation.

Jika belum:

`DEFERRED — contract/schema/migration approval required`

==================================================
FASE 9 — FILE/SHARE API AUDIT
==================================================

Audit B-071 end-to-end.

Pastikan endpoint/route yang memang sudah ada bekerja dengan:

- workspace authorization,
- upload,
- download,
- metadata,
- create share,
- revoke share,
- public share,
- error mapping,
- object storage.

Pastikan layer tetap terpisah:

HTTP route
    ->
service
    ->
repository + ObjectStoragePort

Jangan memindahkan business logic ke route.

Jangan membuat storage implementation di API layer.

==================================================
FASE 10 — FILE LIST / UPLOAD / SHARE UI
==================================================

Sekarang lihat roadmap repository untuk task setelah B-071.

Jika memang ada task seperti:

- F-070 file list,
- upload UI,
- share UI,
- download UI,
- file management UI,

maka lanjutkan task tersebut secara end-to-end.

Jangan membuat UI berdasarkan asumsi.

Audit:

- existing frontend,
- existing API client,
- existing routing,
- existing authentication,
- existing workspace context,
- existing design system,
- existing file/share endpoint.

Implementasikan hanya feature yang memang ada di roadmap.

Untuk File UI minimal jika contract sudah mendukung:

1. File list.
2. Upload.
3. Download.
4. Create share.
5. Revoke share.
6. Copy share link.
7. Loading state.
8. Empty state.
9. Error state.
10. Permission denied state.
11. Workspace isolation.

Jangan membuat fake API.

UI harus menggunakan API nyata.

Jika backend endpoint belum cukup:

- implementasikan dependency backend yang memang diperlukan,
- jangan membuat endpoint duplikat.

==================================================
FASE 11 — API + UI INTEGRATION
==================================================

Pastikan frontend benar-benar terhubung ke backend.

Verifikasi:

- authentication/session,
- workspace ID,
- API base URL,
- upload request,
- multipart handling,
- response parsing,
- download behavior,
- share creation,
- share revoke,
- error handling.

Jangan hardcode production API credentials.

Jangan menaruh secret di frontend.

Jika API membutuhkan authorization header:

gunakan mekanisme auth yang sudah ada.

==================================================
FASE 12 — SECURITY HARDENING
==================================================

Lakukan targeted security audit terhadap seluruh pekerjaan yang disentuh.

Periksa:

### Authentication
- unauthorized request ditolak.

### Authorization
- workspace A tidak dapat mengakses workspace B.

### File
- path traversal ditolak,
- invalid object identifier ditolak,
- unsafe upload input ditolak.

### Storage
- internal storage key tidak bocor,
- storage credentials tidak bocor.

### Share
- token aman,
- revoked share ditolak,
- invalid token ditolak,
- public share hanya mengakses object yang benar.

### Error
- tidak ada stack trace sensitif di production response,
- tidak ada database credential,
- tidak ada storage credential,
- tidak ada raw secret.

### Logs
- jangan log secret,
- jangan log password,
- jangan log storage credential,
- jangan log raw share token.

==================================================
FASE 13 — TESTING LENGKAP
==================================================

Jalankan semua validation yang benar-benar tersedia.

Minimal:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Lalu:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jika repository memiliki script tambahan yang memang digunakan oleh CI:

jalankan juga.

Untuk:

node scripts/check-symlinks.mjs

JIKA FILE TIDAK ADA:

JANGAN membuat file dummy.

Catat:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

Jika ada integration test PostgreSQL:

jalankan bila environment tersedia.

Jika tidak:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jika ada MinIO/S3 smoke test:

jalankan bila environment tersedia.

Jika tidak:

`SKIPPED — MinIO/S3 test environment unavailable`

Jangan menyamarkan SKIPPED menjadi PASS.

==================================================
FASE 14 — FIX SEMUA FAILURE YANG BERASAL DARI KODE
==================================================

Jika test/build/typecheck/lint gagal:

JANGAN langsung berhenti.

Lakukan:

1. baca error lengkap,
2. cari file penyebab,
3. perbaiki root cause,
4. jalankan test terkait,
5. jalankan validation lengkap kembali.

Jika failure berasal dari:

- environment,
- missing credential,
- missing service,
- unavailable database,
- unavailable MinIO,
- deployment configuration,

jangan membuat workaround palsu.

Catat sebagai deferred/unavailable dan lanjutkan task lain yang bisa dikerjakan.

==================================================
FASE 15 — TYPESCRIPT / PARSER SAFETY
==================================================

Khusus karena repository sebelumnya pernah mengalami parser/build error:

Audit source untuk:

- malformed TypeScript,
- broken generic,
- incomplete declaration,
- merge conflict marker,
- accidental pasted text,
- invalid character,
- broken import,
- duplicate export,
- malformed object literal,
- malformed function declaration.

Cari:

<<<<<<<
=======
>>>>>>>

dan hapus hanya jika memang merupakan leftover conflict marker yang tidak valid.

Jangan mengubah source code valid hanya karena string tersebut muncul di dokumentasi/test fixture.

==================================================
FASE 16 — NO UNRELATED CHANGES
==================================================

Sebelum commit review seluruh diff.

Pastikan TIDAK ADA:

- perubahan Gorouter.app,
- perubahan NVIDIA provider yang tidak diperlukan,
- perubahan TokenHarbor yang tidak diperlukan,
- credential,
- `.env`,
- secret,
- password,
- API key,
- temporary files,
- generated junk,
- debug logs,
- unrelated refactor,
- dependency baru yang tidak diperlukan.

Jika ada file tidak relevan:

hapus perubahan tersebut dari working tree.

==================================================
FASE 17 — DOCUMENTATION / ROADMAP UPDATE
==================================================

Jika repository menggunakan README/roadmap sebagai tracking:

Update dokumentasi YANG SUDAH ADA.

Jangan membuat banyak README baru.

Dokumentasikan:

- task yang selesai,
- validation,
- skipped environment checks,
- remaining deferred,
- next roadmap.

Jangan mengklaim test PASS jika sebenarnya SKIPPED.

Jangan mengklaim infrastructure selesai jika hanya boundary yang selesai.

==================================================
FASE 18 — COMMIT
==================================================

Setelah semua implementation yang valid selesai dan validation selesai:

jalankan:

git status
git diff --stat
git diff --check

Review seluruh perubahan.

Jika ada perubahan valid:

buat SATU commit untuk batch pekerjaan ini.

Gunakan commit message yang mencerminkan perubahan AKTUAL.

Contoh:

`feat: complete remaining botspace file infrastructure`

atau message yang lebih tepat berdasarkan hasil nyata.

JANGAN membuat empty commit.

Jika tidak ada perubahan kode:

jangan membuat commit kosong.

==================================================
FASE 19 — PUSH OTOMATIS
==================================================

Jika commit dibuat:

langsung jalankan:

git push origin backend-dev-recovery

Setelah push:

verifikasi:

git rev-parse HEAD
git rev-parse origin/backend-dev-recovery
git status

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

working tree clean.

Jika push gagal:

- jangan hapus commit,
- jangan reset --hard,
- jangan force push,
- jangan mengubah credential secara sembarangan.

Diagnosis error push dan laporkan.

==================================================
FASE 20 — LANJUTKAN ROADMAP
==================================================

Setelah satu batch selesai:

JANGAN berhenti hanya karena task tersebut selesai.

Audit roadmap repository lagi.

Jika ada task berikutnya yang:

- contract-nya sudah tersedia,
- dependency-nya sudah selesai,
- dapat dikerjakan dari environment saat ini,

lanjutkan task tersebut.

Tetap gunakan prinsip:

AUDIT -> IMPLEMENT -> TEST -> FIX -> VALIDATE -> COMMIT -> PUSH.

Jangan mengerjakan task yang masih membutuhkan keputusan architecture/deployment yang belum tersedia.

Jika semua task yang dapat dikerjakan sudah selesai:

berhenti secara aman dan tampilkan remaining deferred.

==================================================
ATURAN KERAS
==================================================

1. Jangan mengulang B-030.
2. Jangan mengulang B-070.
3. Jangan mengulang B-071 yang sudah selesai.
4. Jangan membuat contract kedua.
5. Jangan membuat schema speculative.
6. Jangan membuat credential palsu.
7. Jangan hardcode secret.
8. Jangan log secret.
9. Jangan menyentuh Gorouter.app.
10. Jangan membuat Telegram runtime jika belum menjadi roadmap task.
11. Jangan mengubah BotInstallation.status menjadi process state.
12. Jangan menambahkan share expiry tanpa contract/schema.
13. Jangan membuat rate limiter tanpa approved boundary.
14. Jangan membuat audit system tanpa approved boundary.
15. Jangan mengganti PostgreSQL dengan SQLite.
16. Jangan membuat fake integration test.
17. Jangan membuat dummy script hanya agar validation PASS.
18. Jangan mengubah test supaya PASS.
19. Jangan membuat empty commit.
20. Jangan force push.
21. Jangan berhenti hanya karena satu environment dependency unavailable.
22. Kerjakan semua bagian lain yang memang dapat dikerjakan.
23. Jangan meminta saya memilih task berikutnya jika roadmap repository sudah jelas.
24. Gunakan implementation repository sebagai source of truth.
25. Commit dan push setiap batch valid sesuai aturan di atas.
26. Pastikan branch tetap:
    `backend-dev-recovery`

==================================================
OUTPUT AKHIR
==================================================

Setelah seluruh pekerjaan yang dapat dilakukan selesai, tampilkan laporan:

## Completed
- task yang selesai
- feature yang selesai
- backend/API
- UI jika ada

## SecretResolver
- boundary:
- provider:
- deployment adapter:
- startup verification:
- status:

## PostgreSQL
- integration:
- migration:
- test:
- status:

## MinIO/S3
- upload:
- download:
- cleanup:
- status:

## File/Share
- upload:
- download:
- create share:
- revoke:
- public access:
- authorization:
- workspace isolation:

## UI
- file list:
- upload:
- download:
- share:
- revoke:
- error/loading state:

## Security
- authentication:
- authorization:
- path traversal:
- token handling:
- secret handling:

## Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:
- symlink:

## Git
- branch:
- commit SHA:
- push:
- local SHA:
- remote SHA:
- working tree:

## Remaining Deferred
HANYA tampilkan item yang benar-benar masih membutuhkan:

- deployment infrastructure,
- provider decision,
- environment,
- external service,
- approved contract,
- atau migration/architecture approval.

## Next Roadmap
Tentukan task berikutnya berdasarkan roadmap nyata repository.

Jangan membuat roadmap fiktif.

Jika semua task yang dapat dikerjakan sudah selesai, nyatakan:

`No further repository task can be safely implemented without the remaining external dependency/approval.`

KERJAKAN LANGSUNG.
JANGAN HANYA MEMBERIKAN RENCANA.
JANGAN BERHENTI SETELAH AUDIT.
IMPLEMENTASIKAN SEMUA YANG VALID SAMPAI SELESAI.
TEST.
FIX.
COMMIT.
PUSH.
VERIFIKASI.
LALU LANJUT KE ROADMAP BERIKUTNYA YANG VALID.

```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
