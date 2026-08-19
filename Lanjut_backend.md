

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
