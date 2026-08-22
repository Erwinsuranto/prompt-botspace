

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
# Prompt: B-058 — Credential Provisioning Contract Review
```

Lanjutkan project BotSpace dari kondisi repository saat ini.

KONDISI TERAKHIR

- B-030 Workspace API/Contract SUDAH selesai.
- B-070 Storage Adapter SUDAH selesai.
- B-071 File/Share contract SUDAH selesai.
- B-071 File/Share API SUDAH selesai.
- Production wiring B-071 SUDAH selesai.
- B-054 Module Management UI SUDAH selesai.
- B-055 Bot Installation Listing SUDAH selesai.
- B-056 Bot Installation Lifecycle UI SUDAH selesai.
- B-057 Managed Secret Reference Flow SUDAH selesai.
- Working tree terakhir CLEAN.
- Branch: backend-dev-recovery.

NEXT TASK:
B-058 — Bot Credential Provisioning Contract
ADR-011 §4 resolution

JANGAN langsung membuat implementation besar.

Tujuan tahap ini adalah menyelesaikan keputusan contract/architecture untuk provisioning credential bot sebelum implementation B-058.

MASALAH YANG DITEMUKAN

Flow create-bot sebelumnya meminta operator memberikan `secret_ref`.

Itu bukan UX yang benar.

Operator seharusnya memberikan credential/bot token.

Sistem kemudian:
1. menerima credential,
2. melakukan provisioning melalui secret-handling boundary yang benar,
3. menghasilkan/mendapatkan internal secret reference,
4. menyimpan reference tersebut pada installation,
5. tidak mengekspos raw credential.

TUGAS

1. Audit ADR-011 §4 secara langsung di repository.

2. Cari seluruh implementation dan contract yang berkaitan dengan:
   - BotInstallation create flow,
   - createBot,
   - connection-service.ts,
   - SecretResolver,
   - secret provisioning,
   - secret_ref,
   - credential handling,
   - connection creation,
   - API DTO,
   - web/client create-bot flow.

3. Jangan membuat SecretResolver interface baru.

4. Jangan membuat secret manager baru.

5. Jangan memilih vendor secret manager baru.

6. Pelajari pattern credential handling yang SUDAH digunakan oleh `connection-service.ts`.

7. Tentukan secara eksplisit boundary yang benar untuk:

   operator credential
        ↓
   credential provisioning
        ↓
   secret reference
        ↓
   BotInstallation

8. Tentukan apakah provisioning seharusnya:
   - dilakukan oleh connection service yang sudah ada,
   - dilakukan oleh dedicated provisioning boundary,
   - atau menggunakan abstraction yang sudah tersedia.

9. Jangan langsung membuat implementation baru hanya berdasarkan asumsi.

10. Tentukan contract minimum yang diperlukan untuk B-058.

Contract harus menjawab minimal:

- input credential apa yang diterima operator,
- siapa yang memiliki tanggung jawab menyimpan credential,
- bagaimana secret reference dibuat,
- apa yang disimpan pada BotInstallation,
- apa yang dikembalikan API,
- bagaimana error provisioning ditangani,
- bagaimana credential tidak bocor ke log/response,
- bagaimana test menggunakan credential synthetic.

11. Pastikan `secret_ref` tetap menjadi internal reference.

12. Operator/UI TIDAK boleh diminta memasukkan `secret_ref` internal.

13. Raw bot token TIDAK boleh:
   - disimpan sebagai installation metadata,
   - dikembalikan API,
   - dicetak log,
   - dimasukkan error,
   - dimasukkan commit/source code.

14. Jangan mengubah `BotInstallation.status`.

15. Jangan mengimplementasikan Telegram polling/webhook runtime.

16. Jangan mengimplementasikan provider/module runtime baru.

17. Jangan menyentuh Gorouter.app.

18. NVIDIA dan TokenHarbor tidak perlu disentuh.

19. Jangan mengimplementasikan managed secret vendor tertentu.

20. Jangan membuat migration/schema baru pada tahap review ini.

HASIL YANG DIHARAPKAN

Setelah audit, dokumentasikan:

### B-058 Decision

- existing credential flow:
- existing secret flow:
- existing connection-service pattern:
- correct provisioning boundary:
- create-bot input:
- internal stored value:
- API response:
- error behavior:
- security considerations:

### Contract

Definisikan contract minimum yang diperlukan untuk implementation B-058.

Jika contract yang sudah ada sebenarnya sudah cukup:
- jangan membuat contract kedua,
- jelaskan bahwa implementation dapat langsung menggunakan contract existing.

Jika contract memang belum ada:
- buat hanya contract minimum yang benar-benar diperlukan,
- jangan membuat implementation provider/vendor.

VALIDATION

Jalankan validation yang relevan untuk audit/contract:

- pnpm test
- pnpm build
- pnpm typecheck
- pnpm lint
- pnpm format:check
- node scripts/check-imports.mjs
- node scripts/check-ownership.mjs
- node scripts/check-doc-links.mjs
- git diff --check

Jangan menjalankan atau membuat:

node scripts/check-symlinks.mjs

karena script tersebut tidak tersedia.

Jika tahap ini hanya menghasilkan keputusan/dokumentasi dan tidak ada perubahan kode yang diperlukan:
- jangan membuat empty commit,
- jangan membuat commit palsu,
- jangan push perubahan kosong.

Jika ada perubahan contract yang benar-benar diperlukan:
- review diff,
- buat satu commit yang sesuai,
- push ke:
  git push origin backend-dev-recovery
- verifikasi local SHA dan remote SHA.

PENTING

Jangan implementasikan B-058 penuh sebelum keputusan ADR-011 §4 jelas.

Jangan membuat architecture speculative.

Jangan membuat vendor dependency.

Jangan membuat credential palsu.

Jangan mengubah B-071.

Kerjakan langsung pada:

/root/botspace

OUTPUT AKHIR

Tampilkan:

### B-058 Decision
- keputusan architecture:
- provisioning boundary:
- credential input:
- secret reference:
- API behavior:
- security:

### Contract
- existing contract yang digunakan:
- contract baru jika benar-benar diperlukan:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit SHA:
- push:
- local/remote SHA:
- working tree:

### Remaining Deferred

### Next Roadmap

Tentukan implementation B-058 sebagai task berikutnya hanya setelah contract/decision ini benar-benar jelas.

```
# Prompt: B-057 — Managed Secret Reference Flow
```

Lanjutkan project BotSpace dari kondisi repository saat ini.

KONDISI TERAKHIR

- B-030 Workspace API/Contract SUDAH selesai.
- B-070 Storage Adapter SUDAH selesai.
- B-071 File/Share contract SUDAH selesai.
- B-071 File/Share API SUDAH selesai.
- Production wiring B-071 SUDAH selesai.
- Production SecretResolver boundary SUDAH tersedia.
- B-054 Module Management UI SUDAH selesai.
- B-055 Bot Installation Listing SUDAH selesai.
- B-056 Bot Installation Lifecycle UI SUDAH selesai.
- Working tree terakhir CLEAN.
- Branch: backend-dev-recovery.

Jangan mengulang B-030, B-070, B-071, B-054, B-055, atau B-056.

NEXT TASK: B-057 — MANAGED SECRET REFERENCE FLOW

Tujuan:

Perbaiki lifecycle pembuatan bot agar operator memasukkan credential/bot token yang sebenarnya, sementara aplikasi menyimpan credential melalui secret-handling boundary yang sudah tersedia dan hanya menggunakan `secret_ref` sebagai reference internal.

Masalah yang ditemukan pada audit B-056:

- Create bot masih meminta `secret_ref` mentah dari operator.
- Ini bukan UX yang benar.
- Operator seharusnya memasukkan credential/bot token.
- Sistem kemudian menyerahkan credential tersebut ke secret-handling mechanism yang sudah tersedia.
- Setelah tersimpan, aplikasi menggunakan reference/identifier secret, bukan raw credential.
- Jangan membuat secret-management system baru jika repository sudah memiliki pola yang dapat digunakan.

TUGAS

1. Audit implementation B-056 dan flow `createBot`.

2. Cari dan gunakan secret-handling pattern yang SUDAH ADA di repository, terutama:
   - connection-service.ts
   - SecretResolver
   - existing secret boundary
   - existing credential handling
   - existing configuration/composition root.

3. Jangan membuat interface `SecretResolver` kedua.

4. Jangan membuat secret manager baru.

5. Jangan memilih vendor secret manager baru.

6. Ubah create-bot flow agar input operator adalah credential/bot token, bukan internal `secret_ref`.

7. Setelah credential diterima:
   - jangan menyimpan raw credential sebagai BotInstallation field jika architecture tidak mengharuskannya,
   - jangan mengembalikan raw credential melalui API response,
   - jangan mencetak credential ke log,
   - gunakan existing secret-storage/secret boundary,
   - simpan hanya reference yang memang diperlukan oleh domain/application.

8. Jika existing secret-handling API membutuhkan `secret_ref`, buat reference tersebut secara internal setelah credential berhasil disimpan.

9. Pastikan UI create-bot tidak meminta operator mengetahui atau mengetik `secret_ref` internal.

10. Pastikan response API create-bot hanya mengembalikan data aman:
    - installation ID,
    - bot metadata,
    - status,
    - secret reference hanya jika contract memang secara eksplisit mengizinkan reference tersebut dikembalikan.

11. Jangan pernah mengembalikan raw bot token.

12. Pastikan error handling tidak membocorkan credential.

13. Pastikan test menggunakan synthetic/test credential saja.

14. Tambahkan test untuk:
    - create bot dengan credential valid,
    - credential diteruskan ke existing secret boundary,
    - secret reference dibuat/disimpan dengan benar,
    - raw credential tidak masuk response,
    - raw credential tidak masuk log/error,
    - missing credential ditolak,
    - secret-storage failure ditangani dengan aman,
    - create bot tidak meninggalkan installation invalid jika secret storage gagal,
    - existing lifecycle enable/disable/delete tetap bekerja.

15. Audit route + client/UI:
    - API request,
    - DTO,
    - create-bot form,
    - validation,
    - response mapping.

16. Jangan mengubah BotInstallation.status menjadi runtime/process state.

17. Jangan mengimplementasikan Telegram polling/webhook runtime.

18. Jangan menambahkan managed secret vendor baru.

19. Jangan mengerjakan public-share rate limiting, audit event, share expiry, distributed lock, retry/DLQ, event/outbox, atau multi-bot multiplexing.

20. Jangan menyentuh Gorouter.app.

21. NVIDIA dan TokenHarbor tidak perlu disentuh.

VALIDATION

Jalankan validation yang tersedia dan relevan:

- pnpm test
- pnpm build
- pnpm typecheck
- pnpm lint
- pnpm format:check
- node scripts/check-imports.mjs
- node scripts/check-ownership.mjs
- node scripts/check-doc-links.mjs
- git diff --check

Jangan membuat atau menjalankan:

node scripts/check-symlinks.mjs

karena file tersebut tidak tersedia.

SECURITY CHECK

Sebelum selesai, audit diff untuk memastikan tidak ada:

- raw bot token,
- API key,
- password,
- credential,
- secret,
- token test yang tertinggal,
- secret di log,
- secret di HTTP response,
- secret di error message.

Jika menemukan raw credential yang sudah ada sebelumnya, jangan menyalinnya ke tempat lain. Perbaiki hanya jika memang bagian dari B-057.

COMMIT

Jika implementation valid dan validation PASS:

1. Review git diff.
2. Pastikan hanya perubahan B-057.
3. Buat satu commit:

feat: implement managed secret reference flow

4. Push:

git push origin backend-dev-recovery

5. Verifikasi local SHA dan remote SHA sama.
6. Pastikan working tree CLEAN.

Jika tidak ada perubahan valid:
- jangan membuat empty commit,
- jangan push kosong.

OUTPUT AKHIR

Tampilkan:

### B-057
- create credential flow:
- secret storage:
- secret reference:
- API:
- UI:
- security:
- tests:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit SHA:
- push:
- local/remote SHA:
- working tree:

### Remaining Deferred
Hanya item yang benar-benar masih membutuhkan infrastructure, contract, environment, atau keputusan product.

### Next Roadmap
Tentukan task berikutnya berdasarkan dependency nyata repository.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-056 — Bot Installation Lifecycle UI
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
STATUS TERAKHIR
==================================================

B-030 Workspace API/Contract:
SELESAI.

B-070 Storage Adapter:
SELESAI.

B-071 File/Share contract:
SELESAI.

B-071 File/Share API:
SELESAI.

B-071 Production wiring:
SELESAI.

B-052 Module enable/disable use-case + API:
SELESAI.

B-053 API client + contract surfacing:
SELESAI.

B-054 Module Management UI:
SELESAI.

B-055 Bot Installation Listing Surfacing:
SELESAI.

Working tree terakhir:
CLEAN.

Branch:
backend-dev-recovery.

Jangan mengulang pekerjaan yang sudah selesai.

==================================================
TUJUAN B-056
==================================================

Implementasikan:

B-056 — Bot Installation Lifecycle UI

Tujuan utama:

Melengkapi lifecycle Bot Installation dari UI sampai
application/API layer:

CREATE
  ↓
LIST
  ↓
SELECT
  ↓
ENABLE / DISABLE
  ↓
DELETE

Audit terakhir menemukan:

BotInstallationService SUDAH tersedia.

Permission/use-case untuk lifecycle berikut SUDAH tersedia
di service/domain:

- create/bot
- status/bot
- delete/bot

Namun:

- route mutation belum seluruhnya diregister,
- API client belum memiliki method mutation lengkap,
- UI belum memiliki lifecycle management lengkap.

B-056 harus menutup gap tersebut.

==================================================
BAGIAN 1 — AUDIT WAJIB
==================================================

Sebelum coding, audit repository terlebih dahulu.

Cari dan pahami:

- BotInstallation entity/model
- BotInstallationService
- createBot
- get/list Bot Installation
- enableBot
- disableBot
- deleteBot
- permission/authorization
- existing API routes
- existing route registration
- API DTO/contract
- apps/web API client
- B-055 Bot Installation selector
- B-054 Module Management UI
- workspace context
- authentication
- existing modal/dialog components
- existing confirmation dialog
- existing toast/error pattern
- existing loading/mutation pattern.

PENTING:

Gunakan implementation yang SUDAH ADA.

Jangan membuat service kedua.

Jangan membuat repository kedua.

Jangan membuat authorization system baru.

Jangan membuat API client kedua.

==================================================
BAGIAN 2 — CREATE BOT INSTALLATION API
==================================================

Audit apakah createBot sudah memiliki application/use-case
dan contract yang benar.

Jika sudah tersedia:

Expose melalui API route menggunakan convention repository.

Jangan mengarang route path.

Ikuti naming/routing convention existing.

Request harus menggunakan workspace context yang authenticated.

Jangan mempercayai workspace ID dari client tanpa authorization
existing.

Response harus menggunakan DTO/shape yang sesuai contract.

Jangan mengembalikan:

- bot token,
- secret,
- credential,
- API key,
- private configuration.

Jika createBot membutuhkan credential/token:

gunakan boundary yang memang sudah ada.

Jangan hardcode credential.

==================================================
BAGIAN 3 — ENABLE / DISABLE API
==================================================

Register route untuk mutation:

- enable bot installation
- disable bot installation

Gunakan existing service/use-case.

Jangan membuat business logic baru di route.

Route hanya menangani:

- authentication,
- authorization boundary,
- input validation,
- service invocation,
- response mapping,
- error mapping.

Pastikan mutation hanya berlaku untuk Bot Installation
yang dimiliki workspace tersebut.

Cross-workspace mutation HARUS ditolak.

==================================================
BAGIAN 4 — DELETE API
==================================================

Expose delete Bot Installation melalui API jika service
dan contract existing memang sudah mendukungnya.

Requirements:

- authenticated,
- workspace scoped,
- authorization enforced,
- hanya owner/authorized workspace yang dapat menghapus,
- response/error mengikuti convention repository.

Jangan menghapus Bot Installation workspace lain hanya
karena ID diketahui.

Jangan melakukan hard delete terhadap data lain yang tidak
termasuk scope use-case.

Jangan membuat cascading delete speculative.

==================================================
BAGIAN 5 — ROUTE REGISTRATION
==================================================

Audit route registry/application composition.

Pastikan route baru benar-benar DIREGISTER.

Jangan hanya membuat file route tetapi lupa memasukkannya
ke router.

Verifikasi seluruh lifecycle:

CREATE
LIST
ENABLE
DISABLE
DELETE

dapat ditemukan oleh application router.

==================================================
BAGIAN 6 — API CLIENT
==================================================

Update typed API client yang sudah digunakan B-053/B-055.

Tambahkan method:

- listBotInstallations
- createBotInstallation
- enableBotInstallation
- disableBotInstallation
- deleteBotInstallation

Jika sebagian method sudah ada:

JANGAN membuat duplicate.

Gunakan implementation existing.

Jangan melakukan raw fetch langsung dari React component.

Jangan membuat API client baru.

==================================================
BAGIAN 7 — UI BOT INSTALLATION MANAGEMENT
==================================================

Update `apps/web`.

B-055 sudah menyediakan listing/selector.

Sekarang tambahkan lifecycle management UI.

UX minimal:

Bot Installations

[ + Add Bot ]

Bot Installation list:

[ Bot A ]     Enabled
             [Disable] [Delete]

[ Bot B ]     Disabled
             [Enable] [Delete]

User dapat:

1. membuat Bot Installation,
2. melihat daftar,
3. memilih bot,
4. enable,
5. disable,
6. delete.

Gunakan component/design system existing.

Jangan redesign seluruh dashboard.

==================================================
BAGIAN 8 — CREATE UI
==================================================

Tambahkan modal/dialog/page sesuai pattern UI existing.

Form hanya meminta field yang memang diperlukan oleh
existing createBot contract.

Jangan membuat field tambahan berdasarkan asumsi.

Jika createBot membutuhkan:

- bot name,
- bot identifier,
- credential,
- atau field lain,

gunakan contract yang sebenarnya.

Jangan menampilkan secret setelah submission jika contract
tidak mengharuskannya.

Jika credential bersifat secret:

- input harus appropriate,
- jangan log value,
- jangan menyimpan di browser state lebih lama dari yang diperlukan,
- jangan memasukkannya ke error message.

==================================================
BAGIAN 9 — ENABLE / DISABLE UX
==================================================

Enable/disable harus memiliki:

- loading state,
- success state,
- error state.

Saat mutation berlangsung:

- cegah double submission,
- jangan menjalankan mutation kedua secara tidak sengaja.

Setelah berhasil:

- refresh/update Bot Installation state,
- selector B-055 ikut berubah,
- Module Management B-054 menggunakan state terbaru.

Jangan membutuhkan reload browser penuh jika architecture
existing mendukung update state langsung.

==================================================
BAGIAN 10 — DELETE UX
==================================================

Delete adalah destructive action.

Gunakan confirmation dialog existing.

Contoh:

Delete this bot installation?

[Cancel] [Delete]

Jangan delete langsung ketika user menekan tombol tanpa
confirmation jika design system sudah menyediakan
confirmation pattern.

Setelah delete berhasil:

- hapus item dari list,
- reset selected Bot Installation jika yang dihapus sedang
  dipilih,
- jangan mempertahankan Bot Installation ID yang sudah
  tidak valid,
- Module Management harus masuk ke empty state atau
  memilih bot valid berikutnya sesuai UX existing.

==================================================
BAGIAN 11 — EMPTY STATE
==================================================

Jika workspace tidak memiliki Bot Installation:

Tampilkan empty state yang jelas.

Contoh:

No bot installations found.

[ + Add Bot ]

Jangan menampilkan:

- fake bot,
- hardcoded Bot Installation ID,
- module list tanpa bot.

==================================================
BAGIAN 12 — WORKSPACE ISOLATION
==================================================

Pastikan perubahan workspace menyebabkan:

- list Bot Installation reload,
- selected Bot Installation di-reset jika tidak valid,
- module state tidak bocor dari workspace sebelumnya.

Cache/state key harus memperhitungkan workspace.

Jangan sampai:

Workspace A
Bot A
Module state A

terbawa ketika user berpindah ke:

Workspace B.

==================================================
BAGIAN 13 — MODULE MANAGEMENT INTEGRATION
==================================================

Integrasikan dengan B-054 dan B-055.

Flow akhir harus:

Workspace
  ↓
Bot Installations
  ↓
Select Bot
  ↓
Manage Modules

Jika user:

CREATE bot
→ bot muncul di list.

ENABLE bot
→ status berubah.

DISABLE bot
→ status berubah.

DELETE selected bot
→ selection reset.

Pilih bot lain
→ module state bot tersebut dimuat.

Jangan mengubah Module Management business logic jika
tidak diperlukan.

==================================================
BAGIAN 14 — STATUS SEMANTICS
==================================================

Jangan mengubah arti `BotInstallation.status`.

Lifecycle state:

- enabled
- disabled
- atau enum/status yang memang sudah digunakan repository.

Jangan menggunakan status tersebut sebagai:

- process state,
- polling state,
- worker state,
- runtime connection state.

Jangan menambahkan Telegram runtime hanya untuk membuat
status terlihat aktif.

==================================================
BAGIAN 15 — SECURITY
==================================================

Review seluruh lifecycle API.

Pastikan:

- authentication,
- workspace authorization,
- ownership,
- cross-workspace isolation,
- input validation,
- error sanitization.

Jangan bocorkan:

- bot token,
- secret,
- credential,
- API key.

Pastikan ID Bot Installation yang berasal dari client
selalu divalidasi terhadap workspace/auth context.

==================================================
BAGIAN 16 — TEST BACKEND
==================================================

Tambahkan/update test untuk:

CREATE:

1. authenticated workspace dapat membuat Bot Installation.
2. unauthorized request ditolak.
3. invalid input ditolak.
4. credential/secret tidak masuk response/log.

LIST:

5. hanya Bot Installation workspace sendiri yang dikembalikan.

ENABLE:

6. workspace dapat enable bot miliknya.
7. cross-workspace enable ditolak.

DISABLE:

8. workspace dapat disable bot miliknya.
9. cross-workspace disable ditolak.

DELETE:

10. workspace dapat delete bot miliknya.
11. cross-workspace delete ditolak.
12. deleting nonexistent bot menghasilkan error yang sesuai.

Lifecycle:

13. create → list.
14. enable → status berubah.
15. disable → status berubah.
16. delete → bot tidak lagi muncul.

==================================================
BAGIAN 17 — TEST FRONTEND
==================================================

Tambahkan/update test untuk:

1. list Bot Installation tampil.
2. create dialog tampil.
3. create berhasil memperbarui list.
4. create error ditampilkan dengan aman.
5. enable mutation bekerja.
6. disable mutation bekerja.
7. delete confirmation bekerja.
8. cancel delete tidak melakukan mutation.
9. delete berhasil menghapus item dari UI.
10. delete selected bot me-reset selection.
11. workspace switch me-reset state yang invalid.
12. module UI mengikuti selected Bot Installation.
13. loading state mutation bekerja.
14. double submission dicegah.

Gunakan test utility/pattern existing.

Jangan membuat fake architecture.

==================================================
BAGIAN 18 — VALIDATION
==================================================

Jalankan validation yang tersedia:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs

Dan:

git diff --check

Untuk:

node scripts/check-symlinks.mjs

Jangan membuat script tersebut.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jangan membuat fake validation.

==================================================
BAGIAN 19 — DIFF REVIEW
==================================================

Setelah implementation:

git status
git diff --stat
git diff

Pastikan perubahan hanya untuk B-056.

Hapus:

- debug logs,
- temporary files,
- unused imports,
- duplicate DTO,
- duplicate API client,
- hardcoded Bot Installation ID,
- hardcoded credential,
- unrelated refactor.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA provider,
- TokenHarbor provider,

kecuali perubahan benar-benar diperlukan oleh compile/test
dan langsung terkait architecture yang sedang dikerjakan.

==================================================
BAGIAN 20 — COMMIT + PUSH
==================================================

Jika implementation valid dan validation selesai:

Buat SATU commit.

Commit message:

feat: add bot installation lifecycle ui

atau gunakan message yang lebih tepat berdasarkan diff.

Kemudian langsung:

git push origin backend-dev-recovery

Setelah push:

git rev-parse HEAD

dan verifikasi remote branch SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

WORKING TREE == CLEAN

Jika tidak ada perubahan valid:

- jangan membuat empty commit,
- jangan push kosong.

Jika push gagal:

- jangan reset commit,
- jangan menghapus commit,
- jangan mengubah credential GitHub sembarangan,
- tampilkan error dengan jelas.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan:

### B-056 STATUS

Create API:
List API:
Enable API:
Disable API:
Delete API:
API client:
UI:
Workspace authorization:
Module integration:

### TEST

Backend:
Frontend:

### VALIDATION

Test:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Local SHA:
Remote SHA:
Push:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih deferred.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata
repository.

Jangan membuat fitur acak.

PENTING:
- Jangan mengulang B-030.
- Jangan mengulang B-070.
- Jangan mengulang B-071.
- Jangan membuat production module definitions.
- Jangan membuat Telegram polling/webhook runtime.
- Jangan mengubah BotInstallation.status menjadi process state.
- Jangan membuat contract speculative.
- Jangan menyentuh Gorouter.app.
- NVIDIA dan TokenHarbor tidak perlu disentuh.
- Kerjakan langsung pada `/root/botspace`.

```
# Prompt: B-055 — Bot Installation Listing Surfacing
```
Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
STATUS TERAKHIR
==================================================

B-030 Workspace API/Contract:
SELESAI.

B-070 Storage Adapter:
SELESAI.

B-071 File/Share contract:
SELESAI.

B-071 File/Share API:
SELESAI.

B-071 Production wiring:
SELESAI.

B-052 Module enable/disable use-case + API:
SELESAI.

B-053 API client + contract surfacing:
SELESAI.

B-054 Module Management UI:
SELESAI.

Push terakhir:
BERHASIL.

Working tree:
CLEAN.

Jangan mengulang pekerjaan di atas.

==================================================
TUJUAN B-055
==================================================

Implementasikan:

B-055 — Bot Installation Listing Surfacing

Tujuan:

Menyediakan kemampuan untuk mengambil daftar Bot Installation
milik workspace melalui API dan menampilkannya di `apps/web`
sehingga user dapat memilih bot installation yang sedang
dikelola.

Hasil audit terakhir menunjukkan:

- `BotInstallationService` SUDAH tersedia.
- Service tersebut SUDAH dibuat di composition root.
- API route untuk listing bot installation BELUM tersedia.
- API client belum memiliki method listing bot installation.
- UI masih membutuhkan input Bot Installation ID secara manual.

Tugas B-055 adalah menutup gap tersebut.

Alur yang diinginkan:

BotInstallationService
        ↓
API route
        ↓
typed API contract/client
        ↓
apps/web
        ↓
Bot Installation selector
        ↓
Module Management UI

==================================================
BAGIAN 1 — AUDIT WAJIB
==================================================

Sebelum coding, audit repository terlebih dahulu:

- BotInstallation domain
- BotInstallationService
- repository/interface yang sudah tersedia
- composition root
- existing API routes
- API DTO
- API client
- apps/web
- workspace context
- Module Management UI B-054
- authentication/authorization
- existing selector/dropdown component
- existing loading/error pattern
- existing data-fetching pattern.

Cari implementasi yang sudah ada.

JANGAN membuat service BotInstallation baru jika service
yang dibutuhkan sudah tersedia.

JANGAN membuat repository baru jika repository existing
sudah dapat digunakan.

JANGAN menduplikasi contract.

==================================================
BAGIAN 2 — BOT INSTALLATION LIST API
==================================================

Expose endpoint/API untuk mengambil Bot Installations
yang dimiliki workspace aktif.

Gunakan naming dan routing convention yang sudah dipakai
repository.

Contoh konsep:

GET /workspaces/:workspaceId/bots

TAPI:

Jangan langsung menggunakan path tersebut jika repository
sudah mempunyai convention berbeda.

Ikuti convention existing.

Endpoint harus:

- authenticated,
- workspace-scoped,
- hanya mengembalikan bot installation yang boleh dilihat
  oleh user/workspace tersebut.

Jangan mengembalikan Bot Installation milik workspace lain.

==================================================
BAGIAN 3 — RESPONSE CONTRACT
==================================================

Audit model/DTO BotInstallation yang sudah ada.

Expose hanya field yang memang diperlukan oleh UI.

Minimal UI membutuhkan identifier dan informasi display
yang memang tersedia dari model.

Jangan mengarang:

- bot username,
- bot name,
- Telegram metadata,
- status,
- token,
- credential.

Jika field tersedia, gunakan.

Jika tidak tersedia, jangan membuat fake value.

PENTING:

Jangan pernah mengembalikan:

- bot token,
- secret,
- credential,
- API key,
- internal secret,
- private configuration.

==================================================
BAGIAN 4 — AUTHORIZATION
==================================================

Workspace isolation WAJIB.

Jika request berasal dari:

workspace A

maka hanya Bot Installation workspace A yang boleh
dikembalikan.

Jangan mempercayai workspace ID dari client tanpa validasi
authorization existing.

Gunakan authentication/workspace authorization boundary
yang sudah ada.

Jangan membuat authorization system baru.

Test minimal:

1. authorized workspace dapat melihat bot installation sendiri.
2. workspace A tidak dapat melihat bot installation workspace B.
3. unauthenticated request ditolak sesuai convention API.
4. invalid workspace context ditolak dengan aman.

==================================================
BAGIAN 5 — API CLIENT B-053
==================================================

Tambahkan method typed API client untuk listing Bot Installation.

Gunakan architecture B-053.

Jangan:

- melakukan raw fetch langsung dari component,
- membuat API client kedua,
- membuat duplicate DTO,
- membuat duplicate route helper.

Gunakan pattern yang sudah digunakan modules.list,
modules.enable, dan modules.disable.

Jika API client B-053 membutuhkan contract surfacing baru:

buat perubahan minimum yang diperlukan.

==================================================
BAGIAN 6 — WEB UI
==================================================

Update `apps/web`.

Tujuan:

HAPUS kebutuhan user untuk memasukkan Bot Installation ID
secara manual pada Module Management UI jika UI B-054
saat ini memang masih menggunakan input manual.

Ganti dengan Bot Installation selector.

Contoh UX:

Bot Installation
[ Select bot installation ▼ ]

Setelah bot dipilih:

Module list
- Module A   Enabled
- Module B   Disabled
- ...

Selector harus mengambil data dari API.

Jangan hardcode bot ID.

==================================================
BAGIAN 7 — WORKSPACE CONTEXT
==================================================

Gunakan workspace context existing.

Jika user berpindah workspace:

- daftar Bot Installation harus mengikuti workspace baru,
- pilihan bot lama harus di-reset jika tidak lagi valid,
- module state harus mengikuti bot baru.

Jangan menyimpan bot installation selection
sebagai global state yang melewati workspace.

==================================================
BAGIAN 8 — DEFAULT SELECTION
==================================================

Jika workspace memiliki beberapa Bot Installation:

Jangan memilih secara random.

Gunakan convention existing jika ada.

Jika belum ada:

- boleh memilih item pertama sebagai default hanya jika
  itu konsisten dengan UX repository,
- atau biarkan user memilih secara eksplisit.

Yang penting jangan mengarang Bot Installation.

Jika daftar kosong:

Tampilkan empty state yang jelas.

Contoh:

"No bot installations found."

Jangan menampilkan fake bot.

==================================================
BAGIAN 9 — MODULE MANAGEMENT INTEGRATION
==================================================

Integrasikan selector dengan B-054.

Flow:

1. Load workspace.
2. Load bot installations.
3. User memilih bot installation.
4. Load module state untuk bot tersebut.
5. Enable/disable module menggunakan B-052/B-053.
6. Jika bot berubah:
   - module state lama tidak boleh terbawa,
   - load state bot baru.

Pastikan query/cache key memperhitungkan:

workspace
+
bot installation

Jangan sampai:

Bot A module state

terpakai untuk:

Bot B.

==================================================
BAGIAN 10 — LOADING STATE
==================================================

Pisahkan loading state:

- loading bot installations,
- loading modules,
- mutation enable/disable.

Jangan memblokir seluruh halaman jika hanya module mutation
yang sedang berjalan.

Saat daftar bot sedang dimuat:

selector menunjukkan loading state.

Saat daftar kosong:

empty state.

Saat API gagal:

error state sesuai UI convention.

==================================================
BAGIAN 11 — ERROR HANDLING
==================================================

Jika API listing gagal:

- jangan menampilkan stack trace,
- jangan menampilkan SQL error,
- jangan menampilkan credential,
- jangan menampilkan internal path.

Gunakan error UI yang sudah digunakan project.

Jika bot installation tidak lagi valid:

- reset selection,
- jangan menjalankan module mutation menggunakan ID lama.

==================================================
BAGIAN 12 — RESPONSIVE UI
==================================================

Pastikan selector dapat digunakan pada:

- desktop,
- tablet,
- mobile.

Ikuti design system existing.

Jangan redesign seluruh dashboard.

Jangan menambahkan dependency UI baru jika tidak diperlukan.

==================================================
BAGIAN 13 — TEST BACKEND
==================================================

Tambahkan test untuk API listing.

Minimal:

1. authenticated workspace dapat list bot installation.
2. hanya installation workspace sendiri yang dikembalikan.
3. cross-workspace access ditolak.
4. unauthorized request ditolak.
5. empty workspace menghasilkan empty list.
6. response tidak mengandung token/secret/credential.
7. invalid workspace context ditangani dengan benar.

Gunakan test helper existing.

Jangan membuat mock architecture baru.

==================================================
BAGIAN 14 — TEST FRONTEND
==================================================

Tambahkan/update test untuk:

1. Bot Installation selector muncul.
2. selector mengambil data dari API client.
3. daftar bot ditampilkan.
4. empty state bekerja.
5. API error bekerja.
6. memilih bot memuat module state yang benar.
7. mengganti bot mengganti module state.
8. workspace change tidak mempertahankan bot ID lama
   jika tidak valid.
9. tidak ada hardcoded Bot Installation ID.

==================================================
BAGIAN 15 — SECURITY AUDIT
==================================================

Periksa diff untuk memastikan:

- tidak ada bot token,
- tidak ada Telegram credential,
- tidak ada API key,
- tidak ada secret,
- tidak ada workspace ID hardcoded,
- tidak ada Bot Installation ID hardcoded,
- tidak ada bypass authorization.

Jangan mengubah security architecture yang sudah benar.

==================================================
BAGIAN 16 — SCOPE KERAS
==================================================

JANGAN mengerjakan:

- Telegram polling,
- Telegram webhook runtime,
- multi-bot multiplexing,
- managed secret manager,
- PostgreSQL integration infrastructure,
- MinIO infrastructure,
- public-share rate limiting,
- public-share audit event,
- share expiry,
- production module definitions,
- module registry baru,
- provider integration,
- Gorouter.app.

B-055 hanya:

Bot Installation listing surfacing
+
API client
+
UI selector
+
B-054 integration.

==================================================
BAGIAN 17 — VALIDATION
==================================================

Jalankan validation yang tersedia:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs

Dan:

git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script tersebut.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jangan membuat fake validation.

==================================================
BAGIAN 18 — DIFF REVIEW
==================================================

Setelah coding:

git status
git diff --stat
git diff

Pastikan perubahan hanya terkait B-055.

Hapus jika ada:

- temporary files,
- debug logs,
- unused imports,
- duplicate API client,
- duplicate DTO,
- hardcoded IDs,
- unrelated refactor.

==================================================
BAGIAN 19 — COMMIT + PUSH
==================================================

Jika implementation valid dan validation selesai:

Buat SATU commit.

Commit message:

feat: surface bot installation listing

atau gunakan message yang lebih tepat berdasarkan
perubahan aktual.

Kemudian LANGSUNG:

git push origin backend-dev-recovery

Setelah push:

git rev-parse HEAD

dan verifikasi remote branch SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

WORKING TREE == CLEAN

Jika tidak ada perubahan valid:

jangan membuat empty commit.

Jika push gagal:

- jangan reset commit,
- jangan menghapus commit,
- jangan mengubah credential GitHub sembarangan,
- tampilkan error push dengan jelas.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan:

### B-055 STATUS

Backend route:
API contract:
API client:
Workspace authorization:
Bot selector:
Module integration:
Loading/error state:
Tests:

### FILE YANG BERUBAH

Daftar file + alasan singkat.

### VALIDATION

Test:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Local SHA:
Remote SHA:
Push:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih deferred.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata
repository.

Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace


```
# Prompt: B-054 — Module Management UI
```
Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
STATUS TERAKHIR
==================================================

B-030 Workspace API/Contract:
SELESAI.

B-070 Storage Adapter:
SELESAI.

B-071 File/Share contract:
SELESAI.

B-071 File/Share API:
SELESAI.

B-071 Production wiring:
SELESAI.

B-052 Enable/Disable Module Use-Case + API:
SELESAI.

B-053 API Client + Contract Surfacing:
SELESAI.

Push terakhir:
BERHASIL.

Local SHA == Remote SHA.

Working tree:
CLEAN.

Jangan mengulang pekerjaan di atas.

==================================================
TUJUAN B-054
==================================================

Implementasikan:

B-054 — Module Management UI di apps/web

Tujuannya adalah menyediakan UI web untuk:

1. mengambil daftar module yang tersedia,
2. menampilkan status module,
3. enable module,
4. disable module,
5. mengelola enabled/disabled state PER BOT INSTALLATION.

UI harus menggunakan API client/contract yang sudah dibuat
oleh B-052/B-053.

Dependency yang sudah tersedia:

modules.list
modules.enable
modules.disable

Gunakan implementation yang sudah ada.

Jangan membuat API baru hanya untuk UI.

==================================================
BAGIAN 1 — AUDIT DULU
==================================================

Sebelum coding, audit:

- apps/web
- routing web
- existing dashboard/page structure
- existing API client usage
- authentication
- workspace context
- bot installation selection
- module-related API client
- existing UI component library
- existing loading state
- existing error handling
- existing toast/notification pattern
- existing confirmation dialog/modal pattern.

Cari apakah sudah ada halaman:

- bot detail,
- bot installation detail,
- settings,
- modules,
- configuration.

Jika sudah ada lokasi yang tepat:

INTEGRASIKAN ke halaman tersebut.

Jangan membuat dashboard baru jika tidak diperlukan.

==================================================
BAGIAN 2 — MODULE LIST
==================================================

Buat UI untuk menampilkan daftar module yang tersedia
berdasarkan API `modules.list` yang sudah ada.

Setiap module minimal menampilkan informasi yang memang
tersedia dari API contract.

Jangan mengarang field.

Jika contract memiliki:

- module id,
- name,
- description,
- enabled state,
- metadata,

gunakan field tersebut.

Jika field tertentu tidak tersedia:

jangan membuat data palsu hanya agar UI terlihat lengkap.

==================================================
BAGIAN 3 — PER BOT INSTALLATION
==================================================

PENTING:

Status module harus dikelola PER BOT INSTALLATION.

Contoh:

Bot A:
- Module X ENABLED
- Module Y DISABLED

Bot B:
- Module X DISABLED
- Module Y ENABLED

Jangan membuat global module state yang menyebabkan
satu bot mengubah bot lain.

UI harus mengetahui bot installation yang sedang dipilih.

Gunakan existing workspace/bot installation context.

Jangan hardcode bot ID.

==================================================
BAGIAN 4 — ENABLE / DISABLE
==================================================

Gunakan API client B-053:

- modules.enable
- modules.disable

Jangan memanggil HTTP endpoint secara manual dari component
jika repository sudah menyediakan typed API client.

Flow:

User klik Enable
    ↓
UI loading
    ↓
API client modules.enable
    ↓
success
    ↓
update/revalidate state
    ↓
UI menunjukkan Enabled

User klik Disable
    ↓
UI loading
    ↓
API client modules.disable
    ↓
success
    ↓
update/revalidate state
    ↓
UI menunjukkan Disabled

Jangan mengubah state UI secara permanen jika API gagal.

==================================================
BAGIAN 5 — LOADING STATE
==================================================

Implementasikan loading state yang jelas.

Saat enable/disable sedang berjalan:

- tombol/module toggle tidak boleh menghasilkan request
  berulang secara tidak sengaja,
- tampilkan state processing,
- cegah race condition sederhana pada module yang sama.

Jangan memblokir seluruh dashboard jika hanya satu module
yang sedang diubah.

==================================================
BAGIAN 6 — ERROR HANDLING
==================================================

Jika API gagal:

- jangan menampilkan stack trace,
- jangan menampilkan credential,
- jangan menampilkan internal database error,
- jangan menampilkan secret,
- jangan menganggap operasi berhasil.

Tampilkan error yang aman dan user-friendly sesuai
convention UI yang sudah ada.

Setelah error:

- state harus kembali konsisten,
- jangan meninggalkan UI dalam keadaan enabled jika server
  sebenarnya masih disabled.

==================================================
BAGIAN 7 — AUTHORIZATION
==================================================

UI harus menghormati authorization yang sudah ada.

Jangan menambahkan authorization logic palsu di frontend.

Server/API tetap menjadi authority.

Frontend hanya:

- menggunakan authenticated session,
- workspace context,
- bot installation context,
- typed API client.

Jangan menyediakan cara untuk mengganti workspace/bot ID
secara manual untuk bypass authorization.

==================================================
BAGIAN 8 — UX
==================================================

Gunakan UI style yang sudah dipakai `apps/web`.

Jangan memperkenalkan design system baru.

Module list harus:

- mudah dibaca,
- compact,
- responsive,
- jelas mana Enabled/Disabled,
- mudah melakukan toggle,
- memiliki empty state jika tidak ada module,
- memiliki loading state,
- memiliki error state.

Jika existing UI menggunakan card/table/list:

ikuti pattern existing.

Jangan membuat UI berlebihan.

==================================================
BAGIAN 9 — CONFIRMATION
==================================================

Untuk DISABLE:

Periksa apakah UI repository sudah memiliki confirmation
dialog untuk destructive/behavior-changing action.

Jika pattern tersebut tersedia, gunakan.

Jika tidak tersedia dan disable memang dianggap aman
menurut existing UX convention, jangan membuat dialog
kompleks hanya untuk task ini.

Jangan mengubah backend behavior.

==================================================
BAGIAN 10 — CACHE / REVALIDATION
==================================================

Audit mekanisme data fetching existing:

- React Query,
- SWR,
- server actions,
- loader,
- fetcher,
- custom API hooks,
- atau pattern lain.

Gunakan pattern yang SUDAH digunakan project.

Setelah enable/disable:

- invalidate/revalidate module state,
- atau update cache sesuai convention existing.

Jangan membuat state-management system baru.

==================================================
BAGIAN 11 — TEST
==================================================

Tambahkan test sesuai testing architecture `apps/web`.

Minimal test behavior:

1. module list berhasil ditampilkan.
2. enabled state ditampilkan dengan benar.
3. disabled state ditampilkan dengan benar.
4. enable memanggil API client yang benar.
5. disable memanggil API client yang benar.
6. bot installation context diteruskan dengan benar.
7. loading state muncul saat mutation.
8. duplicate click/request dicegah saat mutation.
9. API failure menampilkan error aman.
10. state tidak falsely berubah ketika API gagal.
11. empty module list ditangani.
12. workspace/bot context tidak hardcoded.

Jangan membuat mock API baru yang berbeda dari
contract B-053.

Gunakan mock/test helper existing jika tersedia.

==================================================
BAGIAN 12 — RESPONSIVE
==================================================

Pastikan UI dapat digunakan pada:

- desktop,
- tablet,
- mobile.

Jangan melakukan redesign seluruh `apps/web`.

Hanya buat layout module management yang diperlukan.

==================================================
BAGIAN 13 — SCOPE KERAS
==================================================

JANGAN mengerjakan:

- production module definitions,
- module manifest baru,
- module handler baru,
- Telegram polling,
- Telegram webhook,
- secret-manager,
- distributed lock,
- retry/DLQ,
- event/outbox,
- multi-bot multiplexing,
- share expiry,
- public-share rate limiting,
- public-share audit event.

Jangan membuat module baru hanya agar UI mempunyai
contoh data.

Jika registry module saat ini kosong:

UI harus menangani empty state dengan benar.

Jangan mengarang production module.

==================================================
BAGIAN 14 — API CONTRACT
==================================================

Gunakan contract yang sudah tersedia.

Jangan:

- membuat `modules.enable` kedua,
- membuat `modules.disable` kedua,
- membuat route kedua,
- membuat DTO kedua,
- membuat API client kedua.

Jika B-053 ternyata belum menyediakan method tertentu:

audit repository terlebih dahulu.

Jika benar-benar missing:

buat perubahan minimum yang diperlukan dan tetap
mengikuti contract existing.

Jangan melakukan refactor besar.

==================================================
BAGIAN 15 — VALIDATION
==================================================

Jalankan validation yang tersedia:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs

Dan:

git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script tersebut.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jangan membuat fake validation.

==================================================
BAGIAN 16 — AUDIT UI
==================================================

Sebelum commit:

Periksa:

- tidak ada hardcoded credential,
- tidak ada token di source,
- tidak ada API key,
- tidak ada workspace ID hardcoded,
- tidak ada bot installation ID hardcoded,
- tidak ada debug console yang tidak diperlukan,
- tidak ada temporary component,
- tidak ada unused import,
- tidak ada duplicate API client,
- tidak ada unrelated frontend refactor.

Pastikan hanya scope B-054 yang berubah.

==================================================
BAGIAN 17 — GIT
==================================================

Jalankan:

git status
git diff --stat
git diff

Jika validation PASS dan perubahan valid:

buat SATU commit.

Commit message:

feat: add module management ui

atau gunakan message yang lebih tepat berdasarkan
perubahan aktual.

Kemudian LANGSUNG:

git push origin backend-dev-recovery

Verifikasi:

git rev-parse HEAD

dan remote branch SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

WORKING TREE == CLEAN

Jika tidak ada perubahan valid:

jangan membuat empty commit.

Jika push gagal:

- jangan menghapus commit,
- jangan reset,
- jangan mengubah credential GitHub sembarangan,
- tampilkan error push dengan jelas.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-054 STATUS

Module list:
Enable:
Disable:
Per-bot installation:
Loading:
Error handling:
Authorization:
Responsive UI:

### FILE YANG BERUBAH

Tampilkan daftar file dan alasan singkat.

### TEST

Unit:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Local SHA:
Remote SHA:
Push:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih
belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency
NYATA repository.

Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace


```
# Prompt: B-053 — API Client + Contract Surfacing
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-030 — Workspace API/Contract:
SELESAI.

B-070 — Storage Adapter:
SELESAI.

B-071 — File/Share:
SELESAI.

B-040 s/d B-052 — worker/runtime foundation dan
enabled-module lifecycle:
SELESAI.

B-052 sudah menyediakan:

- enabled-module persistence,
- enable use-case,
- disable use-case,
- API route,
- DTO,
- authorization/workspace boundary,
- validation dan test.

Build terakhir PASS.
Working tree terakhir CLEAN.

Next roadmap yang teridentifikasi:

B-053 — API client + contract surfacing untuk module
enable/disable.

==================================================
TUJUAN
==================================================

Lengkapi sisi API client/contract surfacing untuk
B-052.

Jangan mengulang implementasi B-052.

Target:

Existing API route/DTO B-052
        ↓
typed API contract
        ↓
@botspace/api-client
        ↓
consumer dapat menggunakan enable/disable module
secara typed dan konsisten.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-030
- B-070
- B-071
- B-050
- B-051
- B-052

Jangan membuat use-case enable/disable kedua.

Jangan membuat repository kedua.

Jangan membuat route kedua.

Jangan membuat DTO kedua yang menduplikasi B-052.

Jangan membuat API client abstraction kedua.

Audit terlebih dahulu struktur `@botspace/api-client`
yang SUDAH ADA.

Gunakan pattern API client existing.

Jangan membuat OpenAPI generator baru jika repository
belum menggunakan OpenAPI generation.

Jangan menambahkan dependency eksternal hanya untuk
membuat typed client.

Jangan mengubah database schema.

Jangan mengubah persistence adapter.

Jangan mengubah module runtime.

Jangan membuat production module definitions.

Jangan mengimplementasikan Telegram integration.

Jangan mengimplementasikan secret-manager.

Jangan mengimplementasikan distributed lock.

Jangan mengimplementasikan retry/DLQ.

Jangan mengimplementasikan event/outbox.

Jangan mengimplementasikan multi-bot multiplexing.

Jangan menyentuh Gorouter.app.

NVIDIA dan TokenHarbor tidak perlu disentuh.

==================================================
BAGIAN 1 — AUDIT API CLIENT
==================================================

Audit repository terlebih dahulu.

Cari:

- package `@botspace/api-client`,
- existing API client modules,
- typed request/response pattern,
- route contract pattern,
- DTO mapping,
- authentication/request context,
- error handling,
- workspace context,
- generated types jika ada,
- existing client tests.

Cari apakah endpoint B-052 sudah memiliki
representasi typed di client.

Jangan coding sebelum mengetahui pattern existing.

==================================================
BAGIAN 2 — TYPE SURFACING
==================================================

Expose contract B-052 melalui API client dengan
menggunakan type/model yang sudah menjadi source of truth.

Minimal:

- enable module request,
- enable module response,
- disable module request,
- disable module response,
- relevant error/result types jika architecture
  API client memang mengeksposnya.

Jangan membuat duplicate domain model jika type
existing dapat digunakan.

Jika repository memiliki shared API contract package,
gunakan package tersebut.

==================================================
BAGIAN 3 — CLIENT METHODS
==================================================

Tambahkan typed client methods untuk:

- enable module,
- disable module.

Gunakan naming convention API client yang sudah ada.

Client method harus:

1. mengirim request ke route B-052 yang sebenarnya,
2. menggunakan authentication mechanism existing,
3. meneruskan workspace context secara benar,
4. memetakan response ke type yang benar,
5. memetakan error sesuai convention existing.

Jangan hardcode workspace ID jika client architecture
mengambilnya dari authenticated context.

Jangan memasukkan credential/token ke source code.

==================================================
BAGIAN 4 — CONTRACT CONSISTENCY
==================================================

Pastikan:

API route
=
DTO
=
API contract
=
typed client

Tidak boleh ada perbedaan:

- field name,
- optional/required,
- enum,
- identifier,
- error semantics,
- response shape.

Jika menemukan mismatch:

audit mana yang merupakan source of truth.

Jangan mengubah B-052 secara besar-besaran hanya
demi client.

Jika perubahan kecil memang diperlukan untuk
consistency, lakukan hanya jika justified.

==================================================
BAGIAN 5 — AUTHORIZATION
==================================================

Pastikan API client tidak menyediakan cara untuk
bypass authorization.

Client hanya mengirim request sesuai contract.

Server tetap menjadi authority untuk:

- authenticated user,
- workspace,
- permission,
- module availability.

Jangan memindahkan authorization logic ke client.

==================================================
BAGIAN 6 — TEST
==================================================

Tambahkan test sesuai pattern repository.

Minimal:

1. enable client request menggunakan route yang benar.
2. disable client request menggunakan route yang benar.
3. request body sesuai contract.
4. response mapping sesuai DTO.
5. error mapping sesuai API convention.
6. authentication/request context tetap diteruskan.
7. tidak ada credential yang masuk log/test output.

Jika repository menggunakan contract snapshot atau
generated API schema:

jalankan validation yang memang sudah tersedia.

Jangan membuat test infrastructure baru hanya untuk
B-053.

==================================================
BAGIAN 7 — BACKWARD COMPATIBILITY
==================================================

Jangan merusak existing API client.

Pastikan seluruh client method existing tetap bekerja.

Jangan melakukan refactor besar.

Jika ada duplicate helper:

gunakan helper existing jika aman.

==================================================
BAGIAN 8 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script tersebut.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jangan menjalankan integration test Gorouter.app.

==================================================
BAGIAN 9 — DIFF REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan perubahan hanya berkaitan dengan:

- API client B-052,
- shared API contract bila memang diperlukan,
- tests,
- dokumentasi yang relevan.

Hapus:

- debug code,
- temporary files,
- generated junk,
- unrelated refactor.

==================================================
BAGIAN 10 — COMMIT + PUSH
==================================================

Jika implementation valid dan validation selesai:

buat SATU commit.

Gunakan message:

feat: surface module toggle api client

atau commit message yang lebih tepat berdasarkan
perubahan aktual.

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote branch SHA.

Pastikan:

local SHA == remote SHA
working tree == CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah credential GitHub sembarangan,
- tampilkan error push dengan jelas.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-053 STATUS

API Client:
Enable:
Disable:
Typed Contract:
Error Mapping:
Authorization:

### TEST

Unit:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih
belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency
nyata repository.

Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-052 — Enable/Disable Module Use-Case + API Contract
```
Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-030 — Workspace API/Contract:
SELESAI.

B-070 — Storage Adapter:
SELESAI.

B-071 — File/Share:
SELESAI.

B-040 s/d B-050 — worker/runtime foundation:
SELESAI.

B-051 — Enabled-module persistence adapter:
SELESAI.

B-051 sudah menyediakan persistence path nyata untuk enabled
modules dan PostgreSQL adapter.

Validation terakhir berhasil:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push berhasil.

==================================================
TARGET SEKARANG
==================================================

Implementasikan:

B-052 — enable/disable module use-case + contract (API side).

B-051 sudah menyediakan persistence read/write foundation
yang diperlukan.

Sekarang lengkapi lifecycle enable/disable dari sisi
application/use-case dan API contract.

Target architecture:

API / route
    ↓
Enable/Disable Module Use-Case
    ↓
EnabledModuleRepository
    ↓
PostgreSQL Adapter
    ↓
enabled-module persistence

Serta:

Module Runtime
    ↓
listEnabled / enabled-module state
    ↓
Module Registry / Composition

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-030
- B-070
- B-071
- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-047
- B-048
- B-049
- B-050
- B-051

Jangan membuat persistence abstraction kedua.

Jangan membuat EnabledModuleRepository kedua.

Jangan membuat ModuleRuntime kedua.

Jangan membuat module registry kedua.

Jangan membuat API contract yang menduplikasi contract existing.

Jangan membuat schema speculative.

Jangan membuat migration baru jika schema B-051 sudah cukup.

Jangan mengubah persistence model tanpa alasan nyata.

Jangan implementasikan product module definitions pada tahap ini
kecuali repository memang sudah memiliki module-definition contract
yang wajib digunakan oleh B-052.

Jangan implementasikan real Telegram integration.

Jangan implementasikan polling/webhook.

Jangan implementasikan managed secret-manager ADR-010.

Jangan implementasikan distributed lock.

Jangan implementasikan retry/DLQ.

Jangan implementasikan event/outbox.

Jangan implementasikan multi-bot multiplexing.

Jangan menyentuh Gorouter.app.

NVIDIA dan TokenHarbor tidak perlu disentuh.

==================================================
BAGIAN 1 — AUDIT EXISTING CONTRACT
==================================================

Audit terlebih dahulu:

- enabled-module persistence contract dari B-051,
- PostgreSQL enabled-module adapter,
- module runtime,
- module registry,
- module context,
- workspace authorization,
- existing API architecture,
- existing route/use-case/service pattern,
- composition root,
- existing error semantics,
- existing request/response conventions.

Cari secara spesifik:

1. Contract repository enabled-module.
2. Method yang sudah tersedia.
3. Apakah write operation sudah tersedia.
4. Apakah write operation perlu diperluas atau sebenarnya sudah
   cukup dan hanya belum dipakai oleh use-case.
5. Bagaimana workspace identity diteruskan ke application layer.
6. Bagaimana authorization dilakukan oleh API existing.
7. Bagaimana use-case/service existing melakukan validation.
8. Bagaimana route existing memetakan error menjadi HTTP response.
9. Bagaimana module identifier divalidasi.
10. Bagaimana module runtime membaca enabled state.

JANGAN coding sebelum dependency existing dipahami.

==================================================
BAGIAN 2 — ENABLE/DISABLE USE-CASE
==================================================

Implementasikan application use-case untuk:

- enable module,
- disable module.

Gunakan repository contract B-051.

Use-case harus:

1. menerima workspace/installation context sesuai boundary
   repository existing,
2. memvalidasi module identifier menggunakan rule existing,
3. memastikan module memang dikenal oleh module registry/definition
   yang tersedia,
4. memeriksa authorization sesuai workspace boundary,
5. menyimpan enabled state melalui repository,
6. disable module melalui repository,
7. menghasilkan result/error yang konsisten dengan application
   architecture.

Jangan memasukkan SQL ke use-case.

Jangan memasukkan HTTP logic ke use-case.

Jangan memasukkan PostgreSQL dependency langsung ke use-case.

==================================================
BAGIAN 3 — ENABLE BEHAVIOR
==================================================

Enable module harus bersifat idempotent jika repository contract
memang mendukung semantics tersebut.

Contoh:

enable module A
→ enabled

enable module A lagi
→ jangan menghasilkan duplicate state.

Gunakan constraint/repository behavior existing.

Jangan membuat duplicate-prevention logic yang bertentangan
dengan database semantics.

Jika existing contract menetapkan duplicate sebagai error:

→ ikuti contract tersebut.

Jangan mengubah contract hanya agar test menjadi PASS.

==================================================
BAGIAN 4 — DISABLE BEHAVIOR
==================================================

Disable module harus benar-benar mengubah state persistence.

Setelah disable:

listEnabled
→ module tidak lagi dianggap enabled.

Module runtime yang membaca enabled state harus dapat melihat
state terbaru pada lifecycle berikutnya.

Jangan membuat runtime hot-reload/event system pada tahap ini.

Tidak perlu websocket.

Tidak perlu outbox.

Tidak perlu event bus.

Tidak perlu background worker tambahan.

==================================================
BAGIAN 5 — MODULE VALIDATION
==================================================

Sebelum enable:

module identifier harus diverifikasi terhadap module definition/
registry yang memang sudah tersedia.

Jika module tidak dikenal:

→ reject dengan error application yang sesuai.

Jangan membuat module definition baru hanya untuk membuat
test enable berhasil.

Jika repository belum mempunyai production module definitions:

→ gunakan registry/contract existing yang memang tersedia.

Jika B-052 membutuhkan module-definition contract yang belum ada:

→ audit terlebih dahulu.

Jika dependency tersebut memang internal dan kecil:

→ implementasikan hanya contract minimum yang benar-benar
dibutuhkan.

Jika membutuhkan keputusan product/business:

→ tandai deferred.

Jangan menebak module list.

==================================================
BAGIAN 6 — WORKSPACE / INSTALLATION ISOLATION
==================================================

WAJIB memastikan isolation.

Workspace A:

enable module X

Workspace B:

tidak boleh melihat module X sebagai enabled.

Test minimal:

1. enable pada workspace A.
2. query/list workspace A.
3. query/list workspace B.
4. pastikan state tidak bocor.

Jika boundary sebenarnya installation-scoped:

gunakan installation identity yang benar.

Jangan mengubah scope hanya demi implementasi lebih mudah.

==================================================
BAGIAN 7 — API CONTRACT
==================================================

Tambahkan API-side contract sesuai pola API repository existing.

Minimal behavior:

- enable module,
- disable module.

Gunakan HTTP semantics existing.

Jangan membuat endpoint baru dengan path arbitrary jika repository
sudah mempunyai route convention.

Audit route naming terlebih dahulu.

Request minimal harus menggunakan identifier yang memang
diperlukan oleh contract.

Jangan menambahkan:

- quota,
- pricing,
- scheduler,
- module configuration,
- secrets,
- credentials,
- runtime process state.

Response harus konsisten dengan API conventions existing.

Jangan expose database row mentah jika architecture existing
menggunakan DTO/application result.

==================================================
BAGIAN 8 — AUTHORIZATION
==================================================

Route/use-case harus menghormati workspace authorization.

User/workspace yang tidak memiliki akses:

→ reject.

Jangan mempercayai workspace ID dari request body jika
authentication/request context existing menyediakan workspace
identity yang authoritative.

Gunakan identity dari authorization context sesuai architecture.

Jangan memungkinkan:

workspace A user
→ mengaktifkan module pada workspace B.

==================================================
BAGIAN 9 — ERROR SEMANTICS
==================================================

Gunakan error type existing.

Tangani minimal:

- invalid module identifier,
- unknown module,
- unauthorized workspace,
- module already enabled jika contract menganggapnya error,
- module already disabled jika contract menganggapnya error,
- persistence failure.

Jangan membuat hierarchy error baru jika repository sudah memiliki
standard application errors.

Error response tidak boleh membocorkan:

- SQL,
- database URL,
- credentials,
- secrets,
- internal stack trace.

==================================================
BAGIAN 10 — COMPOSITION ROOT
==================================================

Wire use-case ke composition root existing.

Target:

API
 ↓
UseCase
 ↓
EnabledModuleRepository
 ↓
PostgreSQL Adapter

Pastikan production composition menggunakan dependency nyata.

Test composition boleh menggunakan fake repository.

Jangan membuat global singleton tersembunyi.

Jangan bypass dependency injection.

==================================================
BAGIAN 11 — RUNTIME COMPATIBILITY
==================================================

Pastikan B-052 tidak merusak B-050.

Module runtime tetap membaca enabled-module state melalui
dependency yang sudah ada.

Jangan membuat runtime baru.

Jangan menambahkan hot reload.

Jangan menambahkan event-driven synchronization.

Jangan mengubah lifecycle worker.

B-052 hanya menyediakan persistence-backed control path.

==================================================
BAGIAN 12 — TEST
==================================================

Tambahkan test yang benar-benar memverifikasi:

### Use-case

1. enable module berhasil.
2. disable module berhasil.
3. enable module unknown ditolak.
4. invalid module identifier ditolak.
5. persistence failure diteruskan secara aman.
6. duplicate behavior sesuai contract.
7. disabled state benar-benar tersimpan.

### Authorization

8. workspace A dapat enable module miliknya.
9. workspace B tidak dapat mengubah state workspace A.
10. cross-workspace lookup tidak bocor.

### API

11. request validation.
12. authorization.
13. success response.
14. invalid module response.
15. persistence failure response.
16. error mapping sesuai convention existing.

### Runtime compatibility

17. listEnabled setelah enable mengembalikan module.
18. listEnabled setelah disable tidak mengembalikan module.
19. module runtime tetap menggunakan repository injection existing.

Jangan membuat fake schema hanya agar test PASS.

==================================================
BAGIAN 13 — POSTGRESQL INTEGRATION
==================================================

Jika environment menyediakan:

PERSISTENCE_TEST_DATABASE_URL

jalankan integration test B-051/B-052 yang relevan.

Verifikasi:

- enable,
- disable,
- list,
- isolation,
- duplicate behavior,
- persistence consistency.

Jika environment tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan:

- membuat PostgreSQL palsu,
- menggunakan SQLite,
- membuat database sementara tanpa dasar,
- mengubah test agar PASS.

==================================================
BAGIAN 14 — SECURITY REVIEW
==================================================

Review:

- authorization context,
- workspace isolation,
- module identifier validation,
- SQL parameterization,
- error sanitization,
- logging.

Pastikan tidak ada:

- secret di log,
- credential di response,
- SQL injection,
- cross-workspace mutation,
- raw database error ke client.

==================================================
BAGIAN 15 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script tersebut.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jika PostgreSQL environment tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan menyamarkan SKIPPED sebagai PASS.

==================================================
BAGIAN 16 — DIFF REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan perubahan hanya berkaitan dengan:

- B-052 enable/disable use-case,
- API contract/route,
- repository wiring bila diperlukan,
- tests,
- dokumentasi yang relevan.

Hapus:

- debug code,
- temporary files,
- generated files,
- unrelated refactor.

==================================================
BAGIAN 17 — COMMIT
==================================================

Jika implementasi valid dan validation selesai:

buat SATU commit.

Gunakan:

feat: add module enable disable use-case

atau commit message yang lebih tepat berdasarkan perubahan
aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 18 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote SHA.

Target:

local SHA == remote SHA
working tree == CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah credential GitHub sembarangan,
- tampilkan error dengan jelas.

==================================================
FINAL OUTPUT
==================================================

### B-052 STATUS

Use-case:
Enable:
Disable:
API Contract:
Authorization:
Workspace Isolation:
Runtime Compatibility:

### TEST

Unit:
API:
Integration:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata
repository.

Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace


```
# Prompt: B-051 — Enabled-Module Persistence Adapter
```


Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-030 — Workspace API/Contract:
SELESAI.

B-070 — Storage Adapter:
SELESAI.

B-071 — File/Share:
SELESAI.

B-040 s/d B-049 — worker/runtime foundation:
SELESAI.

B-050 — Module Runtime Composition:
SELESAI.

B-050 berhasil membuat module runtime composition nyata
yang digunakan worker.

Validation terakhir:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push berhasil.

==================================================
NEXT ROADMAP
==================================================

B-051 — enabled-module persistence adapter.

Tujuan B-051:

Hubungkan enabled-module persistence dengan PostgreSQL
persistence adapter yang SUDAH ADA sehingga module runtime
tidak lagi hanya menerima enabled modules melalui fake/injected
repository pada production composition.

B-051 harus tetap berada pada boundary persistence.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-030
- B-070
- B-071
- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-047
- B-048
- B-049
- B-050

Jangan membuat module runtime kedua.

Jangan membuat worker runtime kedua.

Jangan membuat persistence abstraction kedua.

Jangan membuat PostgreSQL adapter kedua jika adapter existing
sudah dapat diperluas.

Jangan membuat schema speculative.

Jangan membuat migration tanpa dasar contract/repository.

Jangan mengimplementasikan managed secret-manager ADR-010.

Jangan mengimplementasikan real Telegram integration.

Jangan membuat distributed lock.

Jangan membuat retry/DLQ.

Jangan membuat event/outbox infrastructure.

Jangan membuat multi-bot multiplexing.

Jangan mengubah BotInstallation.status.

Jangan menyentuh Gorouter.app.

NVIDIA dan TokenHarbor tidak perlu disentuh.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Audit terlebih dahulu:

- B-050 module runtime composition
- enabled-module repository/port
- module registry
- module context
- module runtime
- WorkerPersistenceResource
- PostgreSQL persistence adapter
- workspace/installation persistence
- existing migration system
- existing schema
- existing repository patterns
- production composition root
- worker bootstrap.

Cari secara spesifik:

1. Interface/port enabled-module persistence yang sudah ada.
2. Apakah repository enabled-module sudah ada.
3. Apakah PostgreSQL adapter sudah mempunyai connection/query
   infrastructure yang dapat digunakan.
4. Apakah schema enabled modules sudah tersedia.
5. Apakah migration untuk enabled modules sudah tersedia.
6. Apakah enabled modules harus scoped berdasarkan:
   - workspace,
   - installation,
   - atau kombinasi keduanya.
7. Bagaimana B-050 sekarang mendapatkan enabled modules.
8. Apakah B-050 masih menggunakan fake/in-memory repository
   hanya karena production persistence belum tersedia.
9. Apakah WorkerPersistenceResource sudah menjadi dependency
   injection boundary resmi.

JANGAN coding sebelum dependency existing dipahami.

==================================================
BAGIAN 2 — CONTRACT BOUNDARY
==================================================

Gunakan contract/port enabled-module yang SUDAH ADA.

Jika sudah ada:

EnabledModuleRepository / EnabledModulePersistencePort
atau equivalent:

→ implementasikan adapter untuk contract tersebut.

Jangan membuat contract kedua.

Jika contract belum ada:

→ buat contract minimum hanya jika memang diperlukan oleh
arsitektur existing.

Contract harus tetap sederhana dan persistence-oriented.

Jangan memasukkan business logic ke repository.

==================================================
BAGIAN 3 — POSTGRESQL ADAPTER
==================================================

Implementasikan PostgreSQL adapter untuk enabled-module
persistence menggunakan PostgreSQL infrastructure yang sudah
ada.

Adapter harus mengikuti pola repository PostgreSQL existing.

Minimal behavior sesuai contract yang benar-benar tersedia:

- list enabled modules,
- lookup enabled module,
- enable module,
- disable module,

HANYA implementasikan operasi yang memang didukung contract.

Jangan menambahkan CRUD tambahan secara otomatis.

Pastikan workspace/installation isolation.

Tidak boleh:

workspace A
→ membaca enabled module workspace B.

Jika scope sebenarnya installation-specific:

→ gunakan installation identity yang benar.

Jangan menebak scope.

Tentukan berdasarkan model/contract repository existing.

==================================================
BAGIAN 4 — SCHEMA / MIGRATION
==================================================

Audit schema terlebih dahulu.

Jika schema enabled-module SUDAH ADA:

→ gunakan schema tersebut.

Jika migration memang belum ada tetapi contract B-051
secara eksplisit membutuhkan persistence table:

→ buat migration minimum yang sesuai dengan model/contract
yang sudah ada.

Jangan menambahkan field spekulatif.

Minimal data harus mendukung identity yang memang diperlukan
untuk isolation, misalnya:

- workspace/installation identity,
- module identifier,
- enabled state,

tetapi gunakan nama/struktur yang sesuai dengan model
repository sebenarnya.

Jangan membuat:

- expiry,
- scheduler,
- event table,
- audit table,
- lock table,
- retry table.

==================================================
BAGIAN 5 — CONSTRAINT DAN INTEGRITY
==================================================

Pastikan persistence mencegah duplicate enabled-module state
sesuai scope contract.

Contoh prinsip:

scope + module identifier

harus deterministic.

Jika database architecture existing mendukung unique
constraint:

→ gunakan constraint tersebut.

Jangan mengandalkan application-level duplicate prevention saja
jika database schema memang merupakan source of truth.

Jangan menambahkan constraint yang tidak sesuai dengan model
existing.

==================================================
BAGIAN 6 — MODULE RUNTIME INTEGRATION
==================================================

Hubungkan adapter persistence ke B-050 module runtime composition.

Target architecture:

worker
 ↓
startWorkerRoot
 ↓
WorkerPersistenceResource
 ↓
EnabledModuleRepository
 ↓
ModuleRuntime
 ↓
ModuleRegistry
 ↓
ModuleHandler

Pastikan production composition menggunakan adapter nyata.

Test environment tetap dapat menggunakan fake/in-memory
repository melalui dependency injection.

Jangan membuat global singleton.

Jangan bypass composition root.

==================================================
BAGIAN 7 — WORKSPACE / INSTALLATION ISOLATION
==================================================

Ini wajib diuji.

Pastikan:

workspace A:
- hanya melihat enabled modules miliknya.

workspace B:
- hanya melihat enabled modules miliknya.

Jika installation menjadi boundary:

installation A:
- tidak dapat membaca installation B.

Test harus membuktikan cross-scope lookup gagal atau tidak
mengembalikan data.

Jangan hanya test happy path.

==================================================
BAGIAN 8 — ERROR HANDLING
==================================================

Gunakan error semantics persistence yang sudah ada.

Tangani:

- module tidak ditemukan,
- duplicate state,
- invalid module identifier,
- persistence failure,
- missing workspace/installation context.

Jangan bocorkan:

- SQL,
- connection string,
- password,
- credential,
- secret,
- internal database details.

Jangan membuat error framework baru.

==================================================
BAGIAN 9 — TRANSACTION
==================================================

Jika enable/disable membutuhkan transaction berdasarkan
existing persistence architecture:

→ gunakan transaction abstraction yang sudah tersedia.

Jangan membuat transaction abstraction kedua.

Jika operasi sederhana tidak membutuhkan transaction:

→ jangan menambahkan transaction hanya demi terlihat lebih
production-ready.

==================================================
BAGIAN 10 — TEST
==================================================

Tambahkan test yang benar-benar memverifikasi:

1. enabled module dapat disimpan.
2. enabled module dapat dibaca.
3. enable/disable behavior.
4. duplicate behavior.
5. module lookup.
6. workspace isolation.
7. installation isolation jika memang menjadi scope.
8. invalid module identifier.
9. persistence failure.
10. module runtime menggunakan repository yang di-inject.
11. production composition membuat dependency graph yang benar.
12. fake/in-memory repository tetap dapat digunakan oleh test.

Jika PostgreSQL integration test tersedia dan membutuhkan:

PERSISTENCE_TEST_DATABASE_URL

maka:

- gunakan database test tersebut,
- jalankan migration yang sesuai,
- jalankan integration test.

Jika environment tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan:

- membuat PostgreSQL palsu,
- mengganti dengan SQLite,
- mengubah test supaya PASS,
- memasukkan credential database ke source.

==================================================
BAGIAN 11 — REAL PRODUCTION READINESS
==================================================

Production composition harus menggunakan PostgreSQL adapter
nyata hanya jika configuration/infrastructure memang tersedia
di architecture.

Jangan menganggap database tersedia jika environment belum
menyediakannya.

Jika production DB belum tersedia:

→ adapter tetap harus benar,
→ composition boundary harus benar,
→ integration test dapat tetap deferred.

Jangan membuat fake production persistence.

==================================================
BAGIAN 12 — SECURITY REVIEW
==================================================

Review:

- workspace isolation,
- installation isolation,
- module identifier validation,
- SQL parameterization,
- credential handling,
- error sanitization,
- logging.

Pastikan query menggunakan parameterized query / existing
safe database API.

Tidak boleh ada:

- SQL interpolation dari user input,
- credential di log,
- connection string di error,
- secret di test output.

==================================================
BAGIAN 13 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script tersebut.

Jika memang tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jika PostgreSQL integration membutuhkan environment dan tidak
tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan menyamarkan SKIPPED menjadi PASS.

==================================================
BAGIAN 14 — DIFF REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan perubahan hanya berkaitan dengan:

- enabled-module persistence,
- PostgreSQL adapter,
- migration/schema jika benar-benar diperlukan,
- B-050 production wiring,
- tests,
- dokumentasi yang relevan.

Hapus:

- debug code,
- temporary files,
- generated files,
- unrelated refactor.

==================================================
BAGIAN 15 — COMMIT
==================================================

Jika implementasi valid:

Buat SATU commit.

Gunakan:

feat: add enabled module persistence adapter

atau commit message yang lebih tepat berdasarkan perubahan
aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 16 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote SHA.

Target:

local SHA == remote SHA
working tree == CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error dengan jelas.

==================================================
FINAL OUTPUT
==================================================

### B-051 STATUS

Contract:
Schema/Migration:
PostgreSQL Adapter:
Enabled Module Repository:
B-050 Integration:
Workspace/Installation Isolation:

### TEST

Unit:
Integration:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar masih belum
tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata
repository.

Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace
```
# Prompt: B-050 — Module Runtime Composition
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-040 — Account Session Connection:
SELESAI.

B-041 — Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 — Runtime Execution:
SELESAI.

B-043 — Real Telegram Runtime Driver:
SELESAI.

B-044 — Telegram SDK-backed TelegramClientFactory:
SELESAI.

B-045 — Production Worker Bootstrap + Update Routing:
SELESAI.

B-046 — Persistence-backed Installation Discovery +
Worker Credential Wiring:
SELESAI.

B-047 — Production Composition Root:
SELESAI.

B-048 — Deployment Adapter + Operational Readiness:
SELESAI.

B-049 — Worker Process Entrypoint Finalization +
Deployment Runbook:
SELESAI.

Validation terakhir:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push berhasil.

==================================================
ROADMAP TERAKHIR
==================================================

B-049 menyatakan dua dependency nyata masih memblokir
direct-run production penuh:

1. ADR-010 managed secret-manager:
   masih menunggu keputusan/vendor infrastructure.

2. Infrastructure eksternal:
   PostgreSQL integration environment,
   real Telegram credential/environment,
   distributed coordination/lock,
   retry/DLQ,
   outbox/event infrastructure.

JANGAN mencoba menyelesaikan dependency tersebut secara
speculative.

Roadmap berikutnya yang direkomendasikan:

B-050 — module runtime composition.

B-050 dapat dikerjakan sekarang karena dependency internal
untuk module runtime sudah tersedia.

==================================================
TARGET B-050
==================================================

Implementasikan module runtime composition yang membuat
worker runtime memiliki module runtime nyata.

Target architecture:

worker process
    ↓
startWorkerRoot
    ↓
load/create module runtime
    ↓
module registry
    ↓
module context resolver
    ↓
enabled-module repository
    ↓
module handlers
    ↓
runWorkerProcess

Tujuan utama:

`runWorkerProcess` tidak lagi berhenti pada runtime shell/
composition placeholder.

Worker harus mempunyai module runtime composition yang nyata
menggunakan abstraction yang SUDAH tersedia di repository.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-047
- B-048
- B-049

Jangan membuat runtime kedua.

Jangan membuat worker bootstrap kedua.

Jangan membuat Telegram driver kedua.

Jangan membuat persistence abstraction kedua.

Jangan membuat SecretResolver kedua.

Jangan membuat HTTP framework baru.

Jangan membuat queue.

Jangan membuat retry/DLQ.

Jangan membuat distributed lock.

Jangan membuat outbox.

Jangan membuat multi-bot multiplexing.

Jangan membuat managed secret-manager vendor secara speculative.

Gunakan architecture dan abstraction yang sudah ada.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Audit terlebih dahulu:

- `runWorkerProcess`
- `startWorkerRoot`
- worker runtime package
- module runtime package
- module registry
- module context
- context resolver
- enabled-module repository
- module handler interfaces
- module lifecycle
- installation/workspace context
- existing module implementations
- composition root
- worker entrypoint
- existing tests.

Cari secara khusus:

1. Apakah module registry sudah ada?
2. Apakah module handler contract sudah ada?
3. Apakah context resolver sudah ada?
4. Apakah enabled-module repository sudah ada?
5. Apakah module runtime sudah memiliki interface/factory?
6. Apakah `runWorkerProcess` sekarang menerima module runtime?
7. Bagian mana yang masih placeholder/no-op?
8. Apakah B-061 sudah menjadi dependency nyata?

Jangan langsung coding sebelum dependency internal tersebut
dipahami.

==================================================
BAGIAN 2 — MODULE RUNTIME COMPOSITION
==================================================

Buat composition yang menghubungkan:

module registry
+
context resolver
+
enabled-module repository
+
module handlers

menjadi module runtime yang dapat digunakan worker.

Gunakan interface yang SUDAH ADA.

Jika factory/composition abstraction sudah tersedia:

→ gunakan abstraction tersebut.

Jika belum ada tetapi memang dibutuhkan untuk composition:

→ buat abstraction minimum pada boundary yang tepat.

Jangan membuat abstraction kedua yang duplikatif.

==================================================
BAGIAN 3 — MODULE REGISTRY
==================================================

Audit module registry.

Registry harus menjadi source of truth untuk module yang
tersedia di runtime.

Pastikan:

- module identifier deterministic,
- module registration tidak duplicate,
- handler mapping jelas,
- module lookup memiliki error yang aman,
- module tidak dapat mengambil handler module lain secara
  tidak sengaja.

Jika registry contract belum cukup:

→ identifikasi dependency yang benar-benar diperlukan.

Jika dependency tersebut adalah B-061:

→ jangan mengarang B-061.

Implementasikan hanya composition yang dapat dilakukan
berdasarkan contract existing.

==================================================
BAGIAN 4 — ENABLED MODULE
==================================================

Gunakan enabled-module repository yang sudah ada.

Worker runtime harus dapat menentukan module mana yang aktif
untuk workspace/installation berdasarkan repository tersebut.

Rules:

- jangan hardcode enabled module,
- jangan bypass repository,
- jangan menganggap semua module selalu enabled,
- jangan mengubah persistence schema hanya untuk B-050,
- jangan membuat fake repository production.

Jika repository membutuhkan persistence environment nyata:

→ gunakan abstraction existing.

Jangan membuat PostgreSQL test palsu.

==================================================
BAGIAN 5 — MODULE CONTEXT
==================================================

Pastikan setiap module handler mendapatkan context yang benar.

Context minimal hanya berdasarkan abstraction existing.

Audit apakah context berisi:

- workspace identity,
- installation identity,
- bot identity,
- provider/session context,
- configuration,
- logger,
- dependencies yang memang dibutuhkan.

Jangan memasukkan credential mentah ke module context jika
tidak diperlukan.

Jangan memasukkan secret manager credential ke context.

Workspace/installation boundary harus tetap dipertahankan.

==================================================
BAGIAN 6 — CONTEXT RESOLVER
==================================================

Integrasikan context resolver yang sudah ada.

Resolver harus:

1. resolve context berdasarkan runtime identity,
2. menghormati workspace boundary,
3. tidak mengambil context lintas workspace,
4. gagal secara aman ketika context tidak ditemukan,
5. tidak membocorkan credential/secret,
6. tidak membuat global mutable context.

Jika context resolver sudah production-ready:

→ jangan refactor tanpa alasan.

==================================================
BAGIAN 7 — MODULE HANDLER DISPATCH
==================================================

Hubungkan module runtime ke handler dispatch yang sudah ada.

Target:

incoming runtime event
    ↓
resolve installation/workspace context
    ↓
determine enabled modules
    ↓
lookup registered module
    ↓
resolve handler
    ↓
execute handler
    ↓
return outcome

Jangan membuat event system baru.

Gunakan event/update abstraction yang sudah tersedia dari
B-045 dan runtime sebelumnya.

Jika event dispatch contract belum tersedia:

→ jangan membuat event bus speculative.

Implementasikan hanya composition boundary yang tersedia.

==================================================
BAGIAN 8 — FAILURE ISOLATION
==================================================

Pastikan kegagalan satu module tidak merusak composition
runtime secara global jika existing architecture memang
mendukung isolation.

Contoh:

module A gagal
→ module B tidak otomatis kehilangan registry/context.

Namun jangan membuat error isolation framework baru jika
runtime existing sudah memiliki policy.

Gunakan error semantics existing.

==================================================
BAGIAN 9 — LIFECYCLE
==================================================

Module runtime harus mengikuti lifecycle worker yang sudah
tersedia.

Target:

worker start
→ module runtime initialized
→ registry ready
→ context dependencies ready
→ worker process running

shutdown:
→ worker runtime shutdown
→ module runtime cleanup jika abstraction tersedia.

Jangan membuat lifecycle framework kedua.

Jika module handler tidak memiliki lifecycle:

→ jangan menambahkan lifecycle method hanya untuk memenuhi
target B-050.

==================================================
BAGIAN 10 — PRODUCTION VS TEST
==================================================

Production composition:

gunakan dependency nyata yang sudah tersedia.

Test composition:

gunakan injected fake/in-memory implementation yang memang
sudah menjadi pattern repository.

Jangan membuat production fake.

Jangan memasukkan Telegram credential nyata ke test.

Jangan memasukkan database credential nyata ke source.

==================================================
BAGIAN 11 — B-061 BOUNDARY
==================================================

Audit B-061 secara khusus.

Jika B-061 hanya merupakan contract/module registry +
handler contract yang memang SUDAH tersedia sebagian:

→ gunakan yang sudah ada.

Jika B-061 merupakan dependency yang BELUM tersedia:

→ jangan mengimplementasikan seluruh B-061 sekarang.

Tentukan minimum contract yang benar-benar dibutuhkan B-050.

Jangan membuat speculative API.

==================================================
BAGIAN 12 — TEST
==================================================

Tambahkan test untuk behavior baru yang benar-benar
diimplementasikan.

Minimal:

1. module registry composition.
2. duplicate module registration ditolak jika contract
   mendukung behavior tersebut.
3. enabled module resolution.
4. context resolver integration.
5. workspace isolation.
6. handler lookup.
7. handler dispatch.
8. missing module behavior.
9. missing context behavior.
10. module runtime startup.
11. module runtime failure behavior.
12. worker → module runtime integration.

Jangan membuat mock hanya untuk mendapatkan PASS.

Gunakan fake/in-memory implementation existing jika tersedia.

==================================================
BAGIAN 13 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut memang tidak tersedia.

Jika PostgreSQL integration membutuhkan:

PERSISTENCE_TEST_DATABASE_URL

dan variable tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat database palsu.

Real Telegram integration:

SKIPPED/DEFERRED — credential/test environment unavailable

Jangan membuat credential palsu.

==================================================
BAGIAN 14 — SECURITY REVIEW
==================================================

Review perubahan B-050 untuk:

- workspace isolation,
- installation isolation,
- module authorization,
- context leakage,
- secret leakage,
- credential logging,
- cross-workspace access,
- handler lookup,
- invalid module identifier,
- error sanitization.

Pastikan tidak ada secret/token/password masuk ke:

- log,
- error response,
- module context yang tidak diperlukan,
- test snapshot.

==================================================
BAGIAN 15 — DIFF REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan perubahan hanya terkait:

- module runtime composition,
- registry/context wiring jika memang diperlukan,
- enabled module resolution,
- handler dispatch,
- test,
- dokumentasi bila memang diperlukan.

Hapus:

- debug code,
- temporary files,
- generated junk,
- unrelated refactor.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA,
- TokenHarbor,
- B-071,
- SecretResolver vendor implementation,
- deployment infrastructure.

==================================================
BAGIAN 16 — COMMIT
==================================================

Jika implementasi valid dan validation selesai:

Buat SATU commit.

Gunakan:

feat: implement module runtime composition

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 17 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD
git status

Jika memungkinkan, verifikasi remote SHA juga.

Target:

local SHA == remote SHA
working tree == CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error secara jelas.

==================================================
FINAL OUTPUT
==================================================

### B-050 STATUS

Module registry:
Module context:
Enabled modules:
Handler dispatch:
Worker integration:
Lifecycle:

### TEST

Unit:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### INTEGRATION

PostgreSQL:
Real Telegram:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency yang benar-benar belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata
repository.

PENTING:

Jangan mengerjakan fitur acak.

Jangan mengulang B-049.

Jangan mengimplementasikan vendor secret-manager.

Jangan membuat infrastructure speculative.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-049 — Worker Process Entrypoint Finalization + Deployment Runbook
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-040 — Account Session Connection:
SELESAI.

B-041 — Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 — Runtime Execution:
SELESAI.

B-043 — Real Telegram Runtime Driver:
SELESAI.

B-044 — Real Telegram SDK-backed TelegramClientFactory:
SELESAI.

B-045 — Production Worker Bootstrap + Update Routing:
SELESAI.

B-046 — Persistence-backed Installation Discovery +
Worker Credential Wiring:
SELESAI.

B-047 — Production Composition Root:
SELESAI.

B-048 — Deployment Adapter + Operational Readiness:
SELESAI.

Validation terakhir:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push berhasil.

==================================================
REMAINING DEFERRED
==================================================

1. Managed secret-manager client nyata belum tersedia.
2. Direct-run production deployment input masih perlu dirapikan.
3. PostgreSQL integration membutuhkan:
   PERSISTENCE_TEST_DATABASE_URL
4. Real Telegram integration membutuhkan credential/test environment.
5. Distributed multi-worker coordination/lock belum tersedia.
6. Update retry/DLQ contract belum tersedia.
7. Event/outbox runtime lifecycle infrastructure belum tersedia.
8. Multi-bot multiplexing pada satu connection tetap out of scope.

Jangan mencoba menyelesaikan dependency tersebut secara speculative.

==================================================
TARGET B-049
==================================================

B-049 — worker process entrypoint finalization +
deployment runbook.

Tujuan:

Membuat entrypoint worker production menjadi jalur resmi
untuk menjalankan worker runtime yang SUDAH tersedia.

Target:

environment/config
    ↓
loadConfigFromEnv
    ↓
createPostgresPersistence
    ↓
SecretResolver boundary
    ↓
startWorkerRoot
    ↓
existing worker runtime

Deployment runbook harus menjelaskan cara menjalankan
worker production tanpa membuat architecture baru.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-047
- B-048

Jangan membuat:

- worker runtime kedua,
- Telegram driver kedua,
- persistence abstraction kedua,
- SecretResolver kedua,
- composition root kedua,
- queue baru,
- retry system,
- DLQ,
- distributed lock,
- outbox system,
- multi-bot multiplexing.

Gunakan implementation yang SUDAH ADA.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Audit:

- worker package,
- worker entrypoint yang sudah ada,
- startWorkerRoot,
- loadConfigFromEnv,
- createPostgresPersistence,
- SecretResolver,
- WorkerPersistenceResource,
- existing runtime composition,
- package scripts,
- Dockerfile jika tersedia,
- deployment files,
- README/deployment documentation.

Tentukan:

1. Entry point worker production yang paling tepat.
2. Apakah entrypoint sudah ada tetapi belum final.
3. Function/API yang harus dipanggil.
4. Configuration yang wajib tersedia.
5. Lifecycle startup/shutdown yang sudah disediakan.
6. Dokumentasi deployment yang sudah ada dan perlu diperbarui.

Jangan melakukan full repository rewrite.

==================================================
BAGIAN 2 — WORKER PROCESS ENTRYPOINT
==================================================

Finalisasikan worker process entrypoint.

Entrypoint harus:

1. Load configuration melalui configuration mechanism yang sudah ada.
2. Validasi configuration sebelum runtime dimulai.
3. Membuat persistence melalui createPostgresPersistence().
4. Menggunakan SecretResolver boundary yang sudah ada.
5. Memanggil startWorkerRoot() atau composition API resmi yang
   sudah tersedia.
6. Menjaga workspace scope sesuai configuration.
7. Menangani startup failure dengan exit status yang benar.
8. Menangani SIGTERM/SIGINT jika lifecycle abstraction sudah
   mendukungnya.
9. Menjalankan graceful shutdown menggunakan lifecycle yang
   sudah ada.
10. Tidak membuka koneksi database secara manual jika
    persistence factory sudah menangani lifecycle.
11. Tidak membuat Telegram polling/webhook baru.

Jangan membuat duplicate bootstrap.

==================================================
BAGIAN 3 — CONFIGURATION
==================================================

Gunakan configuration API yang SUDAH ADA.

Configuration minimal yang diperlukan hanya berdasarkan
implementation repository.

Kemungkinan termasuk:

DATABASE_URL
WORKER_WORKSPACE_SCOPE
SECRET_MANAGER_REF

Tetapi JANGAN menganggap semua variable tersebut wajib jika
kode existing menentukan behavior berbeda.

Audit source of truth terlebih dahulu.

Rules:

- tidak hardcode credential,
- tidak hardcode database URL,
- tidak hardcode Telegram token,
- tidak mencetak secret,
- error harus sanitized,
- missing required configuration harus fail fast.

==================================================
BAGIAN 4 — PROCESS LIFECYCLE
==================================================

Pastikan worker process memiliki lifecycle production yang jelas:

START
→ load configuration
→ validate
→ create dependencies
→ start worker
→ remain running

SHUTDOWN
→ receive termination signal
→ stop worker runtime
→ cleanup persistence/resources
→ exit cleanly

Gunakan lifecycle abstraction yang sudah ada.

Jangan membuat shutdown framework baru.

Jika runtime memang belum memiliki signal/shutdown abstraction
yang cukup:

→ implementasikan perubahan minimum hanya untuk entrypoint.

Jangan melakukan refactor runtime besar.

==================================================
BAGIAN 5 — ERROR HANDLING
==================================================

Pastikan process failure dapat didiagnosis tanpa membocorkan:

- password,
- API key,
- Telegram token,
- database credential,
- secret.

Error startup harus menjelaskan kategori masalah.

Contoh:

"Worker configuration is invalid"

atau

"Worker persistence initialization failed"

Bukan menampilkan nilai credential.

Pastikan process exit non-zero ketika startup gagal.

==================================================
BAGIAN 6 — PACKAGE SCRIPT
==================================================

Audit package.json.

Jika architecture repository menggunakan script khusus worker,
pastikan ada command production yang jelas.

Contoh pola:

pnpm worker

atau script existing yang lebih tepat.

JANGAN menambahkan banyak command duplikat.

Pilih SATU entrypoint resmi untuk production worker berdasarkan
struktur repository.

Jika command sudah ada:

→ gunakan dan rapikan bila perlu.

==================================================
BAGIAN 7 — DEPLOYMENT RUNBOOK
==================================================

Perbarui dokumentasi deployment yang SUDAH ADA.

Jangan membuat banyak README baru.

Gunakan README.md/documentasi deployment existing.

Dokumentasikan:

1. prerequisite production,
2. environment variables,
3. cara install dependency,
4. cara build,
5. cara menjalankan worker,
6. cara menjalankan worker sebagai process/service jika
   repository memang menyediakan mekanismenya,
7. graceful restart,
8. log location/behavior,
9. health/readiness verification jika endpoint/command
   memang sudah tersedia,
10. troubleshooting startup failure.

Jangan mengarang:

- systemd service yang belum tersedia,
- Docker deployment yang belum digunakan,
- Kubernetes deployment,
- cloud-specific infrastructure.

Dokumentasikan hanya deployment mechanism yang benar-benar
didukung repository.

==================================================
BAGIAN 8 — DIRECT-RUN PRODUCTION
==================================================

Pastikan direct-run production path jelas.

Target:

configuration
→ persistence
→ worker runtime

Jangan membuat deployment-specific abstraction baru jika
existing composition root sudah dapat digunakan.

Jika production runbook membutuhkan build artifact:

→ gunakan build output existing.

Jika membutuhkan workspace scope:

→ dokumentasikan configuration existing.

==================================================
BAGIAN 9 — TEST
==================================================

Tambahkan test hanya untuk behavior yang benar-benar baru.

Minimal:

1. entrypoint configuration validation.
2. missing required configuration ditolak.
3. dependency composition berhasil.
4. worker startup failure menghasilkan failure yang benar.
5. shutdown lifecycle tidak meninggalkan resource.
6. secret tidak bocor ke error/log.

Jika entrypoint sulit ditest langsung karena process boundary:

→ extract hanya helper configuration/composition kecil
   menggunakan abstraction yang existing.

Jangan membuat duplicate runtime abstraction.

==================================================
BAGIAN 10 — REAL TELEGRAM
==================================================

Jangan menjalankan real Telegram integration jika credential
environment belum tersedia.

Jika credential tidak tersedia:

REAL TELEGRAM:
DEFERRED — credential/test environment unavailable

Jangan membuat fake production Telegram.

==================================================
BAGIAN 11 — POSTGRESQL
==================================================

Jika:

PERSISTENCE_TEST_DATABASE_URL

tersedia:

→ jalankan PostgreSQL integration test yang SUDAH ADA.

Jika tidak:

→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan:

- menggunakan SQLite,
- membuat fake PostgreSQL,
- mengubah test agar PASS.

==================================================
BAGIAN 12 — DEFERRED INFRASTRUCTURE
==================================================

Tetap deferred:

- managed secret-manager vendor integration,
- distributed lock,
- retry/DLQ,
- outbox,
- multi-worker coordination,
- multi-bot multiplexing.

Jangan membuat implementation speculative.

==================================================
BAGIAN 13 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut memang tidak tersedia.

Jika PostgreSQL environment tersedia:
→ jalankan integration test.

Jika tidak:
→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Real Telegram:
→ tetap deferred jika credential tidak tersedia.

==================================================
BAGIAN 14 — DIFF REVIEW
==================================================

Review:

git status
git diff --stat
git diff

Pastikan perubahan hanya:

- worker entrypoint,
- configuration wiring jika diperlukan,
- lifecycle wiring minimum,
- package script jika diperlukan,
- deployment documentation,
- test yang relevan.

Hapus:

- debug code,
- temporary files,
- generated files,
- unrelated refactor,
- duplicate abstraction.

==================================================
BAGIAN 15 — COMMIT
==================================================

Jika perubahan valid dan validation selesai:

Buat SATU commit.

Gunakan message:

feat: finalize worker process entrypoint

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 16 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

git status

Pastikan local SHA == remote SHA.

Working tree harus:

CLEAN

Jika push gagal:

- jangan reset,
- jangan hapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error secara jelas.

==================================================
DEFINITION OF DONE
==================================================

B-049 selesai jika:

- production worker entrypoint resmi tersedia,
- configuration loading benar,
- persistence composition benar,
- SecretResolver boundary tetap digunakan,
- workspace scope benar,
- startup failure aman,
- graceful shutdown benar,
- package command jelas,
- deployment runbook diperbarui,
- Unit PASS,
- Build PASS,
- Typecheck PASS,
- Lint PASS,
- Format PASS,
- Imports PASS,
- Ownership PASS,
- Docs PASS,
- Diff PASS,
- commit berhasil,
- push berhasil,
- local SHA == remote SHA,
- working tree CLEAN.

==================================================
FINAL OUTPUT
==================================================

### B-049 STATUS

Entrypoint:
Configuration:
Persistence:
SecretResolver:
Lifecycle:
Deployment runbook:

### TEST

Unit:
PostgreSQL:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata repository.

Jangan membuat fitur speculative.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-048 — Deployment Adapter + Operational Readiness
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-040 — Account Session Connection:
SELESAI.

B-041 — Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 — Runtime Execution:
SELESAI.

B-043 — Real Telegram Runtime Driver:
SELESAI.

B-044 — Real Telegram SDK-backed TelegramClientFactory:
SELESAI.

B-045 — Production Worker Bootstrap + Update Routing:
SELESAI.

B-046 — Persistence-backed Installation Discovery +
Worker Credential Wiring:
SELESAI.

B-047 — Production Composition Root:
SELESAI.

Validation terakhir B-047:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push: berhasil

==================================================
REMAINING DEFERRED TERAKHIR
==================================================

1. Managed secret-manager client nyata belum tersedia.
   SecretResolver boundary sudah tersedia.

2. Deployment adapter untuk production PostgreSQL persistence
   belum dibuat.

3. PostgreSQL integration test masih membutuhkan:
   PERSISTENCE_TEST_DATABASE_URL

4. Real Telegram integration masih membutuhkan:
   credential/test environment nyata.

5. Distributed multi-worker coordination/lock belum memiliki
   infrastructure.

6. Update retry/DLQ belum memiliki contract.

7. Event/outbox runtime lifecycle belum memiliki infrastructure.

8. Multi-bot multiplexing pada satu connection masih out of scope.

==================================================
TARGET B-048
==================================================

B-048 — deployment adapter + operational readiness.

Tujuan:

Membuat THIN deployment adapter yang menghubungkan API
persistence yang sudah ada ke worker runtime production.

Target architecture:

deployment configuration
        ↓
deployment adapter
        ↓
createPostgresPersistence()
        ↓
WorkerPersistenceResource
        ↓
existing composition root
        ↓
worker runtime

PENTING:

B-048 BUKAN membuat persistence architecture baru.

B-048 hanya membuat adapter deployment yang membungkus API
yang SUDAH ADA.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-047
- B-030
- B-070
- B-071

Jangan membuat:

- persistence abstraction kedua,
- WorkerPersistenceResource kedua,
- database repository kedua,
- SecretResolver kedua,
- Telegram driver kedua,
- worker bootstrap kedua,
- runtime driver kedua,
- queue baru,
- retry system baru,
- DLQ baru,
- distributed lock baru,
- outbox system baru.

Gunakan abstraction yang SUDAH ADA.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Audit hanya bagian yang relevan dengan B-048:

- createPostgresPersistence
- WorkerPersistenceResource
- existing persistence adapter
- worker package
- composition root B-047
- configuration loader
- deployment configuration
- workspace scope
- existing worker bootstrap
- package boundaries
- import rules
- deployment documentation.

Jangan melakukan full repository rewrite.

Tentukan secara eksplisit:

1. API persistence yang sudah tersedia.
2. API worker resource yang sudah tersedia.
3. dependency yang masih perlu dijembatani.
4. lokasi terbaik untuk deployment adapter.
5. apakah adapter harus berada di package deployment,
   infrastructure, atau worker composition berdasarkan
   struktur repository yang SUDAH ADA.

Jangan memindahkan package hanya demi preferensi pribadi.

==================================================
BAGIAN 2 — CREATE POSTGRES PERSISTENCE ADAPTER
==================================================

Implementasikan thin adapter menggunakan:

createPostgresPersistence()

jika function tersebut memang sudah tersedia.

Target:

DATABASE_URL
    ↓
deployment configuration
    ↓
createPostgresPersistence()
    ↓
WorkerPersistenceResource

Adapter harus:

- menerima configuration melalui dependency injection,
- tidak membaca environment variable secara acak,
- tidak membuat repository business baru,
- tidak mengandung business logic,
- tidak mengubah domain model,
- tidak mengubah repository contract,
- tidak membuat database abstraction baru.

Jika createPostgresPersistence() belum memiliki API yang cukup:

→ audit terlebih dahulu.

Jika perubahan API benar-benar diperlukan untuk compatibility:

→ lakukan perubahan minimum.

Jangan refactor besar.

==================================================
BAGIAN 3 — ENVIRONMENT CONFIGURATION
==================================================

Gunakan configuration mechanism yang SUDAH ADA.

Production deployment harus mendukung configuration seperti:

DATABASE_URL
WORKER_WORKSPACE_SCOPE

dan secret-manager reference jika memang sudah digunakan oleh
B-047.

Jangan hardcode:

- database URL,
- username,
- password,
- Telegram token,
- secret,
- API key.

Jangan mencetak DATABASE_URL ke log.

Jika configuration invalid:

→ fail fast dengan error yang jelas dan sanitized.

Contoh:

"DATABASE_URL is required for production persistence"

Bukan menampilkan nilai DATABASE_URL.

==================================================
BAGIAN 4 — WORKER WORKSPACE SCOPE
==================================================

Pastikan deployment adapter meneruskan:

WORKER_WORKSPACE_SCOPE

ke worker runtime/resource sesuai abstraction existing.

Workspace scope harus tetap:

- explicit,
- validated,
- isolated,
- tidak boleh mengambil workspace lain secara otomatis.

Jangan mengubah ownership model.

Jangan membuat worker mengambil SEMUA workspace jika existing
architecture memang menggunakan scoped worker.

Jika workspace scope memang optional menurut architecture:

→ gunakan behavior existing.

Jangan mengarang policy baru.

==================================================
BAGIAN 5 — PERSISTENCE RESOURCE LIFECYCLE
==================================================

Pastikan persistence resource memiliki lifecycle yang benar.

Startup:

configuration
→ create persistence
→ worker startup

Shutdown:

worker stop
→ persistence cleanup/close

Gunakan lifecycle abstraction yang SUDAH ADA.

Jangan membuat shutdown manager kedua.

Jangan membuat connection pool global tersembunyi.

Jangan membuka koneksi database di setiap update.

==================================================
BAGIAN 6 — FAILURE HANDLING
==================================================

Pastikan kegagalan persistence startup ditangani dengan benar.

Contoh:

DATABASE_URL invalid
→ startup fails clearly

Database unavailable
→ startup fails safely

Credential resolver gagal
→ startup fails safely jika dependency memang required

Jangan:

- retry infinite,
- membuat queue,
- membuat DLQ,
- membuat fallback SQLite,
- membuat in-memory database production,
- membuat fake PostgreSQL production.

Jika infrastructure belum tersedia, error harus jelas dan sanitized.

==================================================
BAGIAN 7 — TEST COMPOSITION
==================================================

Tambahkan test untuk deployment adapter.

Minimal:

1. valid configuration menghasilkan WorkerPersistenceResource.

2. DATABASE_URL missing ditolak.

3. invalid configuration ditolak.

4. workspace scope diteruskan dengan benar.

5. persistence lifecycle dapat dibuat.

6. shutdown/cleanup dipanggil.

7. database credential tidak masuk error/log.

8. adapter tidak membuat dependency kedua.

Gunakan fake/test persistence hanya di TEST COMPOSITION.

Jangan membuat fake production adapter.

==================================================
BAGIAN 8 — POSTGRESQL INTEGRATION
==================================================

Periksa:

PERSISTENCE_TEST_DATABASE_URL

Jika tersedia:

→ jalankan integration test PostgreSQL yang SUDAH ADA.

Pastikan test benar-benar menggunakan PostgreSQL.

Jika tidak tersedia:

→

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan:

- membuat SQLite fallback,
- membuat database palsu,
- mengubah test agar PASS,
- mengubah production adapter agar memakai fake.

Jika test gagal:

→ diagnosis penyebab sebenarnya.

==================================================
BAGIAN 9 — SECRET MANAGER
==================================================

JANGAN implementasikan managed secret-manager vendor baru pada B-048.

SecretResolver boundary dari B-047 tetap digunakan.

Jika managed secret-manager nyata belum tersedia:

→ tetap DEFERRED.

Jangan:

- memilih vendor secara speculative,
- menambahkan SDK vendor,
- hardcode secret,
- membuat fake production secret manager.

B-048 hanya memastikan deployment adapter compatible dengan
SecretResolver/configuration boundary yang SUDAH ADA.

==================================================
BAGIAN 10 — REAL TELEGRAM
==================================================

JANGAN mengimplementasikan Telegram integration baru.

Jika credential/test environment belum tersedia:

REAL TELEGRAM:

DEFERRED — credential/test environment unavailable

Jangan membuat:

- fake production Telegram,
- token palsu,
- webhook,
- polling tambahan,
- Telegram SDK baru.

==================================================
BAGIAN 11 — OUT OF SCOPE
==================================================

Jangan mengerjakan:

- distributed lock,
- multi-worker coordination,
- retry,
- DLQ,
- event/outbox,
- multi-bot multiplexing,
- rate limiting,
- share expiry,
- audit event,
- provider baru,
- UI baru,
- Gorouter.app.

Semua tetap deferred jika belum memiliki dependency yang nyata.

==================================================
BAGIAN 12 — SECURITY REVIEW
==================================================

Review perubahan B-048 untuk:

- DATABASE_URL leakage,
- password leakage,
- secret leakage,
- credential leakage,
- workspace isolation,
- configuration validation,
- sanitized errors,
- sanitized logs.

Pastikan:

git diff

tidak mengandung:

- password,
- API key,
- database credential,
- Telegram token,
- secret manager credential.

==================================================
BAGIAN 13 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut memang tidak tersedia.

Jika PostgreSQL environment tersedia:

→ jalankan integration test PostgreSQL.

Jika tidak:

→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan menyamarkan SKIPPED menjadi PASS.

==================================================
BAGIAN 14 — DIFF REVIEW
==================================================

Setelah validation:

git status
git diff --stat
git diff

Pastikan perubahan hanya:

- deployment adapter,
- persistence wiring compatibility,
- configuration validation,
- lifecycle wiring,
- deployment adapter tests,
- dokumentasi yang memang diperlukan.

Hapus:

- debug code,
- temporary files,
- generated files,
- unrelated refactor,
- duplicate abstraction.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA,
- TokenHarbor,
- B-070,
- B-071,
- Telegram runtime architecture yang sudah selesai.

==================================================
BAGIAN 15 — COMMIT
==================================================

Jika implementation valid dan validation PASS:

buat SATU commit.

Gunakan:

feat: add postgres deployment adapter

atau commit message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 16 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD
git status

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan hapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-048 selesai jika:

- thin deployment adapter tersedia,
- createPostgresPersistence() ter-wire,
- WorkerPersistenceResource ter-wire,
- DATABASE_URL configuration ter-wire,
- WORKER_WORKSPACE_SCOPE ter-wire jika memang diperlukan,
- lifecycle startup/shutdown benar,
- configuration validation benar,
- secret tidak bocor,
- PostgreSQL integration PASS atau SKIPPED dengan alasan nyata,
- Unit PASS,
- Build PASS,
- Typecheck PASS,
- Lint PASS,
- Format PASS,
- Imports PASS,
- Ownership PASS,
- Docs PASS,
- Diff PASS,
- commit berhasil,
- push berhasil,
- local SHA == remote SHA,
- working tree CLEAN.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-048 STATUS

Deployment adapter:
Persistence:
Configuration:
Workspace scope:
Lifecycle:
Security:

### TEST

Unit:
PostgreSQL:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata repository.

Jangan membuat fitur speculative.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-047 — Production Composition Root Deployment Wiring
```
Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-040 — Account Session Connection:
SELESAI.

B-041 — Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 — Runtime Execution:
SELESAI.

B-043 — Real Telegram Runtime Driver:
SELESAI.

B-044 — Real Telegram SDK-backed TelegramClientFactory:
SELESAI.

B-045 — Production Worker Bootstrap + Update Routing:
SELESAI.

B-046 — Persistence-backed Installation Discovery +
worker credential wiring:
SELESAI.

B-046 validation terakhir:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN
- Commit/push: berhasil

Remaining deferred yang SUDAH DIKETAHUI:
- Managed secret-manager implementation nyata belum tersedia.
- PostgreSQL integration membutuhkan PERSISTENCE_TEST_DATABASE_URL.
- Real Telegram integration membutuhkan credential/test environment.
- Distributed multi-worker coordination/lock belum ada infrastructure.
- Update retry/DLQ belum memiliki contract.
- Event/outbox runtime lifecycle belum memiliki infrastructure.
- Multi-bot multiplexing pada satu Telegram connection masih out of scope.

==================================================
NEXT ROADMAP
==================================================

B-047 — production composition root deployment wiring.

Tujuan:

Menyediakan root composition yang benar-benar meng-inject:

configuration
    ↓
persistence
    ↓
managed secret resolver boundary
    ↓
workspace/installation discovery
    ↓
credential resolver
    ↓
TelegramClientFactory
    ↓
Telegram RuntimeExecutionDriver
    ↓
worker runtime

B-047 harus menyelesaikan wiring deployment,
BUKAN membuat architecture baru.

==================================================
ATURAN KERAS
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-046
- B-030
- B-070
- B-071

Jangan membuat:

- InstallationDiscovery kedua.
- CredentialResolver kedua.
- SecretResolver interface kedua.
- TelegramClientFactory kedua.
- RuntimeExecutionDriver kedua.
- repository kedua.
- worker bootstrap kedua.
- queue baru.
- scheduler baru.
- retry/DLQ baru.
- distributed lock baru.
- outbox system baru.

Gunakan abstraction yang SUDAH ADA.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Audit composition root dan deployment entrypoint.

Cari dan pahami:

- main.ts
- worker entrypoint
- configuration loader
- persistence composition
- BotInstallationRepository
- InstallationDiscovery B-046
- SecretResolver
- CapabilityCredentialResolver
- ProviderSessionDriver
- TelegramClientFactory B-044
- RuntimeExecutionDriver B-043/B-045
- runtime registry
- workspace repository/service
- existing deployment configuration
- existing environment/config documentation.

Jangan melakukan full repository audit.

Tentukan:

1. dependency mana yang sudah production-ready,
2. dependency mana yang hanya test/fake,
3. dependency mana yang masih deferred karena infrastructure,
4. dependency mana yang harus di-wire di composition root.

==================================================
BAGIAN 2 — ROOT CONFIGURATION
==================================================

Pastikan production configuration dibangun melalui SATU
composition boundary yang jelas.

Configuration harus mencakup dependency yang memang sudah tersedia,
misalnya:

- database configuration,
- Telegram provider configuration,
- SecretResolver reference,
- runtime configuration,
- worker configuration.

Jangan membaca process.env secara acak di service/module.

Jika repository sudah memiliki configuration abstraction:

→ gunakan abstraction tersebut.

Jika configuration helper sudah ada:

→ jangan membuat helper kedua.

==================================================
BAGIAN 3 — PERSISTENCE
==================================================

Composition root harus membuat persistence dependency melalui
adapter/repository yang SUDAH ADA.

Target:

configuration
→ database/persistence adapter
→ BotInstallationRepository
→ InstallationDiscovery

Worker tidak boleh:

- membuat koneksi database sendiri,
- membuat repository sendiri,
- membaca SQL langsung,
- mengetahui detail database.

Jika PostgreSQL production adapter sudah ada:

→ wire adapter tersebut.

Jika production PostgreSQL infrastructure belum tersedia:

→ jangan membuat fake production database.

Tetap gunakan abstraction existing dan tandai infrastructure verification
sebagai DEFERRED.

==================================================
BAGIAN 4 — SECRETRESOLVER
==================================================

Audit SecretResolver boundary yang SUDAH ADA.

Composition root harus menerima SecretResolver melalui dependency
injection.

Jangan membuat SecretResolver interface baru.

Jika managed secret manager vendor BELUM ditentukan atau belum tersedia:

→ jangan memilih vendor secara speculative.

Gunakan existing production boundary/reference mechanism.

Jika hanya fake/test resolver yang tersedia:

→ gunakan fake hanya pada test composition.

Production composition TIDAK BOLEH diam-diam menggunakan fake resolver.

Jangan hardcode:

- token,
- API key,
- password,
- access key,
- secret key,
- Telegram credential.

==================================================
BAGIAN 5 — INSTALLATION DISCOVERY
==================================================

Wire InstallationDiscovery hasil B-046 ke worker.

Target:

Persistence
→ BotInstallationRepository
→ InstallationDiscovery
→ Worker bootstrap

Jangan membuat discovery baru.

Pastikan discovery tetap:

- workspace-aware,
- ownership-aware,
- eligibility-aware,
- persistence-backed.

==================================================
BAGIAN 6 — CREDENTIAL RESOLVER
==================================================

Wire existing CapabilityCredentialResolver/
credential resolver ke runtime.

Target:

Installation
→ credential/session reference
→ existing resolver
→ credential
→ TelegramClientFactory

Credential tidak boleh:

- masuk log,
- masuk error message,
- masuk HTTP response,
- disimpan ulang,
- ditulis ke Git.

Jika resolver gagal untuk installation tertentu:

→ installation tersebut gagal secara terisolasi.

Jangan menghentikan seluruh worker jika architecture B-045
memang mendukung per-installation isolation.

==================================================
BAGIAN 7 — TELEGRAM CLIENT FACTORY
==================================================

Composition root HARUS menggunakan TelegramClientFactory dari B-044.

Jangan instantiate Telegram SDK langsung di worker.

Target:

CredentialResolver
→ TelegramClientFactory
→ TelegramClient
→ RuntimeExecutionDriver

Jika provider-specific library dependency memang belum tersedia:

→ jangan membuat fake production Telegram client.

Tandai real provider integration sebagai DEFERRED.

==================================================
BAGIAN 8 — RUNTIME DRIVER
==================================================

Wire RuntimeExecutionDriver yang SUDAH dibuat pada B-043/B-045.

Jangan membuat driver baru.

Pastikan dependency graph:

InstallationDiscovery
+
CredentialResolver
+
TelegramClientFactory
+
RuntimeExecutionDriver
+
runtime registry
+
worker bootstrap

dapat dibuat dari SATU composition root.

==================================================
BAGIAN 9 — NO INSTALLATION
==================================================

Production worker harus dapat startup ketika:

eligible installations = 0

Ini bukan fatal error.

Worker harus:

- startup,
- log sanitized status,
- tetap ready untuk lifecycle yang memang sudah didukung.

Jangan membuat polling loop baru hanya untuk menunggu installation.

Jangan membuat scheduler baru.

==================================================
BAGIAN 10 — FAILURE ISOLATION
==================================================

Pastikan dependency wiring tidak menyebabkan satu installation
menghentikan worker global.

Contoh:

Installation A → STARTED
Installation B → credential failure
Installation C → STARTED

Worker tetap hidup.

Jangan membuat retry queue.

Jangan membuat DLQ.

Jangan membuat distributed lock.

==================================================
BAGIAN 11 — SHUTDOWN
==================================================

Audit graceful shutdown existing.

Composition root harus mengembalikan lifecycle dependency yang dapat
ditutup secara benar.

Pastikan:

SIGTERM/SIGINT
→ stop worker
→ stop runtimes
→ close Telegram clients jika supported
→ close persistence resources
→ exit cleanly

Gunakan lifecycle abstraction yang SUDAH ADA.

Jangan membuat shutdown manager kedua jika existing lifecycle sudah tersedia.

==================================================
BAGIAN 12 — CONFIGURATION VALIDATION
==================================================

Validasi hanya configuration yang memang wajib.

Jika production configuration invalid:

→ fail fast dengan error yang jelas.

Namun:

JANGAN mencetak nilai secret.

Contoh yang aman:

"Telegram credential reference is missing"

Bukan:

"Telegram token = ..."

Test environment harus tetap dapat menggunakan dependency injection.

==================================================
BAGIAN 13 — TEST COMPOSITION ROOT
==================================================

Tambahkan unit/integration-style composition test yang tidak membutuhkan
real Telegram credential.

Test:

1. production dependency graph dapat dibangun dengan injected fakes,
2. InstallationDiscovery ter-wire,
3. CredentialResolver ter-wire,
4. TelegramClientFactory ter-wire,
5. RuntimeExecutionDriver ter-wire,
6. zero installation startup,
7. multiple installation composition,
8. credential failure isolation,
9. invalid configuration ditolak,
10. SecretResolver failure tidak membocorkan secret,
11. graceful shutdown dependency graph,
12. no duplicate runtime dependency construction.

Gunakan fake/test implementations hanya di test.

Jangan membuat fake production implementation.

==================================================
BAGIAN 14 — ENVIRONMENT-GATED TEST
==================================================

Jika:

PERSISTENCE_TEST_DATABASE_URL

tersedia:

→ jalankan integration test PostgreSQL yang memang sudah ada.

Jika tidak tersedia:

→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat database palsu.

Real Telegram:

Jika credential/test environment tidak tersedia:

→ DEFERRED — real Telegram credentials/test environment unavailable

Jangan membuat token palsu.

==================================================
BAGIAN 15 — SECURITY REVIEW
==================================================

Review seluruh composition root untuk:

- secret leakage,
- credential leakage,
- workspace isolation,
- installation ownership,
- configuration injection,
- provider credential boundary,
- sanitized errors,
- sanitized logs.

Pastikan production composition tidak menggunakan test fake secara tidak sengaja.

==================================================
BAGIAN 16 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut memang diketahui tidak tersedia.

Jika command validation tidak tersedia:

→ SKIPPED/UNAVAILABLE

Jangan membuat script dummy.

==================================================
BAGIAN 17 — DIFF REVIEW
==================================================

Review:

git status
git diff --stat
git diff

Pastikan perubahan hanya:

- composition root,
- deployment configuration wiring,
- dependency injection,
- lifecycle wiring,
- composition tests,
- documentation yang benar-benar diperlukan.

Hapus:

- debug code,
- temporary files,
- generated files,
- unrelated refactor,
- secrets.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA provider,
- TokenHarbor,
- B-070,
- B-071,
- B-030.

==================================================
BAGIAN 18 — COMMIT
==================================================

Jika implementation valid dan validation PASS:

buat SATU commit.

Gunakan message:

feat: wire production composition root

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 19 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

git status

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan hapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-047 selesai jika:

- production composition root jelas,
- configuration dependency ter-wire,
- persistence dependency ter-wire,
- InstallationDiscovery B-046 ter-wire,
- SecretResolver boundary ter-wire,
- credential resolver ter-wire,
- TelegramClientFactory B-044 ter-wire,
- RuntimeExecutionDriver ter-wire,
- worker bootstrap menggunakan dependency graph tersebut,
- zero-installation startup aman,
- failure isolation aman,
- graceful shutdown ter-wire,
- test composition PASS,
- Unit PASS,
- Build PASS,
- Typecheck PASS,
- Lint PASS,
- Format PASS,
- Imports PASS,
- Ownership PASS,
- Docs PASS,
- Diff PASS,
- PostgreSQL PASS atau SKIPPED dengan alasan nyata,
- Real Telegram PASS atau DEFERRED dengan alasan nyata,
- commit berhasil,
- push berhasil,
- local SHA == remote SHA,
- working tree CLEAN.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-047 STATUS

Composition root:
Configuration:
Persistence:
InstallationDiscovery:
SecretResolver:
CredentialResolver:
TelegramClientFactory:
RuntimeExecutionDriver:
Worker bootstrap:
Graceful shutdown:

### SECURITY

Secret handling:
Credential handling:
Workspace isolation:
Installation ownership:
Error sanitization:
Log sanitization:

### TEST

Unit:
PostgreSQL:
Real Telegram:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata.
Jangan membuat fitur speculative.

Kerjakan langsung pada:

/root/botspace


```
# Prompt: B-046 — Persistence Installation Discovery + Worker Credential Wiring
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR
==================================================

B-040 — Account Session Connection:
SELESAI.

B-041 — Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 — Runtime Execution:
SELESAI.

B-043 — Real Telegram Runtime Driver:
SELESAI.

B-044 — Real Telegram SDK-backed TelegramClientFactory:
SELESAI.

B-045 — Production Worker Bootstrap + Update Routing:
SELESAI.

B-045 validation:

- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS
- Working tree: CLEAN

Real Telegram integration:
DEFERRED — real Telegram credentials/test environment unavailable.

==================================================
REMAINING DEFERRED DARI B-045
==================================================

- Live Telegram integration test — credential/environment belum tersedia.
- Persistence-backed InstallationDiscovery + worker credential-resolver wiring.
- Distributed multi-worker coordination — belum ada infrastructure.
- Update retry/DLQ — belum ada contract.
- Event/outbox emission runtime lifecycle — outbox infrastructure belum tersedia.

==================================================
NEXT ROADMAP
==================================================

B-046 — persistence-backed installation discovery + worker credential wiring.

Tujuan:

Mengganti discovery/credential wiring worker yang masih bergantung pada
in-memory/static composition dengan repository-backed discovery dan
credential resolution yang benar-benar mengikuti architecture existing.

Fokus:

BotInstallation repository
        ↓
InstallationDiscovery
        ↓
eligible installations
        ↓
credential/session resolver
        ↓
TelegramClientFactory
        ↓
B-045 worker runtime

==================================================
ATURAN UTAMA
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-045
- B-030
- B-070
- B-071

Jangan membuat architecture kedua.

Jangan membuat:

- InstallationRepository kedua.
- InstallationDiscovery kedua.
- SecretResolver kedua.
- CredentialResolver kedua jika abstraction existing sudah tersedia.
- TelegramClientFactory kedua.
- RuntimeExecutionDriver kedua.
- Worker bootstrap kedua.
- queue baru.
- scheduler baru.
- distributed lock baru.
- retry/DLQ baru.
- outbox system baru.

Gunakan abstraction yang SUDAH ADA.

==================================================
BAGIAN 1 — TARGETED AUDIT
==================================================

Sebelum coding, audit hanya dependency B-046.

Cari dan pahami:

- BotInstallation model.
- BotInstallation repository/port.
- existing persistence adapter.
- existing InstallationDiscovery.
- worker bootstrap B-045.
- runtime registry.
- ProviderSessionDriver B-041.
- SecretResolver.
- credential resolver jika sudah ada.
- TelegramClientFactory B-044.
- Telegram runtime driver B-043.
- workspace/ownership contract.
- installation lifecycle state.
- database configuration.
- existing migrations.

Jangan melakukan full repository rewrite.

Tentukan:

1. Mana abstraction yang sudah tersedia.
2. Mana yang hanya placeholder.
3. Mana yang benar-benar perlu diimplementasikan untuk B-046.
4. Mana yang masih harus deferred karena infrastructure belum tersedia.

==================================================
BAGIAN 2 — PERSISTENCE-BACKED INSTALLATION DISCOVERY
==================================================

Implementasikan InstallationDiscovery menggunakan persistence yang SUDAH ADA.

Target:

database
  ↓
BotInstallationRepository
  ↓
InstallationDiscovery
  ↓
eligible BotInstallation
  ↓
worker runtime

Discovery TIDAK boleh:

- membaca database langsung dari worker,
- membuat SQL di worker,
- membaca process.env secara acak,
- membuat repository sendiri,
- bypass service/repository boundary.

Worker hanya bergantung pada abstraction.

==================================================
BAGIAN 3 — BOT INSTALLATION ELIGIBILITY
==================================================

Audit state/status BotInstallation yang sudah ada.

Gunakan state existing.

JANGAN mengubah:

BotInstallation.status

menjadi runtime process state.

Bedakan:

Installation lifecycle state
vs
Runtime process state.

Installation hanya boleh ditemukan jika memang eligible berdasarkan
contract existing.

Pertimbangkan existing rules untuk:

- enabled/active,
- revoked,
- disabled,
- deleted,
- session/connection validity,
- provider availability,
- workspace ownership.

Jangan membuat status baru hanya untuk B-046.

Jika eligibility sudah memiliki helper/service:

→ gunakan helper tersebut.

Jika belum:

→ buat predicate/helper minimal di domain/service boundary yang tepat.

Jangan menaruh business rules di SQL query kecuali architecture existing memang demikian.

==================================================
BAGIAN 4 — WORKSPACE ISOLATION
==================================================

Pastikan InstallationDiscovery tidak mencampurkan workspace.

Installation milik workspace A:

TIDAK BOLEH ditemukan sebagai installation workspace B.

Pastikan:

- workspace identity berasal dari trusted context,
- installation ownership diverifikasi,
- repository query tetap scoped,
- worker tidak menerima workspace identity arbitrary dari Telegram update.

Jika worker global memang harus menemukan seluruh eligible installations:

→ discovery tetap mengembalikan ownership identity secara eksplisit.

Jangan menghapus workspace identity dari result.

==================================================
BAGIAN 5 — CREDENTIAL RESOLUTION
==================================================

Audit abstraction credential yang SUDAH tersedia.

Jika sudah ada:

- SecretResolver,
- ProviderSessionDriver,
- CredentialResolver,
- session credential abstraction,

gunakan abstraction tersebut.

Jangan membuat duplicate.

Target flow:

Installation
    ↓
session/credential reference
    ↓
existing resolver/provider boundary
    ↓
credential material
    ↓
TelegramClientFactory
    ↓
Telegram client

Credential material TIDAK BOLEH:

- disimpan kembali ke database,
- dimasukkan ke BotInstallation object jika tidak diperlukan,
- ditulis ke log,
- dimasukkan ke error message,
- dikirim ke core runtime,
- dikirim ke HTTP response.

==================================================
BAGIAN 6 — SECRETRESOLVER BOUNDARY
==================================================

Jika SecretResolver sudah tersedia:

worker harus bergantung pada abstraction tersebut.

Jangan:

process.env.TELEGRAM_BOT_TOKEN

atau pattern sejenis langsung dari worker.

Jika provider/session credential membutuhkan SecretResolver:

gunakan existing dependency injection.

Jika deployment SecretResolver belum tersedia:

tetap implementasikan wiring berdasarkan abstraction existing.

Jangan membuat production fake.

Tandai real secret-manager integration sebagai DEFERRED bila environment belum tersedia.

==================================================
BAGIAN 7 — TELEGRAM CLIENT FACTORY
==================================================

Worker HARUS menggunakan:

TelegramClientFactory

dari B-044.

Flow:

InstallationDiscovery
→ eligible installation
→ credential/session resolution
→ TelegramClientFactory
→ TelegramClient
→ B-045 runtime

Jangan instantiate Telegram SDK secara langsung.

Jangan membuat client factory baru.

Jangan membuat provider-specific credential logic di worker.

==================================================
BAGIAN 8 — WORKER STARTUP INTEGRATION
==================================================

Update B-045 worker bootstrap agar:

startup
  ↓
load configuration
  ↓
create persistence dependencies
  ↓
create InstallationDiscovery
  ↓
discover eligible installations
  ↓
resolve credentials
  ↓
create Telegram clients
  ↓
create runtime instances
  ↓
attach update routing
  ↓
start runtime

Jika tidak ada installation:

worker tetap startup dengan aman.

Status:

READY / RUNNING

sesuai lifecycle existing.

Jangan menganggap "no installation" sebagai fatal error.

==================================================
BAGIAN 9 — FAILURE ISOLATION
==================================================

Jika satu installation gagal:

misalnya:

- invalid credential,
- revoked session,
- malformed configuration,
- Telegram client initialization failure,

jangan otomatis menghentikan seluruh worker.

Gunakan isolation B-045.

Contoh:

Installation A → STARTED
Installation B → FAILED
Installation C → STARTED

Worker tetap hidup.

Jangan membuat retry queue.

Jangan membuat DLQ.

Jangan membuat scheduler.

Failure hanya dicatat secara sanitized dan runtime installation terkait
masuk failure state sesuai existing lifecycle.

==================================================
BAGIAN 10 — DUPLICATE RUNTIME
==================================================

Gunakan runtime registry/guard dari B-045.

Pastikan discovery tidak menyebabkan:

installation yang sama
→ dua runtime instance

dalam satu worker process.

Jika runtime sudah aktif:

→ jangan start instance kedua.

Jangan membuat distributed lock.

Distributed multi-worker coordination tetap:

DEFERRED.

==================================================
BAGIAN 11 — PERSISTENCE ADAPTER
==================================================

Jika BotInstallation repository adapter sudah tersedia:

→ gunakan.

Jika belum:

implementasikan hanya adapter yang memang menjadi dependency langsung B-046.

Repository harus:

- scoped,
- typed,
- tidak mengandung business logic,
- tidak membaca credential,
- tidak membuat Telegram client,
- tidak mengetahui worker lifecycle.

Jangan membuat database schema baru jika schema existing sudah cukup.

Jika migration/schema benar-benar kurang:

jangan speculative.

Laporkan dependency schema tersebut sebagai deferred dan jangan memaksakan implementation.

==================================================
BAGIAN 12 — TESTING
==================================================

Tambahkan unit test untuk:

1. InstallationDiscovery tanpa installation.
2. Satu eligible installation.
3. Multiple eligible installations.
4. Disabled installation tidak ditemukan.
5. Revoked installation tidak ditemukan.
6. Invalid installation tidak ditemukan.
7. Workspace isolation.
8. Repository failure.
9. Credential resolution success.
10. Credential resolution failure.
11. Credential tidak bocor ke error.
12. TelegramClientFactory menerima credential melalui dependency injection.
13. Worker tidak instantiate Telegram SDK langsung.
14. One installation failure tidak menghentikan installation lain.
15. Duplicate runtime protection.
16. Startup dengan zero installations.
17. Graceful shutdown terhadap discovered runtimes.

Gunakan fake/in-memory repository untuk unit test.

Jangan membutuhkan:

- production PostgreSQL,
- Telegram production token,
- real Telegram account.

==================================================
BAGIAN 13 — POSTGRESQL INTEGRATION
==================================================

Periksa:

PERSISTENCE_TEST_DATABASE_URL

Jika tersedia:

jalankan integration test repository/installation yang memang sudah tersedia.

Jika tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan:

- membuat database palsu,
- mengganti PostgreSQL dengan SQLite,
- mengubah test agar PASS,
- menjalankan migration destruktif.

==================================================
BAGIAN 14 — REAL TELEGRAM INTEGRATION
==================================================

Jika real Telegram credentials/test environment tersedia:

jalankan integration test yang memang sudah ada.

Jika tidak:

DEFERRED — real Telegram credentials/test environment unavailable

Jangan:

- menggunakan production token,
- membuat token palsu,
- memasukkan token ke source,
- memasukkan token ke test fixture,
- mencetak credential.

==================================================
BAGIAN 15 — SECURITY REVIEW
==================================================

Review:

- workspace isolation,
- installation ownership,
- credential resolution,
- SecretResolver boundary,
- revoked/disabled handling,
- error sanitization,
- log sanitization,
- Telegram credential lifecycle,
- runtime isolation.

Pastikan tidak ada:

- token di log,
- secret di exception,
- credential di Git diff,
- raw provider response yang mengandung credential,
- cross-workspace runtime.

==================================================
BAGIAN 16 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut memang tidak tersedia.

Jika command validation tertentu tidak tersedia:

jangan membuat script dummy.

Laporkan sebagai SKIPPED/UNAVAILABLE.

==================================================
BAGIAN 17 — DIFF REVIEW
==================================================

Sebelum commit:

git status

git diff --stat

git diff

Pastikan perubahan hanya:

- InstallationDiscovery,
- persistence wiring,
- credential resolver wiring,
- worker integration,
- tests,
- documentation yang benar-benar diperlukan.

Hapus:

- debug code,
- temporary files,
- generated files,
- credentials,
- unrelated refactor.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA provider,
- TokenHarbor,
- B-071,
- B-070,
- B-030.

==================================================
BAGIAN 18 — COMMIT
==================================================

Jika implementation valid dan validation PASS:

buat SATU commit.

Commit message:

feat: wire persistent installation discovery

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 19 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

git status

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-046 dianggap selesai jika:

- InstallationDiscovery persistence-backed.
- Existing BotInstallation repository digunakan.
- Eligibility menggunakan existing lifecycle rules.
- Workspace isolation terjaga.
- Credential resolution menggunakan abstraction existing.
- SecretResolver boundary tidak dibypass.
- TelegramClientFactory B-044 digunakan.
- B-045 worker menggunakan discovery baru.
- Multiple installations dapat diproses.
- Failure isolation bekerja.
- Duplicate local runtime dicegah.
- Zero-installation startup aman.
- Credential tidak bocor.
- Unit tests PASS.
- Build PASS.
- Typecheck PASS.
- Lint PASS.
- Format PASS.
- Imports PASS.
- Ownership PASS.
- Docs PASS.
- Diff PASS.
- PostgreSQL integration PASS atau SKIPPED dengan alasan nyata.
- Real Telegram integration PASS atau DEFERRED dengan alasan nyata.
- Commit berhasil.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-046 STATUS

InstallationDiscovery:
Status:

Persistence:
Status:

Eligibility:
Status:

Workspace isolation:
Status:

Credential resolution:
Status:

SecretResolver:
Status:

TelegramClientFactory:
Status:

Worker integration:
Status:

Failure isolation:
Status:

Duplicate runtime protection:
Status:

### SECURITY

Credential handling:
Workspace isolation:
Installation ownership:
Error sanitization:
Log sanitization:

### TEST

Unit:
PostgreSQL integration:
Real Telegram integration:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Tentukan roadmap berikutnya berdasarkan dependency nyata setelah B-046.

Jangan kembali ke B-040 sampai B-045.
Jangan membuat architecture kedua.
Jangan membuat queue/DLQ speculative.
Jangan membuat distributed lock speculative.
Jangan mengerjakan fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-045 — Production Worker Bootstrap + Update Routing
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR — B-044 SUDAH SELESAI
==================================================

B-040 Account Session Connection:
SELESAI.

B-041 Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 Runtime Execution:
SELESAI.

B-043 Real Telegram Runtime Driver boundary:
SELESAI.

B-044 Real Telegram SDK-backed TelegramClientFactory:
SELESAI.

Commit B-044:
6a825ec

Commit:
feat: add telegram client factory

Push:
OK

Local SHA == Remote SHA

Working tree:
CLEAN

Validation:
PASS

Real Telegram integration:
DEFERRED — real Telegram credentials/test environment unavailable.

Deferred infrastructure:
- Live Telegram integration test.
- Event/outbox emission runtime.
- Durable/distributed runtime scheduling.
- Queue/lock infrastructure belum tersedia/disetujui.

==================================================
NEXT ROADMAP
==================================================

B-045 — production worker bootstrap + update routing.

Tujuan B-045:

Menghubungkan:

TelegramClientFactory
        ↓
Telegram runtime driver
        ↓
production worker bootstrap
        ↓
Telegram update normalization
        ↓
runtime execution

Tanpa membuat architecture kedua.

==================================================
ATURAN UTAMA
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043
- B-044
- B-071
- B-070
- B-030

Gunakan implementation existing sebagai source of truth.

Jangan membuat:

- RuntimeExecutionPort kedua.
- TelegramRuntimeExecutionDriver kedua.
- TelegramClientFactory kedua.
- ProviderSessionDriver kedua.
- SecretResolver kedua.
- worker framework kedua.
- queue system baru.
- outbox system baru.
- scheduler baru.
- distributed lock baru.

Fokus hanya B-045.

==================================================
BAGIAN 1 — AUDIT CURRENT ARCHITECTURE
==================================================

Sebelum coding, audit repository secara targeted.

Cari dan pahami:

- TelegramClientFactory dari B-044.
- Telegram client abstraction.
- TelegramRuntimeExecutionDriver dari B-043.
- ProviderSessionDriver dari B-041.
- RuntimeExecutionPort dari B-042.
- runtime composition.
- worker module.
- existing worker bootstrap.
- existing application entrypoint.
- existing process entrypoint.
- update/event types.
- configuration system.
- installation/session state.
- SecretResolver.
- existing lifecycle state.
- existing runtime environment/configuration.

Jangan melakukan full repository audit yang mengulang pekerjaan sebelumnya.

Audit hanya dependency B-045.

Setelah memahami architecture:

implementasikan B-045 berdasarkan abstraction yang SUDAH ADA.

==================================================
BAGIAN 2 — PRODUCTION WORKER BOOTSTRAP
==================================================

Implementasikan production worker bootstrap jika belum ada.

Worker bootstrap bertanggung jawab untuk:

1. membuat composition root,
2. membuat dependencies,
3. membuat provider runtime,
4. menemukan installation yang eligible,
5. membuat runtime instance,
6. memasang update handler,
7. menjalankan runtime,
8. menangani shutdown,
9. menangani startup failure secara aman.

Worker bootstrap TIDAK boleh:

- mengandung business logic Telegram,
- membaca secret secara langsung,
- membuat Telegram SDK client secara manual,
- mengakses database secara acak,
- membuat singleton tersembunyi,
- membuat scheduler baru.

Semua dependency harus melalui composition root/existing dependency injection.

==================================================
BAGIAN 3 — WORKER ENTRYPOINT
==================================================

Audit apakah repository sudah memiliki:

- worker entrypoint,
- worker command,
- process entrypoint,
- `main.ts`,
- `worker.ts`,
- bootstrap module,
- package.json scripts.

Jika entrypoint sudah ada:

→ gunakan dan extend.

Jika belum:

→ buat entrypoint minimal yang konsisten dengan architecture existing.

Jangan membuat dua worker entrypoint untuk fungsi yang sama.

Production flow harus kira-kira:

process
  ↓
bootstrap
  ↓
composition root
  ↓
runtime manager/driver
  ↓
Telegram runtime

Gunakan nama module yang sesuai dengan existing naming convention.

==================================================
BAGIAN 4 — INSTALLATION DISCOVERY
==================================================

Worker harus hanya menjalankan installation yang eligible.

Audit existing BotInstallation model/state.

Gunakan state yang SUDAH ADA.

Jangan mengubah:

`BotInstallation.status`

menjadi process state.

Bedakan:

installation lifecycle state
vs
runtime process state.

Worker hanya boleh membuat runtime untuk installation yang:

- enabled/active sesuai contract,
- memiliki valid session/connection,
- memiliki provider yang didukung,
- memiliki credential reference yang valid,
- tidak revoked,
- tidak disabled.

Jangan mengarang state baru.

Jika existing contract belum menyediakan eligibility query:

→ buat helper/query minimal hanya jika memang diperlukan oleh B-045 dan tetap menggunakan contract existing.

Jangan membuat database schema baru hanya untuk worker.

==================================================
BAGIAN 5 — TELEGRAM CLIENT CREATION
==================================================

WAJIB menggunakan:

TelegramClientFactory

dari B-044.

Jangan:

- instantiate Telegram SDK langsung,
- membaca token dari process.env di worker,
- membuat client object manual,
- bypass SecretResolver,
- bypass ProviderSessionDriver.

Flow:

installation/session
→ provider/session boundary
→ credential resolution
→ TelegramClientFactory
→ TelegramClient
→ runtime driver

Jika credential invalid:

worker harus menangani error dengan aman.

Jangan menampilkan raw credential.

==================================================
BAGIAN 6 — UPDATE ROUTING
==================================================

B-045 harus menghubungkan Telegram update dari client ke runtime execution.

Target:

Telegram SDK update
        ↓
adapter/normalizer
        ↓
normalized Telegram update
        ↓
runtime execution
        ↓
existing provider/session context

Jangan memasukkan Telegram SDK object ke core runtime.

Jika update type existing sudah tersedia:

→ gunakan.

Jika belum:

→ buat normalized update adapter minimum yang diperlukan.

Telegram SDK-specific types hanya boleh berada di provider boundary.

==================================================
BAGIAN 7 — NORMALIZED UPDATE
==================================================

Audit apakah repository sudah memiliki:

- `NormalizedTelegramUpdate`,
- generic `RuntimeUpdate`,
- provider update contract,
- update envelope.

Jika sudah:

→ gunakan existing contract.

Jika belum:

buat abstraction minimal.

Normalized update minimal harus mampu membawa informasi yang memang dibutuhkan runtime existing, misalnya:

- update identifier,
- update type,
- installation identity,
- provider identity,
- timestamp/context jika memang contract membutuhkan.

Jangan membawa seluruh raw Telegram SDK object ke core.

Jangan memasukkan credential ke update.

Jangan memasukkan raw authorization header.

Jangan memasukkan session secret.

==================================================
BAGIAN 8 — UPDATE ROUTING RULE
==================================================

Pastikan update hanya masuk ke runtime yang benar.

Routing harus menggunakan identity yang sudah tersedia:

- installation ID,
- workspace/account identity,
- provider identity,
- session/connection identity.

Jangan merutekan hanya berdasarkan:

- bot username,
- display name,
- user-supplied string.

Workspace isolation harus tetap berlaku.

Update dari installation A:

TIDAK BOLEH masuk ke runtime installation B.

Update dari workspace A:

TIDAK BOLEH diproses oleh workspace B.

==================================================
BAGIAN 9 — RUNTIME LIFECYCLE
==================================================

Gunakan lifecycle yang sudah dibuat B-042/B-043.

Worker harus menangani:

STARTING
RUNNING
STOPPING
STOPPED
FAILED

Hanya jika state tersebut memang sudah ada di architecture.

Jangan membuat state baru hanya untuk laporan.

Jika existing lifecycle abstraction sudah ada:

→ gunakan.

Worker tidak boleh membuat lifecycle system kedua.

==================================================
BAGIAN 10 — STARTUP
==================================================

Saat worker startup:

1. load configuration,
2. validate configuration,
3. initialize dependencies,
4. initialize runtime manager,
5. discover eligible installations,
6. initialize runtime untuk installation,
7. create Telegram client melalui factory,
8. attach update routing,
9. start runtime.

Jika satu installation gagal:

jangan otomatis membuat seluruh worker crash jika architecture memang mendukung isolation.

Gunakan failure isolation sesuai existing contract.

Jangan membuat retry scheduler baru.

Jika retry belum memiliki contract:

→ tandai deferred.

==================================================
BAGIAN 11 — SHUTDOWN
==================================================

Implementasikan graceful shutdown jika belum tersedia.

Tangani:

- SIGTERM,
- SIGINT.

Shutdown flow:

signal
→ stop accepting new runtime work
→ stop Telegram runtime/client
→ release resources
→ close persistence connections
→ exit cleanly

Jangan memanggil process.exit() sebelum cleanup selesai kecuali benar-benar diperlukan.

Jangan membuat shutdown system kedua jika existing lifecycle manager sudah menyediakan shutdown.

==================================================
BAGIAN 12 — MULTI-INSTALLATION
==================================================

Worker harus mampu menjalankan lebih dari satu Telegram installation berdasarkan architecture existing.

Setiap installation harus memiliki runtime isolation.

Jangan menggunakan global mutable Telegram client.

Gunakan:

installationId
→ runtime instance
→ Telegram client

Jika map/registry runtime memang diperlukan:

gunakan existing runtime registry.

Jika belum ada:

buat registry minimal hanya jika benar-benar diperlukan B-045.

Jangan membuat distributed runtime registry.

==================================================
BAGIAN 13 — DUPLICATE RUNTIME PROTECTION
==================================================

B-042/B-043 mungkin sudah memiliki guard.

Audit dan gunakan guard existing.

Pastikan worker tidak menjalankan dua runtime untuk installation yang sama secara tidak sengaja.

Jangan membuat distributed lock.

Jangan menambahkan Redis.

Jangan menambahkan PostgreSQL advisory lock.

Jangan membuat queue.

Jika distributed duplicate protection memang belum tersedia:

tetap gunakan local/in-process guard yang sudah tersedia.

Catat distributed multi-worker coordination sebagai deferred.

==================================================
BAGIAN 14 — POLLING / WEBHOOK
==================================================

B-044 sudah menyediakan Telegram client.

Sekarang audit apakah existing runtime contract menentukan:

- polling,
atau
- webhook.

Jika polling sudah ditentukan:

→ gunakan polling.

Jika webhook sudah ditentukan:

→ gunakan webhook.

Jika belum ditentukan:

pilih hanya satu mode untuk B-045 berdasarkan architecture existing.

Jangan implementasikan polling + webhook sekaligus.

Jangan membuat HTTP webhook server baru jika belum diperlukan oleh architecture.

Jika webhook infrastructure belum tersedia:

→ gunakan polling jika memang compatible dengan existing client/runtime contract.

Jika pilihan tidak dapat ditentukan tanpa contract baru:

→ jangan memaksa implementation speculative.

Laporkan dependency tersebut.

==================================================
BAGIAN 15 — ERROR HANDLING
==================================================

Worker harus aman terhadap:

- invalid credential,
- revoked session,
- Telegram initialization failure,
- Telegram connection failure,
- malformed update,
- runtime execution error,
- installation configuration error.

Error log harus berisi informasi diagnostik yang cukup tanpa secret.

Jangan log:

- Telegram bot token,
- session secret,
- API key,
- Authorization header,
- raw credential,
- full provider response jika mengandung secret.

==================================================
BAGIAN 16 — UPDATE ERROR ISOLATION
==================================================

Jika satu update gagal diproses:

jangan otomatis menghentikan seluruh worker.

Gunakan existing runtime error boundary.

Jika belum ada:

buat error boundary minimal di routing layer.

Target:

update
→ normalize
→ route
→ execute
→ catch/log sanitized error

Bukan:

update
→ exception
→ worker crash

Jangan membuat retry queue.

Retry/DLQ tetap DEFERRED jika contract belum tersedia.

==================================================
BAGIAN 17 — SECURITY
==================================================

Review:

- workspace isolation,
- installation isolation,
- credential boundary,
- session validation,
- provider ownership,
- disabled installation,
- revoked session,
- update routing,
- error sanitization,
- log sanitization.

Pastikan update tidak dapat digunakan untuk memilih installation arbitrary.

Pastikan installation ID berasal dari trusted runtime context.

Jangan menerima workspace/installation identity dari payload Telegram sebagai authority.

==================================================
BAGIAN 18 — TESTING
==================================================

Tambahkan test untuk:

1. Worker bootstrap berhasil.
2. Configuration validation.
3. No eligible installation.
4. One eligible installation.
5. Multiple installations.
6. Disabled installation tidak dijalankan.
7. Revoked session tidak dijalankan.
8. Invalid credential handling.
9. TelegramClientFactory dipanggil melalui dependency injection.
10. Telegram SDK tidak dibuat langsung oleh worker.
11. Update normalization.
12. Update routing.
13. Correct installation receives update.
14. Cross-installation routing ditolak.
15. Cross-workspace routing ditolak.
16. Malformed update tidak menghentikan worker.
17. Runtime execution error tidak menghentikan worker.
18. Graceful shutdown.
19. Duplicate runtime protection.
20. Credential tidak bocor ke error/log.

Gunakan fake:

- TelegramClientFactory,
- TelegramClient,
- runtime driver,
- repository,

untuk unit test.

Jangan membutuhkan Telegram production token.

==================================================
BAGIAN 19 — REAL TELEGRAM TEST
==================================================

Jika environment memiliki TEST-ONLY Telegram credentials:

dan repository memang memiliki integration test mechanism:

→ jalankan integration test.

Jika tidak:

`SKIPPED — real Telegram test credentials/environment unavailable`

Jangan:

- menggunakan production token,
- membuat token palsu,
- memasukkan token ke source,
- memasukkan token ke test fixture,
- commit credential.

==================================================
BAGIAN 20 — VALIDATION
==================================================

Setelah coding:

jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut tidak tersedia.

Jangan membuat script tersebut.

Jika repository memiliki integration test PostgreSQL:

dan:

PERSISTENCE_TEST_DATABASE_URL

tidak tersedia:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan membuat fake database.

==================================================
BAGIAN 21 — FORMAT / PARSER CHECK
==================================================

Karena sebelumnya repository pernah mengalami TypeScript parser failure:

jika build/typecheck gagal:

JANGAN langsung mengubah architecture.

Cari file yang menyebabkan error.

Lakukan:

- identify exact file,
- inspect surrounding syntax,
- check merge conflict markers,
- check malformed declarations,
- check illegal characters,
- run targeted TypeScript check jika tersedia.

Perbaiki hanya root cause.

Jangan melakukan broad rewrite.

==================================================
BAGIAN 22 — DIFF REVIEW
==================================================

Sebelum commit:

git status

git diff --stat

git diff

Pastikan perubahan hanya:

- worker bootstrap,
- update routing,
- normalized update adapter jika diperlukan,
- runtime wiring,
- lifecycle/shutdown,
- tests,
- documentation jika benar-benar diperlukan.

Hapus:

- debug code,
- temporary files,
- generated junk,
- credentials,
- unrelated refactor.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA provider,
- TokenHarbor,
- B-071,
- B-070,
- B-030.

==================================================
BAGIAN 23 — COMMIT
==================================================

Jika implementation valid dan validation PASS:

buat SATU commit.

Gunakan:

feat: bootstrap production telegram worker

atau commit message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 24 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

git status

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-045 dianggap selesai jika:

- Production worker bootstrap tersedia.
- Existing composition root digunakan.
- Existing TelegramClientFactory digunakan.
- Existing Telegram runtime driver digunakan.
- Eligible installation dapat ditemukan.
- Runtime per installation terisolasi.
- Telegram update dapat dinormalisasi.
- Update dapat diarahkan ke runtime yang benar.
- Cross-workspace routing dicegah.
- Disabled/revoked installation tidak dijalankan.
- Graceful shutdown tersedia.
- Duplicate local runtime dicegah.
- Error boundary tersedia.
- Tidak ada credential leakage.
- Unit test PASS.
- Build PASS.
- Typecheck PASS.
- Lint PASS.
- Format PASS.
- Imports PASS.
- Ownership PASS.
- Docs PASS.
- Diff check PASS.
- Commit berhasil.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

Jika real Telegram integration belum tersedia:

tetap:

`DEFERRED — real Telegram credentials/test environment unavailable`

Jangan menganggap ini sebagai implementation failure.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-045 STATUS

Worker bootstrap:
Status:

Composition root:
Status:

Installation discovery:
Status:

Telegram client:
Status:

Update normalization:
Status:

Update routing:
Status:

Lifecycle:
Status:

Shutdown:
Status:

### SECURITY

Credential handling:
Workspace isolation:
Installation isolation:
Disabled/revoked handling:
Error sanitization:
Log sanitization:

### TEST

Unit:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

Real Telegram integration:
PASS / SKIPPED / DEFERRED

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Tentukan task berikutnya berdasarkan dependency nyata setelah B-045.

Jangan kembali ke audit B-040 sampai B-044.
Jangan membuat architecture kedua.
Jangan membuat queue/DLQ speculative.
Jangan membuat distributed lock speculative.
Jangan mengerjakan fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-044 — Telegram SDK Selection + TelegramClientFactory
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR — B-043 SUDAH SELESAI
==================================================

B-040 Account Session Connection:
SELESAI.

B-041 Provider Session Adapter + Runtime Handoff:
SELESAI.

B-042 Runtime Execution:
SELESAI.

B-043 Real Telegram Runtime Driver boundary:
SELESAI.

Commit B-043:
8aeb3d5

Commit message:
feat: implement telegram runtime driver

Push:
OK

Local SHA == Remote SHA

Working tree:
CLEAN

Validation terakhir:
- Unit: PASS
- Build: PASS
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Imports: PASS
- Ownership: PASS
- Docs: PASS
- Diff: PASS

B-043 deferred karena:

- Real SDK-backed TelegramClientFactory/TelegramClient
  belum tersedia.
- Belum ada library/connector Telegram yang disetujui.
- Real provider credential exchange belum dapat dilakukan.
- Event/outbox masih deferred.
- Durable/distributed runtime scheduling masih deferred.

NEXT ROADMAP:

B-044 — real Telegram SDK-backed TelegramClientFactory.

==================================================
ATURAN UTAMA
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042
- B-043

Gunakan implementation existing sebagai source of truth.

Jangan membuat:

- RuntimeExecutionPort kedua.
- ProviderSessionDriver kedua.
- TelegramRuntimeExecutionDriver kedua.
- SecretResolver kedua.
- session manager kedua.
- authentication architecture kedua.
- queue system baru.
- outbox system baru.
- distributed lock system baru.

Fokus HANYA B-044.

==================================================
TUJUAN B-044
==================================================

Sekarang hilangkan dependency utama yang membuat B-043 deferred:

REAL TELEGRAM SDK/LIBRARY.

Target architecture:

RuntimeExecutionPort
        ↓
ProviderSessionDriver
        ↓
TelegramRuntimeExecutionDriver
        ↓
TelegramClientFactory
        ↓
TelegramClient
        ↓
Approved Telegram SDK/library

Factory harus menjadi boundary antara:

BotSpace runtime
dan
Telegram SDK.

Core BotSpace TIDAK BOLEH bergantung langsung pada Telegram SDK.

==================================================
BAGIAN 1 — AUDIT DEPENDENCY EXISTING
==================================================

Sebelum mengubah kode:

Audit:

- package.json
- pnpm-lock.yaml
- existing dependencies
- Telegram-related imports
- provider module
- TelegramRuntimeExecutionDriver
- ProviderSessionDriver
- RuntimeExecutionPort
- SecretResolver
- configuration
- composition root
- test doubles
- existing provider registry/factory.

Cari apakah project SUDAH memiliki:

- Telegram SDK,
- Telegram client library,
- Telegram bot library,
- Telegram connector,
- internal adapter,
- package yang sebelumnya dipakai untuk Telegram.

Jangan menginstall dependency baru sebelum audit selesai.

Jika library Telegram sudah ada:

→ gunakan library existing.

Jangan mengganti library tanpa alasan teknis yang kuat.

==================================================
BAGIAN 2 — PEMILIHAN LIBRARY
==================================================

Jika belum ada Telegram library:

Tentukan library yang paling tepat berdasarkan kebutuhan B-043/B-044:

- bot runtime,
- polling atau webhook,
- authenticated bot session,
- update handling,
- start/stop lifecycle,
- graceful shutdown,
- TypeScript compatibility,
- Node.js compatibility,
- maintenance status,
- security,
- compatibility dengan existing project.

Jangan memilih library hanya karena populer.

Prioritas:

1. kompatibel dengan existing architecture,
2. mendukung lifecycle yang dibutuhkan,
3. TypeScript support,
4. mudah di-test,
5. tidak memaksa architecture berubah,
6. dependency footprint wajar,
7. tidak memerlukan service eksternal tambahan.

Jika repository/project sudah memiliki preferred library:
→ ikuti repository.

Jika tidak ada preferred library:
→ pilih library yang paling minimal untuk kebutuhan BotSpace.

Jangan menambahkan beberapa Telegram library sekaligus.

Hanya SATU Telegram SDK/library yang menjadi implementation resmi.

==================================================
BAGIAN 3 — INSTALL DEPENDENCY
==================================================

Jika dependency baru benar-benar diperlukan:

gunakan package manager repository:

pnpm

Jangan menggunakan npm install jika repository menggunakan pnpm.

Jangan menggunakan yarn.

Jangan mengubah package manager.

Install dependency hanya setelah alasan pemilihannya jelas.

Setelah install:

- package.json berubah hanya sesuai kebutuhan,
- pnpm-lock.yaml diperbarui,
- jangan memasukkan dependency tidak terkait.

==================================================
BAGIAN 4 — TelegramClientFactory
==================================================

Implementasikan:

TelegramClientFactory

atau nama paling sesuai dengan existing naming convention.

Factory bertanggung jawab untuk:

- menerima configuration/session input yang aman,
- membuat Telegram SDK client,
- mengisolasi Telegram SDK API,
- mengembalikan Telegram client melalui abstraction yang dibutuhkan runtime.

Factory TIDAK BOLEH:

- menyimpan credential secara permanen,
- menulis token ke log,
- mengubah workspace state,
- mengubah installation state,
- mengatur billing,
- menjalankan worker,
- membuat scheduler.

Factory hanya membuat/configure client.

==================================================
BAGIAN 5 — CLIENT ABSTRACTION
==================================================

Audit apakah B-043 sudah menyediakan abstraction:

TelegramClient

atau equivalent.

Jika SUDAH:

→ gunakan abstraction tersebut.

Jika BELUM:

buat abstraction minimum yang benar-benar diperlukan.

Contoh behavior:

- start,
- stop,
- onUpdate,
- health/status jika memang diperlukan.

Jangan mengekspos Telegram SDK object langsung ke core.

Jangan membuat abstraction besar yang belum dibutuhkan.

==================================================
BAGIAN 6 — CREDENTIAL BOUNDARY
==================================================

WAJIB menggunakan existing credential architecture.

Credential harus berasal dari:

B-040/B-041
+
SecretResolver bila diperlukan.

Jangan membuat:

TELEGRAM_BOT_TOKEN langsung di runtime service.

Jangan membaca secret langsung dari:

process.env

di TelegramRuntimeExecutionDriver.

Jika configuration memang menggunakan environment variable:

→ environment variable hanya menjadi reference/configuration input.

Secret resolution tetap mengikuti existing SecretResolver boundary.

Raw secret hanya digunakan ketika membuat Telegram client.

Jangan menyimpan raw secret di:

- database,
- runtime handoff,
- event,
- status,
- error,
- logs.

==================================================
BAGIAN 7 — TELEGRAM BOT TOKEN
==================================================

Audit model session/connection.

Jangan mengasumsikan field baru.

Jika credential sudah direpresentasikan sebagai secret reference:

→ gunakan secret reference.

Jika SecretResolver membutuhkan key/reference:

→ resolve melalui resolver.

Jika credential model belum cukup:

JANGAN membuat database migration speculative.

Tandai:

DEFERRED — existing session credential contract insufficient.

Jangan memaksa schema baru hanya untuk menyelesaikan B-044.

==================================================
BAGIAN 8 — POLLING VS WEBHOOK
==================================================

Audit capability library yang dipilih.

Untuk B-044:

jangan implementasikan full production runtime execution jika scope factory belum memerlukannya.

Factory cukup memastikan client dapat dikonstruksi dengan mode runtime yang akan digunakan B-043.

Jika existing B-043 contract sudah memilih polling:

→ factory harus mendukung polling.

Jika existing contract memilih webhook:

→ factory harus mendukung webhook.

Jika belum ditentukan:

→ pilih mode yang paling sesuai dengan existing runtime architecture tanpa membuat dua implementation.

Jangan membuat polling + webhook architecture sekaligus jika belum diperlukan.

==================================================
BAGIAN 9 — RUNTIME LIFECYCLE
==================================================

TelegramClientFactory tidak boleh mengambil alih lifecycle B-042/B-043.

Lifecycle tetap:

Runtime
→ Driver
→ ClientFactory
→ Client

Bukan:

ClientFactory
→ Worker
→ Scheduler
→ Runtime

Start/stop tetap dikelola oleh runtime driver.

Factory hanya membuat client.

==================================================
BAGIAN 10 — ERROR HANDLING
==================================================

Pastikan factory dapat membedakan atau meneruskan error secara aman:

- invalid credential,
- invalid configuration,
- provider initialization failure,
- network configuration error,
- SDK initialization error.

Jangan bocorkan:

- token,
- Authorization header,
- secret,
- session secret,
- raw SDK request,
- sensitive configuration.

Error harus disanitasi sebelum keluar dari provider boundary jika library membocorkan credential dalam message.

==================================================
BAGIAN 11 — SDK TYPE ISOLATION
==================================================

Ini WAJIB.

Telegram SDK types tidak boleh menyebar ke:

- domain,
- application service,
- generic runtime contract,
- database model,
- HTTP response.

Telegram SDK types hanya boleh berada di:

- Telegram provider adapter,
- TelegramClientFactory,
- TelegramRuntimeExecutionDriver jika memang unavoidable.

Jika SDK type harus dikonversi:

buat mapper/adapter kecil.

Jangan memasukkan SDK dependency ke semua module.

==================================================
BAGIAN 12 — COMPOSITION ROOT
==================================================

Wire:

TelegramClientFactory
        ↓
TelegramRuntimeExecutionDriver
        ↓
Runtime worker/composition root.

Jangan membuat global singleton.

Gunakan dependency injection existing.

Production:

real TelegramClientFactory

Test:

fake/in-memory TelegramClientFactory

Jangan membuat test membutuhkan Telegram credential nyata.

==================================================
BAGIAN 13 — TESTING
==================================================

Tambahkan test untuk:

1. Factory construction.
2. Valid configuration.
3. Invalid configuration.
4. Client creation.
5. Credential reference handling.
6. SecretResolver integration.
7. Missing credential.
8. Resolver failure.
9. Credential tidak masuk error.
10. Credential tidak masuk log.
11. SDK client dibuat dengan configuration yang benar.
12. Factory tidak menyimpan credential secara tidak perlu.
13. Runtime driver menerima client dari factory.
14. Start/stop menggunakan existing lifecycle.
15. Duplicate runtime tetap dicegah oleh B-042/B-043.
16. Workspace isolation tetap berlaku.
17. Disabled installation tidak membuat client.
18. Revoked session tidak membuat client.
19. Telegram SDK type tidak bocor ke generic runtime contract.

Gunakan fake client untuk unit test.

Jangan memerlukan:

- real Telegram bot,
- production token,
- production Telegram account.

==================================================
BAGIAN 14 — REAL TELEGRAM INTEGRATION
==================================================

JANGAN menjalankan real Telegram integration test kecuali:

- environment memang menyediakan explicit test-only Telegram credentials,
- credential bukan production,
- repository sudah memiliki mekanisme test credential,
- test memang aman dijalankan.

Jika tidak tersedia:

SKIPPED — real Telegram credentials/environment unavailable.

Jangan membuat token palsu dan menganggapnya sebagai integration test.

Jangan memasukkan token ke repository.

==================================================
BAGIAN 15 — SECURITY REVIEW
==================================================

Review:

- dependency security,
- credential handling,
- token leakage,
- SDK initialization,
- error sanitization,
- logging,
- workspace isolation,
- session ownership,
- installation state,
- revoked credential,
- disabled installation.

Pastikan:

Tidak ada raw Telegram token dalam:

- source,
- test fixture,
- snapshot,
- log,
- error,
- event payload,
- database metadata,
- git diff.

==================================================
BAGIAN 16 — VALIDATION
==================================================

Setelah coding:

jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

JANGAN menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut tidak tersedia.

Jangan membuat script tersebut.

Jika ada PostgreSQL integration:

PERSISTENCE_TEST_DATABASE_URL

dan environment tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable.

Jangan membuat fake database.

==================================================
BAGIAN 17 — GIT REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Review seluruh perubahan.

Pastikan hanya:

- Telegram SDK dependency,
- TelegramClientFactory,
- Telegram client abstraction/adapter,
- composition wiring,
- tests,
- documentation jika memang diperlukan.

Hapus:

- debug,
- temporary files,
- generated junk,
- credential,
- unrelated refactor.

==================================================
BAGIAN 18 — COMMIT
==================================================

Jika implementasi valid dan validation PASS:

Buat SATU commit.

Gunakan:

feat: add telegram client factory

atau commit message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
BAGIAN 19 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- tampilkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-044 dianggap selesai jika:

- Telegram library yang dipilih jelas.
- Dependency terinstall dengan pnpm.
- TelegramClientFactory tersedia.
- Telegram client abstraction tersedia bila diperlukan.
- Credential menggunakan existing secure boundary.
- Telegram SDK terisolasi di provider boundary.
- Composition root sudah di-wire.
- Unit tests PASS.
- Build PASS.
- Typecheck PASS.
- Lint PASS.
- Format PASS.
- Imports PASS.
- Ownership PASS.
- Docs PASS.
- Diff check PASS.
- Tidak ada credential leakage.
- Commit dibuat.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

Jika real Telegram credentials/environment belum tersedia:

jangan menganggap integration test gagal.

Tampilkan:

Real Telegram integration:
DEFERRED — credentials/environment unavailable.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-044 STATUS

Telegram library:
Version:
Reason for selection:

TelegramClientFactory:
Status:

TelegramClient:
Status:

Credential boundary:
Status:

Composition root:
Status:

### SECURITY

Credential leakage:
SDK isolation:
Workspace isolation:
Session validation:
Installation validation:
Error sanitization:

### TEST

Unit:
Build:
Typecheck:
Lint:
Format:
Imports:
Ownership:
Docs:
Diff:

Real Telegram integration:
PASS / SKIPPED / DEFERRED

### GIT

Commit:
Push:
Local SHA:
Remote SHA:
Working tree:

### REMAINING DEFERRED

Hanya tampilkan dependency nyata yang belum tersedia.

### NEXT ROADMAP

Setelah B-044 selesai, tentukan task berikutnya berdasarkan dependency nyata.

Jangan kembali ke B-040 sampai B-043.
Jangan membuat architecture kedua.
Jangan membuat fake Telegram production runtime.
Jangan membuat queue/lock speculative.
Jangan menyentuh Gorouter.app.
Jangan mengerjakan fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-043 — Real Telegram RuntimeExecutionDriver + Runtime Integration
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR — B-042 SUDAH SELESAI
==================================================

B-040 Account Session Connection:
SUDAH SELESAI.

B-041 Provider Session Adapter + Runtime Handoff:
SUDAH SELESAI.

B-042 Runtime Execution:
SUDAH SELESAI.

Hasil B-042 terakhir:

- RuntimeExecutionPort sudah tersedia/terintegrasi.
- ProviderSessionDriver sudah terhubung.
- Runtime worker/orchestration sudah tersedia.
- Start/stop/restart lifecycle sudah diimplementasikan.
- Duplicate runtime prevention sudah tersedia.
- Workspace isolation sudah dijaga.
- Disabled/revoked session protection sudah tersedia.
- SecretResolver digunakan melalui secure boundary.
- Raw credential tidak dibawa melalui runtime handoff.
- Error handling sudah disanitasi.
- Composition root sudah di-wire.
- Unit test/runtime test PASS.
- Build PASS.
- Typecheck PASS.
- Lint PASS.
- Format PASS.
- Imports PASS.
- Ownership PASS.
- Docs PASS.
- Diff check PASS.

Commit B-042:
52a3f52

Push:
OK

Local SHA == Remote SHA

Working tree:
CLEAN

Deferred dari B-042:

1. Real Telegram RuntimeExecutionDriver
   - polling/webhook nyata,
   - real provider credential exchange.

2. Event/outbox runtime emission
   - outbox infrastructure belum tersedia.

3. Durable/distributed runtime scheduling
   - queue/lock infrastructure belum diperlukan/dipilih.

NEXT ROADMAP:
B-043 — Real Telegram RuntimeExecutionDriver.

==================================================
ATURAN PALING PENTING
==================================================

JANGAN mengulang:

- B-040
- B-041
- B-042

Gunakan implementation existing sebagai source of truth.

Jangan membuat architecture kedua.

Jangan membuat RuntimeExecutionPort kedua.

Jangan membuat ProviderSessionDriver kedua.

Jangan membuat SecretResolver kedua.

Jangan membuat worker system kedua.

Jangan membuat queue/lock infrastructure speculative.

==================================================
ATURAN PROVIDER
==================================================

WAJIB:

Jangan menjalankan atau membuat integration test Gorouter.app.

Jangan menggunakan Gorouter.app sebagai provider verification.

NVIDIA dan TokenHarbor.ai boleh diverifikasi hanya jika benar-benar tersentuh oleh perubahan, tetapi tidak perlu dijadikan target test.

Fokus B-043 hanya pada:

REAL TELEGRAM PROVIDER RUNTIME.

==================================================
TUJUAN B-043
==================================================

Implementasikan provider driver nyata:

ProviderSessionDriver
        ↓
Telegram RuntimeExecutionDriver
        ↓
Telegram provider/library
        ↓
polling/webhook runtime

Driver harus menggunakan boundary B-041/B-042.

Core BotSpace tidak boleh mengetahui detail SDK Telegram.

Target:

RuntimeExecutionPort
        ↓
ProviderSessionDriver
        ↓
TelegramRuntimeExecutionDriver
        ↓
Telegram SDK/library

Bukan:

Runtime
        ↓
Telegram SDK langsung

==================================================
1. TARGETED AUDIT
==================================================

Jangan melakukan full repository audit.

Audit hanya:

- B-041 ProviderSessionDriver.
- B-042 RuntimeExecutionPort.
- B-042 runtime worker.
- RuntimeHandoff.
- Session model.
- Connection model.
- Account model.
- BotInstallation.
- SecretResolver.
- provider registry/factory.
- composition root.
- dependency manifest/package.json.
- existing Telegram dependency jika ada.
- existing configuration.
- existing event/update abstraction.
- existing runtime lifecycle.
- existing tests.

Cari terlebih dahulu apakah Telegram library/provider implementation SUDAH ada.

JANGAN install dependency baru sebelum memastikan:

1. library belum tersedia,
2. architecture memang membutuhkan library tersebut,
3. library yang dipilih kompatibel dengan project,
4. tidak ada library existing yang sudah melakukan fungsi sama.

Jika library Telegram sudah tersedia:
→ gunakan library tersebut.

Jika tidak tersedia:
→ jangan memilih library secara sembarangan.

==================================================
2. TELEGRAM PROVIDER DRIVER
==================================================

Implementasikan concrete:

TelegramRuntimeExecutionDriver

atau nama yang paling sesuai dengan naming repository.

Driver harus memenuhi contract existing.

Driver bertanggung jawab untuk:

- initialize Telegram runtime,
- establish authenticated provider session,
- start polling/webhook sesuai capability,
- receive updates,
- process lifecycle,
- stop runtime,
- cleanup resource,
- expose safe runtime errors.

Provider-specific implementation harus tetap berada di provider/infrastructure boundary.

Jangan memasukkan Telegram SDK object ke:

- domain,
- service,
- API response,
- generic runtime DTO,
- database model.

==================================================
3. AUTHENTICATION / SESSION
==================================================

Gunakan session yang berasal dari:

B-040/B-041.

Jangan membuat authentication system baru.

Jangan menyimpan raw credential di:

- RuntimeHandoff,
- RuntimeExecutionPort,
- Runtime status,
- event,
- log,
- database metadata yang tidak ditujukan untuk credential.

Gunakan SecretResolver jika credential harus di-resolve.

Jika Telegram library membutuhkan credential/session material:

→ resolve melalui existing secure boundary.

Credential hanya berada di memory selama diperlukan.

==================================================
4. TELEGRAM BOT TOKEN
==================================================

Audit bagaimana Telegram bot credential/session direpresentasikan di repository.

Jangan mengasumsikan field baru.

Jika existing session model sudah menyediakan credential reference:
→ gunakan reference tersebut.

Jika existing SecretResolver menyimpan secret:
→ resolve secret berdasarkan reference.

Jangan memasukkan token langsung ke configuration source code.

Jangan menampilkan token.

Jangan membuat test token production.

==================================================
5. RUNTIME START
==================================================

Implementasikan start yang:

- validasi runtime handoff,
- validasi workspace/account/connection/session/install identity,
- memastikan installation memang boleh running,
- memastikan session masih valid,
- resolve credential melalui secure boundary,
- membuat Telegram provider client,
- start runtime,
- menyimpan runtime handle/reference hanya pada runtime layer.

Jika runtime sudah running:

→ jangan membuat runtime kedua.

Gunakan idempotency/concurrency mechanism dari B-042.

==================================================
6. RUNTIME STOP
==================================================

Stop harus:

- graceful,
- idempotent,
- menghentikan polling/webhook,
- unregister handler jika diperlukan,
- release connection/resource,
- membersihkan runtime handle,
- tidak menghapus account,
- tidak menghapus connection,
- tidak menghapus session,
- tidak revoke credential.

Runtime stop ≠ session revoke.

==================================================
7. RESTART
==================================================

Gunakan lifecycle B-042.

Restart harus:

- stop existing runtime,
- cleanup,
- start runtime baru,
- tidak membuat duplicate runtime.

Perhatikan race:

- start + start,
- start + stop,
- stop + stop,
- restart + stop,
- revoke + running,
- disconnect + running.

Jangan membuat distributed locking infrastructure baru.

Gunakan concurrency mechanism yang sudah tersedia.

==================================================
8. POLLING VS WEBHOOK
==================================================

Audit kemampuan library dan architecture.

Pilih mode yang memang didukung repository.

Jika polling adalah mode yang sudah cocok:

→ implementasikan polling.

Jika webhook boundary sudah tersedia dan memang siap:

→ implementasikan webhook.

JANGAN membangun polling DAN webhook sekaligus jika salah satunya belum diperlukan.

Jika library/provider hanya memungkinkan salah satu:
→ gunakan yang tersedia.

Jika real provider execution membutuhkan dependency yang benar-benar belum tersedia:

JANGAN membuat fake production implementation.

Implementasikan boundary yang dapat dilakukan dan tandai:

DEFERRED:
Real Telegram RuntimeExecutionDriver — dependency unavailable.

==================================================
9. UPDATE HANDLING
==================================================

Audit bagaimana runtime menerima Telegram updates.

Jika B-042 sudah memiliki generic runtime callback/event boundary:

→ gunakan boundary tersebut.

Telegram-specific update object harus dikonversi di provider adapter.

Jangan membocorkan Telegram SDK types ke core.

Contoh:

Telegram Update
    ↓
Telegram adapter
    ↓
Generic RuntimeUpdate
    ↓
Bot runtime

Jika generic update contract belum tersedia:

Jangan membuat event architecture besar.

Buat abstraction minimum yang benar-benar diperlukan untuk menjalankan driver.

==================================================
10. ERROR HANDLING
==================================================

Map provider error menjadi safe internal runtime error.

Bedakan minimal jika library dapat membedakan:

- authentication failure,
- invalid token/session,
- provider unavailable,
- network failure,
- polling failure,
- webhook failure,
- rate limit,
- runtime shutdown,
- unexpected provider error.

Jangan membocorkan:

- bot token,
- session token,
- credential,
- HTTP Authorization header,
- raw secret,
- internal provider request details.

Error log harus aman.

==================================================
11. RECONNECT
==================================================

Audit apakah existing runtime contract sudah memiliki reconnect semantics.

Jika sudah:

→ implementasikan sesuai contract.

Jika belum:

→ jangan membuat reconnect framework besar.

Gunakan behavior minimum yang dibutuhkan oleh Telegram library.

Perhatikan:

- transient network failure,
- authentication failure,
- intentional stop.

Authentication failure jangan terus-menerus retry.

Intentional stop tidak boleh otomatis restart.

==================================================
12. GRACEFUL SHUTDOWN
==================================================

Pastikan runtime dapat dihentikan ketika:

- stop command,
- runtime shutdown,
- application shutdown,
- session revoked,
- installation disabled,
- provider failure.

Gunakan existing lifecycle.

Jangan membuat process manager baru.

==================================================
13. SESSION INVALIDATION
==================================================

Jika session:

- revoked,
- disconnected,
- invalid,
- credential unavailable,

runtime tidak boleh terus menggunakan session tersebut.

Jika Telegram runtime aktif:

→ lakukan stop.

Jangan mengubah lifecycle account secara otomatis kecuali existing contract memang mengharuskannya.

==================================================
14. WORKSPACE ISOLATION
==================================================

WAJIB diuji.

Workspace A:

account A
connection A
session A
installation A
runtime A

tidak boleh mengakses:

account B
connection B
session B
installation B
runtime B

Pastikan driver tidak hanya percaya pada ID dari caller.

Gunakan authorization/ownership boundary B-040/B-041/B-042.

Jangan membuat authorization system kedua.

==================================================
15. INSTALLATION STATE
==================================================

Jangan menggunakan:

BotInstallation.status

sebagai runtime process state.

Installation lifecycle tetap terpisah dari:

RuntimeState.

Runtime hanya boleh start jika installation state sesuai dengan existing contract.

Jangan mengubah schema/state machine installation kecuali benar-benar diperlukan oleh existing contract.

==================================================
16. PROVIDER FACTORY / REGISTRY
==================================================

Jika repository sudah memiliki provider registry:

tambahkan Telegram driver di sana.

Contoh konsep:

provider = telegram
driver = TelegramRuntimeExecutionDriver

Jangan membuat factory kedua.

Jika provider registry belum ada:

buat abstraction minimum hanya jika B-043 benar-benar membutuhkannya.

Jangan membuat generic plugin framework besar.

==================================================
17. COMPOSITION ROOT
==================================================

Wire production:

TelegramRuntimeExecutionDriver
        ↓
ProviderSessionDriver
        ↓
RuntimeExecutionPort
        ↓
Worker

Pastikan dependency injection eksplisit.

Test environment harus dapat menggunakan:

FakeProviderSessionDriver
FakeRuntimeExecutionDriver

tanpa Telegram credential.

Jangan menggunakan environment production dalam unit tests.

==================================================
18. TESTING
==================================================

Tambahkan unit tests yang benar-benar memverifikasi:

1. Telegram driver construction.
2. Valid runtime handoff.
3. Invalid runtime handoff rejected.
4. Start runtime.
5. Start idempotency.
6. Duplicate runtime prevention.
7. Stop runtime.
8. Stop idempotency.
9. Restart runtime.
10. Provider authentication failure.
11. Provider network failure.
12. Provider unavailable.
13. Credential unavailable.
14. SecretResolver failure.
15. Session revoked.
16. Session disconnected.
17. Installation disabled.
18. Workspace isolation.
19. Cross-workspace rejection.
20. Runtime cleanup.
21. Intentional stop does not reconnect.
22. Runtime failure state.
23. Credential tidak masuk log.
24. Credential tidak masuk error.
25. Credential tidak masuk runtime handoff.
26. Telegram SDK object tidak bocor ke core.
27. Composition root wiring.

Jika provider library menyediakan testable fake client:

→ gunakan untuk unit test.

Jika tidak:

→ buat adapter-level test double, bukan fake production provider.

==================================================
19. REAL TELEGRAM INTEGRATION TEST
==================================================

JANGAN menggunakan production Telegram account.

Jika repository/environment memiliki explicit test-only Telegram credentials:

→ hanya jalankan real integration test jika memang sudah menjadi bagian testing architecture.

Jika tidak tersedia:

→ SKIPPED — real Telegram credentials/environment unavailable.

Jangan membuat credential palsu.

Jangan memasukkan token ke repository.

Jangan menjalankan real Telegram test hanya untuk membuat laporan terlihat lengkap.

==================================================
20. EVENT / OUTBOX
==================================================

Audit event/outbox.

Jika infrastructure belum tersedia:

JANGAN membuat outbox system baru.

Runtime event emission tetap:

DEFERRED — outbox infrastructure unavailable.

Jika event contract sudah tersedia dan mudah diintegrasikan tanpa infrastructure baru:

gunakan contract existing.

Jangan memasukkan credential ke event payload.

==================================================
21. DURABLE SCHEDULING
==================================================

Jangan implementasikan:

- Redis lock,
- distributed scheduler,
- durable queue,
- persistent worker orchestration,

pada B-043 jika infrastructure tersebut belum tersedia.

Tetap:

DEFERRED — durable runtime scheduling requires approved infrastructure.

==================================================
22. SECURITY REVIEW
==================================================

Review khusus:

- credential leakage,
- token leakage,
- session leakage,
- workspace isolation,
- cross-account runtime,
- revoked session,
- disabled installation,
- duplicate runtime,
- stale runtime,
- reconnect loop,
- provider error sanitization,
- shutdown behavior.

Pastikan tidak ada:

token di log
token di event
token di error
token di test snapshot
token di API response

==================================================
23. VALIDATION
==================================================

Setelah coding:

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

JANGAN menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut tidak tersedia.

Jangan membuat script pengganti.

Jika PostgreSQL integration membutuhkan:

PERSISTENCE_TEST_DATABASE_URL

dan tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable.

Jangan membuat fake database.

==================================================
24. GIT REVIEW
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan B-043.

Hapus:

- debug,
- temporary files,
- credentials,
- tokens,
- generated files,
- unrelated refactor.

Jangan menyentuh:

- Gorouter.app,
- NVIDIA provider implementation yang tidak relevan,
- TokenHarbor implementation yang tidak relevan.

==================================================
25. COMMIT
==================================================

Jika implementation valid dan validation selesai:

buat SATU commit.

Gunakan:

feat: implement telegram runtime driver

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
26. PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote branch SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah credential Git sembarangan,
- laporkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-043 selesai jika:

- TelegramRuntimeExecutionDriver tersedia.
- ProviderSessionDriver terintegrasi.
- RuntimeExecutionPort terintegrasi.
- Telegram provider client dapat dibuat melalui secure boundary.
- Start/stop/restart berjalan.
- Duplicate runtime dicegah.
- Workspace isolation terjaga.
- Revoked/disconnected session tidak menjalankan runtime.
- Disabled installation tidak menjalankan runtime.
- Error provider disanitasi.
- Credential tidak bocor.
- Graceful shutdown tersedia.
- Unit tests tersedia.
- Validation PASS.
- Commit dibuat.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

Jika real Telegram library/credential/environment belum tersedia:

IMPLEMENTED:
- driver boundary,
- provider integration architecture,
- runtime lifecycle,
- secure credential resolution,
- tests,
- composition wiring.

DEFERRED:
- actual Telegram network execution,
- real polling/webhook,
- real provider credential exchange,

hanya jika dependency nyata memang unavailable.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-043 STATUS
- TelegramRuntimeExecutionDriver:
- ProviderSessionDriver:
- RuntimeExecutionPort:
- Start:
- Stop:
- Restart:
- Reconnect:
- Graceful shutdown:

### SECURITY
- Credential handling:
- SecretResolver:
- Workspace isolation:
- Session validation:
- Installation validation:
- Error sanitization:

### TEST
- Unit:
- Integration:
- Build:
- Typecheck:
- Lint:
- Format:
- Imports:
- Ownership:
- Docs:
- Diff:

### DEFERRED
Hanya item yang benar-benar membutuhkan external dependency/environment.

### GIT
- Commit:
- Push:
- Local SHA:
- Remote SHA:
- Working tree:

### NEXT ROADMAP
Tentukan task berikutnya berdasarkan dependency nyata setelah B-043.

PENTING:

Jangan kembali ke B-040.
Jangan kembali ke B-041.
Jangan kembali ke B-042.
Jangan meminta human approval untuk task yang sudah jelas.
Jangan membuat fake production Telegram runtime.
Jangan menjalankan test Gorouter.app.
Jangan membuat queue/lock infrastructure speculative.
Jangan mengerjakan fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-042 — Runtime Execution + Provider Driver
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
KONDISI TERAKHIR — B-041 SUDAH SELESAI
==================================================

B-040 Account Session Connection:
SUDAH SELESAI.

B-041 Provider Session Adapter + Runtime Handoff:
SUDAH SELESAI.

Hasil B-041 terakhir:

- Provider session adapter boundary implemented.
- ProviderSessionDriver/runtime handoff boundary implemented.
- Session lifecycle terhubung ke adapter.
- SecretResolver boundary digunakan.
- Runtime handoff menggunakan identifier/reference aman.
- Raw credential tidak dibawa dalam handoff.
- Workspace isolation dipertahankan.
- Error sanitization diterapkan.
- Test PASS.
- Build PASS.
- Typecheck PASS.
- Lint PASS.
- Format PASS.
- Imports PASS.
- Ownership PASS.
- Docs PASS.
- Diff check PASS.
- PostgreSQL integration SKIPPED jika environment tidak tersedia.
- Real Telegram provider driver + real session credential exchange masih deferred jika library/credential nyata belum tersedia.
- Real bot runtime polling/webhook masih deferred jika runtime environment belum tersedia.
- Outbox/event delivery masih deferred jika infrastructure belum tersedia.
- Secret manager vendor integration masih deferred jika deployment dependency belum tersedia.

Commit terakhir:
0e30a28

Push:
OK

Local SHA == Remote SHA

Working tree:
CLEAN

JANGAN mengulang B-040.
JANGAN mengulang B-041.
JANGAN meminta approval untuk B-040/B-041.

==================================================
TARGET SEKARANG
==================================================

Implementasikan:

B-042 — Runtime Execution

Fokus:

ProviderSessionDriver
        ↓
Runtime Execution Capability
        ↓
Bot Runtime
        ↓
Polling/Webhook/Worker execution
        ↓
Lifecycle + stop/restart/revoke

Tujuan B-042 adalah membuat runtime execution boundary nyata tanpa mencampurkan:

- account lifecycle,
- session lifecycle,
- provider authentication,
- bot installation lifecycle,
- runtime process lifecycle.

==================================================
ATURAN UTAMA
==================================================

Jangan membuat fake production Telegram runtime.

Jika provider/library nyata tersedia:
→ gunakan secara modular.

Jika provider/library nyata BELUM tersedia:
→ implementasikan runtime execution abstraction, worker lifecycle, driver contract, composition wiring, dan tests yang dapat dilakukan sekarang.

Jangan menyatakan real Telegram runtime berhasil jika sebenarnya dependency eksternal belum tersedia.

Pisahkan:

IMPLEMENTED

dan

DEFERRED — external dependency unavailable

secara jelas.

==================================================
1. TARGETED INSPECTION
==================================================

Audit hanya bagian yang relevan:

- B-040 session implementation.
- B-041 provider session adapter.
- ProviderSessionDriver.
- RuntimeHandoffPort.
- BotInstallation.
- Worker module.
- runtime module.
- process/runtime abstraction yang sudah ada.
- composition root.
- configuration.
- SecretResolver.
- provider ownership boundary.
- existing queue/worker abstraction.
- existing polling/webhook capability jika tersedia.
- roadmap B-042.

Jangan melakukan full repository audit.

Gunakan implementation B-040 dan B-041 sebagai source of truth.

==================================================
2. RUNTIME EXECUTION CONTRACT
==================================================

Pastikan runtime memiliki boundary yang jelas.

Target arsitektur:

Account
  ↓
Connection
  ↓
Session
  ↓
ProviderSessionDriver
  ↓
RuntimeHandoff
  ↓
RuntimeExecutionPort
  ↓
Bot Runtime

RuntimeExecutionPort minimal harus dapat menangani lifecycle yang memang dibutuhkan:

- start
- stop
- restart
- status/health jika architecture membutuhkan
- graceful shutdown
- failure handling

Jangan membuat method yang tidak diperlukan.

Jangan membuat duplicate runtime abstraction jika repository sudah memiliki abstraction yang sesuai.

==================================================
3. BOTINSTALLATION VS RUNTIME STATE
==================================================

Sangat penting:

JANGAN mengubah:

BotInstallation.status

menjadi runtime process state.

Installation lifecycle dan runtime lifecycle harus tetap berbeda.

Contoh konsep:

BotInstallation:
- configured
- enabled
- disabled
- revoked
- dll sesuai existing contract

Runtime:
- starting
- running
- stopping
- stopped
- failed

Jangan menambahkan state baru jika contract existing sudah cukup.

Jika runtime state abstraction belum ada:
→ buat boundary minimum yang benar-benar diperlukan.

==================================================
4. PROVIDER SESSION DRIVER
==================================================

Gunakan ProviderSessionDriver dari B-041.

Driver bertanggung jawab terhadap provider-specific execution.

Core runtime tidak boleh mengetahui detail SDK provider.

Target:

Runtime
   ↓
ProviderSessionDriver
   ↓
Telegram/provider implementation

Bukan:

Runtime
   ↓
Telegram SDK directly

Provider-specific objects tidak boleh bocor ke:

- domain,
- API response,
- generic runtime interface,
- database model.

==================================================
5. REAL TELEGRAM PROVIDER
==================================================

Audit dependency Telegram/provider.

Jika library Telegram nyata SUDAH tersedia:

- implementasikan driver nyata,
- gunakan existing dependency,
- jangan menambahkan library kedua yang melakukan fungsi sama,
- jangan membuat fake Telegram client,
- jangan menggunakan production credential dalam unit test.

Driver harus dapat:

- establish provider runtime,
- receive/update events jika library mendukung,
- graceful stop,
- reconnect jika provider/runtime contract mendukung,
- report failure secara aman.

Jika library nyata BELUM tersedia:

JANGAN menginstall dependency hanya berdasarkan tebakan.

Implementasikan:

- ProviderSessionDriver contract,
- runtime execution boundary,
- worker orchestration,
- lifecycle,
- fake/in-memory driver untuk unit tests,
- composition boundary.

Kemudian:

DEFERRED:
Real Telegram provider driver/runtime execution — provider library/environment unavailable.

==================================================
6. RUNTIME HANDOFF
==================================================

Gunakan handoff dari B-041.

Handoff harus tetap scoped:

- workspaceId
- accountId
- connectionId
- sessionId
- provider
- installationId jika tersedia

Jangan membawa:

- password
- API key
- access token
- session token
- raw credential
- provider secret

Runtime harus resolve credential melalui secure boundary bila memang diperlukan.

Jangan menambahkan credential ke runtime handoff DTO hanya agar implementation lebih mudah.

==================================================
7. SECRETRESOLVER
==================================================

Gunakan SecretResolver existing.

Jangan membuat resolver kedua.

Runtime/provider driver harus mendapatkan credential hanya melalui boundary yang benar.

Pastikan:

- missing secret → safe failure.
- resolver error → safe failure.
- secret tidak masuk log.
- secret tidak masuk event.
- secret tidak masuk runtime status.
- secret tidak masuk API response.
- secret tidak masuk error string.

Jangan mencetak credential untuk debugging.

==================================================
8. RUNTIME WORKER
==================================================

Jika worker module sudah tersedia:

gunakan worker tersebut.

Jangan membuat worker system kedua.

Worker harus dapat:

1. menerima runtime handoff,
2. memvalidasi workspace/session/install identity,
3. start runtime,
4. track runtime state,
5. stop runtime,
6. handle runtime failure,
7. cleanup resource.

Jika queue sudah tersedia:
→ gunakan queue.

Jika queue belum tersedia:
→ jangan membuat queue infrastructure besar secara speculative.

Gunakan synchronous capability/boundary yang architecture repository sudah dukung.

==================================================
9. START
==================================================

Start runtime harus:

- authorization-safe,
- idempotent sesuai contract,
- tidak membuat duplicate runtime,
- tidak membuat duplicate provider session,
- tidak menjalankan runtime untuk installation yang disabled/revoked,
- tidak menggunakan session workspace lain.

Jika runtime sudah running:

→ jangan membuat process kedua.

Ikuti existing idempotency semantics.

==================================================
10. STOP
==================================================

Stop harus:

- graceful,
- idempotent,
- membersihkan runtime resource,
- tidak menghapus session credential,
- tidak mengubah account lifecycle secara tidak semestinya.

Stop runtime ≠ revoke account.

Stop runtime ≠ delete connection.

Stop runtime ≠ delete session.

==================================================
11. RESTART
==================================================

Restart harus aman terhadap race condition.

Perhatikan:

- restart saat starting,
- restart saat stopping,
- stop saat starting,
- revoke saat running,
- disconnect saat runtime running,
- installation disable saat runtime running.

Jangan membuat duplicate runtime.

Gunakan concurrency mechanism yang sudah tersedia.

Jangan menambahkan distributed lock dependency speculative.

==================================================
12. REVOKE / DISCONNECT
==================================================

Integrasikan lifecycle B-040/B-041.

Jika session:

- revoked,
- disconnected,
- invalid,
- credential unavailable,

runtime tidak boleh terus berjalan menggunakan credential/session yang sudah tidak valid.

Jika runtime sedang berjalan dan session direvoke:

→ lakukan graceful stop sesuai capability yang tersedia.

Jangan mengubah account/session state hanya karena runtime stop.

==================================================
13. FAILURE HANDLING
==================================================

Runtime failure harus diterjemahkan menjadi safe internal state.

Bedakan:

- authentication failure,
- credential unavailable,
- provider unavailable,
- runtime crash,
- invalid session,
- invalid installation,
- authorization failure,
- lifecycle conflict.

Jangan menyimpan raw provider exception jika tidak diperlukan.

Jangan mengirim raw stack trace ke API client.

Jangan memasukkan credential/token ke error.

==================================================
14. RUNTIME STATUS
==================================================

Jika architecture membutuhkan runtime status:

gunakan dedicated runtime state.

Jangan menaruh runtime process state di BotInstallation.status.

Status harus cukup untuk:

- starting,
- running,
- stopping,
- stopped,
- failed

hanya jika memang dibutuhkan oleh implementation.

Jangan menambahkan state yang tidak memiliki consumer.

==================================================
15. HEALTH / HEARTBEAT
==================================================

Audit apakah existing runtime architecture sudah memiliki:

- heartbeat,
- health check,
- worker liveness,
- process status.

Jika sudah:
→ integrasikan.

Jika belum:
→ jangan membangun monitoring platform besar.

Implementasikan hanya minimal health/status capability yang dibutuhkan B-042.

==================================================
16. POLLING / WEBHOOK
==================================================

Jika provider library nyata tersedia dan architecture memang mendukung polling:

implementasikan polling melalui provider driver.

Jika architecture mendukung webhook:

gunakan existing HTTP/webhook boundary.

Jangan membuat kedua mode sekaligus jika belum diperlukan.

Pilih mode yang memang didukung architecture.

Jika provider runtime belum tersedia:

DEFERRED:
real polling/webhook execution.

Jangan membuat fake HTTP webhook production.

Jangan membuat fake Telegram polling yang mengklaim production-ready.

==================================================
17. EVENT / OUTBOX
==================================================

Audit event/outbox infrastructure.

Jika tersedia:

gunakan contract existing.

Event yang relevan dapat mencakup:

- runtime started,
- runtime stopped,
- runtime failed,

hanya jika existing event architecture mendukung.

Jangan membuat event system baru.

Jangan memasukkan secret dalam payload.

Jika outbox belum tersedia:

jangan membuat full outbox implementation speculative.

Tandai:

DEFERRED — outbox delivery infrastructure unavailable.

==================================================
18. WORKSPACE ISOLATION
==================================================

Test:

Workspace A runtime
tidak boleh:

- memakai session Workspace B,
- memakai account Workspace B,
- memakai installation Workspace B,
- membaca credential Workspace B,
- menjalankan provider runtime Workspace B.

Gunakan authorization boundary B-040/B-041.

Jangan membuat authorization system kedua.

==================================================
19. ACTOR ATTRIBUTION
==================================================

Jika runtime start dipicu oleh actor:

gunakan existing actor context.

Jangan membuat arbitrary identity string.

Jika existing actor context tidak diperlukan untuk internal worker execution:
→ jangan menambahkannya secara speculative.

==================================================
20. COMPOSITION ROOT
==================================================

Wire:

ProviderSessionDriver
        ↓
RuntimeExecutionPort
        ↓
Worker
        ↓
Bot Runtime

Production:

real driver jika dependency tersedia.

Test:

fake/in-memory driver.

Pastikan dependency injection dapat diuji tanpa provider credential nyata.

Jangan membuat global singleton tersembunyi.

==================================================
21. TESTING
==================================================

Tambahkan test behavior nyata.

Minimal:

1. runtime start success.
2. runtime start idempotency.
3. runtime stop success.
4. runtime stop idempotency.
5. runtime restart.
6. duplicate runtime prevention.
7. invalid installation rejected.
8. disabled installation rejected.
9. revoked session rejected.
10. disconnected session rejected.
11. workspace isolation.
12. cross-workspace runtime rejected.
13. provider failure mapping.
14. credential unavailable handling.
15. SecretResolver failure handling.
16. credential tidak masuk runtime handoff.
17. credential tidak masuk error.
18. runtime failure state.
19. graceful cleanup.
20. concurrent start protection.
21. stop during start.
22. restart during stop.
23. revoke while runtime active.
24. disconnect while runtime active.
25. composition root wiring.
26. fake driver test.
27. real provider driver test jika dependency/environment nyata tersedia.

Jangan menggunakan production Telegram account.

==================================================
22. PROVIDER TEST SAFETY
==================================================

WAJIB:

Jangan menjalankan integration test Gorouter.app.

Jangan menyentuh Gorouter.app.

NVIDIA dan TokenHarbor tidak perlu disentuh.

Jika shared provider infrastructure berubah secara langsung:
→ hanya lakukan verification yang benar-benar diperlukan.

Jangan membuat test provider yang tidak relevan.

==================================================
23. VALIDATION
==================================================

Setelah coding selesai jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check
node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan:

node scripts/check-symlinks.mjs

karena script tersebut tidak tersedia.

Jika:

PERSISTENCE_TEST_DATABASE_URL

tersedia:

→ jalankan integration test PostgreSQL yang memang sudah ada.

Jika tidak tersedia:

→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable.

Jangan membuat fake PostgreSQL.

==================================================
24. SECURITY REVIEW
==================================================

Sebelum commit periksa:

- credential leakage,
- secret leakage,
- provider object leakage,
- cross-workspace runtime,
- duplicate runtime,
- stale session,
- revoked session still running,
- disabled installation still running,
- raw provider error leakage,
- runtime handoff leakage,
- unsafe process cleanup.

==================================================
25. REVIEW DIFF
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Hapus:

- debug code,
- temporary files,
- credentials,
- secrets,
- generated junk,
- unrelated refactor.

Pastikan hanya B-042 yang berubah.

==================================================
26. COMMIT
==================================================

Jika implementation valid:

buat SATU commit.

Gunakan:

feat: implement runtime execution

atau commit message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
27. PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian:

git rev-parse HEAD

Verifikasi remote branch SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah Git credential sembarangan,
- laporkan error,
- pastikan commit lokal tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-042 dianggap selesai apabila:

- RuntimeExecutionPort tersedia/terintegrasi.
- ProviderSessionDriver terhubung.
- Worker/runtime orchestration terhubung.
- Start/stop/restart lifecycle tersedia.
- Duplicate runtime dicegah.
- Workspace isolation terjaga.
- Disabled/revoked session tidak dapat menjalankan runtime.
- SecretResolver digunakan melalui secure boundary.
- Raw credential tidak masuk handoff.
- Error handling aman.
- Composition root ter-wire.
- Tests tersedia.
- Validation PASS.
- Commit dibuat.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

Jika real Telegram/provider runtime belum tersedia:

IMPLEMENTED:
- runtime abstraction,
- worker lifecycle,
- driver boundary,
- orchestration,
- security,
- tests,
- composition wiring.

DEFERRED:
- real Telegram/provider execution,
- real polling/webhook,
- real provider credential exchange,
- outbox delivery,

hanya jika dependency tersebut memang benar-benar belum tersedia.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-042 STATUS
- RuntimeExecutionPort:
- ProviderSessionDriver:
- Worker:
- Start/Stop/Restart:
- Runtime state:
- Composition root:

### SECURITY
- Workspace isolation:
- Credential protection:
- SecretResolver:
- Runtime handoff:
- Revoked/disabled protection:

### TEST
- Unit:
- Integration:
- Build:
- Typecheck:
- Lint:
- Format:
- Imports:
- Ownership:
- Docs:
- Diff:

### DEFERRED
Hanya dependency eksternal yang benar-benar unavailable.

### GIT
- Commit:
- Push:
- Local SHA:
- Remote SHA:
- Working tree:

### NEXT ROADMAP
Tentukan task berikutnya berdasarkan dependency nyata setelah B-042.

PENTING:

Jangan kembali ke B-040.
Jangan kembali ke B-041.
Jangan meminta human approval.
Jangan membuat fake production Telegram runtime.
Jangan menjalankan test Gorouter.app.
Jangan menyentuh provider yang tidak relevan.
Jangan membuat fitur acak.

Kerjakan langsung pada:

/root/botspace

```
# Prompt: B-041 — Provider Session Adapter + Runtime Handoff
```

# PROMPT: B-041 — PROVIDER SESSION ADAPTER + RUNTIME HANDOFF

Lanjutkan project BotSpace dari kondisi repository SAAT INI:

/root/botspace

Branch:
backend-dev-recovery

==================================================
CURRENT VERIFIED STATE
==================================================

B-040 / ADR-011 Account Session Connection SUDAH SELESAI.

Verified dari implementation terakhir:

- B-040 implemented.
- Account model implemented.
- Connection model implemented.
- Session model implemented.
- Lifecycle implemented.
- Workspace authorization implemented.
- Credential boundary implemented.
- SecretResolver boundary integrated.
- Security behavior implemented.
- Tests PASS.
- Build PASS.
- Typecheck PASS.
- Imports/ownership/docs validation PASS.
- Commit berhasil:
  4ca3f6f
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

JANGAN mengulang B-040.

JANGAN melakukan audit B-040 dari awal.

JANGAN meminta human approval lagi untuk B-040.

==================================================
REMAINING DEFERRED
==================================================

Dari hasil B-040, remaining deferred adalah:

1. Real Telegram/provider library + real session credential exchange.
2. Event/outbox emission karena infrastructure belum tersedia.
3. Runtime handoff ke polling/webhook/queue.
4. Secret manager vendor selection/deployment integration.

Roadmap berikutnya:

B-041 — provider session adapter + runtime handoff.

==================================================
PRIMARY OBJECTIVE
==================================================

Sekarang implementasikan B-041.

Fokus:

PROVIDER SESSION ADAPTER
+
RUNTIME HANDOFF CAPABILITY

Tujuan B-041:

Memisahkan:

Account/Connection/Session lifecycle
DARI
provider-specific authentication/session runtime
DAN
Bot runtime execution.

Architecture target:

Workspace
  ↓
Account
  ↓
Connection
  ↓
Session
  ↓
Provider Session Adapter
  ↓
Runtime Handoff Capability
  ↓
Bot Runtime

JANGAN mencampurkan semua layer menjadi satu service.

==================================================
IMPORTANT — DO NOT REPEAT AUDIT LOOP
==================================================

Jangan berhenti dengan:

- "B-041 needs approval"
- "provider belum tersedia"
- "runtime belum tersedia"
- "implementation blocked"

Jika external provider/runtime dependency tersedia:
→ implementasikan.

Jika external provider/runtime dependency BELUM tersedia:
→ implementasikan seluruh abstraction, adapter boundary, capability contract, lifecycle integration, test, dan composition-root integration yang dapat dilakukan sekarang.

Hanya bagian yang benar-benar membutuhkan external infrastructure boleh diberi status:

DEFERRED — external dependency unavailable.

Jangan memblokir seluruh B-041 hanya karena provider credentials atau runtime environment belum tersedia.

Jangan membuat fake production provider.

==================================================
STEP 1 — TARGETED REPOSITORY INSPECTION
==================================================

Audit hanya bagian yang relevan dengan B-041:

- B-040 account/session implementation,
- ADR-011,
- B-041 roadmap,
- provider abstraction yang sudah ada,
- SecretResolver,
- account/session repository,
- runtime module,
- worker module,
- BotInstallation,
- runtime composition root,
- existing provider boundaries,
- existing event/outbox boundary jika ada.

JANGAN melakukan full repository audit.

JANGAN mengubah modul yang tidak berkaitan.

Gunakan implementation B-040 sebagai source of truth.

==================================================
STEP 2 — PROVIDER SESSION PORT
==================================================

Buat atau gunakan provider session abstraction yang tepat.

Jangan membuat abstraction kedua jika repository sudah memiliki provider/session port yang sesuai.

Provider session adapter harus bertanggung jawab terhadap provider-specific behavior seperti:

- authenticate,
- establish session,
- reconnect,
- disconnect,
- revoke,
- session health/status,
- credential/session material handling.

Core BotSpace tidak boleh mengetahui detail provider SDK.

Target architecture:

Application
    ↓
ProviderSessionPort
    ↓
ProviderSessionAdapter
    ↓
Provider SDK / external provider

Jangan:

Application
    ↓
Telegram SDK directly

==================================================
STEP 3 — TELEGRAM PROVIDER BOUNDARY
==================================================

B-041 harus mempersiapkan Telegram/provider integration.

Audit apakah repository sudah memiliki Telegram library/provider dependency.

Jika SUDAH tersedia:

- gunakan dependency tersebut,
- buat adapter modular,
- jangan menyebarkan SDK types ke domain layer.

Jika BELUM tersedia:

- jangan memilih library secara sembarangan,
- jangan menambahkan provider SDK hanya berdasarkan asumsi,
- buat provider adapter boundary yang benar,
- tandai real provider authentication sebagai deferred.

Jangan membuat fake authentication yang mengklaim account berhasil connected.

==================================================
STEP 4 — SESSION CREDENTIAL FLOW
==================================================

Integrasikan session credential flow dengan B-040.

Credential lifecycle:

B-040 Account/Connection
        ↓
Credential reference
        ↓
SecretResolver
        ↓
Provider Session Adapter
        ↓
Provider session
        ↓
Session state update

RAW SECRET tidak boleh:

- masuk API response,
- masuk event,
- masuk log,
- masuk database domain object,
- masuk error message,
- masuk Git.

Gunakan SecretResolver boundary yang SUDAH ADA.

JANGAN membuat SecretResolver kedua.

==================================================
STEP 5 — PROVIDER SESSION LIFECYCLE
==================================================

Provider adapter harus menghormati lifecycle B-040.

Implementasikan mapping yang jelas untuk:

- connect,
- authenticate,
- establish session,
- reconnect,
- disconnect,
- revoke,
- unavailable credential,
- authentication failure,
- provider unavailable,
- session expired jika provider memang menyediakan informasi tersebut.

Jangan membuat state baru hanya karena mudah.

Gunakan state machine B-040.

Provider failure tidak boleh menyebabkan state menjadi active jika session sebenarnya tidak berhasil.

==================================================
STEP 6 — IDEMPOTENCY
==================================================

Perhatikan:

connect dua kali,
reconnect dua kali,
disconnect dua kali,
revoke dua kali.

Jika B-040 sudah memiliki idempotency semantics:

ikuti semantics tersebut.

Jangan membuat duplicate provider session secara tidak sengaja.

Jika operation sudah berada pada terminal state:

gunakan behavior yang sudah ditentukan oleh B-040.

==================================================
STEP 7 — RUNTIME HANDOFF
==================================================

Implementasikan boundary untuk handoff dari account/session ke runtime.

PENTING:

Account connected
TIDAK SAMA DENGAN
Bot runtime running.

Runtime handoff harus eksplisit.

Target:

Session
  ↓
RuntimeCapability / RuntimeHandoff
  ↓
BotInstallation / Worker
  ↓
Runtime process

Runtime handoff harus membawa hanya informasi yang dibutuhkan.

Jangan mengirim raw credential ke generic runtime event/API.

Gunakan:

- account ID,
- connection ID,
- session ID,
- provider ID,
- capability/reference,
- workspace ID jika memang diperlukan.

Credential tetap di SecretResolver/provider boundary.

==================================================
STEP 8 — BOTINSTALLATION SAFETY
==================================================

JANGAN mengubah arti:

BotInstallation.status

menjadi process/runtime state.

Jika existing BotInstallation lifecycle sudah ada:

gunakan lifecycle tersebut.

Jika runtime process state memang diperlukan:

gunakan field/abstraction runtime yang SUDAH ada.

Jika belum ada:

buat minimal runtime boundary hanya jika B-041 memang membutuhkan.

Jangan menggabungkan:

installation state
dengan
process state.

==================================================
STEP 9 — RUNTIME CAPABILITY
==================================================

Buat capability boundary jika architecture membutuhkannya.

Contoh conceptual model:

RuntimeHandoffRequest

berisi:

- workspaceId,
- accountId,
- connectionId,
- sessionId,
- provider,
- installationId jika memang tersedia,
- capability/reference.

JANGAN masukkan:

- password,
- API key,
- session token,
- raw provider credential.

Runtime harus memperoleh credential melalui secure boundary bila memang diperlukan.

==================================================
STEP 10 — WORKSPACE ISOLATION
==================================================

Runtime handoff WAJIB menghormati workspace isolation.

Workspace A tidak boleh:

- menggunakan session Workspace B,
- menjalankan runtime dengan account Workspace B,
- mengambil credential Workspace B,
- melakukan provider handoff untuk Workspace B.

Gunakan authorization boundary B-030/B-040.

Jangan membuat authorization system baru.

==================================================
STEP 11 — ACTOR ATTRIBUTION
==================================================

Jika B-040 sudah memiliki actor attribution:

teruskan actor/context tersebut ke operation B-041.

Jangan menggunakan arbitrary username/string sebagai security identity.

Jika existing context tidak tersedia:

gunakan boundary yang memang tersedia.

Jangan membuat IAM system baru.

==================================================
STEP 12 — PROVIDER OWNERSHIP
==================================================

Pastikan provider-specific logic hanya berada di provider module.

Core application tidak boleh mengetahui:

- Telegram SDK object,
- provider client object,
- provider session object,
- provider-specific error class,

kecuali melalui adapter translation.

Provider errors harus diterjemahkan ke application/domain error yang aman.

==================================================
STEP 13 — ERROR MAPPING
==================================================

Provider error harus dipetakan ke error internal yang aman.

Minimal bedakan:

- invalid credentials,
- credential unavailable,
- authentication failed,
- session unavailable,
- provider unavailable,
- session revoked,
- session expired,
- invalid lifecycle transition,
- authorization failure.

Jangan mengembalikan raw provider error ke client.

Jangan memasukkan credential/token ke error.

==================================================
STEP 14 — EVENT / OUTBOX
==================================================

Audit apakah existing event/outbox infrastructure sekarang tersedia.

Jika SUDAH tersedia:

integrasikan B-041 lifecycle event sesuai contract.

Contoh event:

- connection.authentication.started
- connection.authentication.succeeded
- connection.authentication.failed
- connection.session.established
- connection.session.disconnected
- connection.session.revoked
- runtime.handoff.requested
- runtime.handoff.accepted
- runtime.handoff.failed

JANGAN membuat event baru jika contract existing sudah menentukan naming.

Jika outbox belum tersedia:

JANGAN membuat full event infrastructure speculative.

Buat hanya integration boundary yang diperlukan dan tandai outbox delivery sebagai:

DEFERRED — outbox infrastructure unavailable.

Jangan memasukkan secret ke event payload.

==================================================
STEP 15 — RUNTIME EXECUTION
==================================================

JANGAN langsung membuat Telegram polling/webhook system besar jika B-041 hanya membutuhkan handoff boundary.

Jika existing runtime worker sudah tersedia:

integrasikan handoff ke worker tersebut.

Jika runtime worker belum menyediakan provider execution:

buat adapter/capability boundary yang diperlukan.

Jangan membuat daemon/process manager baru secara speculative.

Jangan menjalankan production Telegram polling dari test.

==================================================
STEP 16 — COMPOSITION ROOT
==================================================

Wire dependency secara eksplisit.

Target:

composition root
  ↓
B-040 account/session service
  ↓
ProviderSessionPort
  ↓
ProviderSessionAdapter
  ↓
SecretResolver
  ↓
RuntimeHandoffPort
  ↓
Worker/runtime boundary

Jangan menggunakan hidden global singleton jika repository menggunakan dependency injection.

Test environment harus dapat inject fake adapter.

Production harus menggunakan real adapter jika dependency tersedia.

==================================================
STEP 17 — TESTING
==================================================

Tambahkan test behavior nyata.

Minimal:

1. provider session adapter can be injected.
2. connect uses provider adapter.
3. reconnect uses provider adapter.
4. disconnect uses provider adapter.
5. revoke uses provider adapter.
6. provider authentication failure mapped correctly.
7. unavailable credential mapped correctly.
8. provider unavailable mapped correctly.
9. invalid lifecycle transition rejected.
10. duplicate connect behavior.
11. duplicate disconnect behavior.
12. workspace isolation.
13. cross-workspace runtime handoff rejected.
14. runtime handoff contains safe identifiers only.
15. raw credential never appears in handoff payload.
16. raw credential never appears in errors.
17. SecretResolver failure handled safely.
18. provider adapter failure does not incorrectly activate session.
19. runtime handoff success state.
20. runtime handoff failure state.
21. event/outbox integration if infrastructure exists.

Jika real Telegram/provider dependency tersedia:

tambahkan integration test yang aman.

Jangan menggunakan production account.

Jika dependency tidak tersedia:

unit/contract tests tetap harus berjalan.

==================================================
STEP 18 — SECURITY REVIEW
==================================================

Lakukan targeted security review terhadap B-041.

Cari:

- secret leakage,
- credential leakage,
- token leakage,
- provider SDK object leaking into API,
- cross-workspace session access,
- runtime handoff authorization bypass,
- invalid state transition,
- duplicate session,
- stale session,
- unsafe provider errors,
- log leakage,
- event leakage.

Perbaiki masalah yang ditemukan.

==================================================
STEP 19 — VALIDATION
==================================================

Setelah implementation:

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

JANGAN menjalankan atau membuat:

node scripts/check-symlinks.mjs

karena script tersebut memang tidak tersedia.

PostgreSQL:

Jika PERSISTENCE_TEST_DATABASE_URL tersedia:
→ jalankan integration test yang memang ada.

Jika tidak:
→ SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat fake database.

==================================================
STEP 20 — PROVIDER TEST SAFETY
==================================================

Jangan menjalankan integration test Gorouter.app.

Jangan menyentuh Gorouter.app.

NVIDIA dan TokenHarbor:

- jangan diubah,
- jangan dites ulang kecuali B-041 secara langsung menyentuh shared provider infrastructure yang memang membutuhkan verification.

Jika provider Telegram test membutuhkan real credentials:

jangan menggunakan credential production.

Gunakan synthetic/test environment atau tandai deferred.

==================================================
STEP 21 — REVIEW DIFF
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Review seluruh perubahan.

Hapus:

- temporary files,
- debug output,
- generated files,
- secrets,
- credentials,
- unrelated refactor.

Pastikan perubahan hanya B-041.

==================================================
STEP 22 — COMMIT
==================================================

Jika implementation valid:

buat SATU commit.

Suggested:

feat: add provider session adapter and runtime handoff

Gunakan message yang lebih tepat jika perubahan aktual berbeda.

Jangan membuat empty commit.

==================================================
STEP 23 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian:

git rev-parse HEAD

Verifikasi remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

Working tree harus:

CLEAN

Jika push gagal:

- jangan reset,
- jangan menghapus commit,
- jangan mengubah credential Git secara sembarangan,
- laporkan error,
- commit lokal harus tetap aman.

==================================================
DEFINITION OF DONE
==================================================

B-041 dianggap selesai jika:

- ProviderSessionPort tersedia/terintegrasi.
- Provider adapter boundary tersedia.
- B-040 lifecycle terhubung ke provider adapter.
- SecretResolver terintegrasi.
- Provider errors diterjemahkan dengan aman.
- Runtime handoff boundary tersedia.
- Workspace isolation diterapkan.
- Runtime handoff tidak membawa raw credential.
- Composition root sudah di-wire.
- Test behavior tersedia.
- Validation PASS.
- Commit dibuat.
- Push berhasil.
- Local SHA == Remote SHA.
- Working tree CLEAN.

Jika real provider/runtime belum tersedia:

status harus dibagi jelas:

IMPLEMENTED:
- abstraction,
- adapter boundary,
- lifecycle integration,
- handoff contract,
- tests,
- composition wiring.

DEFERRED:
- real provider credential exchange,
- real provider SDK integration,
- real runtime execution,
- outbox delivery,

hanya jika dependency tersebut memang tidak tersedia.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-041 STATUS
- ProviderSessionPort:
- Provider adapter:
- Session lifecycle:
- SecretResolver:
- Runtime handoff:
- Composition root:
- Workspace isolation:

### SECURITY
- Credential protection:
- Secret leakage:
- Cross-workspace protection:
- Provider error sanitization:
- Runtime handoff safety:

### TEST
- Unit:
- Integration:
- Build:
- Typecheck:
- Lint:
- Format:
- Imports:
- Ownership:
- Docs:
- Diff check:

### DEFERRED
Hanya dependency nyata yang belum tersedia.

### GIT
- Commit:
- Push:
- Local SHA:
- Remote SHA:
- Working tree:

### NEXT ROADMAP
Tentukan task berikutnya berdasarkan dependency nyata setelah B-041.

PENTING:

Jangan kembali ke B-040.

Jangan meminta approval.

Jangan berhenti hanya karena real provider belum tersedia.

Jangan membuat fake production authentication.

Jangan membuat runtime Telegram polling besar secara speculative.

Jangan menyentuh Gorouter.app.

Kerjakan langsung coding B-041 di:

/root/botspace

```
# Prompt: B-040 — Owner Approval + Implement Account/Session Connection
```

# PROMPT: B-040 — OWNER APPROVAL + IMPLEMENT ACCOUNT/SESSION CONNECTION

Lanjutkan project BotSpace dari kondisi repository SAAT INI di:

/root/botspace

BRANCH:
backend-dev-recovery

==================================================
IMPORTANT — OWNER APPROVAL IS GRANTED NOW
==================================================

Saya sebagai owner project memberikan HUMAN APPROVAL secara eksplisit untuk:

B-040 / ADR-011 — Telegram Account Connection / Account Session Architecture.

Approval ini berlaku untuk memulai IMPLEMENTASI, bukan hanya audit.

JANGAN kembali menjawab:
- "human approval belum tersedia"
- "B-040 masih BLOCKED"
- "obtain human approval"
- "approval diperlukan"
- "tidak ada code change karena approval belum ada"

Approval sudah diberikan melalui prompt ini.

Setelah membaca prompt ini:

1. Validasi approval secara singkat.
2. Buka ADR-011 dan decision package yang sudah tersedia.
3. Gunakan keputusan yang sudah disepakati di repository sebagai source of truth.
4. LANGSUNG IMPLEMENTASIKAN B-040.
5. Jangan mengulang audit penuh yang sebelumnya sudah dilakukan.
6. Jangan membuat prompt approval baru.
7. Jangan berhenti setelah membuat dokumentasi.
8. Jangan hanya membuat plan.
9. Kerjakan source code sampai implementation B-040 selesai sesuai dependency nyata.

==================================================
CURRENT STATE
==================================================

Audit sebelumnya sudah menghasilkan:

- B-030 Workspace API/Contract: DONE.
- B-070 Storage Adapter: DONE.
- B-071 File/Share contract: DONE.
- B-071 File/Share API: DONE.
- Production wiring B-071: DONE.
- SecretResolver application boundary: AVAILABLE.
- Working tree terakhir: CLEAN.
- Local/remote branch terakhir: synchronized.
- ADR-011: sudah dibuat dan decision package sudah disiapkan.
- Formatting ADR-011 sudah diperbaiki.
- Tidak ada perubahan source code pada audit terakhir.
- B-040 sebelumnya BLOCKED hanya karena owner approval.
- Approval SEKARANG SUDAH DIBERIKAN.

Jangan mengulang implementasi:
- B-030
- B-070
- B-071

Jangan mengubah schema/contract B-071 kecuali B-040 secara nyata membutuhkan integrasi yang memang sudah ditentukan oleh ADR/contract.

==================================================
PRIMARY OBJECTIVE
==================================================

Implementasikan B-040 / ADR-011 secara nyata.

Scope utama:

ACCOUNT / SESSION CONNECTION ARCHITECTURE

Implementasi harus menyediakan foundation yang aman dan modular untuk:

1. Authentication mechanism boundary.
2. Provider/library boundary.
3. Account identity.
4. Connection identity.
5. Session model.
6. Credential lifecycle.
7. Credential storage boundary.
8. Connect semantics.
9. Disconnect semantics.
10. Reconnect semantics.
11. Revoke semantics.
12. Account removal semantics.
13. Workspace authorization.
14. Actor attribution.
15. Versioned API/error behavior.
16. Persistence boundary.
17. Event/outbox boundary jika memang sudah ditetapkan contract.
18. Runtime handoff/capability boundary.
19. Provider ownership boundary.
20. Security boundary.

==================================================
CRITICAL ARCHITECTURE RULE
==================================================

JANGAN membuat architecture speculative.

Sebelum coding:

- baca ADR-011,
- baca decision package,
- baca roadmap terkait B-040,
- baca contract yang sudah ada,
- baca existing account/session/provider-related code,
- baca SecretResolver boundary,
- baca workspace authorization boundary,
- baca runtime/provider boundary.

Gunakan architecture yang SUDAH ada.

Jika sebuah keputusan memang sudah ditentukan di ADR-011:
→ ikuti keputusan tersebut.

Jika ADR-011 tidak menentukan detail implementation tertentu:
→ pilih implementation MINIMAL yang paling kompatibel dengan repository saat ini.

Jangan membuat vendor-specific implementation tanpa alasan.

Jangan memilih Telegram library/provider baru hanya berdasarkan asumsi.

Jangan menambahkan dependency eksternal jika dependency yang diperlukan belum jelas.

==================================================
AUTHENTICATION / PROVIDER BOUNDARY
==================================================

Implementasikan authentication melalui abstraction yang memungkinkan provider berbeda di masa depan.

Architecture harus memungkinkan provider memiliki mekanisme authentication berbeda, misalnya:

- API key,
- OAuth,
- device code,
- browser/session authentication,
- Telegram account session,
- provider-specific credential.

Namun:

JANGAN implementasikan semua mekanisme tersebut sekarang.

Buat boundary yang memungkinkan future provider tanpa mengubah core account/session architecture.

Authentication mechanism harus dipisahkan dari:

- account identity,
- connection identity,
- session state,
- credential storage,
- workspace ownership.

Jangan mencampur provider SDK langsung ke domain model.

==================================================
ACCOUNT IDENTITY
==================================================

Account harus memiliki identity yang stabil.

Pisahkan:

- account identity,
- connection identity,
- session identity,
- credential identity jika diperlukan.

Jangan menggunakan raw credential sebagai identity.

Jangan menggunakan token/session secret sebagai public identifier.

Account identity harus dapat digunakan oleh workspace-scoped authorization.

Pastikan satu account dapat memiliki lifecycle yang jelas.

==================================================
CONNECTION MODEL
==================================================

Implementasikan connection model sesuai ADR-011.

Connection harus dapat merepresentasikan hubungan:

workspace
    ↓
account
    ↓
provider/connection
    ↓
session
    ↓
credential reference

Jangan menyimpan secret mentah sebagai bagian dari object yang dikembalikan API.

Connection harus memiliki state/lifecycle yang eksplisit sesuai keputusan ADR-011.

Jika state machine sudah ditentukan:

- implementasikan state tersebut,
- validasi transition,
- tolak transition ilegal.

Jika state machine belum ditentukan secara eksplisit:

gunakan state minimum yang diperlukan dan jangan menambahkan state speculative.

==================================================
SESSION MODEL
==================================================

Session harus terpisah dari account identity.

Session harus dapat memiliki:

- stable session identifier,
- account reference,
- provider reference,
- lifecycle state,
- created/updated timestamps jika contract memang membutuhkannya,
- credential reference jika memang diperlukan.

Jangan menyimpan:

- raw password,
- raw API key,
- raw session token,
- private authentication material

di response API atau log.

Session lifecycle harus mendukung sesuai ADR:

- connect,
- active,
- reconnect,
- disconnect,
- revoke,
- compromised jika memang disepakati,
- removal jika memang disepakati.

Jangan membuat lifecycle state yang tidak diperlukan.

==================================================
CREDENTIAL STORAGE
==================================================

Gunakan SecretResolver boundary yang SUDAH ADA.

JANGAN membuat secret storage abstraction kedua.

Credential architecture harus:

- menyimpan reference, bukan raw secret, pada domain/persistence jika memungkinkan,
- menggunakan SecretResolver untuk resolve secret,
- tidak mencetak secret,
- tidak memasukkan secret ke error,
- tidak memasukkan secret ke response,
- tidak memasukkan secret ke event payload,
- tidak memasukkan secret ke Git.

Jika SecretResolver hanya tersedia sebagai boundary:

gunakan dependency injection.

Jangan hardcode credential.

Jangan membuat fake production credential.

==================================================
CREDENTIAL LIFECYCLE
==================================================

Implementasikan lifecycle berdasarkan ADR-011.

Harus jelas:

- kapan credential dibuat,
- kapan credential digunakan,
- kapan credential diperbarui,
- kapan credential dirotasi,
- kapan credential dicabut,
- kapan credential dihapus,
- bagaimana unavailable-secret behavior ditangani.

Jangan menghapus credential secara destruktif jika lifecycle contract belum mendukungnya.

Jika provider revoke diperlukan:

buat provider boundary untuk revoke.

Jangan langsung memanggil provider SDK dari generic domain service.

==================================================
CONNECT
==================================================

Implementasikan connection workflow sesuai contract.

Minimal flow harus memiliki boundary:

request
→ authorization
→ account/connection creation
→ authentication
→ credential resolution/storage boundary
→ session establishment
→ persistence
→ result

Jangan membuat fake successful authentication.

Jika provider SDK/runtime belum tersedia:

implementasikan boundary dan integration point yang memang dapat dilakukan sekarang.

Jangan mengklaim provider connection berhasil jika provider runtime sebenarnya belum tersedia.

Gunakan status yang jujur seperti pending/unsupported/failed sesuai contract.

==================================================
DISCONNECT
==================================================

Implementasikan disconnect semantics sesuai ADR.

Pastikan:

- authorization diperiksa,
- hanya owner/authorized actor yang dapat disconnect,
- session tidak lagi dianggap active,
- credential/session cleanup mengikuti lifecycle,
- provider disconnect dipanggil melalui provider boundary jika tersedia.

Jangan menghapus account secara otomatis hanya karena disconnect kecuali ADR memang menentukan demikian.

==================================================
RECONNECT
==================================================

Implementasikan reconnect boundary.

Reconnect harus:

- memeriksa account/connection masih valid,
- memeriksa credential masih tersedia,
- menggunakan provider authentication boundary,
- memperbarui session state,
- tidak membuat duplicate account secara tidak sengaja.

Gunakan idempotency semantics jika sudah ditentukan ADR.

==================================================
REVOKE
==================================================

Implementasikan revoke semantics sesuai keputusan ADR.

Revoke harus berbeda secara jelas dari disconnect jika ADR membedakannya.

Jika credential/session sudah revoked:

- jangan dapat digunakan kembali,
- jangan diam-diam menjadi active kembali,
- reconnect harus mengikuti policy yang benar.

Jangan membuat revoke hanya sebagai perubahan boolean jika lifecycle contract membutuhkan state transition yang lebih kuat.

==================================================
ACCOUNT REMOVAL
==================================================

Jika ADR-011 menetapkan account removal:

Implementasikan lifecycle yang aman.

Perhatikan:

- workspace ownership,
- active connections,
- sessions,
- credential references,
- provider revoke,
- persistence cleanup,
- event behavior jika memang tersedia.

Jangan melakukan hard delete terhadap data yang masih diperlukan untuk audit/security jika architecture memang membutuhkan retention.

Jangan menghapus data secara spekulatif.

==================================================
WORKSPACE AUTHORIZATION
==================================================

Account/connection HARUS workspace-scoped.

Pastikan:

Workspace A
tidak dapat:

- melihat account Workspace B,
- melihat connection Workspace B,
- mengambil session Workspace B,
- disconnect account Workspace B,
- revoke account Workspace B,
- mengubah credential Workspace B.

Gunakan workspace authorization boundary yang sudah ada.

Jangan membuat authorization system kedua.

==================================================
ACTOR ATTRIBUTION
==================================================

Operation harus dapat mengidentifikasi actor jika contract/architecture sudah menyediakan request context.

Contoh:

- user actor,
- admin actor,
- system actor.

Jangan menggunakan arbitrary string sebagai security identity jika repository sudah memiliki actor abstraction.

Jika actor attribution belum memiliki contract:

jangan membuat sistem IAM baru.

Gunakan boundary yang sudah tersedia atau dokumentasikan dependency yang benar-benar belum tersedia.

==================================================
API CONTRACT
==================================================

Jika B-040 memiliki API surface yang ditentukan ADR:

implementasikan endpoint/service contract tersebut.

Pisahkan:

HTTP/API layer
↓
application service
↓
domain
↓
repository/provider/secret boundary

Jangan memasukkan business logic besar ke route handler.

Response tidak boleh mengandung:

- raw credential,
- secret,
- private session material,
- provider access token,
- password.

Gunakan public-safe representation.

==================================================
VERSIONED API / ERROR CONTRACT
==================================================

Implementasikan error contract yang sudah ditentukan ADR.

Pastikan error membedakan minimal:

- invalid request,
- unauthorized,
- forbidden,
- not found,
- invalid state transition,
- authentication failure,
- credential unavailable,
- provider unavailable,
- conflict,
- internal failure.

Jangan membocorkan:

- secret,
- provider credential,
- internal filesystem path,
- database credentials,
- stack trace production.

Jika API version sudah ada:
ikuti version tersebut.

Jangan membuat API version kedua.

==================================================
IDEMPOTENCY
==================================================

Jika connect/reconnect operation membutuhkan idempotency dan ADR sudah mendefinisikannya:

implementasikan dengan benar.

Jangan membuat duplicate connection ketika request yang sama diulang.

Jika idempotency contract belum tersedia:

jangan membuat sistem idempotency kompleks secara speculative.

Gunakan existing infrastructure jika tersedia.

==================================================
CONCURRENCY
==================================================

Perhatikan race condition:

- dua connect bersamaan,
- disconnect saat reconnect,
- revoke saat reconnect,
- account removal saat session aktif.

Gunakan persistence/transaction primitive yang memang tersedia.

Jangan membuat fake locking system.

Jangan menambahkan distributed lock dependency hanya berdasarkan asumsi.

==================================================
PERSISTENCE
==================================================

Audit persistence layer yang tersedia.

Jika migration/schema B-040 memang sudah ditentukan ADR:

implementasikan migration sesuai contract.

Jika schema belum ditentukan:

buat schema minimum yang benar-benar diperlukan untuk B-040 dan konsisten dengan architecture repository.

JANGAN mengubah B-071 schema secara unrelated.

Pastikan:

- unique constraints,
- workspace ownership,
- stable IDs,
- state,
- timestamps,
- credential references

sesuai kebutuhan nyata.

Jangan menyimpan raw secrets di database.

==================================================
EVENTS / OUTBOX
==================================================

Jika ADR-011 sudah menentukan event/outbox contract:

implementasikan sesuai contract.

Event harus aman.

Jangan memasukkan:

- password,
- access token,
- raw credential,
- session secret.

Event payload hanya boleh berisi public-safe identifiers dan state information yang memang dibutuhkan.

Jika outbox infrastructure belum tersedia:

jangan membuat event system besar secara speculative.

Implementasikan hanya boundary yang benar-benar menjadi bagian B-040.

==================================================
RUNTIME HANDOFF
==================================================

B-040 harus memisahkan account/session lifecycle dari runtime bot lifecycle.

JANGAN:

- menjalankan Telegram polling otomatis hanya karena account connected,
- mengubah BotInstallation.status menjadi process state,
- membuat account connection langsung menjadi bot process.

Account/session:

Account connected
    ≠
Bot running

Runtime handoff harus melalui capability/provider boundary.

Jika runtime handoff contract sudah tersedia:

implementasikan integration point.

Jika belum:

jangan membuat runtime orchestration baru.

==================================================
TELEGRAM / PROVIDER BOUNDARY
==================================================

B-040 adalah account/session architecture.

Jangan mencampur seluruh Telegram provider implementation ke core.

Gunakan provider abstraction.

Provider-specific code harus modular sehingga provider lain dapat ditambahkan kemudian.

Jika Telegram provider SDK sudah ada:

gunakan boundary tersebut.

Jika belum:

buat interface/adapter boundary yang diperlukan tanpa fake authentication.

JANGAN mengklaim Telegram account benar-benar connected jika SDK/runtime credential exchange belum tersedia.

==================================================
SECURITY
==================================================

Lakukan targeted security review terhadap implementation B-040.

Pastikan:

- workspace isolation,
- authorization,
- credential secrecy,
- SecretResolver usage,
- session isolation,
- revoke behavior,
- disconnect behavior,
- account removal,
- provider boundary,
- error sanitization,
- log sanitization,
- input validation,
- ID validation,
- concurrency safety.

Cari juga:

- hardcoded secret,
- token,
- password,
- private key,
- credential,
- accidental debug logs.

Jika ditemukan:
perbaiki sebelum commit.

==================================================
TESTING
==================================================

Tambahkan test yang benar-benar menguji implementation.

Minimal:

1. account creation.
2. connection creation.
3. workspace isolation.
4. unauthorized access.
5. forbidden cross-workspace access.
6. session creation.
7. valid lifecycle transition.
8. invalid lifecycle transition.
9. disconnect.
10. reconnect.
11. revoke.
12. credential resolution.
13. missing credential.
14. SecretResolver failure.
15. secret tidak bocor ke error.
16. secret tidak bocor ke response.
17. duplicate connection behavior.
18. concurrency behavior jika contract mendukung.
19. account removal behavior.
20. provider failure handling.
21. runtime handoff boundary jika contract sudah tersedia.
22. API error mapping jika API endpoint diimplementasikan.

Jangan membuat fake test yang hanya memeriksa object dibuat.

Test harus memverifikasi behavior.

==================================================
VALIDATION
==================================================

Setelah implementation selesai jalankan validation repository yang tersedia.

Minimal:

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

JANGAN membuat script tersebut jika memang tidak ada.

Jika tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

Untuk PostgreSQL:

Jika:
PERSISTENCE_TEST_DATABASE_URL

tersedia, jalankan integration test yang memang tersedia.

Jika tidak:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat database palsu.

Jangan mengganti PostgreSQL dengan SQLite hanya untuk PASS.

==================================================
BOTSPACE / GOROUTER / PROVIDER SAFETY
==================================================

JANGAN menyentuh:

- Gorouter.app integration test.
- Gorouter runtime integration.
- provider test yang tidak diperlukan.

NVIDIA dan TokenHarbor:

- jangan diubah,
- jangan ditest ulang kecuali perubahan B-040 benar-benar menyentuh shared code yang berhubungan langsung.

Jangan mengubah provider yang tidak relevan.

==================================================
DOCUMENTATION
==================================================

Update ADR-011 hanya jika implementation menemukan keputusan yang perlu dicatat.

Jangan menulis dokumentasi palsu yang mengatakan feature production-ready jika infrastructure/provider belum tersedia.

Dokumentasikan:

- implemented decisions,
- deferred dependencies,
- provider/runtime limitations,
- security boundary,
- credential boundary.

Jangan membuat banyak README.

Gunakan dokumentasi architecture yang sudah ada.

==================================================
GIT DISCIPLINE
==================================================

Sebelum coding:

git status

Pastikan working tree clean.

Setelah coding:

git status
git diff --stat
git diff

Review seluruh perubahan.

Hapus:

- temporary files,
- debug files,
- generated junk,
- unrelated refactor,
- secrets,
- credentials.

Jangan mengubah file yang tidak berkaitan dengan B-040.

==================================================
COMMIT
==================================================

Jika implementation valid dan validation selesai:

buat SATU commit.

Gunakan commit message:

feat: implement account session connection

atau message yang lebih tepat berdasarkan perubahan aktual.

Jangan membuat empty commit.

==================================================
PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

dan remote SHA.

Pastikan:

LOCAL SHA == REMOTE SHA

dan:

working tree CLEAN

Jika push gagal karena credential/network:

- jangan menghapus commit,
- jangan reset,
- jangan mengubah credential sembarangan,
- laporkan error,
- commit lokal harus tetap aman.

==================================================
IMPORTANT — DO NOT STOP AT AUDIT
==================================================

Ini adalah bagian paling penting.

Approval sudah diberikan.

Jangan berhenti dengan:

"Implementation blocked."

Jangan berhenti dengan:

"Human approval required."

Jangan berhenti dengan:

"Need owner decision."

Jangan hanya menghasilkan:

- audit report,
- roadmap,
- decision package,
- list of blockers.

KERJAKAN CODING.

Jika ada dependency yang benar-benar belum tersedia:

1. Implementasikan bagian B-040 yang dapat dikerjakan sekarang.
2. Integrasikan dengan boundary yang sudah tersedia.
3. Tandai hanya dependency tersebut sebagai deferred.
4. Jangan membuat fake implementation.
5. Jangan memblokir seluruh B-040 hanya karena satu integration dependency eksternal belum tersedia.

==================================================
DEFINITION OF DONE
==================================================

B-040 dianggap selesai untuk tahap repository jika:

- owner approval tercatat,
- account model implemented,
- connection model implemented,
- session model implemented,
- lifecycle implemented,
- authorization implemented,
- credential boundary integrated,
- provider boundary implemented,
- persistence implemented bila contract/schema memungkinkan,
- API/application service implemented bila scope ADR mengharuskannya,
- security tests tersedia,
- validation selesai,
- documentation diperbarui bila diperlukan,
- commit dibuat,
- push berhasil,
- local dan remote SHA sama,
- working tree clean.

Jika sebagian infrastructure provider masih unavailable:

jangan mengklaim external integration PASS.

Tampilkan status:

IMPLEMENTED
atau
DEFERRED — external dependency unavailable

secara jelas.

==================================================
FINAL OUTPUT
==================================================

Setelah coding selesai, tampilkan laporan ringkas:

### B-040 STATUS
- Owner approval: APPROVED
- Account model:
- Connection model:
- Session model:
- Lifecycle:
- Authorization:
- Credential boundary:
- Provider boundary:
- Persistence:
- API/application service:
- Runtime handoff:

### SECURITY
- Workspace isolation:
- Credential protection:
- SecretResolver:
- Revoke:
- Disconnect:
- Error sanitization:

### TEST
- Unit:
- Integration:
- Build:
- Typecheck:
- Lint:
- Format:
- Imports:
- Ownership:
- Docs:
- Diff check:
- Symlink check:

### GIT
- Commit:
- Push:
- Local SHA:
- Remote SHA:
- Working tree:

### REMAINING DEFERRED
Hanya tampilkan dependency yang BENAR-BENAR masih membutuhkan:
- external provider,
- deployment infrastructure,
- unavailable environment,
- atau contract yang memang belum tersedia.

### NEXT ROADMAP
Tentukan task berikutnya berdasarkan dependency nyata setelah B-040 selesai.

JANGAN mengulang audit B-040 dari awal.

JANGAN meminta approval lagi.

LANGSUNG CODING setelah approval ini.

Kerjakan langsung pada:

/root/botspace

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
# Prompt: BotSpace — Fix Current Validation Blocker and Continue Directly to Coding

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

KONDISI TERAKHIR YANG SUDAH DIKETAHUI:

- Branch aktif: backend-dev-recovery
- Repository working tree saat ini CLEAN.
- Tidak ada code change dari percobaan terakhir.
- Tidak ada commit baru.
- Tidak ada push baru.
- B-030 SUDAH SELESAI.
- B-070 SUDAH SELESAI.
- B-071 SUDAH SELESAI.
- Production wiring B-071 SUDAH SELESAI.
- SecretResolver application boundary SUDAH tersedia.
- Deferred infrastructure verification SUDAH dilakukan.
- B-040/ADR-011 MASIH BLOCKED karena membutuhkan human approval.
- Jangan mengulang audit B-040.
- Jangan meminta approval berulang-ulang.
- Jangan membuat implementation B-040 sebelum approval resmi tersedia.
- Jangan membuat approval palsu.
- Jangan membuat contract speculative.

HASIL ANALISIS ROADMAP TERAKHIR:

Task berikut diketahui masih bergantung pada B-040 atau dependency yang belum disetujui/tersedia:

- B-041
- B-050
- B-051
- B-052
- frontend F-040
- frontend F-050
- frontend F-051
- F-060
- B-090
- B-092/F-090
- B-100/F-100
- B-110/B-111/F-110
- B-130/B-131/F-130
- B-140/B-141/F-140
- B-150/B-151/F-150
- B-080/B-120
- B-003 jika membutuhkan environment/runtime yang memang tidak tersedia.

JANGAN mengulang analisis panjang terhadap daftar tersebut kecuali ada bukti dependency repository sudah berubah.

==================================================
BAGIAN 1 — PERBAIKI VALIDATION BLOCKER SAAT INI
==================================================

Validation terakhir menunjukkan:

pnpm format:check

GAGAL pada:

docs/architecture/ADR-011-telegram-account-connection.md

Masalahnya adalah formatting/prettier pada tabel dokumentasi tersebut.

Ini adalah masalah dokumentasi/formatting yang sudah ada di HEAD, bukan alasan untuk melakukan full audit lagi.

Tugas:

1. Buka file:
   docs/architecture/ADR-011-telegram-account-connection.md

2. Periksa formatting yang menyebabkan:
   pnpm format:check
   gagal.

3. Perbaiki HANYA formatting dokumentasi yang diperlukan agar file sesuai formatter repository.

4. Jangan mengubah:
   - keputusan architecture,
   - scope B-040,
   - approval status,
   - contract,
   - API,
   - schema,
   - source code,
   - security behavior,
   - provider,
   - Telegram runtime.

5. Jangan mengubah isi substantif ADR hanya demi membuat format PASS.

6. Setelah perbaikan jalankan:

   pnpm format:check

7. Jika PASS, lanjutkan validation ringan:

   git diff --check

8. Review diff.

Jika perubahan hanya formatting dokumentasi:
- boleh commit karena merupakan fix nyata terhadap validation blocker.
- jangan membuat empty commit.

Gunakan commit message yang sesuai, misalnya:

docs: fix ADR-011 formatting

Jika repository policy membutuhkan commit terpisah, gunakan satu commit saja.

Push ke:

git push origin backend-dev-recovery

Verifikasi local SHA == remote SHA.

==================================================
BAGIAN 2 — JANGAN MENGULANG FULL AUDIT
==================================================

SETELAH FORMAT BLOCKER SELESAI:

JANGAN menjalankan full repository audit lagi.

JANGAN mengulang:
- audit B-040,
- audit ADR-011,
- audit B-071,
- audit B-070,
- audit SecretResolver,
- audit dependency graph secara panjang.

Lakukan hanya dependency check singkat terhadap roadmap terbaru.

Tujuannya hanya untuk menemukan apakah ADA task CODING yang sekarang benar-benar unlocked.

==================================================
BAGIAN 3 — CARI TASK CODING YANG BENAR-BENAR UNLOCKED
==================================================

Gunakan source of truth repository:

- ROADMAP_V2.md
- AI_TASKS.md
- ADR/documentation yang relevan
- dependency markers/task status
- git history terbaru.

Cari task dengan kondisi:

- implementation allowed,
- dependency terpenuhi,
- tidak membutuhkan human approval,
- tidak membutuhkan provider contract yang belum disetujui,
- tidak membutuhkan infrastructure yang tidak tersedia,
- tidak bergantung pada B-040,
- tidak bergantung transitively pada B-040.

PENTING:

Jangan menganggap task unlocked hanya karena namanya ada di roadmap.

Verifikasi dependency aktual.

Jika ditemukan SATU task coding yang benar-benar unlocked:

LANGSUNG KERJAKAN.

Jangan berhenti pada laporan audit.

==================================================
BAGIAN 4 — IMPLEMENTASI TASK UNLOCKED
==================================================

Jika ada task coding unlocked:

1. Baca requirement task tersebut.
2. Audit hanya file yang relevan dengan task tersebut.
3. Implementasikan secara modular.
4. Jangan membuat architecture baru jika abstraction yang dibutuhkan sudah tersedia.
5. Jangan membuat duplicate contract.
6. Jangan mengubah behavior unrelated.
7. Jangan menyentuh B-040.
8. Jangan mengubah BotInstallation.status menjadi runtime process state.
9. Jangan menyentuh Gorouter.app.
10. NVIDIA dan TokenHarbor hanya boleh disentuh jika task tersebut memang secara langsung membutuhkan provider tersebut.
11. Jangan membuat credential palsu.
12. Jangan memasukkan secret/API key/token ke repository.
13. Tambahkan test yang relevan dengan implementation.

Setelah coding selesai:

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

Jika tidak tersedia, cukup catat:

SKIPPED — scripts/check-symlinks.mjs unavailable

Jika ada test integration yang membutuhkan environment yang tidak tersedia:
- jangan membuat fake environment,
- jangan mengubah test agar PASS,
- tandai SKIPPED/UNAVAILABLE.

==================================================
BAGIAN 5 — REVIEW DAN COMMIT
==================================================

Jika coding berhasil:

1. git status
2. git diff --stat
3. review seluruh git diff
4. pastikan hanya task yang dipilih.
5. pastikan tidak ada:
   - secret,
   - credential,
   - temporary file,
   - generated junk,
   - unrelated refactor,
   - Gorouter changes,
   - provider changes yang tidak diperlukan.

Kemudian buat SATU commit.

Gunakan commit message sesuai perubahan aktual.

Kemudian:

git push origin backend-dev-recovery

Verifikasi:

git rev-parse HEAD
git rev-parse origin/backend-dev-recovery

Keduanya HARUS sama.

Pastikan:

git status

menunjukkan working tree clean.

==================================================
BAGIAN 6 — JIKA TIDAK ADA TASK CODING YANG UNLOCKED
==================================================

Jika setelah dependency check singkat ternyata TIDAK ADA task coding yang dapat dikerjakan tanpa B-040:

JANGAN:

- mengulang audit,
- mengulang ADR-011,
- mengarang task,
- mengimplementasikan B-040 tanpa approval,
- membuat contract speculative,
- membuat fake dependency,
- membuat commit kosong.

Sebagai gantinya:

1. Pastikan format blocker sudah diperbaiki.
2. Pastikan repository clean dan remote sinkron.
3. Buat PREPARED IMPLEMENTATION PACKAGE untuk B-040/ADR-011.

Package tersebut hanya boleh berupa dokumentasi/persiapan yang tidak mengubah architecture decision.

Isi package:

- scope B-040,
- dependency yang sudah tersedia,
- dependency yang masih diperlukan,
- decision yang membutuhkan owner approval,
- file/module yang kemungkinan akan diubah setelah approval,
- migration impact,
- security impact,
- Telegram/provider impact,
- deployment impact,
- test plan,
- rollback considerations,
- exact approval decisions yang harus diberikan owner.

JANGAN menulis implementation code B-040.

JANGAN membuat source-code changes untuk B-040.

JANGAN membuat schema/migration B-040.

Tujuannya agar setelah human approval tersedia, coding dapat dimulai tanpa melakukan audit ulang dari nol.

==================================================
BAGIAN 7 — APPROVAL GATE
==================================================

B-040 memiliki approval gate.

Status harus dipertahankan:

B-040/ADR-011: BLOCKED — human approval required.

Approval harus mencakup keputusan nyata mengenai:

- authentication mechanism,
- provider/library boundary,
- account/session identity model,
- connection identity,
- session lifecycle,
- credential storage/resolution,
- connect semantics,
- disconnect semantics,
- revoke semantics,
- reconnect semantics,
- workspace authorization,
- actor attribution,
- API versioning,
- error contract,
- idempotency,
- concurrency,
- persistence schema,
- migration,
- event model,
- event delivery,
- runtime handoff,
- provider ownership,
- deployment ownership.

Jangan memilih keputusan tersebut sendiri jika roadmap mensyaratkan owner approval.

==================================================
BAGIAN 8 — VALIDATION AKHIR
==================================================

Jika hanya documentation formatting yang berubah:

Jalankan minimal:

pnpm format:check
git diff --check

Jika coding task unlocked dikerjakan:

jalankan full validation:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check
node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan menjalankan atau membuat:

node scripts/check-symlinks.mjs

==================================================
BAGIAN 9 — OUTPUT AKHIR
==================================================

Tampilkan laporan ringkas:

### Current Status
- B-040:
- ADR-011:
- Format blocker:
- Working tree:

### Coding Task
- Task yang ditemukan:
- Dependency:
- Status:
- Apakah coding dilakukan:

### Changes
- file berubah:
- implementation:
- tests:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit:
- push:
- local SHA:
- remote SHA:
- working tree:

### Remaining Blockers
Hanya tampilkan blocker nyata.

### NEXT SINGLE ACTION

Jika task coding unlocked:
tulis task berikutnya.

Jika tidak ada:
tulis persis:

NEXT SINGLE ACTION:
Obtain human approval for B-040/ADR-011.

JANGAN melakukan audit ulang setelah output tersebut.

==================================================
ATURAN PALING PENTING
==================================================

- Jangan mengulang audit panjang.
- Jangan mengulang B-040 tanpa approval.
- Jangan mengulang B-070.
- Jangan mengulang B-071.
- Jangan mengulang SecretResolver.
- Jangan membuat fake dependency.
- Jangan membuat contract speculative.
- Jangan menyentuh Gorouter.app.
- Jangan membuat credential palsu.
- Jangan mengubah BotInstallation.status.
- Jangan membuat empty commit.
- Jangan berhenti pada audit jika ADA task coding yang benar-benar unlocked.
- Jika ADA task unlocked → LANGSUNG CODING → TEST → COMMIT → PUSH.
- Jika TIDAK ADA task unlocked → jangan memaksa coding; siapkan approval package B-040.
- Jangan mengulang pekerjaan yang sudah selesai.

Kerjakan langsung di:

/root/botspace



```
# 
```

Prompt: BotSpace — Skip Blocked B-040 and Continue Unlocked Roadmap

Lanjutkan project BotSpace dari kondisi repository saat ini.

PENTING:
B-040/ADR-011 SUDAH DIKONFIRMASI BLOCKED karena human approval belum tersedia.

JANGAN:
- mengulang audit B-040,
- meminta approval lagi,
- membuat approval palsu,
- membuat implementation B-040,
- mengulang ADR-011,
- membuat commit kosong.

Sekarang pindah ke roadmap berikutnya.

Tugas:

1. Baca roadmap/dependency graph repository saat ini.
2. Identifikasi SEMUA task yang tidak bergantung langsung maupun transitif pada B-040.
3. Jangan mengerjakan B-041, B-050, B-051, B-052, atau task lain yang dependency-nya masih B-040.
4. Pilih task dengan dependency paling lengkap yang benar-benar UNLOCKED.
5. Audit task tersebut SECARA SINGKAT saja, jangan melakukan full repository audit.
6. Jika contract/dependency sudah tersedia:
   LANGSUNG IMPLEMENTASIKAN.
7. Jika task membutuhkan approval/contract/environment yang belum tersedia:
   SKIP task tersebut dan cari task unlocked berikutnya.
8. Jangan membuat contract atau architecture secara speculative hanya untuk membuka task.
9. Jangan mengerjakan fitur acak di luar roadmap.
10. Jangan menyentuh Gorouter.app.
11. NVIDIA dan TokenHarbor jangan disentuh kecuali memang menjadi dependency langsung task yang dipilih.

Untuk task yang dipilih:

- implementasikan secara modular sesuai architecture repository,
- tambahkan test yang relevan,
- jangan mengubah fitur yang sudah selesai tanpa alasan,
- jangan memasukkan secret/credential,
- jangan membuat fake production infrastructure.

Setelah implementation selesai jalankan validation yang tersedia:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check
node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan membuat scripts/check-symlinks.mjs jika file tersebut tidak tersedia.

Jika validation PASS:

1. review git diff,
2. pastikan perubahan hanya untuk task yang dipilih,
3. buat SATU commit,
4. push ke:
   git push origin backend-dev-recovery
5. verifikasi local SHA == remote SHA,
6. pastikan working tree clean.

Jika tidak ada task yang unlocked:

JANGAN mengulang audit.

Tampilkan singkat:
- B-040: BLOCKED — human approval belum tersedia.
- Tidak ada independent task yang unlocked.
- Tidak ada code change.
- Tidak ada commit.
- Tidak ada push.

Jika ada task unlocked, JANGAN berhenti pada laporan audit.
LANGSUNG CODING → TEST → COMMIT → PUSH.

Kerjakan langsung di:
/root/botspace

```
# Prompt: B-040 Approval → Implementation → Continue Roadmap
```

Lanjutkan project BotSpace dari kondisi repository SAAT INI di:

/root/botspace

PENTING:
Jangan mengulang audit besar yang sudah dilakukan sebelumnya.
Jangan hanya membuat laporan audit lalu berhenti.
Tujuan prompt ini adalah membuka B-040 jika approval yang diperlukan memang sudah tersedia, kemudian LANGSUNG melakukan implementation work yang sudah unlocked, menjalankan validation, commit, push, dan melanjutkan roadmap ke dependency berikutnya yang benar-benar dapat dikerjakan.

==================================================
KONDISI TERAKHIR YANG SUDAH DIKONFIRMASI
==================================================

Repository:
- Branch: backend-dev-recovery
- Working tree terakhir: CLEAN
- Local SHA dan remote SHA terakhir: sama
- Repository sudah melalui beberapa audit sebelumnya.
- Jangan mengulang pekerjaan B-030.
- Jangan mengulang B-070.
- Jangan mengulang B-071.
- Jangan mengulang production wiring B-071.
- Jangan mengulang SecretResolver boundary yang sudah tersedia.
- Jangan mengulang verification yang sudah selesai.

Validation terakhir yang sudah diketahui PASS:
- pnpm test
- pnpm build
- pnpm typecheck
- pnpm lint
- pnpm format:check
- import check
- ownership check
- documentation/link check
- git diff --check

Integration yang tidak tersedia sebelumnya:
- PostgreSQL integration: PERSISTENCE_TEST_DATABASE_URL belum tersedia.
- MinIO/S3 smoke environment belum tersedia.
- scripts/check-symlinks.mjs memang tidak tersedia.
- Gorouter.app integration TIDAK BOLEH dijalankan.

NVIDIA dan TokenHarbor:
- jangan disentuh kecuali perubahan yang sedang dikerjakan secara langsung dan tidak dapat dihindari berkaitan dengannya.
- Jangan menjalankan Gorouter.app.

==================================================
STATUS ROADMAP TERAKHIR
==================================================

Audit terakhir menunjukkan:

B-030:
DONE

B-070:
DONE

B-071:
DONE / production wiring selesai

SecretResolver application boundary:
DONE

Infrastructure verification:
SUDAH diaudit dan tidak perlu diulang tanpa dependency baru.

B-040 / ADR-011:
BLOCKED hanya karena membutuhkan human approval lintas owner.

B-041:
BLOCKED oleh B-040.

B-050 / B-051 / B-052:
BLOCKED oleh dependency B-040.

Frontend Telegram yang bergantung pada B-040:
BLOCKED.

Queue/operator/billing/abuse-control/telemetry/release/infrastructure:
tetap deferred jika contract/provider/evidence belum tersedia.

AI dan marketplace:
tetap deferred karena requirement belum tersedia.

==================================================
TUJUAN UTAMA
==================================================

Sekarang lakukan:

1. Verifikasi apakah HUMAN APPROVAL untuk B-040 / ADR-011 sudah tersedia di repository/documentation/decision package atau diberikan melalui konteks kerja saat ini.

2. JIKA APPROVAL SUDAH ADA:
   - anggap B-040 unlocked,
   - jangan melakukan audit B-040 dari awal,
   - gunakan approval/decision package yang sudah tersedia sebagai source of truth,
   - langsung implementasikan B-040 sesuai contract/decision yang telah disetujui.

3. JIKA APPROVAL BELUM ADA:
   - JANGAN mengarang approval.
   - JANGAN menganggap approval ada.
   - JANGAN melakukan audit panjang lagi.
   - Tampilkan status singkat:
     B-040 tetap BLOCKED — human approval belum tersedia.
   - Jangan mengubah source code.
   - Jangan membuat commit.
   - Jangan membuat empty commit.
   - Berhenti setelah pemeriksaan singkat tersebut.

4. JIKA APPROVAL ADA, jangan berhenti setelah membuat dokumentasi.
   Lanjutkan sampai implementation B-040 selesai atau sampai menemukan dependency nyata yang memang belum tersedia.

==================================================
BAGIAN 1 — APPROVAL CHECK
==================================================

Periksa decision package yang sudah dibuat sebelumnya.

Cari:

- ADR-011
- B-040 approval package
- architecture approval
- Telegram/provider owner approval
- Security owner approval
- Deployment owner approval
- explicit sign-off
- decision matrix
- accepted/rejected/pending decisions

Jangan membuat approval baru sendiri.

Approval harus dianggap valid hanya jika memang ada evidence yang jelas.

Jika approval ditemukan:

catat secara internal:
- approval source,
- approved scope,
- owner/sign-off yang tersedia,
- decision constraints.

Jangan meminta Kiro untuk mengulang seluruh audit.

==================================================
BAGIAN 2 — B-040 SCOPE
==================================================

Jika B-040 unlocked, implementasikan B-040 sesuai approved decision.

B-040 berkaitan dengan Telegram/provider account connection foundation.

Gunakan keputusan yang SUDAH DISETUJUI sebagai source of truth untuk:

- authentication mechanism,
- provider/library boundary,
- account identity,
- connection identity,
- session model,
- credential lifecycle,
- credential storage,
- SecretResolver boundary,
- connect semantics,
- disconnect semantics,
- revoke semantics,
- reconnect semantics,
- account removal,
- workspace authorization,
- actor attribution,
- versioned API contract,
- error contract,
- idempotency,
- concurrency,
- persistence,
- migration,
- event model,
- runtime handoff,
- provider ownership,
- capability boundary.

JANGAN memilih mechanism baru jika ADR-011 sudah menentukan pilihan.

JANGAN membuat architecture alternatif hanya karena implementation belum ada.

JANGAN membuat vendor/provider SDK dependency jika approved decision belum menetapkannya.

==================================================
BAGIAN 3 — ACCOUNT/SESSION MODEL
==================================================

Implementasikan account/session model sesuai approved contract.

Pastikan secara eksplisit ada pemisahan antara:

- account identity,
- connection identity,
- session identity,
- workspace ownership,
- credential reference,
- provider identity,
- runtime handoff state.

Jangan mencampurkan:

- BotInstallation.status
dengan
- runtime process state.

BotInstallation.status harus tetap menjadi lifecycle/domain state yang sudah ada.

Jangan mengubahnya menjadi status proses Telegram runtime.

==================================================
BAGIAN 4 — CREDENTIAL SECURITY
==================================================

Credential lifecycle harus mengikuti approved security decision.

Pastikan:

- credential tidak disimpan plaintext jika contract tidak mengizinkannya,
- secret resolution melewati SecretResolver boundary yang sudah ada,
- tidak ada secret hardcoded,
- tidak ada token/API key/password di source,
- tidak ada secret di log,
- tidak ada secret di error response,
- tidak ada secret di event payload,
- tidak ada credential di test fixture yang menyerupai production credential.

Gunakan synthetic/test credentials hanya pada test.

Jika implementation membutuhkan managed secret infrastructure yang belum tersedia:
- jangan membuat fake production secret manager,
- gunakan abstraction yang sudah tersedia,
- tandai hanya infrastructure verification sebagai deferred,
- jangan memblokir implementation yang memang dapat dilakukan tanpa infrastructure nyata.

==================================================
BAGIAN 5 — CONNECT / DISCONNECT / REVOKE
==================================================

Implementasikan behavior yang memang sudah disetujui oleh ADR-011.

Minimal pastikan jika didukung contract:

CONNECT:
- valid workspace,
- valid actor,
- provider validation,
- connection creation,
- account/session association,
- credential reference handling.

DISCONNECT:
- connection dapat dinonaktifkan/dilepas sesuai lifecycle,
- tidak menghapus data yang contract melarang untuk dihapus.

REVOKE:
- credential/session tidak dapat digunakan lagi setelah revoke,
- revoke behavior idempotent jika contract mensyaratkannya.

RECONNECT:
- mengikuti lifecycle yang telah disetujui,
- tidak membuat duplicate connection jika idempotency mengharuskannya.

ACCOUNT REMOVAL:
- hanya jika memang termasuk approved B-040 scope,
- hormati retention/deletion policy.

Jangan menambahkan behavior di luar approved contract.

==================================================
BAGIAN 6 — WORKSPACE AUTHORIZATION
==================================================

Semua account/connection/session harus tetap terikat ke workspace yang benar.

Pastikan:

- workspace A tidak dapat membaca connection workspace B,
- workspace A tidak dapat memodifikasi connection workspace B,
- actor attribution benar,
- authorization dilakukan sebelum sensitive operation,
- provider ownership tidak dapat dibypass melalui ID langsung,
- object/account identifier tidak menjadi satu-satunya security boundary.

Tambahkan test untuk cross-workspace access.

==================================================
BAGIAN 7 — API CONTRACT
==================================================

Jika B-040 approved API contract sudah tersedia:

implementasikan API tersebut.

Jangan membuat endpoint alternatif hanya karena lebih mudah.

Pastikan:

- request validation,
- response shape,
- HTTP status,
- error code,
- idempotency,
- concurrency,
- authorization,
- provider error mapping

sesuai contract yang approved.

Jangan membocorkan:

- credential,
- provider secret,
- session token,
- internal storage key,
- stack trace,
- internal filesystem path.

==================================================
BAGIAN 8 — PERSISTENCE
==================================================

Jika B-040 membutuhkan schema/migration:

implementasikan hanya field/table/index yang diperlukan oleh approved contract.

Pastikan:

- migration deterministic,
- uniqueness constraint sesuai contract,
- workspace ownership terjaga,
- transaction boundary jelas,
- duplicate connection behavior sesuai idempotency,
- revoke state dapat dipersist,
- session/account lifecycle dapat dipersist.

Jangan membuat schema speculative.

Jangan membuat migration untuk fitur yang belum approved.

Jangan menjalankan migration destruktif pada database production.

==================================================
BAGIAN 9 — EVENTS
==================================================

Jika approved B-040 contract sudah menentukan event:

implementasikan event sesuai contract.

Jangan membuat event baru secara speculative.

Pastikan event:

- memiliki nama yang sesuai contract,
- payload sesuai schema,
- tidak berisi secret,
- tidak berisi raw credential,
- memiliki actor/workspace attribution jika contract membutuhkan,
- delivery semantics sesuai keputusan.

Jika event boundary belum tersedia dan memang merupakan dependency B-040:
- implementasikan hanya boundary yang memang termasuk B-040,
- jangan membuat event architecture besar di luar scope.

==================================================
BAGIAN 10 — RUNTIME HANDOFF
==================================================

B-040 membutuhkan pemisahan yang jelas antara:

ACCOUNT/CONNECTION LIFECYCLE

dan

BOT RUNTIME PROCESS.

Jangan menjalankan Telegram polling/webhook runtime hanya untuk membuktikan B-040.

Implementasikan runtime handoff/capability boundary hanya jika contract B-040 sudah mendefinisikannya.

Pastikan:

- provider ownership jelas,
- allowed runtime state jelas,
- handoff tidak memberikan credential mentah ke consumer yang tidak berwenang,
- revoke dapat memblokir handoff berikutnya,
- capability boundary tidak dapat digunakan lintas workspace.

==================================================
BAGIAN 11 — TESTING
==================================================

Setelah implementation B-040:

tambahkan/perbaiki test yang benar-benar diperlukan.

Minimal:

- account creation,
- connection identity,
- workspace ownership,
- workspace isolation,
- authorization,
- duplicate/idempotency,
- reconnect,
- disconnect,
- revoke,
- credential reference handling,
- SecretResolver interaction,
- missing credential,
- provider error mapping,
- persistence,
- migration,
- event behavior jika contract mendukung,
- concurrency behavior jika contract mendukung,
- runtime handoff boundary jika contract mendukung.

Jangan membuat fake behavior hanya supaya test PASS.

==================================================
BAGIAN 12 — VALIDATION CEPAT DAN LENGKAP
==================================================

Setelah implementation selesai jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan membuat:

scripts/check-symlinks.mjs

Jika file tidak tersedia, cukup:

SKIPPED — scripts/check-symlinks.mjs unavailable

PostgreSQL:

Jika PERSISTENCE_TEST_DATABASE_URL tersedia:
- jalankan integration test yang relevan.

Jika tidak:
- jangan membuat database palsu,
- jangan mengubah test,
- laporkan:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

MinIO/S3:

Jika environment tersedia:
- jalankan smoke test yang relevan.

Jika tidak:
- laporkan:

SKIPPED — MinIO/S3 test environment unavailable

Gorouter.app:
- JANGAN dijalankan.

NVIDIA/TokenHarbor:
- jangan menjalankan test tambahan yang tidak diperlukan oleh perubahan.

==================================================
BAGIAN 13 — SECURITY REVIEW
==================================================

Sebelum commit lakukan targeted review terhadap perubahan B-040.

Cari:

- hardcoded secret,
- API key,
- password,
- access token,
- session token,
- provider credential,
- unsafe logging,
- credential response leakage,
- cross-workspace authorization bypass,
- insecure direct object reference,
- incorrect revoke behavior,
- duplicate connection race,
- unsafe persistence,
- migration issue,
- event secret leakage.

Jika ditemukan issue:
- perbaiki sekarang jika berada dalam scope B-040.

Jangan hanya melaporkan issue yang jelas berasal dari implementation baru.

==================================================
BAGIAN 14 — DIFF REVIEW
==================================================

Setelah validation:

git status
git diff --stat
git diff

Review seluruh perubahan.

Pastikan tidak ada:

- unrelated refactor,
- generated junk,
- temporary files,
- credentials,
- secrets,
- changes to Gorouter.app,
- unrelated NVIDIA changes,
- unrelated TokenHarbor changes,
- speculative AI feature,
- marketplace feature,
- billing feature,
- queue feature,
- telemetry system besar,
- frontend feature yang belum menjadi dependency B-040.

Jika ada perubahan tidak relevan:
hapus sebelum commit.

==================================================
BAGIAN 15 — COMMIT
==================================================

Jika implementation B-040 selesai dan validation memadai:

buat SATU commit.

Gunakan commit message yang sesuai dengan perubahan aktual, misalnya:

feat: implement B-040 account connection foundation

Jangan membuat banyak commit kecil.

Jangan membuat empty commit.

==================================================
BAGIAN 16 — PUSH
==================================================

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

git rev-parse HEAD

git rev-parse origin/backend-dev-recovery

Pastikan SHA sama.

Pastikan:

git status

menunjukkan working tree clean.

Jika push gagal karena credential/network:
- jangan mengubah credential Git sembarangan,
- jangan menghapus commit,
- jangan membuat commit tambahan,
- laporkan error push secara jelas.

==================================================
BAGIAN 17 — LANJUT ROADMAP OTOMATIS
==================================================

INI BAGIAN PENTING.

Jika B-040 berhasil diimplementasikan dan dipush:

JANGAN berhenti hanya karena B-040 selesai.

Audit dependency berikutnya SECARA RINGKAS berdasarkan roadmap yang sudah ada.

Prioritas:

1. B-041 jika seluruh dependency B-040 sudah terpenuhi.
2. B-050/B-051/B-052 jika dependency B-040/B-041 yang diperlukan sudah terpenuhi.
3. Telegram frontend/runtime handoff jika contract/provider dependency sudah tersedia.
4. Infrastruktur yang sebelumnya blocked jika environment sekarang tersedia.
5. Task berikutnya yang memiliki dependency paling lengkap.

Namun:

JANGAN langsung mengerjakan task berikutnya jika membutuhkan approval/contract/provider yang belum ada.

Jika task berikutnya masih blocked:
- catat alasan dependency,
- lanjut ke task lain yang benar-benar unlocked jika ada.

Jangan membuat fitur acak.

==================================================
ATURAN ANTI-AUDIT LOOP
==================================================

Jangan lakukan:

- audit repository penuh berulang kali,
- membaca semua file tanpa alasan,
- membuat decision package baru yang sama,
- mengulang B-040 approval package,
- mengulang security report yang sudah selesai,
- mengulang validation yang tidak diperlukan sebelum implementation.

Gunakan hasil audit sebelumnya sebagai baseline.

Audit hanya bagian yang diperlukan untuk implementasi.

Jika sebuah dependency sudah jelas DONE:
jangan audit ulang kecuali perubahan baru menyentuhnya.

Jika sebuah dependency jelas BLOCKED:
jangan mencoba mengakali blocker.

Jika approval sudah ada:
langsung implementation.

Jika approval belum ada:
berhenti singkat dan jangan coding.

==================================================
OUTPUT AKHIR
==================================================

Jika approval belum ada:

Tampilkan hanya:

B-040/ADR-011:
BLOCKED — human approval belum tersedia.

No code changed.
No commit created.
No push performed.

Jangan mengulang audit.

Jika approval ada dan implementation selesai:

Tampilkan:

### B-040
- approval:
- implementation:
- account model:
- session model:
- credential boundary:
- authorization:
- persistence:
- API:
- events:
- runtime handoff:

### Validation
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
- PostgreSQL:
- MinIO/S3:

### Security
- credential leakage:
- workspace isolation:
- authorization:
- revoke:
- error/log sanitization:

### Git
- commit:
- push:
- local SHA:
- remote SHA:
- working tree:

### Remaining Blocked
Hanya tampilkan blocker yang BENAR-BENAR masih ada.

### NEXT SINGLE ACTION
Tentukan task berikutnya berdasarkan dependency nyata.

Jangan memberikan daftar panjang pekerjaan hipotetis.

KERJAKAN LANGSUNG PADA:

/root/botspace

Dan jangan berhenti pada audit jika B-040 sudah benar-benar unlocked.

```
# 
```

Lanjutkan `/root/botspace` pada branch `backend-dev-recovery`.

JANGAN melakukan full audit, full test, build, typecheck, lint, security scan, atau repository-wide scan lagi.

Gunakan hasil audit dan `docs/architecture/ADR-011-telegram-account-connection.md` yang SUDAH ADA.

Tujuan hanya menentukan status B-040/ADR-011.

1. Baca approval/decision package yang sudah ada.
2. Jangan mengubah source code.
3. Jangan membuat schema, contract, provider, authentication, account/session implementation, atau runtime.
4. Jangan membuat approval palsu.
5. Jangan commit/push jika tidak ada perubahan.

Tentukan secara singkat:

- apakah human approval B-040 SUDAH ADA atau BELUM;
- siapa/role yang masih harus memberikan approval;
- keputusan apa saja yang wajib disetujui;
- dependency apa yang akan terbuka setelah approval;
- next single action.

Jika approval BELUM ADA, berhenti setelah laporan tersebut.

JANGAN mengulang audit sebelumnya.

Output maksimal 15 baris.

```
# 
```

# Prompt: B-040 Human Approval Gate

Lanjutkan dari `/root/botspace` pada branch `backend-dev-recovery`.

Status saat ini:
- B-040/ADR-011 masih BLOCKED.
- Tidak ada B-040 dependency yang unlocked.
- Working tree clean.
- Tidak ada source code yang perlu diubah.
- Human approval lintas Architecture, Telegram/provider, Security, dan Deployment belum tercatat sebagai APPROVED.

JANGAN melakukan implementasi B-040.

Lakukan hanya pemeriksaan approval gate:

1. Baca:
   `docs/architecture/ADR-011-telegram-account-connection.md`

2. Identifikasi format/catatan approval yang memang sudah digunakan repository.

3. Periksa apakah sudah ada approval manusia yang eksplisit dan dapat diverifikasi untuk B-040.

4. Jika BELUM ada:
   - jangan mengubah source code,
   - jangan membuat commit,
   - jangan membuat approval palsu,
   - jangan menganggap hasil audit sebagai approval,
   - tampilkan persis apa yang masih dibutuhkan untuk approval B-040.

5. Jika SUDAH ada approval eksplisit:
   - verifikasi scope approval,
   - jangan langsung implementasi,
   - tampilkan dependency B-040 yang sekarang unlocked,
   - tampilkan task implementasi pertama yang diizinkan.

Jangan menyentuh:
- B-030
- B-070
- B-071
- Gorouter.app
- NVIDIA
- TokenHarbor
- provider/runtime lain yang tidak terkait langsung.

Tidak perlu membuat commit jika tidak ada perubahan.

Output hanya:
- Approval status
- Approved scope
- Remaining approval
- Unlocked dependencies
- Next single action

```
# 
```
# Prompt: B-040 Approval Gate Check

Lanjutkan dari repository `/root/botspace` pada branch `backend-dev-recovery`.

Periksa status approval B-040/ADR-011.

1. Baca approval package:
   `docs/architecture/ADR-011-telegram-account-connection.md`

2. Periksa apakah sudah ada approval manusia yang VALID untuk:
   - Architecture
   - Telegram/provider
   - Security
   - Deployment

3. Jangan menganggap dokumentasi atau hasil audit sebagai approval.

4. Jika approval belum lengkap:
   - JANGAN mengubah source code.
   - JANGAN mengimplementasikan B-040.
   - Jangan membuat commit.
   - Tampilkan decision yang masih PENDING.
   - Tetapkan:
     `NEXT SINGLE ACTION: Obtain human approval for B-040/ADR-011.`

5. Jika approval lengkap dan dapat diverifikasi:
   - jangan langsung implementasi,
   - tampilkan keputusan yang telah APPROVED,
   - tampilkan dependency yang sekarang unlocked,
   - tentukan implementation task B-040 pertama berdasarkan approval tersebut.

Jangan menyentuh B-030, B-070, B-071, Gorouter.app, NVIDIA, atau TokenHarbor.


```
# Prompt: B-040 Approval Package — ADR-011
```
# Prompt: BotSpace — Prepare B-040 / ADR-011 Human Approval Package

Lanjutkan project BotSpace dari kondisi repository saat ini.

Repository:
`/root/botspace`

Branch:
`backend-dev-recovery`

==================================================
CURRENT STATE
==================================================

B-030, B-070, dan B-071 sudah selesai.

Validation terakhir PASS.

Working tree:
CLEAN

Local SHA:
sama dengan remote SHA.

B-040 / ADR-011 saat ini BLOCKED karena human approval belum tersedia.

Approval yang masih diperlukan:

- Architecture: belum tersedia
- Telegram/provider: belum tersedia
- Security: belum tersedia
- Deployment: belum tersedia

Decision yang belum disetujui:

- authentication mechanism
- provider/library
- account/session model
- credential lifecycle
- connect semantics
- disconnect semantics
- revoke semantics
- versioned API contract
- persistence contract
- event contract
- runtime handoff boundary

==================================================
TUJUAN
==================================================

JANGAN implementasikan B-040.

JANGAN membuat source-code changes.

JANGAN membuat fake approval.

JANGAN memilih keputusan architecture secara sepihak.

Sekarang hanya siapkan PACKAGE APPROVAL B-040/ADR-011 agar human owner dapat melakukan review dan approval.

==================================================
STEP 1 — AUDIT CURRENT DOCUMENTATION
==================================================

Baca dan audit:

- ADR-011
- B-040 decision package
- approval matrix
- AI_CONTEXT.md
- AI_TASKS.md
- PROJECT_STATUS.md
- ROADMAP_V2.md
- CHANGELOG.md
- docs/architecture/DECISIONS.md
- seluruh dokumentasi terkait Telegram account connection

Gunakan keputusan yang SUDAH tertulis di repository.

Jangan mengarang keputusan baru.

==================================================
STEP 2 — PREPARE DECISION MATRIX
==================================================

Buat decision matrix yang jelas untuk human reviewer.

Untuk setiap keputusan tampilkan:

1. Decision
2. Current repository evidence
3. Proposed option(s), jika memang sudah ada di repository
4. Consequence
5. Security impact
6. Migration/persistence impact
7. Runtime impact
8. Owner yang harus approve
9. Status

Minimal matrix:

### Authentication
- mechanism
- provider/library
- authentication lifecycle

### Account/Session
- account identity
- session model
- connection state
- reconnect behavior

### Credential Lifecycle
- storage
- resolution
- rotation
- revoke
- retention/deletion
- unavailable-secret behavior

### Connection Semantics
- connect
- disconnect
- revoke
- reconnect

### API Contract
- request
- response
- errors
- idempotency
- concurrency

### Persistence
- account/session records
- uniqueness
- transaction boundary
- ownership
- deletion/revoke behavior

### Events
- event names
- payload
- delivery guarantee
- retry behavior

### Runtime Handoff
- capability boundary
- allowed states
- provider ownership
- revoke propagation
- runtime lifecycle separation

==================================================
STEP 3 — SECURITY REVIEW PACKAGE
==================================================

Siapkan bagian khusus untuk Security owner.

Pastikan package menjelaskan:

- credential tidak disimpan plaintext jika contract tidak mengizinkannya,
- credential tidak masuk log,
- session tidak bocor,
- revoke semantics,
- workspace isolation,
- account ownership,
- provider boundary,
- secret resolver boundary,
- runtime handoff boundary,
- error sanitization.

Jangan membuat implementation baru.

==================================================
STEP 4 — DEPLOYMENT REVIEW PACKAGE
==================================================

Siapkan bagian untuk Deployment owner:

- required configuration,
- secret references,
- SecretResolver dependency,
- runtime configuration,
- persistence dependency,
- provider dependency,
- startup requirements,
- environment requirements.

Jangan memasukkan secret aktual.

==================================================
STEP 5 — TELEGRAM/PROVIDER REVIEW PACKAGE
==================================================

Siapkan bagian untuk Telegram/provider owner:

- authentication mechanism,
- provider SDK/library,
- account identity,
- session lifecycle,
- connect/disconnect/revoke,
- reconnect behavior,
- provider error mapping,
- runtime ownership,
- capability limitations.

Jika provider/library belum ditentukan:

JANGAN memilih sendiri.

Tandai:

`DECISION REQUIRED — provider/library not approved`

==================================================
STEP 6 — ARCHITECTURE REVIEW PACKAGE
==================================================

Siapkan architecture decision summary:

- domain boundary,
- application service boundary,
- provider adapter boundary,
- SecretResolver boundary,
- persistence boundary,
- API boundary,
- event boundary,
- runtime handoff boundary.

Pastikan account lifecycle TIDAK dicampur dengan bot runtime lifecycle.

Jangan mengubah:

`BotInstallation.status`

menjadi process/runtime state.

==================================================
STEP 7 — APPROVAL MATRIX
==================================================

Buat approval matrix final:

| Decision | Architecture | Telegram/Provider | Security | Deployment | Status |
|----------|--------------|-------------------|----------|------------|--------|

Setiap decision yang belum disetujui harus tetap:

`PENDING`

Jangan mengubah PENDING menjadi APPROVED.

==================================================
STEP 8 — DOCUMENTATION
==================================================

Jika repository memang sudah memiliki format approval/decision package:

gunakan format tersebut.

Jika perlu memperbarui documentation:

ubah hanya documentation yang memang menjadi source of truth untuk B-040.

Jangan membuat banyak README baru.

Gunakan documentation existing.

Jangan membuat commit jika hanya menghasilkan laporan sementara dan repository policy tidak mengharuskannya.

==================================================
STEP 9 — VALIDATION
==================================================

Karena task ini documentation/approval preparation:

Jalankan hanya validation yang relevan.

Minimal:

- git status
- git diff --check
- documentation/link validation yang tersedia

Jangan menjalankan integration test provider yang tidak diperlukan.

Jangan menjalankan Gorouter.app.

NVIDIA/TokenHarbor tidak perlu disentuh.

==================================================
STEP 10 — GIT SAFETY
==================================================

Jika tidak ada perubahan:

- jangan membuat empty commit.

Jika documentation berubah:

- review git diff,
- pastikan tidak ada secret,
- pastikan tidak ada fake approval,
- commit hanya jika perubahan memang diperlukan sebagai official B-040 approval package.

Jangan push jika repository policy meminta human review sebelum documentation approval.

Jika perubahan memang harus dipush sesuai workflow:

`git push origin backend-dev-recovery`

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### B-040 Approval Status
- Architecture: PENDING / APPROVED
- Telegram/provider: PENDING / APPROVED
- Security: PENDING / APPROVED
- Deployment: PENDING / APPROVED

### Decision Matrix
Tampilkan semua keputusan yang masih membutuhkan approval.

### Approval Package
- lokasi document/package:
- decision count:
- pending count:

### Security Review
- credential lifecycle:
- session lifecycle:
- workspace isolation:
- revoke:
- runtime boundary:

### Validation
- documentation:
- links:
- diff:

### Git
- changed:
- commit:
- push:
- working tree:

### NEXT SINGLE ACTION

Jika approval masih belum tersedia:

`Obtain human approval for B-040/ADR-011 using the prepared decision package.`

JANGAN implementasikan B-040 sampai approval valid tersedia.

Jika approval valid kemudian tersedia pada repository, baru lanjutkan ke implementation B-040 sesuai keputusan yang telah disetujui.

PENTING:
- Jangan fake approval.
- Jangan memilih provider sendiri.
- Jangan coding B-040 sebelum approval.
- Jangan mengulang B-030/B-070/B-071.
- Jangan membuat fitur lain.
- Kerjakan langsung pada `/root/botspace`.


```
# Prompt: B-040 Implementation — Approval-Gated
```
# Prompt: BotSpace — B-040 Telegram Account Connection Implementation

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

Repository:
`/root/botspace`

Branch:
`backend-dev-recovery`

==================================================
CURRENT STATE
==================================================

Validation terakhir sudah PASS:

- pnpm test: PASS
- pnpm build: PASS
- pnpm typecheck: PASS
- pnpm lint: PASS
- pnpm format: PASS
- imports: PASS
- ownership: PASS
- docs: PASS
- secrets: PASS
- migration smoke: PASS
- git diff: PASS

Beberapa integration test tetap SKIPPED karena environment memang tidak tersedia:

- PostgreSQL: PERSISTENCE_TEST_DATABASE_URL unavailable
- MinIO/S3: environment unavailable
- symlink check: script unavailable

Security review tidak menemukan credential/secret leakage baru.

Git:

- working tree CLEAN
- local SHA == remote SHA
- branch: backend-dev-recovery
- tidak ada pekerjaan repository yang tersisa tanpa dependency approval.

B-040 / ADR-011 adalah blocker resmi terakhir.

==================================================
MANDATORY APPROVAL GATE
==================================================

SEBELUM MENYENTUH SOURCE CODE:

Cari evidence APPROVAL yang nyata di repository/documentation untuk B-040 / ADR-011.

Periksa:

- ADR-011
- B-040 decision package
- approval matrix
- architecture decision documentation
- PROJECT_STATUS.md
- CHANGELOG.md
- docs/architecture/DECISIONS.md

Approval HARUS memiliki evidence eksplisit dari owner yang diperlukan.

Owner/dependency yang harus diperiksa:

- Architecture
- Telegram/provider
- Security
- Deployment

Selain itu pastikan keputusan berikut sudah approved:

- authentication mechanism
- account/session model
- credential lifecycle
- connect semantics
- disconnect semantics
- revoke semantics
- versioned API contract
- persistence contract
- event contract
- runtime handoff boundary

JANGAN menganggap:

- dokumentasi draft = approval
- audit PASS = approval
- commit = approval
- human approval request = approval
- "ready" = approval

==================================================
IF APPROVAL IS NOT PRESENT
==================================================

Jika approval valid BELUM tersedia:

JANGAN melakukan implementation.

JANGAN membuat source-code changes.

JANGAN membuat fake approval.

JANGAN membuat contract baru.

JANGAN mengulang audit infrastructure yang sudah selesai.

JANGAN mengulang B-030/B-070/B-071.

JANGAN membuat empty commit.

Cukup tampilkan:

### B-040 STATUS
BLOCKED — human approval not found.

### REQUIRED APPROVAL
- Architecture:
- Telegram/provider:
- Security:
- Deployment:

### REQUIRED DECISIONS
- authentication:
- account/session:
- credential lifecycle:
- API:
- persistence:
- events:
- runtime handoff:

### NEXT ACTION
Obtain human approval for B-040/ADR-011.

Lalu STOP.

==================================================
IF VALID APPROVAL IS PRESENT
==================================================

HANYA jika evidence approval lengkap dan valid ditemukan, lanjutkan implementasi B-040.

==================================================
B-040 IMPLEMENTATION
==================================================

Audit implementation boundary yang SUDAH disetujui.

Implementasikan Telegram Account Connection secara modular.

Scope:

1. Account connection domain/service.
2. Authentication flow sesuai mechanism yang APPROVED.
3. Account/session lifecycle sesuai contract APPROVED.
4. Credential lifecycle sesuai security decision APPROVED.
5. Connect/disconnect/revoke semantics.
6. Persistence sesuai approved persistence contract.
7. API routes sesuai approved API contract.
8. Event emission sesuai approved event contract.
9. Runtime handoff hanya pada boundary yang APPROVED.
10. Workspace/account authorization.

Architecture requirements:

- Jangan membuat Telegram runtime/polling baru jika runtime handoff belum menjadi bagian implementation yang disetujui.
- Jangan mengubah `BotInstallation.status` menjadi process/runtime state.
- Pisahkan account lifecycle dari bot runtime lifecycle.
- Gunakan repository/service/adapter pattern yang sudah digunakan project.
- Jangan membuat global singleton tersembunyi.
- Gunakan dependency injection melalui composition root.
- Jangan mencampurkan HTTP layer dengan provider SDK.
- Provider-specific implementation harus berada pada adapter/provider boundary.
- Core application tidak boleh bergantung langsung pada provider-specific SDK.
- Jangan membuat abstraction kedua jika abstraction yang dibutuhkan sudah ada.

==================================================
SECURITY
==================================================

Credential/session handling WAJIB mengikuti approval ADR-011.

Pastikan:

- credential tidak masuk log,
- credential tidak masuk response,
- credential tidak masuk error message,
- credential tidak masuk test fixture plaintext,
- credential tidak masuk Git,
- session data tidak bocor,
- revoke benar-benar invalid,
- disconnect semantics sesuai contract,
- workspace isolation tetap berlaku.

Jangan hardcode:

- Telegram credential,
- API key,
- token,
- password,
- session secret.

Gunakan SecretResolver boundary yang SUDAH ADA.

==================================================
TESTING
==================================================

Tambahkan test hanya untuk behavior B-040 yang benar-benar diimplementasikan.

Minimal:

- authentication success/failure,
- account creation/connection,
- session lifecycle,
- disconnect,
- revoke,
- workspace authorization,
- workspace isolation,
- credential resolution,
- missing credential,
- provider error handling,
- persistence behavior,
- event behavior,
- runtime handoff boundary.

Jangan membuat fake provider behavior yang berbeda dari approved contract.

Jika provider integration membutuhkan environment nyata dan environment tidak tersedia:

- jangan membuat fake integration PASS,
- tandai SKIPPED/UNAVAILABLE,
- tetap jalankan unit/contract tests.

JANGAN menjalankan Gorouter.app.

NVIDIA/TokenHarbor tidak perlu disentuh kecuali perubahan B-040 secara langsung membutuhkan dependency tersebut.

==================================================
VALIDATION
==================================================

Setelah implementation:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan membuat `scripts/check-symlinks.mjs` jika memang tidak tersedia.

Jika ada integration test PostgreSQL dan:

`PERSISTENCE_TEST_DATABASE_URL`

tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat database palsu.

==================================================
SECURITY + DIFF REVIEW
==================================================

Sebelum commit:

- git status
- git diff --stat
- git diff

Pastikan tidak ada:

- secret,
- credential,
- session data,
- temporary files,
- generated junk,
- unrelated refactor,
- B-030 regression,
- B-070 regression,
- B-071 regression,
- Gorouter changes,
- speculative infrastructure.

==================================================
COMMIT + PUSH
==================================================

Jika implementation selesai dan validation PASS:

Buat SATU commit.

Gunakan message sesuai perubahan aktual, misalnya:

`feat: implement telegram account connection`

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

- local SHA
- remote SHA
- working tree clean

Jika push gagal:

- jangan mengubah credential GitHub sembarangan,
- jangan menghapus commit,
- jangan membuat empty commit.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### Approval Gate
- approval found:
- Architecture:
- Telegram/provider:
- Security:
- Deployment:
- decisions approved:

### B-040
- implementation status:
- authentication:
- account/session:
- credential lifecycle:
- connect:
- disconnect:
- revoke:
- API:
- persistence:
- events:
- runtime handoff:

### Security
- credential leak:
- session leak:
- workspace isolation:
- SecretResolver:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit:
- SHA:
- push:
- local/remote:
- working tree:

### Remaining Deferred
Tampilkan hanya dependency nyata yang masih blocked.

### Next Roadmap
Tentukan task berikutnya berdasarkan dependency graph setelah B-040.

PENTING:

Jika approval BELUM ada, JANGAN CODING DAN JANGAN MENGULANG AUDIT.

Jika approval SUDAH ada, langsung implementasikan B-040 sesuai keputusan yang telah disetujui.

Kerjakan langsung pada `/root/botspace`.


```
# Prompt: B-040 Implementation — Approval-Gated
```

# Prompt: BotSpace — B-040 Telegram Account Connection Implementation

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

Repository:
`/root/botspace`

Branch:
`backend-dev-recovery`

==================================================
CURRENT STATE
==================================================

Validation terakhir sudah PASS:

- pnpm test: PASS
- pnpm build: PASS
- pnpm typecheck: PASS
- pnpm lint: PASS
- pnpm format: PASS
- imports: PASS
- ownership: PASS
- docs: PASS
- secrets: PASS
- migration smoke: PASS
- git diff: PASS

Beberapa integration test tetap SKIPPED karena environment memang tidak tersedia:

- PostgreSQL: PERSISTENCE_TEST_DATABASE_URL unavailable
- MinIO/S3: environment unavailable
- symlink check: script unavailable

Security review tidak menemukan credential/secret leakage baru.

Git:

- working tree CLEAN
- local SHA == remote SHA
- branch: backend-dev-recovery
- tidak ada pekerjaan repository yang tersisa tanpa dependency approval.

B-040 / ADR-011 adalah blocker resmi terakhir.

==================================================
MANDATORY APPROVAL GATE
==================================================

SEBELUM MENYENTUH SOURCE CODE:

Cari evidence APPROVAL yang nyata di repository/documentation untuk B-040 / ADR-011.

Periksa:

- ADR-011
- B-040 decision package
- approval matrix
- architecture decision documentation
- PROJECT_STATUS.md
- CHANGELOG.md
- docs/architecture/DECISIONS.md

Approval HARUS memiliki evidence eksplisit dari owner yang diperlukan.

Owner/dependency yang harus diperiksa:

- Architecture
- Telegram/provider
- Security
- Deployment

Selain itu pastikan keputusan berikut sudah approved:

- authentication mechanism
- account/session model
- credential lifecycle
- connect semantics
- disconnect semantics
- revoke semantics
- versioned API contract
- persistence contract
- event contract
- runtime handoff boundary

JANGAN menganggap:

- dokumentasi draft = approval
- audit PASS = approval
- commit = approval
- human approval request = approval
- "ready" = approval

==================================================
IF APPROVAL IS NOT PRESENT
==================================================

Jika approval valid BELUM tersedia:

JANGAN melakukan implementation.

JANGAN membuat source-code changes.

JANGAN membuat fake approval.

JANGAN membuat contract baru.

JANGAN mengulang audit infrastructure yang sudah selesai.

JANGAN mengulang B-030/B-070/B-071.

JANGAN membuat empty commit.

Cukup tampilkan:

### B-040 STATUS
BLOCKED — human approval not found.

### REQUIRED APPROVAL
- Architecture:
- Telegram/provider:
- Security:
- Deployment:

### REQUIRED DECISIONS
- authentication:
- account/session:
- credential lifecycle:
- API:
- persistence:
- events:
- runtime handoff:

### NEXT ACTION
Obtain human approval for B-040/ADR-011.

Lalu STOP.

==================================================
IF VALID APPROVAL IS PRESENT
==================================================

HANYA jika evidence approval lengkap dan valid ditemukan, lanjutkan implementasi B-040.

==================================================
B-040 IMPLEMENTATION
==================================================

Audit implementation boundary yang SUDAH disetujui.

Implementasikan Telegram Account Connection secara modular.

Scope:

1. Account connection domain/service.
2. Authentication flow sesuai mechanism yang APPROVED.
3. Account/session lifecycle sesuai contract APPROVED.
4. Credential lifecycle sesuai security decision APPROVED.
5. Connect/disconnect/revoke semantics.
6. Persistence sesuai approved persistence contract.
7. API routes sesuai approved API contract.
8. Event emission sesuai approved event contract.
9. Runtime handoff hanya pada boundary yang APPROVED.
10. Workspace/account authorization.

Architecture requirements:

- Jangan membuat Telegram runtime/polling baru jika runtime handoff belum menjadi bagian implementation yang disetujui.
- Jangan mengubah `BotInstallation.status` menjadi process/runtime state.
- Pisahkan account lifecycle dari bot runtime lifecycle.
- Gunakan repository/service/adapter pattern yang sudah digunakan project.
- Jangan membuat global singleton tersembunyi.
- Gunakan dependency injection melalui composition root.
- Jangan mencampurkan HTTP layer dengan provider SDK.
- Provider-specific implementation harus berada pada adapter/provider boundary.
- Core application tidak boleh bergantung langsung pada provider-specific SDK.
- Jangan membuat abstraction kedua jika abstraction yang dibutuhkan sudah ada.

==================================================
SECURITY
==================================================

Credential/session handling WAJIB mengikuti approval ADR-011.

Pastikan:

- credential tidak masuk log,
- credential tidak masuk response,
- credential tidak masuk error message,
- credential tidak masuk test fixture plaintext,
- credential tidak masuk Git,
- session data tidak bocor,
- revoke benar-benar invalid,
- disconnect semantics sesuai contract,
- workspace isolation tetap berlaku.

Jangan hardcode:

- Telegram credential,
- API key,
- token,
- password,
- session secret.

Gunakan SecretResolver boundary yang SUDAH ADA.

==================================================
TESTING
==================================================

Tambahkan test hanya untuk behavior B-040 yang benar-benar diimplementasikan.

Minimal:

- authentication success/failure,
- account creation/connection,
- session lifecycle,
- disconnect,
- revoke,
- workspace authorization,
- workspace isolation,
- credential resolution,
- missing credential,
- provider error handling,
- persistence behavior,
- event behavior,
- runtime handoff boundary.

Jangan membuat fake provider behavior yang berbeda dari approved contract.

Jika provider integration membutuhkan environment nyata dan environment tidak tersedia:

- jangan membuat fake integration PASS,
- tandai SKIPPED/UNAVAILABLE,
- tetap jalankan unit/contract tests.

JANGAN menjalankan Gorouter.app.

NVIDIA/TokenHarbor tidak perlu disentuh kecuali perubahan B-040 secara langsung membutuhkan dependency tersebut.

==================================================
VALIDATION
==================================================

Setelah implementation:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Jangan membuat `scripts/check-symlinks.mjs` jika memang tidak tersedia.

Jika ada integration test PostgreSQL dan:

`PERSISTENCE_TEST_DATABASE_URL`

tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jangan membuat database palsu.

==================================================
SECURITY + DIFF REVIEW
==================================================

Sebelum commit:

- git status
- git diff --stat
- git diff

Pastikan tidak ada:

- secret,
- credential,
- session data,
- temporary files,
- generated junk,
- unrelated refactor,
- B-030 regression,
- B-070 regression,
- B-071 regression,
- Gorouter changes,
- speculative infrastructure.

==================================================
COMMIT + PUSH
==================================================

Jika implementation selesai dan validation PASS:

Buat SATU commit.

Gunakan message sesuai perubahan aktual, misalnya:

`feat: implement telegram account connection`

Kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

- local SHA
- remote SHA
- working tree clean

Jika push gagal:

- jangan mengubah credential GitHub sembarangan,
- jangan menghapus commit,
- jangan membuat empty commit.

==================================================
FINAL OUTPUT
==================================================

Tampilkan:

### Approval Gate
- approval found:
- Architecture:
- Telegram/provider:
- Security:
- Deployment:
- decisions approved:

### B-040
- implementation status:
- authentication:
- account/session:
- credential lifecycle:
- connect:
- disconnect:
- revoke:
- API:
- persistence:
- events:
- runtime handoff:

### Security
- credential leak:
- session leak:
- workspace isolation:
- SecretResolver:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit:
- SHA:
- push:
- local/remote:
- working tree:

### Remaining Deferred
Tampilkan hanya dependency nyata yang masih blocked.

### Next Roadmap
Tentukan task berikutnya berdasarkan dependency graph setelah B-040.

PENTING:

Jika approval BELUM ada, JANGAN CODING DAN JANGAN MENGULANG AUDIT.

Jika approval SUDAH ada, langsung implementasikan B-040 sesuai keputusan yang telah disetujui.

Kerjakan langsung pada `/root/botspace`.027301037463509027301037463509

```
# Prompt: B-040 Final Approval Readiness + Full Dependency Audit
```

# Prompt: BotSpace — B-040 Final Approval Readiness, Contract Audit & Dependency Unlock

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

Repository:
`/root/botspace`

Branch:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR
==================================================

Audit terakhir menunjukkan:

- Working tree CLEAN.
- Local SHA dan remote SHA sinkron.
- Tidak ada source implementation baru yang aman untuk dibuat saat ini.
- B-040 Telegram Account Connection masih BLOCKED.
- Next single action:
  Obtain human approval for B-040 / ADR-011.

Remaining deferred yang terlihat:

- B-040 membutuhkan human approval lintas Architecture, Telegram/provider, Security, dan Deployment.
- B-040 membutuhkan approved authentication mechanism.
- B-040 membutuhkan approved account/session model.
- B-040 membutuhkan approved credential lifecycle.
- B-040 membutuhkan approved API contract.
- B-040 membutuhkan approved persistence contract.
- B-040 membutuhkan approved event contract.
- B-040 membutuhkan approved runtime-handoff boundary.
- B-041 bergantung langsung pada B-040.
- B-050/B-051/B-052 bergantung pada contract/provider/runtime yang belum tersedia.
- Queue/scheduler/operator/billing/abuse-control/telemetry/release masih memiliki dependency yang belum tersedia.
- Managed Secret Manager masih menunggu vendor/deployment decision jika memang belum dipilih.
- PostgreSQL integration membutuhkan `PERSISTENCE_TEST_DATABASE_URL`.
- MinIO/S3 smoke test membutuhkan environment yang tersedia.
- Public-share rate limiting membutuhkan approved policy/middleware boundary.
- Public-share audit event membutuhkan approved event/service/repository boundary.
- Share expiry membutuhkan approved contract/schema/migration.
- AI dan marketplace masih deferred.

==================================================
ATURAN UTAMA
==================================================

JANGAN mengarang human approval.

JANGAN menganggap commit, dokumentasi draft, atau approval request sebagai approval.

JANGAN mengimplementasikan B-040 secara speculative.

JANGAN membuat:
- fake Telegram authentication,
- fake Telegram session,
- fake credential,
- fake provider,
- fake runtime,
- fake approval,
- fake API contract,
- fake persistence contract.

Jika approval belum ada, B-040 tetap BLOCKED.

Namun, jangan berhenti hanya dengan mengatakan "blocked".

Kerjakan SELURUH pekerjaan yang masih aman dan contract-backed untuk membuat B-040 READY TO IMPLEMENT setelah approval diberikan.

==================================================
BAGIAN 1 — AUDIT ADR-011
==================================================

Audit lengkap:

- ADR-011
- B-040 decision package
- architecture documentation
- PROJECT_STATUS.md
- ROADMAP_V2.md
- CHANGELOG.md
- AI_CONTEXT.md
- AI_TASKS.md
- approval matrix
- recent git history

Cari apakah ada perubahan terbaru terhadap:

- authentication mechanism,
- account/session model,
- credential storage,
- credential rotation,
- credential revoke,
- API contract,
- persistence contract,
- event contract,
- runtime handoff.

Jangan mengubah architecture hanya berdasarkan opini.

Jika ada conflict antar dokumen:

1. identifikasi conflict,
2. tentukan dokumen mana yang menjadi source of truth berdasarkan repository convention,
3. jangan mengarang keputusan baru,
4. dokumentasikan conflict yang masih membutuhkan owner decision.

==================================================
BAGIAN 2 — FINAL APPROVAL MATRIX
==================================================

Buat audit matrix yang jelas untuk B-040.

Periksa minimal:

1. Architecture owner
2. Telegram/provider owner
3. Security owner
4. Deployment/infrastructure owner
5. Authentication mechanism
6. Account/session model
7. Credential model
8. Credential lifecycle
9. Connect semantics
10. Disconnect semantics
11. Revoke semantics
12. API contract
13. Persistence contract
14. Event contract
15. Runtime handoff boundary
16. Versioned API contract
17. Minimum permissions
18. Workload identity
19. Secret manager boundary

Untuk setiap item tentukan:

- APPROVED
- DOCUMENTED BUT NOT APPROVED
- MISSING
- BLOCKED
- READY

Jangan mengubah status menjadi APPROVED tanpa evidence nyata.

==================================================
BAGIAN 3 — APPROVAL PACKAGE
==================================================

Jika approval package B-040/ADR-011 belum lengkap, rapikan dokumentasinya.

Tujuannya bukan membuat approval palsu.

Tujuannya membuat reviewer manusia dapat mengambil keputusan dengan jelas.

Approval package harus menjelaskan:

### A. Scope

Apa yang B-040 lakukan.

### B. Non-scope

Apa yang sengaja TIDAK dilakukan oleh B-040.

Contoh:
- tidak menjalankan Telegram bot runtime,
- tidak mengubah BotInstallation.status,
- tidak membuat queue,
- tidak membuat scheduler,
- tidak membuat billing,
- tidak membuat marketplace.

### C. Authentication

Dokumentasikan mekanisme authentication yang membutuhkan approval.

Jangan memilih mekanisme baru jika belum disetujui.

### D. Account/session model

Dokumentasikan bagaimana account/session seharusnya diperlakukan berdasarkan ADR.

### E. Credential lifecycle

Dokumentasikan:

- create/connect,
- use,
- refresh/rotation jika ada,
- revoke,
- disconnect,
- invalidation.

### F. Security boundary

Dokumentasikan:

- secret handling,
- workspace isolation,
- credential redaction,
- logging policy,
- storage boundary.

### G. API contract

Dokumentasikan endpoint/operation yang memang sudah disepakati.

Jika belum disepakati:

`PENDING APPROVAL`

Jangan membuat contract baru hanya untuk mengisi kekosongan.

### H. Persistence

Dokumentasikan persistence requirement.

Jika belum disetujui:

`PENDING APPROVAL`

### I. Runtime handoff

Dokumentasikan boundary antara account connection dan runtime.

Pastikan account connection tidak otomatis berarti Telegram bot runtime harus dijalankan.

==================================================
BAGIAN 4 — IMPLEMENTATION READINESS CHECK
==================================================

Audit repository untuk memastikan setelah approval diberikan, implementation dapat langsung dimulai.

Cari:

- existing auth infrastructure,
- existing account models,
- existing workspace authorization,
- existing secret resolver,
- existing repository patterns,
- existing API route patterns,
- existing error handling,
- existing event patterns,
- existing dependency injection/composition root,
- existing test patterns.

Buat daftar:

READY TO REUSE
vs
MISSING DEPENDENCY
vs
REQUIRES APPROVAL

Jangan membuat implementation jika dependency masih membutuhkan approval.

==================================================
BAGIAN 5 — DEPENDENCY GRAPH
==================================================

Buat dependency graph nyata:

B-040
  ↓
B-041
  ↓
B-050/B-051/B-052

Dan task lain yang bergantung pada B-040.

Jangan menganggap semua task Phase 4 dapat langsung dikerjakan.

Untuk setiap task berikutnya:

- contract available?
- provider available?
- runtime available?
- infrastructure available?
- approval available?

Jika salah satu dependency belum ada:

BLOCKED/DEFERRED.

==================================================
BAGIAN 6 — CARI PEKERJAAN YANG TIDAK TERBLOCK B-040
==================================================

Audit seluruh roadmap untuk mencari task yang benar-benar independent dari B-040.

Jika ada task yang:

- contract sudah tersedia,
- dependency lengkap,
- tidak membutuhkan human approval baru,
- tidak membutuhkan infrastructure yang belum tersedia,

maka BOLEH dikerjakan.

Tetapi:

JANGAN memilih task hanya karena nomor task lebih kecil/besar.

Gunakan dependency graph sebagai source of truth.

Jika tidak ada task yang aman:

jangan coding.

==================================================
BAGIAN 7 — INFRASTRUCTURE AUDIT
==================================================

Untuk PostgreSQL:

Periksa apakah:

`PERSISTENCE_TEST_DATABASE_URL`

tersedia.

Jika tersedia:
- jalankan integration test yang memang tersedia.

Jika tidak:
- jangan membuat fake database,
- jangan mengganti PostgreSQL dengan SQLite,
- tandai unavailable.

Untuk MinIO/S3:

Periksa apakah environment tersedia.

Jika tersedia:
- jalankan smoke test menggunakan synthetic/test-only credential.

Jika tidak:
- jangan install infrastructure permanen hanya untuk membuat test PASS,
- tandai unavailable.

Untuk Secret Manager:

Periksa apakah vendor/deployment decision sudah tersedia.

Jika belum:
- jangan memilih vendor sendiri,
- jangan memasang SDK vendor secara speculative.

==================================================
BAGIAN 8 — SECURITY AUDIT
==================================================

Lakukan audit source-level tanpa mengubah behavior yang sudah benar.

Cari:

- Telegram credential,
- bot token,
- session data,
- API key,
- password,
- secret,
- private key.

Pastikan tidak ada credential baru yang bocor.

Jangan menjalankan test provider yang tidak diperlukan.

Jangan menjalankan:

Gorouter.app

NVIDIA dan TokenHarbor jangan disentuh kecuali benar-benar diperlukan oleh perubahan yang sedang dikerjakan.

==================================================
BAGIAN 9 — VALIDATION
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

Jika file tidak tersedia:

SKIPPED — scripts/check-symlinks.mjs unavailable

JANGAN membuat script pengganti.

Jika PostgreSQL environment tidak tersedia:

SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable

Jika MinIO/S3 environment tidak tersedia:

SKIPPED — MinIO/S3 test environment unavailable

Jangan menyamarkan SKIPPED menjadi PASS.

==================================================
BAGIAN 10 — DOCUMENTATION
==================================================

Update hanya dokumentasi yang memang perlu.

Gunakan file yang sudah ada:

- AI_CONTEXT.md
- AI_TASKS.md
- PROJECT_STATUS.md
- ROADMAP_V2.md
- CHANGELOG.md
- docs/architecture/ADR-011-telegram-account-connection.md
- docs/architecture/DECISIONS.md

JANGAN membuat README baru.

Dokumentasikan:

1. B-040 masih blocked.
2. Approval yang masih diperlukan.
3. Evidence yang sudah tersedia.
4. Dependency yang sudah siap.
5. Dependency yang masih missing.
6. Exact next action setelah approval.

Jangan menulis "approved" jika belum ada approval.

==================================================
BAGIAN 11 — GIT
==================================================

Setelah pekerjaan audit/documentation:

jalankan:

git status
git diff --stat
git diff

Pastikan tidak ada:

- secret,
- credential,
- temporary file,
- generated junk,
- unrelated refactor,
- speculative implementation.

Jika perubahan documentation memang diperlukan:

buat SATU commit yang sesuai.

Contoh:

`docs: finalize B-040 approval readiness`

Jangan membuat empty commit.

Jika tidak ada perubahan:

jangan membuat commit.

Jika commit dibuat dan validation PASS:

git push origin backend-dev-recovery

Kemudian verifikasi:

LOCAL SHA == REMOTE SHA

dan:

working tree clean.

==================================================
BAGIAN 12 — FINAL DECISION
==================================================

Setelah semua audit selesai, tentukan salah satu:

CASE A:
B-040 APPROVED

→ Jika evidence approval benar-benar ada, lanjutkan implementasi B-040 sesuai ADR-011.

CASE B:
B-040 NOT APPROVED

→ Jangan coding B-040.
→ Pastikan approval package lengkap.
→ Identifikasi exact human decision yang diperlukan.
→ Cari task independent lain jika memang tersedia.

CASE C:
B-040 APPROVAL PARTIAL

→ Jangan implementasi bagian yang membutuhkan keputusan belum disetujui.
→ Kerjakan hanya bagian yang memang sudah contract-backed dan tidak bergantung pada unresolved decision.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan:

### B-040 Approval Status
- overall:
- Architecture:
- Telegram/provider:
- Security:
- Deployment:
- authentication:
- account/session:
- credential lifecycle:
- API:
- persistence:
- event:
- runtime handoff:

### Approval Package
- complete:
- missing decisions:
- exact reviewer decisions required:

### Implementation Readiness
- ready components:
- reusable components:
- missing dependencies:
- blocked dependencies:

### Dependency Graph
- B-040:
- B-041:
- B-050/B-051/B-052:
- other unlocked tasks:

### Infrastructure
- PostgreSQL:
- MinIO/S3:
- Secret Manager:

### Security
- credential leak:
- secret leak:
- workspace isolation:
- security status:

### Validation
- test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:

### Git
- commit:
- SHA:
- push:
- local/remote:
- working tree:

### FINAL NEXT ACTION

Tulis SATU tindakan paling tepat.

Jika B-040 masih blocked:

`Obtain human approval for B-040/ADR-011`

Jangan membuat task palsu hanya supaya roadmap terlihat berjalan.

==================================================
ATURAN PENUTUP
==================================================

Jangan mengarang approval.

Jangan membuat fake contract.

Jangan membuat fake provider.

Jangan membuat fake Telegram authentication.

Jangan membuat fake credentials.

Jangan membuat speculative runtime.

Jangan mengubah BotInstallation.status.

Jangan menjalankan Gorouter.app.

Jangan mengulang B-030, B-070, atau B-071.

Jangan membuat empty commit.

Kerjakan seluruh pekerjaan yang aman dan contract-backed sampai benar-benar tidak ada lagi pekerjaan repository yang dapat dilakukan tanpa keputusan manusia.

Kerjakan langsung pada `/root/botspace`.

```
# Prompt: B-040 Telegram Account Connection — Approval Gate → Full Implementation
```
# Prompt: BotSpace — B-040 Telegram Account Connection + Dependency Chain

Lanjutkan project BotSpace dari kondisi repository TERAKHIR.

KERJA LANGSUNG DI:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR YANG WAJIB DIHORMATI
==================================================

Repository saat ini sudah melalui audit dan validation besar.

Yang SUDAH SELESAI dan JANGAN DIULANG:

- B-030 Workspace API/Contract
- B-070 Storage Adapter
- B-071 File/Share contract
- B-071 File/Share API
- B-071 production wiring
- SecretResolver application boundary
- deployment/infrastructure verification yang memang dapat dilakukan dari environment
- security review yang sudah dilakukan
- ownership/path traversal/security checks yang sudah PASS

Validation terakhir menunjukkan:

- pnpm test: PASS
- pnpm build: PASS
- pnpm typecheck: PASS
- pnpm lint: PASS
- pnpm format:check: PASS
- check-imports: PASS
- check-ownership: PASS
- check-doc-links: PASS
- git diff --check: PASS
- Gorouter.app TIDAK dijalankan
- NVIDIA/TokenHarbor tidak disentuh
- working tree terakhir CLEAN
- local dan remote branch sebelumnya sudah sinkron

Repository juga sudah memiliki documentation/ADR package untuk:

`B-040 / ADR-011 Telegram Account Connection`

Approval package sebelumnya sudah dipersiapkan dan dipush.

==================================================
ATURAN PALING PENTING
==================================================

JANGAN mengarang approval.

Sebelum melakukan implementation B-040:

1. Audit repository untuk mencari status approval B-040/ADR-011.
2. Periksa:
   - ADR-011
   - docs/architecture/
   - PROJECT_STATUS.md
   - ROADMAP_V2.md
   - CHANGELOG.md
   - AI_CONTEXT.md
   - AI_TASKS.md
   - commit history
   - git log
   - branch state
   - dokumentasi approval matrix
   - decision package B-040
3. Tentukan apakah terdapat bukti approval manusia/owner yang eksplisit dan dapat dipertanggungjawabkan.

Approval dianggap VALID hanya jika repository memang memiliki bukti eksplisit bahwa B-040/ADR-011 telah disetujui oleh owner/maintainer/architecture/security/deployment authority yang relevan.

Jangan menganggap:
- commit biasa,
- dokumentasi draft,
- "ready",
- "prepared",
- "proposed",
- "should approve",
- "approval requested"

sebagai approval.

Jika approval VALID sudah ada:

→ LANJUTKAN IMPLEMENTASI B-040.

Jika approval BELUM ada:

→ JANGAN membuat implementation speculative.
→ Jangan membuat Telegram connector palsu.
→ Jangan membuat OAuth/device-code flow berdasarkan asumsi.
→ Jangan membuat polling/webhook.
→ Jangan mengubah BotInstallation.status.
→ Jangan membuat fake approval.
→ Jangan berhenti hanya karena ada banyak roadmap item lain.
→ Tampilkan dengan jelas bahwa B-040 masih blocked oleh approval manusia.

Namun sebelum berhenti, pastikan seluruh evidence approval sudah dicari dengan benar.

==================================================
BAGIAN 1 — AUDIT B-040
==================================================

Jika approval belum jelas, lakukan audit lengkap terlebih dahulu.

Audit:

- Telegram account connection architecture
- account/session model
- authentication mechanism
- credential boundary
- account/session lifecycle
- connect/disconnect/revoke semantics
- provider/runtime handoff
- API versioning
- persistence requirements
- workspace ownership
- security boundary
- deployment boundary

Gunakan ADR-011 sebagai source of truth.

Jangan membuat architecture baru apabila ADR-011 sudah menetapkan architecture.

Jika ada ketidaksesuaian antara implementation repository dan ADR:

- identifikasi secara spesifik,
- gunakan ADR sebagai design source of truth jika ADR sudah approved,
- jangan mengubah ADR diam-diam.

==================================================
BAGIAN 2 — B-040 IMPLEMENTATION
==================================================

HANYA jalankan bagian ini jika approval B-040 VALID.

Implementasikan Telegram Account Connection end-to-end berdasarkan ADR-011.

Scope minimal:

1. Telegram account identity model sesuai contract.
2. Workspace ownership.
3. Connection state machine.
4. Authentication mechanism yang telah disetujui.
5. Credential/session boundary.
6. Connect operation.
7. Connection status.
8. Disconnect/revoke operation.
9. Credential/session invalidation.
10. API contract.
11. Service layer.
12. Repository/persistence jika memang ditentukan oleh ADR.
13. Runtime handoff boundary jika memang sudah ditentukan.
14. Security/error handling.
15. Tests.

==================================================
BAGIAN 3 — SECURITY
==================================================

Telegram account connection adalah security-sensitive.

WAJIB:

- jangan menyimpan credential plaintext jika architecture tidak mengizinkannya,
- jangan mencetak credential,
- jangan mencetak session secret,
- jangan mengembalikan credential melalui API,
- jangan memasukkan secret ke error response,
- jangan memasukkan credential ke Git,
- jangan memasukkan credential ke documentation,
- jangan memasukkan Telegram auth material ke logs,
- workspace A tidak boleh membaca connection workspace B,
- revoke harus benar-benar memutus penggunaan credential/session,
- disconnect harus aman dan idempotent bila contract mengharuskannya.

Gunakan SecretResolver/credential boundary yang SUDAH ADA.

Jangan membuat SecretResolver kedua.

Jangan hardcode Telegram credential.

==================================================
BAGIAN 4 — ACCOUNT/SESSION LIFECYCLE
==================================================

Implementasikan lifecycle sesuai ADR-011.

Pastikan ada behavior yang jelas untuk:

- not connected,
- connecting,
- connected,
- failed,
- revoked/disconnected,

HANYA jika state tersebut memang ada di approved contract.

Jangan mengubah:

`BotInstallation.status`

menjadi process/runtime state.

Account connection state harus dipisahkan dari bot installation lifecycle.

Jangan membuat Telegram polling atau webhook runtime jika B-040 hanya mendefinisikan account connection boundary.

Jika runtime handoff memang bagian approved ADR:

- implementasikan boundary saja,
- jangan membuat background runtime speculative,
- jangan menjalankan Telegram bot tanpa contract/provider implementation yang diperlukan.

==================================================
BAGIAN 5 — API
==================================================

Implementasikan API sesuai contract yang sudah disetujui.

Minimal jika contract mendukung:

- connect account
- get connection status
- disconnect/revoke account

Gunakan workspace-scoped authorization.

Pastikan:

- user hanya dapat mengelola account yang dimilikinya,
- workspace isolation,
- invalid account ID ditolak,
- unauthorized access ditolak,
- revoked connection tidak dapat digunakan,
- error response aman,
- credential tidak pernah muncul di response.

Jangan membuat endpoint tambahan hanya karena terlihat berguna.

==================================================
BAGIAN 6 — PERSISTENCE
==================================================

Jika ADR-011 membutuhkan persistence:

Audit schema/repository architecture terlebih dahulu.

Gunakan pattern persistence yang sudah ada.

Jangan:

- membuat database abstraction kedua,
- membuat SQLite khusus,
- membuat schema palsu,
- menyimpan credential plaintext,
- membuat migration speculative.

Jika migration memang merupakan bagian approved B-040:

- buat migration yang minimal,
- gunakan ownership yang benar,
- gunakan constraint yang benar,
- tambahkan index hanya jika diperlukan,
- jangan merusak schema B-071.

Jika database integration environment tidak tersedia:

- tetap jalankan unit tests,
- jangan membuat database palsu,
- tandai integration test sebagai SKIPPED/UNAVAILABLE.

==================================================
BAGIAN 7 — TESTING
==================================================

Tambahkan test yang benar-benar membuktikan behavior.

Minimal:

- workspace authorization,
- workspace isolation,
- connect success,
- invalid authentication handling,
- connection state,
- get status,
- disconnect/revoke,
- revoked credential cannot be reused,
- missing account,
- duplicate connection behavior,
- credential redaction,
- secret tidak masuk logs,
- secret tidak masuk response,
- repository behavior,
- API error mapping.

Jika ada persistence integration test:

gunakan:

`PERSISTENCE_TEST_DATABASE_URL`

Jika environment tidak tersedia:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

Jangan mengubah test agar PASS.

==================================================
BAGIAN 8 — SECURITY REGRESSION
==================================================

Setelah implementation:

Cari seluruh source untuk kemungkinan:

- API key,
- Telegram token,
- bot token,
- session string,
- password,
- auth code,
- credential,
- private key,
- secret.

Pastikan tidak ada credential nyata yang masuk source.

Jalankan security/secret checks yang memang tersedia repository.

Jangan membuat fake secret hanya untuk membuat scanner PASS.

==================================================
BAGIAN 9 — VALIDATION LENGKAP
==================================================

Jalankan:

pnpm test
pnpm build
pnpm typecheck
pnpm lint
pnpm format:check

Kemudian:

node scripts/check-imports.mjs
node scripts/check-ownership.mjs
node scripts/check-doc-links.mjs
git diff --check

Untuk:

node scripts/check-symlinks.mjs

JANGAN membuat script baru.

Jika file tidak tersedia:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

PostgreSQL:

Jika `PERSISTENCE_TEST_DATABASE_URL` tersedia:
- jalankan integration test yang memang tersedia.

Jika tidak:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

==================================================
BAGIAN 10 — JANGAN SENTUH YANG TIDAK PERLU
==================================================

Jangan:

- mengulang B-030,
- mengulang B-070,
- mengulang B-071,
- mengubah B-071 schema tanpa dependency nyata,
- menambahkan share expiry,
- membuat public-share rate limiter speculative,
- membuat audit-event system speculative,
- membuat queue system,
- membuat scheduler,
- membuat billing,
- membuat marketplace,
- membuat AI feature,
- membuat Telegram polling,
- membuat Telegram webhook,
- mengubah BotInstallation.status,
- menjalankan integration test Gorouter.app.

NVIDIA dan TokenHarbor jangan disentuh.

==================================================
BAGIAN 11 — SETELAH B-040 SELESAI
==================================================

Jangan langsung mengerjakan fitur acak.

Setelah B-040 implementation selesai dan validation PASS:

1. Audit roadmap kembali.
2. Identifikasi dependency berikutnya yang benar-benar sudah unlocked oleh B-040.
3. Jangan memilih task hanya berdasarkan nomor terbesar.
4. Gunakan dependency order.
5. Jika B-041 sekarang sudah memiliki contract dan dependency lengkap, implementasikan B-041.
6. Jika B-041 masih membutuhkan contract/approval, audit dependency berikutnya.
7. Jangan mengimplementasikan task yang masih blocked.
8. Jangan membuat speculative architecture.

Jika beberapa task berturut-turut sudah benar-benar contract-backed dan dependency-nya lengkap, lanjutkan secara berurutan dalam sesi ini tanpa meminta prompt baru, SELAMA:

- scope jelas,
- contract tersedia,
- tidak membutuhkan human approval baru,
- tidak membutuhkan external infrastructure yang belum tersedia,
- tidak berisiko mengubah architecture yang belum disetujui.

Jika bertemu blocker baru yang membutuhkan approval manusia:

- berhenti pada blocker tersebut,
- jangan membuat workaround palsu,
- dokumentasikan blocker.

==================================================
BAGIAN 12 — GIT
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Review seluruh perubahan.

Pastikan tidak ada:

- secret,
- credential,
- temporary files,
- generated junk,
- unrelated refactor,
- perubahan Gorouter,
- provider changes yang tidak diperlukan.

Jika ada implementation valid:

buat SATU commit untuk scope yang selesai.

Gunakan commit message yang sesuai dengan perubahan aktual, misalnya:

`feat: implement telegram account connection`

Jangan membuat empty commit.

Setelah commit:

git push origin backend-dev-recovery

Kemudian verifikasi:

- local HEAD SHA
- origin/backend-dev-recovery SHA
- working tree clean

Pastikan:

LOCAL SHA == REMOTE SHA

Jika push gagal karena credential/network:

- jangan mengubah credential sembarangan,
- jangan menghapus commit,
- jangan reset --hard,
- simpan commit lokal,
- laporkan error secara jelas.

==================================================
BAGIAN 13 — DOCUMENTATION
==================================================

Jika implementation berhasil:

Update documentation yang memang menjadi source of truth:

- PROJECT_STATUS.md
- ROADMAP_V2.md
- CHANGELOG.md
- AI_CONTEXT.md
- AI_TASKS.md

Jangan membuat README baru.

Jangan membuat file dokumentasi duplikat.

Dokumentasikan:

- B-040 status,
- implementation status,
- validation status,
- remaining dependency,
- next roadmap task.

Jika documentation update sudah dilakukan oleh repository automation atau task sebelumnya, jangan membuat duplikasi.

==================================================
OUTPUT AKHIR
==================================================

Tampilkan laporan:

### B-040 Approval
- approval evidence:
- approval status:
- implementation allowed: YES/NO

### B-040 Implementation
- account model:
- authentication:
- credential/session boundary:
- connect:
- status:
- disconnect/revoke:
- API:
- persistence:
- runtime handoff:

### Security
- workspace isolation:
- credential handling:
- secret redaction:
- revoke behavior:

### Tests
- unit tests:
- integration tests:
- skipped tests:

### Validation
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

### Git
- commit SHA:
- push status:
- local SHA:
- remote SHA:
- working tree:

### Remaining Deferred
HANYA tampilkan blocker yang benar-benar masih membutuhkan:
- human approval,
- contract,
- infrastructure,
- external environment,
- deployment configuration.

### Next Roadmap
Tentukan berdasarkan dependency nyata repository.

PENTING:
- Jangan mengatakan selesai jika belum benar-benar diimplementasikan.
- Jangan mengarang approval.
- Jangan membuat fake implementation.
- Jangan membuat fake infrastructure.
- Jangan membuat fake credential.
- Jangan mengubah test agar PASS.
- Jangan membuat empty commit.
- Jangan menyentuh Gorouter.app.
- Jangan menyentuh NVIDIA/TokenHarbor tanpa alasan langsung.
- Jangan mengulang pekerjaan yang sudah selesai.
- Kerjakan sebanyak mungkin task yang benar-benar sudah unlocked.
- Jika tidak ada approval B-040, jangan coding speculative; laporkan blocker secara akurat.


```
# Prompt: B-040 Telegram Account Connection → Continue Full Roadmap
```
# Prompt: BotSpace — B-040 Telegram Account Connection + Continue Full Roadmap

Lanjutkan project BotSpace dari kondisi repository SAAT INI.

KERJA LANGSUNG DI:
`/root/botspace`

BRANCH:
`backend-dev-recovery`

==================================================
KONDISI TERAKHIR YANG SUDAH TERVERIFIKASI
==================================================

Repository saat ini sudah melalui beberapa tahap besar:

- B-030 Workspace API/Contract — DONE
- B-070 Storage Adapter — DONE
- B-071 File/Share Contract — DONE
- B-071 File/Share API — DONE
- B-071 Production Wiring — DONE
- SecretResolver application boundary — DONE
- Infrastructure/deferred verification — SUDAH DIAUDIT
- Security audit terakhir — PASS
- Validation utama — PASS
- Local SHA dan remote SHA sebelumnya sudah sinkron
- Working tree terakhir CLEAN
- Branch: `backend-dev-recovery`

Jangan mengulang pekerjaan yang sudah selesai.

Jangan membuat ulang:
- B-030
- B-070
- B-071 contract
- B-071 API
- B-071 production wiring
- SecretResolver boundary yang sudah ada

==================================================
BLOCKER TERAKHIR
==================================================

Roadmap audit terakhir menyatakan:

B-040 — Telegram account connection

masih BLOCKED karena:

- contract dan implementation Telegram account connection belum tersedia/approved,
- authentication mechanism belum mendapatkan approval,
- account/session model belum mendapatkan approval,
- credential/revoke policy belum mendapatkan approval,
- lifecycle state machine belum mendapatkan approval,
- disconnect/revoke semantics belum mendapatkan approval,
- versioned API/persistence contract belum mendapatkan approval,
- runtime handoff boundary belum mendapatkan approval.

ADR terkait:

`ADR-011`

Human approval diperlukan dari owner yang relevan sebelum implementasi production B-040.

PENTING:

JANGAN MEMBUAT APPROVAL PALSU.

JANGAN MENGANGGAP APPROVAL ADA HANYA KARENA DOKUMEN ADA.

JANGAN MEMILIH ARCHITECTURE TELEGRAM SENDIRI JIKA CONTRACT BELUM DISETUJUI.

==================================================
TUJUAN UTAMA
==================================================

Kerjakan roadmap BotSpace sejauh mungkin secara aman.

Urutan dependency yang wajib dihormati:

1. B-040 Telegram account connection
2. B-041 connection health/state machine
3. B-050/B-051/B-052 bot/provider/runtime dependency
4. B-090 queue/job infrastructure
5. B-091 worker runtime
6. B-092 scheduler
7. F-090 job monitoring/replay
8. B-100/F-100 operator/admin
9. B-110/B-111 billing/entitlement
10. B-130/B-131 abuse/security
11. B-140/B-141 telemetry/SLO/alerting
12. B-150/B-151/F-150 release/staging/backup/rollback/production readiness
13. F-080 AI
14. F-120 marketplace
15. F-070 File/Share UI
16. remaining deferred public-share infrastructure

JANGAN melompati dependency.

JANGAN membuat implementation speculative hanya untuk mengubah status roadmap menjadi DONE.

==================================================
PHASE 1 — AUDIT B-040
==================================================

Mulai dengan audit lengkap.

Cari dan baca:

- roadmap B-040,
- ADR-011,
- AI_CONTEXT.md,
- AI_TASKS.md,
- PROJECT_STATUS.md,
- ROADMAP_V2.md,
- CHANGELOG.md,
- docs/architecture/,
- existing account/user/workspace models,
- existing authentication abstraction,
- existing provider abstraction,
- existing runtime abstraction,
- existing persistence abstraction,
- existing API client,
- existing Telegram-related code,
- BotInstallation model/status,
- configuration system,
- SecretResolver,
- session/credential handling,
- existing test suite.

Jangan hanya membaca nama file.

Telusuri dependency dan implementasi aktual.

Buat kesimpulan:

A. Apa yang sudah tersedia untuk B-040?
B. Apa yang masih benar-benar missing?
C. Apa yang membutuhkan approval?
D. Apa yang sebenarnya sudah contract-backed?
E. Apa yang dapat diimplementasikan tanpa keputusan architecture baru?

==================================================
PHASE 2 — VALIDASI APPROVAL B-040
==================================================

Cari evidence approval B-040/ADR-011 di repository.

Evidence harus berupa sesuatu yang benar-benar eksplisit, misalnya:

- approval record,
- approved ADR,
- decision document,
- owner approval,
- status resmi yang menunjukkan APPROVED,
- atau mekanisme approval resmi yang memang digunakan repository.

Jangan menganggap:

- commit documentation biasa,
- audit result,
- roadmap note,
- AI-generated statement,
- "ready",
- "planned",
- "proposed"

sebagai approval.

JIKA APPROVAL BELUM ADA:

JANGAN IMPLEMENTASIKAN B-040.

Sebaliknya:

1. Audit seluruh dependency B-040.
2. Pastikan approval package/ADR-011 lengkap.
3. Identifikasi secara jelas keputusan yang harus dibuat manusia.
4. Rapikan documentation bila memang diperlukan.
5. Pastikan tidak ada code implementation speculative.
6. Jalankan validation yang aman.
7. Jangan membuat empty commit.
8. Jangan mengubah status B-040 menjadi DONE.
9. Jangan lanjut B-041 karena B-041 bergantung pada B-040.

Kemudian tampilkan:

`BLOCKED — HUMAN APPROVAL REQUIRED`

dan daftar keputusan yang masih harus disetujui.

JIKA APPROVAL B-040 BENAR-BENAR ADA:

LANJUTKAN PHASE 3.

==================================================
PHASE 3 — IMPLEMENT B-040
==================================================

Jika dan hanya jika approval benar-benar tersedia:

Implementasikan B-040 sesuai ADR-011 yang telah disetujui.

Jangan menambahkan architecture yang tidak ada di approval.

Minimal audit/implementasi harus mencakup:

1. Telegram account identity
2. account/session model
3. authentication mechanism
4. credential boundary
5. session lifecycle
6. connect flow
7. disconnect flow
8. revoke flow
9. reconnect behavior
10. account ownership
11. workspace association
12. authorization
13. credential storage
14. SecretResolver integration
15. state transitions
16. API contract
17. persistence contract
18. runtime handoff boundary
19. error handling
20. security handling

Pastikan:

- credential tidak disimpan plaintext jika architecture tidak mengizinkannya,
- credential tidak masuk log,
- credential tidak masuk HTTP response,
- session secret tidak masuk error,
- account hanya dapat digunakan oleh owner/workspace yang berwenang,
- cross-workspace account access ditolak,
- revoke benar-benar mencabut penggunaan credential/session,
- disconnect tidak menghapus data yang tidak seharusnya dihapus,
- reconnect mengikuti lifecycle yang telah disetujui.

Jangan menggunakan Telegram polling/webhook runtime sebagai shortcut jika ADR tidak memintanya.

Jangan mengubah:

`BotInstallation.status`

menjadi process/runtime state.

Pisahkan lifecycle state dari runtime process state.

==================================================
PHASE 4 — TEST B-040
==================================================

Tambahkan test nyata untuk behavior yang diimplementasikan.

Minimal:

- valid Telegram account connection
- invalid authentication
- duplicate account handling
- workspace ownership
- cross-workspace rejection
- session creation
- session lifecycle
- disconnect
- revoke
- reconnect
- credential resolution
- missing secret
- resolver failure
- sanitized errors
- no credential leakage
- persistence behavior
- API response behavior
- state transition correctness

Jangan membuat fake behavior hanya agar test PASS.

Gunakan mock/fake hanya jika memang sesuai architecture testing repository.

Jangan membuat test yang mengklaim Telegram connection berhasil jika tidak ada real integration environment.

Jika real Telegram integration environment tidak tersedia:

- unit/integration boundary test tetap dijalankan,
- real external Telegram verification ditandai unavailable,
- jangan mengubah unavailable menjadi PASS.

==================================================
PHASE 5 — B-041
==================================================

Setelah B-040 benar-benar selesai dan validation PASS:

Audit B-041.

B-041 adalah:

Telegram account connection health/state machine.

Jangan implementasikan B-041 jika B-040 belum stabil.

Implementasikan hanya berdasarkan contract yang sudah tersedia atau dependency yang benar-benar berasal dari B-041.

State machine harus deterministic.

Jangan mencampur:

- account lifecycle,
- connection state,
- runtime process state,
- bot installation lifecycle.

Pastikan state transition memiliki:

- valid initial state,
- valid connect transition,
- authenticated state,
- degraded/error state jika contract mendukung,
- disconnected state,
- revoked state jika contract mendukung,
- reconnect behavior,
- invalid transition rejection.

Tambahkan test untuk seluruh transition.

==================================================
PHASE 6 — B-050/B-051/B-052
==================================================

Setelah B-041 selesai:

Audit dependency:

- B-050
- B-051
- B-052

Roadmap sebelumnya menunjukkan dependency:

`B-050/B-051/B-052`

berhubungan dengan bot/provider/runtime.

Jangan implementasikan semuanya sekaligus tanpa audit.

Untuk masing-masing:

1. baca roadmap,
2. baca contract,
3. identifikasi dependency,
4. implementasikan hanya jika contract tersedia,
5. jangan membuat provider/runtime behavior speculative.

Pastikan account connection dapat diserahkan ke runtime melalui boundary yang jelas.

Jangan menjalankan Telegram polling/webhook hanya karena ingin membuat feature terlihat selesai.

==================================================
PHASE 7 — QUEUE / JOB INFRASTRUCTURE
==================================================

Setelah B-050/B-051/B-052 dependency selesai:

Audit B-090.

B-090 sebelumnya BLOCKED karena:

- JobEnvelope belum tersedia,
- queue adapter belum tersedia,
- retry policy belum tersedia,
- DLQ behavior belum tersedia,
- replay semantics belum tersedia,
- execution semantics belum tersedia,
- persistence belum tersedia.

Jika contract masih belum tersedia:

JANGAN membuat queue system speculative.

Jika contract sudah tersedia:

implementasikan:

- JobEnvelope
- queue abstraction
- queue adapter
- retry policy
- dead-letter queue behavior
- replay behavior
- deterministic execution semantics
- persistence
- idempotency bila contract mendukungnya.

Jangan memilih vendor queue secara sepihak jika architecture belum menentukan.

==================================================
PHASE 8 — B-091 WORKER
==================================================

Setelah B-090 selesai:

Implementasikan B-091 hanya berdasarkan queue/job contracts.

Worker harus:

- menerima JobEnvelope,
- menjalankan job,
- menangani retry,
- menangani failure,
- mendukung DLQ,
- memiliki deterministic behavior,
- tidak mencampur scheduler logic,
- tidak mencampur billing logic.

Tambahkan test worker lifecycle dan failure handling.

==================================================
PHASE 9 — B-092 SCHEDULER
==================================================

Setelah B-090 tersedia:

Implementasikan B-092.

Scheduler harus:

- membuat job berdasarkan contract,
- memiliki deterministic scheduling behavior,
- tidak membuat queue abstraction kedua,
- tidak menjalankan job langsung jika architecture memerlukan queue,
- menghormati retry/job semantics.

Tambahkan test.

==================================================
PHASE 10 — F-090 JOB MONITORING
==================================================

Setelah B-090/B-091/B-092 tersedia:

Implementasikan F-090:

- job monitoring,
- job status,
- replay API,
- failure inspection,

hanya sesuai contract.

Jangan membuat operator/admin API sebelum B-100 jika B-100 memang dependency-nya.

==================================================
PHASE 11 — B-100/F-100 OPERATOR
==================================================

Audit operator/admin contract.

Implementasikan:

- operator identity,
- authorization,
- admin API,
- required permissions,

hanya berdasarkan contract.

Pastikan normal user tidak mendapatkan operator privileges.

==================================================
PHASE 12 — B-110/B-111 BILLING
==================================================

Audit entitlement dan billing contract.

Jangan membuat payment system speculative.

Implementasikan hanya jika:

- entitlement model tersedia,
- billing provider contract tersedia,
- authorization boundary tersedia.

Pisahkan:

- billing state,
- entitlement,
- account state,
- runtime state.

==================================================
PHASE 13 — B-130/B-131 SECURITY / ABUSE
==================================================

Audit:

- abuse control,
- webhook validation,
- security settings.

Jangan membuat security architecture baru jika contract belum tersedia.

Implementasikan approved boundary saja.

Pastikan webhook validation tidak menerima request tanpa verification jika contract mensyaratkan signature/authentication.

==================================================
PHASE 14 — B-140/B-141 OBSERVABILITY
==================================================

Implementasikan hanya jika contract tersedia:

- telemetry provider,
- SLO,
- alert,
- runbook.

Jangan membuat fake telemetry.

Jangan memasukkan credential/token ke telemetry.

==================================================
PHASE 15 — B-150/B-151/F-150 RELEASE
==================================================

Setelah application/runtime dependencies selesai:

Audit:

- release,
- staging,
- backup/restore,
- rollback,
- production approval.

Jangan menyatakan production-ready hanya karena build PASS.

Production readiness harus berdasarkan evidence nyata.

==================================================
PHASE 16 — DEFERRED ITEMS
==================================================

Tetap hormati deferred items sebelumnya.

PUBLIC SHARE RATE LIMITING:

Jika approved policy/middleware boundary belum tersedia:

`DEFERRED`

Jangan memilih angka limit sendiri.

PUBLIC SHARE AUDIT EVENT:

Jika approved event/service/repository boundary belum tersedia:

`DEFERRED`

SHARE EXPIRY:

Tetap:

`DEFERRED`

Jangan menambahkan:

- expiresAt,
- expiry column,
- expiry migration,
- cleanup scheduler,

tanpa contract/schema approval.

POSTGRESQL:

Jika:

`PERSISTENCE_TEST_DATABASE_URL`

tersedia, jalankan integration test yang memang ada.

Jika tidak:

`SKIPPED — PERSISTENCE_TEST_DATABASE_URL unavailable`

MINIO/S3:

Jika environment tersedia, jalankan smoke test.

Jika tidak:

`SKIPPED — MinIO/S3 test environment unavailable`

Jangan membuat environment palsu hanya agar test PASS.

==================================================
PHASE 17 — SECURITY AUDIT
==================================================

Setelah implementation batch selesai lakukan security audit.

Cari:

- hardcoded credential,
- token leakage,
- secret leakage,
- unsafe logging,
- unsafe error messages,
- cross-workspace access,
- path traversal,
- object storage key leakage,
- unauthorized Telegram account access,
- session leakage,
- revoke bypass,
- invalid state transition,
- insecure webhook handling,
- unsafe admin authorization.

Jalankan repository security checks yang tersedia.

Jangan mengubah behavior yang benar tanpa alasan.

==================================================
PHASE 18 — VALIDATION
==================================================

Setelah setiap implementation batch:

jalankan validation yang tersedia.

Minimal:

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

JANGAN membuat file tersebut jika memang tidak tersedia.

Catat:

`SKIPPED — scripts/check-symlinks.mjs unavailable`

Jangan menyamarkan skipped sebagai PASS.

==================================================
PHASE 19 — GIT DISCIPLINE
==================================================

Sebelum setiap commit:

git status
git diff --stat
git diff --check

Review seluruh perubahan.

Hapus:

- temporary files,
- generated junk,
- debug code,
- credentials,
- secrets,
- unrelated changes.

Jangan mengubah:

- Gorouter.app,
- integration test Gorouter.app.

NVIDIA dan TokenHarbor hanya boleh tersentuh jika perubahan benar-benar membutuhkan.

Jangan melakukan refactor besar yang tidak diperlukan.

==================================================
COMMIT POLICY
==================================================

Jangan membuat empty commit.

Jika satu logical phase selesai dan validation PASS:

buat SATU commit untuk phase tersebut.

Contoh:

`feat: implement telegram account connection`

kemudian:

`git push origin backend-dev-recovery`

Verifikasi:

- local HEAD SHA,
- remote SHA,
- working tree clean.

Jika push gagal:

- jangan menghapus commit,
- jangan reset,
- jangan mengubah credential sembarangan,
- laporkan error push.

==================================================
ATURAN PALING PENTING
==================================================

1. Jangan mengarang approval.
2. Jangan mengarang contract.
3. Jangan mengarang schema.
4. Jangan membuat fake infrastructure.
5. Jangan membuat test palsu.
6. Jangan mengubah test supaya PASS.
7. Jangan mengubah BotInstallation.status menjadi process state.
8. Jangan menjalankan Gorouter.app integration test.
9. Jangan menyentuh Gorouter.app.
10. NVIDIA dan TokenHarbor tidak perlu disentuh kecuali benar-benar diperlukan.
11. Jangan membuat Telegram runtime/polling/webhook speculative.
12. Jangan membuat queue vendor-specific tanpa architecture approval.
13. Jangan membuat billing provider speculative.
14. Jangan membuat AI/marketplace feature sebelum dependency-nya siap.
15. Jangan implementasikan share expiry tanpa approved contract/schema.
16. Jangan implementasikan rate limit tanpa approved policy boundary.
17. Jangan implementasikan audit event tanpa approved event boundary.
18. Jangan berhenti pada audit jika implementation memang sudah contract-backed.
19. Jika blocked oleh human approval, berhenti tepat pada blocker tersebut.
20. Setelah blocker terselesaikan, lanjutkan dependency berikutnya secara otomatis.
21. Kerjakan sebanyak mungkin dalam satu run tanpa menunggu instruksi baru, tetapi selalu hormati dependency order.
22. Jangan mengulang task yang sudah DONE.

==================================================
OUTPUT AKHIR
==================================================

Setelah run selesai, tampilkan laporan:

### Current Phase
- task:
- status:
- reason:

### B-040
- approval:
- implementation:
- tests:
- status:

### B-041
- implementation:
- tests:
- status:

### B-050/B-051/B-052
- status masing-masing:
- blocker:

### Queue / Worker / Scheduler
- B-090:
- B-091:
- B-092:
- F-090:

### Operator / Billing / Security
- B-100/F-100:
- B-110/B-111:
- B-130/B-131:

### Observability / Release
- B-140/B-141:
- B-150/B-151/F-150:

### Deferred
Hanya tampilkan dependency yang benar-benar masih blocked.

### Validation
- pnpm test:
- build:
- typecheck:
- lint:
- format:
- imports:
- ownership:
- docs:
- diff:
- symlink:

### Git
- branch:
- commit SHA:
- remote SHA:
- push:
- working tree:

### NEXT SINGLE ACTION

Tentukan SATU task berikutnya berdasarkan dependency nyata.

Jangan memberikan daftar task acak.

Jika B-040 masih menunggu approval:

`NEXT SINGLE ACTION: Obtain human approval for B-040/ADR-011`

Jika B-040 approved dan selesai:

tentukan B-041.

Jika B-041 selesai:

tentukan B-050/B-051/B-052 sesuai dependency aktual.

Teruskan sampai dependency berikutnya benar-benar blocked.

==================================================

JANGAN hanya memberikan rekomendasi.

KERJAKAN LANGSUNG semua implementation yang contract-backed dan aman.

Jika blocked, jangan memaksakan architecture.

Mulai sekarang di:

`/root/botspace`


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
