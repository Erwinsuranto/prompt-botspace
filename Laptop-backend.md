






# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# Prompt: BotSpace — Final Production Readiness Verification
```
PROMPT: BotSpace — Final Production Readiness Verification

Kita melanjutkan project BotSpace setelah tahap Bot Lifecycle & Resource Integrity.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Checkpoint terbaru:
 d24aeed5d2151484449d94c72609e6f26b332d9c

Commit:
 docs: finalize product verification guidance

Kondisi verification terakhir:

- Domain: 107 passed
- API: 113 passed
- Full repository tests: 11 packages passed
- pnpm check: 44/44 passed
- Typecheck: 11/11 passed
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 passed
- Working tree: CLEAN

Database migration:
- BLOCKED
- Penyebab: environment tidak memiliki Docker
- Error: `/bin/sh: 1: docker: not found`

PENTING:
Database migration BLOCKED karena Docker tidak tersedia di environment.
JANGAN mengubah source code hanya untuk mengakali blocker Docker.
JANGAN membuat fake migration result.
JANGAN menghapus migration test.
JANGAN mengganti migration behavior hanya agar verification terlihat PASS.

Jangan reset.
Jangan force push.
Jangan rebase sembarangan.
Jangan checkout branch lain.
Jangan merge ke backend-dev.
Jangan membuat authentication/authorization system baru.
Jangan menggunakan Kiro.

==================================================
TUJUAN
==================================================

Ini adalah FINAL PRODUCTION READINESS VERIFICATION.

Tujuan:

AUDIT FINAL
→ SECURITY REGRESSION
→ TEST
→ TYPECHECK
→ BUILD
→ SECRET SCAN
→ GIT AUDIT
→ PUSH
→ FINAL REPORT

Jangan menambahkan fitur besar baru.

==================================================
1. AUDIT FINAL SOURCE CODE
==================================================

Audit perubahan dari checkpoint sebelumnya.

Pastikan perubahan hanya berkaitan dengan:

- authentication
- session
- workspace authorization
- workspace membership
- ownership
- permission
- bot authorization
- bot lifecycle
- resource integrity
- credential security
- documentation/verification

Cari kembali:

- TODO security
- FIXME security
- debug code
- console.log sensitif
- hardcoded secret
- token
- password
- API key
- credential
- @ts-ignore baru
- any baru yang tidak diperlukan
- dead code
- duplicate authorization system

Jangan melakukan refactor besar jika tidak ada bug nyata.

==================================================
2. SECURITY REGRESSION
==================================================

Pastikan seluruh security boundary tetap aktif:

Authentication
→ Current User
→ Account
→ Workspace
→ Membership
→ Role/Permission
→ Bot
→ Child Resource

Pastikan tidak ada jalur yang dapat melewati:

- authentication
- workspace authorization
- membership
- permission
- ownership

Audit kembali kemungkinan IDOR:

- workspaceId
- botId
- membershipId
- commandId
- flowId
- integrationId
- webhookId
- credentialId
- resource ID lainnya

User dari workspace A tidak boleh mengakses resource workspace B hanya dengan mengetahui ID.

==================================================
3. CREDENTIAL SECURITY
==================================================

Pastikan tidak ada:

- password
- bot token
- API key
- session token
- refresh token
- webhook secret
- integration secret

yang masuk ke:

- response
- logs
- errors
- test output
- git diff
- repository

Jalankan secrets scan yang tersedia.

Jangan menampilkan secret pada final report.

==================================================
4. TEST FINAL
==================================================

Jalankan verification resmi repository.

Minimal:

- Domain tests
- API tests
- Authentication/session tests
- Workspace authorization tests
- Membership tests
- Bot/resource tests
- Typecheck
- Format
- Import boundary
- Secrets scan
- Build

Jika command repository memiliki full verification command, gunakan command tersebut.

JANGAN skip test.

JANGAN menghapus test.

Jika test gagal:

- identifikasi root cause
- perbaiki hanya jika failure berasal dari source code
- jalankan ulang test
- ulangi full verification

==================================================
5. DATABASE MIGRATION
==================================================

Jalankan migration verification HANYA jika environment menyediakan Docker.

Pertama cek:

docker --version

Jika Docker tersedia:

- jalankan migration test resmi repository
- pastikan migration PASS

Jika Docker tidak tersedia:

JANGAN install Docker.
JANGAN mengubah source code.
JANGAN membuat workaround.
JANGAN mengklaim migration PASS.

Catat secara eksplisit:

Database migration:
BLOCKED — Docker unavailable

Source-code verification tetap dianggap valid jika seluruh verification lain PASS.

==================================================
6. BUILD FINAL
==================================================

Jalankan full build.

Pastikan:

- semua package berhasil build
- tidak ada TypeScript error
- tidak ada syntax error
- tidak ada import boundary violation
- tidak ada missing dependency

Expected:

Build: PASS

==================================================
7. GIT AUDIT
==================================================

Jalankan:

git status
git diff --stat
git diff
git log --oneline -5
git branch --show-current
git remote -v

Pastikan:

- branch = backend-dev-recovery
- working tree clean
- tidak ada secret
- tidak ada temporary file
- tidak ada build artifact
- tidak ada perubahan tidak sengaja

JANGAN mengubah remote.

==================================================
8. COMMIT
==================================================

Jika source code sudah clean dan tidak ada perubahan baru:

JANGAN membuat empty commit.

Pertahankan checkpoint:

d24aeed5d2151484449d94c72609e6f26b332d9c

Jika ternyata ada perubahan source code kecil yang memang diperlukan dari verification final:

- review diff
- test ulang
- buat SATU commit
- gunakan message sesuai perubahan sebenarnya

Jangan membuat commit hanya untuk membuat aktivitas terlihat.

==================================================
9. PUSH
==================================================

Pastikan checkpoint terbaru sudah berada di remote.

Jalankan:

git fetch origin
git status
git push

Jika sudah up-to-date:

jangan membuat commit kosong.

Jika push gagal karena GitHub authentication:

JANGAN mengubah source code.

Laporkan error sebenarnya.

Jangan force push.

==================================================
10. FINAL DECISION
==================================================

Tentukan status berdasarkan fakta.

READY FOR PRODUCTION:
jika:

- security regression PASS
- tests PASS
- typecheck PASS
- format PASS
- import boundary PASS
- secrets scan PASS
- build PASS
- working tree CLEAN
- checkpoint aman
- push berhasil atau remote sudah up-to-date

Database migration boleh tetap:

BLOCKED — Docker unavailable

selama blocker tersebut hanya environment limitation dan bukan source-code failure.

NOT READY:
jika ada source-code/test/build/security failure.

Jangan menyatakan READY jika ada source-code failure.

==================================================
11. FINAL REPORT
==================================================

Tampilkan laporan singkat:

FINAL DECISION:
- READY / NOT READY

Source Code:
- Audit: PASS/FAIL
- Security regression: PASS/FAIL
- Credential security: PASS/FAIL

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Secrets scan: ...
- Build: ...

Database:
- Migration: PASS / BLOCKED
- Reason jika BLOCKED: Docker unavailable

Git:
- Branch: ...
- HEAD: ...
- Working tree: CLEAN/DIRTY
- Remote: ...
- Push: SUCCESS / UP-TO-DATE / FAILED

Final:
- Production readiness: ...

Jika migration masih BLOCKED karena Docker tidak tersedia, tulis dengan jelas bahwa itu adalah ENVIRONMENT BLOCKER, bukan source-code failure.

Jangan mengklaim migration berhasil jika Docker tidak tersedia.

==================================================
PENTING
==================================================

Ini adalah tahap final.

Jangan menambahkan fitur baru.
Jangan refactor besar.
Jangan membuat sistem security baru.
Jangan mengubah database migration hanya karena Docker tidak tersedia.

Fokus:

FINAL AUDIT
→ SECURITY REGRESSION
→ TEST
→ BUILD
→ GIT
→ PUSH
→ FINAL DECISION

Setelah final report selesai, berhenti.


```
# Prompt berikutnya — Bot Lifecycle & Resource Integrity
```

PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace setelah checkpoint security terakhir yang SUDAH BERHASIL DIPUSH.

Repository: /root/botspace
Branch: backend-dev-recovery

Kondisi:
- checkpoint security terakhir sudah berhasil dipush
- working tree harus dipertahankan clean
- jangan reset
- jangan force push
- jangan rebase sembarangan
- jangan merge ke backend-dev
- jangan mengubah remote
- jangan membuat authentication/authorization system kedua
- jangan menggunakan Kiro

TUJUAN

Lanjutkan sampai tahap berikutnya dengan fokus pada:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ BOT AUTHORIZATION
→ BOT LIFECYCLE
→ RESOURCE INTEGRITY
→ STATE TRANSITION
→ DATABASE CONSISTENCY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

1. AUDIT DAHULU

Sebelum mengubah kode, audit repository aktual.

Cari seluruh implementasi:

- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot
- bot status
- bot configuration
- bot credentials
- bot settings
- bot commands
- bot flows
- bot integrations
- webhook
- seluruh resource yang memiliki botId

Pahami hubungan:

User
→ Account
→ Workspace
→ Bot
→ Child Resources

Jangan membuat endpoint baru jika belum diperlukan.

2. BOT STATE

Identifikasi state bot yang benar-benar sudah digunakan.

Jangan membuat state baru jika tidak ada di architecture.

Audit seluruh state transition:

- enable
- disable
- activate
- deactivate
- start
- stop
- delete

Pastikan authorization diperiksa SEBELUM mutation.

Jika bot sudah berada pada state yang tidak memungkinkan operasi tertentu, ikuti behavior yang sudah digunakan repository.

3. BOT CREATION

Pastikan:

- user sudah authenticated
- workspace valid
- user memiliki akses workspace
- workspaceId tidak dapat dipalsukan
- ownerId tidak dapat dipalsukan
- accountId tidak dapat dipalsukan
- ownership ditentukan server
- relasi bot → workspace benar

Request tidak boleh membuat bot di workspace milik user lain hanya dengan mengirim workspaceId yang valid.

4. BOT UPDATE

Audit seluruh field yang dapat diubah.

Pisahkan field:

CLIENT-CONTROLLED
dan
SERVER-CONTROLLED

Periksa khusus:

- workspaceId
- ownerId
- accountId
- createdBy
- createdAt
- updatedAt
- status
- role
- permissions
- credential identifiers

Update biasa tidak boleh digunakan untuk:

- mengganti workspace
- mengganti owner
- mengganti account
- menaikkan permission

kecuali architecture memang secara eksplisit mendukung operasi tersebut.

5. BOT DELETE

Pastikan:

- authorization dilakukan sebelum delete
- cross-workspace delete ditolak
- member tanpa permission delete ditolak
- nonexistent bot mengikuti error convention
- child resource tidak menjadi orphan secara tidak sengaja

Pertahankan soft-delete/hard-delete sesuai implementasi existing.

Jangan mengubah model deletion tanpa kebutuhan nyata.

6. BOT ENABLE / DISABLE

Audit seluruh endpoint/service status.

Pastikan:

authorized user
→ allowed

unauthorized member
→ denied

cross-workspace user
→ denied

unauthenticated
→ denied

Authorization harus dilakukan sebelum perubahan status.

7. CHILD RESOURCE INTEGRITY

Audit seluruh resource turunan bot yang memang tersedia, misalnya:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- statistics
- analytics
- credentials
- configuration

Pastikan user yang tidak memiliki akses bot tidak dapat mengakses child resource hanya dengan mengetahui child ID.

Jangan membuat fitur baru.

8. WORKSPACE RELATION INTEGRITY

Audit kemungkinan relasi invalid:

- bot.workspaceId berbeda dengan workspace yang seharusnya
- bot.ownerId tidak sesuai
- bot.accountId tidak sesuai
- botId tidak valid
- child resource menunjuk bot yang salah
- child resource menunjuk workspace yang salah

Fokus pada pencegahan melalui backend/service/repository.

Jangan memperbaiki data production secara otomatis.

9. IDOR AUDIT

Cari pola:

findById(id)
findUnique({ id })
where: { id }

Untuk setiap resource workspace/bot:

pastikan authorization tetap dilakukan.

Jika repository abstraction mendukung workspace-scoped query, gunakan abstraction tersebut.

Jangan melakukan perubahan query secara membabi buta.

10. CREDENTIAL SECURITY

Audit:

- bot token
- Telegram token
- webhook secret
- API key
- integration secret
- access token
- refresh token

Pastikan secret tidak:

- muncul pada list bot
- bocor pada response yang tidak diperlukan
- masuk log
- masuk error
- masuk analytics
- masuk audit log plaintext
- digunakan sebagai dasar ownership

Jangan menampilkan secret dalam test output.

11. MASS ASSIGNMENT

Cari request body yang memungkinkan field privilege ikut diubah.

Audit minimal:

- workspaceId
- ownerId
- userId
- accountId
- permissions
- role
- createdBy
- status

Hanya proses field yang memang diizinkan endpoint.

12. INPUT VALIDATION

Gunakan validation system yang sudah ada.

Audit:

- botId
- workspaceId
- status
- configuration
- settings
- commandId
- flowId
- integrationId
- webhookId

Jangan membuat validation framework baru.

13. ERROR HANDLING

Gunakan error system existing.

Pastikan:

unauthenticated
→ authentication error

authenticated tetapi tidak punya akses
→ authorization error

resource tidak ada
→ not found

invalid state/input
→ domain/validation error sesuai convention

Jangan membocorkan detail resource workspace lain.

14. TEST MATRIX

Tambahkan atau perbaiki test sesuai resource yang benar-benar ada.

CREATE:
- authenticated + valid workspace = PASS
- unauthenticated = DENY
- wrong workspace = DENY
- spoofed ownerId = DENY
- spoofed accountId = DENY

READ:
- own bot = PASS
- other workspace bot = DENY

UPDATE:
- authorized update = PASS
- unauthorized update = DENY
- workspaceId spoof = DENY
- ownerId spoof = DENY
- permission spoof = DENY

DELETE:
- authorized delete = PASS
- unauthorized delete = DENY
- cross-workspace delete = DENY

STATUS:
- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY
- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY

CHILD RESOURCE:
- authorized access = PASS
- cross-workspace access = DENY
- invalid parent relation = DENY

CREDENTIAL:
- secret tidak muncul pada response yang tidak seharusnya
- secret tidak muncul pada error
- secret tidak muncul pada log/test output

15. REGRESSION

Pastikan security checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization

Jangan melemahkan test existing.

16. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate bot lifecycle logic
- tidak ada circular dependency baru
- tidak ada hardcoded secret

17. README

Jika memang diperlukan, update README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan singkat:

- bot lifecycle
- authorization
- resource integrity
- credential handling
- test command

18. VERIFICATION

Jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika gagal:

1. cari root cause
2. perbaiki
3. ulangi test terkait
4. ulangi full verification

Jangan skip test.
Jangan menghapus test existing.

19. GIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary files
- build artifacts

Jika verification PASS:

buat SATU commit baru dengan message sesuai perubahan sebenarnya.

Contoh:

fix: harden bot lifecycle integrity

Setelah commit:

git status
git log --oneline -3

Kemudian:

git push

Branch tetap:

backend-dev-recovery

Jangan force push.
Jangan merge.
Jangan mengubah remote.

20. HASIL AKHIR

Laporkan:

Implementation:
- ...

Bot Lifecycle:
- ...

Resource Integrity:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum berhasil.

21. PENTING

Jangan membuat fitur besar baru.

Fokus hanya:

AUDIT
→ BOT LIFECYCLE
→ STATE INTEGRITY
→ OWNERSHIP INTEGRITY
→ WORKSPACE RELATION
→ CHILD RESOURCE INTEGRITY
→ CREDENTIAL SECURITY
→ IDOR TEST
→ REGRESSION
→ BUILD
→ COMMIT
→ PUSH

Setelah push berhasil, berhenti dan laporkan hasil final.

```
# Prompt: Final Git Push Recovery
```

PROMPT: BotSpace — Final Git Push Recovery

Project:
 /root/botspace

Branch:
 backend-dev-recovery

Kondisi saat ini:
- Source code verification: READY
- Working tree: CLEAN
- HEAD: d24aeed
- Commit: docs: finalize production verification guidance
- HEAD berada 1 commit di depan upstream
- Commit sudah tersimpan lokal
- Push sebelumnya GAGAL karena GitHub authentication:
  fatal: could not read Username for 'https://github.com': No such device or address

TUJUAN:
Selesaikan hanya proses push commit terakhir ke GitHub.

ATURAN SANGAT PENTING:

1. JANGAN mengubah source code.
2. JANGAN membuat commit baru.
3. JANGAN membuat empty commit.
4. JANGAN reset.
5. JANGAN force push.
6. JANGAN rebase.
7. JANGAN merge.
8. JANGAN mengubah remote.
9. JANGAN mengubah credential/token yang sudah tersimpan.
10. JANGAN meminta atau menampilkan secret/token.
11. Jangan melakukan perubahan apa pun selain yang diperlukan untuk retry push.

Periksa:

git status
git log --oneline -3
git remote -v
git branch -vv

Pastikan:
- branch tetap backend-dev-recovery
- HEAD tetap d24aeed
- working tree tetap clean

Kemudian coba:

git push

Jika push berhasil:

verifikasi:

git status
git log --oneline -3
git branch -vv

Pastikan HEAD dan origin/backend-dev-recovery sudah sinkron.

Jika push gagal lagi karena GitHub authentication:

JANGAN mengubah commit.
JANGAN membuat commit baru.
JANGAN force push.
JANGAN mengubah source code.

Laporkan error GitHub authentication sebenarnya.

FINAL REPORT:

Git:
- Branch: ...
- HEAD: ...
- Commit: d24aeed
- Push: SUCCESS / FAILED
- Upstream: ...
- Working tree: CLEAN

FINAL DECISION:
Jika push berhasil:
READY — FINAL

Jika push gagal:
READY LOCALLY — PUSH BLOCKED BY GITHUB AUTHENTICATION

Setelah laporan akhir, berhenti.

```

# Prompt: BotSpace — Final Production Readiness & Verification
```

PROMPT: BotSpace — Final Production Readiness & Final Verification

Kita melanjutkan project BotSpace dari checkpoint terakhir yang SUDAH BERHASIL.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Checkpoint terakhir:
 ab4df16 — fix: harden bot credential reference integrity

Status checkpoint:
- Working tree: CLEAN
- HEAD dan origin/backend-dev-recovery: SINKRON
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful

Database Migration:
- STATUS: BLOCKED
- Reason: Docker tidak tersedia di environment ini
- Error: /bin/sh: 1: docker: not found

PENTING:
JANGAN install Docker hanya untuk verification ini.
JANGAN mengubah source code hanya untuk menghilangkan blocker Docker.
JANGAN membuat migration palsu.
JANGAN mengklaim database migration PASS.
Catat migration sebagai BLOCKED BY ENVIRONMENT jika masih tidak dapat dijalankan.

Git:
- branch: backend-dev-recovery
- remote sudah sinkron
- jangan reset
- jangan force push
- jangan rebase sembarangan
- jangan checkout branch lain
- jangan merge ke backend-dev

==================================================
TUJUAN FINAL
==================================================

Ini adalah tahap FINAL verification BotSpace.

Jangan membuat fitur besar baru.

Tujuan:

AUDIT FINAL
→ RUNTIME/CONFIGURATION SAFETY
→ SECURITY REGRESSION
→ API CONTRACT
→ TEST
→ TYPECHECK
→ FORMAT
→ BUILD
→ GIT AUDIT
→ COMMIT HANYA JIKA ADA PERBAIKAN NYATA
→ PUSH
→ FINAL REPORT

Setelah tahap ini selesai dan semua verification yang tersedia PASS, berhenti.

==================================================
1. FINAL REPOSITORY AUDIT
==================================================

Baca struktur repository aktual.

Audit:

- packages/domain
- services/api
- infrastructure
- database
- bot/resource modules
- configuration
- scripts
- tests
- README.md

Cari TODO/FIXME yang berkaitan dengan:

- authentication
- authorization
- workspace isolation
- membership
- ownership
- bot lifecycle
- credential
- secret leakage
- resource access
- database consistency

Jangan memperbaiki TODO yang tidak relevan.

Jangan membuat fitur baru.

==================================================
2. SECURITY REGRESSION
==================================================

Pastikan checkpoint sebelumnya tetap aman.

Verifikasi kembali:

Authentication
→ Session
→ Current User
→ Workspace Authorization
→ Membership
→ Ownership
→ Permission
→ Bot Authorization
→ Bot Lifecycle
→ Child Resource Integrity
→ Credential Security

Pastikan tidak ada bypass melalui:

- userId
- accountId
- workspaceId
- botId
- ownerId
- membershipId
- role
- permission
- status

yang berasal langsung dari request.

Authenticated identity harus tetap berasal dari auth/session context.

==================================================
3. API CONTRACT AUDIT
==================================================

Audit protected API yang sudah tersedia.

Pastikan:

- authentication tetap diwajibkan
- workspace isolation tetap berlaku
- permission tetap berlaku
- input validation tetap aktif
- response tidak membocorkan secret
- error tidak membocorkan internal data
- tidak ada endpoint yang secara tidak sengaja menjadi public

Jangan membuat endpoint baru.

Jangan mengubah API contract jika tidak ada bug nyata.

==================================================
4. BOT LIFECYCLE REGRESSION
==================================================

Pastikan lifecycle bot tetap konsisten.

Audit operasi yang tersedia:

- create
- read
- list
- update
- enable
- disable
- delete
- configuration
- credentials
- child resources

Pastikan:

- cross-workspace access DENY
- unauthorized mutation DENY
- ownership spoof DENY
- workspace spoof DENY
- credential spoof DENY
- invalid lifecycle transition ditangani sesuai architecture

Jangan membuat state baru.

==================================================
5. SECRET / CREDENTIAL FINAL AUDIT
==================================================

Cari kemungkinan credential leakage melalui:

- API response
- error
- logs
- test output
- debug output
- serialization
- audit data
- configuration output

Cari:

- token
- API key
- password
- session token
- webhook secret
- bot credential

Pastikan tidak ada secret hardcoded.

Jangan menampilkan secret selama verification.

Jika menemukan kebocoran nyata, perbaiki minimal dan tambahkan regression test.

==================================================
6. DATABASE MIGRATION
==================================================

Coba verifikasi apakah environment saat ini menyediakan tool migration yang memang diperlukan.

Jika Docker TIDAK tersedia:

JANGAN:
- install Docker
- mengubah source code
- membuat fake migration result
- menghapus migration test
- skip silently

Laporkan:

Database Migration:
BLOCKED — Docker unavailable in verification environment.

Jika ada migration command yang dapat diverifikasi TANPA Docker menggunakan tooling resmi repository, boleh jalankan.

Jika tidak memungkinkan, jangan dipaksakan.

==================================================
7. FULL TEST
==================================================

Jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace tests
- membership tests
- bot/resource tests
- lifecycle tests
- validation tests
- abuse/security tests
- secret leakage tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Jangan skip test.

Jangan menghapus test.

Jika failure:

1. identifikasi root cause
2. perbaiki hanya jika failure disebabkan source code
3. jalankan test terkait
4. jalankan full verification kembali

Jika failure hanya karena environment, jangan mengubah source code untuk memalsukan PASS.

==================================================
8. PACKAGE / DEPENDENCY AUDIT
==================================================

Periksa dependency yang digunakan project.

Cari:

- dependency tidak terpakai
- package yang baru ditambahkan tanpa alasan
- script yang rusak
- duplicate dependency
- configuration yang tidak konsisten

Jangan melakukan upgrade dependency besar pada tahap final.

Jangan mengubah lockfile tanpa kebutuhan.

==================================================
9. TYPESCRIPT / CODE QUALITY
==================================================

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate security system
- tidak ada duplicate validation
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- tidak ada debug code

Jangan melakukan refactor besar hanya untuk style.

==================================================
10. README FINAL
==================================================

Gunakan README.md yang SUDAH ADA.

Jika dokumentasi belum mencerminkan security architecture final, update secara singkat:

- authentication
- workspace isolation
- membership/permission
- bot authorization
- bot lifecycle
- credential security
- verification command
- database migration requirement

Jangan membuat README baru.

Jangan menambahkan dokumentasi yang tidak relevan.

==================================================
11. GIT AUDIT
==================================================

Setelah semua implementation selesai:

git status
git diff --stat
git diff

Pastikan tidak ada:

- .env
- API key
- token
- password
- credential
- logs
- temporary files
- build artifacts

Jika TIDAK ADA perubahan source code yang diperlukan:

JANGAN membuat empty commit.

Jika README atau source code memang berubah karena task final ini:

buat SATU commit.

Gunakan commit message sesuai perubahan sebenarnya.

Contoh:

docs: finalize BotSpace security documentation

atau:

fix: finalize production security checks

Pilih yang benar-benar sesuai.

==================================================
12. PUSH
==================================================

Jika ada commit baru:

git push

Pastikan branch:

backend-dev-recovery

Jangan:

- force push
- reset
- rebase
- ubah remote
- merge ke backend-dev

Jika tidak ada perubahan:

tidak perlu membuat commit.

Tetap pastikan HEAD sudah sinkron dengan origin.

==================================================
13. FINAL STATUS
==================================================

Tampilkan laporan FINAL secara jelas.

Format:

FINAL VERIFICATION

Repository:
- /root/botspace

Branch:
- backend-dev-recovery

Security:
- Authentication: PASS
- Session: PASS
- Workspace authorization: PASS
- Membership: PASS
- Ownership: PASS
- Permission: PASS
- Bot authorization: PASS
- Bot lifecycle: PASS
- Resource integrity: PASS
- Credential security: PASS
- Secret leakage: PASS

Tests:
- Domain: ...
- API: ...
- Observability: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Abuse: ...
- Secret scan: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Database Migration:
- PASS / BLOCKED
- Jika BLOCKED: jelaskan "Docker tidak tersedia"

Git:
- HEAD: ...
- Upstream: ...
- Commit: ...
- Push: success / not needed / failed

Working Tree:
- CLEAN / DIRTY

FINAL DECISION:
- READY
atau
- NOT READY

Jangan menyatakan READY jika ada source-code failure yang belum diperbaiki.

Database migration yang BLOCKED hanya karena Docker tidak tersedia TIDAK dianggap source-code failure.

==================================================
14. ATURAN TERAKHIR
==================================================

Jangan membuat fitur baru.

Jangan memperbesar scope.

Jangan mengulang security architecture.

Jangan membuat authorization system kedua.

Jangan install Docker.

Jangan menyentuh production database.

Jangan mengubah credential GitHub.

Jangan force push.

Fokus hanya pada final verification dan perbaikan kecil jika memang ditemukan bug nyata.

Setelah:

AUDIT
→ TEST
→ BUILD
→ GIT CHECK
→ PUSH jika diperlukan
→ FINAL REPORT

SELESAI.

BERHENTI setelah final report.

```
# Prompt: BotSpace — Final Security Audit & Release Readiness
```

PROMPT: BotSpace — Final Security Audit & Release Readiness

Kita melanjutkan project BotSpace dari checkpoint security terakhir.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

JANGAN:
- reset
- force push
- rebase sembarangan
- checkout branch lain
- merge ke backend-dev
- menghapus checkpoint yang sudah ada

TUJUAN

Ini adalah FINAL AUDIT sebelum project BotSpace dinyatakan siap.

Jangan membuat fitur baru.

Jangan melakukan refactor besar.

Jangan mengubah architecture jika tidak ada bug nyata.

Fokus hanya memastikan seluruh security checkpoint sebelumnya tetap konsisten dan project siap digunakan.

AUDIT FLOW:

Authentication
→ Session
→ Current User
→ Workspace Authorization
→ Membership
→ Ownership
→ Permission
→ Bot Authorization
→ Bot Lifecycle
→ Resource Integrity
→ Secret Security
→ Validation
→ Regression
→ Build

1. AUDIT FINAL

Periksa seluruh implementasi yang sudah ada.

Pastikan tidak ada regression pada:

- authentication
- session
- current user
- workspace isolation
- membership
- ownership
- permission policy
- bot authorization
- bot lifecycle
- child resource authorization
- secret/token handling
- mass-assignment protection
- IDOR protection
- API validation

Jangan membuat sistem security baru.

2. SEARCH SECURITY REGRESSION

Cari kembali pola berbahaya:

- findById(id)
- findUnique({ id })
- where: { id }
- userId dari request sebagai identity
- ownerId dari request
- workspaceId tanpa authorization
- permissions dari request body
- role dari request body
- secret/token pada response
- secret/token pada log
- @ts-ignore baru
- any baru
- TODO security

Jika ditemukan masalah nyata, perbaiki secara minimal.

Jika tidak ditemukan masalah, JANGAN mengubah source code.

3. FINAL TEST

Jalankan full verification repository.

Minimal:

- Domain tests
- API tests
- Auth/Session
- Workspace
- Membership
- Bot/Resource
- Security tests
- Typecheck
- Format
- Import boundary
- Build
- pnpm check

Gunakan command resmi repository.

Jangan skip test.

Jangan menghapus test.

Jika database migration verification membutuhkan Docker tetapi Docker tidak tersedia di environment:

- jangan install Docker hanya untuk membuat hasil terlihat PASS
- jangan mengubah source code untuk menghilangkan BLOCKED
- catat sebagai environment limitation
- semua verification lain tetap harus dijalankan

4. SECURITY RESULT

Pastikan hasil akhir mencakup:

- Cross-workspace access DENY
- Unauthorized membership access DENY
- Ownership escalation DENY
- Permission escalation DENY
- User identity spoofing DENY
- Bot cross-workspace access DENY
- Bot privilege escalation DENY
- Secret leakage DENY
- Mass assignment DENY
- IDOR protection PASS

5. GIT

Setelah verification:

git status
git diff --stat
git diff

Jika TIDAK ADA perubahan source code:

- jangan membuat empty commit
- jangan commit
- jangan push
- cukup laporkan bahwa repository sudah clean dan checkpoint terakhir tetap valid

Jika ADA perubahan source code yang benar-benar diperlukan:

- buat SATU commit
- gunakan commit message sesuai perubahan
- git status
- git log --oneline -3
- git push

Jangan force push.

6. FINAL READINESS

Nyatakan project:

READY

hanya jika:

- security verification PASS
- tests PASS
- build PASS
- typecheck PASS
- working tree clean
- tidak ada regression
- tidak ada secret leakage
- tidak ada unresolved source-code blocker

Jika ada blocker nyata, nyatakan:

NOT READY

dan tampilkan blocker sebenarnya.

7. LAPORAN AKHIR

Tampilkan:

FINAL STATUS:
- READY / NOT READY

Security:
- Authentication: PASS/FAIL
- Session: PASS/FAIL
- Workspace: PASS/FAIL
- Membership: PASS/FAIL
- Ownership: PASS/FAIL
- Permission: PASS/FAIL
- Bot Authorization: PASS/FAIL
- Bot Lifecycle: PASS/FAIL
- Resource Integrity: PASS/FAIL
- Secret Leakage: PASS/FAIL
- IDOR: PASS/FAIL
- Mass Assignment: PASS/FAIL

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Security: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- pnpm check: ...
- Build: ...

Database Migration:
- PASS / BLOCKED
- jika BLOCKED, jelaskan hanya karena environment Docker tidak tersedia

Git:
- Branch: ...
- HEAD: ...
- Working tree: clean/dirty
- Commit: ...
- Push: success/not needed/failed

FINAL DECISION:
- READY / NOT READY

PENTING:

Jika semua sudah PASS dan tidak ada perubahan source code baru, JANGAN memaksa membuat commit.

Ini adalah final audit, bukan tahap implementasi fitur baru.

Selesaikan audit sampai FINAL STATUS jelas, lalu berhenti.

```
# 
```
PROMPT: BotSpace — Validation & Mass-Assignment Hardening

Lanjutkan project BotSpace dari checkpoint terakhir yang SUDAH VALID.

Repository: /root/botspace
Branch: backend-dev-recovery

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint.

KONDISI TERAKHIR:
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Working tree: clean
- Database migration BLOCKED hanya karena Docker tidak tersedia

TUJUAN

Lakukan audit terakhir yang terarah pada:
- API input validation
- mass-assignment
- privilege escalation melalui request body
- unsafe field updates
- bounded pagination/filter/sort
- abuse boundary

PENTING:
Jika semua area sudah benar dan test sudah PASS, JANGAN mengubah source code hanya untuk membuat commit.

AUDIT:

1. Cari endpoint/service yang menerima:
- workspaceId
- userId
- accountId
- ownerId
- role
- permissions
- status
- createdBy
- botId
- resourceId

Pastikan field server-controlled tidak dapat digunakan untuk menaikkan privilege atau mengambil resource lain.

2. Audit pola mass-assignment seperti:
- spread request body langsung ke entity
- Object.assign
- update(data)
- create(data)

Pastikan hanya field yang memang boleh diubah endpoint yang diproses.

3. Audit:
- pagination limit
- offset/cursor
- sorting
- filtering
- search

Pastikan tidak ada query atau response yang tidak bounded.

4. Audit privilege escalation:
- role spoof
- permission spoof
- ownerId spoof
- userId spoof
- workspaceId spoof
- accountId spoof

Pastikan authorization selalu berdasarkan authenticated identity dan policy backend.

5. Audit validation schema yang sudah tersedia.
Jangan membuat validation framework baru.

6. Jangan mengubah database schema kecuali ditemukan bug nyata yang memang membutuhkan perubahan.

7. Tambahkan test hanya jika memang ada coverage gap nyata.
Jangan membuat test duplikat.

VERIFICATION:

Jalankan:
- targeted validation/mass-assignment tests
- Domain tests
- API tests
- Typecheck
- Format
- Import boundary
- Build
- pnpm check

Database migration boleh tetap BLOCKED jika Docker tidak tersedia.

Jika ditemukan bug:
AUDIT → FIX → TEST → FULL VERIFICATION

Jika tidak ditemukan bug:
jangan membuat perubahan dan jangan membuat empty commit.

GIT:

Jika ada perubahan valid dan semua verification PASS:
- git status
- git diff --stat
- git diff
- satu commit
- git push

Jika tidak ada perubahan:
- jangan commit
- jangan push

Tetap di branch:
backend-dev-recovery

Jangan merge ke backend-dev.

HASIL AKHIR:

Laporkan singkat:
- temuan
- perubahan
- validation
- mass-assignment
- abuse boundary
- tests
- build
- commit/push jika ada
- working tree

Setelah selesai, berhenti.


```
# API Boundary & Abuse Hardening
```

PROMPT: BotSpace — API Boundary & Abuse Hardening

Lanjutkan project BotSpace dari checkpoint TERAKHIR yang SUDAH VALID.

Repository: /root/botspace
Branch: backend-dev-recovery

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint.

HASIL VERIFICATION TERAKHIR:
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Response/secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Working tree: clean

Database migration integration:
BLOCKED karena environment tidak memiliki Docker.
Jangan menginstal Docker dan jangan mengubah source code hanya untuk mengatasi blocker environment tersebut.

TUJUAN

Karena security workspace, membership, authentication, bot authorization, lifecycle, credential integrity, dan mass-assignment sudah PASS, lakukan audit berikutnya pada API boundary dan abuse resistance.

Fokus hanya pada masalah nyata yang ditemukan.

AUDIT:

1. API boundary
- protected endpoint wajib authentication
- workspace/resource endpoint wajib authorization
- jangan percaya userId/workspaceId dari client
- pastikan resource ID tidak dapat digunakan untuk IDOR

2. Input abuse
Audit:
- pagination
- limit
- offset/cursor
- filter
- sorting
- search
- bulk/mass assignment
- nested input
- oversized input

Pastikan endpoint tidak menerima nilai yang dapat menyebabkan unbounded query atau response.

3. Pagination
Pastikan list endpoint memakai bounded pagination jika architecture memang mendukungnya.

Jangan membuat pagination system baru.

4. Resource enumeration
Pastikan user tidak dapat menggunakan list/detail endpoint untuk mengambil resource workspace lain.

5. Error boundary
Pastikan error:
- tidak membocorkan secret
- tidak membocorkan resource workspace lain
- tidak membocorkan stack trace/internal detail production
- mengikuti error convention yang sudah ada

6. Logging
Pastikan:
- token/credential/password tidak masuk log
- request body sensitif tidak dilog
- error tidak membocorkan secret

7. Regression
Jangan merusak security yang sudah PASS.

TEST minimal sesuai endpoint yang benar-benar tersedia:
- unauthenticated → DENY
- cross-workspace → DENY
- invalid pagination → DENY/normalize sesuai convention
- excessive limit → bounded/rejected
- invalid filter → handled safely
- unauthorized resource enumeration → DENY
- secret leakage → PASS

Jangan membuat endpoint baru.
Jangan membuat security framework baru.
Jangan membuat fitur besar.

VERIFICATION:

Jalankan:
- targeted tests
- domain tests
- API tests
- typecheck
- format
- import boundary
- build
- pnpm check

Database migration boleh tetap BLOCKED jika hanya karena Docker tidak tersedia.
Jangan menganggap blocker Docker sebagai source-code failure.

Jika ada masalah nyata:
AUDIT → FIX → TEST → FULL VERIFICATION

Jika tidak ada masalah:
jangan membuat perubahan hanya demi menghasilkan commit.

GIT:

Jika ada perubahan valid dan seluruh verification PASS:
- git status
- git diff --stat
- git diff
- buat SATU commit
- git push

Jika tidak ada perubahan:
- jangan membuat empty commit
- jangan push ulang

Tetap di branch:
backend-dev-recovery

HASIL AKHIR:

Laporkan:
- temuan
- perubahan
- tests
- build
- database migration blocker jika masih ada
- commit jika ada
- push jika dilakukan
- working tree

Jangan mengklaim ada perubahan jika repository memang tidak berubah.

Setelah selesai, berhenti.

```
# Prompt berikutnya — Bot Lifecycle & Resource Integrity
```

PROMPT: BotSpace — Bot Lifecycle & Resource Integrity

Lanjutkan project BotSpace dari checkpoint yang SUDAH BERHASIL dipush.

Repository: /root/botspace
Branch: backend-dev-recovery
Checkpoint terakhir: ab4df16
Commit: fix: harden bot credential reference integrity

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint.

TUJUAN

Audit dan harden BOT LIFECYCLE serta RESOURCE INTEGRITY tanpa membuat arsitektur baru.

Security yang sudah dikerjakan sebelumnya:
- authentication/session
- workspace authorization
- membership/ownership
- permission policy
- bot resource authorization
- credential/reference integrity

Sekarang pastikan lifecycle bot tidak dapat menghasilkan state atau relasi resource yang tidak valid.

1. AUDIT DAHULU

Baca implementasi aktual repository.

Cari:
- create bot
- get/list bot
- update bot
- delete bot
- enable/disable
- bot status
- bot configuration
- bot credentials
- child resources yang memiliki botId

Jangan membuat endpoint baru.

2. BOT CREATION

Pastikan:
- authenticated user wajib digunakan
- workspace harus dapat diakses user
- workspaceId tidak dapat digunakan untuk membuat bot di workspace lain
- ownerId/accountId tidak dapat dipalsukan dari request
- relasi User → Workspace → Bot tetap konsisten

3. BOT UPDATE

Audit field yang dapat diubah.

Pastikan request tidak dapat mengubah secara ilegal:
- workspaceId
- ownerId
- accountId
- createdBy
- permissions
- role

Gunakan explicit field mapping jika diperlukan.

4. BOT DELETE

Pastikan:
- authorization diperiksa sebelum mutation
- user workspace lain ditolak
- permission delete tetap dihormati
- child resource tidak menjadi orphan secara tidak sengaja

Pertahankan mekanisme soft/hard delete yang sudah digunakan repository.

5. ENABLE / DISABLE / STATUS

Audit seluruh perubahan status.

Pastikan:
- hanya user yang berwenang yang dapat mengubah status
- cross-workspace selalu DENY
- bot yang sudah tidak valid tidak dapat dipaksa ke state yang tidak didukung

Jangan membuat state baru jika belum ada di architecture.

6. CHILD RESOURCE

Audit resource yang memiliki botId, misalnya jika tersedia:
- commands
- flows
- settings
- integrations
- webhook
- logs
- credentials
- analytics

Pastikan child resource tidak dapat diakses atau dimodifikasi hanya dengan mengetahui ID-nya jika parent bot tidak boleh diakses user tersebut.

7. RELATION INTEGRITY

Cari kemungkinan:
- bot.workspaceId berbeda dari workspace yang seharusnya
- bot.ownerId tidak sesuai
- accountId tidak sesuai
- child resource menunjuk bot yang salah
- resource menunjuk parent yang tidak ada

Jangan memperbaiki data production otomatis.

Fokus pada source code, validation, authorization, dan test.

8. CREDENTIAL SECURITY

Pastikan credential/token/secret:
- tidak muncul pada list bot
- tidak bocor pada response yang tidak diperlukan
- tidak masuk log
- tidak masuk error message
- tidak dapat digunakan untuk mengubah ownership/workspace

Gunakan abstraction security yang sudah ada.

9. TEST

Tambahkan/perbaiki test sesuai resource yang memang tersedia.

Minimal:

Create:
- valid workspace → PASS
- cross-workspace → DENY
- spoofed ownerId → DENY
- spoofed accountId → DENY

Read:
- own bot → PASS
- other workspace bot → DENY

Update:
- authorized → PASS
- unauthorized → DENY
- workspaceId spoof → DENY
- ownerId spoof → DENY

Delete:
- authorized → PASS
- unauthorized → DENY
- cross-workspace → DENY

Status:
- authorized enable/disable → PASS
- unauthorized → DENY
- cross-workspace → DENY

Child resource:
- authorized → PASS
- cross-workspace → DENY

Credential:
- secret tidak bocor pada response/log/error.

Jangan membuat test untuk endpoint yang tidak tersedia.

10. REGRESSION

Pastikan test sebelumnya tetap PASS:

- authentication
- session
- workspace authorization
- membership
- ownership
- permission
- bot authorization
- credential integrity

11. VERIFICATION

Jalankan verification resmi repository:

- domain tests
- API tests
- auth/session
- workspace/membership
- bot/resource
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Jika gagal:
→ cari root cause
→ perbaiki
→ test ulang
→ full verification ulang.

Jangan skip atau menghapus test.

12. GIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jika semua PASS:

buat SATU commit dengan message sesuai perubahan, misalnya:

fix: harden bot lifecycle integrity

Kemudian:

git status
git log --oneline -3
git push

Tetap di:
backend-dev-recovery

Jangan merge atau force push.

13. LAPORAN

Laporkan:

Implementation:
- ...

Lifecycle:
- ...

Resource integrity:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Bot/Resource: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash
- message

Git:
- branch
- push

Working tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Selesaikan:
AUDIT → IMPLEMENT → TEST → BUILD → COMMIT → PUSH

Setelah push berhasil, berhenti.

```
# 
```
PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint security terakhir yang SUDAH BERHASIL DIPUSH.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Gunakan HEAD/commit yang saat ini benar-benar aktif sebagai checkpoint.
JANGAN menebak atau mengganti checkpoint berdasarkan dokumentasi lama.

JANGAN:
- reset
- force push
- rebase sembarangan
- checkout branch lain
- merge ke backend-dev
- menghapus commit yang sudah berhasil dipush
- mengubah remote Git

TUJUAN

Lanjutkan BotSpace ke tahap BOT LIFECYCLE dan RESOURCE INTEGRITY.

Authentication, session security, workspace authorization, membership, ownership, permission policy, dan bot resource authorization yang sudah ada harus tetap dipertahankan.

Fokus:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ BOT AUTHORIZATION
→ BOT LIFECYCLE
→ RESOURCE INTEGRITY
→ STATE TRANSITION
→ DATABASE CONSISTENCY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat authorization system kedua.

1. AUDIT TERLEBIH DAHULU

Sebelum mengubah kode, audit repository aktual.

Cari:

- Bot entity/model
- Bot repository
- Bot service
- Bot API routes
- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot
- bot status
- bot configuration
- bot credentials
- bot settings
- bot commands
- bot flows
- bot integrations
- bot webhook
- seluruh resource yang memiliki botId

Pahami hubungan:

User
→ Account
→ Workspace
→ Bot
→ Bot Resource

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat endpoint baru hanya untuk task ini.

2. BOT STATE

Identifikasi state bot yang benar-benar digunakan repository saat ini.

Jangan membuat state baru jika belum ada.

Audit seluruh operasi:

- create
- enable
- disable
- update
- delete
- status change

Pastikan setiap perubahan state:

Authentication
→ Workspace access
→ Bot authorization
→ Permission
→ State mutation

Authorization harus dilakukan SEBELUM mutation.

3. INVALID STATE TRANSITION

Jika repository memiliki konsep deleted/inactive/disabled state, audit transisi yang tidak valid.

Contoh:

deleted → enable
deleted → update
deleted → disable

Sesuaikan dengan behavior yang memang sudah digunakan project.

Jangan membuat state machine baru jika repository belum menggunakannya.

4. BOT CREATION INTEGRITY

Audit create bot.

Pastikan:

- user harus authenticated
- workspace harus valid
- user harus memiliki akses workspace
- bot dibuat pada workspace yang benar
- owner/creator ditentukan dari authentication context
- client tidak dapat memalsukan ownerId
- client tidak dapat memalsukan accountId
- client tidak dapat membuat bot pada workspace yang tidak dapat diakses

Jangan hanya memvalidasi bahwa workspaceId ada.

5. BOT UPDATE INTEGRITY

Audit seluruh field yang dapat diubah.

Pisahkan:

CLIENT-CONTROLLED FIELD

dan

SERVER-CONTROLLED FIELD

Audit khusus:

- id
- workspaceId
- ownerId
- accountId
- createdBy
- createdAt
- updatedAt
- status
- role
- permissions
- credential identifiers

Update biasa tidak boleh digunakan untuk memindahkan bot ke workspace lain atau mengganti ownership jika architecture tidak mendukungnya.

Gunakan explicit field mapping jika diperlukan.

6. BOT DELETE

Audit delete bot.

Pastikan:

- authorization dilakukan sebelum delete
- cross-workspace delete ditolak
- member tanpa permission delete ditolak
- nonexistent bot mengikuti error convention
- child resource tidak menjadi orphan secara tidak sengaja

Jika project menggunakan soft delete, pertahankan soft delete.

Jika menggunakan hard delete, audit dependency terlebih dahulu.

Jangan mengubah mekanisme delete tanpa alasan.

7. BOT ENABLE / DISABLE

Audit semua endpoint/service:

- enable
- disable
- activate
- deactivate
- start
- stop

Gunakan hanya operasi yang memang tersedia.

Test minimal:

- authorized user → PASS
- unauthorized member → DENY
- cross-workspace user → DENY
- unauthenticated → DENY

8. CHILD RESOURCE INTEGRITY

Cari seluruh resource yang bergantung pada bot.

Jika tersedia, audit:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- credentials
- analytics
- configuration

Pastikan child resource mengikuti security boundary parent bot/workspace.

User yang tidak dapat mengakses bot tidak boleh mengakses child resource hanya dengan mengetahui child resource ID.

Jangan membuat cascade delete besar-besaran jika database tidak mendukungnya.

9. RELATION INTEGRITY

Audit relasi:

User
→ Account
→ Workspace
→ Bot
→ Child Resource

Cari kemungkinan:

- bot.workspaceId berbeda dari workspace yang seharusnya
- ownerId tidak konsisten
- accountId tidak sesuai workspace
- botId invalid
- child resource menunjuk bot yang tidak ada
- child resource menunjuk bot workspace lain

Fokus pada enforcement dan test.

JANGAN mengubah data production secara otomatis.

10. DATABASE / REPOSITORY SAFETY

Audit method:

- create
- update
- delete
- status update
- child resource creation

Cari pola:

findById(id)
findUnique({ id })
where: { id }

Pastikan authorization tetap dilakukan.

Jika repository sudah mendukung workspace-scoped query, gunakan abstraction tersebut.

Jangan mengubah semua query secara membabi buta.

11. DUPLICATE RESOURCE

Periksa apakah architecture memiliki aturan uniqueness untuk:

- Telegram bot token
- external bot ID
- bot identifier
- workspace resource identifier

Jika memang sudah ada business rule/unique constraint, pastikan enforcement dan error handling benar.

Jangan menciptakan business rule baru tanpa bukti dari repository.

12. CREDENTIAL INTEGRITY

Audit:

- bot token
- webhook secret
- API key
- integration secret
- access token
- refresh token

Pastikan credential:

- tidak menentukan ownership
- tidak menentukan workspace
- tidak muncul pada list bot
- tidak bocor pada response
- tidak masuk log
- tidak masuk error message
- tidak dapat diubah tanpa permission yang sesuai

Jangan mencetak secret dalam test output.

13. MASS ASSIGNMENT

Cari request body yang memungkinkan perubahan banyak field sekaligus.

Contoh berbahaya:

workspaceId
ownerId
accountId
role
permissions
status

Pastikan hanya field yang memang diizinkan endpoint yang diproses.

Server-controlled field tidak boleh dapat digunakan untuk privilege escalation.

14. API INPUT VALIDATION

Audit schema/input untuk:

- botId
- workspaceId
- status
- configuration
- settings
- commandId
- flowId
- integrationId
- webhookId

Gunakan validation system yang sudah ada.

Jangan membuat validation framework baru.

15. ERROR HANDLING

Gunakan error system existing.

Pastikan:

unauthenticated
→ authentication error

authenticated tetapi tidak punya akses
→ authorization error

resource tidak ada
→ not found sesuai convention

invalid state
→ domain/validation error sesuai convention

Jangan membocorkan detail resource workspace lain.

16. TEST MATRIX

Tambahkan atau perbaiki test sesuai resource yang BENAR-BENAR tersedia.

Create:
- authenticated + valid workspace = PASS
- unauthenticated = DENY
- wrong workspace = DENY
- spoofed ownerId = DENY
- spoofed accountId = DENY

Read:
- own bot = PASS
- other workspace bot = DENY

Update:
- authorized update = PASS
- unauthorized update = DENY
- workspaceId spoof = DENY
- ownerId spoof = DENY
- permission spoof = DENY

Delete:
- authorized delete = PASS
- unauthorized delete = DENY
- cross-workspace delete = DENY

Status:
- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY
- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY

Child resources:
- authorized child access = PASS
- cross-workspace child access = DENY
- invalid parent relation = DENY

Credential:
- secret tidak muncul pada response yang tidak seharusnya
- secret tidak muncul pada error
- secret tidak muncul pada log/test output

Jangan membuat test untuk endpoint yang tidak tersedia.

17. SECURITY REGRESSION

Pastikan checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization

Jangan melemahkan test lama.

18. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate lifecycle logic
- tidak ada circular dependency baru
- tidak ada hardcoded secret

19. README

Jika memang diperlukan, UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

- bot lifecycle
- bot status
- authorization
- resource integrity
- test command

20. VERIFICATION

Setelah implementasi jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika gagal:

1. identifikasi root cause
2. perbaiki
3. jalankan ulang test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

21. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary file
- build artifact

22. COMMIT

Jika seluruh verification PASS:

buat SATU commit baru.

Gunakan commit message berdasarkan perubahan sebenarnya.

Contoh:

fix: harden bot lifecycle integrity

atau:

fix: enforce bot lifecycle security

Pilih yang paling sesuai dengan implementation aktual.

Setelah commit:

git status
git log --oneline -3

23. PUSH

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- ubah remote
- merge ke backend-dev
- reset checkpoint
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code lagi.

Pertahankan commit lokal dan laporkan error sebenarnya.

24. LAPORAN AKHIR

Tampilkan:

Implementation:
- ...

Bot Lifecycle:
- ...

Resource Integrity:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum berhasil.

25. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya fokus:

AUDIT
→ BOT LIFECYCLE
→ STATE INTEGRITY
→ OWNERSHIP INTEGRITY
→ WORKSPACE RELATION
→ CHILD RESOURCE INTEGRITY
→ CREDENTIAL SECURITY
→ IDOR TEST
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan abstraction security yang sudah ada.

Jangan membuat authorization system kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil lalu berhenti.


```
# 
```
PROMPT: BotSpace — API Boundary & Resource Enumeration Hardening

Lanjutkan project BotSpace dari checkpoint TERAKHIR yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery

HASIL VERIFICATION TERAKHIR:
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Response/secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

TUJUAN

Lanjutkan security hardening BotSpace dengan fokus pada:

API BOUNDARY
→ RESOURCE ENUMERATION
→ IDOR
→ LIST/SEARCH FILTERING
→ CROSS-WORKSPACE ISOLATION
→ RESPONSE SECURITY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

1. AUDIT API BOUNDARY

Audit seluruh protected API yang berhubungan dengan:

- workspace
- membership
- bot
- bot resource
- integration
- credential
- webhook
- logs
- statistics
- settings
- commands
- flows
- resource lain yang tersedia

Pastikan setiap endpoint mengikuti:

Authentication
→ Current User
→ Workspace Access
→ Resource Ownership/Membership
→ Permission
→ Operation

Jangan membuat authorization system baru.

2. RESOURCE ENUMERATION

Cari kemungkinan user dapat melakukan enumeration terhadap resource dengan:

- ID guessing
- sequential ID
- UUID
- search
- filter
- sorting
- pagination
- list endpoint
- detail endpoint
- error response

User dari workspace-A tidak boleh mengetahui keberadaan resource workspace-B hanya dengan mencoba ID resource.

Pastikan behavior error mengikuti convention project dan tidak membocorkan metadata yang tidak diperlukan.

3. LIST ENDPOINT

Audit seluruh endpoint list.

Pastikan response hanya berisi resource yang memang boleh dilihat oleh authenticated user.

Jangan menggunakan pola:

ambil semua resource
→ filter di memory

jika repository/service memungkinkan query yang sudah workspace-scoped.

Pastikan:

- workspace isolation
- membership authorization
- permission
- pagination boundary
- maximum limit

tetap enforced.

4. SEARCH DAN FILTER

Audit endpoint yang menerima:

- search
- query
- filter
- status
- ownerId
- workspaceId
- accountId
- botId

Jangan mempercayai field tersebut sebagai authorization.

Contoh:

workspaceId=workspace-B

tidak boleh membuat User A dapat mencari resource workspace-B.

Authorization harus ditentukan berdasarkan authentication context dan policy.

5. PAGINATION

Pastikan seluruh list/search endpoint:

- memiliki default limit
- memiliki maximum limit
- tidak menerima unlimited request
- pagination tetap workspace-scoped
- pagination tidak dapat melewati authorization boundary

Jika pagination sudah benar, jangan mengubahnya.

Jangan membuat pagination framework baru.

6. IDOR AUDIT

Cari pola seperti:

findById(id)
findUnique({ id })
where: { id }

Untuk setiap hasil lookup, pastikan authorization dilakukan dengan benar.

Periksa terutama:

- workspace
- membership
- bot
- child resource
- integration
- credential
- webhook
- command
- flow
- logs
- statistics

Jangan mengubah semua query secara membabi buta.

Perbaiki hanya vulnerability nyata.

7. RESPONSE SECURITY

Audit response DTO/schema.

Pastikan endpoint tidak membocorkan:

- password
- API key
- bot token
- webhook secret
- session token
- credential
- internal authorization metadata
- resource workspace lain

Jangan mengembalikan raw database object jika menyebabkan secret leakage.

8. ERROR SECURITY

Audit error response untuk:

- invalid ID
- unauthorized resource
- nonexistent resource
- cross-workspace resource
- invalid filter
- invalid pagination

Pastikan error tidak membocorkan:

- database details
- stack trace
- secret
- token
- credential
- resource metadata workspace lain

Gunakan error system existing.

9. INPUT BOUNDARY

Audit input API:

- ID
- search string
- filter
- arrays
- pagination
- sorting
- batch input

Pastikan validation existing benar-benar enforced.

Jangan membuat validation framework baru.

10. REGRESSION TEST

Tambahkan test hanya jika diperlukan.

Minimal:

- User A tidak dapat list resource workspace B
- User A tidak dapat search resource workspace B
- User A tidak dapat mengambil detail resource workspace B
- User A tidak dapat menggunakan filter workspace B untuk bypass authorization
- pagination tidak melewati workspace boundary
- invalid resource ID tidak membocorkan metadata
- unauthorized resource tidak membocorkan secret
- existing abuse tests tetap PASS

Sesuaikan dengan endpoint yang benar-benar tersedia.

Jangan membuat test untuk endpoint yang tidak ada.

11. FULL REGRESSION

Pastikan tetap PASS:

- Domain
- API
- Observability
- Auth/Session
- Workspace
- Membership
- Bot/Resource
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage
- Typecheck
- Format
- Import boundary
- Build
- pnpm check

Jangan skip test.

Jangan menghapus test existing.

12. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada unused import
- tidak ada dead code
- tidak ada hardcoded secret
- tidak ada circular dependency baru

13. README

Jika benar-benar diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan hanya perubahan penting.

14. GIT

Setelah verification PASS:

git status
git diff --stat
git diff

Pastikan perubahan hanya terkait task ini.

Jika ada perubahan valid:

buat SATU commit.

Gunakan commit message berdasarkan perubahan sebenarnya, misalnya:

fix: harden api resource boundaries

Kemudian:

git status
git log --oneline -3
git push

Branch tetap:

backend-dev-recovery

Jangan force push.
Jangan ubah remote.
Jangan merge ke backend-dev.

Jika tidak ada perubahan valid:
jangan membuat empty commit.

15. HASIL AKHIR

Laporkan:

Implementation:
- ...

API Boundary:
- ...

Enumeration/IDOR:
- ...

Response Security:
- ...

Tests:
- Domain: ...
- API: ...
- Observability: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Mass-assignment: ...
- Abuse: ...
- Secret leakage: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...
- pnpm check: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification atau push belum berhasil.

Selesaikan:

AUDIT
→ IMPLEMENT
→ TEST
→ BUILD
→ COMMIT
→ PUSH

lalu berhenti.


```
# 
```
PROMPT: BotSpace — API Abuse Protection & Expensive Operation Hardening

Lanjutkan project BotSpace dari checkpoint TERAKHIR yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery

HASIL AUDIT TERAKHIR:
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Response/secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Existing list boundary sudah menggunakan bounded pagination
- Integration endpoint sudah diaudit
- Credential verification endpoint sudah diaudit
- Runtime bot operation sudah diaudit

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

TUJUAN

Lanjutkan security hardening dengan fokus pada:

API ABUSE
→ EXPENSIVE OPERATION
→ PAGINATION BOUNDARY
→ BULK/ENUMERATION PROTECTION
→ RESOURCE LIMIT
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

PENTING:
Jangan membuat framework rate-limit baru jika repository belum memilikinya.
Jangan menambahkan dependency besar.
Gunakan abstraction dan boundary yang sudah ada.

1. AUDIT EXPENSIVE API

Cari endpoint/service yang dapat melakukan operasi mahal atau berulang, terutama:

- integration endpoint
- credential verification endpoint
- runtime bot operation
- search/list endpoint
- statistics/analytics
- logs
- export
- bulk operation
- webhook processing
- endpoint yang melakukan external API call

Pahami implementation aktual sebelum mengubah kode.

2. PAGINATION

Audit seluruh endpoint list/search.

Pastikan:

- pagination memiliki batas maksimum
- client tidak dapat meminta jumlah record tidak terbatas
- default limit aman
- limit maksimum enforced di backend
- cursor/offset tidak dapat digunakan untuk melewati authorization boundary
- query tetap workspace-scoped jika resource bersifat workspace-scoped

Jangan mengubah pagination yang sudah benar.

3. EXPENSIVE OPERATION LIMIT

Untuk endpoint yang melakukan operasi mahal:

- periksa apakah sudah memiliki guard/validation
- periksa apakah request dapat melakukan pekerjaan berulang tanpa batas
- periksa apakah input size sudah dibatasi
- periksa apakah batch size sudah dibatasi
- periksa apakah timeout/limit sudah tersedia

Jika repository belum memiliki mechanism yang sesuai:

JANGAN membuat framework baru.

Dokumentasikan sebagai future hardening scope jika memang diperlukan.

4. CREDENTIAL VERIFICATION

Audit credential verification endpoint.

Pastikan user tidak dapat:

- melakukan verification terhadap credential workspace lain
- menggunakan bot/resource ID milik workspace lain
- melakukan verification dengan input tidak terbatas
- membocorkan credential melalui response/error/log

Authorization harus dilakukan sebelum operasi verification.

Jangan pernah menampilkan credential asli dalam test output.

5. RUNTIME BOT OPERATION

Audit endpoint/service yang menjalankan operasi bot runtime.

Pastikan:

- authentication wajib
- workspace authorization wajib
- bot authorization wajib
- bot dari workspace lain ditolak
- input operation dibatasi
- operation tidak dapat dijalankan berulang tanpa boundary yang tersedia
- error tidak membocorkan credential/internal detail

Jangan mengubah behavior bot jika tidak ada security issue nyata.

6. BULK OPERATION

Cari endpoint yang menerima array/list input.

Periksa:

- maximum items
- maximum payload size
- duplicate items
- invalid IDs
- cross-workspace IDs
- nested/bulk request abuse

Jika limit sudah tersedia, pastikan benar-benar enforced di backend.

Jangan menambahkan bulk endpoint baru.

7. ENUMERATION

Pastikan pagination/search tidak dapat digunakan untuk melakukan enumeration resource workspace lain.

Test:

User A:
workspace-A

User B:
workspace-B

User A tidak boleh menemukan resource workspace-B melalui:

- list
- search
- pagination
- filter
- sorting
- ID guessing
- child resource ID

Authorization harus tetap berlaku pada setiap query.

8. REQUEST SIZE / INPUT BOUNDARY

Audit input yang dapat berukuran besar:

- strings
- arrays
- JSON configuration
- filters
- search query
- batch input
- bot configuration
- webhook payload

Pastikan schema validation yang sudah ada memiliki boundary yang wajar jika memang diperlukan.

Jangan membuat validation framework baru.

9. RATE LIMITING

Cari apakah repository sudah memiliki:

- rate limiter
- throttle
- request counter
- abuse guard
- retry protection

Jika SUDAH ADA:
- pastikan endpoint sensitif menggunakannya sesuai abstraction existing.

Jika BELUM ADA:
- jangan membuat framework rate limiter baru pada task ini.
- dokumentasikan endpoint yang membutuhkan rate limiting sebagai future scope.

Jangan mengklaim rate limiting sudah implemented jika memang belum ada.

10. TEST

Tambahkan regression test hanya jika memang ada behavior yang diperbaiki.

Minimal audit/test:

- pagination maximum enforced
- oversized list request ditolak
- oversized batch ditolak jika batch memang tersedia
- cross-workspace list/search ditolak
- credential verification cross-workspace ditolak
- runtime bot operation cross-workspace ditolak
- unauthorized expensive operation ditolak
- existing abuse tests tetap PASS

Jangan membuat test untuk endpoint yang tidak tersedia.

11. SECURITY REGRESSION

Pastikan tetap PASS:

- Authentication
- Session
- Workspace
- Membership
- Ownership
- Permission
- Bot/Resource
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage
- Observability

Jangan melemahkan test lama.

12. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate validation
- tidak ada duplicate authorization
- tidak ada hardcoded secret
- tidak ada circular dependency baru

13. VERIFICATION

Jalankan verification resmi repository.

Minimal:

- Domain tests
- API tests
- Observability tests
- Auth/Session tests
- Workspace tests
- Membership tests
- Bot/Resource tests
- Lifecycle tests
- Validation tests
- Mass-assignment tests
- Abuse tests
- Response/secret leakage tests
- Typecheck
- Format
- Import boundary
- Build
- pnpm check

Jika gagal:

1. cari root cause
2. perbaiki
3. jalankan test terkait
4. ulangi full verification

Jangan skip test.

14. GIT

Sebelum commit:

git status
git diff --stat
git diff

Jika TIDAK ada perubahan valid:
- jangan membuat empty commit
- jangan push ulang tanpa kebutuhan
- laporkan bahwa checkpoint tetap sama

Jika ADA perubahan valid:
- buat SATU commit
- gunakan commit message berdasarkan perubahan sebenarnya
- jalankan git status
- jalankan git log --oneline -3
- git push

Branch tetap:
backend-dev-recovery

Jangan force push.
Jangan mengubah remote.
Jangan merge ke backend-dev.

15. HASIL AKHIR

Laporkan:

Implementation:
- ...

API Abuse:
- ...

Pagination:
- ...

Expensive Operations:
- ...

Rate Limit:
- existing / future scope

Tests:
- Domain: ...
- API: ...
- Observability: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Mass-assignment: ...
- Abuse: ...
- Response/secret leakage: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...
- pnpm check: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification belum selesai.

16. PENTING

Scope hanya:

AUDIT
→ API ABUSE
→ EXPENSIVE OPERATION
→ PAGINATION
→ INPUT/REQUEST BOUNDARY
→ ENUMERATION
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat fitur besar baru.
Jangan membuat rate-limit framework baru tanpa existing architecture.
Jangan mengubah business behavior tanpa bukti security issue.

Selesaikan sampai verification dan push selesai, lalu berhenti.


```
# 
```
PROMPT: BotSpace — API Abuse & Rate-Limit Boundary Audit

Lanjutkan project BotSpace dari checkpoint yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Checkpoint: 28d9438 — fix: secure bot resource authorization

HASIL TERAKHIR:
- Domain: PASS
- API: PASS
- Observability: PASS
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Response/secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Working tree: clean
- Tidak ada commit baru karena tidak ada perubahan valid

JANGAN reset, force push, rebase sembarangan, merge ke backend-dev, atau menghapus checkpoint.

TUJUAN

Audit tahap berikutnya:

API ABUSE
→ RATE-LIMITING BOUNDARY
→ RESOURCE ENUMERATION PROTECTION
→ EXPENSIVE OPERATION PROTECTION
→ REGRESSION TEST

PENTING:
Jangan membuat rate-limit framework baru jika repository belum memilikinya.
Jangan menambahkan dependency besar hanya untuk task ini.
Jika rate limiting memang belum tersedia, audit boundary dan dokumentasikan sebagai future scope.

1. AUDIT

Cari implementasi yang sudah ada untuk:

- rate limit
- throttling
- request limits
- abuse protection
- pagination
- expensive API operation
- authentication abuse
- bot creation abuse
- resource enumeration
- bulk operation

Gunakan architecture repository aktual.

2. IDENTIFIKASI ENDPOINT SENSITIF

Audit endpoint yang berpotensi disalahgunakan:

- login/authentication
- session
- bot creation
- bot deletion
- bot enable/disable
- workspace creation
- membership mutation
- search/list resource
- bulk operation
- webhook/integration
- endpoint yang menjalankan operasi mahal

Jangan membuat endpoint baru.

3. RATE-LIMIT BOUNDARY

Jika project sudah memiliki rate-limit abstraction:

- pastikan digunakan pada endpoint yang memang membutuhkan
- jangan bypass melalui route alternatif
- jangan menggunakan userId dari request sebagai identity
- gunakan authentication context yang benar

Jika belum ada rate limiter:

JANGAN membuat framework baru.

Dokumentasikan endpoint yang paling membutuhkan rate limiting sebagai future hardening scope.

4. RESOURCE ENUMERATION

Audit apakah attacker dapat melakukan enumeration melalui:

- sequential ID
- pagination
- list endpoint
- search endpoint
- error response
- timing/error difference

Pastikan workspace authorization tetap diterapkan sebelum resource dibocorkan.

Cross-workspace enumeration harus DENY.

5. EXPENSIVE OPERATIONS

Cari operasi yang berpotensi mahal:

- bulk query
- large list
- search tanpa pagination
- bot statistics
- logs
- analytics
- export
- webhook processing

Jika sudah ada limit/pagination, pastikan tidak mudah dibypass.

Jangan mengubah business behavior tanpa bukti masalah nyata.

6. AUTHENTICATION ABUSE

Audit:

- repeated failed login
- session creation abuse
- repeated logout
- invalid token requests

Jika belum ada rate limiting infrastructure, jangan membuat sistem baru.

Pastikan failure tetap aman dan tidak membocorkan credential atau identity.

7. TEST

Tambahkan test hanya jika memang ada behavior yang perlu diperbaiki.

Minimal regression:

- cross-workspace enumeration = DENY
- unauthorized resource listing = DENY
- unauthorized expensive operation = DENY
- invalid authentication = DENY
- existing abuse tests tetap PASS

Jangan membuat test untuk fitur rate limit yang memang belum tersedia.

8. SECURITY REGRESSION

Pastikan tetap PASS:

- Authentication
- Session
- Workspace
- Membership
- Ownership
- Permission
- Bot/Resource
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage

9. VERIFICATION

Jalankan verification repository:

- Domain
- API
- Observability
- Auth/Session
- Workspace
- Membership
- Bot/Resource
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage
- Typecheck
- Format
- Import boundary
- Build
- pnpm check

Jika semua PASS tetapi tidak ada perubahan kode valid:

JANGAN membuat empty commit.

10. GIT

Jika ada perubahan valid:

git status
git diff --stat
git diff

Buat SATU commit dengan message sesuai perubahan.

Kemudian:

git push

Branch tetap:

backend-dev-recovery

Jika tidak ada perubahan valid:

jangan commit dan jangan push.

11. HASIL AKHIR

Laporkan:

Audit:
- ...

Abuse Protection:
- ...

Rate Limit:
- existing / future scope

Enumeration:
- ...

Tests:
- ...

Commit:
- created / no valid changes

Git:
- push success / not needed / failed

Working Tree:
- clean / dirty

Jangan mengklaim implementasi rate limiting jika framework tersebut memang belum ada.

Selesaikan audit ini sampai verification selesai lalu berhenti.


```
# 
```
PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint TERBARU yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

CHECKPOINT TERBARU

Commit:
96831da2797f1553cae5649b9b6d88d625180e8c

Verification terakhir:
- Domain: 107 passed
- API: 113 passed
- Observability: 31 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse: PASS
- Response/secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful

JANGAN:
- reset commit
- force push
- rebase sembarangan
- checkout branch lain
- merge ke backend-dev
- menghapus checkpoint yang sudah ada

Pertahankan seluruh security hardening sebelumnya.

TUJUAN

Lanjutkan BotSpace ke tahap berikutnya dengan fokus pada:

BOT LIFECYCLE
→ RESOURCE STATE INTEGRITY
→ DATABASE CONSISTENCY
→ CHILD RESOURCE INTEGRITY
→ CONCURRENCY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Authentication, session security, workspace authorization, membership, bot authorization, input validation, mass-assignment, abuse boundaries, dan response/secret security sudah diperbaiki.

Jangan membuat authorization system kedua.

1. AUDIT BOT LIFECYCLE

Audit implementasi bot yang benar-benar tersedia di repository.

Cari:

- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot
- status bot
- configuration bot
- settings bot
- credential bot
- webhook bot
- integrations bot
- commands
- flows
- logs
- statistics
- resource lain yang memiliki botId

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat endpoint baru jika belum tersedia.

2. IDENTIFIKASI STATE AKTUAL

Cari state bot yang benar-benar digunakan project.

Contoh hanya jika memang ada:

- active
- inactive
- disabled
- pending
- stopped
- deleted

JANGAN membuat state baru hanya untuk task ini.

Dokumentasikan state yang ditemukan dan audit transisinya.

3. STATE TRANSITION

Pastikan operasi:

- enable
- disable
- activate
- deactivate
- start
- stop

hanya dapat dilakukan oleh user yang memiliki authorization sesuai policy yang sudah ada.

Authorization harus dilakukan SEBELUM mutation.

Jangan mempercayai botId saja sebagai bukti akses.

4. INVALID STATE TRANSITION

Audit kemungkinan transition yang tidak valid.

Contoh jika deleted state memang ada:

deleted
→ enable

deleted
→ update

deleted
→ disable

Jika repository tidak memiliki deleted state atau state machine formal, jangan membuat behavior baru.

Ikuti behavior yang memang sudah ada.

5. BOT CREATION INTEGRITY

Audit create bot.

Pastikan bot baru:

- dibuat oleh authenticated user
- workspace valid
- user memiliki akses ke workspace
- workspaceId tidak dapat digunakan untuk masuk ke workspace lain
- ownerId tidak dapat dipalsukan
- accountId tidak dapat dipalsukan
- creator identity berasal dari authentication context

Server harus menentukan ownership dari context yang dipercaya.

6. BOT UPDATE INTEGRITY

Audit seluruh field update.

Pisahkan:

CLIENT CONTROLLED
dan
SERVER CONTROLLED

Perhatikan:

- id
- workspaceId
- ownerId
- accountId
- userId
- createdBy
- createdAt
- updatedAt
- status
- role
- permissions
- credential identifiers

Pastikan update biasa tidak dapat memindahkan bot ke workspace lain atau mengganti ownership secara ilegal.

Jangan melemahkan mass-assignment protection yang sudah PASS.

7. DELETE INTEGRITY

Audit delete bot.

Pastikan:

- authorization dilakukan sebelum delete
- cross-workspace delete ditolak
- user tanpa permission ditolak
- nonexistent resource mengikuti error convention
- child resource tidak menjadi orphan secara tidak sengaja

Jika project menggunakan soft delete, pertahankan.

Jika project menggunakan hard delete, jangan mengubah behavior tanpa alasan.

8. CHILD RESOURCE INTEGRITY

Audit resource yang bergantung pada bot.

Contoh jika tersedia:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- credentials
- analytics
- configuration

Pastikan child resource tetap mengikuti:

Authentication
→ Workspace Access
→ Bot Access
→ Permission
→ Resource Access

User yang tidak dapat mengakses bot tidak boleh mengakses child resource hanya dengan mengetahui child resource ID.

Cari juga kemungkinan orphan resource.

Jangan membuat cascade-delete besar jika database architecture tidak mendukungnya.

9. CROSS-WORKSPACE RELATION

Audit hubungan:

User
→ Account
→ Telegram Account
→ Workspace
→ Bot
→ Child Resource

Cari kemungkinan:

- bot.workspaceId berbeda dengan workspace parent
- ownerId tidak sesuai
- accountId tidak sesuai
- child resource memiliki botId invalid
- child resource menunjuk parent yang tidak ada
- resource dapat dibuat dengan parent dari workspace lain

Fokus pada enforcement dan regression test.

Jangan melakukan perubahan langsung terhadap production database.

10. REPOSITORY INTEGRITY

Audit repository/service method yang melakukan:

- create
- update
- delete
- status update
- child resource creation
- child resource update
- child resource deletion

Pastikan client input tidak dapat membuat relasi database yang invalid.

Gunakan repository abstraction yang sudah ada.

Jangan membuat repository system kedua.

11. CONCURRENCY

Audit mutation yang dapat terjadi bersamaan.

Contoh:

Request A:
enable bot

Request B:
disable bot

Periksa apakah race condition dapat menghasilkan state yang tidak konsisten.

Jika transaction atau atomic update sudah tersedia, gunakan abstraction tersebut.

Jangan membuat concurrency framework baru.

Jika tidak ada bug nyata, jangan melakukan refactor besar.

12. DUPLICATE RESOURCE

Periksa apakah architecture memiliki aturan uniqueness untuk:

- bot identifier
- external bot identifier
- Telegram bot identifier
- webhook identifier
- integration identifier

Hanya enforce aturan yang memang sudah ada dalam schema/domain/business logic.

Jangan menciptakan business rule baru tanpa bukti.

13. CREDENTIAL INTEGRITY

Audit credential handling.

Pastikan credential:

- tidak menentukan ownership
- tidak dapat memindahkan workspace
- tidak muncul di list response
- tidak muncul pada error
- tidak masuk log
- tidak dapat diubah user tanpa permission
- tetap terikat pada bot/workspace yang benar

Response/secret leakage checkpoint sebelumnya harus tetap PASS.

14. INPUT VALIDATION REGRESSION

Audit input lifecycle:

- botId
- workspaceId
- status
- configuration
- settings
- commandId
- flowId
- integrationId
- webhookId

Gunakan validation system yang sudah ada.

Jangan membuat validation framework baru.

15. ERROR HANDLING

Gunakan error system yang sudah ada.

Pastikan:

unauthenticated
→ authentication error

authenticated tetapi tidak punya akses
→ authorization error

resource tidak ada
→ not found sesuai convention

invalid state
→ domain/validation error sesuai convention

Jangan membocorkan resource workspace lain.

16. TEST MATRIX

Tambahkan/perbaiki test sesuai resource yang memang tersedia.

CREATE:
- authenticated + valid workspace = PASS
- unauthenticated = DENY
- wrong workspace = DENY
- spoofed ownerId = DENY
- spoofed accountId = DENY

READ:
- own bot = PASS
- cross-workspace bot = DENY

UPDATE:
- authorized update = PASS
- unauthorized update = DENY
- workspaceId spoof = DENY
- ownerId spoof = DENY
- permission spoof = DENY

DELETE:
- authorized delete = PASS
- unauthorized delete = DENY
- cross-workspace delete = DENY

STATUS:
- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY
- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY

CHILD RESOURCE:
- authorized access = PASS
- cross-workspace access = DENY
- invalid parent relation = DENY
- deleted/inaccessible parent behavior = sesuai architecture

CONCURRENCY:
- concurrent state mutation tidak menghasilkan database state korup

17. REGRESSION SECURITY

Pastikan checkpoint sebelumnya tetap PASS:

- Authentication
- Session
- Workspace
- Membership
- Ownership
- Permission
- Bot/Resource authorization
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage

Jangan menghapus atau melemahkan test lama.

18. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate lifecycle logic
- tidak ada circular dependency baru
- tidak ada hardcoded secret

19. README

Jika diperlukan, update README.md yang SUDAH ADA.

JANGAN membuat README baru.

Dokumentasikan singkat:

- bot lifecycle
- state behavior
- resource integrity
- authorization relationship
- test command

20. VERIFICATION

Setelah implementasi jalankan verification resmi repository.

Minimal:

- Domain tests
- API tests
- Observability tests jika tersedia
- Auth/Session
- Workspace
- Membership
- Bot/Resource
- Lifecycle
- Validation
- Mass-assignment
- Abuse
- Response/secret leakage
- Typecheck
- Format
- Import boundary
- lint jika tersedia
- Build
- pnpm check

Jika gagal:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

21. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- password
- credential
- log
- temporary files
- build artifacts

22. COMMIT

Jika ada perubahan valid dan seluruh verification PASS:

buat SATU commit.

Gunakan commit message sesuai implementation aktual.

Contoh:

fix: harden bot lifecycle integrity

atau:

fix: enforce bot resource state integrity

Pilih yang paling sesuai dengan perubahan nyata.

Jika tidak ada perubahan valid:

JANGAN membuat empty commit.

23. PUSH

Setelah commit:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- reset
- rebase sembarangan
- ubah remote
- merge ke backend-dev

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

Pertahankan commit lokal dan laporkan error sebenarnya.

24. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

Bot Lifecycle:
- ...

Resource Integrity:
- ...

State Transition:
- ...

Child Resources:
- ...

Security Regression:
- ...

Tests:
- Domain: ...
- API: ...
- Observability: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Mass-assignment: ...
- Abuse: ...
- Response/secret leakage: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...
- pnpm check: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum benar-benar berhasil.

25. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya:

AUDIT
→ BOT LIFECYCLE
→ STATE INTEGRITY
→ OWNERSHIP INTEGRITY
→ WORKSPACE RELATION
→ CHILD RESOURCE INTEGRITY
→ CONCURRENCY
→ CREDENTIAL SECURITY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan abstraction security yang sudah ada.

Jangan membuat authorization system kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil lalu berhenti.


```
# 
```

PROMPT: BotSpace — API Data Exposure & Response Security Hardening

Kita melanjutkan project BotSpace dari checkpoint TERBARU yang SUDAH BERHASIL secara lokal.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terbaru:
208d2fd — fix: harden api abuse boundaries

Verification checkpoint:
- Domain: 107 passed
- API: 113 passed
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse/pagination/body-limit: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Working tree: clean

Catatan Git:
- branch: backend-dev-recovery
- local HEAD: 208d2fd
- upstream masih e961be8
- push gagal hanya karena credential GitHub:
  fatal: could not read Username for 'https://github.com': No such device or address
- JANGAN reset commit 208d2fd.
- JANGAN force push.
- JANGAN rebase sembarangan.
- JANGAN merge ke backend-dev.
- Pertahankan semua commit lokal.

TUJUAN

Lanjutkan security hardening BotSpace dengan fokus pada API DATA EXPOSURE dan RESPONSE SECURITY.

Security boundary berikut sudah diperbaiki:

Authentication
→ Session
→ Workspace Authorization
→ Membership
→ Ownership
→ Permission
→ Bot Resource Authorization
→ Input Validation
→ Mass Assignment
→ API Abuse Boundaries

Sekarang audit apakah API dapat membocorkan data yang sebenarnya tidak boleh dikembalikan kepada client.

Jangan membuat framework baru.
Gunakan abstraction dan DTO yang sudah ada.

1. AUDIT SELURUH API RESPONSE

Audit endpoint API yang sudah tersedia.

Cari response yang mengembalikan:

- database entity langsung
- ORM object langsung
- user object
- account object
- workspace object
- membership object
- bot object
- credential object
- session object
- integration object
- configuration object
- logs
- statistics
- internal metadata

Pastikan response hanya mengembalikan field yang memang diperlukan client.

Jangan melakukan redesign API besar-besaran.

2. SECRET EXPOSURE

Cari seluruh kemungkinan kebocoran:

- password
- password hash
- session token
- access token
- refresh token
- API key
- bot token
- webhook secret
- integration secret
- credential
- encryption key
- internal secret

Pastikan secret tidak muncul pada:

- list response
- detail response
- create response jika tidak diperlukan
- update response
- error response
- logs
- audit logs
- debug output
- test output

Jika project memang memiliki behavior "show secret once", pertahankan behavior tersebut.

Jangan mengubah secret architecture tanpa kebutuhan.

3. USER DATA EXPOSURE

Audit response user/account.

Pastikan API tidak mengembalikan data internal yang tidak diperlukan seperti:

- password hash
- authentication metadata
- internal session data
- secret fields
- internal database information

Gunakan DTO/serializer yang sudah tersedia jika ada.

Jangan mengembalikan database object mentah jika menyebabkan data leakage.

4. WORKSPACE DATA EXPOSURE

Audit workspace response.

Pastikan user hanya menerima:

- workspace yang memang dapat dia akses
- membership yang memang boleh dia lihat
- metadata yang memang diperlukan

Jangan membocorkan:

- member dari workspace lain
- owner internal workspace lain
- internal permission metadata
- secret configuration
- internal database fields

Cross-workspace isolation harus tetap PASS.

5. MEMBERSHIP RESPONSE

Audit endpoint membership jika tersedia.

Periksa:

- list members
- member detail
- role
- permission
- membership metadata

Pastikan user biasa tidak dapat melihat atau mengubah data membership yang seharusnya hanya dapat dilihat oleh administrator/owner.

Jangan membuat permission baru.
Gunakan policy yang sudah ada.

6. BOT RESPONSE

Audit:

- bot list
- bot detail
- create bot
- update bot
- status response

Pastikan bot response tidak membocorkan:

- bot token
- webhook secret
- API credential
- internal provider credential
- private configuration
- internal authorization metadata

Bot list khususnya harus aman karena biasanya mengembalikan banyak resource sekaligus.

7. CHILD RESOURCE RESPONSE

Jika tersedia:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- statistics
- analytics
- credentials

Audit response masing-masing.

Pastikan child resource tetap mengikuti:

Authentication
→ Workspace Access
→ Bot Access
→ Permission
→ Response Filtering

Jangan hanya mengamankan endpoint tetapi membocorkan parent/child metadata melalui response.

8. ERROR RESPONSE

Audit seluruh API error.

Pastikan production response tidak membocorkan:

- stack trace
- SQL query
- database schema
- filesystem path
- environment variable
- secret
- token
- internal service details
- authorization internals

Gunakan error system yang sudah ada.

Jangan membuat error framework kedua.

Pastikan error behavior tetap konsisten:

Authentication failure
→ authentication error

Authorization failure
→ authorization error

Validation failure
→ validation error

Not found
→ not found convention project

9. ID ENUMERATION RESPONSE

Audit response ketika resource tidak dapat diakses.

Contoh:

User A mencoba bot milik User B.

Pastikan response tidak membocorkan informasi seperti:

- bot exists
- owner
- workspace
- status
- configuration
- timestamps

Ikuti convention repository.

Jangan mengubah semua endpoint menjadi 404 secara membabi buta.

10. LIST RESPONSE

Audit semua endpoint list/search.

Pastikan response:

- hanya berisi resource yang authorized
- tidak mengandung hidden resource
- tidak membocorkan jumlah resource workspace lain
- pagination metadata tidak membocorkan data workspace lain
- total count tidak berasal dari seluruh database jika seharusnya workspace-scoped

Perhatikan terutama:

- total
- count
- hasNext
- cursor
- pagination metadata

11. FILTER DAN SORT

Audit query/filter API.

Pastikan user tidak dapat menggunakan filter untuk mendapatkan data workspace lain.

Contoh:

workspaceId
ownerId
userId
accountId
botId

harus tetap tunduk pada authorization.

Filter bukan security boundary.

12. MASS-ASSIGNMENT REGRESSION

Pastikan perubahan response tidak melemahkan protection yang sudah dibuat.

Server-controlled field tetap server-controlled:

- ownerId
- workspaceId
- accountId
- userId
- createdBy
- permissions
- role
- createdAt
- updatedAt

Jangan mempercayai field tersebut dari request.

13. LOGGING SECURITY

Audit logging yang berkaitan dengan API.

Pastikan log tidak mencetak:

- Authorization header
- session token
- API key
- bot token
- password
- webhook secret
- request body yang berisi secret

Jika ada logging yang terlalu verbose:

- sanitasi field sensitif
- gunakan abstraction logging yang sudah ada
- jangan membuat logging framework baru

14. SERIALIZATION / DTO

Cari apakah project sudah memiliki:

- DTO
- serializer
- mapper
- response schema
- presenter

Jika ada, gunakan abstraction tersebut.

Jangan membuat serializer kedua.

Jika response masih menggunakan entity mentah dan memang menyebabkan security issue, lakukan perubahan minimal.

15. API SECURITY REGRESSION

Pastikan security checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission
- bot resource authorization
- lifecycle
- input validation
- mass assignment
- abuse boundaries

Jangan melemahkan test existing.

16. TESTING

Tambahkan atau perbaiki test sesuai endpoint yang benar-benar tersedia.

Minimal jika resource tersedia:

User:
- password/hash tidak muncul
- session data tidak muncul

Workspace:
- cross-workspace data tidak muncul
- internal permission metadata tidak bocor

Membership:
- unauthorized membership data tidak muncul
- sensitive membership fields tidak bocor

Bot:
- bot token tidak muncul pada list
- bot token tidak muncul pada detail jika tidak diperlukan
- secret tidak muncul pada error
- unauthorized bot tidak muncul pada list

Child resources:
- unauthorized resource tidak muncul
- secret child configuration tidak bocor

Errors:
- stack trace tidak bocor
- SQL/database detail tidak bocor
- token tidak bocor
- credential tidak bocor

Pagination:
- count/metadata tetap workspace-scoped

17. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada duplicate serializer
- tidak ada duplicate error system
- tidak ada unused import
- tidak ada dead code
- tidak ada circular dependency baru
- tidak ada hardcoded secret

18. BACKWARD COMPATIBILITY

Jangan merusak API existing.

Sebelum mengubah:

- DTO
- response shape
- service signature
- repository signature
- serializer

cari seluruh caller.

Jika perubahan response memang diperlukan karena security, pastikan client/test yang terdampak diperbarui secara aman.

Jangan membuat breaking change tanpa alasan.

19. README

Jika diperlukan, update README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

- API response security
- secret handling
- DTO/serialization
- error security
- test command

20. VERIFICATION

Setelah implementation:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- validation tests
- mass-assignment tests
- abuse/pagination/body-limit tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Pastikan:

- tidak ada regression
- semua security tests PASS
- build PASS

Jika gagal:

1. cari root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.
Jangan menghapus test existing.

21. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- password
- credential
- logs
- temporary files
- build artifacts

22. COMMIT

Jika ada perubahan valid dan seluruh verification PASS:

buat SATU commit.

Gunakan commit message sesuai implementation aktual.

Contoh:

fix: harden api response security

atau:

fix: prevent sensitive api data exposure

Jangan membuat empty commit jika tidak ada perubahan valid.

23. PUSH

Setelah commit:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- reset
- rebase sembarangan
- ubah remote
- merge ke backend-dev

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

Pertahankan commit lokal dan laporkan error sebenarnya.

24. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

Response Security:
- ...

Secret Exposure:
- ...

Error Security:
- ...

Data Isolation:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Mass-assignment: ...
- Abuse: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...
- atau "No new commit — no valid changes"

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum benar-benar berhasil.

25. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya:

AUDIT
→ API RESPONSE SECURITY
→ SECRET EXPOSURE
→ ERROR SECURITY
→ DTO/SERIALIZATION
→ DATA ISOLATION
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan security abstraction yang sudah ada.

Jangan membuat authorization system kedua.

Selesaikan sampai push berhasil jika memang ada perubahan, lalu berhenti.

```
# 
```

PROMPT: BotSpace — API Abuse Protection & Security Boundary Audit

Lanjutkan project BotSpace dari checkpoint TERBARU yang SUDAH BERHASIL secara lokal.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terbaru:
e961be8 — fix: harden api input validation

Verification checkpoint:
- Mass-assignment regression: PASS
- Typecheck: PASS
- pnpm check: 44/44 successful
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- Working tree: clean

PENTING:
Commit e961be8 sudah berhasil dibuat secara lokal.
Push sebelumnya dapat gagal karena credential GitHub:
fatal: could not read Username for 'https://github.com': No such device or address

JANGAN menghapus commit e961be8.
JANGAN reset.
JANGAN force push.
JANGAN rebase sembarangan.
JANGAN checkout branch lain.
JANGAN merge backend-dev-recovery ke backend-dev.

TUJUAN

Lanjutkan security hardening BotSpace dengan fokus pada API ABUSE PROTECTION dan SECURITY BOUNDARY.

Authentication, session security, workspace authorization, membership, ownership, bot resource authorization, bot lifecycle integrity, API input validation, dan mass-assignment protection sudah diperbaiki.

Sekarang audit apakah API yang sudah ada aman terhadap penggunaan berlebihan atau abuse tanpa membuat sistem rate-limit baru yang besar.

Fokus:

AUTHENTICATION
→ AUTHORIZATION
→ INPUT VALIDATION
→ RESOURCE BOUNDARY
→ API ABUSE AUDIT
→ SENSITIVE OPERATION PROTECTION
→ ERROR SECURITY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

1. AUDIT API YANG SUDAH ADA

Baca struktur repository terlebih dahulu.

Cari seluruh:

- API routes
- controllers
- handlers
- services
- authentication endpoints
- session endpoints
- workspace endpoints
- membership endpoints
- bot endpoints
- bot lifecycle endpoints
- credential endpoints
- configuration endpoints
- webhook endpoints jika memang ada
- upload endpoints jika memang ada
- search/list endpoints
- mutation endpoints

Jangan membuat endpoint baru.

Gunakan implementation repository aktual sebagai sumber kebenaran.

2. IDENTIFIKASI OPERASI SENSITIF

Kelompokkan endpoint berdasarkan tingkat sensitivitas.

HIGH RISK jika tersedia:

- login
- session creation
- password/authentication
- credential creation
- credential rotation
- bot token update
- webhook modification
- membership modification
- role modification
- permission modification
- ownership modification
- destructive delete
- bulk operation

MEDIUM RISK:

- create bot
- update bot
- enable/disable bot
- create command
- create flow
- integration changes

LOW RISK:

- read/list operation
- health endpoint
- public metadata

Jangan mengubah behavior hanya berdasarkan asumsi.
Gunakan endpoint yang benar-benar tersedia.

3. RATE LIMIT / THROTTLING AUDIT

Cari apakah repository sudah memiliki:

- rate limiter
- throttle middleware
- request limiter
- abuse protection
- retry protection
- login attempt protection

Jika sudah ada:

- audit penggunaannya
- pastikan protected endpoint menggunakan abstraction yang benar
- pastikan tidak ada bypass sederhana

Jika belum ada:

JANGAN membuat rate-limit framework besar pada tahap ini.

Fokus pada audit dan protection boundary yang sudah tersedia.

4. AUTHENTICATION ABUSE

Audit login/authentication endpoint jika tersedia.

Pastikan:

- invalid authentication tidak membuat session
- malformed authentication tidak membuat session
- failed authentication tidak menghasilkan authenticated context
- session hanya dibuat setelah authentication berhasil
- session tidak dapat dibuat hanya dengan userId
- client tidak dapat memalsukan identity
- error response tidak membocorkan credential

Jangan menambahkan CAPTCHA atau 2FA.

Jangan membuat authentication system baru.

5. SESSION ABUSE

Audit:

- session creation
- session validation
- logout
- revoke
- expiration

Pastikan:

- expired session ditolak
- revoked session ditolak
- malformed session ditolak
- session tidak dapat dipakai untuk impersonation
- logout tidak menghasilkan session baru
- session identifier tidak muncul di log

6. RESOURCE ENUMERATION

Audit endpoint yang menggunakan ID.

Cari kemungkinan enumeration melalui:

- workspaceId
- botId
- memberId
- commandId
- flowId
- integrationId
- credentialId

Pastikan unauthorized user tidak dapat menggunakan response API untuk memetakan resource workspace lain.

Periksa:

- status code
- error body
- response metadata
- existence leakage

Gunakan convention project.

Jangan mengubah semua error menjadi 404 tanpa alasan.

7. LIST ENDPOINT

Audit endpoint list/search.

Pastikan query:

- memiliki workspace boundary
- tidak mengembalikan resource lintas workspace
- tidak mengabaikan membership
- tidak menerima arbitrary userId sebagai authorization source
- pagination tidak dapat melewati security boundary

Jika endpoint menerima:

userId
workspaceId
accountId

pastikan parameter tersebut hanya menjadi filter yang diizinkan, bukan pengganti authenticated identity.

8. PAGINATION

Jika API memiliki pagination:

Audit:

- limit
- offset
- cursor
- page
- sort

Pastikan nilai abnormal tidak menyebabkan:

- memory exhaustion
- query terlalu besar
- database scan tidak terbatas

Gunakan validation yang sudah ada.

Jangan mengubah pagination contract tanpa kebutuhan.

Jika ada default/max limit yang sudah digunakan repository, pertahankan dan perkuat jika memang diperlukan.

9. BULK OPERATION

Cari endpoint yang menerima banyak ID sekaligus.

Contoh:

ids[]
botIds[]
memberIds[]

Pastikan:

- setiap resource tetap di-authorize
- user tidak dapat memasukkan ID workspace lain
- jumlah input divalidasi
- satu resource unauthorized tidak menyebabkan bypass terhadap resource lain

Jangan membuat bulk API baru.

10. DESTRUCTIVE OPERATION

Audit operasi:

- delete
- revoke
- disable
- remove member
- remove integration
- delete credential
- reset configuration

Pastikan:

Authentication
→ Workspace access
→ Permission
→ Resource authorization
→ Mutation

Urutan ini harus dipertahankan.

Jangan melakukan mutation sebelum authorization.

11. REPEATED MUTATION

Audit endpoint yang dapat dipanggil berulang:

- enable
- disable
- revoke
- delete
- rotate credential
- update settings

Pastikan repeated request tidak menghasilkan state korup.

Contoh:

delete → delete

disable → disable

revoke → revoke

Behavior harus mengikuti domain model yang sudah ada.

Jangan membuat state baru hanya untuk task ini.

12. IDEMPOTENCY

Jika repository sudah memiliki abstraction idempotency:

gunakan yang sudah ada.

Jika belum ada:

jangan membuat framework idempotency besar.

Fokus memastikan mutation yang tersedia tidak menghasilkan database corruption ketika request diulang.

Tambahkan regression test jika ditemukan bug nyata.

13. ERROR RESPONSE SECURITY

Audit semua API error.

Pastikan error tidak membocorkan:

- database schema
- SQL query
- stack trace production
- credential
- token
- password
- session data
- workspace data lain
- internal authorization metadata

Gunakan error system yang sudah ada.

Jangan membuat error framework kedua.

14. LOG SECURITY

Audit log/error/debug output.

Pastikan tidak ada:

- password
- API key
- bot token
- session token
- refresh token
- webhook secret
- credential

Jangan menambahkan verbose logging untuk security testing yang membocorkan secret.

15. REQUEST BODY SIZE

Jika repository sudah memiliki body size/configuration limit:

audit dan pastikan digunakan.

Jika belum ada:

jangan membuat perubahan server configuration besar.

Hanya dokumentasikan jika ada risiko nyata yang ditemukan.

16. FILE / UPLOAD ENDPOINT

Jika project memiliki upload endpoint:

audit:

- file size
- file type
- filename
- path handling
- unauthorized workspace access
- arbitrary path
- dangerous extension

Jangan membuat sistem upload baru.

Jika tidak ada upload endpoint, lewati bagian ini.

17. WEBHOOK ENDPOINT

Jika project memiliki webhook:

audit:

- authentication/signature
- replay behavior
- secret handling
- bot ownership
- workspace relation
- malformed payload
- unauthorized source

Jika runtime/webhook implementation belum tersedia, jangan membuat implementation baru.

18. SECURITY REGRESSION

Pastikan semua checkpoint security tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization
- bot lifecycle integrity
- API input validation
- mass-assignment protection

Jangan melemahkan test existing.

19. TESTING

Tambahkan/perbaiki test hanya untuk behavior yang benar-benar tersedia.

Minimal jika endpoint tersedia:

Authentication abuse:
- invalid authentication DENY
- malformed authentication DENY

Session:
- expired session DENY
- revoked session DENY

Enumeration:
- cross-workspace resource access DENY
- unauthorized ID lookup DENY

List:
- cross-workspace resource tidak muncul
- unauthorized filtering DENY

Pagination:
- invalid limit DENY
- excessive limit DENY jika policy memang tersedia

Bulk:
- unauthorized resource DENY
- cross-workspace IDs DENY

Mutation:
- unauthorized delete DENY
- unauthorized disable DENY
- unauthorized revoke DENY

Error security:
- secret tidak bocor
- token tidak bocor
- credential tidak bocor

Jangan membuat test endpoint yang tidak tersedia.

20. TYPESCRIPT QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada duplicate security abstraction
- tidak ada duplicate rate-limit framework
- tidak ada unused import
- tidak ada dead code
- tidak ada circular dependency baru
- tidak ada hardcoded secret

Ikuti architecture repository.

21. BACKWARD COMPATIBILITY

Sebelum mengubah:

- API contract
- DTO
- middleware
- service signature
- repository signature

cari seluruh caller.

Update caller dan test jika memang diperlukan.

Jangan membuat breaking change tanpa alasan.

22. README

Jika memang diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

- API security boundary
- sensitive operation protection
- abuse protection yang benar-benar tersedia
- cara menjalankan security tests

23. VERIFICATION

Setelah implementation:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- input validation tests
- mass-assignment regression
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika failure:

1. cari root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.
Jangan menghapus test existing.

24. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- password
- token
- credential
- logs
- temporary files
- build artifacts

25. COMMIT

Jika ada perubahan valid dan semua verification PASS:

buat SATU commit.

Gunakan commit message sesuai implementasi aktual.

Contoh:

fix: harden api abuse protection

atau:

fix: strengthen api security boundaries

Jika audit tidak menemukan perubahan valid:

JANGAN membuat empty commit.

26. PUSH

Setelah commit baru dibuat:

git push

Branch tetap:

backend-dev-recovery

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

JANGAN reset commit.

Pertahankan commit lokal.

Laporkan error sebenarnya.

Jika push berhasil:

verifikasi:

git status
git log --oneline -3

27. HASIL AKHIR

Tampilkan:

Implementation:
- ...

API Abuse Audit:
- ...

Security:
- ...

Resource Enumeration:
- ...

Mutation Protection:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Mass-assignment: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...
- atau "No new commit — no valid changes"

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum benar-benar berhasil.

28. PENTING

Jangan membuat fitur besar baru.

Jangan membuat rate-limit framework baru jika repository belum memilikinya.

Jangan membuat authentication system baru.

Jangan membuat authorization system kedua.

Tahap ini hanya:

AUDIT
→ API ABUSE PROTECTION
→ RESOURCE ENUMERATION
→ SENSITIVE MUTATION
→ ERROR SECURITY
→ LOG SECURITY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan security abstraction yang sudah ada.

Selesaikan sampai push berhasil jika memang ada perubahan, lalu berhenti.

```
# 
```
PROMPT: BotSpace — API Input Validation & Privilege Escalation Hardening

Kita melanjutkan project BotSpace dari checkpoint yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terakhir:
2947d34 — fix: harden bot lifecycle integrity

Verification terakhir:
- Format check: PASS
- Import boundary check: PASS
- Build: 11 tasks successful
- Runtime/integration/webhook: not applicable, no implementation exists
- Tidak ada perubahan baru yang valid pada tahap runtime/integration/webhook
- Tidak membuat empty commit
- Working tree: clean
- HEAD tetap 2947d34

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

TUJUAN

Lanjutkan BotSpace ke tahap berikutnya dengan fokus pada API INPUT VALIDATION dan PRIVILEGE ESCALATION.

Security sebelumnya sudah mencakup:

- authentication
- session security
- current user identity
- workspace authorization
- workspace membership
- ownership
- permission policy
- bot resource authorization
- bot lifecycle integrity

Sekarang audit seluruh input API untuk memastikan client tidak dapat memalsukan field server-controlled atau menaikkan privilege melalui request body, query, params, atau DTO.

Fokus:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ RESOURCE AUTHORIZATION
→ INPUT VALIDATION
→ MASS ASSIGNMENT PROTECTION
→ PRIVILEGE ESCALATION PROTECTION
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat validation framework baru.
Jangan membuat authorization system kedua.

1. AUDIT INPUT API

Audit seluruh API endpoint yang sudah tersedia.

Cari:

- request body
- query parameters
- route parameters
- DTO
- schema validation
- create input
- update input
- patch input
- workspace input
- bot input
- membership input
- permission input
- role input
- status input
- configuration input

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat endpoint baru.

2. SERVER-CONTROLLED FIELD

Cari field yang seharusnya ditentukan backend, bukan client.

Minimal audit:

- id
- userId
- accountId
- workspaceId
- ownerId
- createdBy
- createdAt
- updatedAt
- role
- permissions
- membershipId
- botId
- status
- credentialId
- integrationId

Pastikan endpoint hanya menerima field yang memang boleh diubah oleh client.

3. MASS ASSIGNMENT

Cari pola seperti:

request.body langsung digunakan untuk create/update

atau:

spread request body

atau:

Object.assign entity dengan input client

atau pola equivalent.

Pastikan client tidak dapat mengirim field privilege tambahan.

Contoh request berbahaya:

workspaceId: workspace-B
ownerId: user-B
role: owner
permissions: ["*"]
createdBy: user-B
accountId: account-B

Backend tidak boleh mempercayai field tersebut hanya karena format request valid.

Gunakan explicit field mapping atau schema yang sudah digunakan repository jika diperlukan.

4. WORKSPACE ID SPOOFING

Test:

Authenticated User A
memiliki workspace-A.

Client mengirim:

workspaceId = workspace-B

Pastikan backend tetap menolak jika User A tidak memiliki akses workspace-B.

Jangan hanya memvalidasi bahwa workspace-B ada.

Authorization harus tetap dilakukan setelah validation.

5. USER ID SPOOFING

Test:

Session user = user-A

Request body:

userId = user-B

Pastikan operasi tetap berjalan atas identity user-A jika memang operasi tersebut menggunakan current user.

Client tidak boleh mengubah authenticated identity melalui request body.

6. ACCOUNT ID SPOOFING

Jika accountId digunakan:

Session:
account-A

Request:
accountId = account-B

Pastikan account-B tidak dapat digunakan untuk mengambil atau mengubah resource account-B tanpa authorization.

Gunakan authentication context dan workspace relationship yang sudah ada.

7. OWNER ID SPOOFING

Cari seluruh create/update endpoint yang menerima ownerId.

Pastikan user tidak dapat:

- menjadi owner resource lain
- mengganti owner secara ilegal
- membuat resource atas nama user lain
- mengubah ownership melalui update biasa

Jika ownership transfer memang belum menjadi fitur resmi, jangan membuat fitur tersebut.

Cegah privilege escalation saja.

8. ROLE SPOOFING

Audit semua input:

role

Jika client mengirim:

role: owner

atau role privilege tinggi lainnya,

backend harus tetap menggunakan policy yang benar.

Pastikan member biasa tidak dapat menaikkan role dirinya sendiri melalui request.

Tambahkan regression test.

9. PERMISSION SPOOFING

Audit input:

permissions

Pastikan client tidak dapat mengirim:

permissions: ["*"]

atau permission tingkat tinggi lainnya untuk menaikkan akses dirinya sendiri.

Permission harus ditentukan berdasarkan policy dan authorization yang sudah ada.

Jangan membuat permission system kedua.

10. STATUS SPOOFING

Audit field:

status

enabled
disabled
active
inactive

dan enum status lain yang benar-benar tersedia.

Pastikan client tidak dapat mengubah status server-controlled melalui endpoint biasa jika status tersebut memang harus diubah melalui operation khusus.

Jangan mengubah business behavior tanpa bukti dari architecture.

11. ID SPOOFING

Audit seluruh endpoint dengan:

:id
:botId
:workspaceId
:memberId
:integrationId
:commandId
:flowId

Pastikan ID hanya digunakan setelah authorization terhadap resource terkait.

Jangan mengandalkan validation sebagai pengganti authorization.

Validation menjawab:

"Apakah format input benar?"

Authorization menjawab:

"Apakah user boleh menggunakan resource ini?"

Keduanya harus tetap terpisah.

12. CREATE INPUT

Audit semua create operation.

Pastikan backend sendiri menentukan:

- owner
- creator
- workspace relation
- account relation
- timestamps
- internal status
- internal metadata

Client hanya boleh menentukan field bisnis yang memang diperbolehkan.

13. UPDATE INPUT

Audit semua update/patch operation.

Pastikan update tidak memungkinkan client mengubah:

- ownership
- workspace
- account
- creator
- privilege
- permission
- role

kecuali fitur tersebut memang secara eksplisit tersedia dan sudah dilindungi authorization.

14. DELETE INPUT

Audit delete endpoint.

Pastikan delete hanya menggunakan identifier yang diperlukan dan authorization tetap dilakukan.

Jangan menerima field privilege tambahan yang tidak diperlukan.

15. API RESPONSE

Audit response DTO.

Pastikan response tidak mengembalikan:

- password
- token
- secret
- credential
- internal permission metadata
- data workspace lain
- data account lain

Gunakan DTO/schema yang sudah ada.

Jangan mengembalikan database object mentah jika menyebabkan secret leakage.

16. VALIDATION ERROR

Pastikan invalid input menghasilkan error sesuai convention project.

Contoh:

invalid ID
→ validation error

invalid enum
→ validation error

invalid permission
→ validation error

unauthorized resource
→ authorization error

resource tidak ada
→ not found sesuai convention

Jangan membocorkan data workspace lain melalui validation/error response.

17. ZOD/SCHEMA/VALIDATOR

Jika repository sudah menggunakan validation library:

gunakan library yang sudah ada.

Audit schema agar:

- unknown privilege fields tidak lolos jika memang harus ditolak
- field server-controlled tidak dapat diubah
- enum valid
- ID valid
- string/number/boolean sesuai type
- required field benar
- optional field benar

Jangan menambahkan validation library baru tanpa kebutuhan.

18. QUERY INPUT

Audit query parameters.

Cari kemungkinan:

?userId=
?accountId=
?workspaceId=
?ownerId=

Pastikan parameter tersebut tidak dapat digunakan untuk mengganti current user atau authorization scope.

Jika query parameter memang diperlukan untuk filtering, pastikan filtering tetap dibatasi oleh authorization.

19. REGRESSION TEST

Tambahkan/perbaiki test untuk:

Authentication:
- unauthenticated request DENY

Identity:
- spoofed userId DENY
- spoofed accountId DENY

Workspace:
- spoofed workspaceId DENY
- cross-workspace resource DENY

Ownership:
- spoofed ownerId DENY
- unauthorized ownership modification DENY

Role:
- self role escalation DENY
- unauthorized role escalation DENY

Permission:
- self permission escalation DENY
- wildcard permission spoof DENY

Mass assignment:
- protected fields tidak dapat diubah
- server-controlled fields tetap berasal dari server

Status:
- unauthorized status mutation DENY

Validation:
- invalid ID
- invalid enum
- malformed body
- unknown/protected field sesuai convention

20. REGRESSION SECURITY

Pastikan semua checkpoint sebelumnya tetap PASS:

- authentication
- session
- workspace authorization
- membership
- ownership
- permission policy
- bot authorization
- bot lifecycle integrity

Jangan melemahkan test existing.

21. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada duplicate validator
- tidak ada duplicate authorization
- tidak ada unused import
- tidak ada dead code
- tidak ada hardcoded secret
- tidak ada circular dependency baru

Ikuti architecture repository.

22. BACKWARD COMPATIBILITY

Sebelum mengubah DTO/schema/function signature:

- cari seluruh caller
- update caller yang relevan
- update test
- jalankan typecheck

Jangan membuat breaking change tanpa alasan.

23. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

- API validation
- protected fields
- authorization boundary
- cara menjalankan test

24. VERIFICATION

Setelah implementation:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- input validation tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika gagal:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

25. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary file
- build artifact

26. COMMIT

Jika ada perubahan valid dan seluruh verification PASS:

buat SATU commit.

Gunakan commit message sesuai perubahan aktual.

Contoh:

fix: harden api input validation

atau:

fix: prevent api privilege escalation

Pilih yang paling sesuai dengan implementation sebenarnya.

Jika audit menemukan tidak ada perubahan valid yang diperlukan:

JANGAN membuat empty commit.

Tetap tampilkan hasil audit dan checkpoint aktif.

27. PUSH

Jika commit baru dibuat:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- ubah remote
- merge ke backend-dev
- reset checkpoint
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code lagi.

Pertahankan commit lokal dan tampilkan error sebenarnya.

28. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

Input Validation:
- ...

Privilege Escalation:
- ...

Mass Assignment:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- Validation: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...
- atau "No new commit — no valid changes"

Git:
- branch: ...
- push: success/failed/not needed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum benar-benar berhasil.

29. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya fokus:

AUDIT
→ API INPUT VALIDATION
→ MASS ASSIGNMENT
→ ID SPOOFING
→ PRIVILEGE ESCALATION
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan security abstraction yang sudah ada.

Jangan membuat authorization system kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil jika memang ada perubahan, lalu berhenti.


```
# 
```
PROMPT: BotSpace — Bot Runtime, Deployment & Integration Security Hardening

Kita melanjutkan project BotSpace dari checkpoint yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

CHECKPOINT TERAKHIR:
2947d34 — fix: harden bot lifecycle integrity

Verification checkpoint terakhir:
- Format check: PASS
- Import boundary check: PASS
- Build: 11 tasks successful
- Working tree: clean
- Commit berhasil dibuat
- Push berhasil

JANGAN melakukan reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

Kita sudah menyelesaikan:
- workspace authorization
- workspace membership
- ownership security
- authentication/session security
- bot resource authorization
- bot lifecycle integrity

SEKARANG lanjutkan ke tahap berikutnya.

TUJUAN

Audit dan harden BOT RUNTIME, BOT DEPLOYMENT, INTEGRATION, WEBHOOK, dan RESOURCE EXECUTION SECURITY berdasarkan arsitektur yang benar-benar sudah tersedia di repository.

Fokus:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ BOT AUTHORIZATION
→ BOT LIFECYCLE
→ BOT RUNTIME
→ INTEGRATION
→ WEBHOOK
→ EXECUTION SECURITY
→ SECRET SECURITY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat authorization system kedua.

Jangan membuat fitur besar baru.

1. AUDIT BOT RUNTIME

Audit seluruh kode yang berhubungan dengan menjalankan bot.

Cari implementasi aktual untuk:

- start bot
- stop bot
- restart bot
- enable bot
- disable bot
- bot worker
- bot process
- bot runtime
- bot executor
- bot scheduler
- bot queue
- bot polling
- webhook listener
- Telegram connection
- runtime status
- health status
- deployment status

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jika fitur tertentu belum ada, jangan membuatnya hanya untuk memenuhi prompt.

2. RUNTIME AUTHORIZATION

Pastikan operasi runtime selalu memverifikasi akses terhadap bot terlebih dahulu.

Operasi seperti:

start
stop
restart
enable
disable

tidak boleh hanya menggunakan botId.

Flow harus:

authenticated user
→ workspace access
→ bot authorization
→ permission check
→ runtime operation

User tidak boleh menjalankan bot workspace lain hanya dengan mengetahui botId.

3. RUNTIME STATE CONSISTENCY

Audit hubungan antara:

database bot status
dan
runtime bot status.

Cari kemungkinan:

database mengatakan active
tetapi runtime tidak berjalan

atau:

database mengatakan inactive
tetapi runtime masih berjalan.

Jangan membuat sistem orchestration baru.

Jika repository sudah memiliki runtime abstraction, gunakan abstraction tersebut.

Tujuan tahap ini adalah menemukan bug nyata dan memastikan state transition tidak menghasilkan state yang menyesatkan.

4. START / STOP SECURITY

Audit seluruh jalur start dan stop.

Pastikan:

- unauthenticated user ditolak
- user workspace lain ditolak
- member tanpa permission ditolak
- authorized user diperbolehkan sesuai policy
- bot yang tidak ada ditangani sesuai convention
- bot yang disabled tidak dapat dijalankan jika architecture memang melarangnya
- bot yang sudah berjalan tidak menghasilkan duplicate runtime jika architecture tidak mengizinkannya

Jangan mengubah behavior bisnis tanpa bukti dari code/test.

5. RESTART SECURITY

Jika restart tersedia:

Pastikan restart tidak menjadi bypass terhadap permission.

Restart harus tetap:

authentication
→ workspace authorization
→ bot authorization
→ permission
→ restart

Jangan menggunakan internal runtime identifier sebagai pengganti authorization.

6. BOT PROCESS ISOLATION

Audit bagaimana runtime menentukan bot yang dijalankan.

Pastikan process/worker tidak dapat dijalankan menggunakan:

- botId workspace lain
- workspaceId palsu
- ownerId palsu
- accountId palsu

Runtime harus mengambil ownership/workspace relationship dari server/database, bukan mempercayai client.

7. WEBHOOK SECURITY

Jika repository memiliki webhook:

Audit:

- webhook creation
- webhook update
- webhook delete
- webhook endpoint
- webhook secret
- webhook configuration
- webhook bot association

Pastikan webhook tidak dapat dipasang ke bot workspace lain.

Jika webhook memiliki secret:

- jangan log secret
- jangan expose secret tanpa alasan
- jangan menyimpan secret di response publik
- jangan mempercayai botId dari payload tanpa validasi

Gunakan webhook security mechanism yang sudah ada.

Jangan membuat webhook architecture baru.

8. WEBHOOK CALLBACK

Jika terdapat callback endpoint dari Telegram atau provider lain:

Audit apakah callback dapat menyebabkan:

- bot action
- command execution
- configuration update
- message processing
- external API call

Pastikan callback hanya diproses untuk bot/integration yang valid.

Jangan menganggap ID dari callback otomatis trusted.

Jika callback memang harus public karena provider membutuhkan endpoint public, authentication user biasa tidak boleh dipaksakan pada callback tersebut.

Sebagai gantinya gunakan mekanisme verifikasi callback yang memang tersedia di architecture, seperti secret/token/signature jika memang sudah digunakan.

Jangan mengarang mekanisme baru tanpa kebutuhan.

9. INTEGRATION SECURITY

Audit seluruh integration yang tersedia.

Contoh jika ada:

- Telegram
- webhook
- external API
- OAuth
- API key
- provider connection
- account integration
- bot credential

Pastikan integration selalu terikat dengan resource yang benar:

User
→ Account
→ Workspace
→ Bot
→ Integration

Jangan sampai integration milik workspace-A dapat dipakai oleh bot workspace-B.

10. CROSS-WORKSPACE INTEGRATION

Buat regression test untuk skenario:

Workspace A:
bot A
integration A

Workspace B:
bot B
integration B

User A tidak boleh menggunakan:

integration B
untuk
bot A

atau:

integration B
untuk
bot B

jika user A tidak memiliki akses workspace B.

Pastikan semua lookup integration melewati authorization boundary.

11. CREDENTIAL SECURITY

Audit semua credential yang digunakan runtime/integration.

Cari:

- bot token
- API key
- webhook secret
- access token
- refresh token
- OAuth credential
- provider credential
- encryption key reference

Pastikan credential:

- tidak dikembalikan dalam list
- tidak masuk response yang tidak perlu
- tidak masuk log
- tidak masuk error
- tidak masuk test output
- tidak dapat diganti oleh user tanpa permission
- tidak dapat digunakan untuk mengambil resource workspace lain

Jangan mengubah secret storage architecture secara besar-besaran.

12. ENVIRONMENT SECURITY

Audit penggunaan environment variables.

Pastikan:

- secret tidak hardcoded
- credential tidak ditulis ke source code
- test tidak membutuhkan production secret
- error tidak mencetak environment variables
- configuration tidak membocorkan secret

Jangan mengubah .env production.

Jangan membuat atau commit credential.

13. BOT COMMAND EXECUTION

Jika bot memiliki command/flow execution:

Audit apakah user dapat memodifikasi command/flow milik bot workspace lain.

Pastikan:

- command read authorized
- command update authorized
- command delete authorized
- flow read authorized
- flow update authorized
- flow delete authorized

Jika command/flow dieksekusi oleh runtime:

pastikan runtime hanya mengambil resource yang memang terkait dengan bot yang sedang dijalankan.

14. RESOURCE RELATION INTEGRITY

Audit relasi:

Bot
→ Workspace
→ Integration
→ Credential
→ Webhook
→ Command
→ Flow
→ Runtime

Cari kemungkinan:

- integration.botId berbeda dengan runtime bot
- integration.workspaceId berbeda dengan bot.workspaceId
- webhook mengarah ke bot lain
- credential digunakan oleh workspace lain
- command berasal dari bot lain
- flow berasal dari bot lain

Jangan memperbaiki production data secara otomatis.

Perbaiki enforcement dan test.

15. IDOR AUDIT

Cari seluruh pola:

findById(id)

findUnique({ id })

findFirst({ id })

where: { id }

dan equivalent lainnya.

Untuk resource runtime/integration:

Pastikan lookup tidak memungkinkan cross-workspace access.

Gunakan workspace/bot scoped query jika repository abstraction mendukungnya.

Jangan mengubah semua query secara otomatis.

Hanya perbaiki yang benar-benar memiliki security boundary issue.

16. MASS ASSIGNMENT

Audit request body untuk runtime/integration resource.

Perhatikan field:

- workspaceId
- botId
- ownerId
- accountId
- integrationId
- credentialId
- webhookId
- status
- role
- permissions

Pastikan client tidak dapat mengubah server-controlled relation.

Gunakan explicit field mapping jika diperlukan.

17. RUNTIME ERROR HANDLING

Pastikan runtime error tidak membocorkan:

- bot token
- API key
- webhook secret
- access token
- refresh token
- database credentials
- internal credential IDs yang sensitif
- stack trace ke client jika production convention melarangnya

Gunakan error system yang sudah ada.

Jangan membuat error system kedua.

18. CONCURRENCY

Audit kemungkinan race condition pada:

start
stop
restart
enable
disable

Contoh:

request A → start
request B → start

Pastikan tidak menghasilkan duplicate worker/process jika architecture melarangnya.

Contoh lain:

request A → disable
request B → start

Pastikan hasil akhir tidak menghasilkan runtime state yang tidak konsisten.

Jika transaction/atomic operation sudah tersedia, gunakan abstraction tersebut.

Jangan membuat concurrency framework baru.

19. TEST MATRIX

Tambahkan/perbaiki test sesuai fitur yang benar-benar tersedia.

Authentication:
- unauthenticated runtime access = DENY

Workspace:
- authorized workspace = PASS
- cross-workspace runtime access = DENY

Bot:
- authorized bot start = PASS
- unauthorized bot start = DENY
- cross-workspace start = DENY
- authorized stop = PASS
- unauthorized stop = DENY
- cross-workspace stop = DENY
- restart authorization = PASS/DENY sesuai permission

Integration:
- authorized integration access = PASS
- cross-workspace integration = DENY
- integration reassignment spoof = DENY

Webhook:
- valid callback = PASS
- invalid callback = DENY
- wrong bot association = DENY
- secret tidak bocor

Credential:
- secret tidak muncul pada response
- secret tidak muncul pada error
- secret tidak muncul pada log/test output

Command/Flow:
- authorized resource access = PASS
- cross-workspace resource access = DENY

20. REGRESSION

Pastikan semua security checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- workspace membership
- ownership
- permission policy
- bot resource authorization
- bot lifecycle integrity

Jangan melemahkan test lama.

21. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate runtime logic
- tidak ada circular dependency baru
- tidak ada hardcoded secret

Ikuti architecture repository.

22. BACKWARD COMPATIBILITY

Sebelum mengubah:

- function signature
- DTO
- route contract
- repository contract
- service contract

cari seluruh caller.

Update caller dan test secara aman.

Jangan membuat breaking change tanpa alasan.

23. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

- bot runtime lifecycle
- runtime authorization
- integration security
- webhook security
- credential handling
- test command

24. VERIFICATION

Setelah implementasi selesai jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- runtime/integration tests jika tersedia
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika gagal:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

25. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary file
- build artifact

26. COMMIT

Jika seluruh verification PASS:

buat SATU commit.

Gunakan commit message berdasarkan perubahan aktual.

Contoh:

fix: harden bot runtime security

atau:

fix: secure bot runtime integrations

Pilih message yang paling sesuai dengan implementation sebenarnya.

Setelah commit:

git status
git log --oneline -3

27. PUSH

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- ubah remote
- merge ke backend-dev
- reset checkpoint
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code lagi.

Pertahankan commit lokal dan tampilkan error sebenarnya.

28. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

Runtime:
- ...

Integration:
- ...

Webhook:
- ...

Credential Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Runtime/Integration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum berhasil.

29. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya fokus:

AUDIT
→ BOT RUNTIME
→ START/STOP/RESTART SECURITY
→ INTEGRATION ISOLATION
→ WEBHOOK SECURITY
→ CREDENTIAL SECURITY
→ COMMAND/FLOW EXECUTION SECURITY
→ CONCURRENCY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan abstraction security yang sudah ada.

Jangan membuat authorization system kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil lalu berhenti.


```
# 
```
PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint security terakhir yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terakhir:
28d9438 — fix: secure bot resource authorization

Verification checkpoint terakhir:
- Format check: PASS
- Import boundary check: PASS
- Build: 11 tasks successful
- Working tree: clean
- Commit lokal aman
- Push dapat gagal hanya jika credential GitHub bermasalah

JANGAN reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

TUJUAN

Lanjutkan BotSpace ke tahap berikutnya dengan fokus pada BOT LIFECYCLE dan RESOURCE INTEGRITY.

Authentication, session security, workspace authorization, membership, ownership, permission policy, dan bot resource authorization sudah diperbaiki.

Sekarang pastikan lifecycle bot tidak dapat menghasilkan state atau relasi database yang tidak valid.

Fokus:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ BOT AUTHORIZATION
→ BOT LIFECYCLE
→ RESOURCE INTEGRITY
→ STATE TRANSITION
→ DATABASE CONSISTENCY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat authorization system baru.

1. AUDIT BOT LIFECYCLE

Audit implementasi bot yang sudah tersedia.

Cari seluruh operasi:

- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot
- bot status
- bot configuration
- bot credentials
- bot settings
- bot commands
- bot flows
- bot integrations
- bot webhook
- resource lain yang memiliki botId

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat endpoint baru hanya untuk task ini.

2. BOT STATE

Identifikasi state bot yang benar-benar digunakan repository.

Contoh jika memang tersedia:

- active
- inactive
- disabled
- pending
- stopped
- deleted

Jangan membuat state baru jika belum ada di architecture.

Audit seluruh transisi state.

Pastikan state transition hanya dapat dilakukan oleh user yang memiliki permission yang sesuai.

3. STATE TRANSITION SECURITY

Pastikan operasi seperti:

enable
disable
activate
deactivate
start
stop

tidak dapat dilakukan pada bot workspace lain.

Pastikan authorization dilakukan sebelum mutation.

User tidak boleh mengubah state hanya dengan mengetahui botId.

4. INVALID STATE TRANSITION

Cari kemungkinan transisi yang tidak valid berdasarkan state machine yang sebenarnya.

Contoh:

bot sudah deleted
→ enable

bot sudah deleted
→ update

bot sudah deleted
→ disable

Jika repository memang memiliki konsep deleted state, pastikan behavior sesuai architecture.

Jangan mengubah behavior tanpa bukti dari code dan test.

Jika tidak ada state machine formal, jangan membuat state machine baru hanya untuk terlihat lebih kompleks.

5. BOT CREATION INTEGRITY

Audit create bot.

Pastikan bot baru:

- memiliki workspace yang valid
- dibuat oleh authenticated user
- user memiliki akses ke workspace
- owner/membership relation benar
- tidak dapat dibuat menggunakan workspaceId milik workspace lain
- tidak menerima ownerId palsu dari client
- tidak menerima accountId palsu dari client

Server harus menentukan ownership berdasarkan authentication context dan workspace authorization.

6. BOT UPDATE INTEGRITY

Audit seluruh field update.

Pisahkan:

CLIENT-CONTROLLED FIELD
dan
SERVER-CONTROLLED FIELD

Periksa khusus:

- id
- workspaceId
- ownerId
- accountId
- createdBy
- createdAt
- updatedAt
- status
- role
- permissions
- credential identifiers

Jangan mengizinkan update biasa mengubah ownership atau workspace assignment jika architecture tidak mendukungnya.

Gunakan explicit field mapping jika diperlukan.

7. DELETE INTEGRITY

Audit delete bot.

Pastikan:

- authorization dilakukan sebelum delete
- user tidak dapat delete bot workspace lain
- member tanpa permission delete ditolak
- bot yang tidak ada ditangani dengan error convention
- child resource tidak menjadi orphan secara tidak sengaja

Jika project menggunakan soft delete, pertahankan behavior tersebut.

Jika project menggunakan hard delete, audit dependency terlebih dahulu.

Jangan mengubah soft delete menjadi hard delete atau sebaliknya tanpa alasan.

8. CHILD RESOURCE INTEGRITY

Audit resource yang bergantung pada bot.

Contoh jika tersedia:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- credentials
- analytics
- configuration

Pastikan child resource tidak dapat tetap digunakan melalui ID setelah parent bot tidak lagi dapat diakses.

Periksa juga kemungkinan orphan resource.

Jangan melakukan cascade delete besar-besaran jika database relation saat ini tidak mendukungnya.

9. CROSS-WORKSPACE RELATION

Pastikan semua relasi berikut konsisten:

User
→ Account
→ Telegram Account
→ Workspace
→ Bot
→ Bot Resource

Cari kemungkinan resource memiliki:

- workspaceId berbeda dari bot.workspaceId
- ownerId berbeda dari creator yang seharusnya
- accountId berbeda dari workspace account
- botId yang tidak valid
- parent resource yang sudah tidak ada

Jangan memperbaiki data production secara otomatis.

Fokus pada enforcement dan test.

10. DATABASE CONSTRAINT / REPOSITORY

Audit repository method yang membuat atau mengubah bot.

Periksa:

- create
- update
- delete
- status update
- child resource creation

Pastikan repository/service tidak dapat membuat relasi invalid hanya karena input client.

Jika database constraint sudah tersedia, gunakan sesuai architecture.

Jika constraint tidak tersedia tetapi bug nyata ditemukan, evaluasi perubahan minimal.

Jangan membuat migration besar tanpa kebutuhan.

11. CONCURRENCY

Audit mutation yang berpotensi dipanggil bersamaan.

Contoh:

request A:
enable bot

request B:
disable bot

Pastikan hasil akhir tidak menghasilkan state korup atau behavior yang tidak konsisten.

Jika transaction atau atomic update sudah tersedia, gunakan abstraction existing.

Jangan membuat concurrency framework baru.

12. DUPLICATE RESOURCE

Periksa apakah bot dapat dibuat duplicate secara tidak sengaja jika architecture memiliki unique constraint atau business rule tertentu.

Cari:

- duplicate bot identifier
- duplicate Telegram bot token
- duplicate external identifier
- duplicate workspace resource

Hanya enforce rule yang memang sudah tersirat dalam architecture.

Jangan menciptakan business rule baru tanpa bukti.

13. CREDENTIAL INTEGRITY

Audit bot credential handling.

Pastikan:

- credential tidak digunakan untuk menentukan ownership
- credential tidak mengubah workspace
- credential tidak muncul dalam list response
- credential tidak masuk log
- credential tidak masuk error
- credential tidak dapat diganti oleh user tanpa permission
- credential update tetap berada pada bot/workspace yang benar

Jangan menampilkan secret dalam test output.

14. API INPUT VALIDATION

Audit input pada seluruh lifecycle endpoint.

Validasi:

- botId
- workspaceId
- status
- configuration
- settings
- commandId
- flowId
- integrationId
- webhookId

Gunakan schema validation yang sudah ada.

Jangan membuat validation framework baru.

15. ERROR HANDLING

Gunakan error system yang sudah ada.

Pastikan:

unauthenticated
→ authentication error

authenticated tetapi tidak punya akses
→ authorization error

resource tidak ada
→ not found sesuai convention

invalid state
→ validation/domain error sesuai convention

Jangan membocorkan detail resource workspace lain.

16. TEST MATRIX

Tambahkan/perbaiki test sesuai resource yang benar-benar tersedia.

Create:
- authenticated + valid workspace = PASS
- unauthenticated = DENY
- wrong workspace = DENY
- spoofed ownerId = DENY
- spoofed accountId = DENY

Read:
- own bot = PASS
- other workspace bot = DENY

Update:
- authorized update = PASS
- unauthorized update = DENY
- workspaceId spoof = DENY
- ownerId spoof = DENY
- permission spoof = DENY

Delete:
- authorized delete = PASS
- unauthorized delete = DENY
- cross-workspace delete = DENY

Status:
- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY
- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY

Child resources:
- authorized child access = PASS
- cross-workspace child access = DENY
- invalid parent relation = DENY

Credential:
- secret tidak muncul pada response yang tidak seharusnya
- secret tidak muncul pada error
- secret tidak muncul pada log/test output

17. REGRESSION

Pastikan seluruh security checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization

Jangan melemahkan test lama.

18. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate bot lifecycle logic
- tidak ada circular dependency baru
- tidak ada hardcoded secret

Ikuti architecture repository.

19. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

- bot lifecycle
- bot status
- authorization
- resource integrity
- test command

20. VERIFICATION

Setelah implementasi jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika gagal:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

21. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary file
- build artifact

22. COMMIT

Jika seluruh verification PASS:

buat SATU commit.

Gunakan commit message sesuai perubahan sebenarnya.

Contoh:

fix: harden bot lifecycle integrity

atau:

fix: enforce bot lifecycle security

Pilih yang paling sesuai dengan implementation aktual.

Setelah commit:

git status
git log --oneline -3

23. PUSH

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- ubah remote
- merge ke backend-dev
- reset checkpoint
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code lagi.

Pertahankan commit lokal dan laporkan error sebenarnya.

24. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

Bot Lifecycle:
- ...

Resource Integrity:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification, commit, atau push belum berhasil.

25. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya fokus:

AUDIT
→ BOT LIFECYCLE
→ STATE INTEGRITY
→ OWNERSHIP INTEGRITY
→ WORKSPACE RELATION
→ CHILD RESOURCE INTEGRITY
→ CREDENTIAL SECURITY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan abstraction security yang sudah ada.

Jangan membuat authorization system kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil lalu berhenti.


```
# 
```
PROMPT: BotSpace — API Security & Bot Resource Authorization

Kita melanjutkan project BotSpace setelah checkpoint Authentication & Session Security.

CHECKPOINT TERAKHIR

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint sebelumnya:
e28105b — fix: secure workspace membership access

Checkpoint terbaru:
f6b1ab1 — fix: harden authentication and session security

Verification sebelumnya:

* Format check: PASS
* Import boundary check: PASS
* Build: 11 tasks successful
* Working tree: clean
* Commit berhasil dibuat
* Push mungkin perlu dilakukan jika belum berhasil

JANGAN reset, force push, rebase sembarangan, checkout branch lain, atau menghapus checkpoint yang sudah ada.

Jangan merge backend-dev-recovery ke backend-dev.

TUJUAN

Setelah workspace authorization, membership, ownership, authentication, dan session security diperbaiki, tahap berikutnya adalah memastikan seluruh BOT RESOURCE dan API RESOURCE benar-benar mengikuti security boundary tersebut.

Fokus utama:

AUTHENTICATION
→ CURRENT USER
→ WORKSPACE ACCESS
→ BOT OWNERSHIP/MEMBERSHIP
→ RESOURCE AUTHORIZATION
→ API SECURITY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat sistem authorization kedua.

1. AUDIT SELURUH BOT RESOURCE

Audit seluruh implementasi bot yang sudah ada.

Cari:

* Bot entity/model
* Bot repository
* Bot service
* Bot API routes
* bot creation
* bot listing
* bot detail
* bot update
* bot delete
* bot enable
* bot disable
* bot status
* bot configuration
* bot token/credential handling
* bot logs
* bot statistics
* bot settings
* bot integrations
* bot templates
* bot commands
* bot flow
* semua resource yang memiliki botId

Pahami hubungan:

User
→ Workspace
→ Bot
→ Bot Resource

Jangan mengubah arsitektur yang sudah benar.

2. BOT WORKSPACE BOUNDARY

Setiap bot harus memiliki workspace yang jelas.

Pastikan:

* bot hanya dapat diakses oleh user yang memiliki akses ke workspace bot
* bot tidak dapat dipindahkan secara ilegal ke workspace lain
* botId dari request tidak boleh melewati workspace authorization
* user tidak boleh mengambil bot workspace lain hanya karena mengetahui botId

Test:

User A:
workspace-A
bot-A

User B:
workspace-B
bot-B

User A:

GET bot-A = ALLOW
UPDATE bot-A = ALLOW
DELETE bot-A = ALLOW sesuai permission

GET bot-B = DENY
UPDATE bot-B = DENY
DELETE bot-B = DENY

3. BOT CREATION

Audit create bot.

Pastikan user tidak dapat membuat bot atas nama workspace yang tidak dapat dia akses.

Request seperti:

workspaceId = workspace-B

harus tetap diverifikasi berdasarkan authenticated user.

Jangan hanya memvalidasi bahwa workspaceId valid.

Pastikan:

Authentication
→ workspace access
→ create bot
→ assign workspaceId

4. BOT UPDATE

Audit seluruh field yang dapat diubah.

Perhatikan terutama:

* workspaceId
* ownerId
* bot status
* bot token
* bot configuration
* permissions
* integrations
* webhook
* commands

User yang hanya memiliki permission mengelola bot tidak boleh otomatis dapat mengubah ownership atau workspace assignment jika permission tersebut tidak diberikan oleh policy.

Jangan mempercayai:

ownerId
workspaceId
role
permissions

dari request body sebagai authorization source.

5. BOT DELETE

Pastikan delete bot membutuhkan authorization terhadap workspace bot.

Test:

* owner dapat delete jika policy mengizinkan
* member dengan permission delete dapat delete
* member tanpa permission ditolak
* user workspace lain ditolak
* unauthenticated ditolak
* nonexistent bot ditangani sesuai error convention

Jangan melakukan deletion sebelum authorization selesai.

6. BOT ENABLE / DISABLE

Audit endpoint atau service untuk:

* enable bot
* disable bot
* toggle bot status

Pastikan status change tidak dapat digunakan untuk mengakses atau memodifikasi bot workspace lain.

Test:

* authorized user → allowed
* unauthorized member → denied
* cross-workspace user → denied
* unauthenticated → denied

7. BOT TOKEN DAN SECRET

Audit semua penyimpanan dan response bot credential.

Cari:

* bot token
* Telegram token
* webhook secret
* API key
* integration secret
* access token
* refresh token

Pastikan secret tidak:

* dikembalikan dalam list bot
* dikembalikan dalam response detail tanpa alasan
* dicetak ke log
* masuk ke error message
* dimasukkan ke analytics
* dimasukkan ke audit log secara plaintext

Jika secret memang perlu ditampilkan sekali saat creation, ikuti behavior yang sudah ada.

Jangan mengubah secret architecture secara besar-besaran tanpa kebutuhan.

8. BOT LISTING

Audit endpoint list bots.

Pastikan query tidak mengembalikan semua bot kemudian hanya menyembunyikan bot pada response.

Jika repository memungkinkan workspace-scoped query, gunakan scope tersebut.

User hanya boleh mendapatkan:

* bot workspace yang dapat dia akses

Bukan:

* seluruh bot database

Test bahwa user A tidak menerima bot workspace B dalam list response.

9. BOT DETAIL

Audit get bot.

Pastikan:

botId
→ resolve bot
→ resolve workspace
→ verify access
→ return resource

Jangan:

botId
→ return resource

tanpa authorization.

10. BOT RESOURCE TURUNAN

Cari semua resource yang memiliki hubungan dengan bot:

* bot settings
* commands
* flows
* templates
* logs
* statistics
* analytics
* webhook
* integrations
* credentials
* API configuration
* deployment configuration

Semua resource tersebut harus mewarisi security boundary bot/workspace.

Jika user tidak memiliki akses ke bot, user juga tidak boleh mengakses resource turunannya hanya dengan mengetahui child resource ID.

Contoh:

User A tidak boleh:

GET /flows/flow-B

jika flow-B milik bot-B di workspace-B.

11. RESOURCE IDOR AUDIT

Cari pola:

findById(id)

findUnique({ id })

where: { id }

atau equivalent lainnya.

Untuk setiap resource workspace/bot:

tentukan apakah authorization sudah dilakukan setelah lookup atau query sudah workspace-scoped.

Jangan melakukan perubahan query secara membabi buta.

Gunakan abstraction repository yang sudah ada.

Prioritas:

* correctness
* security
* minimal change

12. API ROUTE AUDIT

Audit semua protected API route.

Pastikan tidak ada route yang:

* lupa authentication
* lupa workspace authorization
* lupa membership check
* lupa permission check
* mempercayai userId dari request
* mempercayai workspaceId dari request
* mempercayai ownerId dari request

Buat daftar internal route yang diaudit dan perbaiki yang memang bermasalah.

Tidak perlu menambahkan endpoint baru.

13. API INPUT VALIDATION

Audit input bot/resource.

Pastikan:

* ID divalidasi sesuai schema
* enum divalidasi
* status divalidasi
* workspaceId divalidasi
* botId divalidasi
* body tidak dapat memasukkan field privilege yang seharusnya server-controlled

Jika schema validation library sudah tersedia, gunakan yang sudah ada.

Jangan membuat validation framework baru.

14. MASS ASSIGNMENT / PRIVILEGE ESCALATION

Cari request body yang memungkinkan user mengubah field sensitif sekaligus.

Contoh berbahaya:

{
workspaceId,
ownerId,
role,
permissions,
status
}

Pastikan hanya field yang memang boleh diubah oleh endpoint yang diproses.

Field server-controlled harus diabaikan atau ditolak sesuai convention project.

Minimal audit:

* workspaceId
* ownerId
* userId
* permissions
* role
* createdBy
* accountId

15. BOT OWNERSHIP TRANSFER

Jangan menambahkan fitur transfer ownership.

Tetapi pastikan endpoint update biasa tidak dapat digunakan untuk melakukan transfer ownership secara diam-diam.

Jika bot tidak boleh berpindah workspace melalui update biasa:

* cegah perubahan workspaceId
* gunakan policy yang sesuai
* tambahkan regression test

16. API RESPONSE SECURITY

Audit response DTO/schema.

Pastikan response tidak membocorkan:

* internal database IDs jika tidak diperlukan
* password
* token
* secret
* credential
* internal authorization metadata
* workspace/resource milik user lain

Gunakan DTO yang sudah ada jika tersedia.

Jangan mengembalikan object database mentah jika itu menyebabkan secret leakage.

17. ERROR SECURITY

Pastikan error tidak membocorkan:

* SQL/database detail
* secret
* token
* credential
* resource milik workspace lain
* internal stack trace pada production response

Ikuti error handling yang sudah ada.

Jangan membuat error system kedua.

18. TESTING WAJIB

Tambahkan atau perbaiki test minimal:

Authentication:

* unauthenticated bot access DENY

Workspace:

* authorized workspace access PASS
* cross-workspace access DENY

Bot:

* own bot GET PASS
* own bot UPDATE PASS
* own bot DELETE PASS sesuai permission
* other workspace bot GET DENY
* other workspace bot UPDATE DENY
* other workspace bot DELETE DENY

Bot status:

* authorized enable PASS
* unauthorized enable DENY
* cross-workspace enable DENY
* authorized disable PASS
* unauthorized disable DENY

Bot list:

* hanya bot yang boleh diakses yang muncul
* bot workspace lain tidak muncul

Child resources:

* unauthorized flow DENY
* unauthorized command DENY
* unauthorized log DENY
* unauthorized integration DENY
* sesuai resource yang memang tersedia di project

Privilege escalation:

* workspaceId spoof DENY
* ownerId spoof DENY
* userId spoof DENY
* role spoof DENY
* permissions spoof DENY

Secret:

* bot token tidak muncul pada list
* bot token tidak bocor pada response yang tidak seharusnya
* credential tidak masuk log/error

Sesuaikan dengan API dan resource yang benar-benar ada.

Jangan membuat test untuk endpoint yang tidak tersedia.

19. REGRESSION TEST

Pastikan perubahan tidak merusak:

* workspace authorization
* workspace membership
* ownership
* authentication
* session security
* permission policy

Semua test lama harus tetap berjalan.

20. TYPESCRIPT QUALITY

Pastikan:

* tidak menambahkan any tanpa alasan
* tidak menambahkan @ts-ignore
* tidak ada duplicate authorization logic
* tidak ada duplicate validation system
* tidak ada unused import
* tidak ada dead code
* tidak ada circular dependency baru
* tidak ada hardcoded secret
* mengikuti struktur repository

21. BACKWARD COMPATIBILITY

Jangan merusak API existing.

Sebelum mengubah:

* function signature
* DTO
* route contract
* repository contract
* service contract

cari seluruh caller dan update secara aman.

Jangan membuat breaking change tanpa alasan.

22. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

* bot workspace isolation
* bot authorization
* resource security
* credential handling
* test command

23. VERIFICATION

Setelah implementation:

jalankan verification resmi repository.

Minimal:

* domain tests
* API tests
* auth/session tests
* workspace authorization tests
* membership tests
* bot/resource tests
* typecheck
* format check
* import boundary check
* lint jika tersedia
* build

Pastikan semua PASS.

Jika ada failure:

* identifikasi root cause
* perbaiki
* ulangi test terkait
* ulangi full verification

Jangan skip test.

Jangan menghapus test existing.

24. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan yang berkaitan dengan task.

Jangan commit:

* .env
* credential
* secret
* temporary files
* logs
* build artifacts

25. COMMIT

Jika seluruh verification PASS:

buat SATU commit.

Gunakan commit message berdasarkan perubahan sebenarnya.

Contoh:

fix: secure bot resource authorization

atau:

fix: enforce bot workspace isolation

Pilih message yang paling sesuai dengan implementation aktual.

Setelah commit:

git status
git log --oneline -3

26. PUSH

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan force push.

Jangan mengubah remote.

Jangan merge ke backend-dev.

Jika push gagal karena credential GitHub, jangan melakukan perubahan lain.

Commit lokal harus tetap dipertahankan.

27. HASIL AKHIR

Tampilkan laporan:

Implementation:

* ...

Bot Security:

* ...

Workspace Isolation:

* ...

Secret Security:

* ...

Tests:

* Domain: ...
* API: ...
* Auth/Session: ...
* Workspace: ...
* Membership: ...
* Bot: ...
* Typecheck: ...
* Format: ...
* Import boundary: ...
* Build: ...

Commit:

* hash: ...
* message: ...

Git:

* branch: ...
* push: success/failed

Working Tree:

* clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika verification belum selesai.

28. PENTING

Jangan membuat fitur baru yang besar.

Tahap ini hanya fokus memastikan seluruh BOT RESOURCE dan API RESOURCE mengikuti security boundary yang sudah dibangun.

Alur:

AUDIT
→ AUTHENTICATION
→ WORKSPACE ACCESS
→ MEMBERSHIP/PERMISSION
→ BOT AUTHORIZATION
→ CHILD RESOURCE AUTHORIZATION
→ SECRET SECURITY
→ IDOR TEST
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Selesaikan sampai push berhasil lalu berhenti.



```

# 
```
PROMPT: BotSpace — Authentication & Session Security Hardening

Kita melanjutkan project BotSpace setelah checkpoint WORKSPACE MEMBERSHIP dan OWNERSHIP yang sudah selesai.

CHECKPOINT TERAKHIR

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint sebelumnya:
c4c66ff — fix: enforce workspace authorization

Checkpoint terbaru:
e28105b — fix: secure workspace membership access

Verification sebelumnya:

* pnpm check: 44 tasks successful
* Format check: PASS
* Import boundary check: PASS
* Working tree: clean
* Push checkpoint terbaru sudah dilakukan sebelum melanjutkan tahap ini

JANGAN reset, force push, rebase sembarangan, checkout branch lain, atau menghapus checkpoint yang sudah ada.

Jangan merge backend-dev-recovery ke backend-dev.

TUJUAN

Tahap berikutnya fokus pada AUTHENTICATION dan SESSION SECURITY BotSpace.

Workspace authorization dan membership authorization sudah diperbaiki. Sekarang pastikan identitas user yang masuk ke backend benar-benar tervalidasi dan session/authentication flow tidak dapat digunakan untuk melewati workspace permission.

Fokus:

Authentication
→ Session
→ Current User
→ Account Identity
→ Authorization
→ Workspace Membership
→ Resource Access

Jangan membuat authentication system kedua jika project sudah memiliki implementasinya.

1. AUDIT AUTHENTICATION YANG SUDAH ADA

Sebelum mengubah kode, audit repository secara menyeluruh.

Cari:

* authentication API
* login
* logout
* session
* session token
* current user
* current account
* user identity
* authentication middleware
* authorization middleware
* password handling jika ada
* token handling jika ada
* cookie handling jika ada
* API authentication
* protected routes
* public routes
* session repository
* user repository
* account repository
* authentication tests
* session tests

Baca implementasi aktual repository sebelum melakukan perubahan.

Jangan membuat sistem auth baru hanya karena menemukan struktur yang belum sempurna.

2. AUTHENTICATION BOUNDARY

Pastikan endpoint yang membutuhkan login benar-benar protected.

Audit seluruh API route dan tandai:

PUBLIC:

* endpoint yang memang harus bisa diakses tanpa login

PROTECTED:

* endpoint yang membutuhkan authenticated user

Pastikan protected endpoint tidak dapat dipanggil hanya dengan:

* workspaceId
* userId
* accountId
* botId
* membershipId

tanpa authentication context yang valid.

Jangan mempercayai userId/accountId dari request body sebagai identitas user yang sedang login.

Identitas user harus berasal dari authentication/session context.

3. CURRENT USER

Pastikan backend memiliki cara yang konsisten untuk menentukan current user.

Jangan menggunakan pola berbahaya seperti:

userId dari body
userId dari query
userId dari URL

sebagai sumber utama identitas authenticated user jika session/auth context sudah tersedia.

Jika request memiliki:

userId = user-A

tetapi session sebenarnya milik user-B,

backend harus tetap memperlakukan request sebagai user-B dan tidak boleh memberikan akses user-A.

Tambahkan regression test untuk kasus ini.

4. SESSION SECURITY

Audit lifecycle session:

* create session
* validate session
* retrieve current user
* expire session
* logout
* revoke session
* invalid session
* expired session
* malformed session
* repeated logout

Pastikan session yang expired tidak dapat digunakan.

Pastikan session yang sudah direvoke tidak dapat digunakan.

Jika project memang mendukung multiple sessions, pastikan logout behavior mengikuti arsitektur yang sudah ada.

Jangan mengubah semantics logout tanpa alasan.

5. SESSION OWNERSHIP

Pastikan session selalu terkait dengan identity yang benar.

Contoh:

User A login.

Session A dibuat.

User A tidak boleh dapat menggunakan session tersebut untuk mengambil data User B.

Test minimal:

* session A → user A
* session B → user B
* session A tidak dapat impersonate user B
* invalid session ditolak
* expired session ditolak
* revoked session ditolak

6. SESSION TOKEN HANDLING

Audit bagaimana token/session identifier disimpan dan dibandingkan.

Pastikan:

* tidak ada token plaintext yang tidak diperlukan di database
* tidak ada logging token rahasia
* tidak ada token yang dikirim dalam response secara tidak perlu
* comparison mengikuti mekanisme yang sudah digunakan project
* session expiration benar-benar diperiksa
* revoked session benar-benar diperiksa

Jangan mengganti hashing/token architecture secara besar-besaran jika sistem yang ada sudah benar.

Perbaiki hanya kelemahan nyata yang ditemukan.

7. COOKIE / HEADER SECURITY

Jika authentication menggunakan cookie:

Audit:

* HttpOnly
* Secure
* SameSite
* expiration/max-age
* domain/path
* session clearing saat logout

Jika authentication menggunakan Authorization header/token:

Audit:

* format token
* validation
* expiration
* invalid token behavior
* token leakage melalui log/error

Gunakan pendekatan yang sesuai dengan implementasi repository.

Jangan memaksakan cookie jika project menggunakan bearer token atau sebaliknya.

8. AUTHENTICATION VS AUTHORIZATION

Pastikan boundary jelas.

Authentication menjawab:

"Siapa user ini?"

Authorization menjawab:

"Apakah user ini boleh melakukan operasi tersebut?"

Flow harus konsisten:

Authentication
→ resolve identity
→ resolve workspace
→ membership/ownership
→ permission
→ operation

Jangan menggunakan permission check untuk menggantikan authentication.

Jangan menggunakan userId dari request untuk menggantikan authentication.

9. WORKSPACE SECURITY REGRESSION

Karena authentication menjadi dasar authorization, tambahkan regression test gabungan:

User A login
→ akses workspace A = allowed

User A login
→ akses workspace B = denied

User B login
→ akses workspace B = allowed

User B login
→ akses workspace A = denied

Pastikan hasilnya tidak berubah setelah authentication hardening.

10. IDENTITY SPOOFING TEST

Buat test untuk request yang mencoba memalsukan:

* userId
* accountId
* workspaceId
* ownerId
* membership userId

Authentication context harus selalu menjadi sumber identity.

Contoh:

Session:
user-A

Request:
userId=user-B

Hasil:
authorization harus tetap menggunakan user-A.

Jangan mengizinkan request body mengubah identity authenticated user.

11. LOGIN FLOW

Jika login flow sudah tersedia, audit:

* valid credential
* invalid credential
* missing credential
* malformed credential
* repeated invalid authentication
* inactive/disabled account jika konsep tersebut ada
* session creation
* current-user resolution

Jangan menambahkan CAPTCHA, 2FA, rate limiting, atau fitur besar lain jika belum ada dalam architecture project.

Fokus pada correctness dan security dari sistem yang sudah ada.

12. LOGOUT FLOW

Pastikan logout:

* invalidates/revokes session sesuai architecture
* tidak meninggalkan session aktif secara tidak sengaja
* tidak membocorkan session information
* dapat menangani session yang sudah expired/revoked dengan behavior yang konsisten

Tambahkan test logout jika belum ada.

13. API ERROR BEHAVIOR

Pastikan authentication failure tidak membocorkan informasi sensitif.

Contoh jangan membedakan secara berlebihan:

user tidak ada

versus

password salah

jika convention security project memang menggunakan generic authentication failure.

Ikuti error system yang sudah ada.

Jangan membuat error system kedua.

14. AUTH MIDDLEWARE / SERVICE

Jika project memiliki authentication middleware/service:

* gunakan satu abstraction utama
* jangan membuat middleware duplicate
* jangan membuat current-user resolver duplicate
* jangan menyebarkan parsing token ke setiap endpoint

Jika logic authentication tersebar dan dapat dipusatkan tanpa breaking change, refactor secara aman.

15. DATABASE / REPOSITORY

Audit query authentication/session.

Cari:

* session lookup
* user lookup
* account lookup
* session deletion
* session revocation
* expiration filtering

Pastikan query session tidak mengembalikan session yang sudah expired/revoked jika architecture mengharuskan filtering di repository.

Jangan mengubah schema database kecuali memang diperlukan.

Jika migration benar-benar diperlukan:

* buat migration aman
* jangan menghapus data
* jangan menyentuh production database
* test migration
* dokumentasikan perubahan

16. TESTING

Tambahkan atau perbaiki test minimal untuk:

Authentication:

* valid authentication PASS
* invalid authentication DENY
* missing authentication DENY
* malformed authentication DENY

Session:

* valid session PASS
* expired session DENY
* revoked session DENY
* invalid session DENY
* logout invalidates session

Identity:

* current user berasal dari auth context
* spoofed userId DENY
* spoofed accountId DENY
* user A tidak menjadi user B

Authorization regression:

* user A → workspace A PASS
* user A → workspace B DENY
* user B → workspace B PASS
* user B → workspace A DENY

Resource regression:

* authenticated user dapat mengakses resource miliknya
* authenticated user tidak dapat mengakses resource workspace lain

17. TEST EXISTING SUITE

Jangan menghapus atau melemahkan test yang sudah ada.

Jalankan test existing sebelum dan sesudah perubahan jika memungkinkan.

Jika test gagal:

* identifikasi root cause
* perbaiki implementation
* jalankan ulang test
* jangan skip test
* jangan mengubah expected result hanya agar test PASS kecuali behavior memang sengaja berubah dan alasannya valid

18. TYPESCRIPT QUALITY

Pastikan:

* tidak menambahkan any tanpa alasan
* tidak menambahkan @ts-ignore
* tidak ada unused import
* tidak ada dead code
* tidak ada duplicate authentication logic
* tidak ada duplicate session system
* tidak ada circular dependency baru
* tidak ada secret/token yang hardcoded
* mengikuti struktur package repository

19. SECURITY LOGGING

Audit log/error output.

Jangan mencetak:

* password
* session token
* access token
* refresh token
* secret
* credential

Jika terdapat logging sensitif, hapus atau sanitasi.

Jangan menambahkan verbose authentication logging yang dapat membocorkan credential.

20. BACKWARD COMPATIBILITY

Jangan merusak API existing.

Sebelum mengubah:

* function signature
* middleware contract
* session structure
* authentication response

cari seluruh caller.

Update caller dan test yang diperlukan.

Jangan membuat breaking change tanpa alasan yang jelas.

21. README

Jika diperlukan, update README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

* authentication flow
* session behavior
* protected API
* logout/session invalidation
* cara menjalankan authentication test

Jangan menulis dokumentasi panjang yang tidak diperlukan.

22. VERIFICATION

Setelah implementation selesai jalankan:

* domain tests
* API tests
* authentication tests
* session tests
* typecheck
* format check
* import boundary check
* lint jika tersedia
* build semua package yang tersedia

Pastikan tidak ada regression pada:

* workspace authorization
* workspace membership
* ownership
* permission policy

Jika repository memiliki command khusus untuk verification, gunakan command resmi repository.

23. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan yang berkaitan dengan authentication/session security.

Jangan commit file:

* .env
* secret
* credential
* temporary files
* log files
* build artifacts

24. COMMIT

Jika seluruh verification PASS:

buat SATU commit baru.

Gunakan commit message sesuai perubahan sebenarnya.

Contoh:

fix: harden authentication and session security

atau:

feat: secure authentication session flow

Pilih message berdasarkan implementasi aktual.

Setelah commit:

git status
git log --oneline -3

25. PUSH

Setelah commit:

git push

Branch tetap:

backend-dev-recovery

Jangan mengubah remote.

Jangan force push.

Jangan merge ke backend-dev.

26. HASIL AKHIR

Setelah selesai tampilkan laporan:

Implementation:

* ...

Authentication:

* ...

Session:

* ...

Security:

* ...

Regression:

* Workspace authorization: ...
* Membership authorization: ...
* Ownership: ...

Tests:

* Domain: ...
* API: ...
* Auth: ...
* Session: ...
* Typecheck: ...
* Format: ...
* Import boundary: ...
* Build: ...

Commit:

* hash: ...
* message: ...

Git:

* branch: ...
* push: success/failed

Working Tree:

* clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika test, build, commit, atau push belum berhasil.

27. PENTING

Jangan membuat fitur besar baru.

Tahap ini hanya fokus pada:

AUTHENTICATION
→ SESSION
→ CURRENT USER
→ IDENTITY SECURITY
→ AUTHORIZATION REGRESSION
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Pastikan authentication menjadi fondasi yang aman untuk workspace authorization dan membership yang sudah selesai.

Selesaikan sampai push berhasil lalu berhenti.



```

# 
```


PROMPT: BotSpace — Workspace Membership & Ownership Enforcement

Kita melanjutkan project BotSpace setelah checkpoint authorization terakhir yang SUDAH BERHASIL.

Kondisi saat ini:

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git
Checkpoint terakhir yang sudah dipush: c4c66ff
Commit: fix: enforce workspace authorization

Verification sebelumnya:

* Build: 11 packages successful
* pnpm check: 44 tasks successful
* Format check: PASS
* Import boundary check: PASS
* Working tree: clean
* Push: berhasil

JANGAN reset, force push, rebase sembarangan, checkout branch lain, atau menghapus checkpoint c4c66ff.

TUJUAN

Lanjutkan BotSpace ke tahap berikutnya dengan fokus pada WORKSPACE MEMBERSHIP dan OWNERSHIP.

Permission policy sudah diperbaiki pada tahap sebelumnya. Sekarang pastikan model membership workspace benar-benar aman dan konsisten sehingga akses workspace tidak hanya bergantung pada owner/user ID sederhana.

Arsitektur yang harus dipertahankan:

* satu account website dapat memiliki beberapa Telegram account/workspace
* setiap Telegram account memiliki workspace sendiri
* bot dibuat di dalam workspace
* workspace memiliki owner/membership
* akses resource mengikuti membership dan permission
* backend adalah sumber kebenaran authorization
* frontend tidak boleh menjadi security boundary

1. AUDIT TERLEBIH DAHULU

Sebelum mengubah kode, audit implementasi yang sudah ada.

Cari:

* Workspace entity/model
* Workspace repository
* Workspace service
* Workspace API routes
* Workspace membership
* Workspace owner
* user/account relationship
* bot → workspace relationship
* permission policy
* authorization middleware/service
* database schema dan migration terkait workspace
* test workspace yang sudah ada

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat sistem membership baru jika repository sudah memilikinya.

2. TENTUKAN MODEL AKSES YANG SUDAH ADA

Pahami apakah project saat ini menggunakan:

* ownerId
* userId
* accountId
* membership table
* workspace members
* roles
* permission
* kombinasi beberapa mekanisme tersebut

Jangan mengganti model yang sudah benar.

Jika membership sudah ada tetapi enforcement belum lengkap, perbaiki enforcement.

Jika owner adalah special membership, pastikan behavior tersebut konsisten.

3. WORKSPACE OWNER

Pastikan owner workspace memiliki akses sesuai permission yang memang dimaksudkan oleh arsitektur.

Minimal audit:

* owner dapat melihat workspace
* owner dapat mengubah workspace
* owner dapat mengelola resource workspace
* owner dapat mengelola membership jika fitur tersebut memang tersedia
* owner tidak dapat kehilangan akses secara tidak sengaja
* owner tidak dapat dihapus dari workspace dengan cara yang membuat workspace kehilangan owner, kecuali arsitektur memang secara eksplisit mendukung transfer ownership

Jangan menambahkan transfer ownership jika fitur tersebut belum menjadi bagian scope.

4. WORKSPACE MEMBER

Jika project mendukung membership:

Pastikan member hanya mendapatkan akses sesuai permission/role mereka.

Test minimal:

* member dengan permission valid dapat melakukan operasi yang diizinkan
* member tanpa permission ditolak
* member tidak dapat mengakses workspace lain
* member tidak dapat mengubah permission dirinya sendiri tanpa hak yang sesuai
* member tidak dapat mengubah owner workspace tanpa authorization

Jangan memberikan akses penuh kepada semua member hanya karena mereka terdaftar dalam workspace.

5. CROSS-WORKSPACE ISOLATION

Pastikan membership Workspace A tidak memberikan akses ke Workspace B.

Test skenario:

User A:
workspace-A

User B:
workspace-B

User A tidak boleh:

* membaca workspace-B
* membaca member workspace-B
* menambah/menghapus member workspace-B
* mengubah role workspace-B
* mengubah bot workspace-B
* menghapus resource workspace-B

meskipun ID workspace atau resource diketahui.

6. MEMBERSHIP API

Audit endpoint yang berkaitan dengan membership.

Jika endpoint tersedia, periksa:

* list members
* get member
* add member
* remove member
* update member role
* update member permission
* leave workspace

Pastikan setiap endpoint melakukan authorization terhadap workspace yang benar.

Jangan membuat endpoint baru jika fitur tersebut belum ada.

Jika endpoint belum tersedia tetapi domain/service sudah mendukung membership, jangan memperluas scope menjadi pembuatan UI/API baru tanpa kebutuhan.

Fokus pada security dan correctness dari implementasi yang sudah ada.

7. SELF-MODIFICATION

Periksa apakah user dapat memodifikasi membership dirinya sendiri.

Contoh yang harus diperhatikan:

* member menaikkan role dirinya sendiri
* member memberikan permission tambahan kepada dirinya sendiri
* member menghapus restriction dirinya sendiri
* member mengubah ownerId

Semua harus ditolak jika user tidak memiliki permission yang sesuai.

Jangan mempercayai role atau permission dari request body.

Contoh request berbahaya:

role: owner

atau:

permissions: ["*"]

Backend harus menentukan authorization berdasarkan data yang tersimpan dan policy yang sebenarnya.

8. OWNER PROTECTION

Pastikan operasi membership tidak dapat menghasilkan workspace tanpa owner.

Test minimal:

* tidak dapat menghapus satu-satunya owner tanpa replacement mechanism yang memang sudah tersedia
* member biasa tidak dapat menghapus owner
* member biasa tidak dapat mengganti owner
* user dari workspace lain tidak dapat memodifikasi owner

Jangan membuat mekanisme transfer ownership baru pada task ini.

Jika behavior yang dibutuhkan belum didukung arsitektur, dokumentasikan sebagai limitation daripada membuat fitur besar di luar scope.

9. AUTHORIZATION ORDER

Pastikan urutan pemeriksaan aman:

Authentication
→ resolve current user/account
→ resolve workspace
→ verify membership/ownership
→ verify permission
→ execute operation

Jangan melakukan mutation terlebih dahulu baru memeriksa permission.

Jangan mengambil resource workspace lain lalu menggunakan data tersebut untuk menentukan authorization jika pola repository memungkinkan query langsung dengan workspace scope.

10. DATABASE / REPOSITORY SAFETY

Audit query membership dan workspace.

Cari pola seperti:

findById(id)

atau query berdasarkan ID saja pada resource yang seharusnya workspace-scoped.

Jika repository mendukung:

* workspaceId
* userId
* membershipId

gunakan scope tersebut dengan benar.

Jangan mengubah database schema kecuali memang diperlukan untuk memperbaiki bug nyata yang ditemukan.

Jika migration benar-benar diperlukan:

* buat migration yang aman
* jangan menghapus data
* jangan mengubah production database
* test migration
* dokumentasikan perubahan

11. TESTING

Tambahkan atau perbaiki test untuk:

Workspace owner:

* owner access PASS
* owner mutation PASS
* owner protection PASS

Workspace member:

* valid member access PASS
* unauthorized member access DENY
* insufficient permission DENY

Cross workspace:

* read DENY
* update DENY
* delete DENY
* membership modification DENY

Self escalation:

* role escalation DENY
* permission escalation DENY
* ownership modification DENY

Invalid membership:

* nonexistent member
* nonexistent workspace
* duplicate membership
* membership dari workspace lain

Sesuaikan test dengan behavior yang memang tersedia di repository.

Jangan membuat test untuk endpoint yang tidak ada.

12. ERROR HANDLING

Gunakan error system yang sudah ada.

Pastikan:

* unauthenticated → authentication error sesuai convention
* authenticated tetapi bukan member → authorization error sesuai convention
* member tetapi tidak memiliki permission → authorization error sesuai convention
* resource benar-benar tidak ada → not found sesuai convention

Jangan membocorkan informasi membership workspace lain.

13. BACKWARD COMPATIBILITY

Jangan merusak API yang sudah bekerja.

Sebelum mengubah function signature:

* cari semua caller
* update caller
* update unit test
* update integration/API test
* jalankan typecheck

Jangan membuat breaking change tanpa alasan.

14. CODE QUALITY

Pastikan:

* tidak ada any baru tanpa alasan
* tidak ada @ts-ignore baru
* tidak ada duplicate authorization logic
* tidak ada duplicate membership system
* tidak ada unused import
* tidak ada dead code
* tidak ada circular dependency baru
* mengikuti struktur package yang sudah ada

Gunakan abstraction authorization yang dibuat pada commit c4c66ff jika memang sesuai.

Jangan membuat permission system kedua.

15. VERIFICATION

Setelah implementasi:

jalankan test yang tersedia.

Minimal:

* domain tests
* API tests
* typecheck
* lint jika tersedia
* build jika tersedia

Jika ada failure:

* cari root cause
* perbaiki
* ulangi test
* ulangi full verification

Jangan skip test.

Jangan menghapus test existing.

16. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan hanya hal penting:

* workspace owner
* workspace membership
* authorization
* role/permission behavior
* test command

17. GIT

Setelah verification PASS:

jalankan:

git status
git diff --stat
git diff

Pastikan tidak ada perubahan di luar scope.

Buat SATU commit baru.

Gunakan commit message berdasarkan perubahan sebenarnya.

Contoh:

feat: enforce workspace membership authorization

atau:

fix: secure workspace membership access

Setelah commit:

git status
git log --oneline -3

Kemudian:

git push

Branch tetap:

backend-dev-recovery

Jangan mengubah remote.

18. JANGAN MERGE

Jangan merge backend-dev-recovery ke backend-dev.

Jangan melakukan merge otomatis.

Hanya:

AUDIT
→ IMPLEMENT
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Setelah push berhasil, berhenti.

19. LAPORAN AKHIR

Tampilkan:

Implementation:

* ...

Membership:

* ...

Security:

* ...

Tests:

* Domain: ...
* API: ...
* Typecheck: ...
* Lint: ...
* Build: ...

Commit:

* hash: ...
* message: ...

Git:

* branch: ...
* push: success/failed

Working tree:

* clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim sukses jika test, build, commit, atau push belum berhasil.

20. PENTING

Jangan membuat fitur besar baru.

Fokus tahap ini:

WORKSPACE
→ OWNER
→ MEMBERSHIP
→ ROLE/PERMISSION
→ AUTHORIZATION
→ CROSS-WORKSPACE ISOLATION
→ TEST
→ COMMIT
→ PUSH

Tujuan akhirnya adalah memastikan setiap workspace memiliki boundary akses yang benar dan tidak ada user yang dapat menaikkan hak aksesnya sendiri atau mengakses workspace lain.

Selesaikan sampai push berhasil lalu berhenti.

```
# Prompt: BotSpace — Workspace Permission Policy Completion & Full Verification
```
PROMPT: BotSpace — Workspace Permission Policy Completion & Full Verification

Kita melanjutkan project BotSpace dari checkpoint yang SUDAH BERHASIL di GitHub.

Kondisi saat ini:

Repository: /root/botspace
Branch aktif: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git
Checkpoint terakhir: c5db8fb
Commit: feat: add workspace permission policy

Status:

* working tree clean
* branch backend-dev-recovery sudah tracking origin/backend-dev-recovery
* commit sudah berhasil dipush ke GitHub
* Domain tests: 95 passed
* API tests: 74 passed

JANGAN melakukan reset, force push, rebase sembarangan, checkout branch lain, atau menghapus checkpoint tersebut.

TUJUAN

Lanjutkan pengembangan BotSpace dari checkpoint c5db8fb.

Fokus utama tahap ini adalah memastikan Workspace Permission Policy benar-benar terimplementasi dan digunakan secara konsisten di backend, bukan hanya didefinisikan di satu file.

Arsitektur BotSpace:

* satu user/account website dapat memiliki beberapa Telegram account/workspace
* setiap Telegram account memiliki workspace sendiri
* bot dibuat dan dikelola di dalam workspace yang dipilih
* resource workspace tidak boleh dapat diakses oleh workspace lain
* permission harus ditegakkan di backend/domain/service layer
* frontend bukan sumber kebenaran authorization

Jangan membuat ulang arsitektur yang sudah ada. Ikuti struktur repository saat ini.

1. AUDIT KODE TERLEBIH DAHULU

Sebelum mengubah kode:

* baca struktur repository
* baca README.md
* baca packages/domain
* baca services/api
* baca service/API yang berkaitan dengan workspace
* baca permission policy yang dibuat pada checkpoint terakhir
* cari seluruh penggunaan workspace
* cari workspaceId
* cari userId
* cari accountId
* cari bot ownership
* cari permissions
* cari authorization
* cari membership
* cari role
* pahami flow request dari API → service → domain → repository

Jangan langsung menulis kode sebelum memahami implementasi yang sudah ada.

2. AUDIT FILE CHECKPOINT TERAKHIR

Periksa minimal:

* packages/domain/src/errors.ts
* packages/domain/src/errors.test.ts
* packages/domain/src/permissions.ts
* packages/domain/src/permissions.test.ts
* services/api/src/errors.ts
* services/api/src/errors.test.ts

Jika struktur repository berbeda, gunakan file aktual sebagai sumber kebenaran.

Jangan menghapus logic yang sudah benar.

3. PASTIKAN PERMISSION POLICY BENAR-BENAR DIGUNAKAN

Cari seluruh endpoint/API/service yang bekerja dengan resource workspace.

Pastikan setiap operasi sensitif memverifikasi authorization sebelum operasi dilakukan.

Minimal audit:

* create workspace
* list workspace
* get workspace
* update workspace
* delete workspace
* workspace membership
* bot creation
* bot listing
* bot detail
* bot update
* bot delete
* bot enable
* bot disable
* resource lain yang memiliki hubungan dengan workspace

Prinsip utama:

User hanya boleh mengakses resource yang memang menjadi miliknya atau workspace yang memang menjadi hak aksesnya.

Jangan hanya mempercayai workspaceId yang dikirim dari request tanpa memverifikasi bahwa user/session memang memiliki akses ke workspace tersebut.

4. WORKSPACE ISOLATION

Pastikan tidak terjadi IDOR atau cross-workspace access.

Contoh:

User A memiliki workspace-A.
User B memiliki workspace-B.

Jika User A mencoba:

GET /workspaces/workspace-B

request harus ditolak.

User A juga tidak boleh:

GET bot milik workspace-B
UPDATE bot milik workspace-B
DELETE bot milik workspace-B
ENABLE bot milik workspace-B
DISABLE bot milik workspace-B

meskipun User A mengetahui ID resource tersebut.

Buat test untuk memastikan cross-workspace access benar-benar ditolak.

5. JANGAN HANYA MEMPERBAIKI FRONTEND

Authorization wajib ditegakkan di backend/domain/service layer.

Frontend boleh menyembunyikan menu yang tidak boleh digunakan, tetapi backend tetap wajib memverifikasi authorization.

Jangan membuat solusi yang hanya berupa:

if (!showButton) ...

atau validasi frontend.

Backend harus menjadi sumber kebenaran authorization.

6. GUNAKAN POLICY YANG SUDAH ADA

Jika packages/domain/src/permissions.ts sudah menyediakan abstraction/policy:

* gunakan abstraction tersebut
* jangan membuat sistem permission kedua
* jangan membuat role system baru tanpa kebutuhan
* jangan hardcode permission di banyak endpoint
* refactor logic authorization yang tersebar agar menggunakan policy yang sama jika aman dilakukan

Tujuannya adalah satu sumber kebenaran untuk permission.

7. ERROR HANDLING

Gunakan error type yang sudah ada.

Pastikan behavior authorization konsisten.

Bedakan:

* authentication gagal / user tidak login
* authorization gagal / user login tetapi tidak memiliki akses
* resource tidak ditemukan
* validation error

Jangan membocorkan detail resource milik workspace lain.

Jika user mencoba mengakses resource yang bukan miliknya, response tidak boleh membocorkan informasi internal resource tersebut secara tidak perlu.

Ikuti convention error project yang sudah ada.

8. TESTING WAJIB DIPERKUAT

Tambahkan atau perbaiki test sesuai kebutuhan.

Workspace:

* owner dapat mengakses workspace sendiri
* user tanpa akses ditolak
* workspace lain tidak dapat diakses
* invalid workspace ditangani dengan benar

Bot:

* user dapat mengakses bot dalam workspace yang dimiliki
* user tidak dapat mengakses bot workspace lain
* update cross-workspace ditolak
* delete cross-workspace ditolak
* enable cross-workspace ditolak
* disable cross-workspace ditolak

Permission:

* permission valid diterima
* permission tidak valid ditolak
* role/permission mapping konsisten
* policy tidak menghasilkan false positive authorization

API:

Tambahkan integration/API test jika architecture repository memang menggunakannya.

Jangan membuat test palsu yang hanya memanggil function tanpa benar-benar memverifikasi authorization behavior.

9. SECURITY AUDIT

Cari pola berbahaya seperti:

findById(id)

yang langsung mengambil resource tanpa memverifikasi ownership/workspace access.

Cari juga query seperti:

where: { id }

yang mungkin perlu dibatasi dengan workspaceId atau authorization policy.

Contoh konsep:

where:

* id
* workspaceId

Namun jangan mengubah query secara membabi buta. Ikuti repository abstraction dan arsitektur yang sudah ada.

Audit seluruh jalur resource yang berkaitan dengan workspace.

10. BACKWARD COMPATIBILITY

Jangan merusak API yang sudah bekerja.

Sebelum mengubah signature function/service:

* cari seluruh caller
* update caller yang relevan
* update test
* pastikan TypeScript build tetap lolos

Jangan membuat breaking change tanpa alasan yang jelas.

11. TYPESCRIPT QUALITY

Pastikan:

* tidak menambahkan any tanpa alasan
* tidak menambahkan @ts-ignore
* tidak meninggalkan TODO security
* tidak ada dead code
* tidak ada duplicate permission system
* tidak ada unused import
* tidak ada circular dependency baru
* mengikuti coding style repository

12. VERIFICATION

Setelah implementasi selesai jalankan verification yang tersedia.

Minimal:

* domain tests
* API tests
* typecheck
* lint jika tersedia
* build jika tersedia

Jika test gagal:

1. cari root cause
2. perbaiki
3. jalankan ulang test terkait
4. jalankan full verification kembali

Jangan skip test hanya supaya hasil terlihat PASS.

Jangan menghapus test existing.

13. JANGAN MENYENTUH DI LUAR SCOPE

Jangan mengubah:

* production deployment
* VPS configuration
* DNS
* Cloudflare
* secret/API key
* .env production
* credential GitHub
* production database

kecuali perubahan source code memang membutuhkan sesuatu yang relevan.

Fokus pada source code BotSpace.

14. README.md

Jika permission implementation membutuhkan dokumentasi:

UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

* konsep workspace permission
* authorization rule
* workspace isolation
* cara menjalankan test terkait

Jangan membuat dokumentasi panjang yang tidak diperlukan.

15. GIT DISCIPLINE

Setelah implementasi selesai jalankan:

git status
git diff --stat
git diff

Pastikan hanya perubahan yang berhubungan dengan task ini.

Kemudian jalankan verification terakhir.

Jika semuanya PASS:

buat SATU commit baru.

Gunakan commit message yang sesuai dengan perubahan, misalnya:

feat: enforce workspace authorization

atau jika lebih tepat:

fix: enforce workspace authorization

Pilih message berdasarkan perubahan sebenarnya.

Setelah commit:

git status
git log --oneline -3

Kemudian push:

git push

Branch sudah tracking:

origin/backend-dev-recovery

Jangan mengubah remote.

16. JANGAN MERGE

Jangan merge backend-dev-recovery ke backend-dev.

Jangan membuat merge otomatis.

Alurnya hanya:

AUDIT
→ IMPLEMENT
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Setelah push berhasil, berhenti.

17. LAPORAN AKHIR

Setelah selesai tampilkan laporan:

Implementation:

* perubahan yang dilakukan

Security:

* authorization yang diperbaiki
* cross-workspace protection

Tests:

* Domain: hasil
* API: hasil
* Typecheck: hasil
* Lint: hasil jika tersedia
* Build: hasil

Commit:

* hash
* message

Git:

* branch
* push: success/failed

Working tree:

* clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim berhasil jika verification atau push belum berhasil.

18. PENTING

Jangan hanya membuat permission policy terlihat bagus di code.

Tujuan utama adalah memastikan authorization benar-benar enforced pada jalur backend yang menggunakan workspace dan seluruh resource yang berhubungan dengan workspace.

Prioritas:

security
→ correctness
→ tests
→ maintainability
→ documentation

Jangan mengejar fitur baru di luar scope.

Selesaikan seluruh proses sampai:

AUDIT
→ IMPLEMENT
→ TEST
→ BUILD
→ COMMIT
→ PUSH

dan berhenti setelah push berhasil.



```
# Prompt: BotSpace — Workspace Permission Policy Completion & Full Verification
```

# Prompt: BotSpace — Workspace Permission Policy Completion & Full Verification

Kita melanjutkan project **BotSpace** dari checkpoint yang SUDAH BERHASIL di GitHub.

## Kondisi saat ini

Repository:
`/root/botspace`

Branch aktif:
`backend-dev-recovery`

Remote:
`https://github.com/zenolamee/botspace.git`

Checkpoint terakhir yang sudah berhasil dipush:
`c5db8fb`

Commit message:
`feat: add workspace permission policy`

Status terakhir:

* working tree clean
* branch `backend-dev-recovery` sudah tracking `origin/backend-dev-recovery`
* commit lokal sudah berhasil dipush
* GitHub menerima branch `backend-dev-recovery`
* Domain tests: 95 passed
* API tests: 74 passed

JANGAN melakukan reset, force push, rebase sembarangan, checkout branch lain, atau menghapus commit checkpoint tersebut.

---

# TUJUAN

Lanjutkan pengembangan BotSpace dari checkpoint `c5db8fb`.

Fokus utama tahap ini adalah memastikan **Workspace Permission Policy benar-benar terimplementasi secara konsisten**, bukan hanya definisi/type/policy di satu tempat.

BotSpace menggunakan konsep:

* satu user/account website dapat memiliki beberapa Telegram account/workspace
* setiap Telegram account memiliki workspace sendiri
* bot dibuat dan dikelola di dalam workspace yang dipilih
* resource workspace tidak boleh dapat diakses oleh workspace lain
* permission harus menjadi bagian dari arsitektur backend, bukan hanya validasi frontend

Jangan membuat ulang arsitektur yang sudah ada. Ikuti struktur repository yang sekarang.

---

# ATURAN PENTING

## 1. Audit kode terlebih dahulu

Sebelum mengubah kode:

* baca struktur repository
* baca `README.md`
* baca package/domain yang relevan
* baca service/API yang berkaitan dengan workspace
* baca file permission yang sudah dibuat pada commit terakhir
* cari seluruh penggunaan:

  * workspace
  * workspaceId
  * userId
  * accountId
  * bot ownership
  * permissions
  * authorization
  * membership
  * role
* pahami flow request dari API sampai domain/service/repository

Jangan langsung menulis kode sebelum memahami implementasi yang sudah ada.

---

# 2. Periksa file yang berubah pada checkpoint terakhir

Audit minimal file berikut:

* `packages/domain/src/errors.ts`
* `packages/domain/src/errors.test.ts`
* `packages/domain/src/permissions.ts`
* `packages/domain/src/permissions.test.ts`
* `services/api/src/errors.ts`
* `services/api/src/errors.test.ts`

Jangan menghapus logic yang sudah benar.

Jika struktur saat ini berbeda, gunakan file aktual repository sebagai sumber kebenaran.

---

# 3. Pastikan permission policy benar-benar digunakan

Cari semua endpoint/API/service yang bekerja dengan resource workspace.

Pastikan setiap operasi sensitif memverifikasi authorization sebelum melakukan operasi.

Minimal periksa:

* create workspace
* list workspace
* get workspace
* update workspace
* delete workspace
* workspace membership
* bot creation
* bot listing
* bot detail
* bot update
* bot delete
* bot enable/disable
* resource lain yang memiliki hubungan dengan workspace

Prinsip utama:

**User hanya boleh mengakses resource yang memang menjadi miliknya atau workspace yang memang menjadi hak aksesnya.**

Jangan hanya mengandalkan:

```text
workspaceId dari request
```

Tanpa memastikan user/session memang memiliki akses ke workspace tersebut.

---

# 4. Workspace isolation

Pastikan tidak terjadi IDOR / cross-workspace access.

Contoh kasus yang WAJIB ditolak:

User A memiliki:

```text
workspace-A
```

User B memiliki:

```text
workspace-B
```

Jika User A mencoba:

```text
GET /workspaces/workspace-B
```

request harus ditolak.

Hal yang sama berlaku untuk bot/resource:

User A tidak boleh:

```text
GET bot milik workspace-B
UPDATE bot milik workspace-B
DELETE bot milik workspace-B
ENABLE bot milik workspace-B
DISABLE bot milik workspace-B
```

meskipun User A mengetahui ID resource tersebut.

---

# 5. Jangan hanya memperbaiki frontend

Permission wajib ditegakkan di backend/domain/service layer.

Frontend boleh menyembunyikan menu yang tidak boleh digunakan, tetapi security decision harus tetap dilakukan backend.

Jangan membuat implementasi yang hanya:

```text
if (!showButton) ...
```

atau validasi frontend.

Backend harus menjadi sumber kebenaran authorization.

---

# 6. Gunakan policy yang sudah ada

Jika `packages/domain/src/permissions.ts` sudah menyediakan abstraction/policy tertentu:

* gunakan abstraction tersebut
* jangan membuat sistem permission kedua yang duplikat
* jangan membuat role system baru tanpa kebutuhan
* jangan hardcode permission di banyak endpoint

Jika ada logic authorization yang tersebar dan bisa menggunakan policy yang sudah ada, refactor secara aman agar konsisten.

---

# 7. Error handling

Gunakan error type yang sudah ada.

Pastikan unauthorized access memiliki behavior yang konsisten.

Bedakan secara benar antara:

* authentication gagal / user tidak login
* authorization gagal / user login tetapi tidak punya akses
* resource tidak ditemukan
* validation error

Jangan membocorkan informasi sensitif tentang resource milik workspace lain.

Contoh yang perlu diperhatikan:

Jika user tidak memiliki akses ke resource:

```text
workspace-B
```

jangan memberikan response yang secara tidak perlu membocorkan detail internal resource tersebut.

Ikuti convention error yang sudah digunakan project.

---

# 8. Testing wajib diperkuat

Tambahkan atau perbaiki test yang diperlukan.

Minimal coverage:

### Workspace

* owner dapat mengakses workspace sendiri
* user tanpa akses ditolak
* workspace lain tidak dapat diakses
* invalid workspace ditangani dengan benar

### Bot

* user dapat mengakses bot dalam workspace yang dimiliki
* user tidak dapat mengakses bot workspace lain
* update cross-workspace ditolak
* delete cross-workspace ditolak
* enable/disable cross-workspace ditolak

### Permission

* permission yang valid diterima
* permission yang tidak valid ditolak
* role/permission mapping konsisten
* policy tidak menghasilkan false positive authorization

### API

Tambahkan integration/API test jika architecture repository memang menggunakannya.

Jangan membuat test palsu yang hanya memanggil function tanpa benar-benar memverifikasi authorization behavior.

---

# 9. Security test

Cari pola berbahaya seperti:

```text
findById(id)
```

yang langsung mengembalikan resource tanpa memverifikasi ownership/workspace access.

Cari juga pola:

```text
where: { id }
```

yang seharusnya mungkin:

```text
where: {
  id,
  workspaceId
}
```

atau harus melewati authorization policy/service.

Jangan mengubah query secara membabi buta. Pastikan perubahan sesuai dengan repository abstraction yang digunakan project.

Audit seluruh jalur yang relevan.

---

# 10. Backward compatibility

Jangan merusak API yang sudah bekerja.

Sebelum mengubah signature function/service:

* cari semua caller
* update seluruh caller yang relevan
* update test
* pastikan TypeScript build tetap lolos

Jangan membuat breaking change tanpa alasan yang jelas.

---

# 11. TypeScript quality

Pastikan:

* tidak ada `any` baru tanpa alasan
* tidak ada `@ts-ignore` baru
* tidak ada TODO security yang dibiarkan
* tidak ada dead code
* tidak ada duplicate permission system
* tidak ada import yang tidak digunakan
* tidak ada circular dependency baru

Ikuti coding style repository.

---

# 12. Jalankan verification

Setelah implementasi selesai, jalankan test/build yang memang tersedia di repository.

Minimal:

* domain tests
* API tests
* typecheck
* lint jika tersedia
* build jika tersedia

Jika ada test failure:

1. identifikasi root cause
2. perbaiki
3. jalankan ulang test terkait
4. jalankan full verification kembali

Jangan mematikan atau skip test hanya supaya CI hijau.

Jangan menghapus test existing.

---

# 13. Jangan menyentuh hal di luar scope

Jangan melakukan perubahan terhadap:

* deployment production
* VPS configuration
* DNS
* Cloudflare
* secret/API key
* `.env` production
* credential GitHub
* database production

kecuali repository memang membutuhkan perubahan kode yang jelas terkait task ini.

Fokus pada source code BotSpace.

---

# 14. README.md

Jika implementation atau workflow permission membutuhkan dokumentasi:

UPDATE `README.md` yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

* konsep workspace permission
* authorization rule
* bagaimana workspace isolation bekerja
* cara menjalankan test terkait

Jangan menulis dokumentasi panjang yang tidak diperlukan.

---

# 15. Git discipline

Setelah semua perubahan selesai:

Jalankan:

```bash
git status
git diff --stat
git diff
```

Pastikan hanya perubahan yang berhubungan dengan task ini.

Kemudian jalankan verification terakhir.

Jika semuanya PASS:

buat SATU commit baru.

Gunakan commit message yang jelas, misalnya:

```text
feat: enforce workspace authorization
```

Jika implementasi lebih cocok dengan `fix`, gunakan:

```text
fix: enforce workspace authorization
```

Pilih message berdasarkan perubahan sebenarnya.

Setelah commit berhasil:

```bash
git status
git log --oneline -3
```

Lalu push:

```bash
git push
```

Karena branch sudah tracking:

```text
origin/backend-dev-recovery
```

tidak perlu mengubah remote.

---

# 16. Jangan merge

Jangan merge:

```text
backend-dev-recovery
```

ke:

```text
backend-dev
```

Jangan membuat Pull Request merge otomatis.

Kita hanya perlu:

```text
implement
→ test
→ commit
→ push
```

Setelah itu berhenti.

---

# 17. Hasil akhir yang wajib dilaporkan

Setelah selesai, tampilkan laporan ringkas:

```text
Implementation:
- ...

Security:
- ...

Tests:
- Domain: ...
- API: ...
- Typecheck: ...
- Build: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working tree:
- clean/dirty
```

Jika ada failure, JANGAN menyembunyikannya.

Tampilkan error sebenarnya dan jangan mengklaim berhasil jika verification belum selesai.

---

# 18. PENTING

Jangan hanya membuat permission policy terlihat bagus secara code.

Tujuan utama task ini adalah:

**memastikan authorization benar-benar enforced pada jalur backend yang menggunakan workspace dan resource workspace.**

Prioritaskan:

```text
security
→ correctness
→ tests
→ maintainability
→ documentation
```

Jangan mengejar banyak fitur baru.

Selesaikan scope ini sampai:

```text
AUDIT
→ IMPLEMENT
→ TEST
→ BUILD
→ COMMIT
→ PUSH
```

dan berhenti setelah push berhasil.


```
# Prompt: Commit & Recovery Safety
```

Sebelum mengerjakan task coding berikutnya, terapkan aturan wajib repository:

1. SETIAP task yang selesai dan sudah tervalidasi WAJIB langsung dibuatkan git commit.
2. Jangan menunggu task berikutnya untuk commit.
3. Jangan melakukan reset, rebase, squash, amend, force-push, atau menghapus commit existing kecuali saya minta secara eksplisit.
4. Commit harus dibuat setelah implementasi selesai dan validation/test yang relevan berhasil.
5. Gunakan commit message yang jelas dan menggambarkan task yang baru selesai.
6. Pastikan working tree bersih setelah commit.
7. Setelah commit, tampilkan:
   - commit hash
   - commit message
   - branch aktif
   - git status --short
   - ringkasan file yang berubah
8. Sebelum memulai task baru, cek branch dan commit terakhir agar pekerjaan dilanjutkan dari state repository yang benar.
9. Jika task gagal atau validation gagal, JANGAN membuat commit palsu. Perbaiki terlebih dahulu atau laporkan error.
10. Jangan menghapus atau menimpa pekerjaan yang sudah ada di history.

ATURAN RECOVERY VPS:
- Anggap VPS dapat mati kapan saja.
- Git commit adalah checkpoint utama pekerjaan.
- Setiap milestone/task harus memiliki commit sendiri.
- Jangan hanya mengandalkan working tree yang belum di-commit.
- Jika VPS sebelumnya hilang, repository harus dapat dipulihkan berdasarkan commit/branch yang sudah tersedia di remote.
- Sebelum coding, cek apakah commit terakhir sudah ada di remote.
- Jika commit lokal belum ada di remote dan akses remote tersedia, push commit tersebut ke remote setelah validation berhasil.
- Jika push tidak memungkinkan karena credential/network, tetap commit secara lokal dan tampilkan hash commit dengan jelas agar dapat direcovery jika filesystem VPS masih tersedia.
- Jangan pernah menghapus commit yang sudah berhasil dibuat.

WORKFLOW WAJIB:
1. Audit state repository.
2. Kerjakan SATU task yang diberikan.
3. Jalankan validation yang relevan.
4. Jika berhasil → git add → git commit.
5. Verifikasi commit.
6. Jika remote tersedia → push branch aktif ke remote.
7. Tampilkan checkpoint akhir.
8. Baru tunggu instruksi task berikutnya.

PENTING:
Jangan membuat perubahan di luar scope task.
Jangan mengubah roadmap atau task berikutnya tanpa instruksi.
Jangan membuat commit kosong.
Jangan menggunakan force push.

Sekarang lanjutkan task berikutnya sesuai roadmap yang tersedia di repository. Sebelum coding, audit terlebih dahulu state branch, commit terakhir, remote, dan working tree.

```
# 
```
LANJUTKAN PROJECT BOTSPACE DARI B-052.

STATUS TERAKHIR:
- B-052 COMPLETE.
- Commit: 269a2ac — feat: add bot permission auditing + admin action audit trail
- Working tree clean.
- Total test 708 dan semuanya hijau.
- B-020..B-051 regression tetap hijau.
- Migration 40/40.
- Build, typecheck, lint, format:check semuanya sukses.
- Jangan mengulang B-052.

TUGAS:
1. Baca ROADMAP_V2.md, FLOWS.md, ADR yang relevan, dan status repository.
2. Tentukan SATU task berikutnya yang benar-benar eligible setelah B-052 berdasarkan dependency dan status aktual.
3. Jangan menebak nomor task.
4. Sebelum coding, jelaskan singkat:
   - task ID
   - tujuan
   - dependency yang sudah terpenuhi
   - mengapa task tersebut eligible sekarang
5. Audit implementasi existing sebelum membuat kode baru.
6. Jangan membuat duplicate abstraction.
7. Pertahankan seluruh contract dan regression B-020..B-052.
8. Backend + frontend tetap SATU WORKFLOW/PROJECT. Jika task membutuhkan keduanya, kerjakan terpadu.
9. Jangan membuat UI jika task belum membutuhkan UI.
10. Jangan mengerjakan task roadmap berikutnya dalam commit yang sama.
11. Jangan mengubah security design yang sudah disepakati, khususnya:
    - BotSecretManager tetap write-only
    - tidak menyimpan plaintext secret
    - tenant/workspace isolation
    - tidak membocorkan token/credential/provider raw error
12. Tambahkan test untuk acceptance criteria, failure path, security, tenant isolation, dan idempotency bila relevan.
13. Jangan menghapus atau melemahkan test existing.
14. Jika task menyentuh database, jalankan migration/schema validation PostgreSQL Docker.
15. Jika task menyentuh UI dan membutuhkan referensi visual, gunakan docs/design-references/ tanpa menghapus gambar referensi.

VALIDASI WAJIB:
- pnpm build
- pnpm test
- pnpm typecheck
- pnpm lint
- pnpm format:check
- migration/schema test jika relevan
- regression B-020..B-052

SETELAH IMPLEMENTASI:
- tampilkan task ID
- summary
- files changed
- tests added/changed
- seluruh validation result
- security/tenant audit
- remaining risks
- commit hash
- pastikan working tree clean

Commit dengan conventional commit yang sesuai.

JANGAN meminta saya memilih task jika roadmap dan dependency dapat diaudit sendiri.

Hanya kerjakan SATU task eligible berikutnya.

Akhiri dengan:
<TASK-ID> COMPLETE — WAIT FOR NEXT INSTRUCTION


```
# 
```
LANJUTKAN DARI B-051.

STATUS TERAKHIR:
- B-051 COMPLETE.
- Evidence B-051: 37 tests.
- Regression B-020..B-050 tetap hijau.
- Total test 340.
- Build/typecheck/lint/format/test semuanya sukses.
- Migration 36/36 sukses.
- Security + tenant isolation audit sukses.
- Working tree harus tetap bersih setelah pekerjaan selesai.

TUGAS:
1. Baca ROADMAP_V2.md dan dokumen architecture/contract terkait.
2. Tentukan SATU task roadmap berikutnya yang benar-benar eligible setelah B-051.
3. Validasi dependency dan status task tersebut sebelum coding.
4. Jangan mengulang B-050 atau B-051.
5. Jangan mengerjakan task berikutnya sekaligus dalam commit yang sama.
6. Audit implementasi existing terlebih dahulu agar tidak membuat duplicate abstraction.
7. Implementasikan task tersebut secara production-quality.
8. Backend dan frontend tetap diperlakukan sebagai SATU workflow/project. Jika task memang membutuhkan keduanya, kerjakan terpadu.
9. Jangan membuat UI jika task belum membutuhkan UI.
10. Pertahankan seluruh contract dan regression B-020..B-051.
11. Tambahkan test untuk acceptance criteria dan failure/security/tenant-isolation path yang relevan.
12. Jangan menghapus atau melemahkan test existing.
13. Jangan mengubah security design seperti BotSecretManager write-only hanya demi mempermudah implementasi.
14. Jika ada gambar/reference UI di docs/design-references/, gunakan sebagai referensi dan jangan hapus.

VALIDASI WAJIB:
- pnpm build
- pnpm test
- pnpm typecheck
- pnpm lint
- pnpm format:check
- migration/schema test jika relevan
- regression B-020..B-051

SECURITY:
- tenant/workspace isolation
- authorization
- secret/token protection
- no plaintext secret persistence
- no credential/raw provider error leakage
- SQL parameterization
- idempotency bila relevan

SETELAH SELESAI:
- tampilkan task ID dan alasan task tersebut eligible
- summary implementasi
- files changed
- tests added/changed
- validation result
- security/tenant audit
- remaining risks
- commit hash
- pastikan working tree clean

Commit dengan conventional commit yang sesuai.

JANGAN memilih task berdasarkan tebakan. Gunakan ROADMAP_V2.md dan dependency aktual repository.

Akhiri dengan:
<TASK-ID> COMPLETE — WAIT FOR NEXT INSTRUCTION


```
# LANJUTKAN IMPLEMENTASI PROJECT BOTSPACE DARI TASK TERAKHIR.
```

LANJUTKAN IMPLEMENTASI PROJECT BOTSPACE DARI TASK TERAKHIR.

KONDISI TERAKHIR:
- B-041 sudah COMPLETE.
- Commit terakhir B-041: fa2f31c
- Working tree harus dipertahankan bersih.
- Jangan mengulang atau mengubah scope B-041 kecuali ditemukan bug/regression nyata.
- Semua pekerjaan backend + frontend tetap dianggap SATU WORKFLOW / SATU PROJECT. Jangan membuat task terpisah hanya karena menyentuh frontend dan backend.
- Jangan membuat branch baru.
- Jangan push ke remote kecuali diminta.
- Setelah pekerjaan selesai, commit perubahan lokal.

TUGAS:

1. Baca ROADMAP_V2.md dan seluruh dokumen governance/architecture yang relevan.
2. Tentukan SECARA OTOMATIS task berikutnya setelah B-041 berdasarkan:
   - ID/dependency roadmap
   - status TODO/COMPLETE
   - dependency yang sudah terpenuhi
   - kontrak yang sudah tersedia
   - pekerjaan yang benar-benar belum dikerjakan di repository
3. Jangan menebak task. Tampilkan terlebih dahulu:
   - ID task berikutnya
   - judul
   - dependency
   - tujuan
   - file/area yang kemungkinan disentuh
4. Setelah tervalidasi, LANGSUNG IMPLEMENTASIKAN task tersebut.
5. Sebelum coding:
   - audit implementasi existing agar tidak membuat duplicate abstraction
   - gunakan contract/domain/repository yang sudah ada
   - ikuti architecture boundary yang sudah ditetapkan
   - jangan mengubah kontrak task sebelumnya tanpa alasan kuat
   - jangan membuat workaround hanya untuk membuat test hijau
6. Jika task berikutnya membutuhkan backend dan frontend, kerjakan dalam SATU IMPLEMENTASI TERPADU.
7. Jika task tersebut belum membutuhkan UI, jangan membuat UI palsu hanya demi memenuhi task.
8. Untuk UI:
   - gunakan folder docs/design-references/ sebagai referensi visual bila tersedia
   - JANGAN menghapus atau mengubah gambar referensi
   - jika membutuhkan contoh gambar untuk desain/implementasi, buat/pertahankan folder referensi yang jelas sehingga AI dapat membaca gambar tersebut
   - jangan memasukkan gambar referensi sebagai asset production kecuali memang diperlukan oleh kontrak/task.
9. Implementasikan production-quality code sesuai architecture yang ada.
10. Tambahkan test yang memang diperlukan untuk acceptance criteria.
11. Jalankan validasi penuh yang relevan:
    - pnpm build
    - pnpm test
    - pnpm typecheck
    - pnpm lint
    - pnpm format:check
    - migration/schema test jika task menyentuh database
12. Jika ada PostgreSQL/Docker integration yang relevan, lakukan validation terhadap PostgreSQL Docker juga.
13. Periksa regression terhadap test B-020 sampai B-041 dan test workspace yang sudah ada.
14. Jangan menghapus test existing.
15. Jangan menurunkan coverage atau melonggarkan assertion hanya supaya test lolos.
16. Audit security:
    - tenant/workspace isolation
    - authentication/authorization
    - secret/token leakage
    - SQL parameterization
    - error leakage
    - cross-workspace access
17. Setelah semua validasi sukses:
    - tampilkan ringkasan implementasi
    - files changed
    - tests added/changed
    - validation result
    - remaining risks
    - commit hash
18. Commit perubahan dengan format conventional commit yang sesuai task.
19. Working tree harus bersih setelah commit.
20. JANGAN mengerjakan task roadmap berikutnya sekaligus. Hanya satu task berikutnya yang benar-benar eligible setelah B-041.

ATURAN PENTING:
- Jangan berhenti hanya karena task membutuhkan investigation.
- Jangan meminta saya memilih file jika repository dapat menentukan jawabannya sendiri.
- Jangan mengarang requirement yang tidak ada di roadmap/architecture.
- Jangan mengubah roadmap hanya untuk menandai task selesai.
- Jangan membuat commit kosong.
- Jika menemukan bahwa task berikutnya sebenarnya sudah selesai di repository, audit dan buktikan terlebih dahulu, lalu cari task eligible berikutnya.
- Jika ada dependency yang belum terpenuhi, jangan memaksakan implementasi; jelaskan dependency tersebut dan pilih task eligible yang benar-benar bisa dikerjakan.
- Setelah selesai, tulis:
  "<TASK-ID> COMPLETE — WAIT FOR NEXT INSTRUCTION"

MULAI DARI B-041 DAN LANJUT KE TASK ELIGIBLE BERIKUTNYA SEKARANG.

```

# 
```

PROMPT B-041 — CONNECTION FAILURE-PATH / TELEGRAM CONNECTION REPOSITORY

Lanjutkan BotSpace dari kondisi repository SAAT INI setelah:

B-040 COMPLETE
Commit: e0996e1 test: add workspace isolation evidence

Fokus HANYA pada task roadmap berikutnya: B-041.

PENTING:
- Jangan mengulang B-040 atau task sebelumnya.
- Jangan melompati dependency.
- Baca ROADMAP_V2.md untuk memastikan scope B-041 yang sebenarnya.
- Audit implementasi yang sudah ada sebelum coding.
- Jangan mengubah arsitektur yang sudah benar.
- Jangan membuat backend dan frontend terpisah.
- Satu task saja.
- Jangan mengerjakan task setelah B-041.

==================================================
1. AUDIT B-041
==================================================

Sebelum coding baca:

- ROADMAP_V2.md
- docs/architecture/*
- docs/contracts/*
- docs/security/*
- services/api/src/
- domain repository/connection-related contracts
- Telegram connection-related code yang sudah ada
- B-030/B-031/B-040 implementation
- existing tests

Cari secara khusus:
- TelegramConnectionRepository
- connectionRepository
- connection service
- adapter interface
- in-memory adapter
- PostgreSQL adapter jika sudah tersedia
- health/state machine
- failure-path contract
- error mapping
- existing mocks/test doubles

Pastikan dependency B-041 dari roadmap memang sudah COMPLETE.

==================================================
2. IMPLEMENTASI B-041
==================================================

Implementasikan B-041 persis berdasarkan ROADMAP_V2.md dan contract existing.

Tujuan utama:
- connection failure-path harus memiliki behaviour yang deterministik;
- repository/service harus dapat menangani persistence failure dengan benar;
- error harus dipetakan ke error contract existing;
- tidak boleh membocorkan credential/token/secret;
- state connection tidak boleh menjadi inconsistent ketika persistence gagal.

Jangan membuat behaviour baru yang tidak ada di roadmap.

Jika B-041 memang membutuhkan TelegramConnectionRepository:
- ikuti repository interface existing;
- jangan membuat interface duplicate;
- gunakan domain type existing;
- gunakan persistence abstraction existing;
- jangan coupling domain dengan HTTP.

Jika adapter PostgreSQL memang belum menjadi scope B-041:
- jangan memaksa implementasi PostgreSQL penuh;
- gunakan adapter/test double sesuai roadmap;
- dokumentasikan remaining risk jika PostgreSQL adapter memang dijadwalkan task berikutnya.

==================================================
3. FAILURE-PATH TEST
==================================================

Tambahkan evidence test yang benar-benar menguji failure path.

Minimal periksa skenario yang sesuai contract:

1. Connection creation/update gagal karena persistence error.
2. Error persistence tidak berubah menjadi success palsu.
3. State connection tidak berubah secara parsial.
4. Retry/recovery behaviour mengikuti contract existing.
5. Error yang dikembalikan ke caller menggunakan error type existing.
6. Tidak ada raw database error/credential/token yang bocor.
7. User/workspace isolation tetap berlaku.
8. Existing successful connection flow tetap bekerja.
9. Existing B-040 isolation tests tetap hijau.

Jika service memiliki state transition:
- pastikan transition hanya terjadi setelah persistence operation berhasil;
- jika persistence gagal, state harus tetap konsisten dengan state sebelumnya.

Jika transaction diperlukan oleh contract:
- gunakan transaction abstraction existing;
- jangan membuat transaction framework baru.

==================================================
4. HEALTH / FAILURE STATE
==================================================

Jika B-041 menyentuh connection health/state:

- gunakan state model yang sudah tersedia;
- jangan membuat state enum duplicate;
- failure harus dapat dibedakan dari successful connection;
- jangan menganggap connection sehat hanya karena object berhasil dibuat;
- jangan melakukan credential logging;
- jangan mengubah /health atau /ready kecuali memang bagian contract B-041.

Jika health/readiness belum menjadi scope B-041:
- jangan mengerjakannya.

==================================================
5. SECURITY
==================================================

Audit khusus:

- token tidak masuk log;
- secret_ref tetap opaque;
- password tidak pernah muncul;
- database error tidak dikirim mentah ke client;
- workspace/user boundary tetap diterapkan;
- failure pada connection milik user A tidak dapat mengubah/membaca connection user B;
- request user tidak dapat memalsukan owner/user_id.

==================================================
6. REGRESSION
==================================================

Jangan menghapus test existing.

Pastikan seluruh regression tetap hijau:

B-020
B-021
B-022
B-023
B-024
B-030
B-031
B-032
B-040

Gunakan test helper existing.

==================================================
7. VALIDATION
==================================================

Setelah implementasi:

pnpm build
pnpm test
pnpm typecheck
pnpm lint
pnpm format:check

Jika ada database migration/schema test yang relevan, jalankan juga.

Jika test gagal:
- cari root cause;
- perbaiki implementation;
- jangan skip test;
- jangan mengurangi coverage hanya agar hijau.

==================================================
8. IMAGE REFERENCE
==================================================

Tidak ada UI pada B-041.

Jangan menambahkan gambar baru.
Jangan mengubah docs/design-references/.
Folder tersebut tetap dipertahankan untuk task frontend/UI mendatang.

==================================================
9. GIT
==================================================

Setelah selesai:

- git status
- git diff --stat
- tampilkan files changed
- tampilkan validation result
- tampilkan test count
- tampilkan security/failure-path evidence
- tampilkan remaining risks

Buat SATU commit saja untuk B-041 jika workflow task menggunakan commit.

Jangan push ke remote.

Commit format:

test: add connection failure path

Jika B-041 membutuhkan production code + tests, tetap satu commit.

==================================================
10. FINAL REPORT
==================================================

Tampilkan:

B-041 — [nama task sesuai ROADMAP_V2.md] — Final Report

1. Roadmap scope
2. Dependency check
3. Audit findings
4. Implementation
5. Failure-path evidence
6. Security
7. Tests
8. Validation
9. Files changed
10. Remaining risks
11. Commit hash
12. B-041 COMPLETE — WAIT FOR NEXT INSTRUCTION

PENTING:
Jika ROADMAP_V2.md menunjukkan nama/scope B-041 berbeda dari asumsi prompt ini, ikuti ROADMAP_V2.md sebagai source of truth dan sesuaikan implementasi tanpa mengerjakan task setelah B-041.

Kerjakan sekarang.

```

# ISOLATION EVIDENCE TEST
```

Lanjutkan B-040 — WORKSPACE ISOLATION EVIDENCE TEST dari kondisi saat ini.

PENTING:
- Jangan mengulang B-032 atau B-033.
- Jangan mengerjakan task setelah B-040.
- Jangan mengubah kontrak API yang sudah selesai.
- Fokus hanya menyelesaikan B-040.
- Gunakan pola test yang sudah ada di tests/src.
- Pertahankan semua 273+ test yang saat ini hijau.

Tujuan B-040:
Tambahkan evidence test yang membuktikan tenant/workspace isolation benar-benar bekerja pada connection/repository path yang digunakan workspace API.

Sebelum coding:
1. Baca ROADMAP_V2.md untuk kontrak B-040.
2. Audit tests/src/workspace-isolation.evidence.test.ts.
3. Audit connectionRepository/startApp dan adapter yang digunakan.
4. Gunakan helper/test setup existing, jangan membuat infrastructure test baru jika tidak diperlukan.

Jika workspace-isolation evidence test membutuhkan connectionRepository:
- perbaiki setup test agar dependency yang benar di-inject melalui startApp;
- jangan menggunakan global/shared repository yang dapat menyebabkan test saling bocor;
- gunakan connectionRepository instance yang sesuai dengan app/test context.

Evidence minimal harus membuktikan:
- User A tidak dapat membaca workspace/resource milik User B.
- User B tidak dapat membaca workspace/resource milik User A.
- workspace_id dari request tidak dapat melewati authorization boundary.
- query/repository tetap menggunakan user/workspace boundary yang benar.
- data tenant lain tidak muncul dalam list/detail response.
- unauthorized access menghasilkan error sesuai contract existing.
- tidak ada raw credential/session/token yang bocor.

Jangan hanya membuat test yang memeriksa HTTP status.
Pastikan evidence test benar-benar memverifikasi data isolation.

Jika perlu:
- tambahkan fixture user/workspace;
- buat dua tenant;
- masukkan data berbeda pada masing-masing tenant;
- lakukan request silang;
- assert data tenant lain tidak dapat diakses.

Jangan mengubah production behaviour hanya agar test lulus.
Jika ditemukan bug isolation pada production code, perbaiki root cause secara minimal dan sesuai architecture existing.

Validation setelah selesai:
pnpm build
pnpm test
pnpm typecheck
pnpm lint
pnpm format:check

Jalankan juga migration/database test yang tersedia jika B-040 membutuhkannya.

Setelah semua hijau:
- tampilkan jumlah test;
- tampilkan file berubah;
- tampilkan hasil validation;
- tampilkan security/isolation evidence;
- tampilkan remaining risks.

GIT:
- satu commit saja untuk B-040;
- jangan pisahkan test dan production code menjadi commit berbeda;
- jangan push ke remote.

Commit format:
test: add workspace isolation evidence

Akhiri dengan:

B-040 COMPLETE — WAIT FOR NEXT INSTRUCTION

```
# 
```

PROMPT B-033 — NEXT ROADMAP TASK

Lanjutkan project BotSpace dari kondisi repository SAAT INI setelah B-032 COMPLETE.

PENTING:
- Jangan mengulang B-001 sampai B-032.
- B-032 sudah selesai dengan commit:
  1e8b19b feat: add workspace api
- Working tree harus dipertahankan bersih sebelum mulai.
- Jangan membuat backend dan frontend sebagai dua task terpisah.
- Kerjakan SATU task roadmap berikutnya saja.
- Sebelum coding, baca ROADMAP_V2.md dan tentukan ID/task berikutnya setelah B-032.
- Jangan menebak isi task. Gunakan ROADMAP_V2.md sebagai source of truth.
- Audit dependency B-033 terlebih dahulu dan pastikan seluruh dependency-nya sudah COMPLETE.
- Jika dependency belum selesai, jangan mengarang implementasi. Laporkan blocker.

==================================================
1. AUDIT
==================================================

Sebelum coding baca:

- ROADMAP_V2.md
- README.md
- PROJECT_STATUS.md jika tersedia
- docs/architecture/*
- docs/contracts/*
- docs/security/*
- database/README.md
- implementation yang berkaitan dengan dependency B-033
- hasil/commit B-032

Cari:
- ID task berikutnya setelah B-032
- Description
- Expected result
- Dependency
- Contract
- Provides
- Status

Tentukan scope B-033 berdasarkan roadmap, bukan asumsi.

==================================================
2. IMPLEMENTASI
==================================================

Implementasikan HANYA task berikutnya setelah B-032 sesuai ROADMAP_V2.md.

Pertahankan architecture existing:

- domain
- contracts
- repository abstraction
- service/use-case
- HTTP handlers
- router
- authentication/session
- authorization
- validation
- error handling
- correlation/request ID
- database migration
- test conventions

Jangan membuat architecture baru jika abstraction existing sudah memenuhi kebutuhan.

Jangan melakukan refactor besar yang tidak diperlukan.

Jangan menghapus behaviour existing.

Jangan membuat endpoint tambahan yang tidak diminta contract.

Jika task membutuhkan database:
- gunakan migration additive/forward-only;
- jangan mengubah migration lama;
- ikuti naming convention existing;
- gunakan parameterized SQL;
- pertahankan tenant isolation.

Jika task membutuhkan authentication/authorization:
- gunakan session/auth implementation existing;
- jangan membuat authentication mechanism baru;
- jangan mempercayai user_id/workspace_id dari client sebagai bukti authorization.

Jika task membutuhkan repository:
- buat interface/domain contract terlebih dahulu bila memang belum ada;
- implementasikan adapter sesuai pola existing;
- jangan coupling domain ke PostgreSQL/HTTP.

==================================================
3. IMAGE REFERENCE
==================================================

Folder berikut SUDAH dibuat pada B-032:

docs/design-references/

Aturan:
- folder tersebut adalah tempat reference image UI;
- jangan menghapus atau memindahkan folder;
- jangan membuat folder reference kedua;
- jika task ini belum membutuhkan frontend, jangan membuat frontend besar;
- jika task ini memang membutuhkan frontend berdasarkan roadmap, WAJIB periksa docs/design-references/ terlebih dahulu sebelum membuat UI;
- gambar reference hanya menjadi acuan visual, bukan source code atau database data.

==================================================
4. TEST
==================================================

Tambahkan test untuk behaviour task ini.

Pastikan mencakup:
- happy path;
- validation;
- authentication jika diperlukan;
- authorization;
- tenant isolation jika workspace-related;
- not found;
- conflict jika relevan;
- persistence/error handling;
- regression terhadap task sebelumnya.

Jangan menghapus test existing.

==================================================
5. VALIDATION
==================================================

Setelah selesai jalankan semua validation yang tersedia, minimal:

pnpm build
pnpm test
pnpm typecheck
pnpm lint
pnpm format:check

Jika project memiliki migration/schema test, jalankan juga.

Jika ada failure:
- perbaiki jika failure disebabkan implementasi task ini;
- jangan menutupi atau melewati test;
- jangan menghapus test untuk membuat build hijau.

==================================================
6. SECURITY AUDIT
==================================================

Sebelum selesai pastikan:

- tidak ada secret/password/session token di log;
- tidak ada raw token dalam response;
- tidak ada SQL injection;
- tidak ada authorization bypass;
- tenant isolation tetap aman;
- error response tidak membocorkan internal detail;
- existing authentication/session behaviour tetap aman.

==================================================
7. GIT
==================================================

Setelah implementation dan validation selesai:

- tampilkan git status;
- tampilkan files changed;
- tampilkan test/build/typecheck/lint result;
- tampilkan remaining risks.

Jika workflow project menggunakan commit per task, buat SATU commit untuk task ini.

Jangan membuat commit backend dan frontend terpisah.

Gunakan commit message yang sesuai dengan ID dan nama task sebenarnya dari ROADMAP_V2.md.

Jangan push ke remote kecuali workflow repository secara eksplisit mengharuskannya.

==================================================
8. FINAL REPORT
==================================================

Tampilkan:

B-XXX — [NAMA TASK] — Final Report

1. Roadmap task
2. Dependency check
3. Scope implemented
4. Files changed
5. Database changes
6. API/contract changes
7. Authorization/security
8. Tests
9. Validation
10. Image reference impact
11. Remaining risks
12. Commit hash
13. B-XXX COMPLETE — WAIT FOR NEXT INSTRUCTION

PENTING:
- Jika ROADMAP_V2.md menunjukkan task berikutnya bukan B-033, gunakan ID yang benar.
- Jangan mengerjakan task setelahnya.
- Jangan melompati dependency.
- Jangan mengubah roadmap.
- Jangan mengulang pekerjaan yang sudah COMPLETE.
- Kerjakan sekarang.

```
# 
```

PROMPT B-032 — WORKSPACE API + IMAGE REFERENCE FOUNDATION

Lanjutkan implementasi project BotSpace dari kondisi repository SAAT INI.

PENTING:
- Jangan mengulang pekerjaan B-001 sampai B-031 yang sudah selesai.
- Jangan merombak arsitektur yang sudah ada.
- Jangan membuat backend dan frontend sebagai dua task terpisah.
- Untuk task ini fokus pada backend/API sesuai roadmap B-032.
- Tetap gunakan architecture, contracts, domain boundaries, repository pattern, validation, error handling, authentication/session flow, dan coding conventions yang sudah ada.
- Sebelum coding, audit singkat repository dan baca ROADMAP_V2.md untuk memastikan kontrak B-032 yang sebenarnya.
- Jangan menebak kontrak jika sudah tersedia di docs/contracts/ADR/roadmap. Ikuti kontrak repository yang sudah ada.
- Pertahankan semua behaviour B-020 sampai B-031.
- Jangan menghapus test existing.
- Jangan membuat mock implementation jika repository/adapter nyata memang sudah menjadi bagian dari kontrak task.
- Jangan mengubah API existing secara breaking.

==================================================
1. TASK UTAMA — B-032 WORKSPACE API
==================================================

Implementasikan B-032 sesuai ROADMAP_V2.md dan kontrak yang sudah tersedia.

Tujuan:
Workspace adalah tenant/boundary utama setelah authentication dan membership/invitation.

Pastikan implementasi workspace mengikuti prinsip:
- setiap workspace memiliki identity/id yang stabil;
- workspace memiliki owner;
- user hanya dapat mengakses workspace yang memang menjadi miliknya melalui membership;
- tenant isolation wajib ditegakkan di repository/query layer;
- jangan pernah mempercayai workspace_id hanya dari input client tanpa memvalidasi membership/authorization;
- gunakan authenticated session/user sebagai sumber identitas;
- jangan bocorkan data workspace milik user lain;
- error response harus konsisten dengan error contract yang sudah ada;
- jangan expose credential, password, session token, token hash, atau secret material.

Ikuti dependency B-030 dan B-031 yang sudah selesai.

==================================================
2. AUDIT SEBELUM IMPLEMENTASI
==================================================

Sebelum mengubah file:

1. Baca:
   - ROADMAP_V2.md
   - README.md
   - docs/architecture/*
   - docs/security/*
   - docs/contracts/*
   - database/README.md
   - package/workspace/domain yang relevan
   - auth/session implementation
   - membership/invitation implementation B-031

2. Cari apakah sudah ada:
   - workspace entity
   - workspace repository interface
   - workspace contracts
   - workspace migration
   - workspace_members/membership table
   - invitation table
   - authenticated request/session helper
   - authorization helper
   - error types
   - pagination primitives

3. Gunakan yang sudah ada.
   Jangan membuat duplikasi entity, repository, error type, pagination, atau auth helper.

4. Jika ada bagian B-032 yang ternyata sudah partially implemented:
   - audit dahulu;
   - pertahankan implementasi yang benar;
   - lengkapi hanya bagian yang kurang;
   - jangan rewrite tanpa alasan.

==================================================
3. DOMAIN / CONTRACT
==================================================

Implementasikan workspace sesuai boundary domain yang sudah ditentukan.

Minimal pastikan domain contract mencakup kebutuhan yang memang disebut B-032, misalnya:
- create workspace
- get workspace
- list current user's workspaces
- update workspace jika memang ada di contract
- membership/authorization check
- workspace ownership

Jangan menambahkan endpoint atau behaviour yang tidak diminta roadmap.

Jika ROADMAP_V2.md memiliki nama endpoint atau response contract spesifik, gunakan nama tersebut secara persis.

Gunakan typed result/error pattern yang sudah digunakan repository.

Validasi:
- workspace name wajib valid sesuai domain rule;
- trim input jika contract mengharuskan;
- jangan menerima nilai kosong;
- validasi panjang maksimal;
- jangan memperbolehkan data invalid masuk database;
- gunakan validation mechanism existing.

==================================================
4. AUTHORIZATION & TENANT ISOLATION
==================================================

Ini bagian penting.

Setiap workspace operation harus memastikan user authenticated.

Aturan:
- unauthenticated -> 401 sesuai contract;
- authenticated tetapi bukan member -> 403 atau error yang sudah ditentukan contract;
- workspace tidak ada -> 404 sesuai contract;
- jangan membocorkan apakah workspace tertentu ada jika security contract mensyaratkan generic response;
- query repository harus selalu memiliki workspace/user boundary yang benar.

Jangan membuat pola seperti:

SELECT * FROM workspaces WHERE id = $1

lalu baru melakukan authorization di tempat lain jika arsitektur repository mengharuskan tenant filtering.

Gunakan boundary yang konsisten.

Untuk list workspace:
- hanya workspace yang user memang memiliki membership/ownership;
- jangan mengembalikan workspace milik user lain;
- gunakan repository query yang memiliki user_id boundary.

Untuk workspace detail:
- pastikan requester memiliki akses;
- jangan percaya workspace_id dari body/query sebagai authorization proof.

==================================================
5. DATABASE
==================================================

Audit migration existing terlebih dahulu.

Jika schema workspace sudah ada:
- gunakan schema tersebut;
- jangan membuat tabel duplicate.

Jika B-032 memang membutuhkan migration baru berdasarkan roadmap:
- buat migration additive/forward-only;
- jangan mengubah migration lama;
- gunakan naming convention migration existing;
- gunakan FK yang tepat;
- gunakan UNIQUE constraint yang memang dibutuhkan contract;
- gunakan timestamp convention yang sama;
- pastikan migration idempotency sesuai migration runner project.

Jika workspace sudah memiliki owner:
- gunakan relation yang benar ke users.
- jangan menyimpan password/session/token di workspace.

Jika membership table sudah tersedia dari B-031:
- gunakan table tersebut.
- jangan membuat duplicate membership table.

==================================================
6. REPOSITORY
==================================================

Tambahkan/selesaikan workspace repository sesuai repository abstraction yang sudah digunakan project.

Repository harus:
- parameterized SQL;
- tidak melakukan string interpolation untuk user input;
- menangani not-found dengan error type existing;
- menangani unique violation/persistence error dengan mapping existing;
- menjaga user/workspace boundary;
- mendukung testability;
- tidak bergantung langsung ke HTTP layer.

Jika project saat ini masih memakai in-memory adapter untuk roadmap tahap tersebut:
- ikuti roadmap;
- jangan tiba-tiba mengubah seluruh repository architecture;
- tetap siapkan contract agar PostgreSQL adapter berikutnya dapat mengikuti interface yang sama.

==================================================
7. SERVICE / USE CASE
==================================================

Workspace business logic harus berada di service/use-case layer, bukan di router.

Service harus:
- menerima authenticated user identity;
- melakukan validation;
- melakukan authorization;
- memanggil repository;
- mengembalikan domain result;
- tidak bergantung pada HTTP framework.

Jangan menaruh business rule di handler jika service pattern existing sudah tersedia.

==================================================
8. HTTP API
==================================================

Tambahkan endpoint B-032 sesuai kontrak ROADMAP_V2.md.

Gunakan:
- router convention existing;
- handler convention existing;
- correlation/request ID existing;
- error mapping existing;
- authentication middleware/helper existing;
- response format existing.

Jangan membuat format response baru jika repository sudah memiliki standard envelope.

Pastikan:
- 401 untuk unauthenticated;
- 400/422 untuk invalid input sesuai contract;
- 403 untuk unauthorized jika contract menggunakan 403;
- 404 untuk resource not found sesuai contract;
- 409 untuk conflict jika diperlukan;
- 500 hanya untuk unexpected persistence/internal error.

Jangan mengembalikan stack trace atau internal database error ke client.

==================================================
9. TEST
==================================================

Tambahkan test yang benar-benar menguji behaviour B-032.

Minimal coverage:

A. Authentication
- request tanpa session -> 401.

B. Create workspace
- authenticated user dapat membuat workspace;
- owner tersimpan benar;
- invalid name ditolak;
- duplicate/conflict mengikuti contract.

C. List workspace
- user hanya melihat workspace yang dia miliki/ikuti;
- workspace user lain tidak muncul.

D. Get workspace
- member/owner dapat melihat workspace;
- user lain tidak dapat melihat workspace.

E. Tenant isolation
Buat test eksplisit:
- user A memiliki workspace A;
- user B memiliki workspace B;
- user A mencoba mengakses workspace B;
- operasi harus ditolak;
- tidak boleh ada data workspace B yang bocor.

F. Regression
- seluruh test B-020/B-021/B-022/B-023/B-024/B-030/B-031 tetap hijau.

Jika sudah ada test helper untuk session/user, gunakan helper tersebut.
Jangan membuat test infrastructure duplicate.

==================================================
10. IMAGE REFERENCE FOUNDATION
==================================================

Tambahkan folder:

docs/design-references/

Buat:

docs/design-references/README.md

Isi README secara singkat bahwa folder tersebut digunakan untuk menyimpan screenshot/gambar referensi desain UI yang akan digunakan AI/OpenCode pada task frontend berikutnya.

Aturan folder:
- PNG/JPG/JPEG/WebP diperbolehkan;
- jangan masukkan gambar ke source code;
- jangan masukkan gambar ke database;
- jangan mengubah gambar yang nantinya saya upload;
- gambar hanya sebagai visual reference;
- pada task frontend berikutnya, AI wajib memeriksa folder ini sebelum mengimplementasikan UI;
- jangan membuat frontend pada task B-032 hanya karena folder reference dibuat.

Jangan membuat folder reference lain.

==================================================
11. FRONTEND
==================================================

JANGAN mengerjakan implementasi frontend besar pada task ini.

Hanya siapkan:

docs/design-references/

beserta README.md.

Frontend akan dikerjakan pada task frontend yang memang sudah ditentukan roadmap.

Namun pastikan API contract B-032 dapat digunakan frontend berikutnya.

==================================================
12. QUALITY GATE
==================================================

Setelah coding jalankan seluruh validation yang tersedia.

Minimal:

pnpm build
pnpm test
pnpm typecheck
pnpm lint
pnpm format:check

Jika script berbeda, gunakan script yang memang tersedia di package.json/root workspace.

Jika ada database migration test:
- jalankan juga migration/schema assertion test yang tersedia.

Jika Docker PostgreSQL diperlukan oleh test:
- gunakan environment existing;
- jangan merusak container/project lain.

==================================================
13. AUDIT SECURITY
==================================================

Sebelum selesai cek:

- tidak ada password/token/secret di log;
- tidak ada raw session token di response;
- tidak ada token hash di response;
- tidak ada SQL injection;
- tidak ada authorization bypass;
- workspace isolation benar;
- user_id tidak dapat dipalsukan melalui request body;
- workspace_id tidak menjadi authorization proof;
- error tidak membocorkan informasi internal;
- existing auth/session security tidak rusak.

==================================================
14. GIT / COMMIT
==================================================

JANGAN push ke remote.

JANGAN membuat commit jika repository workflow saat ini memang meminta working tree untuk diperiksa terlebih dahulu.

Setelah implementation selesai:
- tampilkan git status;
- tampilkan file yang berubah;
- tampilkan ringkasan perubahan;
- tampilkan hasil build/test/typecheck/lint;
- tampilkan remaining risks.

Jika workflow repository memang mengharuskan commit pada setiap task, buat SATU commit saja untuk seluruh B-032.

Jangan membuat commit terpisah backend/frontend.

Format commit:

feat: add workspace api

==================================================
15. FINAL REPORT
==================================================

Di akhir berikan laporan dengan format:

B-032 — Workspace API — Final Report

1. Scope
2. Files Changed
3. Database Changes
4. API Endpoints
5. Authorization / Tenant Isolation
6. Tests
7. Validation
8. Security Checks
9. Image Reference Folder
10. Remaining Risks
11. Commit Hash
12. B-032 COMPLETE — WAIT FOR NEXT INSTRUCTION

PENTING:
Jika ada masalah atau kontrak B-032 ambigu, JANGAN mengarang behaviour baru.
Berhenti pada bagian yang ambigu, jelaskan temuan, dan tunggu instruksi.

Kerjakan sekarang dari repository yang ada.
Jangan mengulang task yang sudah COMPLETE.
Jangan mengubah roadmap.
Jangan membuat frontend besar.
Fokus B-032 + image-reference foundation.

```

# B-031 — Membership / Invitation API
```
Prompt B-031 — Membership / Invitation API

Lanjutkan BotSpace dari commit terakhir B-030:
7436ce6 feat: add workspace api

Implementasikan B-031 — Membership / Invitation API sesuai ROADMAP_V2.md dan contract yang sudah ada.

ATURAN UTAMA:
- Jangan mengulang atau merusak B-020 sampai B-030.
- Jangan mengerjakan B-040 Telegram Account.
- Jangan mengerjakan B-050 Bot Installation.
- Jangan mengerjakan frontend.
- Jangan mengubah ROADMAP_V2.md.
- Ikuti arsitektur dan pola code yang sudah ada.
- Sebelum coding, audit contract/domain/repository/migration/API existing agar implementasi tepat terhadap contract, bukan menebak desain baru.

Scope B-031:
1. Audit contract membership/invitation yang sudah tersedia.
2. Implementasikan domain types/entity/errors yang memang diwajibkan contract.
3. Implementasikan repository interface dan adapter sesuai pola B-030.
4. Tambahkan migration database jika contract membutuhkan perubahan schema.
5. Implementasikan membership lifecycle:
   - member/workspace relationship
   - role sesuai contract
   - invitation lifecycle sesuai contract
   - pending/accepted/rejected/expired state jika memang didefinisikan contract
6. Implementasikan authorization:
   - workspace owner/admin hanya boleh melakukan operasi yang memang diizinkan contract.
   - user tidak boleh mengakses membership workspace lain.
   - tenant/workspace isolation wajib.
   - jangan memperluas permission di luar contract.
7. Implementasikan service/use-case layer.
8. Implementasikan HTTP handlers/routes sesuai API contract.
9. Validasi request dan error mapping harus mengikuti pola existing.
10. Jangan expose credential, token rahasia, password, atau internal database fields.

Invitation security:
- Invitation token/secret jangan disimpan plaintext jika contract memerlukan secret.
- Jangan mengembalikan secret/token sensitif di log.
- Duplicate invitation harus ditangani sesuai contract.
- Expired/revoked/invalid invitation harus menghasilkan error contract yang benar.
- Invitation dari workspace/tenant lain tidak boleh dapat digunakan.
- Acceptance harus atomic dan aman terhadap race condition sesuai kemampuan adapter/database saat ini.

Testing WAJIB:
- domain/unit tests
- membership authorization tests
- invitation lifecycle tests
- duplicate invitation
- invalid/expired/revoked invitation
- cross-workspace/tenant isolation
- owner/admin permission tests
- unauthorized user tests
- repository tests jika adapter tersedia
- API/handler integration tests
- regression seluruh test B-020 sampai B-030

Database:
- Gunakan migration forward-only/additive.
- Jangan mengubah migration lama.
- SQL wajib parameterized.
- Pastikan schema assertion/migration test tetap hijau.

Validation WAJIB:
pnpm build
pnpm test
pnpm typecheck
pnpm lint
pnpm format

Jika ada test/regression gagal akibat implementasi B-031, perbaiki sampai seluruh validation hijau.

Git:
- Setelah implementasi dan semua validation hijau, buat SATU commit:
  feat: add membership invitation api
- Jangan push ke remote.
- Working tree harus bersih setelah commit.

Laporan akhir:
1. Ringkasan B-031.
2. File yang dibuat/diubah.
3. Migration/schema yang ditambahkan.
4. Endpoint membership/invitation.
5. Authorization dan tenant-isolation yang diterapkan.
6. Security invitation.
7. Hasil build/test/typecheck/lint/format.
8. Commit hash.
9. Remaining risks.
10. Jika semua berhasil, tulis:
B-031 COMPLETE — WAIT FOR NEXT INSTRUCTION


```
# Prompt B-030 — Workspace API
```

Prompt B-030 — Workspace API

Lanjutkan project BotSpace dari kondisi repository saat ini. Jangan mengulang atau mengubah fitur B-020, B-021, B-022, B-023, atau B-024 yang sudah ada.

Tugas utama:
Implementasikan B-030 — Workspace API sesuai ROADMAP_V2.md, kontrak yang sudah ada, arsitektur repository, dan pola code/test yang sekarang.

Sebelum coding:
1. Audit kontrak workspace yang sudah tersedia di packages/contracts dan domain primitives yang relevan.
2. Audit repository/service/router/handler yang sudah ada.
3. Audit migration database yang sudah ada.
4. Pastikan desain mengikuti boundary yang sudah ditetapkan:
   - workspace memiliki tenant isolation.
   - workspace mempunyai unique pair sesuai kontrak.
   - workspace memiliki state/status yang jelas.
   - jangan memasukkan logic Telegram bot/account dulu.
   - jangan mengerjakan membership/invitation B-031 dulu kecuali type/interface minimal memang dibutuhkan oleh kontrak B-030.
5. Jangan membuat arsitektur baru jika pola existing bisa digunakan.

Implementasi B-030 harus mencakup:
- workspace domain entity/value types yang diperlukan sesuai contract.
- repository interface dan PostgreSQL repository.
- migration database baru jika memang diwajibkan oleh kontrak.
- use-case/service layer.
- API handler/routes untuk workspace sesuai contract.
- validasi input.
- tenant isolation: operasi workspace tidak boleh bisa mengakses workspace milik tenant/user lain.
- error mapping mengikuti error contract existing.
- correlation/request handling mengikuti pola API existing.
- gunakan parameterized SQL.
- jangan expose secret atau data internal.
- pertahankan framework-agnostic domain/service layer.

Testing wajib:
- unit test domain.
- repository test dengan PostgreSQL Docker bila pola project sudah mendukungnya.
- service/use-case test.
- API/handler integration test.
- test tenant isolation/cross-tenant access.
- test duplicate/invalid input.
- test not-found dan error mapping.
- regression test seluruh fitur sebelumnya.

Validation wajib:
- pnpm build
- pnpm test
- pnpm typecheck
- pnpm lint

Jangan berhenti hanya karena ada test lama yang gagal. Perbaiki regression yang disebabkan implementasi B-030 tanpa merusak kontrak sebelumnya.

Governance:
- Jangan mengubah ROADMAP_V2.md.
- Jangan menghapus test existing.
- Jangan mengubah API auth/session B-020 sampai B-024 kecuali ada dependency nyata yang diperlukan B-030.
- Jangan membuat frontend.
- Jangan membuat fitur B-031 membership/invitation.
- Jangan membuat Telegram account/bot feature.
- Jangan menggunakan mock sebagai pengganti implementasi production jika contract B-030 sudah jelas.
- Ikuti struktur modular repository yang sekarang.

Git:
- Setelah seluruh implementasi selesai dan semua validation hijau, buat SATU commit dengan message:
  feat: add workspace api
- Jangan push ke remote.
- Working tree harus bersih setelah commit.

Laporan akhir wajib berisi:
1. Ringkasan implementasi B-030.
2. Semua file yang dibuat/diubah.
3. Migration yang dibuat dan alasannya.
4. Endpoint API yang ditambahkan.
5. Security/tenant-isolation checks.
6. Hasil build/test/typecheck/lint.
7. Commit hash.
8. Remaining risks jika ada.
9. Tuliskan: B-030 COMPLETE — WAIT FOR NEXT INSTRUCTION hanya jika seluruh validation berhasil.

```
# B-025: Workspace API
```

# Prompt B-025 — Workspace API

Lanjutkan project `/root/botspace` dari B-024.

B-021 Authentication, B-022 Rate Limiting, B-023 SessionRepository Pagination, dan B-024 Session Management API sudah COMPLETE.

Jangan mengulang pekerjaan tersebut.

Tujuan B-025:
Implementasikan Workspace API sebagai fondasi multi-workspace BotSpace.

Konsep:
- Satu user dapat memiliki beberapa workspace.
- Setiap workspace dimiliki oleh satu user.
- Workspace menjadi boundary utama untuk fitur Bot, Telegram account, dan konfigurasi berikutnya.
- User tidak boleh mengakses workspace milik user lain.

Audit terlebih dahulu architecture existing:
- domain
- repository ports
- database migrations
- PostgreSQL adapter
- auth/session
- router/handlers
- existing workspace-related code jika ada

Jangan langsung membuat architecture baru jika fondasi existing sudah tersedia.

Implementasikan minimal:

1. Create Workspace
   POST /v1/workspaces

2. List My Workspaces
   GET /v1/workspaces

3. Get Workspace
   GET /v1/workspaces/:id

4. Update Workspace
   PATCH /v1/workspaces/:id

5. Delete Workspace
   DELETE /v1/workspaces/:id

Authentication:
- Semua endpoint workspace membutuhkan authenticated session.
- Owner berasal dari authenticated user/session.
- Jangan menerima user_id dari client sebagai authority.
- Setiap query workspace wajib dibatasi owner/user boundary.
- Workspace user lain harus tidak dapat dibaca, diubah, atau dihapus.

Workspace fields:
Gunakan schema/database contract existing jika sudah ada.
Jika belum ada, gunakan desain minimal dan modular:
- id
- user_id / owner_id
- name
- created_at
- updated_at

Jangan menambahkan field yang belum diperlukan untuk task ini.

Validation:
- name wajib valid
- trim whitespace
- jangan menerima empty name
- tetapkan batas panjang yang wajar
- response/error mengikuti format API existing

Repository:
Buat WorkspaceRepository interface di domain/port layer.
Implementasikan PostgreSQL adapter.
Jangan menaruh SQL di handler.
Gunakan parameterized query.
Pastikan foreign key/user ownership benar.

Security:
- User A tidak boleh membaca workspace User B.
- User A tidak boleh update workspace User B.
- User A tidak boleh delete workspace User B.
- Jangan bocorkan keberadaan workspace milik user lain.
- Jangan log session token/password.
- Jangan expose credential fields.

Testing wajib:

Authentication:
- request tanpa auth → 401

Create:
- create workspace berhasil
- invalid name ditolak

List:
- hanya workspace milik user
- user dengan banyak workspace
- user tanpa workspace

Get:
- workspace sendiri berhasil
- workspace user lain ditolak

Update:
- workspace sendiri berhasil
- workspace user lain ditolak

Delete:
- workspace sendiri berhasil
- workspace user lain ditolak
- delete ulang ditangani sesuai contract

Regression:
- seluruh test B-021/B-022/B-023/B-024 tetap GREEN.

Jika database migration workspace belum ada:
- buat migration baru yang additive/forward-only
- jangan mengubah migration 0001–0004
- migration harus idempotent sesuai migration runner existing
- foreign key ke users harus benar
- tambahkan index yang memang diperlukan untuk query ownership

Jangan:
- membuat Bot API
- membuat Telegram API
- membuat frontend
- membuat billing
- membuat Redis
- mengubah authentication flow
- mengubah rate limiter
- mengubah session management kecuali diperlukan untuk integration
- push ke GitHub

Validation:

pnpm build
pnpm test
pnpm typecheck
pnpm lint

Kemudian:

curl http://127.0.0.1:3001/health
curl http://127.0.0.1:3001/ready

Lakukan integration test dengan minimal dua user:
- User A membuat workspace
- User A melihat workspace
- User B tidak dapat melihat workspace A
- User B tidak dapat update/delete workspace A
- User A dapat update/delete workspace sendiri

Sebelum selesai:

git diff
git status

Jika semua GREEN, commit:

feat: add workspace api

Jangan push.

Final report wajib berisi:
- files changed
- database migration
- workspace data model
- API endpoints
- ownership/security model
- integration test dua user
- tests
- build
- typecheck
- lint
- health
- ready
- commit hash
- remaining risks

Jika semua berhasil:

B-025 COMPLETE — WAIT FOR NEXT INSTRUCTION

```
# 
```
Audit dan perbaiki masalah API server pada project Botspace di /root/botspace.

Kondisi saat ini:
- PostgreSQL Docker sudah berjalan normal.
- Database migration berhasil: 3 migration applied.
- pnpm install --frozen-lockfile berhasil.
- pnpm build berhasil: 11/11 packages successful.
- pnpm dev juga selesai dengan 5/5 successful, tetapi semua proses langsung exit.
- services/api/src/main.ts sudah memanggil:
  await app.server.start();
- services/api/src/app.ts sudah membuat server melalui createApiServer().
- Namun node dist/main.js langsung kembali ke shell dan tidak membuka port API_PORT=3001.
- Web/admin/worker/scheduler saat ini masih foundation/stub dan hanya mencetak "foundation ready".

Tugas:
1. Audit services/api/src/server.ts dan seluruh implementasi createApiServer().
2. Telusuri kenapa await app.server.start() tidak membuat proses tetap hidup/listen pada port 3001.
3. Audit main.ts, app.ts, server.ts, router.ts dan konfigurasi host/port.
4. Jangan membuat workaround sementara.
5. Jangan menghapus fitur atau merombak arsitektur yang sudah ada.
6. Pertahankan struktur repository dan dependency yang ada.
7. Perbaiki implementasi API server agar benar-benar listen pada APP/API port yang dikonfigurasi.
8. Pastikan proses Node tetap berjalan setelah start().
9. Pastikan endpoint /health dan /ready bisa diakses.
10. Jalankan:
   - pnpm build
   - pnpm dev atau start API yang sesuai
   - curl http://127.0.0.1:3001/health
   - curl http://127.0.0.1:3001/ready
   - ss -lntp | grep 3001
11. Jika ada masalah konfigurasi APP_URL/APP_PORT/API_PORT, gunakan konfigurasi project yang sudah ada dan jangan mengubah .env secara sembarangan.
12. Setelah selesai, tampilkan:
   - file yang diubah
   - penyebab utama
   - perubahan yang dilakukan
   - hasil build
   - hasil curl /health
   - port yang berhasil listen

Penting:
Jangan hanya menjelaskan masalah. Lakukan audit, edit file yang diperlukan, build ulang, dan verifikasi sampai API benar-benar listening.


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
