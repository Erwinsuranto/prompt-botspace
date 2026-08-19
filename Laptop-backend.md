# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# Prompt: B-071 File/Share Contract Design
```

# Prompt: B-071 File/Share Contract Design

Lanjutkan project BotSpace dari kondisi repository saat ini.

Konteks yang benar:

* B-030 Workspace API/Contract SUDAH selesai dan tidak perlu disentuh lagi.
* B-070 Storage Adapter SUDAH selesai.
* Kita sekarang melanjutkan roadmap **B-071**.
* Prompt B-071 sebelumnya sudah dijalankan dan melakukan audit.
* Audit menemukan bahwa implementasi API B-071 belum boleh dilakukan karena contract file/share belum lengkap.
* Jangan mengulang B-030 atau B-070.
* Jangan membuat perubahan di luar scope B-071.

Hasil audit B-071 sebelumnya menunjukkan contract yang perlu diselesaikan:

1. File metadata model dan repository contract.
2. File migration dengan ownership workspace.
3. File ID/object identifier rules.
4. Upload/download API request dan response shapes.
5. File-specific authorization permission.
6. Share-link state model.
7. Share token format dan storage policy.
8. Share access permission.
9. Share expiry/lifecycle behavior jika memang diperlukan oleh roadmap.
10. Binary/multipart request handling contract di API layer.

Tugas sekarang:

1. Audit kembali kode B-030 Workspace contract dan B-070 `ObjectStoragePort` yang SUDAH ADA.
2. Jangan mengubah B-030 atau B-070 kecuali benar-benar diperlukan untuk kompatibilitas contract B-071.
3. Tentukan contract minimum B-071 berdasarkan kode dan schema yang benar-benar tersedia.
4. Implementasikan contract/domain foundation untuk file dan share secara modular.
5. Pastikan setiap file memiliki:

   * workspace ownership,
   * stable file/object identifier,
   * metadata yang diperlukan,
   * hubungan yang jelas dengan object storage.
6. Tambahkan repository contract untuk file metadata jika memang repository abstraction memang diperlukan oleh arsitektur.
7. Tambahkan model/state untuk share-link yang diperlukan oleh roadmap.
8. Definisikan aturan token share secara aman dan deterministic berdasarkan contract yang ada.
9. Definisikan permission/access rules untuk file dan share.
10. Definisikan request/response shape untuk upload, download, dan share tanpa mengimplementasikan HTTP endpoint penuh terlebih dahulu.
11. Binary/multipart handling hanya didefinisikan jika API architecture repository memang sudah memiliki boundary untuk itu.
12. Jangan mengarang database schema, migration field, permission, expiry, atau persistence behavior yang tidak didukung oleh roadmap/codebase.
13. Jangan membuat implementation storage baru. Gunakan `ObjectStoragePort` dari B-070.
14. Jangan membuat Telegram polling/webhook runtime.
15. Jangan mengubah `BotInstallation.status`.
16. Jangan mengimplementasikan File/Share API end-to-end pada tahap ini jika contract belum menjadi fondasi yang stabil.
17. Tambahkan unit test untuk contract/domain behavior yang memang dapat diuji.
18. Jangan mengubah atau menjalankan integration test Gorouter.app.
19. NVIDIA dan TokenHarbor tidak perlu disentuh.

Setelah implementasi selesai jalankan:

* pnpm test
* pnpm build
* pnpm typecheck
* pnpm lint
* pnpm format:check
* scripts/check-imports.mjs
* scripts/check-symlinks.mjs
* scripts/check-ownership.mjs
* scripts/check-doc-links.mjs
* git diff --check

Jika semua validation PASS:

20. Review seluruh diff dan pastikan hanya perubahan B-071 contract/domain foundation.
21. Buat satu commit lokal dengan message yang sesuai, misalnya:
    `feat: define file share contracts`
22. Langsung push:
    `git push origin backend-dev-recovery`
23. Verifikasi SHA lokal dan remote sama.
24. Jika push gagal karena credential/network, jangan mengubah credential secara sembarangan. Commit lokal harus tetap aman.

Terakhir tampilkan:

* commit SHA,
* push status,
* validation status,
* file yang berubah,
* contract yang berhasil ditambahkan,
* remaining issues,
* apakah B-071 sekarang siap dilanjutkan ke implementasi API end-to-end,
* roadmap berikutnya berdasarkan dependency nyata repository.

Kerjakan langsung pada `/root/botspace`.


```
# B-030 Workspace API/Contract
```

# Prompt: B-030 Workspace API/Contract + Push

Lanjutkan project BotSpace dari kondisi repository saat ini.

Kondisi terakhir:

* B-070 Storage Adapter sudah selesai.
* B-071 sudah diaudit tetapi BELUM diimplementasikan karena dependency contract belum tersedia.
* Working tree terakhir clean.
* Remote `origin/backend-dev-recovery` sudah sinkron dengan commit terakhir.
* Jangan mengulang B-070.
* Jangan mengimplementasikan B-071 secara parsial.

Sekarang fokus menyelesaikan dependency **B-030: Workspace API/Contract**.

Tugas:

1. Audit roadmap B-030 dan seluruh contract/domain/workspace implementation yang sudah ada.
2. Tentukan scope B-030 berdasarkan kebutuhan nyata repository dan dependency B-071.
3. Implementasikan Workspace API/contract secara modular dan end-to-end sesuai arsitektur yang sudah ada.
4. Contract harus menyediakan dasar yang dibutuhkan untuk:

   * workspace identity,
   * workspace ownership,
   * workspace-scoped authorization,
   * workspace access boundaries,
   * hubungan user/account dengan workspace,
   * API behavior yang diperlukan oleh file/share system.
5. Jangan membuat schema baru hanya berdasarkan asumsi. Gunakan schema/model/repository contract yang sudah tersedia jika memang sudah ada.
6. Jika ada dependency yang belum tersedia, audit dan implementasikan hanya dependency yang memang merupakan bagian langsung dari B-030.
7. Jangan mengimplementasikan B-071 File/Share API sekarang.
8. Jangan membuat Telegram polling/webhook runtime.
9. Jangan mengubah `BotInstallation.status` menjadi runtime process state.
10. Jangan membuat persistence contract palsu hanya agar dependency terlihat selesai.
11. Pastikan boundary workspace mencegah akses lintas workspace.
12. Tambahkan unit test untuk behavior contract yang benar-benar diimplementasikan, terutama:

    * workspace ownership,
    * workspace authorization,
    * workspace isolation,
    * valid/invalid workspace identifier,
    * access denial.
13. Jangan mengubah atau menjalankan integration test Gorouter.app.
14. NVIDIA dan TokenHarbor hanya diverifikasi jika benar-benar tersentuh perubahan.

Setelah implementasi selesai jalankan validation lengkap:

* pnpm test
* pnpm build
* pnpm typecheck
* pnpm lint
* pnpm format:check
* scripts/check-imports.mjs
* scripts/check-symlinks.mjs
* scripts/check-ownership.mjs
* scripts/check-doc-links.mjs
* git diff --check

Jika semua PASS:

15. Review diff dan pastikan hanya perubahan yang diperlukan untuk B-030.
16. Buat satu commit lokal dengan message yang sesuai, misalnya:
    `feat: add workspace api contract`
    gunakan message yang lebih tepat jika diperlukan.
17. LANGSUNG push:
    `git push origin backend-dev-recovery`
18. Setelah push, verifikasi SHA lokal dan remote sama.
19. Jangan mengubah credential GitHub jika push gagal.

Terakhir tampilkan:

* commit SHA,
* push status,
* validation status,
* file yang berubah,
* remaining issues,
* dependency B-071 yang sekarang sudah terpenuhi atau yang masih kurang,
* roadmap/task berikutnya yang paling tepat.

Jangan mengerjakan fitur acak di luar B-030.
Kerjakan langsung pada `/root/botspace`.


```
# -071: File/Share API + Access Control
```

# Prompt: B-071 File/Share API + Access Control

Lanjutkan project BotSpace dari kondisi repository saat ini.

Kondisi terakhir:

* B-070 Storage Adapter sudah selesai.
* Commit B-070 sudah berhasil dibuat.
* Push ke `origin/backend-dev-recovery` sudah berhasil.
* Working tree harus dipertahankan clean sebelum mulai.
* Jangan mengulang pekerjaan B-070.

Sekarang lanjutkan roadmap **B-071: File/share API + access control**.

Tugas:

1. Audit terlebih dahulu roadmap B-071, contract yang sudah tersedia, `ObjectStoragePort`, storage adapter hasil B-070, module runtime, serta struktur API BotSpace.
2. Gunakan contract/schema yang sudah ada. Jangan mengarang persistence schema baru jika belum ada dasar yang jelas.
3. Implementasikan File/Share API secara modular dengan scope workspace.
4. Sediakan behavior untuk:

   * upload file,
   * download file,
   * share file,
   * workspace-scoped authorization,
   * metadata file sesuai contract yang tersedia,
   * access control untuk share link.
5. Pastikan user/workspace hanya dapat mengakses object yang memang menjadi haknya.
6. Tambahkan perlindungan:

   * path traversal,
   * unsafe upload/path input,
   * invalid object identifier,
   * akses lintas workspace,
   * download object yang tidak memiliki izin.
7. Gunakan `ObjectStoragePort` sebagai abstraction. Jangan membuat storage implementation baru di layer API.
8. Jangan mencampurkan HTTP/API handling dengan storage implementation atau business logic.
9. Share-link access control harus mengikuti schema/roadmap yang memang sudah tersedia. Jangan membuat expiry, permission, token, atau field baru tanpa contract yang mendukungnya.
10. Jangan mengimplementasikan Telegram polling/webhook runtime pada tahap ini.
11. Jangan mengubah `BotInstallation.status` menjadi process/runtime state.
12. Tambahkan unit test untuk:

    * upload authorization,
    * download authorization,
    * workspace isolation,
    * share access,
    * invalid/path traversal input,
    * object-not-found behavior,
    * storage adapter interaction.
13. Jangan membuat mock/schema palsu hanya agar test PASS.
14. Jangan mengubah atau menjalankan integration test Gorouter.app.
15. NVIDIA dan TokenHarbor hanya diverifikasi jika benar-benar tersentuh perubahan; jangan menambahkan provider test yang tidak diperlukan.

Setelah implementasi selesai, jalankan validation lengkap:

* pnpm test
* pnpm build
* pnpm typecheck
* pnpm lint
* pnpm format:check
* scripts/check-imports.mjs
* scripts/check-symlinks.mjs
* scripts/check-ownership.mjs
* scripts/check-doc-links.mjs
* git diff --check

Jika semua validation PASS:

16. Review diff terakhir untuk memastikan tidak ada perubahan di luar scope B-071.
17. Buat satu commit lokal dengan message yang sesuai, misalnya:
    `feat: add file share api access control`
    gunakan message yang lebih tepat jika diperlukan.
18. Setelah commit berhasil, LANGSUNG push:
    `git push origin backend-dev-recovery`
19. Pastikan SHA lokal dan remote sama setelah push.
20. Jika push gagal karena credential/network, jangan mengubah credential secara sembarangan. Commit harus tetap aman secara lokal.

Setelah selesai tampilkan:

* commit SHA,
* push status,
* validation status,
* file yang berubah,
* remaining issues,
* roadmap/task berikutnya berdasarkan dependency nyata repository.

Jangan mengerjakan fitur acak di luar B-071.
Kerjakan langsung pada `/root/botspace`.


```
# Prompt: B-070 Storage Adapter + Push
```

# Prompt: B-070 Storage Adapter + Push

Lanjutkan project BotSpace dari kondisi repository saat ini.

Kondisi terakhir:

* Commit sebelumnya:
  `43f07db398d057a3b71a6d698b6c590c8924ef9a`
* Commit message:
  `feat: wire worker module runtime composition`
* Working tree terakhir clean.
* Validation sebelumnya berhasil.
* Push GitHub sebelumnya belum dilakukan sesuai instruksi karena credential belum tersedia.

Sekarang lanjutkan roadmap **B-070: Storage Adapter**.

Tugas:

1. Audit terlebih dahulu roadmap B-070 dan kode repository saat ini.
2. Jangan langsung membuat schema/storage contract baru jika belum ada contract yang menjadi dasar.
3. Tentukan storage adapter yang memang sudah didukung oleh arsitektur BotSpace saat ini.
4. Jika dependency/contract yang diperlukan untuk B-070 sudah tersedia, implementasikan storage adapter secara modular.
5. Storage adapter harus:

   * memiliki interface/contract yang jelas,
   * tidak mencampurkan business logic dengan persistence,
   * dapat digunakan oleh module runtime,
   * mudah diganti backend storage di masa depan,
   * tidak merusak module dan runtime yang sudah ada.
6. Jangan membuat implementasi Telegram adapter/polling/webhook runtime pada tahap ini jika memang belum menjadi bagian B-070.
7. Jangan mengubah `BotInstallation.status` menjadi runtime process state. Lifecycle state dan process state harus tetap dipisahkan.
8. Tambahkan unit test untuk behavior storage adapter yang benar-benar diimplementasikan.
9. Jangan membuat mock/schema palsu hanya agar test PASS.
10. Jangan mengubah atau menjalankan integration test Gorouter.app.
11. NVIDIA dan TokenHarbor boleh diverifikasi bila memang tersentuh oleh perubahan, tetapi jangan menambahkan test provider yang tidak diperlukan.

Setelah implementasi selesai, jalankan validation:

* pnpm test
* pnpm build
* pnpm typecheck
* pnpm lint
* pnpm format:check
* scripts/check-imports.mjs
* scripts/check-symlinks.mjs
* scripts/check-ownership.mjs
* scripts/check-doc-links.mjs
* git diff --check

Jika semua PASS:
12. Buat commit lokal dengan message yang sesuai, misalnya:
`feat: implement storage adapter foundation`
gunakan message yang lebih tepat jika perubahan berbeda.

13. Setelah commit berhasil, LANGSUNG coba:
    `git push origin backend-dev-recovery`

14. Jika push berhasil, tampilkan SHA commit dan status remote.

15. Jika push gagal karena credential GitHub, jangan mengubah konfigurasi credential secara sembarangan. Pastikan commit tetap aman secara lokal dan tampilkan error push secara jelas.

16. Setelah tahap ini selesai, jangan mengerjakan fitur acak. Tampilkan:

* commit SHA,
* push status,
* validation status,
* file yang berubah,
* remaining issues,
* roadmap/task berikutnya yang paling tepat berdasarkan dependency repository.

Kerjakan langsung pada repository `/root/botspace`.


```
# BotSpace — Continue Module Command Routing
```

Lanjutkan implementasi project BotSpace dari kondisi repository saat ini.

Konteks:
- Commit terakhir sudah berhasil:
  24ecd5718ef3069f99a3416f594c472a29181bf0
- Commit message:
  feat: add module command routing runtime
- Validation terakhir sudah PASS:
  - pnpm test: 10 tests passed
  - pnpm build: 12 packages successful
  - pnpm typecheck: 12 packages successful
  - pnpm lint: 12 packages successful
  - pnpm format:check: PASS
  - scripts/check-imports.mjs: PASS
  - scripts/check-symlinks.mjs: PASS
  - scripts/check-ownership.mjs: PASS
  - scripts/check-doc-links.mjs: PASS
  - git diff --check: PASS
- Jangan mengulang implementasi yang sudah selesai.
- Jangan mengubah arsitektur yang sudah berjalan hanya untuk merapikan kode.
- Jangan menjalankan atau mengubah integration test Gorouter.app.
- Fokus pada BotSpace dan lanjutkan roadmap dari kondisi repository sekarang.

Tugas:
1. Audit implementasi `module command routing runtime` yang baru selesai.
2. Identifikasi bagian berikutnya yang memang diperlukan agar module command routing dapat digunakan oleh runtime BotSpace secara nyata.
3. Implementasikan bagian tersebut secara modular dan konsisten dengan arsitektur repository.
4. Pastikan routing command:
   - menggunakan module yang benar,
   - memiliki boundary yang jelas antara runtime dan adapter,
   - tidak merusak command/module yang sudah ada,
   - mudah ditambah untuk module baru di masa depan.
5. Jangan membuat persistence adapter baru atau storage contract baru jika schema/kontrak produknya memang belum tersedia. Jangan mengarang schema.
6. Tambahkan atau perbarui unit test hanya untuk behavior yang benar-benar berubah/ditambahkan.
7. Jalankan validation yang relevan:
   - tests
   - build
   - typecheck
   - lint
   - format check
   - import/symlink/ownership/doc-link checks bila relevan
   - git diff --check
8. Jangan melakukan push GitHub. Credential push sebelumnya memang tidak tersedia; cukup pastikan commit lokal siap dibuat.
9. Setelah selesai, tampilkan:
   - ringkasan perubahan,
   - file yang diubah,
   - hasil test/validation,
   - masalah yang masih tersisa jika ada,
   - rekomendasi langkah BotSpace berikutnya.
10. Jika semua validasi PASS, buat satu commit lokal dengan commit message yang jelas sesuai perubahan.

Kerjakan langsung pada repository saat ini. Jangan berhenti hanya pada audit; implementasikan tahap berikutnya yang memang sudah siap dikerjakan berdasarkan kode yang ada.

```
# Prompt: B-061 — Command Routing + Module RuntimePrompt: B-061 — Command Routing + Module Runtime
```

Implement ROADMAP_V2.md task B-061 — Command routing + module runtime.

IMPORTANT:
- Work ONLY on B-061.
- B-060 is already completed and pushed. Treat the existing Module Manifest Registry from B-060 as the source of truth.
- Do NOT redesign or rewrite B-060 unless a small compatibility fix is strictly required by B-061.
- Do NOT start B-062 or any later task.
- Do NOT implement frontend F-060 yet.
- Preserve all existing contracts and tenant/workspace isolation rules.
- Do not introduce secrets, bot tokens, credentials, or raw Telegram credentials into logs, errors, tests, fixtures, or responses.
- Do not weaken existing tests or security checks.
- Follow the repository architecture, ADRs, MODULES.md, API contracts, and ROADMAP_V2.md.
- Use the existing domain/repository ports instead of creating duplicate provider/module layers.

TASK:
Implement B-061:
"Command routing + module runtime"

Roadmap requirement:
"Route normalized Telegram updates to enabled modules per bot; per-workspace module configuration."

Expected result:
"Module commands execute isolated per workspace/bot."

SCOPE:

1. AUDIT EXISTING B-060 IMPLEMENTATION FIRST
   - Inspect the current Module Manifest Registry implementation.
   - Identify:
     - module manifest types
     - module IDs/names
     - enabled/disabled semantics
     - workspace/bot configuration model
     - repository ports/adapters
     - existing tests
   - Reuse these contracts.
   - Do not invent a second module registry.

2. DEFINE/IMPLEMENT NORMALIZED UPDATE ROUTING
   - Locate the existing Telegram update normalization/input boundary created by previous tasks.
   - Use the normalized update/domain representation rather than parsing raw Telegram payloads inside modules.
   - Introduce a clear command-routing flow:
       normalized update
          -> resolve bot/workspace context
          -> resolve enabled modules
          -> identify matching module command
          -> execute module handler
          -> return safe result
   - Keep routing deterministic and testable.

3. MODULE RUNTIME
   - Create a small module runtime abstraction responsible for executing an enabled module command.
   - A module must receive only the context it needs.
   - Runtime context must include the resolved tenant/workspace and bot identity.
   - Never trust a workspace ID supplied by a Telegram/client payload.
   - Workspace/bot context must come from the trusted server-side resolution path already established in the repository.

4. COMMAND REGISTRATION / DISPATCH
   - Support module-defined commands based on the B-060 manifest.
   - Only commands belonging to ENABLED modules for the current bot/workspace may execute.
   - Disabled modules must not execute.
   - Unknown commands must produce the existing safe "not handled"/equivalent result rather than an exception.
   - Multiple modules must not accidentally execute the same command unless the existing architecture explicitly supports deterministic priority/ownership.
   - If command collisions are possible, detect them deterministically and fail safely.

5. WORKSPACE/BOT ISOLATION
   - Module configuration must be resolved for the current workspace + bot.
   - Workspace A must never execute a module configuration belonging to Workspace B.
   - Bot A must never inherit module configuration from Bot B unless explicitly defined by an existing repository contract.
   - Do not use a global mutable module configuration cache that can leak tenant state.
   - If caching is necessary, key it by the correct tenant/workspace/bot scope.

6. ERROR AND SECURITY BEHAVIOR
   - Follow the existing error envelope/domain error conventions.
   - Do not expose provider errors, Telegram credentials, bot tokens, secret references, or raw upstream payloads.
   - Do not log raw Telegram updates if they may contain sensitive data.
   - Preserve correlation context and workspace/tenant context in structured logs where the existing observability layer supports it.
   - A module failure must not corrupt the runtime/router state.
   - One workspace/bot failure must not affect another workspace/bot.

7. TESTS
   Add focused tests for B-061 covering at minimum:

   A. Enabled module command executes.
   B. Disabled module command does not execute.
   C. Unknown command is safely ignored/not handled.
   D. Workspace isolation:
      - workspace A cannot execute workspace B module configuration.
   E. Bot isolation:
      - bot A cannot accidentally use bot B module configuration.
   F. Command collision behavior is deterministic/safe.
   G. Module runtime receives the correct workspace/bot context.
   H. Module failure is isolated and returned through the existing error/result mechanism.
   I. No token/secret/raw credential appears in logs/errors.
   J. Empty/no-module configuration behaves safely.
   K. Multiple enabled modules can coexist without cross-execution.
   L. Repeated routing of the same normalized update does not mutate shared global state unexpectedly.

8. ARCHITECTURE
   - Keep module runtime independent from Telegram SDK-specific details where possible.
   - Keep Telegram adapter/input parsing separate from domain/module execution.
   - Use repository ports for persistence/configuration.
   - Avoid circular dependencies.
   - Respect package import boundaries.
   - Do not add unnecessary dependencies.

9. DOCUMENTATION
   - Update documentation only if B-061 genuinely changes the documented architecture/contract.
   - Do NOT modify ROADMAP.md.
   - ROADMAP_V2.md may only be updated if the repository convention requires marking B-061 DONE, and only after all implementation/tests/validation succeed.
   - Do not create another README or roadmap file.

10. VALIDATION
   Before declaring B-061 complete, run the repository's appropriate validation suite, including where available:

   pnpm format:check
   pnpm lint
   pnpm typecheck
   node scripts/check-imports.mjs
   pnpm test
   pnpm build

   Also run focused B-061 tests explicitly if the workspace supports it.

   Do not hide failures.
   Do not skip tests just to obtain a green result.
   If PostgreSQL/runtime integration tests are gated by the existing environment, report exactly which tests were gated and why.

11. GIT SAFETY — VERY IMPORTANT
   The VPS can disappear, so NEVER leave completed work only as an uncommitted working tree.

   After implementation and successful validation:

   git status --short
   git diff --check

   Review the diff and ensure there are no unrelated changes.

   Then create a dedicated commit:

   git add <only B-061 files>
   git commit -m "feat: add module command routing runtime"

   Verify:

   git status --short
   git log -1 --oneline

   Then PUSH the commit to the current working branch and verify the remote contains it.

   If authentication prevents push:
   - DO NOT delete/reset/rebase the commit.
   - Keep the commit safely in local Git history.
   - Report the exact push failure.
   - Show the commit SHA and branch.
   - Do not claim the task is pushed.

12. FINAL REPORT
   At the end report:
   - B-061 implementation summary
   - files changed
   - tests added
   - validation results
   - security/tenant-isolation verification
   - commit SHA
   - branch
   - push result
   - working-tree status
   - any remaining risks

Success condition:
B-061 is complete only when command routing and module runtime work through the existing B-060 module registry, module execution is correctly scoped to workspace+bot, tests pass, validation passes, and the implementation is committed. Push it when credentials are available.

```
# 
```
PROMPT: Lanjut Roadmap Setelah B-052

Lanjutkan pekerjaan BotSpace dari state repository saat ini.

KONDISI:
- B-050 selesai.
- B-051 selesai.
- B-052 selesai.
- Semua validation terakhir hijau.
- Commit terakhir sudah dibuat dan SUDAH di-push ke remote.
- Working tree harus dianggap sebagai checkpoint aman.

ATURAN:
1. Jangan mengulang atau mengubah implementasi B-050, B-051, atau B-052 kecuali diperlukan untuk compatibility.
2. Audit roadmap terlebih dahulu dan tentukan task BACKEND berikutnya setelah B-052.
3. Baca ADR, ROADMAP, FLOWS.md, contracts, serta implementasi existing sebelum coding.
4. Kerjakan hanya SATU task roadmap berikutnya.
5. Jangan mengerjakan task frontend/UI yang belum menjadi dependency task tersebut.
6. Jangan membuat arsitektur baru jika contract/domain primitive yang diperlukan sudah tersedia.
7. Pertahankan tenant/workspace isolation.
8. Pertahankan security rule:
   - jangan menyimpan plaintext token/secret
   - jangan memasukkan credential ke log/error/test output
   - gunakan opaque reference seperti BotInstallationId/secretRef sesuai contract.
9. Gunakan existing repository/adapter/port pattern.
10. Jangan menggunakan fake implementation untuk menggantikan contract production tanpa alasan yang ditentukan roadmap.
11. Tambahkan test/evidence sesuai acceptance criteria task.
12. Jalankan validation yang relevan setelah implementasi:
    - pnpm build
    - pnpm typecheck
    - pnpm lint
    - pnpm format:check
    - pnpm test
    - migration test jika task menyentuh database
13. Jangan menghapus test existing.
14. Jangan melakukan reset, rebase, squash, amend, atau force-push.
15. Jika semua validation hijau:
    - git add perubahan
    - git commit dengan message yang jelas
    - git push branch aktif ke remote
16. Setelah push, tampilkan:
    - task/ID yang dikerjakan
    - ringkasan implementasi
    - test/validation result
    - commit hash
    - branch
    - status push
    - working tree status
    - remaining risks
17. Jika menemukan dependency yang belum selesai, JANGAN melompati kontrak atau membuat workaround sembarangan. Audit dependency tersebut dan jelaskan task yang memang harus dikerjakan lebih dahulu.

MULAI:
Audit roadmap sekarang, tentukan task berikutnya setelah B-052, lalu langsung kerjakan task tersebut sampai validation selesai dan commit + push berhasil.
Jangan bertanya konfirmasi untuk hal yang sudah jelas dari roadmap.


```
# 
```

TASK: FINALIZE AND COMMIT CURRENT WORK

Validation terakhir sudah hijau. Jangan melakukan perubahan kode baru.

1. Periksa git status.
2. Periksa branch aktif.
3. Periksa commit terakhir.
4. Pastikan tidak ada perubahan yang tidak sengaja di luar scope task ini.
5. Jika semua perubahan memang bagian dari task yang baru selesai:
   - git add perubahan yang relevan
   - buat git commit dengan message yang jelas sesuai task
6. Setelah commit, jalankan:
   git status --short
   git log -1 --oneline
7. Pastikan working tree clean.
8. Jika remote origin tersedia dan autentikasi berhasil, push branch aktif ke remote.
9. Setelah push, verifikasi bahwa commit lokal sama dengan commit remote.
10. Jangan amend, reset, rebase, squash, atau force-push.
11. Jangan mengubah source code lagi.

LAPORKAN:
- branch aktif
- commit hash
- commit message
- jumlah file yang di-commit
- status working tree
- apakah commit sudah berhasil dipush ke remote

Ini adalah checkpoint wajib sebelum task berikutnya.

```
# Bot Runtime & Execution Integrity
```
PROMPT: BotSpace — Bot Runtime & Execution Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint security dan lifecycle yang SUDAH BERHASIL.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Remote:
 https://github.com/zenolamee/botspace.git

Kondisi verification terakhir:

- Domain: 110 passed
- API: 121 passed, 3 skipped karena PostgreSQL gating default
- Auth/Session: PASS
- Workspace authorization: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- PostgreSQL adapter/runtime: 3 passed
- PostgreSQL integration berhasil dijalankan menggunakan PostgreSQL lokal
- pnpm check: 44 successful
- Typecheck: 11 successful
- Lint: 11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Migration: 31 passed, 0 failed
- Build: 11 successful
- git diff --check: PASS
- Working tree terakhir clean

Checkpoint terakhir mencakup hardening bot lifecycle dan pengujian idempotency lifecycle.

JANGAN:

- reset
- force push
- rebase sembarangan
- checkout branch lain
- merge ke backend-dev
- menghapus checkpoint yang sudah ada
- mengubah remote Git
- menghapus test existing
- skip test hanya agar verification terlihat PASS

Jika push gagal karena credential GitHub, jangan mengubah source code hanya untuk mengatasi masalah credential. Pertahankan commit lokal.

==================================================
TUJUAN
==================================================

Sekarang fokus pada:

BOT RUNTIME
→ START/STOP
→ ENABLE/DISABLE
→ WORKER LIFECYCLE
→ DUPLICATE RUNTIME PREVENTION
→ GRACEFUL SHUTDOWN
→ RESTART SAFETY
→ WORKSPACE ISOLATION
→ CREDENTIAL SECURITY
→ STATE CONSISTENCY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Tujuan tahap ini bukan membuat sistem bot runtime baru.

Tujuan utamanya adalah memastikan runtime bot yang SUDAH ADA tidak dapat menghasilkan:

- duplicate worker
- bot aktif tetapi database inactive
- bot inactive tetapi worker tetap berjalan
- worker dari workspace lain menggunakan credential bot
- worker lama tetap berjalan setelah disable
- worker baru berjalan dua kali karena retry
- process crash meninggalkan state yang salah
- credential bocor ke log/error
- lifecycle API menghasilkan runtime yang tidak konsisten

Gunakan architecture repository yang sebenarnya.

Jangan mengarang abstraction yang tidak ada.

==================================================
1. AUDIT BOT RUNTIME YANG SUDAH ADA
==================================================

Sebelum mengubah kode, audit seluruh repository.

Cari implementasi yang berkaitan dengan:

- bot runtime
- bot runner
- bot worker
- bot process
- bot service
- bot manager
- bot executor
- bot start
- bot stop
- bot enable
- bot disable
- bot restart
- polling
- webhook
- Telegram client
- Telegram bot token
- runtime registry
- active bot registry
- worker registry
- process manager
- queue
- job
- scheduler
- background worker
- graceful shutdown
- application shutdown
- process shutdown
- SIGTERM
- SIGINT
- startup initialization

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat runtime framework baru jika repository sudah memiliki implementation.

==================================================
2. PAHAMI RELASI DATABASE VS RUNTIME
==================================================

Tentukan dengan jelas:

DATABASE STATE

dan

RUNTIME STATE

Audit apakah project saat ini memiliki state seperti:

- active
- inactive
- enabled
- disabled
- running
- stopped
- pending
- failed
- starting
- stopping

Jangan membuat state baru hanya agar terlihat lebih lengkap.

Gunakan state yang memang sudah ada.

Jika database hanya menyimpan enabled/disabled sedangkan runtime memiliki running/stopped secara internal, dokumentasikan hubungan keduanya secara jelas.

Pastikan:

enabled
≠
harus selalu running jika architecture memang tidak menjamin runtime aktif terus-menerus.

Jangan mengubah semantics existing tanpa bukti dari code.

==================================================
3. START BOT
==================================================

Audit seluruh flow start bot.

Pastikan:

authentication
→ workspace authorization
→ bot authorization
→ lifecycle validation
→ credential resolution
→ runtime start

dilakukan dalam urutan yang aman.

User tidak boleh dapat menjalankan bot workspace lain hanya dengan mengetahui:

botId

atau:

workspaceId

Pastikan runtime mendapatkan bot dari authorization context yang benar.

==================================================
4. ENABLE VS START
==================================================

Periksa apakah:

enable bot

dan:

start bot

merupakan operasi yang sama atau berbeda dalam architecture.

Jangan menggabungkan keduanya jika repository memang memisahkannya.

Jika enable hanya mengubah database state:

jangan secara otomatis membuat runtime behavior baru tanpa alasan.

Jika enable memang memulai runtime:

pastikan behavior tersebut konsisten dan idempotent.

Gunakan semantics existing.

==================================================
5. DISABLE VS STOP
==================================================

Audit:

disable bot

dan:

stop bot.

Pastikan tidak terjadi:

database disabled
tetapi worker masih berjalan tanpa alasan.

Jika architecture memang mengizinkan worker berhenti secara asynchronous, pastikan ada mekanisme yang benar untuk menyelesaikan shutdown.

Jangan menganggap perubahan database otomatis menghentikan process jika runtime implementation tidak melakukan itu.

==================================================
6. DUPLICATE WORKER PREVENTION
==================================================

Ini WAJIB diperiksa.

Cari apakah request seperti:

POST start bot

dipanggil dua kali secara bersamaan dapat membuat:

worker A
worker B

untuk bot yang sama.

Contoh:

Request 1:
start bot-A

Request 2:
start bot-A

secara bersamaan.

Expected:

hanya satu runtime aktif untuk bot-A.

Audit mechanism yang sudah tersedia:

- in-memory registry
- database state
- unique constraint
- lock
- transaction
- atomic update
- runtime manager
- queue
- job deduplication

Gunakan mechanism existing jika tersedia.

Jangan membuat distributed locking system baru hanya untuk task ini.

==================================================
7. IDEMPOTENT START
==================================================

Pastikan:

start bot yang sudah running

tidak membuat worker kedua.

Behavior harus mengikuti architecture.

Contoh:

running
→ start

hasil:

tidak membuat duplicate runtime.

Jika API memang seharusnya mengembalikan conflict/already-running, gunakan error convention existing.

Jangan membuat error system baru.

==================================================
8. IDEMPOTENT STOP
==================================================

Pastikan:

stop bot yang sudah stopped

tidak menyebabkan error internal atau crash.

Pastikan:

stop bot yang tidak memiliki runtime

ditangani sesuai behavior existing.

Jangan melakukan cleanup terhadap runtime bot lain.

==================================================
9. ENABLE/DISABLE RACE CONDITION
==================================================

Audit kondisi:

Request A:
enable bot

Request B:
disable bot

dijalankan hampir bersamaan.

Cari kemungkinan:

database:
disabled

runtime:
running

atau:

database:
enabled

runtime:
stopped

Jika architecture membutuhkan consistency, gunakan abstraction transaction/atomic operation yang sudah tersedia.

Jangan membuat concurrency framework baru.

Tambahkan test jika behavior dapat diuji secara reliable.

==================================================
10. RESTART SAFETY
==================================================

Audit apa yang terjadi jika application/backend restart.

Contoh:

Bot A aktif sebelum restart.

Backend restart.

Apa yang terjadi?

Periksa architecture aktual:

- apakah bot otomatis restart?
- apakah runtime harus direhydrate?
- apakah worker registry dibangun ulang?
- apakah bot harus start manual?
- apakah database state menjadi source of truth?

Jangan mengubah behavior existing.

Jika repository sudah memiliki startup reconciliation:

audit correctness-nya.

Jika tidak ada reconciliation, jangan otomatis membuat fitur baru besar.

Dokumentasikan behavior aktual jika memang diperlukan.

==================================================
11. CRASH RECOVERY
==================================================

Audit behavior ketika runtime bot crash.

Contoh:

Bot A running.

Worker crash.

Pastikan database tidak diam-diam tetap berada pada state yang misleading jika architecture memang menyimpan runtime state.

Periksa:

- error handler
- worker exit
- promise rejection
- process error
- retry behavior
- cleanup
- runtime registry cleanup

Jangan membuat infinite retry loop.

Jangan membuat retry system baru jika belum ada abstraction.

==================================================
12. GRACEFUL SHUTDOWN
==================================================

Audit application shutdown.

Cari:

- SIGTERM
- SIGINT
- shutdown hooks
- worker shutdown
- runtime cleanup
- HTTP server shutdown
- database disconnect

Pastikan shutdown tidak meninggalkan runtime bot yang tetap berjalan jika architecture mengharuskan runtime berhenti.

Jika process manager memang menangani lifecycle tertentu, ikuti architecture tersebut.

Jangan mengubah deployment infrastructure.

Fokus source code.

==================================================
13. RUNTIME REGISTRY
==================================================

Jika project memiliki registry seperti:

Map<botId, runtime>

atau equivalent:

audit seluruh penggunaan registry.

Pastikan:

- key benar-benar botId
- runtime hanya terkait bot yang benar
- workspace tidak dapat tertukar
- stop menghapus runtime yang benar
- restart tidak membuat duplicate entry
- crash membersihkan registry
- disable membersihkan runtime sesuai architecture

Cari juga kemungkinan:

bot A start
→ registry[A]

bot B start
→ registry[B]

kemudian stop A
→ jangan sampai registry[B] ikut terhapus.

==================================================
14. MULTI-WORKSPACE ISOLATION
==================================================

Ini WAJIB diuji.

Misalnya:

workspace-A
→ bot-A
→ token-A

workspace-B
→ bot-B
→ token-B

User dari workspace-A tidak boleh menjalankan:

bot-B.

Runtime bot-A juga tidak boleh menggunakan:

token-B.

Pastikan seluruh runtime initialization menggunakan credential milik bot yang sedang dijalankan.

Jangan mengambil credential berdasarkan:

- user global
- workspace terakhir
- environment default
- bot lain
- global mutable variable

jika architecture tidak mengizinkannya.

==================================================
15. CREDENTIAL SECURITY
==================================================

Audit credential handling pada runtime.

Cari:

- Telegram bot token
- API key
- webhook secret
- integration credential
- session credential
- provider secret

Pastikan credential tidak:

- masuk log
- masuk error message
- masuk exception message
- masuk analytics
- masuk audit log plaintext
- dikembalikan ke API client tanpa alasan
- disimpan pada runtime registry secara tidak perlu

Jika runtime memang membutuhkan credential di memory, gunakan lifetime seminimal mungkin sesuai architecture.

Jangan mencetak credential saat test.

==================================================
16. RUNTIME CONFIGURATION
==================================================

Audit konfigurasi runtime bot.

Cari:

- bot settings
- polling configuration
- webhook configuration
- command configuration
- flow configuration
- integration configuration
- environment configuration

Pastikan runtime bot-A tidak mengambil configuration bot-B.

Pastikan semua resource yang digunakan runtime tetap berada dalam workspace bot.

==================================================
17. CHILD RESOURCE ACCESS DARI RUNTIME
==================================================

Jika runtime bot menggunakan:

- commands
- flows
- templates
- integrations
- settings
- webhook configuration
- analytics configuration

pastikan query/service mengambil resource berdasarkan bot/workspace yang benar.

Jangan melakukan:

findById(childId)

kemudian langsung menggunakan resource.

Pastikan parent relationship tetap diverifikasi.

Audit seluruh runtime path.

==================================================
18. RUNTIME AUTHORIZATION
==================================================

Runtime internal tidak boleh menjadi bypass authorization.

Misalnya jangan sampai:

API:
user tidak punya akses bot

tetapi:

runtime service menerima botId
dan menjalankan bot tanpa memastikan bot tersebut valid.

Bedakan:

USER-FACING AUTHORIZATION

dengan:

INTERNAL TRUST BOUNDARY.

Internal service boleh dipercaya hanya jika caller memang trusted.

Namun jangan membuat endpoint publik yang dapat memanggil internal runtime service tanpa authorization.

==================================================
19. API INPUT VALIDATION
==================================================

Audit endpoint runtime:

- start
- stop
- restart
- enable
- disable
- status

Validasi:

- botId
- workspaceId jika memang digunakan
- operation
- state
- configuration

Jangan menerima field privilege dari client.

Jangan menerima:

ownerId
accountId
role
permissions

sebagai sumber authorization.

==================================================
20. STATUS ENDPOINT
==================================================

Jika project memiliki endpoint status bot:

audit apakah status response benar-benar aman.

Pastikan user hanya dapat melihat status bot yang boleh dia akses.

User workspace-A tidak boleh:

GET status bot-B

hanya karena mengetahui botId.

Jika runtime status bersifat internal, jangan membocorkan detail process internal yang tidak diperlukan.

==================================================
21. ERROR HANDLING RUNTIME
==================================================

Gunakan error system yang sudah ada.

Pastikan:

unauthenticated
→ authentication error

unauthorized
→ authorization error

bot tidak ditemukan
→ not found sesuai convention

invalid lifecycle transition
→ domain/validation error sesuai convention

runtime gagal start
→ runtime/application error sesuai convention

Jangan mengembalikan:

- stack trace
- token
- credential
- database connection string
- SQL detail
- internal process environment

ke client production.

==================================================
22. TEST MATRIX
==================================================

Tambahkan/perbaiki test sesuai runtime yang benar-benar tersedia.

START:

- authorized start = PASS
- unauthenticated start = DENY
- unauthorized start = DENY
- cross-workspace start = DENY
- nonexistent bot = handled
- repeated start = no duplicate runtime

STOP:

- authorized stop = PASS
- unauthorized stop = DENY
- cross-workspace stop = DENY
- repeated stop = safe
- nonexistent runtime = handled

ENABLE:

- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY
- repeated enable = idempotent

DISABLE:

- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY
- repeated disable = idempotent

RUNTIME:

- bot-A cannot start using bot-B credential
- bot-A runtime does not affect bot-B
- stopping bot-A does not stop bot-B
- duplicate start does not create duplicate worker
- runtime cleanup occurs correctly

CREDENTIAL:

- token not logged
- token not returned unexpectedly
- token not included in errors
- token not leaked in test output

==================================================
23. CONCURRENCY TEST
==================================================

Jika runtime implementation memungkinkan testing concurrency secara reliable, tambahkan test:

start bot-A
+
start bot-A

secara bersamaan.

Expected:

satu runtime.

Jika testing concurrency tidak reliable dengan current architecture:

jangan membuat flaky test.

Sebagai gantinya, audit mechanism yang menjamin idempotency dan buat test deterministic pada abstraction yang sudah tersedia.

==================================================
24. REGRESSION TEST
==================================================

Semua checkpoint security sebelumnya harus tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization
- bot lifecycle
- persistence
- API input validation

Jangan melemahkan test existing.

==================================================
25. DATABASE CONSISTENCY
==================================================

Jika runtime lifecycle menggunakan database:

audit seluruh mutation.

Pastikan tidak ada sequence seperti:

1. start runtime
2. database update gagal
3. runtime tetap berjalan tanpa state yang benar

atau:

1. database state berubah
2. runtime start gagal
3. state menjadi misleading

Gunakan transaction atau abstraction existing jika memang diperlukan.

Jangan membuat distributed transaction system baru.

Jika architecture memang asynchronous, pertahankan semantics tersebut dan pastikan failure behavior jelas.

==================================================
26. TYPECRIPT QUALITY
==================================================

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate runtime manager
- tidak ada duplicate lifecycle implementation
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- tidak ada global mutable state baru tanpa alasan
- tidak ada unhandled promise rejection

Gunakan abstraction existing.

==================================================
27. DOCUMENTATION
==================================================

Jika diperlukan, update README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

- bot runtime lifecycle
- hubungan enable/disable dengan runtime
- start/stop behavior
- runtime isolation
- shutdown behavior
- test command

Jangan membuat dokumentasi panjang jika tidak diperlukan.

==================================================
28. VERIFICATION WAJIB
==================================================

Setelah implementation selesai, jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- auth/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- runtime tests jika tersedia
- PostgreSQL integration jika memang digunakan oleh test architecture
- pnpm check
- typecheck
- lint
- format check
- import boundary check
- build
- git diff --check

Jangan skip test.

Jika PostgreSQL integration memang merupakan explicit verification path repository, jalankan dengan PostgreSQL lokal yang tersedia.

Jangan menjalankan test provider/integration yang tidak relevan dengan BotSpace runtime task ini.

Jika ada failure:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

==================================================
29. GIT AUDIT
==================================================

Sebelum commit:

```bash
git status
git diff --stat
git diff


```
# 
```
PROMPT: BotSpace — Production Runtime Persistence & PostgreSQL Consistency Hardening

Kita melanjutkan project BotSpace dari checkpoint TERBARU yang SUDAH BERHASIL diverifikasi secara lokal.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Project:
 BotSpace

TUJUAN UTAMA

Lanjutkan hardening production runtime setelah tahap:

AUTHENTICATION
→ WORKSPACE AUTHORIZATION
→ MEMBERSHIP
→ BOT RESOURCE AUTHORIZATION
→ BOT LIFECYCLE
→ IDEMPOTENCY
→ API PERSISTENCE CONTRACT

sudah berhasil.

Fokus tahap ini:

PRODUCTION RUNTIME
→ DATABASE PERSISTENCE
→ POSTGRESQL CONSISTENCY
→ BOT STATE PERSISTENCE
→ SESSION PERSISTENCE
→ TRANSACTION SAFETY
→ ERROR RECOVERY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

JANGAN membuat fitur besar baru.

JANGAN membuat authorization system baru.

JANGAN mengganti arsitektur database secara besar-besaran.

Gunakan abstraction dan repository yang sudah ada.

==================================================
1. AUDIT RUNTIME PERSISTENCE
==================================================

Sebelum mengubah kode, audit implementasi aktual repository.

Cari seluruh jalur persistence yang berkaitan dengan:

- bot
- workspace
- membership
- session
- account
- bot status
- bot configuration
- bot credentials
- bot resources
- lifecycle mutation
- enable
- disable
- create
- update
- delete

Pahami flow:

API
→ SERVICE
→ DOMAIN
→ REPOSITORY
→ DATABASE

Jangan langsung menulis kode sebelum memahami flow aktual.

==================================================
2. POSTGRESQL RUNTIME PATH
==================================================

Pastikan production runtime menggunakan adapter/database abstraction yang memang dimaksudkan repository.

Audit:

- PostgreSQL adapter
- repository implementation
- database connection
- transaction handling
- persistence methods
- error mapping
- runtime initialization

Pastikan tidak ada code path production yang diam-diam menggunakan:

- in-memory state
- mock repository
- test database
- SQLite fallback
- temporary storage

kecuali architecture memang secara eksplisit mendukungnya.

Jangan menghapus fallback yang memang dibutuhkan oleh test environment.

Pisahkan dengan jelas:

TEST RUNTIME

dan

PRODUCTION RUNTIME.

==================================================
3. BOT STATE PERSISTENCE
==================================================

Audit state bot.

Jika repository menggunakan status seperti:

- active
- inactive
- disabled
- pending
- stopped

gunakan state yang benar-benar sudah ada.

Jangan membuat state baru.

Pastikan ketika bot di-enable:

request
→ authorization
→ state mutation
→ persistence
→ response

dan ketika bot di-disable:

request
→ authorization
→ state mutation
→ persistence
→ response

State yang dikembalikan API harus sesuai dengan state yang benar-benar tersimpan.

==================================================
4. READ-AFTER-WRITE
==================================================

Tambahkan/perbaiki verification untuk memastikan:

CREATE
→ WRITE DATABASE
→ READ DATABASE
→ hasil konsisten

UPDATE
→ WRITE DATABASE
→ READ DATABASE
→ hasil konsisten

ENABLE
→ WRITE DATABASE
→ READ DATABASE
→ status tetap benar

DISABLE
→ WRITE DATABASE
→ READ DATABASE
→ status tetap benar

DELETE
→ DELETE/soft-delete sesuai architecture
→ READ
→ behavior sesuai contract.

Jangan mengubah soft delete menjadi hard delete atau sebaliknya.

==================================================
5. RESTART PERSISTENCE
==================================================

Audit kemungkinan kehilangan state setelah process restart.

Jika bot telah:

- dibuat
- di-enable
- di-disable
- dikonfigurasi

pastikan state tidak hanya berada di memory process.

Database harus menjadi sumber persistence sesuai architecture.

Jika runtime process dimulai kembali:

database state
→ repository
→ service
→ runtime

harus tetap konsisten.

Jangan membuat persistence framework baru.

==================================================
6. TRANSACTION SAFETY
==================================================

Cari mutation yang membutuhkan beberapa operasi database.

Contoh:

bot creation
→ bot record
→ related resource

atau:

bot deletion
→ parent
→ dependent resource

atau:

membership update
→ permission/role relation

Periksa apakah operasi tersebut sudah menggunakan transaction abstraction.

Jika transaction sudah tersedia:

gunakan abstraction tersebut.

Jika transaction tidak diperlukan:

jangan menambahkan transaction hanya untuk terlihat lebih aman.

Jika ditemukan bug nyata berupa partial write:

perbaiki dengan perubahan minimal.

Jangan membuat transaction framework baru.

==================================================
7. PARTIAL FAILURE
==================================================

Audit kondisi:

operation A berhasil

operation B gagal

Pastikan tidak meninggalkan database dalam state invalid.

Contoh:

create bot
→ database insert berhasil
→ related operation gagal

atau:

disable bot
→ state berubah
→ operation lanjutan gagal.

Pastikan behavior mengikuti architecture.

Jika repository sudah menggunakan transaction:

pastikan rollback benar-benar terjadi.

Tambahkan test hanya untuk failure scenario yang relevan.

==================================================
8. DATABASE ERROR MAPPING
==================================================

Audit error dari PostgreSQL/database.

Pastikan database error tidak bocor langsung ke API response.

Contoh jangan membocorkan:

- SQL statement
- connection string
- database hostname
- credentials
- internal table structure
- stack trace

Gunakan error mapping yang sudah tersedia.

Pastikan:

database failure
→ internal/application error sesuai convention

validation failure
→ validation error

not found
→ not found

authorization failure
→ authorization error.

Jangan membuat error system kedua.

==================================================
9. CONCURRENCY
==================================================

Audit mutation yang mungkin terjadi bersamaan.

Contoh:

Request A:
enable bot

Request B:
disable bot

atau:

Request A:
update bot

Request B:
delete bot

Periksa apakah repository/database dapat menghasilkan:

- lost update
- invalid state
- stale state
- orphan resource
- inconsistent response.

Gunakan transaction/atomic operation yang sudah tersedia jika memang diperlukan.

Jangan membuat concurrency framework baru.

==================================================
10. IDEMPOTENCY REGRESSION
==================================================

Checkpoint sebelumnya sudah memverifikasi bot lifecycle idempotency.

Jangan merusaknya.

Pastikan operasi berulang tetap aman sesuai contract:

enable → enable

disable → disable

delete → delete

logout → logout

revoke → revoke

Periksa bahwa persistence layer tidak mengubah behavior menjadi error atau state korup secara tidak sengaja.

Jika architecture memang menganggap operasi kedua sebagai no-op, pertahankan behavior tersebut.

Jangan mengubah contract tanpa alasan.

==================================================
11. SESSION PERSISTENCE
==================================================

Audit session persistence.

Pastikan:

- session dibuat secara benar
- session tersimpan sesuai architecture
- expired session tidak dianggap valid
- revoked session tidak dianggap valid
- logout benar-benar mempengaruhi persistence
- restart process tidak membuat session invalid secara tidak sengaja jika architecture mengharuskan persistence
- session tidak dapat digunakan untuk impersonation.

Jangan mengganti session architecture secara besar-besaran.

==================================================
12. WORKSPACE / MEMBERSHIP PERSISTENCE
==================================================

Pastikan relasi:

User
→ Account
→ Workspace
→ Membership
→ Bot

tetap konsisten setelah database write/read.

Audit kemungkinan:

- workspaceId salah
- accountId salah
- ownerId salah
- membership workspace mismatch
- bot workspace mismatch
- orphan membership
- orphan bot

Jangan memperbaiki data production secara otomatis.

Fokus pada enforcement dan test.

==================================================
13. FOREIGN KEY / RELATION INTEGRITY
==================================================

Audit database relation yang memang tersedia.

Periksa:

- foreign key
- unique constraint
- nullable relation
- cascade behavior
- delete behavior

Jangan membuat migration besar.

Jika constraint sudah ada:

gunakan behavior tersebut.

Jika constraint tidak ada dan ditemukan bug nyata:

evaluasi perubahan minimal.

Jangan mengubah production database secara langsung.

==================================================
14. DUPLICATE CREATION
==================================================

Audit kemungkinan duplicate resource.

Periksa hanya business rule yang memang sudah ada:

- duplicate bot identifier
- duplicate external identifier
- duplicate membership
- duplicate session identifier
- duplicate workspace relation

Jangan menciptakan business rule baru tanpa bukti dari architecture.

Jika database sudah memiliki unique constraint:

pastikan error-nya ditangani dengan benar.

==================================================
15. CACHE / IN-MEMORY STATE
==================================================

Cari penggunaan:

- Map
- object cache
- singleton state
- global variable
- process memory
- temporary runtime registry

Pastikan tidak ada state penting yang seharusnya persistent tetapi hanya disimpan di memory.

Jika memang ada runtime cache:

pastikan cache tidak menjadi sumber kebenaran untuk ownership, authorization, atau persistence.

Database tetap menjadi source of truth sesuai architecture.

==================================================
16. API PERSISTENCE CONTRACT
==================================================

Audit API yang melakukan mutation.

Untuk setiap mutation:

request
→ validation
→ authentication
→ authorization
→ domain/service
→ persistence
→ response

Pastikan response tidak dikirim sebelum persistence berhasil.

Jangan melakukan:

mutation sukses di response
padahal database write gagal.

Jika write gagal:

response harus failure sesuai error convention.

==================================================
17. DATABASE RELOAD TEST
==================================================

Jika test architecture memungkinkan:

buat verification:

1. create resource
2. persist
3. reload repository/database state
4. verify resource
5. update
6. reload
7. verify update
8. delete/disable
9. reload
10. verify final state

Jangan membuat test yang bergantung pada implementation detail yang tidak penting.

Fokus pada persistence contract.

==================================================
18. REGRESSION SECURITY
==================================================

Pastikan hardening persistence tidak melemahkan security sebelumnya.

Regression wajib:

Authentication:
- valid session PASS
- invalid session DENY

Workspace:
- own workspace PASS
- cross-workspace DENY

Membership:
- authorized member PASS
- unauthorized member DENY

Bot:
- own bot PASS
- cross-workspace bot DENY

Lifecycle:
- authorized enable PASS
- unauthorized enable DENY
- authorized disable PASS
- unauthorized disable DENY

Ownership:
- owner relation tetap benar

Persistence:
- state tetap benar setelah read-back.

==================================================
19. TEST MATRIX
==================================================

Tambahkan/perbaiki test hanya sesuai resource yang benar-benar tersedia.

Minimal:

Persistence:
- create → read PASS
- update → read PASS
- enable → read PASS
- disable → read PASS
- delete → read behavior PASS

Database:
- PostgreSQL adapter PASS
- repository persistence PASS
- database error mapping PASS

Lifecycle:
- repeated enable PASS
- repeated disable PASS
- repeated delete PASS sesuai contract

Session:
- create session PASS
- revoke session PASS
- expired session DENY

Security:
- cross-workspace persistence access DENY
- ownership mismatch DENY

Concurrency:
- relevant concurrent mutation behavior PASS

Jangan membuat test untuk endpoint yang tidak tersedia.

==================================================
20. TYPESCRIPT / CODE QUALITY
==================================================

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate repository
- tidak ada duplicate persistence abstraction
- tidak ada duplicate database adapter
- tidak ada hardcoded secret
- tidak ada SQL injection pattern baru
- tidak ada circular dependency baru.

Ikuti architecture repository.

==================================================
21. MIGRATION DISCIPLINE
==================================================

Jangan membuat migration hanya untuk merapikan sesuatu.

Migration hanya boleh dibuat jika:

- ada perubahan schema yang benar-benar diperlukan
- ada bug integrity yang tidak dapat diperbaiki di application layer
- perubahan minimal
- migration aman
- test migration tersedia.

Jika tidak diperlukan:

laporkan:

No migration required.

Jangan menyentuh production database.

==================================================
22. README
==================================================

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

- production persistence
- PostgreSQL runtime
- bot state persistence
- session persistence
- verification command

Jangan membuat dokumentasi panjang.

==================================================
23. FULL VERIFICATION
==================================================

Setelah implementation selesai jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- PostgreSQL integration/runtime tests jika tersedia
- pnpm check
- typecheck
- lint
- format
- import boundary
- build
- git diff --check

Jika PostgreSQL integration test memang tersedia:

JALANKAN SECARA EKSPLISIT.

Jangan mengklaim PostgreSQL runtime verified hanya berdasarkan unit test.

Jika test PostgreSQL membutuhkan:

PERSISTENCE_TEST_DATABASE_URL

gunakan database PostgreSQL test yang memang tersedia.

Jangan menyentuh production database.

==================================================
24. FAILURE HANDLING
==================================================

Jika verification gagal:

1. identifikasi root cause
2. perbaiki implementation
3. jalankan test terkait
4. jalankan full verification kembali

Jangan:

- skip test
- menghapus test
- menurunkan assertion
- mematikan integration test
- mengubah expected result hanya agar PASS.

==================================================
25. GIT AUDIT
==================================================

Sebelum commit:

git status
git diff --stat
git diff
git diff --check

Pastikan perubahan hanya terkait task ini.

Jangan commit:

- .env
- API key
- token
- credential
- database dump
- log
- temporary file
- build artifact.

==================================================
26. COMMIT
==================================================

Jika seluruh verification PASS:

buat SATU commit.

Gunakan message sesuai implementation aktual.

Contoh:

fix: harden production persistence

atau:

fix: enforce runtime persistence consistency

Pilih yang paling sesuai.

Setelah commit:

git status
git log --oneline -3

==================================================
27. PUSH
==================================================

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- reset
- rebase sembarangan
- ubah remote
- checkout branch lain
- merge ke backend-dev.

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

Pertahankan commit lokal.

Laporkan error push sebenarnya.

==================================================
28. HASIL AKHIR
==================================================

Tampilkan laporan:

Implementation:
- ...

Persistence:
- ...

PostgreSQL:
- ...

Runtime:
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
- PostgreSQL: ...
- pnpm check: ...
- Typecheck: ...
- Lint: ...
- Format: ...
- Import boundary: ...
- Build: ...
- git diff --check: ...

Migration:
- required/not required
- result

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim production runtime verified jika PostgreSQL/runtime verification belum benar-benar dijalankan.

==================================================
29. PENTING
==================================================

Jangan membuat fitur besar baru.

Jangan mengubah architecture BotSpace secara besar-besaran.

Jangan membuat database layer baru.

Jangan membuat authorization layer baru.

Jangan membuat migration besar.

Fokus hanya:

AUDIT
→ PRODUCTION RUNTIME
→ POSTGRESQL
→ PERSISTENCE
→ STATE CONSISTENCY
→ SESSION PERSISTENCE
→ TRANSACTION SAFETY
→ FAILURE RECOVERY
→ REGRESSION
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Selesaikan sampai push berhasil lalu berhenti.


```
# 
```

PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint TERBARU yang SUDAH BERHASIL secara lokal.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Checkpoint terbaru:
a52ab394c4b237cffbf5528a5d327297c1e5fe8

Commit:
docs: define bot runtime boundary

STATUS CHECKPOINT

Verification terakhir sudah PASS:

- Domain: 110 passed
- API: 120 passed, 3 skipped by default PostgreSQL gating
- Auth/Session: PASS
- Workspace authorization: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- PostgreSQL adapter/runtime: 3 passed
- pnpm check: 44 successful
- Typecheck: 11 successful
- Lint: 11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Migration: 31/31
- Build: 11 successful
- git diff --check: PASS

Working tree:
clean

PENTING:

Push ke GitHub pada checkpoint sebelumnya gagal karena environment tidak memiliki credential GitHub:

fatal: could not read Username for 'https://github.com': No such device or address

JANGAN menganggap source code gagal.

JANGAN mengubah credential GitHub.

JANGAN mengubah remote.

JANGAN membuat commit hanya untuk memperbaiki push.

Commit lokal harus dipertahankan.

Jika push kembali gagal karena credential GitHub, laporkan error sebenarnya dan berhenti setelah commit selesai.

JANGAN reset.
JANGAN force push.
JANGAN rebase sembarangan.
JANGAN checkout branch lain.
JANGAN merge ke backend-dev.

==================================================
TUJUAN
==================================================

Sekarang lanjutkan BotSpace ke tahap:

BOT LIFECYCLE
→ STATE INTEGRITY
→ RESOURCE RELATION INTEGRITY
→ PROVISIONING INTEGRITY
→ RUNTIME BOUNDARY
→ CREDENTIAL SECURITY
→ CONCURRENCY SAFETY
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Checkpoint sebelumnya sudah mendefinisikan boundary bot runtime.

Sekarang audit apakah lifecycle bot benar-benar konsisten dengan boundary tersebut.

Jangan membuat runtime engine baru.

Jangan membuat authorization system baru.

Jangan membuat permission system baru.

Gunakan abstraction yang sudah tersedia.

==================================================
1. AUDIT IMPLEMENTASI AKTUAL
==================================================

Sebelum mengubah kode, audit repository aktual.

Cari:

- Bot entity/model
- Bot repository
- Bot service
- Bot API routes
- bot creation
- bot update
- bot delete
- bot enable
- bot disable
- bot status
- bot configuration
- bot credential
- runtime registry jika ada
- runtime service jika ada
- lifecycle service jika ada
- provisioning jika ada
- child resources
- commands
- flows
- integrations
- webhooks
- settings
- logs
- statistics

Jangan mengasumsikan feature tersedia hanya karena namanya ditemukan.

Gunakan implementation aktual sebagai sumber kebenaran.

Jika suatu fitur belum ada:

JANGAN membuat fitur besar baru hanya untuk memenuhi checklist.

Fokus pada integrity dari fitur yang memang sudah tersedia.

==================================================
2. RUNTIME BOUNDARY
==================================================

Checkpoint sebelumnya mendefinisikan boundary runtime.

Sekarang verifikasi bahwa lifecycle tidak melewati boundary tersebut.

Pastikan jelas perbedaan:

DATABASE STATE

dan:

RUNTIME STATE

Jika database menyimpan:

- active
- inactive
- enabled
- disabled
- stopped
- deleted

audit semantics sebenarnya.

Jika runtime memiliki:

- starting
- running
- stopping
- stopped
- failed

audit mapping-nya.

JANGAN membuat state baru jika architecture tidak membutuhkan.

JANGAN membuat state machine kompleks jika project belum menggunakan state machine.

==================================================
3. BOT CREATION INTEGRITY
==================================================

Audit create bot.

Pastikan:

authenticated user
→ workspace access
→ permission
→ bot creation
→ workspace relation

Pastikan client tidak dapat menentukan ownership secara ilegal.

Perhatikan:

- workspaceId
- ownerId
- accountId
- createdBy
- botId
- status
- runtime metadata

Jika client mengirim:

ownerId

accountId

atau field internal lainnya,

pastikan field tersebut tidak dapat menggantikan identity server.

Server harus menentukan relation berdasarkan authentication context dan workspace authorization.

==================================================
4. WORKSPACE RELATION
==================================================

Pastikan:

bot.workspaceId

selalu mengarah ke workspace yang benar.

Audit kemungkinan:

bot.workspaceId ≠ configuration.workspaceId

bot.workspaceId ≠ credential.workspaceId

bot.workspaceId ≠ childResource.workspaceId

bot.accountId ≠ workspace.accountId

Jika child resource tidak memiliki workspaceId, pastikan parent bot relation tetap menjadi security boundary.

Jangan melakukan data repair otomatis terhadap production database.

Fokus pada enforcement dan tests.

==================================================
5. BOT UPDATE INTEGRITY
==================================================

Audit seluruh update bot.

Pisahkan:

CLIENT CONTROLLED

dengan:

SERVER CONTROLLED.

Server-controlled yang perlu diaudit:

- id
- workspaceId
- ownerId
- accountId
- createdBy
- createdAt
- updatedAt
- runtime state
- internal status
- permissions
- internal credential identifiers

Jangan menerima object database mentah dari request.

Jika endpoint update memang hanya mengizinkan configuration tertentu, gunakan explicit field mapping.

Jangan memungkinkan update biasa memindahkan bot ke workspace lain.

==================================================
6. BOT ENABLE / DISABLE
==================================================

Audit:

enable
disable
toggle status

Jika endpoint/service tersedia.

Pastikan flow:

Authentication
→ Workspace authorization
→ Bot authorization
→ Permission
→ State validation
→ Mutation/runtime operation

Jangan:

Mutation
→ baru authorization.

Pastikan user workspace lain tidak dapat mengubah status bot hanya dengan mengetahui botId.

Test:

authorized enable
→ PASS

unauthorized enable
→ DENY

cross-workspace enable
→ DENY

authorized disable
→ PASS

unauthorized disable
→ DENY

cross-workspace disable
→ DENY

==================================================
7. IDEMPOTENCY
==================================================

Audit operasi berulang.

Contoh:

enable bot yang sudah enabled

disable bot yang sudah disabled

start bot yang sudah running

stop bot yang sudah stopped

Ikuti semantics existing architecture.

Jika operation memang idempotent:

repeated request
→ tidak menghasilkan duplicate runtime atau corrupted state.

Jika operation memang seharusnya menghasilkan domain error:

ikuti behavior tersebut.

JANGAN mengubah semantics hanya untuk membuat test PASS.

==================================================
8. DUPLICATE RUNTIME
==================================================

Jika runtime start tersedia, audit kemungkinan:

request A:
start bot

request B:
start bot

dijalankan hampir bersamaan.

Pastikan tidak menghasilkan dua runtime instance jika architecture mengharuskan satu instance per bot.

Cari abstraction yang sudah ada:

- runtime registry
- process registry
- lock
- transaction
- atomic update
- unique constraint

Gunakan abstraction existing.

JANGAN membuat distributed lock system baru.

Jika protection belum tersedia dan membutuhkan perubahan architecture besar, dokumentasikan limitation tersebut.

==================================================
9. DELETE BOT
==================================================

Audit delete.

Pastikan authorization dilakukan sebelum mutation.

Test:

authorized delete
→ PASS

unauthorized delete
→ DENY

cross-workspace delete
→ DENY

deleted bot
→ update

deleted bot
→ enable

deleted bot
→ disable

deleted bot
→ start

Ikuti semantics existing repository.

Jika soft delete sudah digunakan:

PERTAHANKAN soft delete.

Jika hard delete digunakan:

audit relation terlebih dahulu.

JANGAN mengubah soft delete menjadi hard delete.

JANGAN mengubah hard delete menjadi soft delete.

==================================================
10. CHILD RESOURCE INTEGRITY
==================================================

Cari semua child resource bot.

Contoh:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- analytics
- credentials
- configuration

Untuk setiap child resource:

Pastikan authorization tidak dapat dilewati hanya dengan mengetahui child resource ID.

Contoh:

User A
→ workspace-A
→ bot-A

User B
→ workspace-B
→ bot-B
→ flow-B

User A tidak boleh:

GET flow-B

hanya karena mengetahui flowId.

Authorization harus mengikuti parent bot/workspace boundary.

==================================================
11. ORPHAN RESOURCE
==================================================

Audit kemungkinan:

parent bot deleted
→ child resource tetap dapat digunakan

atau:

child resource dibuat
→ botId tidak valid

atau:

bot dipindahkan
→ child relation tidak ikut konsisten

Jangan membuat cascade system baru.

Jika database relation sudah memiliki cascade behavior, pastikan service tidak melawannya.

Jika tidak ada cascade, jangan melakukan destructive migration besar.

Fokus pada behavior aktual dan keamanan.

==================================================
12. CREDENTIAL INTEGRITY
==================================================

Audit:

- bot token
- API key
- webhook secret
- integration credential
- access token
- refresh token

Pastikan credential:

- tidak menentukan owner
- tidak menentukan workspace
- tidak menentukan account
- tidak muncul pada list
- tidak muncul pada error
- tidak muncul pada log
- tidak muncul pada test output
- tidak dapat diubah oleh unauthorized user

Jika credential update tersedia:

authentication
→ workspace authorization
→ bot authorization
→ permission
→ credential update

Jangan mengubah credential architecture besar-besaran.

==================================================
13. PROVISIONING
==================================================

Jika provisioning bot tersedia:

audit flow:

workspace access
→ bot creation
→ configuration
→ credential
→ persistence
→ runtime registration

Pastikan kegagalan pada salah satu tahap tidak meninggalkan state yang secara jelas invalid.

Contoh:

credential invalid
→ jangan mengklaim bot fully configured jika architecture tidak memang menggunakan desired-state semantics.

runtime registration gagal
→ ikuti behavior existing.

Database failure
→ jangan meninggalkan partial relation jika transaction abstraction tersedia.

Gunakan transaction yang sudah ada.

Jangan membuat distributed transaction framework baru.

==================================================
14. DATABASE CONSISTENCY
==================================================

Audit skenario:

CASE A
runtime berhasil
database update gagal

CASE B
database update berhasil
runtime gagal

CASE C
credential update berhasil
runtime registration gagal

CASE D
runtime stop berhasil
database state update gagal

CASE E
database state update berhasil
runtime stop gagal

Tentukan behavior berdasarkan architecture aktual.

Jangan mengarang rollback mechanism baru.

Jika repository memiliki transaction/Unit of Work:

gunakan abstraction tersebut.

Jika tidak ada:

jangan membuat transaction framework besar hanya untuk task ini.

Dokumentasikan limitation jika memang diperlukan.

==================================================
15. CONCURRENCY
==================================================

Audit mutation yang dapat berjalan bersamaan:

- create
- update
- enable
- disable
- start
- stop
- delete
- credential update

Cari kemungkinan race condition.

Prioritaskan:

- duplicate runtime
- state overwrite
- relation corruption
- child resource orphan
- credential mismatch

Gunakan mechanism existing.

Jangan membuat concurrency infrastructure baru.

==================================================
16. IDOR AUDIT
==================================================

Cari seluruh pola:

findById(id)

findUnique({ id })

where: { id }

repository lookup berdasarkan ID saja.

Untuk setiap resource yang workspace-scoped:

pastikan authorization tetap dilakukan.

Jika repository abstraction memungkinkan scoped lookup:

gunakan scope yang benar.

Jangan mengganti semua query secara membabi buta.

Perubahan harus minimal dan aman.

==================================================
17. INPUT VALIDATION
==================================================

Audit request body lifecycle.

Perhatikan:

- workspaceId
- ownerId
- accountId
- status
- permissions
- role
- credential identifiers
- bot configuration
- child resource parent IDs

Pastikan privilege field tidak dapat di-mass assign.

Request body tidak boleh menjadi sumber authorization.

Gunakan schema validation yang sudah tersedia.

Jangan membuat validation framework baru.

==================================================
18. ERROR SECURITY
==================================================

Pastikan production errors tidak membocorkan:

- SQL detail
- database connection
- token
- credential
- secret
- stack trace
- workspace resource milik user lain
- runtime internals yang sensitif

Gunakan error system yang sudah tersedia.

Authentication:
→ authentication error

Unauthorized:
→ authorization error

Not found:
→ existing not-found convention

Invalid state:
→ existing domain/validation error

Jangan membuat error system kedua.

==================================================
19. TEST MATRIX
==================================================

Tambahkan atau perbaiki test sesuai implementation aktual.

Creation:

- authenticated + valid workspace = PASS
- unauthenticated = DENY
- cross-workspace = DENY
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
- accountId spoof = DENY
- permission spoof = DENY

Delete:

- authorized delete = PASS
- unauthorized delete = DENY
- cross-workspace delete = DENY

Enable:

- authorized enable = PASS
- unauthorized enable = DENY
- cross-workspace enable = DENY

Disable:

- authorized disable = PASS
- unauthorized disable = DENY
- cross-workspace disable = DENY

Runtime jika tersedia:

- authorized start = PASS
- unauthorized start = DENY
- cross-workspace start = DENY
- authorized stop = PASS
- unauthorized stop = DENY
- cross-workspace stop = DENY
- duplicate start = no duplicate runtime

Child resources:

- authorized child access = PASS
- cross-workspace child access = DENY
- invalid parent relation = DENY

Credential:

- secret tidak muncul di list
- secret tidak muncul di error
- secret tidak muncul di logs/tests

==================================================
20. REGRESSION
==================================================

Semua checkpoint sebelumnya harus tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization
- runtime boundary
- PostgreSQL adapter/runtime

Jangan menghapus atau melemahkan test existing.

==================================================
21. TYPESCRIPT QUALITY
==================================================

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate lifecycle implementation
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- mengikuti architecture repository

==================================================
22. README
==================================================

Jika diperlukan:

UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

- bot lifecycle
- runtime boundary
- state behavior
- resource integrity
- credential boundary
- verification command

Jangan membuat dokumentasi panjang di luar scope.

==================================================
23. FULL VERIFICATION
==================================================

Setelah implementation selesai:

jalankan verification resmi repository.

Minimal:

- Domain tests
- API tests
- Auth/Session
- Workspace authorization
- Membership
- Bot/Resource
- Lifecycle
- PostgreSQL adapter/runtime jika environment test tersedia
- pnpm check
- Typecheck
- Lint
- Format
- Import boundary
- Secrets scan
- Ownership check
- Documentation links
- Migration check
- Build
- git diff --check

Jika PostgreSQL integration tersedia, jangan sengaja melewati test tersebut.

Gunakan database test/local.

Jangan menyentuh production database.

Jika ada failure:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

==================================================
24. GIT AUDIT
==================================================

Sebelum commit:

git status
git diff --stat
git diff
git diff --check

Pastikan perubahan hanya berkaitan dengan task ini.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary file
- database dump
- build artifact

==================================================
25. COMMIT
==================================================

Jika seluruh verification PASS:

buat SATU commit.

Gunakan commit message sesuai implementation aktual.

Contoh:

fix: harden bot lifecycle integrity

atau:

fix: enforce bot resource lifecycle integrity

Pilih message yang paling sesuai dengan perubahan sebenarnya.

Setelah commit:

git status
git log --oneline -3

==================================================
26. PUSH
==================================================

Jalankan:

git push

Branch tetap:

backend-dev-recovery

Jangan:

- force push
- ubah remote
- checkout branch lain
- merge ke backend-dev
- reset checkpoint
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

JANGAN membuat commit tambahan.

Pertahankan commit lokal.

Laporkan error sebenarnya.

==================================================
27. HASIL AKHIR
==================================================

Tampilkan laporan:

Implementation:
- ...

Bot Lifecycle:
- ...

State Integrity:
- ...

Resource Integrity:
- ...

Runtime Boundary:
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
- Lifecycle: ...
- PostgreSQL: ...
- pnpm check: ...
- Typecheck: ...
- Lint: ...
- Format: ...
- Import boundary: ...
- Secrets scan: ...
- Ownership: ...
- Documentation links: ...
- Migration: ...
- Build: ...
- git diff --check: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working tree:
- clean/dirty

Jika push gagal karena credential, tulis:

PUSH FAILED — GitHub credential unavailable

dan tampilkan error sebenarnya.

Jangan mengklaim push berhasil jika memang gagal.

==================================================
28. BATASAN SCOPE
==================================================

Jangan membuat fitur besar baru.

Jangan membuat:

- runtime engine baru
- queue system baru
- distributed lock system baru
- authorization system baru
- permission system baru
- credential architecture baru
- database architecture baru
- provider baru
- integration baru

Gunakan abstraction yang sudah tersedia.

Fokus:

AUDIT
→ BOT LIFECYCLE
→ STATE INTEGRITY
→ RESOURCE RELATION
→ PROVISIONING
→ RUNTIME BOUNDARY
→ CREDENTIAL SECURITY
→ CONCURRENCY
→ IDOR
→ REGRESSION
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Selesaikan sampai verification dan commit selesai.

Jika push berhasil, berhenti.

Jika push gagal karena credential GitHub, jangan melakukan perubahan tambahan dan berhenti dengan commit lokal tetap aman.

```
# Bot Runtime & Provisioning Integrity
```

PROMPT: BotSpace — Bot Runtime & Provisioning Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint terakhir yang SUDAH BERHASIL diverifikasi.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

TUJUAN

Tahap sebelumnya sudah menyelesaikan dan memverifikasi:

- workspace authorization
- membership/ownership
- authentication/session
- bot resource authorization
- bot lifecycle integrity
- PostgreSQL persistence adapter
- API persistence contract
- PostgreSQL runtime/integration verification
- migration verification
- typecheck
- lint
- format
- import boundary
- build

Jangan mengulang pekerjaan tersebut kecuali diperlukan sebagai regression test.

Sekarang fokus pada:

BOT RUNTIME
→ BOT PROVISIONING
→ BOT CONFIGURATION
→ CREDENTIAL BOUNDARY
→ RUNTIME STATE CONSISTENCY
→ START/STOP/ENABLE/DISABLE
→ DATABASE/STATE CONSISTENCY
→ ERROR RECOVERY
→ TEST
→ BUILD
→ COMMIT
→ PUSH

JANGAN membuat sistem runtime baru jika abstraction yang diperlukan sudah tersedia.

JANGAN membuat provider/integration baru.

JANGAN mengubah architecture besar-besaran.

==================================================
1. AUDIT IMPLEMENTASI BOT RUNTIME
==================================================

Sebelum mengubah kode, audit repository aktual.

Cari seluruh implementasi yang berhubungan dengan:

- bot runtime
- bot service
- bot lifecycle
- bot provisioning
- bot start
- bot stop
- bot enable
- bot disable
- bot status
- bot configuration
- bot credentials
- Telegram bot connection jika memang tersedia
- webhook jika memang tersedia
- polling jika memang tersedia
- runtime adapter
- worker
- process/service manager
- background task
- bot health
- runtime state

Gunakan architecture repository sebagai sumber kebenaran.

Jangan mengasumsikan fitur tersedia hanya karena nama endpoint atau model terlihat seperti mendukungnya.

Jika runtime sebenarnya belum diimplementasikan, jangan membuat runtime engine baru hanya untuk memenuhi task.

Audit implementasi yang benar-benar ada.

==================================================
2. BEDAKAN DATABASE STATE DAN RUNTIME STATE
==================================================

Pastikan jelas perbedaan:

DATABASE STATE

contoh:
- active
- inactive
- disabled
- configured
- pending
- stopped

dengan:

RUNTIME STATE

contoh jika memang tersedia:
- starting
- running
- stopping
- stopped
- failed

Jangan membuat state baru jika architecture tidak membutuhkannya.

Jika database hanya menyimpan status sederhana, jangan memaksakan state machine kompleks.

Tujuan utama:

database tidak boleh mengatakan bot running jika runtime sebenarnya tidak pernah berhasil dijalankan, kecuali architecture memang secara eksplisit menggunakan desired state.

Pahami semantics yang sudah digunakan project.

==================================================
3. BOT ENABLE/DISABLE
==================================================

Audit operasi:

enable bot
disable bot

Pastikan authorization sudah dilakukan sebelum mutation.

Flow ideal:

Authentication
→ Workspace access
→ Membership/permission
→ Bot access
→ Validate current state
→ Runtime operation jika tersedia
→ Persist resulting state

Jangan:

database mutation
→ baru mencoba runtime operation
→ gagal
→ database tetap mengatakan sukses

Jika runtime operation memang asynchronous, ikuti abstraction yang sudah tersedia.

Jangan membuat queue system baru.

==================================================
4. BOT START/STOP
==================================================

Jika repository memiliki start/stop:

Audit:

- authorization
- state validation
- duplicate start
- duplicate stop
- start after disable
- stop after already stopped
- start after deleted
- stop after deleted
- runtime failure
- persistence failure

Pastikan operasi idempotent jika architecture memang mengharuskannya.

Contoh:

start bot yang sudah running

tidak boleh menghasilkan dua runtime instance.

stop bot yang sudah stopped

tidak boleh menyebabkan error internal yang tidak perlu jika semantics repository menganggap operasi tersebut idempotent.

Jangan mengubah semantics tanpa bukti dari existing code/test.

==================================================
5. DUPLICATE RUNTIME INSTANCE
==================================================

Cari kemungkinan:

start request A
+
start request B

dijalankan hampir bersamaan.

Pastikan tidak terjadi dua runtime instance untuk bot yang sama jika architecture memang menggunakan single runtime instance.

Periksa:

- existing lock
- transaction
- unique constraint
- runtime registry
- process registry
- atomic state update

Gunakan abstraction existing.

Jangan membuat distributed locking system baru.

Jika concurrency protection belum tersedia dan tidak dapat diperbaiki secara aman tanpa architecture besar, dokumentasikan limitation tersebut.

==================================================
6. PROVISIONING
==================================================

Audit proses provisioning bot jika memang tersedia.

Pastikan provisioning tidak dapat:

- membuat bot tanpa workspace
- membuat bot tanpa owner/context
- menggunakan workspace milik user lain
- menyimpan credential ke workspace yang salah
- menghasilkan bot yang tidak memiliki parent relation
- menghasilkan database state setengah jadi

Periksa urutan:

workspace authorization
→ bot creation
→ configuration
→ credential validation
→ persistence
→ runtime registration

Ikuti flow aktual repository.

Jangan membuat provisioning framework baru.

==================================================
7. BOT CONFIGURATION
==================================================

Audit update configuration.

Pisahkan:

CLIENT CONTROLLED

dengan:

SERVER CONTROLLED

Perhatikan:

- workspaceId
- ownerId
- accountId
- botId
- status
- runtime state
- credential identifiers
- createdAt
- updatedAt
- internal runtime metadata

User tidak boleh mengubah field server-controlled melalui configuration update biasa.

Gunakan explicit field mapping jika diperlukan.

Jangan menerima object database mentah dari request.

==================================================
8. CREDENTIAL BOUNDARY
==================================================

Audit seluruh credential handling.

Cari:

- Telegram bot token
- API key
- webhook secret
- access token
- refresh token
- provider credential
- integration secret

Pastikan credential:

- tidak menentukan ownership
- tidak menentukan workspace
- tidak menentukan current user
- tidak muncul pada list response
- tidak muncul pada error response
- tidak masuk log
- tidak masuk test output
- tidak masuk analytics
- tidak disimpan pada field yang salah

Jika credential perlu disimpan, ikuti mechanism existing.

Jangan melakukan redesign credential storage tanpa kebutuhan.

==================================================
9. CREDENTIAL UPDATE
==================================================

Jika credential dapat diubah:

pastikan user hanya dapat mengubah credential bot yang memang dapat dia kelola.

Test:

authorized bot credential update
→ PASS

cross-workspace credential update
→ DENY

unauthorized member credential update
→ DENY

spoofed workspaceId
→ DENY

spoofed ownerId
→ DENY

credential dari request tidak boleh mengubah ownership.

==================================================
10. RUNTIME ERROR HANDLING
==================================================

Audit failure seperti:

- credential invalid
- runtime start gagal
- runtime stop gagal
- configuration invalid
- provider unavailable
- database unavailable
- bot deleted
- workspace access revoked
- runtime process tidak tersedia

Pastikan error mengikuti error system yang sudah ada.

Jangan membocorkan:

- token
- secret
- database connection
- SQL detail
- internal stack trace
- workspace/resource milik user lain

Production error harus menggunakan error convention repository.

==================================================
11. DATABASE CONSISTENCY
==================================================

Audit transaksi atau persistence pada lifecycle.

Perhatikan skenario:

CASE A

runtime start berhasil
database update gagal

CASE B

database update berhasil
runtime start gagal

CASE C

runtime stop berhasil
database update gagal

CASE D

database update berhasil
runtime stop gagal

CASE E

credential update berhasil
runtime registration gagal

Tentukan behavior berdasarkan architecture yang sudah ada.

Jangan membuat transaction lintas process jika tidak didukung architecture.

Jika repository memiliki abstraction transaction/Unit of Work, gunakan abstraction tersebut.

Jangan membuat transaction framework baru.

==================================================
12. DELETED BOT
==================================================

Jika project memiliki deleted state atau hard delete, audit behavior:

deleted bot
→ start

deleted bot
→ stop

deleted bot
→ enable

deleted bot
→ disable

deleted bot
→ credential update

deleted bot
→ configuration update

Semua harus mengikuti semantics existing architecture.

Jangan membuat state deleted baru jika belum ada.

Jangan mengubah soft delete menjadi hard delete.

Jangan mengubah hard delete menjadi soft delete.

==================================================
13. WORKSPACE MEMBERSHIP REGRESSION
==================================================

Pastikan runtime operation tetap menghormati workspace boundary.

User A:

workspace-A
bot-A

User B:

workspace-B
bot-B

User A tidak boleh:

start bot-B
stop bot-B
enable bot-B
disable bot-B
update configuration bot-B
update credential bot-B

meskipun User A mengetahui botId.

Test authorization sebelum runtime operation.

==================================================
14. PERMISSION REGRESSION
==================================================

Pastikan:

owner
→ sesuai policy dapat mengelola bot

member dengan permission tertentu
→ hanya dapat operasi yang diizinkan

member tanpa permission
→ DENY

Jangan memberikan runtime control hanya karena user adalah member.

Gunakan permission policy yang sudah ada.

Jangan membuat permission system kedua.

==================================================
15. RESOURCE RELATION INTEGRITY
==================================================

Audit hubungan:

User
→ Account
→ Telegram Account
→ Workspace
→ Bot
→ Configuration
→ Credential
→ Runtime

Pastikan tidak ada relation seperti:

bot.workspaceId ≠ configuration.workspaceId

bot.workspaceId ≠ credential.workspaceId

bot.accountId ≠ workspace.accountId

runtime.botId ≠ database bot.id

Jika runtime registry memang tersedia, pastikan mapping-nya benar.

Jangan memperbaiki data production otomatis.

Fokus pada enforcement dan test.

==================================================
16. IDOR AUDIT
==================================================

Cari pola:

findById(id)

findUnique({ id })

where: { id }

pada:

- bot
- configuration
- credential
- runtime
- integration
- webhook
- child resource

Pastikan resource tetap melewati authorization boundary.

Gunakan repository abstraction existing.

Jangan melakukan perubahan query secara membabi buta.

==================================================
17. API CONTRACT
==================================================

Audit endpoint yang berkaitan dengan:

- bot creation
- bot update
- bot status
- bot enable
- bot disable
- bot start
- bot stop
- bot configuration
- bot credential

Jika endpoint tidak tersedia:

JANGAN membuat endpoint baru.

Fokus pada endpoint/service yang memang ada.

Pastikan request validation menggunakan schema yang sudah tersedia.

==================================================
18. IDEMPOTENCY
==================================================

Audit operation yang seharusnya aman dipanggil berulang.

Minimal jika tersedia:

- enable
- disable
- start
- stop
- configuration update

Pastikan repeated request tidak menghasilkan:

- duplicate runtime
- duplicate credential
- duplicate child resource
- corrupted state

Gunakan behavior yang sudah ditentukan architecture.

==================================================
19. TEST MATRIX
==================================================

Tambahkan/perbaiki test sesuai implementation aktual.

### Creation

authenticated + valid workspace
→ PASS

unauthenticated
→ DENY

wrong workspace
→ DENY

spoofed ownerId
→ DENY

spoofed accountId
→ DENY

### Read

own bot
→ PASS

other workspace bot
→ DENY

### Update

authorized update
→ PASS

unauthorized update
→ DENY

workspace spoof
→ DENY

owner spoof
→ DENY

status spoof
→ DENY

### Enable

authorized
→ PASS

unauthorized
→ DENY

cross-workspace
→ DENY

### Disable

authorized
→ PASS

unauthorized
→ DENY

cross-workspace
→ DENY

### Runtime

authorized start
→ PASS

unauthorized start
→ DENY

cross-workspace start
→ DENY

authorized stop
→ PASS

unauthorized stop
→ DENY

cross-workspace stop
→ DENY

### Credential

authorized credential update
→ PASS

cross-workspace credential update
→ DENY

credential tidak muncul pada response yang tidak seharusnya
→ PASS

credential tidak muncul pada error
→ PASS

credential tidak muncul pada log/test output
→ PASS

### Concurrency

duplicate start
→ tidak menghasilkan duplicate runtime

repeated stop
→ behavior sesuai architecture

==================================================
20. REGRESSION SUITE
==================================================

Pastikan checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization
- bot lifecycle
- PostgreSQL adapter
- PostgreSQL runtime integration
- migration
- typecheck
- lint
- format
- import boundary
- build

Jangan skip PostgreSQL integration jika repository menyediakan database test dan environment tersedia.

Jangan mengubah default test behavior hanya untuk mendapatkan hasil PASS.

==================================================
21. POSTGRESQL VERIFICATION
==================================================

Karena persistence sudah diverifikasi sebelumnya:

Jika environment PostgreSQL tersedia, jalankan integration test yang memang disediakan repository.

Pastikan perubahan runtime tidak merusak:

- create
- update
- delete
- status
- relation
- transaction behavior

Jangan melakukan destructive operation terhadap production database.

Gunakan database test/local yang memang disediakan repository.

==================================================
22. TYPESCRIPT QUALITY
==================================================

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate lifecycle logic
- tidak ada duplicate authorization system
- tidak ada hardcoded credential
- tidak ada circular dependency baru

Ikuti architecture repository.

==================================================
23. README
==================================================

Jika memang diperlukan:

UPDATE README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan singkat:

- bot lifecycle
- runtime state
- provisioning
- credential handling
- runtime verification
- test command

Jangan membuat dokumentasi panjang yang tidak diperlukan.

==================================================
24. VERIFICATION
==================================================

Setelah implementasi:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- PostgreSQL adapter/runtime tests jika tersedia
- pnpm check
- typecheck
- lint
- format
- import boundary
- build
- git diff --check

Jika ada failure:

1. identifikasi root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

==================================================
25. GIT AUDIT
==================================================

Sebelum commit:

git status

git diff --stat

git diff

git diff --check

Pastikan perubahan hanya berkaitan dengan task ini.

Jangan commit:

- .env
- API key
- token
- password
- credential
- log
- temporary file
- build artifact
- database dump

==================================================
26. COMMIT
==================================================

Jika semua verification PASS:

buat SATU commit.

Gunakan commit message sesuai implementasi aktual.

Contoh:

fix: harden bot runtime integrity

atau:

fix: secure bot runtime lifecycle

Pilih message yang paling sesuai dengan perubahan sebenarnya.

Setelah commit:

git status
git log --oneline -3

==================================================
27. PUSH
==================================================

Jalankan:

git push

Branch harus tetap:

backend-dev-recovery

Jangan:

- force push
- reset
- rebase sembarangan
- checkout branch lain
- mengubah remote
- merge ke backend-dev

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

JANGAN membuat commit tambahan hanya karena push gagal.

Pertahankan commit lokal dan tampilkan error sebenarnya.

==================================================
28. HASIL AKHIR
==================================================

Tampilkan laporan:

Implementation:
- ...

Runtime:
- ...

Provisioning:
- ...

Credential Security:
- ...

State Consistency:
- ...

Workspace Isolation:
- ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
- PostgreSQL: ...
- pnpm check: ...
- Typecheck: ...
- Lint: ...
- Format: ...
- Import boundary: ...
- Build: ...
- git diff --check: ...

Commit:
- hash: ...
- message: ...

Git:
- branch: ...
- push: success/failed

Working Tree:
- clean/dirty

Jika ada failure, tampilkan error sebenarnya.

Jangan mengklaim PASS jika test atau verification belum benar-benar dijalankan.

==================================================
29. BATASAN SCOPE
==================================================

Jangan membuat fitur besar baru.

Jangan membuat:

- runtime engine baru
- queue system baru
- distributed lock system baru
- provider baru
- integration baru
- authentication system baru
- permission system kedua
- credential architecture baru
- database architecture baru

Gunakan abstraction yang sudah tersedia.

Fokus hanya:

AUDIT
→ RUNTIME INTEGRITY
→ PROVISIONING INTEGRITY
→ CREDENTIAL SECURITY
→ STATE CONSISTENCY
→ CONCURRENCY SAFETY
→ WORKSPACE ISOLATION
→ REGRESSION
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Selesaikan sampai push berhasil lalu berhenti.

```
# 
```



```
# API Functional & End-to-End Contract Hardening.
```

PROMPT: BotSpace — API Functional & End-to-End Contract Hardening

Kita melanjutkan project BotSpace dari checkpoint API persistence yang SUDAH BERHASIL secara lokal.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Remote:
 https://github.com/zenolamee/botspace.git

IMPORTANT:
Beberapa commit terakhir sudah berhasil dibuat secara lokal tetapi push ke GitHub sebelumnya gagal karena credential GitHub:

fatal: could not read Username for 'https://github.com'

JANGAN mengubah credential GitHub.
JANGAN mengubah remote.
JANGAN reset commit.
JANGAN force push.
JANGAN rebase.
JANGAN checkout branch lain.
JANGAN merge ke backend-dev.

Semua commit lokal harus tetap dipertahankan.

Checkpoint lokal terbaru:

980a0c1 — test: verify api persistence contract

Commit sebelumnya juga harus tetap dipertahankan.

Verification terakhir yang sudah PASS:

- Domain: 110 passed
- API: 119 passed
- PostgreSQL adapter/runtime: 3 passed
- pnpm check: 44/44 passed
- Typecheck: PASS
- Lint: PASS
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Migration: PASS
- Build: PASS
- git diff --check: PASS
- Working tree: clean

JANGAN mengulang pekerjaan persistence yang sudah diverifikasi kecuali audit menemukan regression nyata.

==================================================
TUJUAN
==================================================

Tahap berikutnya adalah memastikan API BotSpace benar-benar memiliki contract yang konsisten dari HTTP request sampai domain/service/repository/database dan kembali menjadi HTTP response.

Fokus:

HTTP ROUTE
→ AUTHENTICATION
→ CURRENT USER
→ WORKSPACE ACCESS
→ MEMBERSHIP
→ PERMISSION
→ RESOURCE AUTHORIZATION
→ VALIDATION
→ SERVICE
→ DOMAIN
→ REPOSITORY
→ DATABASE
→ RESPONSE
→ ERROR CONTRACT

Tujuan utama:

- tidak ada endpoint protected yang melewati authentication
- tidak ada endpoint workspace yang melewati authorization
- tidak ada IDOR
- tidak ada mass assignment
- tidak ada response contract yang tidak konsisten
- tidak ada error leakage
- tidak ada route yang langsung memanipulasi database tanpa abstraction yang benar
- mutation benar-benar tersimpan
- read benar-benar membaca persistence
- API behavior konsisten
- existing security tetap PASS

Jangan membuat API architecture kedua.

==================================================
1. AUDIT API AKTUAL
==================================================

JANGAN langsung menulis kode.

Audit repository aktual terlebih dahulu.

Cari seluruh:

- API routes
- HTTP handlers
- controllers
- request schemas
- response schemas
- service layer
- domain services
- repository
- persistence adapter
- authentication middleware
- authorization middleware
- workspace authorization
- membership authorization
- bot authorization
- error handling
- API tests

Gunakan repository aktual sebagai sumber kebenaran.

Jangan mengasumsikan endpoint hanya berdasarkan dokumentasi.

Buat inventory internal dari endpoint yang benar-benar tersedia.

==================================================
2. ROUTE CONTRACT
==================================================

Untuk setiap endpoint yang tersedia, trace:

HTTP
→ route
→ auth
→ current user
→ workspace
→ membership
→ permission
→ validation
→ service
→ repository
→ persistence
→ response

Cari route yang:

- langsung mengakses database
- langsung memakai request.userId
- mempercayai workspaceId dari client
- mempercayai ownerId dari client
- melewati permission policy
- mengembalikan raw database object
- memiliki error handling berbeda tanpa alasan
- memiliki duplicate business logic

Jika ditemukan:

perbaiki secara minimal.

Jangan refactor besar-besaran tanpa kebutuhan.

==================================================
3. AUTHENTICATION CONTRACT
==================================================

Pastikan endpoint protected hanya dapat digunakan oleh authenticated identity.

Test:

- no authentication → DENY
- invalid session → DENY
- expired session → DENY
- revoked session → DENY
- valid session → PASS

Jangan menggunakan:

- userId dari body
- accountId dari body
- ownerId dari body

sebagai pengganti authentication context.

Current user harus berasal dari authentication/session system yang sudah ada.

==================================================
4. WORKSPACE CONTRACT
==================================================

Pastikan setiap endpoint workspace-scoped benar-benar menggunakan workspace authorization.

Test:

User A:
workspace-A

User B:
workspace-B

User A:

workspace-A → PASS
workspace-B → DENY

User B:

workspace-B → PASS
workspace-A → DENY

Periksa:

- list workspace
- get workspace
- update workspace
- delete workspace
- membership
- bot
- child resources

sesuai endpoint yang benar-benar tersedia.

==================================================
5. MEMBERSHIP CONTRACT
==================================================

Pastikan membership tidak hanya menjadi data tetapi benar-benar digunakan sebagai authorization boundary.

Test:

- owner → allowed sesuai policy
- authorized member → allowed
- member tanpa permission → DENY
- non-member → DENY
- cross-workspace member → DENY

Jangan membuat role/permission system baru.

Gunakan policy yang sudah ada.

==================================================
6. BOT CONTRACT
==================================================

Audit seluruh Bot API yang tersedia.

Minimal:

CREATE
GET
LIST
UPDATE
DELETE
ENABLE
DISABLE
STATUS

sesuai implementasi aktual.

Pastikan:

botId
→ resolve bot
→ resolve workspace
→ authorize user
→ perform operation

Bukan:

botId
→ perform operation

Test:

own bot → PASS
other workspace bot → DENY

==================================================
7. MASS ASSIGNMENT
==================================================

Audit request body.

Cari endpoint yang menerima object langsung dari client lalu meneruskannya ke database.

Contoh berbahaya:

{
  userId,
  accountId,
  workspaceId,
  ownerId,
  role,
  permissions,
  status
}

Pastikan field server-controlled tidak dapat dimanipulasi client.

Audit khusus:

- userId
- accountId
- workspaceId
- ownerId
- createdBy
- role
- permissions
- createdAt
- updatedAt

Gunakan explicit field mapping jika diperlukan.

Jangan mempercayai object request secara langsung untuk mutation sensitif.

==================================================
8. RESOURCE IDOR
==================================================

Cari seluruh lookup berdasarkan ID:

findById
findUnique
where id
getById
repository lookup
atau equivalent.

Untuk resource workspace-scoped, pastikan ada authorization.

Jika architecture memungkinkan query scoped:

gunakan workspace/user scope.

Jika authorization dilakukan di service:

pastikan service benar-benar dipanggil sebelum mutation/response.

Audit:

- workspace
- membership
- bot
- commands
- flows
- settings
- integrations
- webhook
- credentials
- logs
- statistics

hanya jika resource tersebut benar-benar tersedia.

Jangan membuat endpoint baru.

==================================================
9. REQUEST VALIDATION
==================================================

Audit:

- path parameter
- query parameter
- request body
- enum
- boolean
- number
- string
- nullable field
- required field

Pastikan invalid input tidak sampai menyebabkan:

- database exception
- TypeError
- undefined behavior
- 500 yang seharusnya 400
- invalid persistence

Gunakan validator yang sudah ada.

Jangan membuat validation framework baru.

==================================================
10. RESPONSE CONTRACT
==================================================

Audit response seluruh API.

Pastikan response:

- konsisten
- tidak mengembalikan raw database entity jika tidak diperlukan
- tidak membocorkan secret
- tidak membocorkan credential
- tidak membocorkan authorization metadata
- tidak mengembalikan resource workspace lain

Cari khusus:

- bot token
- API key
- webhook secret
- session token
- password
- credentials

Jika DTO sudah tersedia:

gunakan DTO tersebut.

Jangan membuat response abstraction kedua.

==================================================
11. ERROR CONTRACT
==================================================

Pastikan error behavior konsisten.

Minimal bedakan:

401:
unauthenticated

403:
authenticated tetapi tidak memiliki permission/access

404:
resource tidak ditemukan sesuai convention project

400:
invalid input

409:
conflict jika memang digunakan architecture

500:
unexpected internal error

Jangan mengubah error convention hanya agar test PASS.

Jangan membocorkan:

- SQL
- stack trace
- token
- credential
- secret
- internal database details

Production response harus aman.

==================================================
12. HTTP METHOD CONTRACT
==================================================

Audit method:

GET
POST
PUT/PATCH
DELETE

Pastikan route tidak menerima method yang tidak didukung.

Jika framework sudah menghasilkan:

405
Allow header

gunakan behavior tersebut.

Jangan membuat custom router baru.

==================================================
13. CRUD CONSISTENCY
==================================================

Untuk resource yang memiliki CRUD:

CREATE
→ persistence

GET
→ persistence

LIST
→ scoped persistence

UPDATE
→ persistence

DELETE
→ persistence

Pastikan hasil operasi benar-benar terlihat pada request berikutnya.

Contoh:

CREATE bot
→ GET bot harus menemukan bot tersebut.

UPDATE bot
→ GET bot harus melihat perubahan.

DELETE bot
→ GET bot harus mengikuti delete semantics architecture.

Jangan menggunakan in-memory fake state pada production path.

==================================================
14. API PERSISTENCE REGRESSION
==================================================

Persistence contract sebelumnya SUDAH PASS.

Sekarang hanya lakukan regression verification.

Pastikan API layer tidak bypass persistence adapter yang sudah diverifikasi.

Jangan mengubah PostgreSQL adapter/runtime tanpa alasan.

Jangan membuat migration baru kecuali ada bug nyata.

Jangan melakukan destructive database operation.

==================================================
15. CROSS-WORKSPACE API TEST
==================================================

Buat regression test matrix:

USER A
workspace-A
bot-A

USER B
workspace-B
bot-B

Test:

A → workspace-A GET = PASS
A → workspace-B GET = DENY

A → bot-A GET = PASS
A → bot-B GET = DENY

A → bot-A UPDATE = PASS
A → bot-B UPDATE = DENY

A → bot-A DELETE = PASS sesuai permission
A → bot-B DELETE = DENY

A → bot-A ENABLE = PASS
A → bot-B ENABLE = DENY

A → bot-A DISABLE = PASS
A → bot-B DISABLE = DENY

Sesuaikan dengan endpoint yang benar-benar tersedia.

==================================================
16. IDENTITY SPOOFING TEST
==================================================

Test request yang mencoba mengirim:

userId=user-B

padahal session:

user-A

Backend harus tetap menggunakan:

user-A

Test juga:

accountId spoof
ownerId spoof
workspaceId spoof
createdBy spoof

Pastikan tidak terjadi impersonation atau privilege escalation.

==================================================
17. PERMISSION SPOOFING
==================================================

Test request yang mencoba:

role=owner

atau:

permissions=["*"]

atau permission lain yang privileged.

Backend tidak boleh mempercayai request tersebut sebagai authorization source.

Authorization harus berdasarkan:

authenticated identity
+
stored membership
+
existing permission policy

==================================================
18. CONCURRENCY / REPEATED REQUEST
==================================================

Audit mutation yang dapat dipanggil berulang.

Contoh:

enable bot
disable bot
update bot
delete bot

Pastikan repeated request tidak menghasilkan state korup.

Jika repository/database abstraction sudah memiliki atomic behavior:

gunakan abstraction tersebut.

Jangan membuat concurrency framework baru.

==================================================
19. DUPLICATE REQUEST
==================================================

Audit create operation.

Jika terdapat unique constraint/business rule:

duplicate create harus menghasilkan behavior yang benar.

Jangan menghapus constraint.

Jangan membuat business rule baru tanpa bukti.

==================================================
20. CHILD RESOURCE SECURITY
==================================================

Jika child resource tersedia:

Bot
→ Child Resource

Pastikan authorization parent tetap berlaku.

Contoh:

User A tidak boleh:

GET child-resource-B

jika:

child-resource-B
→ bot-B
→ workspace-B

meskipun child resource ID diketahui.

==================================================
21. TEST SUITE
==================================================

Tambahkan/perbaiki test sesuai implementation aktual.

Minimal:

AUTH:
- unauthenticated DENY
- invalid session DENY
- valid session PASS

WORKSPACE:
- own workspace PASS
- other workspace DENY

MEMBERSHIP:
- authorized member PASS
- unauthorized member DENY

BOT:
- own bot PASS
- cross-workspace bot DENY
- unauthorized mutation DENY

INPUT:
- invalid body DENY
- invalid ID DENY
- privileged field spoof DENY

PERSISTENCE:
- create persists
- update persists
- delete persists sesuai architecture

RESPONSE:
- no secret leakage

ERROR:
- correct status/error convention

==================================================
22. REGRESSION
==================================================

Semua checkpoint security sebelumnya harus tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot authorization
- bot lifecycle
- persistence

Jangan melemahkan test existing.

==================================================
23. TYPESCRIPT QUALITY
==================================================

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate authorization
- tidak ada duplicate validation
- tidak ada duplicate API layer
- tidak ada circular dependency baru
- tidak ada hardcoded secret

==================================================
24. README
==================================================

Jika diperlukan:

UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan secara singkat:

- API authentication
- workspace authorization
- bot authorization
- persistence contract
- test commands

==================================================
25. VERIFICATION
==================================================

Setelah implementation:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace tests
- membership tests
- bot tests
- persistence tests
- typecheck
- lint
- format
- import boundary
- secrets scan
- ownership check
- migration check
- build
- git diff --check

Jika PostgreSQL suite bersifat opt-in:

jalankan hanya jika environment PostgreSQL tersedia.

Laporkan:

PostgreSQL:
- skipped
- passed
- failed

Jangan mengklaim skipped sebagai PASS.

==================================================
26. GIT AUDIT
==================================================

Sebelum commit:

git status
git diff --stat
git diff

Pastikan hanya perubahan task ini.

Jangan commit:

- .env
- API key
- credential
- token
- log
- temporary file
- build artifact

==================================================
27. COMMIT
==================================================

Jika verification PASS:

buat SATU commit.

Gunakan commit message berdasarkan perubahan aktual.

Contoh:

feat: harden api functional contracts

atau:

fix: enforce api resource contracts

Pilih yang paling sesuai.

Setelah commit:

git status
git log --oneline -5

==================================================
28. PUSH
==================================================

Coba:

git push

Branch tetap:

backend-dev-recovery

JANGAN:

- force push
- reset
- rebase
- merge
- ubah remote
- ubah credential GitHub

Jika push kembali gagal karena:

could not read Username for 'https://github.com'

JANGAN menyentuh source code.

Commit lokal harus dipertahankan.

Laporkan:

PUSH FAILED — GITHUB CREDENTIAL ONLY

dan tampilkan branch/local commits yang belum dipush.

==================================================
29. FINAL REPORT
==================================================

Tampilkan:

Implementation:
- ...

API:
- Route contract: ...
- Authentication: ...
- Authorization: ...
- Validation: ...
- Persistence: ...
- Response: ...
- Error contract: ...

Security:
- IDOR: ...
- Mass assignment: ...
- Cross-workspace: ...
- Identity spoofing: ...
- Secret leakage: ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Persistence: ...
- Typecheck: ...
- Lint: ...
- Format: ...
- Import boundary: ...
- Secrets scan: ...
- Ownership: ...
- Migration: ...
- Build: ...

PostgreSQL:
- skipped/passed/failed

Commit:
- hash: ...
- message: ...

Git:
- branch: backend-dev-recovery
- push: success/failed

Working tree:
- clean/dirty

Jika push gagal:

JANGAN menganggap implementation gagal.

Pisahkan:

CODE STATUS
dan
GIT PUSH STATUS.

==================================================
30. BATASAN SCOPE
==================================================

Jangan membuat fitur besar baru.

Jangan membuat:

- frontend baru
- payment system
- billing
- notification
- OAuth baru
- Telegram runtime baru
- deployment system
- permission system kedua
- persistence system kedua

Fokus:

AUDIT
→ API CONTRACT
→ AUTHENTICATION
→ AUTHORIZATION
→ VALIDATION
→ RESOURCE ISOLATION
→ PERSISTENCE REGRESSION
→ RESPONSE
→ ERROR
→ TEST
→ BUILD
→ COMMIT
→ PUSH

Selesaikan seluruh scope ini.

Jika semua verification PASS, buat satu commit dan coba push.

Setelah itu BERHENTI.

```
# API Contract & Functional Completeness
```

PROMPT: BotSpace — API Functional Completeness & End-to-End Contract Hardening

Kita melanjutkan project BotSpace dari checkpoint security, persistence, dan API verification yang SUDAH BERHASIL.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Remote:
 https://github.com/zenolamee/botspace.git

IMPORTANT:
User sudah melakukan push checkpoint sebelumnya secara manual.

JANGAN:
- reset
- force push
- rebase sembarangan
- checkout branch lain
- merge ke backend-dev
- menghapus commit sebelumnya
- melakukan destructive database operation
- mengubah credential GitHub
- mengubah production secret
- membuat sistem API kedua

Kita tetap bekerja di branch:

backend-dev-recovery


==================================================
TUJUAN UTAMA
==================================================

Security foundation BotSpace sudah melewati beberapa tahap:

AUTHENTICATION
→ SESSION
→ CURRENT USER
→ WORKSPACE AUTHORIZATION
→ MEMBERSHIP
→ OWNERSHIP
→ PERMISSION POLICY
→ BOT RESOURCE AUTHORIZATION
→ BOT LIFECYCLE
→ PERSISTENCE
→ API VERIFICATION

Sekarang fokus tahap ini adalah:

API FUNCTIONAL COMPLETENESS

Tujuan akhirnya bukan membuat fitur baru besar.

Tujuan utama adalah memastikan API yang SUDAH ADA benar-benar bekerja end-to-end:

HTTP ROUTE
→ AUTHENTICATION
→ AUTHORIZATION
→ VALIDATION
→ SERVICE
→ DOMAIN
→ REPOSITORY
→ DATABASE
→ RESPONSE

Setiap endpoint yang memang sudah tersedia harus:

- menerima input yang benar
- menolak input invalid
- menggunakan authenticated identity
- menggunakan workspace authorization
- menggunakan permission policy
- memanggil service yang benar
- melakukan persistence yang benar
- mengembalikan response yang sesuai contract
- mengembalikan error yang sesuai
- tidak membocorkan secret
- tidak membuat state database yang invalid


==================================================
1. AUDIT REPOSITORY TERLEBIH DAHULU
==================================================

JANGAN langsung menulis kode.

Pertama audit repository aktual.

Periksa:

- packages/domain
- services/api
- repository layer
- database layer
- migrations
- API routes
- request schemas
- response DTO
- service layer
- domain services
- error handling
- authentication
- authorization
- workspace
- membership
- bot
- lifecycle
- persistence adapter
- integration tests
- API tests
- domain tests

Cari seluruh endpoint yang benar-benar sudah tersedia.

Jangan mengasumsikan endpoint hanya karena namanya terlihat di dokumentasi.

Repository adalah sumber kebenaran.


==================================================
2. BUAT INVENTORY API INTERNAL
==================================================

Buat inventory internal dari endpoint yang benar-benar ada.

Kelompokkan:

WORKSPACE

- create
- list
- detail
- update
- delete

MEMBERSHIP

- list
- get
- create
- update
- delete
- leave

BOT

- create
- list
- detail
- update
- delete
- enable
- disable
- status

CHILD RESOURCE

Jika tersedia:

- commands
- flows
- settings
- integrations
- webhook
- credentials
- logs
- statistics
- configuration

Gunakan hanya endpoint yang benar-benar ada.

JANGAN membuat endpoint baru hanya untuk melengkapi daftar.


==================================================
3. ROUTE → SERVICE FLOW
==================================================

Untuk setiap endpoint penting, trace flow:

HTTP request
→ route
→ authentication
→ current user
→ workspace authorization
→ permission
→ input validation
→ service
→ domain
→ repository
→ database
→ response

Cari apakah ada route yang:

- langsung mengakses database
- melewati service
- melewati authorization
- melewati validation
- mengembalikan raw database object
- memiliki logic duplicate

Jika menemukan pelanggaran architecture:

perbaiki secara minimal.

Jangan melakukan refactor besar tanpa kebutuhan.


==================================================
4. REQUEST VALIDATION
==================================================

Audit seluruh request body, params, query, dan headers.

Pastikan endpoint menggunakan validation mechanism yang memang sudah tersedia.

Periksa:

- required fields
- optional fields
- ID format
- enum
- boolean
- number
- string
- empty string
- null
- unknown fields
- malformed JSON
- missing body

Jangan membuat validation framework baru.

Gunakan schema/validator yang sudah digunakan project.


==================================================
5. SERVER-CONTROLLED FIELD
==================================================

Audit field yang tidak boleh dipercaya dari client.

Contoh:

- userId
- accountId
- ownerId
- workspaceId
- createdBy
- createdAt
- updatedAt
- permissions
- role
- membership owner
- internal status
- database identifiers

Pastikan field server-controlled tidak dapat digunakan untuk privilege escalation.

Authentication context harus menjadi sumber identity.

Workspace authorization harus berasal dari backend.

Permission harus berasal dari policy.


==================================================
6. WORKSPACE API
==================================================

Audit seluruh API workspace yang memang tersedia.

CREATE:

Pastikan:

- authenticated user valid
- account relation valid
- workspace dibuat dengan owner yang benar
- client tidak dapat memilih owner user lain
- client tidak dapat membuat workspace atas account milik user lain

LIST:

Pastikan hanya workspace yang boleh dilihat user yang dikembalikan.

GET:

Pastikan workspace ID tidak dapat digunakan untuk IDOR.

UPDATE:

Pastikan:

- authenticated user
- membership/ownership
- permission
- valid fields

DELETE:

Pastikan:

- authorization sebelum mutation
- ownership/permission sesuai policy
- tidak meninggalkan relation invalid

Jangan menambahkan transfer ownership.


==================================================
7. BOT API
==================================================

Audit seluruh Bot API.

CREATE BOT:

Flow harus:

authentication
→ workspace access
→ permission
→ validation
→ create bot
→ persistence

Client tidak boleh menentukan:

- owner user lain
- account lain
- workspace lain
- arbitrary permissions

LIST BOT:

Pastikan query benar-benar workspace/user scoped.

Jangan:

ambil semua bot
→ filter hanya di JavaScript

jika repository dapat melakukan scoped query.

GET BOT:

Pastikan:

botId
→ resolve authorization
→ return bot

bukan:

botId
→ return bot


UPDATE BOT:

Gunakan explicit allowed fields.

Jangan memperbolehkan update:

- workspaceId
- ownerId
- accountId
- createdBy
- permissions

kecuali architecture memang secara eksplisit mendukungnya.

DELETE BOT:

Pastikan authorization dilakukan sebelum delete.

ENABLE/DISABLE:

Pastikan status mutation:

- authenticated
- authorized
- workspace scoped
- valid state


==================================================
8. RESPONSE CONTRACT
==================================================

Audit response setiap endpoint.

Pastikan response:

- konsisten
- typed
- tidak mengembalikan database object mentah
- tidak membocorkan secret
- tidak membocorkan credential
- tidak membocorkan authorization metadata
- tidak membocorkan resource workspace lain

Periksa terutama:

- bot token
- API key
- webhook secret
- session token
- credential
- password
- internal database fields

Jika DTO/response mapper sudah tersedia:

gunakan abstraction tersebut.

Jangan membuat response formatter kedua.


==================================================
9. ERROR CONTRACT
==================================================

Pastikan error behavior konsisten.

Minimal bedakan:

401:
unauthenticated

403:
authenticated tetapi tidak memiliki permission/access

404:
resource benar-benar tidak ditemukan atau behavior project memang menyamarkan unauthorized resource sebagai not found

400:
validation error

409:
conflict jika memang architecture menggunakan conflict error

500:
unexpected internal error

Jangan membuat error code baru tanpa kebutuhan.

Ikuti convention existing project.


==================================================
10. DATABASE PERSISTENCE
==================================================

Karena production persistence sudah diverifikasi, sekarang audit apakah setiap API mutation benar-benar menggunakan persistence adapter yang benar.

Periksa:

CREATE:
- insert benar

UPDATE:
- update resource yang benar

DELETE:
- delete behavior sesuai architecture

LIST:
- query benar

GET:
- query benar

STATUS:
- state tersimpan benar

Pastikan tidak ada:

- in-memory fallback
- mock persistence pada production path
- hardcoded response
- fake success response
- silent mutation failure

Jangan mengganti persistence architecture yang sudah diverifikasi.


==================================================
11. TRANSACTION / ATOMICITY
==================================================

Cari operasi yang mengubah lebih dari satu entity.

Contoh:

create bot
→ create credential
→ create configuration

atau:

delete bot
→ delete child resource

Jika architecture sudah memiliki transaction abstraction:

gunakan yang sudah ada.

Jangan membuat transaction framework baru.

Jika transaction belum diperlukan karena operation hanya satu query:

jangan memaksakan transaction.


==================================================
12. NOT FOUND BEHAVIOR
==================================================

Audit seluruh resource lookup.

Kasus:

- workspace tidak ada
- bot tidak ada
- membership tidak ada
- child resource tidak ada
- malformed ID

Pastikan tidak menghasilkan:

- TypeError
- database exception
- stack trace
- undefined response
- 200 kosong yang salah

Gunakan error convention existing.


==================================================
13. DUPLICATE / CONFLICT
==================================================

Audit kemungkinan duplicate create.

Contoh jika memang memiliki unique constraint:

- duplicate workspace
- duplicate membership
- duplicate bot
- duplicate external identifier

Pastikan database constraint error diterjemahkan menjadi application error yang sesuai.

Jangan menghapus unique constraint hanya supaya test PASS.

Jangan membuat business rule baru jika tidak ada di architecture.


==================================================
14. PAGINATION / FILTERING
==================================================

Jika API repository memang sudah mendukung:

- pagination
- limit
- cursor
- offset
- filtering
- sorting

audit contract-nya.

Pastikan:

- limit tidak dapat menjadi nilai berbahaya
- negative value ditolak
- terlalu besar dibatasi sesuai existing convention
- cursor invalid ditangani
- filtering tetap workspace-scoped

Jika fitur pagination belum ada:

JANGAN membuat pagination baru hanya untuk task ini.


==================================================
15. API METHOD SECURITY
==================================================

Pastikan HTTP methods sesuai contract.

Contoh:

GET:
read only

POST:
create/action sesuai contract

PATCH/PUT:
update

DELETE:
delete

Route harus menolak method yang tidak didukung.

Gunakan:

405
dan
Allow header

jika router/project memang sudah menggunakan behavior tersebut.

Jangan menambahkan custom method handling jika framework sudah menangani.


==================================================
16. AUTHORIZATION REGRESSION
==================================================

Semua API functional testing harus mempertahankan security checkpoint sebelumnya.

Minimal:

User A:
workspace-A

User B:
workspace-B

Test:

User A:
workspace-A → PASS

User B:
workspace-B → PASS

User A:
workspace-B → DENY

User B:
workspace-A → DENY

Untuk bot:

User A:
bot-A → PASS

User A:
bot-B → DENY

User B:
bot-B → PASS

User B:
bot-A → DENY


==================================================
17. AUTHENTICATION REGRESSION
==================================================

Pastikan protected API menolak:

- no session
- invalid session
- expired session
- revoked session

Jika auth system project memiliki behavior berbeda, ikuti behavior tersebut.

Jangan membuat authentication system baru.


==================================================
18. INPUT ABUSE
==================================================

Audit input yang berpotensi menyebabkan:

- privilege escalation
- IDOR
- mass assignment
- invalid state
- malformed ID
- oversized payload
- unexpected fields

Tidak perlu membuat rate limiter atau WAF.

Fokus pada application-level correctness.


==================================================
19. CHILD RESOURCE API
==================================================

Jika child resource tersedia, audit:

Parent:
Bot A

Child:
Flow A

User yang memiliki akses Bot A:
→ Flow A PASS

User workspace lain:
→ Flow A DENY

Pastikan child resource tidak dapat bypass authorization hanya karena memiliki ID sendiri.

Semua child resource harus mengikuti parent security boundary.


==================================================
20. API TESTING
==================================================

Perkuat test sesuai endpoint yang benar-benar tersedia.

Minimal:

AUTH:

- unauthenticated = DENY
- invalid session = DENY
- authenticated = PASS

WORKSPACE:

- create valid = PASS
- list scoped = PASS
- get own = PASS
- get other = DENY
- update own = PASS
- update other = DENY
- delete own = PASS sesuai permission
- delete other = DENY

BOT:

- create valid = PASS
- create wrong workspace = DENY
- list scoped = PASS
- get own = PASS
- get other = DENY
- update own = PASS
- update other = DENY
- delete own = PASS
- delete other = DENY
- enable own = PASS
- enable other = DENY
- disable own = PASS
- disable other = DENY

INPUT:

- missing required field = DENY
- malformed ID = DENY
- invalid enum = DENY
- unexpected privileged field = DENY/ignored sesuai convention

ERROR:

- 401/403/404/400 sesuai behavior project

PERSISTENCE:

- create benar-benar tersimpan
- update benar-benar berubah
- delete benar-benar hilang/nonaktif sesuai architecture


==================================================
21. FULL END-TO-END VERIFICATION
==================================================

Setelah implementasi:

jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication tests
- session tests
- workspace tests
- membership tests
- bot tests
- persistence tests
- typecheck
- lint jika tersedia
- format
- import boundary
- build

Jangan skip test.

Jangan menghapus test existing.

Jangan mengubah expected result hanya untuk membuat test PASS.

Jika ada failure:

1. cari root cause
2. perbaiki implementation
3. jalankan test terkait
4. jalankan full suite lagi


==================================================
22. TEST ENVIRONMENT
==================================================

Jika PostgreSQL test suite bersifat opt-in:

ikuti mekanisme repository.

Jangan mengklaim PostgreSQL integration PASS jika memang tidak dijalankan.

Jika PostgreSQL test tersedia dan environment sudah tersedia:

jalankan secara eksplisit.

Pastikan hasil dilaporkan dengan jujur:

- default tests
- PostgreSQL tests
- integration tests

Jangan membuat database production menjadi test database.


==================================================
23. CODE QUALITY
==================================================

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada duplicate service
- tidak ada duplicate repository
- tidak ada duplicate validation
- tidak ada duplicate authorization
- tidak ada dead code
- tidak ada unused import
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- tidak ada debug console yang tidak diperlukan

Ikuti architecture existing.


==================================================
24. README
==================================================

Jika diperlukan:

UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan hanya hal penting:

- API architecture
- authentication
- workspace authorization
- bot API
- persistence
- test commands

Jangan membuat dokumentasi panjang yang tidak diperlukan.


==================================================
25. GIT AUDIT
==================================================

Setelah implementation:

jalankan:

git status

git diff --stat

git diff

Pastikan hanya perubahan task ini.

Periksa agar tidak ada:

.env
secret
credential
log
temporary file
build artifact


==================================================
26. COMMIT
==================================================

Jika seluruh verification PASS:

buat SATU commit.

Gunakan commit message berdasarkan perubahan sebenarnya.

Contoh:

feat: complete botspace api contracts

atau:

fix: harden api functional contracts

Pilih message yang paling sesuai dengan perubahan aktual.

Setelah commit:

git status

git log --oneline -3


==================================================
27. PUSH
==================================================

Push ke:

origin/backend-dev-recovery

Gunakan:

git push

Jangan:

- force push
- ubah remote
- merge
- reset
- rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code.

Pertahankan commit lokal.

Laporkan error sebenarnya.


==================================================
28. FINAL REPORT
==================================================

Setelah selesai tampilkan:

Implementation:
- ...

API:
- Workspace: ...
- Membership: ...
- Bot: ...
- Child resources: ...

Security:
- Authentication: ...
- Authorization: ...
- Cross-workspace isolation: ...
- Input validation: ...
- Secret handling: ...

Persistence:
- Create: ...
- Read: ...
- Update: ...
- Delete: ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Persistence: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

PostgreSQL:
- skipped / passed / failed

Commit:
- hash: ...
- message: ...

Git:
- branch: backend-dev-recovery
- push: success/failed

Working tree:
- clean/dirty

Jika ada failure:

Tampilkan error sebenarnya.

Jangan mengklaim PASS jika sebenarnya skipped atau failed.


==================================================
29. BATASAN SCOPE
==================================================

JANGAN membuat fitur besar baru.

Jangan membuat:

- payment system
- billing
- notification system
- Telegram runtime baru
- frontend redesign
- OAuth baru
- permission system kedua
- database architecture baru
- deployment architecture baru

Fokus hanya pada API functional completeness dari implementation yang sudah ada.


==================================================
30. URUTAN WAJIB
==================================================

Ikuti urutan:

AUDIT
→ INVENTORY API
→ TRACE ROUTE
→ VALIDATION
→ AUTHENTICATION
→ AUTHORIZATION
→ SERVICE
→ DOMAIN
→ REPOSITORY
→ DATABASE
→ RESPONSE
→ ERROR
→ SECURITY REGRESSION
→ API TEST
→ PERSISTENCE TEST
→ FULL VERIFICATION
→ BUILD
→ GIT AUDIT
→ COMMIT
→ PUSH

Jangan berhenti hanya karena unit test PASS.

Pastikan jalur API benar-benar konsisten dari HTTP sampai database.

Selesaikan seluruh scope ini sampai verification selesai.

Jika semua PASS, commit dan push satu kali lalu BERHENTI.

Jangan melanjutkan ke fitur berikutnya setelah push.

```
# 
```



```

# API Contract & Route Completeness.
```
PROMPT: BotSpace — API Contract & Route Completeness Verification

Kita melanjutkan project BotSpace setelah tahap BOT LIFECYCLE dan RESOURCE INTEGRITY yang SUDAH SELESAI.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terakhir:
- Bot lifecycle integrity sudah diverifikasi
- Workspace/resource authorization sudah diverifikasi
- Authentication/session security sudah diverifikasi
- Persistence/runtime verification sudah dilakukan
- Commit lifecycle terakhir sudah dibuat
- Push dilakukan secara manual oleh user jika sebelumnya gagal karena credential GitHub

PENTING:
Jangan reset, force push, rebase sembarangan, checkout branch lain, merge ke backend-dev, atau menghapus checkpoint yang sudah ada.

TUJUAN

Sekarang audit API BotSpace untuk memastikan seluruh route yang memang sudah didukung architecture memiliki:

- authentication yang benar
- authorization yang benar
- input validation yang benar
- response contract yang konsisten
- error handling yang konsisten
- workspace/resource isolation
- tidak ada route yang tertinggal dari security layer sebelumnya

Fokus:

ROUTE INVENTORY
→ AUTHENTICATION
→ AUTHORIZATION
→ INPUT VALIDATION
→ RESPONSE CONTRACT
→ ERROR CONTRACT
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Jangan membuat fitur besar baru.

1. AUDIT SELURUH API ROUTE

Baca struktur services/api dan inventory seluruh route yang benar-benar tersedia.

Kelompokkan:

PUBLIC
- route yang memang boleh tanpa authentication

PROTECTED
- route yang membutuhkan authentication

WORKSPACE-SCOPED
- route yang membutuhkan workspace authorization

BOT-SCOPED
- route yang membutuhkan bot/resource authorization

ADMIN/SYSTEM
- jika memang ada

Jangan membuat route baru hanya untuk melengkapi daftar.

Gunakan route yang benar-benar ada di repository.

2. AUTHENTICATION COVERAGE

Untuk setiap protected route pastikan authentication benar-benar dijalankan.

Cari kemungkinan route yang:

- lupa authentication middleware
- menerima userId dari request
- menerima accountId dari request
- menerima ownerId dari request
- hanya memvalidasi workspaceId
- hanya memvalidasi botId

Authenticated identity harus berasal dari auth/session context.

Tambahkan regression test jika ditemukan route yang sebelumnya belum protected.

3. AUTHORIZATION COVERAGE

Untuk setiap route sensitif pastikan urutannya:

Authentication
→ Current User
→ Workspace Access
→ Membership/Ownership
→ Permission
→ Resource Access
→ Operation

Jangan melakukan mutation sebelum authorization.

Pastikan route tidak hanya mengandalkan frontend.

4. WORKSPACE-SCOPED ROUTE

Audit seluruh route yang menggunakan:

workspaceId

Pastikan user tidak dapat:

- membaca workspace lain
- mengubah workspace lain
- menghapus workspace lain
- membuat resource pada workspace yang tidak dapat diakses
- memodifikasi membership workspace lain

Jika workspaceId berasal dari URL/body/query, tetap lakukan authorization berdasarkan authenticated user.

5. BOT-SCOPED ROUTE

Audit seluruh route yang menggunakan:

botId

Pastikan:

- bot milik workspace sendiri → allowed sesuai permission
- bot workspace lain → denied
- unauthenticated → denied
- invalid bot → error sesuai convention

Audit juga child resource:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- statistics
- configuration

Hanya audit resource yang benar-benar tersedia.

6. INPUT VALIDATION

Audit request schema setiap route.

Pastikan:

- path parameter tervalidasi
- query parameter tervalidasi
- body tervalidasi
- enum tervalidasi
- ID tervalidasi
- required field tervalidasi
- optional field memiliki behavior yang benar

Cari mass assignment.

Field seperti:

- userId
- accountId
- workspaceId
- ownerId
- createdBy
- permissions
- role
- createdAt
- updatedAt

tidak boleh dipercaya dari client jika seharusnya ditentukan server.

Gunakan validation framework yang sudah ada.

Jangan membuat validation framework baru.

7. RESPONSE CONTRACT

Audit response setiap route.

Pastikan response:

- konsisten
- tidak mengembalikan database object mentah jika tidak diperlukan
- tidak membocorkan secret
- tidak membocorkan credential
- tidak membocorkan password
- tidak membocorkan session token
- tidak membocorkan resource workspace lain

Jika DTO/response schema sudah tersedia, gunakan abstraction tersebut.

Jangan mengubah API response tanpa kebutuhan.

8. ERROR CONTRACT

Pastikan route menggunakan error system yang sudah ada.

Bedakan:

- unauthenticated
- unauthorized
- not found
- validation error
- conflict
- domain/business error

Ikuti convention repository.

Jangan membuat error system kedua.

Pastikan error production tidak membocorkan:

- SQL error
- stack trace internal
- credential
- token
- secret
- database structure yang sensitif

9. HTTP METHOD DAN SEMANTIC CHECK

Audit apakah route menggunakan method yang sesuai dengan behavior aktual:

GET
POST
PATCH/PUT
DELETE

Pastikan mutation tidak dapat dilakukan melalui route yang seharusnya read-only.

Pastikan endpoint status seperti enable/disable tetap mengikuti authorization.

Jangan mengubah route contract hanya demi style jika behavior saat ini memang sudah benar.

10. ROUTE DUPLICATION

Cari kemungkinan:

- duplicate endpoint
- duplicate authorization logic
- duplicate validation
- duplicate controller
- duplicate service untuk resource yang sama

Jika ada duplicate yang jelas dan aman diperbaiki, gunakan abstraction yang sudah ada.

Jangan melakukan refactor besar.

11. API CONTRACT TEST

Tambahkan/perbaiki test sesuai route yang memang tersedia.

Minimal test:

Authentication:
- protected route tanpa auth → DENY

Workspace:
- own workspace → PASS
- other workspace → DENY

Bot:
- own bot → PASS
- other workspace bot → DENY

Input:
- invalid ID → DENY
- invalid body → DENY
- missing required field → DENY

Privilege:
- spoofed userId → DENY
- spoofed accountId → DENY
- spoofed ownerId → DENY
- spoofed permissions → DENY
- spoofed role → DENY

Response:
- secret tidak bocor
- credential tidak bocor

Error:
- error type sesuai convention
- tidak ada internal stack trace pada response production

Sesuaikan test dengan route yang benar-benar tersedia.

Jangan membuat test untuk endpoint yang tidak ada.

12. REGRESSION

Pastikan seluruh checkpoint sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- workspace membership
- ownership
- permission policy
- bot authorization
- bot lifecycle
- resource integrity
- persistence/runtime

Jangan melemahkan test lama.

13. API DOCUMENTATION

Periksa apakah repository memiliki dokumentasi API/OpenAPI/schema.

Jika memang sudah ada:

- pastikan route yang tersedia tercermin dengan benar
- pastikan request/response schema tidak bertentangan dengan implementation
- update dokumentasi hanya jika memang sudah stale

Jangan membuat dokumentasi API baru jika project belum menggunakan sistem tersebut.

README.md tetap satu file saja jika perlu diperbarui.

14. TYPESCRIPT QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate controller
- tidak ada duplicate validation
- tidak ada duplicate authorization
- tidak ada circular dependency baru
- tidak ada hardcoded secret

Ikuti architecture repository.

15. BACKWARD COMPATIBILITY

Jangan membuat breaking change.

Sebelum mengubah:

- route path
- HTTP method
- request body
- response schema
- function signature
- service contract
- repository contract

cari seluruh caller dan test yang menggunakan contract tersebut.

Jika contract sudah benar, jangan diubah.

16. VERIFICATION

Setelah implementasi jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- lifecycle tests
- typecheck
- format check
- import boundary check
- lint jika tersedia
- build

Jika ada failure:

1. identifikasi root cause
2. perbaiki
3. jalankan ulang test terkait
4. jalankan full verification kembali

Jangan skip test.

Jangan menghapus test existing.

17. GIT AUDIT

Sebelum commit:

git status
git diff --stat
git diff

Pastikan perubahan hanya terkait API contract/security verification.

Jangan commit:

- .env
- API key
- token
- credential
- log
- temporary files
- build artifacts

18. COMMIT

Jika seluruh verification PASS:

buat SATU commit baru.

Gunakan commit message berdasarkan perubahan sebenarnya.

Contoh:

fix: harden api route contracts

atau:

fix: verify api authorization boundaries

Pilih yang paling sesuai dengan implementation aktual.

Setelah commit:

git status
git log --oneline -3

19. PUSH

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

20. HASIL AKHIR

Tampilkan laporan:

Implementation:
- ...

API Routes:
- jumlah route yang diaudit
- route yang diperbaiki

Security:
- Authentication: ...
- Authorization: ...
- Workspace isolation: ...
- Bot isolation: ...
- Input validation: ...
- Response security: ...
- Error security: ...

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot/Resource: ...
- Lifecycle: ...
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

Jangan membuat fitur baru besar.

Tahap ini hanya:

AUDIT
→ ROUTE INVENTORY
→ AUTHENTICATION
→ AUTHORIZATION
→ INPUT VALIDATION
→ RESPONSE SECURITY
→ ERROR CONTRACT
→ REGRESSION TEST
→ BUILD
→ COMMIT
→ PUSH

Gunakan semua abstraction security yang sudah ada.

Jangan membuat sistem authorization kedua.

Jangan mengubah arsitektur BotSpace secara besar-besaran.

Selesaikan sampai push berhasil lalu berhenti.


```
# Bot Lifecycle & Resource Integrity.
```

PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint security terakhir yang SUDAH BERHASIL DI-PUSH.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terakhir:
d24aeed5d2151484449d94c72609e6f26b332d9c

Status:
- checkpoint sudah berhasil di-push
- working tree harus diverifikasi terlebih dahulu
- jangan reset checkpoint
- jangan force push
- jangan rebase sembarangan
- jangan checkout branch lain
- jangan merge ke backend-dev

TUJUAN

Lanjutkan BotSpace ke tahap berikutnya dengan fokus pada BOT LIFECYCLE dan RESOURCE INTEGRITY.

Tahap sebelumnya sudah mencakup:
- authentication
- session security
- current user
- workspace authorization
- workspace membership
- ownership
- permission policy
- bot resource authorization
- production runtime persistence verification

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

Jangan membuat authorization system kedua.

1. AUDIT TERLEBIH DAHULU

Sebelum mengubah kode:

- cek git status
- baca struktur repository aktual
- baca README.md
- audit bot entity/model
- audit bot repository
- audit bot service
- audit bot API routes
- audit bot lifecycle
- audit bot status
- audit bot configuration
- audit bot credential
- audit child resources yang memiliki botId
- audit workspace → bot relationship
- audit existing tests

Gunakan repository aktual sebagai sumber kebenaran.

Jangan langsung menulis kode sebelum memahami implementasi yang sudah ada.

2. BOT LIFECYCLE

Audit operasi yang memang tersedia:

- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot
- status bot
- configuration
- settings
- commands
- flows
- integrations
- webhook
- credentials
- resource lain yang memiliki botId

Jangan membuat endpoint baru jika belum dibutuhkan architecture.

3. BOT STATE

Identifikasi state bot yang BENAR-BENAR digunakan repository.

Jangan membuat state baru jika belum ada.

Audit seluruh transisi state.

Pastikan hanya user yang memiliki authorization yang sesuai yang dapat mengubah state.

4. INVALID STATE TRANSITION

Periksa kemungkinan transition yang tidak valid berdasarkan implementation aktual.

Contoh jika deleted state memang tersedia:

deleted
→ enable

deleted
→ update

deleted
→ disable

harus ditangani sesuai domain rule yang memang ada.

Jangan membuat state machine baru hanya untuk memperumit architecture.

5. CREATE BOT INTEGRITY

Pastikan create bot:

- menggunakan authenticated user
- workspace valid
- user memiliki akses workspace
- workspaceId tidak dapat digunakan untuk mengakses workspace lain
- ownerId tidak dapat dipalsukan
- accountId tidak dapat dipalsukan
- relationship bot → workspace benar

Jangan mempercayai identity dari request body jika identity sudah tersedia dari authentication context.

6. UPDATE BOT INTEGRITY

Audit semua field update.

Pisahkan:

CLIENT-CONTROLLED

dan

SERVER-CONTROLLED

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

7. DELETE BOT

Pastikan:

- authorization dilakukan sebelum mutation
- cross-workspace delete ditolak
- member tanpa permission delete ditolak
- nonexistent bot mengikuti error convention
- child resource tidak menjadi orphan secara tidak sengaja

Jika project menggunakan soft delete, pertahankan.

Jika hard delete, audit dependency terlebih dahulu.

Jangan mengubah mekanisme delete tanpa alasan nyata.

8. CHILD RESOURCE INTEGRITY

Audit resource yang bergantung pada bot, jika memang tersedia:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- credentials
- analytics
- configuration

Pastikan child resource tidak dapat diakses hanya dengan mengetahui child resource ID.

Contoh:

User A
→ tidak memiliki akses bot-B

maka User A juga tidak boleh:

- mengakses flow-B
- mengakses command-B
- mengakses integration-B
- mengakses webhook-B
- mengakses credential-B

Jangan membuat cascade delete besar-besaran tanpa dukungan architecture.

9. CROSS-WORKSPACE RELATION

Audit relationship:

User
→ Account
→ Telegram Account
→ Workspace
→ Bot
→ Child Resource

Cari kemungkinan:

- bot.workspaceId berbeda dengan workspace yang seharusnya
- ownerId tidak sesuai
- accountId tidak sesuai
- botId tidak valid
- child resource memiliki parent yang salah
- child resource menunjuk ke bot yang sudah tidak valid

Jangan memperbaiki production database secara otomatis.

Fokus pada source code, enforcement, dan test.

10. DATABASE / REPOSITORY

Audit method:

- create
- update
- delete
- status update
- child resource creation

Pastikan repository/service tidak dapat membuat relationship invalid hanya karena input client.

Jika database constraint sudah ada, gunakan sesuai architecture.

Jika ditemukan bug nyata yang membutuhkan migration:

- buat perubahan minimal
- jangan menghapus data
- jangan menyentuh production database
- buat migration aman
- test migration

Jangan membuat migration besar tanpa kebutuhan.

11. CONCURRENCY

Audit mutation yang dapat dipanggil bersamaan.

Contoh:

request A:
enable bot

request B:
disable bot

Pastikan tidak menghasilkan state corrupt.

Jika transaction atau atomic update sudah tersedia, gunakan abstraction existing.

Jangan membuat concurrency framework baru.

12. DUPLICATE RESOURCE

Periksa apakah architecture memiliki aturan uniqueness untuk:

- bot identifier
- Telegram bot token
- external identifier
- workspace resource

Jika memang ada unique/business rule, pastikan enforcement benar.

Jangan membuat business rule baru tanpa bukti dari repository.

13. CREDENTIAL SECURITY

Audit:

- bot token
- Telegram token
- webhook secret
- API key
- integration secret
- access token
- refresh token

Pastikan credential tidak:

- muncul di list bot
- bocor di response yang tidak seharusnya
- masuk log
- masuk error
- masuk analytics
- masuk audit log plaintext
- digunakan sebagai ownership identifier

Jangan menampilkan secret dalam test output.

14. API INPUT VALIDATION

Audit lifecycle input:

- botId
- workspaceId
- status
- configuration
- settings
- commandId
- flowId
- integrationId
- webhookId

Gunakan validation framework yang sudah tersedia.

Jangan membuat framework validation baru.

15. MASS ASSIGNMENT / PRIVILEGE ESCALATION

Cari request body yang memungkinkan user mengirim field sensitif seperti:

- workspaceId
- ownerId
- userId
- accountId
- role
- permissions
- createdBy

Pastikan field server-controlled tidak dapat digunakan untuk privilege escalation.

Authentication context dan authorization policy tetap menjadi sumber kebenaran.

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

17. REGRESSION TEST

Pastikan checkpoint security sebelumnya tetap PASS:

- authentication
- session
- current user
- workspace authorization
- membership
- ownership
- permission policy
- bot resource authorization

Jangan melemahkan test existing.

18. CODE QUALITY

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

Jika diperlukan:

UPDATE README.md yang sudah ada.

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

PROMPT: BotSpace — Production Runtime Persistence Smoke Test

Kita melanjutkan project BotSpace setelah checkpoint:

PERSISTENCE ADAPTER WIRED — READY FOR MANUAL COMMIT/PUSH

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Gunakan source code dan architecture yang sudah ada.

CHECKPOINT TERAKHIR

Persistence foundation sudah berhasil diverifikasi:

- Workspace authorization: PASS
- Membership: PASS
- Bot: PASS
- PostgreSQL connection: PASS
- Migration: PASS
- Schema: PASS
- Migration idempotency: PASS
- Transaction smoke test: PASS
- Runtime startup: PASS
- API process cleanup: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: PASS
- git diff --check: PASS
- Persistence adapter wired: PASS

PostgreSQL integration test juga sudah dijalankan secara eksplisit dengan database yang tersedia dan PASS.

Git saat ini:
- Branch: backend-dev-recovery
- Working tree: DIRTY karena perubahan persistence
- Commit: BELUM dibuat
- Push: BELUM dilakukan

PENTING:

AI JANGAN melakukan:

- git commit
- git push
- git reset
- git clean
- git checkout
- git rebase
- git merge
- force push

USER AKAN COMMIT DAN PUSH MANUAL.

TUJUAN TAHAP INI

Sekarang jangan membuat fitur baru.

Lakukan FINAL PRODUCTION RUNTIME SMOKE TEST untuk memastikan persistence adapter yang baru di-wire benar-benar digunakan oleh runtime aplikasi, bukan hanya lulus test.

Alur:

DATABASE
→ REPOSITORY
→ PERSISTENCE ADAPTER
→ SERVICE
→ RUNTIME
→ API
→ AUTHORIZATION
→ WORKSPACE
→ MEMBERSHIP
→ BOT
→ DATABASE

1. AUDIT RUNTIME BOOTSTRAP

Cari bootstrap runtime aktual.

Pastikan runtime production benar-benar membuat dan memasukkan:

- PostgreSQL/database client
- workspace repository
- membership repository
- bot repository
- authentication/session repository jika tersedia
- persistence adapter
- service layer

Pastikan tidak ada fallback diam-diam ke:

- in-memory repository
- mock repository
- fake adapter
- test adapter
- temporary storage

kecuali memang khusus untuk test environment.

2. RUNTIME HEALTH

Jalankan aplikasi dengan cara resmi repository.

Verifikasi endpoint health/ready yang memang tersedia.

Minimal:

- process startup PASS
- health endpoint PASS
- ready endpoint PASS jika tersedia
- graceful shutdown PASS
- database connection PASS

Jangan membuat endpoint health baru.

3. AUTHENTICATION + PERSISTENCE

Jika authentication/session runtime tersedia, lakukan smoke test:

authenticated request
→ current user
→ session repository
→ PostgreSQL

Pastikan runtime tidak menggunakan mock/in-memory session ketika berjalan dalam production configuration.

4. WORKSPACE RUNTIME

Verifikasi:

- authenticated user dapat mengambil workspace yang memang dia miliki
- workspace repository benar-benar digunakan
- workspace lain tetap ditolak

Jangan hanya memeriksa unit test.

Pastikan request benar-benar melewati runtime → service → repository → PostgreSQL.

5. MEMBERSHIP RUNTIME

Verifikasi:

- membership lookup menggunakan persistence adapter
- authorized member mendapatkan akses
- user tanpa membership ditolak
- cross-workspace access ditolak

Pastikan authorization tetap berjalan sebelum mutation.

6. BOT RUNTIME

Verifikasi minimal operasi bot yang memang tersedia:

- create
- get
- list
- update
- enable
- disable
- delete

Tidak perlu membuat endpoint baru.

Pastikan operasi tersebut menggunakan PostgreSQL-backed repository.

7. PERSISTENCE ROUND TRIP

Jika environment memungkinkan, lakukan smoke test sederhana:

CREATE
→ DATABASE

READ
→ DATABASE

UPDATE
→ DATABASE

READ AGAIN
→ DATABASE

DELETE
→ DATABASE

READ AFTER DELETE
→ expected not found/behavior sesuai architecture

Jangan menggunakan data production.

Gunakan test/temporary data yang aman.

8. RESTART PERSISTENCE TEST

Jika aman dan didukung environment:

1. create test resource
2. pastikan tersimpan
3. restart runtime
4. baca kembali resource tersebut

Tujuan:

membuktikan data tidak hanya berada di memory process.

Jangan melakukan restart terhadap service production yang tidak boleh dihentikan tanpa kebutuhan.

Jika environment tidak aman untuk restart, dokumentasikan sebagai NOT RUN.

9. DATABASE SAFETY

DILARANG:

- DROP DATABASE
- DROP TABLE
- TRUNCATE
- database reset
- destructive migration
- menghapus production data

Jangan mengubah schema jika tidak diperlukan.

10. SECRET SAFETY

Pastikan runtime log tidak menampilkan:

- DATABASE_URL
- password
- API key
- bot token
- session token
- credential
- secret

Jalankan secrets scan yang tersedia.

11. REGRESSION

Pastikan checkpoint security sebelumnya tetap PASS:

- authentication
- session
- workspace authorization
- membership
- ownership
- permission policy
- bot authorization
- bot lifecycle

Jangan melemahkan test existing.

12. TESTING

Jalankan verification resmi repository.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace tests
- membership tests
- bot tests
- PostgreSQL integration tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Jika PostgreSQL integration test memiliki opt-in environment variable:

gunakan database yang memang tersedia dan jalankan test tersebut secara eksplisit.

Jangan menganggap test PASS hanya karena default suite melakukan SKIP.

13. GIT AUDIT

Jangan commit.

Jalankan hanya:

git status
git diff --stat
git diff --check

Pastikan perubahan hanya berasal dari persistence wiring task.

Jangan menghapus perubahan source code.

14. HASIL AKHIR

Tampilkan laporan:

Persistence:
- Adapter wiring: PASS/FAIL
- PostgreSQL: PASS/FAIL
- Repository runtime: PASS/FAIL
- Persistence round trip: PASS/FAIL
- Restart persistence test: PASS/FAIL/NOT RUN

Runtime:
- Startup: PASS/FAIL
- Health: PASS/FAIL
- Shutdown: PASS/FAIL

Security:
- Authentication: PASS/FAIL
- Workspace authorization: PASS/FAIL
- Membership: PASS/FAIL
- Bot authorization: PASS/FAIL
- Secret scan: PASS/FAIL

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- PostgreSQL integration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Git:
- Branch: backend-dev-recovery
- Working tree: clean/dirty
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika semua verification PASS:

PRODUCTION RUNTIME PERSISTENCE VERIFIED — READY FOR MANUAL COMMIT/PUSH

Jika ada masalah:

RUNTIME PERSISTENCE BLOCKED

Tampilkan root cause sebenarnya.

Jangan commit.
Jangan push.
Jangan membuat fitur baru.

STOP setelah verification selesai.

```
# 
```
PROMPT: BotSpace — Persistence Adapter Wiring & Runtime Integration

Kita melanjutkan project BotSpace dari checkpoint terakhir.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Remote:
 https://github.com/zenolamee/botspace.git

CHECKPOINT TERAKHIR

Verification terakhir menunjukkan:

- Authentication: PASS
- Workspace authorization: PASS
- Membership: PASS
- Bot lifecycle: PASS
- Migration: 31/31 PASS
- PostgreSQL: PASS
- Schema tables: 9 present
- Migration history: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- Typecheck: 11/11 PASS
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- git diff --check: PASS

Namun verification runtime menemukan:

- PostgreSQL connection: tersedia
- Migration sudah berjalan
- Repository/database foundation sudah tersedia
- Runtime production bootstrap masih belum sepenuhnya melakukan wiring persistence adapter
- Workspace repository persistence belum sepenuhnya terhubung ke runtime
- Membership repository persistence belum sepenuhnya terhubung ke runtime
- Bot repository persistence belum sepenuhnya terhubung ke runtime
- Beberapa integration/runtime test masih blocked karena adapter belum di-wire ke main runtime

Git:

- Branch: backend-dev-recovery
- Working tree: DIRTY karena perubahan persistence yang sedang dikerjakan
- Commit: JANGAN dibuat
- Push: JANGAN dilakukan
- USER AKAN COMMIT DAN PUSH SECARA MANUAL

JANGAN:
- reset
- force push
- rebase
- merge
- checkout branch lain
- menghapus perubahan existing
- membuat commit
- melakukan push

TUJUAN

Selesaikan wiring persistence adapter dari PostgreSQL ke runtime BotSpace.

Fokus:

DATABASE
→ REPOSITORY
→ PERSISTENCE ADAPTER
→ SERVICE
→ RUNTIME BOOTSTRAP
→ API
→ INTEGRATION TEST

Jangan membuat database system kedua.

Jangan membuat repository system kedua.

Gunakan abstraction persistence/repository yang sudah ada.

1. AUDIT STRUKTUR PERSISTENCE

Sebelum mengubah kode, audit repository aktual.

Cari:

- database client
- PostgreSQL client
- database connection
- Prisma/Drizzle/ORM jika memang digunakan
- repository interface
- repository implementation
- persistence adapter
- workspace repository
- membership repository
- bot repository
- session repository
- user/account repository
- dependency injection
- application container
- runtime bootstrap
- API bootstrap
- test bootstrap

Pahami flow aktual:

API
→ service
→ repository interface
→ persistence adapter
→ PostgreSQL

Jangan membuat abstraction baru jika abstraction tersebut sudah tersedia.

2. AUDIT EXISTING ADAPTER

Cari apakah sudah ada:

- WorkspaceRepository interface
- WorkspaceRepository implementation
- MembershipRepository interface
- MembershipRepository implementation
- BotRepository interface
- BotRepository implementation
- SessionRepository
- UserRepository
- Database adapter

Jika sudah ada:

GUNAKAN IMPLEMENTASI TERSEBUT.

Jangan membuat repository duplicate hanya karena runtime belum menggunakannya.

Jika interface sudah benar tetapi implementation belum selesai, lengkapi implementation minimal yang diperlukan.

3. RUNTIME DEPENDENCY INJECTION

Audit bagaimana application runtime mendapatkan dependency.

Pastikan runtime production memiliki dependency yang benar:

Authentication
→ User/Session repository

Workspace authorization
→ Workspace repository
→ Membership repository

Bot lifecycle
→ Bot repository

Database:
→ PostgreSQL adapter

Jangan membuat singleton global baru jika project sudah memiliki dependency injection/container.

Gunakan pattern yang sudah dipakai repository.

4. WORKSPACE PERSISTENCE

Pastikan operasi workspace yang memang sudah tersedia dapat menggunakan PostgreSQL repository.

Audit:

- create workspace
- get workspace
- list workspace
- update workspace
- delete workspace jika tersedia

Pastikan authorization tetap berjalan sebelum repository mutation.

Jangan melewati authorization hanya karena sekarang menggunakan database persistence.

5. MEMBERSHIP PERSISTENCE

Audit:

- get membership
- list membership
- create membership jika tersedia
- update membership jika tersedia
- remove membership jika tersedia

Pastikan query selalu memiliki workspace/user scope yang benar.

Jangan menggunakan:

findById(id)

secara bebas jika authorization membutuhkan workspace/user context.

Jangan mengizinkan cross-workspace membership access.

6. BOT PERSISTENCE

Audit:

- create bot
- get bot
- list bot
- update bot
- delete bot
- enable bot
- disable bot

Pastikan bot persistence tetap terhubung dengan:

workspaceId
owner/account relationship
authentication context
permission policy

Jangan menerima ownerId atau workspaceId dari client sebagai sumber authorization.

7. SESSION PERSISTENCE

Audit session repository.

Pastikan runtime menggunakan persistence adapter yang benar untuk:

- create session
- validate session
- get current user
- expire session
- revoke session
- logout

Jangan membuat session system kedua.

Jika session saat ini masih menggunakan in-memory storage sementara PostgreSQL adapter sudah tersedia, evaluasi apakah architecture memang mengharuskan persistence production.

Jika memang harus PostgreSQL, wire adapter existing.

8. PRODUCTION RUNTIME

Cari file bootstrap utama.

Contoh kemungkinan:

- main.ts
- server.ts
- app.ts
- bootstrap.ts
- container.ts

Gunakan file aktual repository.

Pastikan production runtime tidak hanya melakukan:

health check
migration
schema initialization

tetapi juga benar-benar menghubungkan repository adapter ke application services.

Jangan mengubah route contract.

9. TEST RUNTIME

Setelah wiring selesai, buat atau perbaiki integration test yang memang sudah didukung architecture.

Minimal verifikasi:

Authentication
→ PostgreSQL session/user repository

Workspace
→ PostgreSQL workspace repository

Membership
→ PostgreSQL membership repository

Bot
→ PostgreSQL bot repository

Authorization
→ PostgreSQL-backed workspace/membership data

Test harus membuktikan bahwa runtime benar-benar menggunakan persistence adapter.

Jangan membuat test yang hanya melakukan mock jika tujuan task adalah membuktikan runtime persistence wiring.

Gunakan integration test yang sesuai dengan infrastructure repository.

10. DATABASE SAFETY

Jangan melakukan perubahan destructive terhadap database.

DILARANG:

- DROP DATABASE
- DROP TABLE
- TRUNCATE
- reset database
- delete production data
- destructive migration

Migration yang sudah ada harus tetap dipertahankan.

Jika migration baru benar-benar diperlukan:

- jelaskan alasannya
- buat migration minimal
- jangan menghapus data
- jalankan migration test
- jalankan idempotency test

Jangan membuat migration jika wiring dapat diselesaikan tanpa schema change.

11. TRANSACTION SAFETY

Audit mutation yang memang membutuhkan transaction.

Minimal periksa:

- workspace creation
- membership creation
- bot creation
- bot deletion
- child resource mutation

Gunakan transaction abstraction yang sudah tersedia jika memang dibutuhkan.

Jangan membuat transaction framework baru.

12. ERROR HANDLING

Gunakan error system existing.

Pastikan database error tidak membocorkan:

- connection string
- password
- DATABASE_URL
- credential
- secret
- SQL internal detail pada production response

Mapping error harus tetap konsisten:

authentication
→ authentication error

authorization
→ authorization error

not found
→ not found

database failure
→ internal/database error sesuai convention

13. ENVIRONMENT SECURITY

Audit database configuration.

Pastikan:

- DATABASE_URL tidak hardcoded
- password tidak hardcoded
- credential tidak masuk source code
- secret tidak masuk test output
- `.env` tidak diubah menjadi tracked file
- runtime tidak mencetak DATABASE_URL

Jangan mengubah production secret.

14. TESTING

Jalankan verification sebelum dan sesudah perubahan jika memungkinkan.

Minimal:

- domain tests
- API tests
- authentication tests
- session tests
- workspace tests
- membership tests
- bot tests
- database migration tests
- integration tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Khusus database:

- PostgreSQL connection
- migration
- schema validation
- migration idempotency
- transaction smoke test

Jangan skip test existing.

15. RUNTIME SMOKE TEST

Setelah adapter selesai di-wire, lakukan smoke test runtime.

Minimal pastikan:

/health

atau endpoint health yang memang tersedia:

HTTP 200

Kemudian endpoint runtime yang membutuhkan authentication dan persistence harus dapat mencapai repository layer tanpa:

- "repository unavailable"
- "adapter not wired"
- "not implemented"
- "persistence unavailable"

Jangan mengklaim production ready jika runtime masih menggunakan stub untuk operasi yang seharusnya sudah persistent.

16. JANGAN MEMBUAT FITUR BARU

Jangan menambahkan:

- UI baru
- endpoint baru
- authentication system baru
- permission system baru
- database schema besar
- bot feature baru
- deployment infrastructure baru

Task ini hanya:

PERSISTENCE ADAPTER
→ RUNTIME WIRING
→ DATABASE INTEGRATION
→ TEST

17. TYPESCRIPT QUALITY

Pastikan:

- tidak menambahkan any tanpa alasan
- tidak menambahkan @ts-ignore
- tidak ada unused import
- tidak ada dead code
- tidak ada duplicate repository
- tidak ada duplicate adapter
- tidak ada circular dependency baru
- tidak ada hardcoded credential

Ikuti architecture repository.

18. BACKWARD COMPATIBILITY

Jangan merusak API existing.

Sebelum mengubah:

- constructor
- dependency injection
- service signature
- repository interface
- bootstrap contract

cari seluruh caller.

Update caller dan test yang relevan.

Jangan membuat breaking change tanpa alasan.

19. README

Jika wiring persistence memerlukan dokumentasi:

UPDATE README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan singkat:

- persistence architecture
- PostgreSQL adapter
- runtime wiring
- test command

20. VERIFICATION FINAL

Setelah implementation selesai jalankan full verification.

Minimal:

- Domain: PASS
- API: PASS
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot: PASS
- Database migration: PASS
- PostgreSQL connection: PASS
- Integration: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: PASS

Jika ada failure:

1. cari root cause
2. perbaiki
3. ulangi test terkait
4. ulangi full verification

Jangan skip test.

21. GIT — SANGAT PENTING

USER AKAN COMMIT DAN PUSH MANUAL.

AI DILARANG:

- git add
- git commit
- git push
- git reset
- git checkout
- git clean
- git rebase
- git merge
- force push

Setelah selesai cukup jalankan:

git status
git diff --stat
git diff --check

Jika diperlukan untuk verification, boleh membaca:

git log --oneline -3

Tetapi JANGAN membuat commit.

Working tree harus tetap berisi perubahan source code yang dibuat.

22. HASIL AKHIR

Tampilkan laporan:

Implementation:
- persistence adapter yang di-wire
- runtime yang diperbaiki
- repository yang sekarang benar-benar digunakan

Database:
- PostgreSQL: PASS/FAIL
- Migration: PASS/FAIL
- Transaction: PASS/FAIL

Runtime:
- Bootstrap: PASS/FAIL
- Health: PASS/FAIL
- Persistence integration: PASS/FAIL

Tests:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Database: ...
- Integration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Git:
- Branch: backend-dev-recovery
- Working tree: clean/dirty
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika semua verification PASS:

PERSISTENCE ADAPTER WIRED — READY FOR MANUAL COMMIT/PUSH

Jika masih ada blocker:

PERSISTENCE WIRING BLOCKED

Tampilkan blocker sebenarnya.

Jangan mengklaim persistence sudah production-ready jika runtime masih menggunakan adapter/stub yang belum di-wire.

23. PENTING

Tujuan task ini bukan membuat fitur baru.

Tujuannya memastikan persistence foundation yang sudah tersedia benar-benar digunakan oleh runtime.

Alur:

AUDIT
→ DATABASE
→ REPOSITORY
→ ADAPTER
→ DEPENDENCY INJECTION
→ RUNTIME
→ AUTH/WORKSPACE/BOT
→ INTEGRATION TEST
→ BUILD
→ GIT DIFF CHECK

STOP setelah verification selesai.

JANGAN COMMIT.
JANGAN PUSH.
USER AKAN PUSH MANUAL.


```
# 
```
PROMPT: BotSpace — Complete Bot Lifecycle Contracts & Mutation Policies

Lanjutkan project BotSpace dari hasil audit Bot Lifecycle terakhir.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

STATUS TERAKHIR:
- Authentication: VERIFIED
- Workspace authorization: VERIFIED
- Membership: VERIFIED
- Ownership: VERIFIED
- Permission policy: VERIFIED
- Bot resource authorization: VERIFIED
- Persistence foundation: VERIFIED
- Migration: PASS
- Typecheck: PASS
- Build: PASS
- Working tree: DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

HASIL AUDIT TERAKHIR:

Bot lifecycle saat ini hanya memiliki contract/operation yang benar-benar tersedia untuk:

- create
- get
- list

Operation berikut belum tersedia secara intentional:

- update
- delete
- enable
- disable
- credential mutation

Jangan mengklaim operation tersebut sudah aman/teruji sebelum contract dan policy-nya benar-benar tersedia.

PENTING:
- JANGAN commit.
- JANGAN push.
- User akan commit dan push manual.
- Jangan reset.
- Jangan force push.
- Jangan rebase.
- Jangan merge.
- Jangan checkout branch lain.
- Jangan menghapus perubahan persistence/lifecycle yang sudah ada.

TUJUAN

Sekarang audit dan, jika memang sesuai architecture, lengkapi contract/domain policy untuk operasi bot lifecycle yang belum tersedia.

Alur:

AUTHENTICATION
→ CURRENT USER
→ WORKSPACE ACCESS
→ BOT AUTHORIZATION
→ LIFECYCLE POLICY
→ MUTATION CONTRACT
→ REPOSITORY
→ TEST

Jangan membuat authorization system kedua.

1. AUDIT CONTRACT AKTUAL

Sebelum coding, cari seluruh contract yang sudah tersedia untuk Bot.

Cari:

- Bot entity/model
- Bot repository interface
- Bot service
- Bot use case
- Bot API route
- DTO/schema
- command/input type
- output/result type
- permission policy
- authorization helper
- status/state representation
- credential representation
- existing tests

Tentukan secara jelas:

SUPPORTED:
- create
- get
- list

UNSUPPORTED:
- update
- delete
- enable
- disable
- credential mutation

Jangan mengasumsikan operation yang belum ada.

2. JANGAN MEMBUAT FITUR BESAR

Fokus hanya pada contract dan policy yang memang dibutuhkan untuk lifecycle.

Jangan membuat:

- UI baru
- dashboard baru
- bot deployment system baru
- webhook system baru
- Telegram integration baru
- credential provider baru
- background worker baru
- queue baru

Jika repository belum memiliki infrastructure untuk operation tertentu, jangan membangun infrastructure besar hanya untuk task ini.

3. BOT UPDATE CONTRACT

Jika architecture repository memang mendukung update bot, buat contract minimal yang aman.

Audit field yang boleh diubah.

Pisahkan:

CLIENT-CONTROLLED:
- name
- description
- configuration
- settings
- field lain yang memang sudah menjadi bagian model

SERVER-CONTROLLED:
- id
- workspaceId
- ownerId
- accountId
- createdBy
- createdAt
- updatedAt
- authorization metadata

Jangan izinkan client mengubah server-controlled field.

Jika update bot belum benar-benar dibutuhkan oleh model/domain saat ini, jangan memaksakannya.

4. BOT DELETE CONTRACT

Jika delete memang didukung architecture:

buat contract/service policy yang jelas.

Authorization wajib:

Authentication
→ Workspace Access
→ Bot Access
→ Delete Permission
→ Delete

Pastikan user workspace lain ditolak.

Pastikan child resources tidak menjadi orphan secara tidak sengaja.

Jika project menggunakan soft delete, pertahankan soft delete.

Jangan mengubah hard delete menjadi soft delete atau sebaliknya tanpa bukti.

5. BOT ENABLE / DISABLE POLICY

Jika bot memiliki status yang memang mendukung active/inactive/disabled:

audit state yang sebenarnya digunakan.

Jangan membuat state baru.

Buat policy yang jelas untuk:

enable
disable

Authorization wajib dilakukan sebelum mutation.

Jangan mengizinkan:

user workspace A
→ bot workspace B
→ enable/disable

6. CREDENTIAL MUTATION

Jangan langsung membuat credential architecture baru.

Audit credential model yang sudah ada.

Jika credential mutation memang sudah memiliki repository/service support:

pastikan policy-nya:

- authenticated
- workspace authorized
- bot authorized
- permission verified

Credential tidak boleh digunakan sebagai sumber ownership.

Credential tidak boleh menentukan workspace.

Credential tidak boleh bocor ke response/log/error.

Jika credential mutation belum didukung architecture, dokumentasikan sebagai UNSUPPORTED dan jangan membuat sistem baru.

7. OWNERSHIP PROTECTION

Pastikan update contract tidak dapat digunakan untuk:

- mengubah workspaceId
- mengubah ownerId
- mengubah accountId
- mengubah createdBy

Tidak ada transfer ownership pada task ini.

Jika transfer ownership belum menjadi fitur resmi, jangan membuatnya.

8. PERMISSION POLICY

Gunakan permission abstraction yang sudah ada.

Jangan membuat permission system baru.

Policy harus dapat membedakan minimal:

- bot read
- bot create
- bot update
- bot delete
- bot status mutation
- credential mutation

Hanya tambahkan permission yang memang diperlukan dan konsisten dengan policy existing.

Jangan menggunakan wildcard permission hanya untuk mempermudah implementation.

9. API CONTRACT

Jika API route untuk operation tersebut memang sudah ada:

hubungkan ke contract/policy yang benar.

Jika route belum ada:

jangan otomatis membuat banyak endpoint.

Prioritaskan domain/service contract terlebih dahulu.

Buat API hanya jika architecture repository memang sudah memiliki pola route untuk operation lifecycle tersebut.

10. REPOSITORY CONTRACT

Audit repository.

Jika method sudah tersedia:

- gunakan method existing.

Jika method belum tersedia tetapi mutation memang dibutuhkan oleh domain:

tambahkan method minimal.

Contoh konsep:

updateBot
deleteBot
updateBotStatus

Gunakan naming convention repository yang sudah ada.

Jangan membuat repository kedua.

11. INPUT VALIDATION

Pastikan input contract memvalidasi:

- botId
- configuration
- settings
- status jika memang diperlukan

Jangan menerima:

- ownerId
- workspaceId
- accountId
- createdBy

sebagai authorization source.

Jika field tersebut ada di request, harus diabaikan/ditolak sesuai convention existing.

12. ERROR CONTRACT

Gunakan error system existing.

Bedakan:

Unauthenticated
→ authentication error

Authenticated tetapi tidak punya workspace access
→ authorization error

Bot tidak ditemukan
→ not found

Invalid state
→ domain/validation error

Invalid input
→ validation error

Jangan membuat error system kedua.

13. TEST CONTRACT

Tambahkan test untuk contract/policy yang benar-benar dibuat.

Minimal:

Update:
- authorized update PASS
- unauthorized update DENY
- cross-workspace update DENY
- workspaceId spoof DENY
- ownerId spoof DENY

Delete:
- authorized delete PASS
- unauthorized delete DENY
- cross-workspace delete DENY

Status:
- authorized enable PASS
- unauthorized enable DENY
- cross-workspace enable DENY
- authorized disable PASS
- unauthorized disable DENY
- cross-workspace disable DENY

Credential:
- authorized mutation PASS jika contract memang tersedia
- unauthorized mutation DENY
- cross-workspace mutation DENY
- secret tidak muncul pada output

Jika operation tertentu tetap UNSUPPORTED karena architecture belum menyediakan foundation yang diperlukan:

JANGAN membuat test palsu.

Laporkan operation tersebut sebagai:

UNSUPPORTED — CONTRACT NOT AVAILABLE

14. REGRESSION

Pastikan test lama tetap PASS:

- authentication
- session
- workspace authorization
- membership
- ownership
- permission
- bot create
- bot get
- bot list
- persistence
- migration

Jangan menghapus atau skip test existing.

15. DATABASE SAFETY

Jangan membuat migration baru kecuali contract baru benar-benar membutuhkan perubahan schema.

Jangan:

- reset database
- truncate
- delete production data
- mengubah production database

Jika schema sudah cukup, gunakan schema existing.

16. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore
- tidak ada duplicate policy
- tidak ada duplicate repository
- tidak ada unused import
- tidak ada dead code
- tidak ada circular dependency baru
- tidak ada hardcoded secret

17. README

Jika diperlukan:

UPDATE README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan singkat:

- bot lifecycle contracts
- supported operations
- unsupported operations
- authorization policy
- test command

18. VERIFICATION

Setelah implementation:

jalankan:

- domain tests
- API tests jika tersedia
- authentication/session tests
- workspace authorization tests
- membership tests
- bot tests
- persistence tests
- migration tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Jika failure:

1. cari root cause
2. perbaiki
3. ulangi test terkait
4. ulangi full verification

Jangan skip test.

19. GIT

JANGAN commit.

JANGAN push.

Setelah verification selesai hanya jalankan:

git status
git diff --stat
git diff --check

Pastikan semua perubahan tetap berada di working tree.

20. FINAL REPORT

Tampilkan:

BOT LIFECYCLE CONTRACTS:
- Create: SUPPORTED/...
- Get: SUPPORTED/...
- List: SUPPORTED/...
- Update: SUPPORTED/UNSUPPORTED + alasan
- Delete: SUPPORTED/UNSUPPORTED + alasan
- Enable: SUPPORTED/UNSUPPORTED + alasan
- Disable: SUPPORTED/UNSUPPORTED + alasan
- Credential mutation: SUPPORTED/UNSUPPORTED + alasan

POLICY:
- Workspace authorization: ...
- Bot authorization: ...
- Permission: ...
- Ownership protection: ...

TESTS:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Persistence: ...
- Migration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

GIT:
- Branch: backend-dev-recovery
- Working tree: CLEAN/DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika contract/policy yang tersedia sudah benar:

BOT LIFECYCLE CONTRACTS VERIFIED — READY FOR MANUAL COMMIT/PUSH

Jika masih ada operation yang memang belum didukung:

BOT LIFECYCLE PARTIALLY VERIFIED

dan tampilkan dengan jelas operation mana yang UNSUPPORTED serta alasan sebenarnya.

Jangan mengklaim update/delete/enable/disable/credential mutation berhasil jika contract atau implementation-nya memang belum tersedia.

Berhenti setelah laporan akhir.


```
# Bot Lifecycle & Resource Integrity.
```

PROMPT: BotSpace — Bot Lifecycle & Resource Integrity

Lanjutkan project BotSpace dari hasil Persistence Foundation yang baru selesai.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

STATUS TERAKHIR:
- Workspace authorization: PASS
- Membership: PASS
- Bot: PASS
- Migration: 31/31 PASS
- pnpm check: 44/44 successful
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- git diff --check: PASS
- Persistence Foundation: VERIFIED
- Working tree: DIRTY karena perubahan persistence belum di-commit

PENTING:
JANGAN commit.
JANGAN push.
User akan commit dan push secara manual.

JANGAN reset, force push, rebase, merge, atau checkout branch lain.

TUJUAN:

Setelah PostgreSQL persistence, Workspace, Membership, dan Bot repository sudah tersedia, sekarang audit dan hardening BOT LIFECYCLE.

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

1. AUDIT BOT LIFECYCLE

Audit implementasi yang sudah ada untuk:

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
- child resource yang memiliki botId

Jangan membuat endpoint baru jika tidak diperlukan.

2. BOT OWNERSHIP

Pastikan setiap bot:

- selalu memiliki workspace valid
- dibuat oleh authenticated user
- user memiliki akses ke workspace
- tidak dapat dibuat menggunakan workspace milik user lain
- tidak dapat dipindahkan ke workspace lain melalui update biasa
- owner/workspace tidak dapat dipalsukan dari request body

Authorization harus tetap menggunakan authentication context + workspace membership/permission.

3. BOT READ

Audit:

- get bot
- list bot

Pastikan user hanya dapat melihat bot yang berada pada workspace yang memang dapat dia akses.

Cross-workspace access harus DENY meskipun user mengetahui botId.

4. BOT UPDATE

Audit semua field yang dapat diubah.

Khusus:

- workspaceId
- ownerId
- accountId
- createdBy
- status
- permissions
- credentials

Jangan izinkan update biasa mengubah ownership/workspace jika architecture tidak mendukungnya.

Gunakan explicit field mapping jika diperlukan.

5. BOT DELETE

Pastikan:

- authorization dilakukan sebelum delete
- cross-workspace delete ditolak
- member tanpa permission delete ditolak
- nonexistent bot mengikuti error convention
- child resource tidak menjadi orphan secara tidak sengaja

Jangan mengubah soft-delete menjadi hard-delete atau sebaliknya tanpa alasan.

6. BOT ENABLE / DISABLE

Audit seluruh state mutation:

- enable
- disable
- activate
- deactivate
- start
- stop

Gunakan state yang memang sudah ada.

Jangan membuat state baru hanya untuk task ini.

Pastikan user tidak dapat mengubah status bot workspace lain.

7. INVALID STATE

Jika project memiliki deleted/inactive/stopped state, audit transisi seperti:

deleted → enable
deleted → update
deleted → disable

Pertahankan behavior architecture yang sudah ada.

Jangan membuat state machine baru jika belum diperlukan.

8. CHILD RESOURCE

Audit resource yang bergantung pada bot, jika tersedia:

- commands
- flows
- settings
- integrations
- webhooks
- logs
- statistics
- credentials
- configuration

Pastikan child resource selalu mengikuti workspace/bot authorization.

User yang tidak dapat mengakses bot tidak boleh mengakses child resource hanya dengan mengetahui child resource ID.

9. CROSS-WORKSPACE INTEGRITY

Audit seluruh relasi:

User
→ Account
→ Workspace
→ Bot
→ Bot Resource

Cari kemungkinan:

- bot.workspaceId berbeda dengan parent workspace
- bot.ownerId tidak sesuai
- bot.accountId tidak sesuai
- child resource memiliki botId invalid
- child resource memiliki workspaceId yang berbeda dari bot
- orphan resource

Jangan memperbaiki data production secara destructive.

Fokus pada enforcement dan test.

10. CREDENTIAL SECURITY

Audit bot credential handling.

Pastikan credential:

- tidak menentukan ownership
- tidak menentukan workspace
- tidak muncul pada list response
- tidak bocor pada error
- tidak masuk log
- tidak dapat diubah tanpa permission
- tetap terikat pada bot yang benar

Jangan menampilkan secret dalam test output.

11. DATABASE CONSISTENCY

Karena PostgreSQL persistence baru saja selesai:

audit repository PostgreSQL untuk:

- Workspace
- Membership
- Bot

Pastikan query menggunakan schema/migration aktual.

Jangan membuat migration baru kecuali benar-benar diperlukan.

Jangan reset database.
Jangan truncate.
Jangan menghapus data.

12. AUTHORIZATION ORDER

Pastikan flow mutation:

Authentication
→ Current User
→ Workspace Access
→ Permission
→ Bot Authorization
→ Mutation
→ Repository

Jangan melakukan mutation sebelum authorization.

Jangan mempercayai workspaceId/ownerId dari client sebagai sumber authorization.

13. TEST WAJIB

Tambahkan/perbaiki test sesuai resource yang benar-benar tersedia.

Create:
- authenticated + valid workspace = PASS
- unauthenticated = DENY
- cross-workspace = DENY
- spoofed ownerId = DENY
- spoofed accountId = DENY

Read:
- own workspace bot = PASS
- other workspace bot = DENY

Update:
- authorized update = PASS
- unauthorized update = DENY
- workspaceId spoof = DENY
- ownerId spoof = DENY

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
- authorized access = PASS
- cross-workspace access = DENY
- invalid parent relation = DENY

14. REGRESSION

Pastikan checkpoint sebelumnya tetap PASS:

- Authentication
- Session
- Workspace authorization
- Membership
- Ownership
- Permission
- Persistence
- Bot authorization

Jangan melemahkan test existing.

15. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore baru
- tidak ada duplicate authorization system
- tidak ada duplicate repository
- tidak ada unused import
- tidak ada dead code
- tidak ada circular dependency baru
- tidak ada hardcoded secret

16. README

Jika diperlukan, update README.md yang sudah ada.

JANGAN membuat README baru.

Dokumentasikan singkat:

- bot lifecycle
- bot authorization
- persistence
- test command

17. VERIFICATION

Setelah implementasi jalankan:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- persistence tests
- migration tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Jika gagal:

1. cari root cause
2. perbaiki
3. ulangi test terkait
4. ulangi full verification

Jangan skip test.

18. GIT

JANGAN commit.
JANGAN push.

Setelah semua selesai hanya jalankan:

git status
git diff --stat
git diff --check

Pastikan perubahan persistence + lifecycle memang berada di working tree.

Jangan membuat commit.

19. FINAL REPORT

Tampilkan:

BOT LIFECYCLE:
- Create: ...
- Read: ...
- Update: ...
- Delete: ...
- Enable/Disable: ...

RESOURCE INTEGRITY:
- Workspace relation: ...
- Ownership: ...
- Child resources: ...
- Credentials: ...

PERSISTENCE:
- PostgreSQL: ...
- Workspace repository: ...
- Membership repository: ...
- Bot repository: ...

TESTS:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Persistence: ...
- Migration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

GIT:
- Branch: backend-dev-recovery
- Working tree: CLEAN/DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika semua verification PASS:

BOT LIFECYCLE VERIFIED — READY FOR MANUAL COMMIT/PUSH

Jika masih ada masalah:

BOT LIFECYCLE BLOCKED — tampilkan root cause sebenarnya.

Berhenti setelah laporan akhir.

Jangan commit.
Jangan push.

```

# 
```
PROMPT: BotSpace — Minimal PostgreSQL Persistence Foundation

Lanjutkan BotSpace dari hasil verification terakhir.

Repository:
/root/botspace

Branch:
backend-dev-recovery

Checkpoint:
d24aeed5d2151484449d94c72609e6f26b332d9c

STATUS TERAKHIR:

- Domain checks: PASS
- API checks: PASS
- pnpm check: 44/44 successful
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- Database migration test: 31 passed, 0 failed
- PostgreSQL 16: PASS
- Migration 0001–0003: PASS
- Schema tables: 9 present
- Migration history: PASS
- Constraints/FKs/indexes/triggers: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- /health: HTTP 200
- /ready: HTTP 200
- Authentication/session route: VERIFIED
- Working tree: CLEAN
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

HASIL AUDIT TERAKHIR:

Workspace persistence: BLOCKED
Membership persistence: BLOCKED
Bot persistence: BLOCKED

Root cause yang ditemukan:

- belum ada PostgreSQL persistence adapter yang dapat digunakan runtime
- belum ada database client/runtime connection yang terintegrasi dengan application layer
- belum ada DI/container minimal untuk menyediakan repository
- workspace/membership/bot repository belum dapat di-resolve oleh runtime

PENTING:

Pada tahap sebelumnya kita mengira adapter PostgreSQL sudah tersedia.

Audit terbaru membuktikan bahwa infrastructure tersebut MEMANG BELUM ADA.

Karena itu, kali ini BOLEH membuat persistence foundation minimal yang benar-benar diperlukan.

Jangan hanya membuat wiring palsu agar verification terlihat PASS.

TUJUAN:

Buat minimal persistence foundation:

PostgreSQL Client
→ Persistence Adapter
→ Repository
→ Service
→ Application Runtime

untuk:

- Workspace
- Workspace Membership
- Bot

Fokus hanya pada foundation yang diperlukan.

Jangan membuat fitur baru di luar scope.

1. AUDIT ULANG REPOSITORY

Sebelum coding:

- audit package structure
- audit domain interfaces
- audit service interfaces
- audit API/application bootstrap
- audit database schema
- audit migration 0001–0003
- audit database configuration
- cari repository interface yang sudah ada
- cari model/entity yang sudah ada
- cari query/database abstraction yang sudah tersedia
- cari dependency yang sudah terinstall untuk PostgreSQL

Jangan membuat abstraction duplicate jika sebenarnya sudah ada dalam bentuk berbeda.

Gunakan architecture aktual repository sebagai sumber kebenaran.

2. DATABASE CLIENT

Jika belum ada PostgreSQL client:

buat satu database client abstraction minimal.

Gunakan dependency PostgreSQL yang memang sudah tersedia atau tambahkan dependency resmi yang sesuai dengan package manager project.

Jangan membuat database engine sendiri.

Jangan membuat ORM baru.

Jangan menambahkan Prisma/Drizzle/TypeORM hanya karena lebih mudah jika project tidak menggunakannya.

Pilih pendekatan paling minimal dan konsisten dengan repository.

DATABASE_URL harus berasal dari environment.

Jangan hardcode credential.

3. DATABASE CONFIGURATION

Buat configuration layer minimal jika belum tersedia.

Minimal support:

DATABASE_URL

Pastikan:

- production/runtime menggunakan environment
- test dapat menggunakan environment/test database sesuai architecture
- secret tidak dicetak ke log
- DATABASE_URL tidak muncul pada error response
- database client dapat ditutup dengan graceful shutdown

Jangan mengubah .env production.

Jangan membuat credential palsu.

4. PERSISTENCE ADAPTER

Buat persistence adapter minimal.

Tujuannya menyediakan database access kepada repository.

Architecture yang diinginkan:

Application
↓
Service
↓
Repository interface
↓
PostgreSQL repository implementation
↓
PostgreSQL client
↓
PostgreSQL

Jangan membiarkan service/API melakukan SQL langsung jika repository abstraction sudah digunakan.

Jangan membuat repository abstraction kedua.

5. WORKSPACE REPOSITORY

Implementasikan repository PostgreSQL untuk Workspace sesuai interface/domain yang sudah ada.

Gunakan schema/migration aktual.

Jangan menebak nama kolom.

Audit migration terlebih dahulu.

Implementasikan hanya operasi yang memang dibutuhkan oleh service saat ini.

Contoh jika interface memang tersedia:

- create
- findById
- findByOwner
- list
- update
- delete

Jangan membuat method yang tidak diperlukan.

6. MEMBERSHIP REPOSITORY

Implementasikan persistence untuk workspace membership sesuai domain yang sudah ada.

Gunakan table/schema aktual.

Implementasikan operasi yang memang sudah digunakan application:

- find membership
- list members
- create membership
- update membership jika tersedia
- remove membership jika tersedia

Pastikan workspaceId dan user/account identity tetap konsisten.

Jangan membuat membership system baru.

7. BOT REPOSITORY

Implementasikan persistence repository untuk Bot sesuai interface/domain yang sudah ada.

Gunakan schema aktual.

Support hanya operasi yang memang digunakan:

- create
- findById
- list by workspace
- update
- delete
- status update jika memang tersedia

Bot harus tetap terikat dengan workspace.

Jangan menerima ownership palsu dari client.

8. QUERY SAFETY

Semua repository query harus mengikuti schema aktual.

Jangan menggunakan:

findById(id)

secara sembarangan untuk resource workspace-scoped jika authorization membutuhkan workspace scope.

Pastikan service/policy tetap melakukan authorization.

Persistence repository tidak boleh menjadi jalan bypass authorization.

Flow harus tetap:

Authentication
→ Current User
→ Workspace Authorization
→ Permission
→ Service
→ Repository
→ PostgreSQL

9. DI / COMPOSITION ROOT

Buat dependency injection minimal hanya jika memang belum ada.

Contoh konsep:

createDatabaseClient()
→ createPersistenceRepositories()
→ createServices()
→ createApplication()

Jangan membuat framework DI besar.

Tidak perlu dependency injection library tambahan jika factory function sederhana sudah cukup.

Pastikan hanya ada SATU database client utama untuk runtime.

10. RUNTIME BOOTSTRAP

Integrasikan persistence container ke application bootstrap.

Pastikan runtime production tidak lagi menghasilkan:

Workspace: BLOCKED
Membership: BLOCKED
Bot: BLOCKED

karena repository tidak tersedia.

Pastikan application startup gagal secara jelas jika DATABASE_URL diperlukan tetapi tidak tersedia.

Jangan fallback diam-diam ke fake/in-memory repository pada production.

11. TEST ADAPTER

Bila repository test/in-memory adapter sudah ada:

- pertahankan
- jangan menggantinya dengan PostgreSQL

Jika test repository belum ada:

buat test minimal untuk PostgreSQL repository hanya jika environment test database memang tersedia.

Jangan membuat test yang membutuhkan database eksternal jika environment tidak tersedia hanya untuk memaksa PASS.

Bedakan:

UNIT TEST

dan:

RUNTIME/POSTGRESQL VERIFICATION

12. MIGRATION

Migration 0001–0003 sudah PASS.

JANGAN membuat migration baru kecuali audit schema membuktikan ada table/column/index yang benar-benar diperlukan tetapi belum tersedia.

Jika schema sudah cukup:

JANGAN mengubah migration.

Jangan:

- drop table
- truncate
- reset database
- menghapus migration
- mengubah migration history

13. TRANSACTION

Gunakan transaction abstraction PostgreSQL jika repository/service memang membutuhkan atomic operation.

Jangan membuat transaction framework baru.

Minimal pastikan connection lifecycle aman.

14. ERROR HANDLING

Database error tidak boleh membocorkan:

- DATABASE_URL
- password
- credential
- SQL secret
- connection string

Gunakan error abstraction project yang sudah ada.

Jangan mengubah semua error system hanya karena persistence dibuat.

15. GRACEFUL SHUTDOWN

Jika application sudah memiliki shutdown handling:

integrasikan database client ke lifecycle tersebut.

Pastikan:

startup
→ database connection
→ application running

shutdown
→ stop server
→ close database connection

Jangan membuat shutdown system kedua.

16. SECURITY

Pastikan:

- DATABASE_URL hanya dari environment
- password database tidak di-log
- query menggunakan parameterized values
- tidak ada SQL string interpolation dari user input
- tidak ada credential hardcoded
- database errors disanitasi
- repository tidak bypass authorization

17. TESTING

Setelah implementasi:

jalankan:

- domain tests
- API tests
- persistence/repository tests jika tersedia
- authentication/session tests
- workspace authorization tests
- membership tests
- bot tests
- database migration tests
- typecheck
- format
- import boundary
- lint jika tersedia
- build

Kemudian jalankan runtime smoke test.

18. RUNTIME VERIFICATION

Dengan PostgreSQL environment yang tersedia, verifikasi:

/health
→ HTTP 200

/ready
→ HTTP 200

Authentication/session
→ PASS

Workspace repository
→ RESOLVED

Membership repository
→ RESOLVED

Bot repository
→ RESOLVED

Database connection
→ PASS

Migration state
→ PASS

Jika DATABASE_URL tidak tersedia:

jangan membuat fake database.

Laporkan:

PERSISTENCE FOUNDATION IMPLEMENTED — DATABASE ENVIRONMENT BLOCKER REMAINS

19. DATA SAFETY

Jangan menghapus data existing.

Jangan reset database.

Jangan truncate.

Jangan menjalankan destructive command.

Jika membutuhkan test record:

gunakan mekanisme test fixture yang sudah tersedia dan jangan merusak data existing.

20. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore
- tidak ada duplicate repository
- tidak ada duplicate database client
- tidak ada duplicate DI container
- tidak ada unused import
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- tidak ada debug logging
- tidak ada fake production adapter

21. README

Update README.md yang sudah ada HANYA jika diperlukan.

Dokumentasikan singkat:

- DATABASE_URL
- PostgreSQL persistence
- repository architecture
- runtime startup requirement
- test/verification command

Jangan membuat README baru.

22. GIT

PENTING:

JANGAN COMMIT.

JANGAN PUSH.

User akan melakukan commit/push manual.

Setelah perubahan:

git status
git diff --stat
git diff

Jangan:

- reset
- force push
- rebase
- merge
- checkout branch lain

23. FINAL REPORT

Tampilkan:

ROOT CAUSE:
- ...

IMPLEMENTATION:
- PostgreSQL client: ...
- Database configuration: ...
- Persistence adapter: ...
- Workspace repository: ...
- Membership repository: ...
- Bot repository: ...
- DI/composition root: ...
- Runtime bootstrap: ...

DATABASE:
- PostgreSQL: ...
- Migration 0001–0003: ...
- Schema: ...

RUNTIME:
- /health: ...
- /ready: ...
- Auth/session: ...
- Workspace repository: ...
- Membership repository: ...
- Bot repository: ...

TESTS:
- Domain: ...
- API: ...
- Persistence: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Migration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

GIT:
- Branch: backend-dev-recovery
- Working tree: CLEAN/DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika PostgreSQL tersedia dan semua repository berhasil di-wire:

PERSISTENCE FOUNDATION VERIFIED — READY FOR MANUAL COMMIT/PUSH

Jika code selesai tetapi DATABASE_URL/PostgreSQL runtime tidak tersedia:

PERSISTENCE FOUNDATION COMPLETE — ENVIRONMENT BLOCKER REMAINS

Jika repository masih gagal:

BLOCKED — PERSISTENCE FOUNDATION INCOMPLETE

Jangan mengklaim PASS jika repository masih unavailable.

FOKUS:

AUDIT
→ POSTGRESQL CLIENT
→ DATABASE CONFIG
→ PERSISTENCE ADAPTER
→ WORKSPACE REPOSITORY
→ MEMBERSHIP REPOSITORY
→ BOT REPOSITORY
→ DI
→ RUNTIME
→ TEST
→ VERIFICATION

Jangan membuat fitur baru.

Jangan commit.

Jangan push.

Berhenti setelah laporan akhir.


```
# 
```

PROMPT: BotSpace — Persistence Adapter Wiring & Runtime Verification

Lanjutkan BotSpace dari checkpoint terakhir.

Repository:
/root/botspace

Branch:
backend-dev-recovery

STATUS TERAKHIR:

- Domain: 107 passed
- API: 113 passed
- pnpm check: 44/44 successful
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- Database migration test: 31 passed, 0 failed
- PostgreSQL 16: PASS
- Migration 0001–0003: PASS
- Migration history: PASS
- Schema tables: 9 present
- Constraints/FKs/indexes/triggers: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- /health: HTTP 200
- /ready: HTTP 200
- Authentication/session route: VERIFIED
- Working tree: CLEAN
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL STATUS TERAKHIR:

AUTH ROUTE VERIFIED — ENVIRONMENT BLOCKER REMAINS

BLOCKER:

- Workspace: BLOCKED — workspace/membership repositories belum di-wire ke persistence adapter
- Bot: BLOCKED — bot repository dan persistence boundary belum di-wire

Runtime application sendiri sudah berhasil start.

TUJUAN TAHAP INI:

Selesaikan hanya persistence adapter wiring untuk:

AUTHENTICATION
→ WORKSPACE
→ MEMBERSHIP
→ BOT
→ REPOSITORY
→ POSTGRESQL
→ RUNTIME VERIFICATION

Jangan membuat sistem persistence baru jika abstraction/repository sudah tersedia.

Jangan mengubah authentication/session architecture yang sudah PASS.

1. AUDIT ARCHITECTURE

Sebelum mengubah kode, audit repository.

Cari:

- persistence adapter
- PostgreSQL adapter
- database client
- repository interfaces
- workspace repository
- membership repository
- bot repository
- dependency injection
- repository factory
- application bootstrap
- runtime composition root
- database configuration
- existing PostgreSQL implementation
- in-memory/mock adapter jika memang tersedia
- tests yang menggunakan repository

Tentukan:

Domain interface
→ implementation
→ dependency injection
→ application bootstrap
→ runtime

Jangan menebak nama file atau abstraction.

2. CARI ROOT CAUSE

Cari secara spesifik kenapa runtime mengatakan:

"workspace/membership repositories belum di-wire ke persistence adapter"

dan:

"bot repository dan persistence boundary belum di-wire"

Tentukan apakah masalahnya:

- repository implementation belum ada
- repository sudah ada tetapi tidak di-export
- repository sudah ada tetapi tidak di-import
- dependency injection belum mendaftarkan repository
- application bootstrap belum membuat adapter
- runtime configuration memilih adapter yang salah
- PostgreSQL client belum diberikan ke repository
- repository factory belum dipanggil
- persistence container belum diteruskan ke service
- environment configuration belum terhubung

Jangan langsung membuat kode baru sebelum root cause ditemukan.

3. GUNAKAN IMPLEMENTASI YANG SUDAH ADA

Jika repository implementation sudah tersedia:

GUNAKAN.

Jika interface sudah tersedia:

GUNAKAN.

Jika PostgreSQL adapter sudah tersedia:

GUNAKAN.

Jangan membuat duplicate:

- database client
- repository interface
- workspace repository
- membership repository
- bot repository
- persistence container
- dependency injection system

Tujuannya hanya memperbaiki wiring.

4. WORKSPACE REPOSITORY

Pastikan runtime dapat membuat workspace repository menggunakan PostgreSQL adapter.

Verifikasi operasi yang memang sudah tersedia:

- create workspace
- get workspace
- list workspace
- update workspace
- delete workspace jika tersedia

Pastikan repository tetap mengikuti authorization layer yang sudah PASS.

Jangan memindahkan authorization ke repository jika architecture saat ini memisahkannya.

5. MEMBERSHIP REPOSITORY

Wire membership repository yang sudah ada.

Verifikasi operasi yang tersedia, misalnya:

- get membership
- list members
- create membership
- update membership
- delete membership

Jangan membuat endpoint baru.

Jangan mengubah permission policy.

Jangan membuat membership system kedua.

6. BOT REPOSITORY

Wire bot repository yang sudah ada.

Verifikasi operasi yang tersedia:

- create bot
- get bot
- list bot
- update bot
- delete bot
- status/enable/disable jika memang tersedia

Pastikan bot tetap terikat dengan workspace.

Jangan mengubah bot lifecycle architecture.

7. DATABASE CONNECTION

Gunakan PostgreSQL configuration yang sudah digunakan repository.

Jangan hardcode:

- password
- DATABASE_URL
- API key
- token
- credential

Pastikan secret tidak muncul dalam:

- log
- error
- test output

Jika DATABASE_URL/environment belum tersedia di runtime, jangan membuat fake database.

Laporkan sebagai environment blocker.

8. MIGRATION

Migration sebelumnya sudah PASS.

Jangan membuat migration baru kecuali root cause benar-benar membutuhkan perubahan schema.

Jangan mengubah:

- production database
- existing migration history
- migration checksum

Jika schema sudah benar, cukup wire repository ke PostgreSQL.

9. DEPENDENCY INJECTION

Audit composition root.

Pastikan dependency chain benar:

PostgreSQL client
→ persistence adapter
→ repository
→ service
→ API/application

Pastikan tidak ada:

- undefined repository
- null repository
- fake repository pada production runtime
- duplicate database client
- circular dependency baru

Jika repository menggunakan dependency injection existing, gunakan mekanisme tersebut.

10. RUNTIME CONFIGURATION

Pastikan production/runtime application menggunakan persistence adapter PostgreSQL.

Jangan mengubah test adapter jika tidak diperlukan.

Bedakan:

TEST ENVIRONMENT

dan:

RUNTIME/PRODUCTION ENVIRONMENT

Jangan membuat production menggunakan mock hanya agar verification PASS.

11. REGRESSION SECURITY

Authentication dan authorization sebelumnya sudah PASS.

Jangan merusaknya.

Pastikan flow tetap:

Authentication
→ current user
→ workspace access
→ membership
→ permission
→ repository
→ database

Persistence adapter tidak boleh bypass:

- authentication
- workspace authorization
- membership
- ownership
- permission

Repository hanya menangani persistence sesuai abstraction existing.

12. TEST

Setelah wiring diperbaiki, jalankan:

- domain tests
- API tests
- authentication/session tests
- workspace tests
- membership tests
- bot tests
- persistence/repository tests jika tersedia
- database migration tests
- typecheck
- format
- import boundary
- build

Jangan skip test.

Jika test gagal:

1. cari root cause
2. perbaiki
3. jalankan test terkait
4. jalankan full verification kembali

13. RUNTIME SMOKE TEST

Jalankan application menggunakan environment runtime yang memang tersedia.

Verifikasi:

/health
→ HTTP 200

/ready
→ HTTP 200

Authentication/session route
→ tetap VERIFIED

Workspace repository
→ dapat di-resolve

Membership repository
→ dapat di-resolve

Bot repository
→ dapat di-resolve

Jika terdapat endpoint runtime yang aman untuk smoke test, gunakan endpoint existing tersebut.

Jangan membuat endpoint baru hanya untuk testing.

14. DATABASE SAFETY

Jangan:

- drop database
- truncate database
- reset database
- menghapus migration
- menghapus production data
- menjalankan destructive migration

Gunakan database yang sudah tersedia.

Jika membutuhkan test database, gunakan mekanisme test repository yang sudah ada.

15. CODE QUALITY

Pastikan:

- tidak ada any baru tanpa alasan
- tidak ada @ts-ignore
- tidak ada duplicate repository
- tidak ada duplicate PostgreSQL client
- tidak ada duplicate DI container
- tidak ada unused import
- tidak ada circular dependency baru
- tidak ada hardcoded secret
- tidak ada temporary debug code

16. README

Tidak perlu membuat README baru.

Update README.md hanya jika wiring persistence membutuhkan dokumentasi yang memang penting.

Dokumentasikan singkat:

- persistence adapter
- PostgreSQL runtime
- repository wiring
- verification command

17. GIT

PENTING:

JANGAN COMMIT.

JANGAN PUSH.

User akan melakukan push/commit manual.

Setelah perubahan:

git status
git diff --stat
git diff

Tampilkan semua file yang berubah.

Working tree boleh DIRTY jika memang ada perubahan implementasi.

Jangan melakukan:

- reset
- force push
- rebase
- merge
- checkout branch lain

18. FINAL REPORT

Tampilkan:

ROOT CAUSE:
- ...

PERSISTENCE:
- PostgreSQL adapter: ...
- Workspace repository: ...
- Membership repository: ...
- Bot repository: ...

WIRING:
- Dependency injection: ...
- Application bootstrap: ...
- Runtime configuration: ...

TESTS:
- Domain: ...
- API: ...
- Auth/Session: ...
- Workspace: ...
- Membership: ...
- Bot: ...
- Persistence: ...
- Database migration: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

RUNTIME:
- /health: ...
- /ready: ...
- Auth route: ...
- Workspace persistence: ...
- Membership persistence: ...
- Bot persistence: ...

GIT:
- Branch: backend-dev-recovery
- Working tree: CLEAN/DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Jika semua repository berhasil di-wire dan runtime verification PASS:

PERSISTENCE VERIFIED — READY FOR MANUAL COMMIT/PUSH

Jika code sudah benar tetapi PostgreSQL/runtime environment tidak tersedia:

PERSISTENCE WIRING COMPLETE — ENVIRONMENT BLOCKER REMAINS

Jika wiring masih gagal:

BLOCKED — PERSISTENCE ADAPTER WIRING INCOMPLETE

Jangan mengklaim PASS jika repository masih unavailable.

FOKUS HANYA:

AUDIT
→ ROOT CAUSE
→ PERSISTENCE WIRING
→ POSTGRESQL
→ WORKSPACE
→ MEMBERSHIP
→ BOT
→ TEST
→ RUNTIME VERIFICATION

Jangan membuat fitur baru.

Jangan commit.

Jangan push.

Berhenti setelah laporan akhir.

```
# BotSpace — Runtime Route Registration & Authentication Wiring Diagnosis
```
PROMPT: BotSpace — Runtime Route Registration & Authentication Wiring Diagnosis

Kita melanjutkan BotSpace dari hasil production verification terakhir.

Repository:
/root/botspace

Branch:
backend-dev-recovery

Kondisi terakhir:

- Domain: 107 passed
- API: 113 passed
- pnpm check: 44/44 successful
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- Database migration test: 31 passed, 0 failed
- PostgreSQL 16: PASS
- Migration 0001 through 0003: PASS
- Migration history: PASS
- Schema tables: 9 present
- Constraints/FKs/indexes/triggers: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- /health: HTTP 200
- /ready: HTTP 200
- Working tree: CLEAN
- Tidak ada source change pada verification terakhir
- Commit baru: TIDAK DIBUAT
- Push: TIDAK DILAKUKAN — USER AKAN PUSH MANUAL

HASIL VERIFICATION TERAKHIR:

Runtime application berhasil start dan melayani operational routes.

Namun ditemukan:

- /health → HTTP 200
- /ready → HTTP 200
- unknown route → HTTP 404
- unsupported method → HTTP 405
- Workspace: BLOCKED oleh unavailable persistence adapter wiring
- Bot: BLOCKED oleh unavailable persistence adapter wiring
- /v1/sessions/current → HTTP 404 karena auth routes belum terdaftar pada runtime configuration

FINAL STATUS:
READY FOR DEPLOYMENT — ENVIRONMENT BLOCKER

PENTING:

JANGAN push.
JANGAN commit.
JANGAN reset.
JANGAN force push.
JANGAN rebase.
JANGAN merge.
JANGAN mengubah remote.
JANGAN mengubah production database.
JANGAN membuat fitur baru.
JANGAN membuat authentication system baru.

TUJUAN TAHAP INI:

Cari ROOT CAUSE kenapa authentication routes yang seharusnya tersedia tidak terdaftar pada runtime application.

Fokus hanya pada:

AUTH ROUTE REGISTRATION
→ ROUTER WIRING
→ APPLICATION BOOTSTRAP
→ MODULE IMPORT
→ ROUTE MOUNTING
→ RUNTIME CONFIGURATION
→ TEST
→ VERIFICATION

1. AUDIT ROUTE REGISTRATION

Cari implementasi authentication/session routes yang sudah ada.

Cari:

- auth routes
- session routes
- login route
- logout route
- current user route
- /v1/sessions
- /v1/auth
- router registration
- route mounting
- app initialization
- server bootstrap
- API application entrypoint

Jangan membuat route baru sebelum memastikan route sebenarnya memang sudah ada tetapi belum ter-register.

2. CARI ROOT CAUSE /v1/sessions/current = 404

Telusuri:

- apakah route `/v1/sessions/current` memang didefinisikan
- file route yang mendefinisikannya
- router yang memuat route tersebut
- apakah router tersebut di-import oleh application
- apakah router tersebut di-mount
- prefix route yang digunakan
- apakah runtime memakai application entrypoint yang benar

Bedakan:

ROUTE TIDAK ADA

dengan:

ROUTE ADA TETAPI TIDAK DI-MOUNT

dengan:

ROUTE ADA TETAPI MODULE TIDAK TER-IMPORT

dengan:

ROUTE ADA TETAPI RUNTIME CONFIGURATION MEMILIH ROUTER YANG SALAH

Jangan menebak.

3. AUDIT APPLICATION BOOTSTRAP

Cari entrypoint resmi application.

Periksa:

- app/server initialization
- router initialization
- route registration
- middleware registration
- auth middleware
- error handler
- environment configuration

Pastikan auth router diregistrasikan pada application yang benar.

Jangan membuat duplicate app instance.

Jangan membuat duplicate router.

Jangan memindahkan architecture hanya untuk membuat test PASS.

4. AUDIT ROUTE PREFIX

Pastikan prefix route konsisten.

Contoh:

/v1/sessions/current

Jika implementasi sebenarnya menggunakan:

/api/v1/sessions/current

atau prefix lain, jangan mengubah route hanya berdasarkan asumsi.

Gunakan route definition dan application mounting aktual sebagai sumber kebenaran.

Jika route memang seharusnya `/v1/sessions/current`, pastikan runtime mendaftarkannya pada path tersebut.

5. AUDIT AUTH ROUTE TEST

Cari test yang sudah memverifikasi:

- login
- logout
- current session
- current user
- invalid session
- authentication

Jika test domain/API sudah PASS tetapi runtime route 404, tentukan apakah test hanya menguji service/router secara isolated dan belum menguji application bootstrap.

Jangan menghapus test existing.

Jika integration test application sudah tersedia, gunakan test tersebut.

6. PERBAIKAN MINIMAL

Jika root cause adalah wiring/registration yang hilang:

perbaiki hanya wiring tersebut.

Contoh perubahan yang mungkin diperlukan:

- import router yang memang sudah ada
- mount router pada application
- memperbaiki route prefix
- memperbaiki bootstrap registration
- memperbaiki module export/import

JANGAN:

- membuat auth service baru
- membuat session system baru
- membuat database schema baru
- mengubah authentication architecture
- mengubah workspace authorization
- mengubah permission policy

7. PERSISTENCE ADAPTER

Untuk blocker:

Workspace: unavailable persistence adapter wiring
Bot: unavailable persistence adapter wiring

Jangan langsung memperbaikinya pada tahap ini kecuali ternyata root cause yang sama dengan application wiring.

Jika persistence adapter membutuhkan PostgreSQL/Docker environment yang belum tersedia, jangan membuat fake adapter.

Jangan mengubah source code hanya untuk menghilangkan status BLOCKED.

Dokumentasikan sebagai environment blocker jika memang external environment yang tidak tersedia.

8. SECURITY

Pastikan perbaikan route registration tidak melewati:

- authentication
- current user resolution
- session validation
- workspace authorization
- membership
- permission

Auth route harus tetap menggunakan abstraction authentication yang sudah ada.

Jangan bypass middleware/security hanya agar endpoint menghasilkan HTTP 200.

9. TESTING

Setelah perubahan minimal jika memang diperlukan, jalankan:

- auth/session tests
- API tests
- typecheck
- format check
- import boundary
- build

Kemudian jalankan runtime verification:

- `/health`
- `/ready`
- auth route yang memang tersedia
- `/v1/sessions/current` jika memang route tersebut adalah route resmi repository

Jangan mengklaim PASS jika endpoint masih 404.

10. GIT

Setelah verification:

git status
git diff --stat
git diff

Jika tidak ada source change:

- Commit: NOT NEEDED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

Jika ada source change yang benar-benar diperlukan untuk memperbaiki route registration:

JANGAN commit.

JANGAN push.

Hanya tampilkan:

- file yang berubah
- root cause
- perubahan yang dilakukan
- hasil test
- hasil build
- status working tree

USER AKAN MENENTUKAN KAPAN COMMIT/PUSH.

11. FINAL REPORT

Tampilkan:

ROOT CAUSE:
- ...

AUTH ROUTE:
- Route definition: ...
- Router: ...
- Application mount: ...
- Runtime result: ...

FIX:
- ...

TESTS:
- Auth: ...
- API: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

RUNTIME:
- /health: ...
- /ready: ...
- auth route: ...

PERSISTENCE:
- Workspace: PASS/BLOCKED
- Bot: PASS/BLOCKED

GIT:
- Working tree: CLEAN/DIRTY
- Commit: NOT PERFORMED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:

Gunakan salah satu:

AUTH ROUTE VERIFIED — ENVIRONMENT BLOCKER REMAINS

atau

AUTH ROUTE FIXED — READY FOR NEXT VERIFICATION

atau

BLOCKED — AUTH ROUTE REGISTRATION ERROR

PENTING:

Fokus hanya diagnosis dan perbaikan minimal authentication route wiring.

Jangan push.
Jangan commit.
Jangan membuat fitur baru.

Berhenti setelah verification selesai dan laporan akhir ditampilkan.


```
# 
```

PROMPT: BotSpace — Manual Deployment & Production Smoke Test

Kita melanjutkan BotSpace dari checkpoint terakhir yang SUDAH BERHASIL.

Repository:
/root/botspace

Branch:
backend-dev-recovery

Kondisi terakhir:

- Domain: 107 passed
- API: 113 passed
- pnpm check: 44/44 successful
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- Database migration test: 31 passed, 0 failed
- PostgreSQL 16: PASS
- Migration 0001 through 0003: PASS
- Migration history: PASS
- Schema tables: 9 present
- Constraints/FKs/indexes/triggers: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- Working tree: CLEAN
- Source code final
- Tidak ada perubahan source code pada verification terakhir

STATUS:
READY FOR DEPLOYMENT — ENVIRONMENT VERIFICATION COMPLETE FOR AVAILABLE RUNTIME

PENTING:

- JANGAN audit source code ulang.
- JANGAN membuat fitur baru.
- JANGAN mengubah architecture.
- JANGAN membuat commit baru jika tidak ada perubahan.
- JANGAN melakukan git push.
- USER AKAN PUSH MANUAL.
- JANGAN force push.
- JANGAN reset.
- JANGAN rebase.
- JANGAN merge ke backend-dev.
- JANGAN mengubah remote Git.
- Jangan mengubah production database secara destructive.
- Jangan mencetak secret, API key, password, token, bot token, atau DATABASE_URL.

TUJUAN TAHAP INI:

Sekarang lanjut dari audit/verifikasi source code menuju:

MANUAL PUSH
→ DEPLOYMENT
→ DATABASE MIGRATION
→ APPLICATION START
→ HEALTH CHECK
→ API SMOKE TEST
→ AUTH SMOKE TEST
→ WORKSPACE SMOKE TEST
→ BOT SMOKE TEST
→ RUNTIME LOG CHECK
→ FINAL PRODUCTION READINESS

1. GIT CHECK ONLY

Periksa:

git status
git branch --show-current
git log --oneline -3

Jangan push.

Jika working tree clean, jangan membuat commit.

2. DEPLOYMENT DISCOVERY

Baca README.md dan package scripts untuk menemukan command deployment resmi repository.

Cari:

- production start command
- Docker configuration
- docker-compose jika tersedia
- migration command
- health endpoint
- readiness endpoint
- environment requirements

Gunakan konfigurasi resmi repository.

Jangan membuat deployment method baru.

3. DATABASE MIGRATION

Jika environment deployment menyediakan PostgreSQL resmi:

jalankan migration resmi repository.

Verifikasi:

- migration berhasil
- migration tidak destructive
- migration idempotent
- schema sesuai migration
- application dapat connect ke database

Jika PostgreSQL/Docker belum tersedia:

JANGAN membuat fake PASS.

Laporkan:

DATABASE ENVIRONMENT NOT AVAILABLE

Lanjutkan hanya verification yang memang dapat dilakukan.

4. APPLICATION START

Jalankan production/runtime start command resmi repository.

Pastikan:

- application berhasil start
- process tetap hidup
- tidak crash
- database connection berhasil
- environment validation berhasil
- tidak ada runtime exception

Jangan mengubah source code hanya untuk melewati environment problem.

5. HEALTH CHECK

Gunakan health endpoint yang memang tersedia.

Verifikasi:

- HTTP status
- response
- application process
- database readiness jika memang termasuk health check

Jika readiness endpoint tersedia, uji juga.

Jangan membuat endpoint baru.

6. AUTHENTICATION SMOKE TEST

Jika environment test memungkinkan:

- unauthenticated protected request → DENY
- valid authenticated request → PASS
- invalid session → DENY
- expired/revoked session → DENY jika dapat diuji

Jangan mencetak credential.

7. WORKSPACE SMOKE TEST

Verifikasi workspace isolation.

User A:
workspace-A

User B:
workspace-B

User A:
workspace-A → PASS
workspace-B → DENY

User B:
workspace-B → PASS
workspace-A → DENY

Pastikan cross-workspace isolation tetap aktif.

8. BOT SMOKE TEST

Jika test fixture atau environment aman tersedia:

- authorized bot GET → PASS
- unauthorized bot GET → DENY
- authorized update → PASS sesuai permission
- cross-workspace update → DENY
- unauthorized delete → DENY
- bot status operation mengikuti permission

Jangan menghapus bot production.

Jangan mengubah credential production.

Gunakan test data jika tersedia.

9. API ERROR SMOKE TEST

Pastikan:

- unauthorized → proper error
- invalid resource → proper error
- invalid request → proper validation error
- tidak ada secret dalam response
- tidak ada production stack trace
- tidak ada credential leakage

10. RUNTIME LOG CHECK

Periksa startup/runtime log.

Pastikan tidak ada:

- password
- API key
- session token
- bot token
- DATABASE_URL
- credential
- secret

Jika ditemukan secret leakage:

STOP.

Laporkan error sebenarnya.

Jangan menghapus atau menyembunyikan log secara sembarangan.

11. PROCESS CHECK

Periksa:

- application process
- listening port
- duplicate application process
- crash loop
- unexpected process yang terkait deployment

Jangan mematikan service lain yang tidak terkait BotSpace.

12. FINAL GIT CHECK

Setelah verification selesai:

git status
git log --oneline -3

Jika source code tetap tidak berubah:

- commit: NOT NEEDED
- push: NOT PERFORMED — USER WILL PUSH MANUALLY

Jika ternyata ada perubahan yang benar-benar diperlukan:

STOP sebelum commit atau push dan laporkan perubahan tersebut.

13. FINAL DECISION

Gunakan hanya salah satu status berikut:

PRODUCTION READY

atau

READY FOR DEPLOYMENT — ENVIRONMENT BLOCKER

atau

BLOCKED — RUNTIME ERROR

atau

BLOCKED — DATABASE ERROR

Jangan menyebut PRODUCTION READY jika application runtime belum berhasil diverifikasi.

14. FINAL REPORT

Tampilkan laporan ringkas:

Deployment:
- Method: ...
- Status: PASS/BLOCKED

Database:
- PostgreSQL: ...
- Migration: ...

Runtime:
- Startup: ...
- Health: ...
- Readiness: ...
- Process: ...

Security:
- Authentication: ...
- Workspace isolation: ...
- Bot authorization: ...
- Secret leakage: ...

Smoke Test:
- API: ...
- Workspace: ...
- Bot: ...

Git:
- Branch: ...
- Working tree: CLEAN/DIRTY
- Commit: NOT NEEDED
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:
...

PENTING:

Jangan mengklaim PASS jika verification sebenarnya gagal.

Jangan membuat perubahan source code untuk memalsukan hasil PASS.

Jangan commit.

Jangan push.

Selesaikan deployment/runtime verification ini lalu berhenti.

```
# 
```
PROMPT: BotSpace — Production Runtime & Deployment Readiness Verification

Kita melanjutkan project BotSpace dari checkpoint terakhir.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

CHECKPOINT TERAKHIR

Source-code/security verification sudah selesai.

Hasil terakhir:
- Domain tests: PASS
- API tests: PASS
- pnpm check: 44/44 PASS
- Typecheck: 11/11 PASS
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Ownership check: PASS
- Documentation links: PASS
- Build: 11/11 successful
- Database migration test: 31 passed, 0 failed
- PostgreSQL 16: PASS
- Migration 0001 through 0003: PASS
- Migration history: PASS
- Schema tables: 9 present
- Constraints/FKs/indexes/triggers: PASS
- Transaction smoke test: PASS
- Migration idempotency: PASS
- Working tree: CLEAN
- Local HEAD dan origin/backend-dev-recovery sudah synchronized

PENTING:
- JANGAN melakukan git push.
- User akan melakukan push secara manual.
- JANGAN mengubah remote.
- JANGAN force push.
- JANGAN reset.
- JANGAN rebase sembarangan.
- JANGAN merge ke backend-dev.
- Jangan membuat commit jika tidak ada source-code change.

TUJUAN

Sekarang lakukan verifikasi akhir terhadap kesiapan runtime/deployment BotSpace.

Fokus:

SOURCE CODE FINAL
→ DATABASE FINAL
→ ENVIRONMENT CHECK
→ RUNTIME STARTUP
→ HEALTH CHECK
→ API SMOKE TEST
→ ERROR HANDLING
→ GRACEFUL SHUTDOWN
→ PRODUCTION READINESS REPORT

1. AUDIT STARTUP

Periksa bagaimana aplikasi BotSpace dijalankan berdasarkan repository aktual.

Cari:

- package scripts
- start command
- production start command
- API entrypoint
- worker entrypoint jika ada
- database initialization
- migration startup behavior
- environment validation
- health endpoint
- readiness endpoint jika tersedia

Jangan membuat entrypoint baru jika sudah tersedia.

2. ENVIRONMENT CHECK

Audit environment variables yang memang dibutuhkan runtime.

Pastikan:

- required environment variable terdeteksi
- missing environment variable menghasilkan error yang jelas
- secret tidak dicetak ke terminal
- .env tidak dimodifikasi
- production secret tidak dibuat
- API key/token/password tidak ditampilkan dalam report

Jangan meminta atau mencetak nilai secret.

Jika environment deployment belum tersedia, catat sebagai ENVIRONMENT BLOCKER dan jangan memalsukan hasil.

3. DATABASE RUNTIME

Gunakan migration yang sudah terbukti PASS.

Verifikasi runtime database connection menggunakan environment yang memang tersedia.

Periksa:

- PostgreSQL connection
- schema tersedia
- migration state
- basic query
- transaction
- connection failure behavior

Jangan menghapus data.

Jangan melakukan destructive migration.

Jangan mengubah production database.

4. APPLICATION STARTUP

Jalankan production/runtime startup command yang memang digunakan repository.

Pastikan:

- process dapat start
- tidak ada TypeScript/runtime error
- database connection berhasil
- dependency resolution berhasil
- environment validation berhasil
- application tidak langsung crash

Jika startup gagal:

1. ambil root cause
2. perbaiki hanya jika source-code issue nyata
3. ulangi startup verification

Jangan mengubah source code hanya untuk menyembunyikan environment problem.

5. HEALTH CHECK

Cari health endpoint yang memang tersedia.

Jika tersedia, lakukan request terhadap endpoint tersebut.

Verifikasi:

- HTTP status benar
- response valid
- tidak membocorkan secret
- database status sesuai architecture
- process tetap berjalan

Jika readiness endpoint tersedia, verifikasi juga.

Jangan membuat endpoint baru hanya untuk task ini.

6. API SMOKE TEST

Gunakan endpoint API yang sudah tersedia.

Lakukan smoke test minimal untuk:

- authentication/current user jika tersedia
- workspace access
- bot/resource access
- protected endpoint
- unauthorized request
- not-found behavior
- validation error

Gunakan data test yang aman.

Jangan menggunakan production credential.

Jangan menghapus atau mengubah data production.

7. SECURITY RUNTIME REGRESSION

Pastikan runtime tidak melewati security boundary yang sebelumnya sudah diperbaiki.

Verifikasi:

- unauthenticated protected request → DENY
- authenticated valid request → PASS
- cross-workspace request → DENY
- invalid resource → proper error
- secret tidak muncul pada response
- secret tidak muncul pada logs

Jangan membuat authorization system baru.

8. ERROR HANDLING

Uji failure scenario yang aman:

- database unavailable jika dapat disimulasikan tanpa merusak environment
- invalid authentication
- invalid resource ID
- malformed request
- unauthorized access

Pastikan error:

- tidak membocorkan secret
- tidak membocorkan stack trace production
- tidak membocorkan credential
- mengikuti error convention repository

Jangan mengubah error system jika tidak diperlukan.

9. GRACEFUL SHUTDOWN

Jika runtime/service mendukung graceful shutdown, verifikasi:

- SIGTERM/SIGINT handling
- database connection close
- HTTP server shutdown
- worker shutdown jika tersedia
- process tidak meninggalkan resource terbuka

Jangan membuat shutdown framework baru.

10. RUNTIME RESOURCE CHECK

Periksa secara singkat:

- memory usage
- process count
- open port yang memang digunakan
- duplicate process
- unexpected background process
- startup crash loop

Jangan mematikan service lain yang tidak terkait BotSpace.

11. PRODUCTION CONFIGURATION

Audit konfigurasi runtime tanpa mengubah infrastructure.

Periksa:

- production NODE_ENV/runtime mode jika memang digunakan
- logging level
- port
- host binding
- database URL presence
- secret configuration presence
- CORS configuration jika tersedia
- API base configuration

Jangan mengubah VPS, DNS, Cloudflare, firewall, atau reverse proxy pada task ini.

12. TEST REGRESSION

Setelah runtime verification, jalankan kembali verification resmi repository jika source code berubah.

Minimal:

- domain tests
- API tests
- typecheck
- format
- import boundary
- build

Jangan skip test.

Jika tidak ada source-code change, tetap laporkan hasil verification terakhir dan hasil runtime test secara terpisah.

13. SOURCE-CODE CHANGE POLICY

Jika semua source code sudah benar dan masalah hanya karena:

- Docker tidak tersedia
- environment deployment belum tersedia
- credential belum tersedia
- external service belum tersedia

JANGAN membuat workaround palsu.

Catat sebagai environment blocker.

Jangan mengubah source code hanya agar status terlihat PASS.

14. GIT

JANGAN PUSH.

Sebelum selesai jalankan:

git status
git diff --stat
git log --oneline -3

Jika tidak ada source-code change:

- jangan membuat commit
- jangan membuat empty commit
- jangan force push

Jika ternyata ada source-code fix yang benar-benar diperlukan:

- buat SATU commit saja
- jangan push
- tampilkan hash commit
- user akan melakukan push manual

15. FINAL DECISION

Tentukan salah satu status berikut berdasarkan bukti nyata:

FULLY VERIFIED — READY FOR PRODUCTION

atau

READY FOR DEPLOYMENT — ENVIRONMENT VERIFICATION PENDING

atau

BLOCKED — SOURCE CODE ISSUE

atau

BLOCKED — ENVIRONMENT ISSUE

Jangan menyebut FULLY VERIFIED jika runtime production belum benar-benar dapat diverifikasi.

16. FINAL REPORT

Tampilkan laporan:

Runtime:
- Startup: PASS/FAIL/BLOCKED
- Database connection: PASS/FAIL/BLOCKED
- Health check: PASS/FAIL/BLOCKED
- API smoke test: PASS/FAIL/BLOCKED
- Security runtime: PASS/FAIL/BLOCKED
- Graceful shutdown: PASS/FAIL/BLOCKED

Database:
- PostgreSQL: ...
- Migration: ...
- Schema: ...
- Transaction: ...

Tests:
- Domain: ...
- API: ...
- Typecheck: ...
- Format: ...
- Import boundary: ...
- Build: ...

Git:
- Branch: backend-dev-recovery
- Working tree: clean/dirty
- Commit: created/not created
- Push: NOT PERFORMED — USER WILL PUSH MANUALLY

FINAL DECISION:
...

Jika ada blocker, tampilkan root cause sebenarnya.

Jangan mengklaim production ready tanpa bukti.

Selesaikan verification ini dan berhenti.


```
# 
```
PROMPT: BotSpace — Bot Lifecycle & Resource Integrity Hardening

Kita melanjutkan project BotSpace dari checkpoint security terakhir yang SUDAH BERHASIL.

Repository: /root/botspace
Branch: backend-dev-recovery
Remote: https://github.com/zenolamee/botspace.git

Checkpoint terakhir:
d24aeed5d2151484449d94c72609e6f26b332d9c — docs: finalize production verification guidance

Verification checkpoint terakhir:

* Format check: PASS
* Import boundary check: PASS
* Build: 11 tasks successful
* Working tree: clean
* Commit lokal aman
* Push dapat gagal hanya jika credential GitHub bermasalah

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

* create bot
* get bot
* list bot
* update bot
* delete bot
* enable bot
* disable bot
* bot status
* bot configuration
* bot credentials
* bot settings
* bot commands
* bot flows
* bot integrations
* bot webhook
* resource lain yang memiliki botId

Gunakan struktur repository aktual sebagai sumber kebenaran.

Jangan membuat endpoint baru hanya untuk task ini.

2. BOT STATE

Identifikasi state bot yang benar-benar digunakan repository.

Contoh jika memang tersedia:

* active
* inactive
* disabled
* pending
* stopped
* deleted

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

* memiliki workspace yang valid
* dibuat oleh authenticated user
* user memiliki akses ke workspace
* owner/membership relation benar
* tidak dapat dibuat menggunakan workspaceId milik workspace lain
* tidak menerima ownerId palsu dari client
* tidak menerima accountId palsu dari client

Server harus menentukan ownership berdasarkan authentication context dan workspace authorization.

6. BOT UPDATE INTEGRITY

Audit seluruh field update.

Pisahkan:

CLIENT-CONTROLLED FIELD
dan
SERVER-CONTROLLED FIELD

Periksa khusus:

* id
* workspaceId
* ownerId
* accountId
* createdBy
* createdAt
* updatedAt
* status
* role
* permissions
* credential identifiers

Jangan mengizinkan update biasa mengubah ownership atau workspace assignment jika architecture tidak mendukungnya.

Gunakan explicit field mapping jika diperlukan.

7. DELETE INTEGRITY

Audit delete bot.

Pastikan:

* authorization dilakukan sebelum delete
* user tidak dapat delete bot workspace lain
* member tanpa permission delete ditolak
* bot yang tidak ada ditangani dengan error convention
* child resource tidak menjadi orphan secara tidak sengaja

Jika project menggunakan soft delete, pertahankan behavior tersebut.

Jika project menggunakan hard delete, audit dependency terlebih dahulu.

Jangan mengubah soft delete menjadi hard delete atau sebaliknya tanpa alasan.

8. CHILD RESOURCE INTEGRITY

Audit resource yang bergantung pada bot.

Contoh jika tersedia:

* commands
* flows
* settings
* integrations
* webhooks
* logs
* credentials
* analytics
* configuration

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

* workspaceId berbeda dari bot.workspaceId
* ownerId berbeda dari creator yang seharusnya
* accountId berbeda dari workspace account
* botId yang tidak valid
* parent resource yang sudah tidak ada

Jangan memperbaiki data production secara otomatis.

Fokus pada enforcement dan test.

10. DATABASE CONSTRAINT / REPOSITORY

Audit repository method yang membuat atau mengubah bot.

Periksa:

* create
* update
* delete
* status update
* child resource creation

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

* duplicate bot identifier
* duplicate Telegram bot token
* duplicate external identifier
* duplicate workspace resource

Hanya enforce rule yang memang sudah tersirat dalam architecture.

Jangan menciptakan business rule baru tanpa bukti.

13. CREDENTIAL INTEGRITY

Audit bot credential handling.

Pastikan:

* credential tidak digunakan untuk menentukan ownership
* credential tidak mengubah workspace
* credential tidak muncul dalam list response
* credential tidak masuk log
* credential tidak masuk error
* credential tidak dapat diganti oleh user tanpa permission
* credential update tetap berada pada bot/workspace yang benar

Jangan menampilkan secret dalam test output.

14. API INPUT VALIDATION

Audit input pada seluruh lifecycle endpoint.

Validasi:

* botId
* workspaceId
* status
* configuration
* settings
* commandId
* flowId
* integrationId
* webhookId

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

* authenticated + valid workspace = PASS
* unauthenticated = DENY
* wrong workspace = DENY
* spoofed ownerId = DENY
* spoofed accountId = DENY

Read:

* own bot = PASS
* other workspace bot = DENY

Update:

* authorized update = PASS
* unauthorized update = DENY
* workspaceId spoof = DENY
* ownerId spoof = DENY
* permission spoof = DENY

Delete:

* authorized delete = PASS
* unauthorized delete = DENY
* cross-workspace delete = DENY

Status:

* authorized enable = PASS
* unauthorized enable = DENY
* cross-workspace enable = DENY
* authorized disable = PASS
* unauthorized disable = DENY
* cross-workspace disable = DENY

Child resources:

* authorized child access = PASS
* cross-workspace child access = DENY
* invalid parent relation = DENY

Credential:

* secret tidak muncul pada response yang tidak seharusnya
* secret tidak muncul pada error
* secret tidak muncul pada log/test output

17. REGRESSION

Pastikan seluruh security checkpoint sebelumnya tetap PASS:

* authentication
* session
* current user
* workspace authorization
* membership
* ownership
* permission policy
* bot resource authorization

Jangan melemahkan test lama.

18. TYPESCRIPT QUALITY

Pastikan:

* tidak menambahkan any tanpa alasan
* tidak menambahkan @ts-ignore
* tidak ada unused import
* tidak ada dead code
* tidak ada duplicate authorization
* tidak ada duplicate validation
* tidak ada duplicate bot lifecycle logic
* tidak ada circular dependency baru
* tidak ada hardcoded secret

Ikuti architecture repository.

19. README

Jika diperlukan, update README.md yang sudah ada.

Jangan membuat README baru.

Dokumentasikan secara singkat:

* bot lifecycle
* bot status
* authorization
* resource integrity
* test command

20. VERIFICATION

Setelah implementasi jalankan verification resmi repository.

Minimal:

* domain tests
* API tests
* authentication/session tests
* workspace authorization tests
* membership tests
* bot/resource tests
* typecheck
* format check
* import boundary check
* lint jika tersedia
* build

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

* .env
* API key
* token
* credential
* log
* temporary file
* build artifact

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

* force push
* ubah remote
* merge ke backend-dev
* reset checkpoint
* rebase sembarangan

Jika push gagal karena credential GitHub:

JANGAN mengubah source code lagi.

Pertahankan commit lokal dan laporkan error sebenarnya.

24. HASIL AKHIR

Tampilkan laporan:

Implementation:

* ...

Bot Lifecycle:

* ...

Resource Integrity:

* ...

Security:

* ...

Tests:

* Domain: ...
* API: ...
* Auth/Session: ...
* Workspace: ...
* Membership: ...
* Bot/Resource: ...
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



```
# Prompt berikutnya — Database Migration Environment
```

PROMPT: BotSpace — Enable Official PostgreSQL Migration Environment

Kita melanjutkan BotSpace dari kondisi terakhir.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Kondisi saat ini:
- Source code FINAL
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- Working tree: CLEAN
- HEAD sama dengan origin/backend-dev-recovery
- Push: NOT NEEDED

BLOCKER SAAT INI:
Database migration belum dapat diverifikasi karena environment PostgreSQL/Docker belum tersedia.

JANGAN melakukan audit source code ulang.
JANGAN membuat fitur baru.
JANGAN refactor source code.
JANGAN membuat migration baru kecuali repository memang secara eksplisit membutuhkan migration baru.
JANGAN mengubah source code hanya untuk melewati migration.

TUJUAN:
Siapkan environment PostgreSQL/Docker yang diperlukan oleh WORKFLOW MIGRATION RESMI repository, kemudian jalankan migration dan verifikasi database.

1. AUDIT ENVIRONMENT SAJA

Periksa:

- docker --version
- docker compose version
- psql --version
- systemctl status docker
- PostgreSQL service jika tersedia
- file docker-compose / compose repository
- package.json scripts
- migration configuration
- migration directory
- README.md bagian database/migration

Gunakan konfigurasi repository sebagai sumber kebenaran.

Jangan menebak nama database, port, user, password, atau command migration jika sudah tersedia di repository.

2. JIKA DOCKER BELUM TERINSTALL

Jika repository memang menggunakan Docker untuk migration dan Docker belum tersedia:

- install Docker dengan metode resmi yang sesuai dengan OS VPS
- jangan mengubah source code repository
- jangan menghapus package
- jangan mengubah aplikasi production yang sedang berjalan
- setelah instalasi, verifikasi:

docker --version
docker compose version

Jika Docker sudah tersedia, jangan install ulang.

3. CEK KONFLIK PORT

Sebelum menjalankan PostgreSQL:

- cek port PostgreSQL yang digunakan repository
- cek apakah port tersebut sudah digunakan
- jangan menghentikan service production secara sembarangan
- jika repository memiliki compose configuration resmi, ikuti configuration tersebut

Jangan mengubah port aplikasi BotSpace tanpa kebutuhan.

4. JALANKAN DATABASE ENVIRONMENT RESMI

Jika repository memiliki:

docker-compose.yml
docker-compose.yaml
compose.yml
compose.yaml

gunakan konfigurasi tersebut.

Jalankan hanya service yang diperlukan untuk migration jika workflow repository memungkinkan.

Pastikan PostgreSQL benar-benar healthy dan dapat menerima koneksi.

5. DATABASE CONNECTION

Gunakan DATABASE_URL/environment yang memang ditentukan repository.

Jangan menampilkan:

- password
- token
- secret
- credential

dalam output final.

Verifikasi koneksi PostgreSQL secara aman.

6. JALANKAN MIGRATION RESMI

Temukan command migration resmi dari repository.

Jalankan migration tersebut.

JANGAN:

- db reset
- drop database
- delete data
- membuat schema manual
- melewati migration
- menandai migration sukses secara palsu

Migration harus benar-benar dijalankan terhadap PostgreSQL.

7. VERIFIKASI MIGRATION

Setelah migration:

- cek migration status
- pastikan seluruh migration repository yang diperlukan sudah applied
- pastikan schema tersedia
- pastikan tidak ada migration failure
- pastikan database connection PASS

Jika migration gagal:

- cari root cause
- jangan mengubah source code kecuali memang migration code repository yang bermasalah
- laporkan error sebenarnya

8. DATABASE SMOKE TEST

Jika migration PASS, jalankan test database yang memang tersedia di repository.

Verifikasi:

- PostgreSQL connection PASS
- schema access PASS
- repository query PASS
- transaction/database operation PASS jika tersedia

Jangan membuat data production sembarangan.

9. APPLICATION VERIFICATION

Setelah database PASS:

jalankan verification aplikasi menggunakan command resmi repository.

Pastikan:

- application start PASS
- database connection PASS
- health check PASS
- readiness PASS jika tersedia

10. REGRESSION

Karena source code sebelumnya sudah PASS, jalankan kembali verification final untuk memastikan database tidak menyebabkan regression.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace tests
- membership tests
- bot/resource tests
- typecheck
- format
- import boundary
- build

Jangan skip test.

Jangan menghapus test.

11. GIT

Database environment tidak boleh menghasilkan perubahan source code yang tidak diperlukan.

Jalankan:

git status
git log --oneline -3

Pastikan:

Working tree: CLEAN

Jika tidak ada perubahan source code:

Commit: NOT NEEDED
Push: NOT NEEDED

Jangan membuat commit kosong.

12. FINAL DECISION

Jika:

- PostgreSQL PASS
- Migration PASS
- Database connection PASS
- Database smoke test PASS
- Application start PASS
- Health check PASS
- Regression PASS
- Build PASS
- Working tree CLEAN

tampilkan:

FINAL STATUS:
FULLY VERIFIED — READY FOR PRODUCTION

Jika PostgreSQL/Docker tetap tidak dapat disediakan:

FINAL STATUS:
READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING

Jika ada error:

FINAL STATUS:
BLOCKED — DATABASE VERIFICATION FAILED

Jangan pernah menyatakan FULLY VERIFIED jika migration belum benar-benar dijalankan.

13. FINAL REPORT

Tampilkan ringkas:

DATABASE ENVIRONMENT:
- Docker: PASS/NOT AVAILABLE
- PostgreSQL: PASS/NOT AVAILABLE
- Connection: PASS/FAILED

MIGRATION:
- Migration command: ...
- Migration status: PASS/FAILED/BLOCKED

RUNTIME:
- Application: PASS/FAILED
- Health: PASS/FAILED
- Readiness: PASS/FAILED jika tersedia

REGRESSION:
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

GIT:
- Branch: ...
- Working tree: CLEAN/DIRTY
- Commit: NOT NEEDED jika tidak ada source change
- Push: NOT NEEDED jika tidak ada source change

FINAL STATUS:
...

Jika Docker/PostgreSQL belum tersedia dan instalasi tidak dapat dilakukan pada environment ini, berhenti dan tampilkan blocker sebenarnya.

Jangan kembali melakukan audit source code.
Selesaikan hanya database environment → migration → verification.

```
# Prompt Final — PostgreSQL Migration & Final Production Verification
```
PROMPT: BotSpace — FINAL PostgreSQL Migration & Production Verification

Kita melanjutkan BotSpace dari kondisi FINAL.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Kondisi TERAKHIR:
- Source code FINAL
- Runtime health VERIFIED tanpa database
- Typecheck: 11/11 successful
- Format: PASS
- Import boundary: PASS
- Secrets scan: PASS
- Build: 11/11 successful
- Working tree: CLEAN
- HEAD sama dengan origin/backend-dev-recovery
- Push: NOT NEEDED
- Tidak ada perubahan source code yang diperlukan

STATUS YANG MASIH TERTUNDA:
DATABASE MIGRATION

Penyebab sebelumnya:
- PostgreSQL dan/atau Docker environment resmi untuk migration belum tersedia
- Migration belum boleh diklaim PASS tanpa benar-benar dijalankan

TUJUAN:
Selesaikan hanya database migration dan final runtime verification.

JANGAN:
- audit source code ulang
- membuat fitur baru
- refactor
- mengubah authorization
- mengubah authentication
- mengubah bot lifecycle
- membuat migration palsu
- membuat database schema manual yang berbeda dari migration repository
- reset database
- drop database
- menghapus data
- force push
- reset git
- rebase
- merge
- membuat commit kosong

1. IDENTIFIKASI DATABASE

Baca repository aktual untuk menentukan:

- database engine
- migration tool
- migration directory
- migration command resmi
- DATABASE_URL yang dibutuhkan
- PostgreSQL version jika ditentukan repository
- apakah Docker memang merupakan bagian official migration workflow

Gunakan package.json, README.md, konfigurasi database, migration files, dan scripts repository sebagai sumber kebenaran.

Jangan menebak command migration.

2. CEK ENVIRONMENT

Periksa tanpa menampilkan secret:

- docker
- docker compose
- psql
- PostgreSQL service
- DATABASE_URL tersedia/tidak
- koneksi database
- migration tool

Jika Docker tersedia:
gunakan workflow migration resmi repository.

Jika PostgreSQL tersedia tanpa Docker:
gunakan workflow resmi repository yang memang mendukung koneksi PostgreSQL langsung.

Jika PostgreSQL DAN Docker sama-sama tidak tersedia:
JANGAN membuat workaround palsu.

Laporkan:

DATABASE MIGRATION:
BLOCKED

Reason:
official PostgreSQL/migration environment unavailable.

3. JIKA DATABASE TERSEDIA

Jalankan migration resmi repository.

Migration harus:

- menggunakan migration files repository
- non-destructive
- tidak melakukan reset
- tidak drop database
- tidak menghapus production data
- tidak membuat schema manual yang tidak tercatat

4. VERIFIKASI MIGRATION

Setelah migration selesai:

verifikasi migration status.

Pastikan:

- seluruh migration yang diperlukan sudah applied
- migration history konsisten
- database schema tersedia
- koneksi PostgreSQL berhasil

Jangan mencetak DATABASE_URL, password, token, atau credential.

5. DATABASE SMOKE TEST

Jika migration PASS:

jalankan smoke test database menggunakan command/test yang memang tersedia di repository.

Verifikasi minimal:

- database connection PASS
- schema access PASS
- repository query PASS
- transaction/database operation PASS jika tersedia

Jangan membuat data production secara sembarangan.

6. APPLICATION RUNTIME

Jika database sudah PASS:

jalankan application menggunakan command resmi repository.

Verifikasi:

- application start PASS
- database connection PASS
- health endpoint PASS
- readiness endpoint PASS jika tersedia

Gunakan environment yang benar.

Jangan mengubah source code hanya agar aplikasi bisa start.

7. FINAL REGRESSION

Karena source code sebelumnya sudah verified, jalankan verification final untuk memastikan migration tidak menyebabkan regression.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization
- membership/ownership
- bot/resource authorization
- typecheck
- format
- import boundary
- build

Gunakan command resmi repository.

Jangan skip test.

Jangan menghapus test.

8. GIT FINAL CHECK

Migration/environment operation tidak boleh menghasilkan perubahan source code yang tidak diperlukan.

Jalankan:

git status
git log --oneline -3

Pastikan:

WORKING TREE:
CLEAN

Jika tidak ada source-code change:

PUSH:
NOT NEEDED

Jangan membuat commit kosong.

9. FINAL DECISION

Jika semua berikut PASS:

SOURCE CODE = PASS
DATABASE MIGRATION = PASS
DATABASE CONNECTION = PASS
APPLICATION START = PASS
HEALTH CHECK = PASS
REGRESSION = PASS
BUILD = PASS
WORKING TREE = CLEAN

maka tampilkan:

FINAL STATUS:
FULLY VERIFIED — READY FOR PRODUCTION

Jika database migration tetap tidak dapat dijalankan karena environment:

FINAL STATUS:
READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING

Jika runtime/database gagal:

FINAL STATUS:
BLOCKED — DATABASE/RUNTIME VERIFICATION FAILED

Jangan pernah menyatakan FULLY VERIFIED jika database migration belum benar-benar dijalankan.

10. FINAL REPORT

Tampilkan ringkas:

DATABASE:
- Engine: ...
- Migration: PASS/BLOCKED
- Migration status: ...
- Database connection: PASS/BLOCKED

RUNTIME:
- Application start: PASS/BLOCKED
- Health check: PASS/BLOCKED
- Readiness: PASS/BLOCKED jika tersedia

REGRESSION:
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

GIT:
- Branch: ...
- HEAD: ...
- Working tree: CLEAN/DIRTY
- Push: NOT NEEDED

FINAL STATUS:
...

PENTING:
Jika PostgreSQL/Docker environment belum tersedia, berhenti setelah melaporkan BLOCKED.
Jangan kembali melakukan audit source code.

Target akhir:

SOURCE CODE FINAL
→ POSTGRESQL READY
→ MIGRATION PASS
→ DATABASE VERIFIED
→ RUNTIME VERIFIED
→ FULLY VERIFIED
→ READY FOR PRODUCTION

Selesaikan sampai final status lalu berhenti.


```
# Prompt Final — Database Migration & Runtime Verification
```

PROMPT: BotSpace — FINAL Database Migration & Runtime Verification

Kita melanjutkan BotSpace dari kondisi FINAL.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Kondisi terakhir:
- Source code FINAL
- Production readiness: READY
- Working tree: CLEAN
- HEAD sama dengan origin/backend-dev-recovery
- Build 11/11 SUCCESSFUL
- Domain/API/security verification sudah PASS
- Tidak ada coding/refactor baru yang diperlukan

SATU-SATUNYA STATUS YANG TERTUNDA:
DATABASE MIGRATION

Sebelumnya migration BLOCKED karena environment tidak memiliki Docker.

JANGAN melakukan audit source code lagi.
JANGAN membuat fitur baru.
JANGAN melakukan refactor.
JANGAN membuat commit kosong.
JANGAN reset.
JANGAN force push.
JANGAN rebase.
JANGAN merge.
JANGAN mengubah source code hanya untuk membuat verification terlihat PASS.

TUJUAN FINAL:

DATABASE ENVIRONMENT
→ DATABASE MIGRATION
→ DATABASE VERIFICATION
→ APPLICATION START
→ HEALTH CHECK
→ FINAL REGRESSION
→ GIT FINAL STATUS

1. IDENTIFIKASI DATABASE

Baca repository aktual dan tentukan:

- database engine yang digunakan
- migration tool yang digunakan
- migration command resmi
- database environment variable yang dibutuhkan
- apakah project membutuhkan PostgreSQL
- apakah Docker hanya digunakan untuk test/migration atau merupakan dependency runtime

Gunakan package.json, README.md, konfigurasi migration, dan source repository sebagai sumber kebenaran.

Jangan menebak command.

2. CEK ENVIRONMENT

Periksa:

- node
- pnpm
- database client
- psql jika PostgreSQL digunakan
- docker
- docker compose jika digunakan
- DATABASE_URL
- environment variable database lainnya

JANGAN mencetak credential atau password.

Jika Docker tersedia sekarang:
→ gunakan workflow migration resmi repository.

Jika Docker tetap tidak tersedia:
→ jangan menginstal Docker otomatis.
→ jangan mengubah VPS.
→ jangan membuat workaround palsu.
→ tentukan apakah migration dapat dijalankan menggunakan database service yang tersedia.

3. DATABASE MIGRATION

Jika database target tersedia dan aman:

jalankan migration resmi repository.

Jangan:

- db reset
- drop database
- drop schema
- delete production data
- destructive migration
- seed production dengan data dummy

Migration harus non-destructive dan mengikuti migration history repository.

Jika migration membutuhkan Docker dan Docker benar-benar tidak tersedia:

JANGAN memalsukan PASS.

Laporkan:

DATABASE MIGRATION:
BLOCKED

Reason:
Docker/database environment unavailable.

4. VERIFY MIGRATION

Jika migration berhasil:

verifikasi migration status.

Pastikan:

- migration tercatat
- schema tersedia
- tabel utama tersedia
- database connection berhasil

Jangan menampilkan credential.

5. APPLICATION START

Cari command resmi untuk menjalankan aplikasi.

Gunakan package script repository.

Jalankan application menggunakan environment yang benar.

Jangan mengubah source code hanya untuk membuat application start.

Jika environment variable wajib belum tersedia:

- identifikasi variable yang hilang
- jangan membuat secret palsu
- jangan mencetak secret
- jangan menebak API key

6. HEALTH CHECK

Jika aplikasi berhasil start:

gunakan health endpoint resmi repository.

Verifikasi:

- process hidup
- API merespons
- database connection berhasil
- health endpoint PASS

Jika ada endpoint readiness:

uji readiness juga.

Jangan melakukan destructive API request.

7. RUNTIME SMOKE TEST

Lakukan smoke test minimum terhadap flow yang sudah tersedia.

Pastikan:

- API dapat menerima request
- authentication boundary aktif
- workspace authorization aktif
- bot/resource authorization aktif
- database query dapat berjalan

Jangan membuat data production sembarangan.

Jika smoke test membutuhkan data:

gunakan mekanisme test/development yang memang disediakan repository.

8. FINAL REGRESSION

Jalankan verification final yang tersedia.

Minimal:

- domain tests
- API tests
- authentication/session tests
- workspace authorization
- membership/permission
- bot/resource authorization
- typecheck
- format
- import boundary
- build

Semua harus PASS jika ingin status FULLY VERIFIED.

Jangan skip test.

Jangan menghapus test.

9. GIT FINAL CHECK

Jalankan:

git status
git log --oneline -3

Migration/environment operation tidak boleh membuat perubahan source code yang tidak diperlukan.

Pastikan:

WORKING TREE = CLEAN

Jika migration menghasilkan file generated yang memang harus masuk repository, periksa terlebih dahulu apakah repository memang mengharuskannya.

Jangan membuat commit kosong.

Jangan push jika tidak ada perubahan.

10. FINAL DECISION

Jika:

SOURCE CODE PASS
+ DATABASE MIGRATION PASS
+ DATABASE CONNECTION PASS
+ APPLICATION START PASS
+ HEALTH CHECK PASS
+ REGRESSION PASS
+ BUILD PASS
+ WORKING TREE CLEAN

maka:

FINAL STATUS:
READY FOR PRODUCTION

Jika source code sudah final tetapi database migration masih tidak dapat dijalankan:

FINAL STATUS:
READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING

Jika runtime gagal:

FINAL STATUS:
BLOCKED — RUNTIME VERIFICATION FAILED

Jangan mengklaim FULLY VERIFIED jika migration/runtime belum benar-benar diuji.

11. FINAL REPORT

Tampilkan hanya laporan akhir yang ringkas:

SOURCE CODE:
PASS

DATABASE:
- Engine: ...
- Migration: PASS/BLOCKED
- Migration reason: ...

RUNTIME:
- Application start: PASS/BLOCKED
- Database connection: PASS/BLOCKED
- Health check: PASS/BLOCKED

TESTS:
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

GIT:
- Branch: ...
- HEAD: ...
- Working tree: CLEAN/DIRTY
- Push: NOT NEEDED / SUCCESS / FAILED

FINAL STATUS:
...

PENTING:

Setelah final status ditentukan, BERHENTI.

Tidak ada audit berikutnya.
Tidak ada fitur baru.
Tidak ada refactor tambahan.

Target akhir adalah:

SOURCE CODE FINAL
→ DATABASE VERIFIED
→ RUNTIME VERIFIED
→ PRODUCTION READY

```
# Prompt: BotSpace — Final Production Deployment & Database Migration
```

PROMPT: BotSpace — Final Production Deployment & Database Migration

Kita melanjutkan project BotSpace dari checkpoint terakhir.

Repository:
 /root/botspace

Branch:
 backend-dev-recovery

Remote:
 https://github.com/zenolamee/botspace.git

STATUS TERAKHIR:

Source code:
- FINAL
- Production readiness: READY
- Working tree: CLEAN
- Git checkpoint sudah aman
- Security verification sudah PASS
- Domain tests PASS
- API tests PASS
- Typecheck PASS
- Format PASS
- Import boundary PASS
- Build 11/11 PASS

Satu-satunya blocker yang tersisa:

DATABASE MIGRATION:
BLOCKED — Docker tidak tersedia pada environment saat verification.

PENTING:

JANGAN melakukan audit source code lagi.
JANGAN mengulang security hardening yang sudah selesai.
JANGAN membuat fitur baru.
JANGAN reset.
JANGAN force push.
JANGAN rebase sembarangan.
JANGAN merge ke backend-dev.
JANGAN menghapus checkpoint yang sudah ada.

TUJUAN FINAL

Selesaikan BotSpace sampai benar-benar siap dijalankan di environment deployment.

Alur:

CHECK ENVIRONMENT
→ DATABASE MIGRATION
→ DATABASE VERIFICATION
→ APPLICATION START
→ RUNTIME HEALTH CHECK
→ FINAL TEST
→ GIT STATUS
→ FINAL REPORT

1. CEK ENVIRONMENT

Periksa environment aktual:

- Node.js version
- pnpm version
- database yang digunakan project
- DATABASE_URL / environment variable yang relevan
- migration command resmi repository
- package scripts
- apakah Docker tersedia
- apakah database service tersedia

JANGAN mengubah source code hanya karena Docker tidak tersedia.

Gunakan package.json dan README sebagai sumber kebenaran untuk command migration.

2. DATABASE MIGRATION

Cari migration system yang benar-benar digunakan project.

Jangan membuat migration baru jika tidak diperlukan.

Jika Docker tersedia:

- jalankan migration menggunakan workflow resmi repository
- jangan menghapus database
- jangan reset database production
- jangan menggunakan destructive migration
- jangan menjalankan db reset kecuali repository secara eksplisit membutuhkan database disposable untuk test

Jika Docker TIDAK tersedia:

- jangan menginstal Docker secara otomatis
- jangan mengubah konfigurasi VPS
- jangan mengubah system service
- jangan mengubah production environment
- jangan membuat workaround palsu

Sebaliknya:

- tentukan command migration yang sebenarnya
- tentukan dependency environment yang hilang
- verifikasi apakah migration dapat dijalankan tanpa Docker menggunakan database yang memang tersedia
- jika benar-benar tidak dapat dijalankan, laporkan blocker secara eksplisit

3. DATABASE SAFETY

Sebelum migration:

- pastikan target database diketahui
- jangan menyentuh production database tanpa konfigurasi yang memang disediakan
- jangan menghapus data
- jangan drop schema
- jangan reset database
- jangan melakukan destructive operation

Migration harus aman dan reproducible.

4. SETELAH MIGRATION BERHASIL

Verifikasi:

- migration status
- database schema tersedia
- tabel/struktur penting tersedia
- application database connection berhasil

Gunakan command resmi repository jika tersedia.

Jangan membuat script database baru hanya untuk verification.

5. START APPLICATION

Cari command resmi untuk menjalankan BotSpace.

Gunakan package scripts yang sudah ada.

Jangan mengubah source code hanya agar aplikasi bisa start.

Jika environment variable wajib belum tersedia:

- identifikasi variable yang hilang
- jangan mencetak secret ke terminal/report
- jangan membuat secret palsu
- jangan menebak API key

6. RUNTIME HEALTH CHECK

Jika aplikasi berhasil start:

uji health endpoint atau endpoint resmi yang memang tersedia.

Minimal verifikasi:

- application process hidup
- database connection berhasil
- API dapat menerima request
- authentication boundary tetap aktif
- workspace authorization tetap aktif
- bot resource authorization tetap aktif

Jangan melakukan destructive API request.

7. REGRESSION

Jalankan verification final:

- domain tests
- API tests
- authentication/session tests
- workspace authorization tests
- membership tests
- bot/resource tests
- typecheck
- format
- import boundary
- build

Jangan skip test.

Jangan menghapus test.

Jika failure terjadi, cari root cause sebenarnya.

8. SOURCE CODE FREEZE

Setelah source-code verification PASS:

JANGAN melakukan refactor baru.

JANGAN menambahkan fitur.

JANGAN mengubah architecture.

JANGAN mengubah security policy yang sudah selesai.

Jika migration/runtime gagal karena environment, jangan mengubah source code untuk menyembunyikan failure.

9. GIT FINAL CHECK

Jalankan:

git status
git diff --stat
git log --oneline -5

Pastikan:

- working tree clean
- tidak ada file secret
- tidak ada temporary file
- tidak ada build artifact
- tidak ada perubahan source code yang tidak diperlukan

Jika tidak ada perubahan source code:

JANGAN membuat empty commit.

Jika migration hanya dilakukan pada environment dan tidak mengubah repository:

JANGAN membuat commit.

10. PUSH

Jika ada commit source-code yang memang belum dipush:

git push

Branch tetap:

backend-dev-recovery

Jangan force push.

Jangan mengubah remote.

Jangan merge.

Jika GitHub authentication gagal:

- jangan mengubah source code
- jangan membuat commit kosong
- pertahankan commit lokal
- laporkan error sebenarnya

11. FINAL DECISION

Jika:

SOURCE CODE PASS
+ TEST PASS
+ BUILD PASS
+ DATABASE MIGRATION PASS
+ DATABASE CONNECTION PASS
+ RUNTIME HEALTH PASS

maka status:

READY FOR PRODUCTION

Jika database migration masih tidak dapat dijalankan karena Docker/environment:

status:

SOURCE CODE FINAL
DEPLOYMENT READY
DATABASE MIGRATION BLOCKED BY ENVIRONMENT

Jangan menyebut project "fully production verified" jika migration atau runtime belum berhasil.

12. FINAL REPORT

Tampilkan laporan ringkas:

SOURCE CODE:
- Status: ...

DATABASE:
- Database: ...
- Migration: PASS/BLOCKED
- Reason: ...

RUNTIME:
- Application start: PASS/BLOCKED
- Database connection: PASS/BLOCKED
- Health check: PASS/BLOCKED

TESTS:
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

GIT:
- Branch: ...
- HEAD: ...
- Working tree: CLEAN/DIRTY
- Push: SUCCESS/FAILED/NOT NEEDED

FINAL STATUS:
- READY FOR PRODUCTION
atau
- READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING
atau
- BLOCKED — [alasan sebenarnya]

PENTING:

Jangan mengklaim migration berhasil jika Docker/database tidak benar-benar menjalankannya.

Jangan mengklaim runtime sehat jika aplikasi belum benar-benar berhasil start.

Jangan mengubah source code hanya untuk membuat laporan terlihat PASS.

Selesaikan verification final dan berhenti.

```
# 
```



```
# Prompt berikutnya — Final Deployment Readiness
```
PROMPT: BotSpace — Final Deployment Readiness & Runtime Verification

Kita melanjutkan project BotSpace setelah SOURCE-CODE FINAL VERIFICATION.

Repository:
/root/botspace

Branch:
backend-dev-recovery

Kondisi terakhir:
- Source-code final verification: PASS
- Tests: PASS
- Build: PASS
- Security checks: PASS
- Working tree: CLEAN
- Git checkpoint sudah sinkron dengan origin
- Production readiness: READY FOR PRODUCTION

Satu-satunya blocker sebelumnya:

DATABASE MIGRATION:
BLOCKED — Docker unavailable in current environment

PENTING:
- Jangan menggunakan Kiro.
- Jangan membuat fitur baru.
- Jangan melakukan refactor besar.
- Jangan mengubah security architecture.
- Jangan membuat commit kosong.
- Jangan force push.
- Jangan reset.
- Jangan rebase.
- Jangan merge ke backend-dev.
- Jangan mengubah credential GitHub.
- Jangan mengubah production database secara destruktif.
- Jangan membuat fake migration success.

TUJUAN TAHAP INI:

FINAL RUNTIME + DEPLOYMENT READINESS

Alur:

SOURCE CODE FINAL
→ ENVIRONMENT CHECK
→ APPLICATION STARTUP
→ HEALTH CHECK
→ API SMOKE TEST
→ PRODUCTION CONFIG AUDIT
→ DATABASE MIGRATION READINESS
→ FINAL REPORT

==================================================
1. GIT CHECKPOINT
==================================================

Periksa:

git status
git branch --show-current
git log --oneline -5
git remote -v

Pastikan:

- branch = backend-dev-recovery
- working tree = CLEAN
- tidak ada perubahan lokal
- remote tidak berubah

Jika clean:

JANGAN membuat commit.

JANGAN push ulang tanpa perubahan.

==================================================
2. ENVIRONMENT AUDIT
==================================================

Periksa environment yang dibutuhkan aplikasi.

Audit:

- Node.js
- pnpm
- environment configuration
- PORT
- HOST
- DATABASE configuration
- authentication configuration
- required API configuration
- production mode configuration

JANGAN menampilkan secret.

Hanya tampilkan:

PRESENT
atau
MISSING

Jangan menampilkan:

- API key
- token
- password
- session secret
- database password
- private key

==================================================
3. PRODUCTION CONFIGURATION
==================================================

Audit konfigurasi production berdasarkan source code aktual.

Pastikan:

- production mode tersedia
- PORT dapat dikonfigurasi
- database configuration tersedia
- authentication configuration tersedia
- CORS sesuai architecture
- session configuration sesuai architecture
- error handling production aman
- logging tidak membocorkan secret
- health endpoint tersedia jika memang sudah ada

Jangan membuat configuration baru kecuali benar-benar diperlukan.

==================================================
4. APPLICATION STARTUP
==================================================

Cari command startup resmi repository.

Jangan menebak command jika package.json atau dokumentasi sudah menyediakan command.

Jalankan startup secara aman.

Tujuan:

memastikan aplikasi dapat melakukan:

- module loading
- configuration loading
- route registration
- service initialization

Jika startup membutuhkan database yang belum tersedia:

jangan membuat fake database.

Laporkan:

STARTUP BLOCKED BY DATABASE

jika memang demikian.

==================================================
5. HEALTH CHECK
==================================================

Jika health endpoint sudah tersedia:

jalankan endpoint tersebut.

Gunakan PORT aktual dari konfigurasi.

Pastikan:

- HTTP response valid
- status sesuai
- tidak ada secret leakage
- process benar-benar berjalan

Jika health endpoint belum tersedia:

jangan membuat endpoint baru.

Laporkan:

Health endpoint: NOT AVAILABLE

==================================================
6. API SMOKE TEST
==================================================

Jika aplikasi berhasil start dan test environment tersedia:

jalankan smoke test minimal.

Test:

Authentication:
- unauthenticated protected request → DENY

Workspace:
- authenticated valid workspace → ALLOW
- cross-workspace → DENY

Bot:
- authorized bot access → ALLOW
- unauthorized bot access → DENY

Jangan menggunakan production credentials.

Jangan membuat data production.

Gunakan test/dev environment jika tersedia.

==================================================
7. DATABASE MIGRATION
==================================================

Audit migration source code dan command.

Cari:

- migration files
- migration command
- database schema
- migration documentation

Jangan menjalankan migration terhadap production database dari tahap ini.

Jika Docker masih tidak tersedia:

DATABASE MIGRATION:
BLOCKED

Reason:
Docker unavailable in current environment.

Jangan mengubah source code untuk menghilangkan blocker.

Jangan membuat fake PASS.

Jika Docker tersedia dan repository menyediakan test migration environment:

jalankan migration verification secara aman pada environment non-production.

==================================================
8. PRODUCTION SECURITY FINAL CHECK
==================================================

Pastikan tidak ada:

- secret di source code
- secret di git diff
- credential di logs
- token di API response
- password di error response
- production .env masuk Git
- temporary files masuk repository

Jangan menampilkan nilai secret.

==================================================
9. BUILD FINAL
==================================================

Jalankan verification build resmi repository.

Minimal:

- typecheck
- tests
- format
- import boundary
- build

Jangan skip test.

Jika semuanya sudah PASS dan tidak ada perubahan source code:

jangan commit ulang.

==================================================
10. FINAL GIT CHECK
==================================================

Jalankan:

git status
git diff --stat
git log --oneline -3

Expected:

Working tree:
CLEAN

Jika clean:

NO NEW COMMIT REQUIRED

==================================================
11. FINAL DECISION
==================================================

Gunakan salah satu:

READY FOR DEPLOYMENT

atau:

READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING

atau:

NOT READY

Jika hanya Docker yang menjadi blocker migration, gunakan:

READY FOR DEPLOYMENT — DATABASE MIGRATION PENDING

Jangan menyebut source code gagal.

==================================================
12. FINAL REPORT
==================================================

Tampilkan:

FINAL BOTSPACE DEPLOYMENT READINESS

Repository:
- /root/botspace

Branch:
- ...

Commit:
- ...

Source Code:
- PASS

Tests:
- PASS

Build:
- PASS

Security:
- PASS

Working Tree:
- CLEAN

Startup:
- PASS / BLOCKED

Health:
- PASS / BLOCKED / NOT AVAILABLE

API Smoke:
- PASS / BLOCKED

Database Migration:
- PASS / BLOCKED

Migration Blocker:
- Docker unavailable jika memang masih terjadi

Git:
- checkpoint synchronized

FINAL DECISION:
READY FOR DEPLOYMENT

Jika migration masih blocked:

READY FOR DEPLOYMENT
DATABASE MIGRATION PENDING DOCKER ENVIRONMENT

==================================================
13. STOP CONDITION
==================================================

Jika:

- source code PASS
- tests PASS
- build PASS
- security PASS
- working tree CLEAN
- Git checkpoint aman

maka JANGAN melakukan coding tambahan.

JANGAN membuat commit kosong.

JANGAN mengulang security hardening.

JANGAN membuat fitur baru.

Nyatakan project:

BOTSPACE SOURCE CODE FINAL
PRODUCTION READY
DEPLOYMENT READY

Jika Docker belum tersedia, catat:

DATABASE MIGRATION PENDING DOCKER

Kemudian STOP.


```
# Prompt: BotSpace — Final Production Smoke Test & Deployment Readiness
```

PROMPT: BotSpace — Final Production Smoke Test & Deployment Readiness

Kita melanjutkan project BotSpace dari checkpoint FINAL SOURCE-CODE yang sudah selesai.

Repository:
/root/botspace

Branch:
backend-dev-recovery

Tujuan tahap ini:
FINAL PRODUCTION VERIFICATION

PENTING:
- Jangan menggunakan Kiro.
- Jangan membuat fitur baru.
- Jangan melakukan refactor besar.
- Jangan mengubah architecture.
- Jangan reset.
- Jangan force push.
- Jangan rebase.
- Jangan checkout branch lain.
- Jangan merge ke backend-dev.
- Jangan mengubah credential GitHub.
- Jangan menyentuh production database secara destruktif.
- Jangan menginstal Docker hanya untuk membuat verification terlihat PASS.
- Jangan mengubah source code hanya karena Docker tidak tersedia.

CHECKPOINT SAAT INI

Source-code verification sebelumnya:

- Domain tests: PASS
- API tests: PASS
- Observability: PASS
- Auth/Session: PASS
- Workspace: PASS
- Membership: PASS
- Bot/Resource: PASS
- Lifecycle: PASS
- Validation: PASS
- Mass-assignment: PASS
- Abuse boundary: PASS
- Secret leakage: PASS
- Typecheck: PASS
- Format: PASS
- Import boundary: PASS
- Build: 11/11 successful
- pnpm check: 44/44 successful
- Working tree: CLEAN
- Git commit: sudah tersedia
- Git push: sudah berhasil

DATABASE MIGRATION

Status sebelumnya:

BLOCKED

Error:

/bin/sh: 1: docker: not found

Ini adalah ENVIRONMENT BLOCKER, bukan source-code failure.

Jangan:
- mengubah migration hanya untuk melewati blocker
- membuat fake migration success
- mengganti migration production behavior
- menghapus migration test
- menambahkan Docker dependency ke source code
- mengubah source code hanya agar verification terlihat hijau

Jika Docker tidak tersedia, laporkan sebagai:

DATABASE MIGRATION:
BLOCKED — Docker unavailable in current environment

Jangan klaim migration PASS.

==================================================
1. FINAL REPOSITORY AUDIT
==================================================

Mulai dengan membaca kondisi repository aktual.

Jalankan:

pwd
git branch --show-current
git status --short
git log --oneline -5
git remote -v

Pastikan:

- berada di /root/botspace
- branch backend-dev-recovery
- working tree clean
- remote tetap benar
- tidak ada perubahan lokal yang tidak diketahui

Jika working tree dirty:

JANGAN langsung commit.

Audit perubahan terlebih dahulu dan laporkan.

==================================================
2. FINAL SOURCE-CODE VERIFICATION
==================================================

Jalankan verification resmi repository yang memang tersedia.

Gunakan command yang sudah digunakan repository sebelumnya.

Minimal:

- pnpm check
- typecheck
- format check
- import boundary check
- test suite
- build

Jangan membuat command baru jika repository sudah memiliki command resmi.

Jangan skip test.

Jika semuanya PASS, jangan mengubah source code.

Jika failure:

1. identifikasi apakah failure berasal dari source code atau environment
2. jika environment-only, jangan mengubah source code
3. jika source-code regression nyata, perbaiki hanya jika benar-benar diperlukan
4. ulangi verification

==================================================
3. DATABASE MIGRATION AUDIT
==================================================

Periksa status migration secara READ-ONLY.

Cari:

- migration files
- migration scripts
- database schema
- migration command
- migration documentation

Pastikan migration source code terlihat konsisten.

Jangan menjalankan migration terhadap production database.

Jika command migration membutuhkan Docker dan Docker tidak tersedia:

STOP pada bagian execution.

Laporkan:

Database migration:
BLOCKED
Reason:
Docker is unavailable in current environment.

Jangan membuat workaround palsu.

==================================================
4. ENVIRONMENT AUDIT
==================================================

Audit environment tanpa menampilkan secret.

Periksa:

- Node.js version
- pnpm version
- environment variable NAMES saja
- required configuration names
- port configuration
- database configuration presence
- API configuration presence

JANGAN tampilkan:

- API key
- token
- password
- secret
- session secret
- credential
- private key

Gunakan masking jika perlu.

Contoh:

API_KEY=********

Bukan nilai sebenarnya.

==================================================
5. PRODUCTION CONFIGURATION AUDIT
==================================================

Audit konfigurasi production yang sudah tersedia.

Cari:

- NODE_ENV
- PORT
- HOST
- database URL presence
- CORS configuration
- cookie/session configuration
- logging configuration
- health endpoint
- readiness endpoint
- graceful shutdown
- error handling

Jangan mengubah configuration production.

Jika configuration belum tersedia, laporkan sebagai checklist item.

==================================================
6. STARTUP SMOKE TEST
==================================================

Jika repository menyediakan command startup resmi:

gunakan command tersebut secara aman.

Tujuan:

memastikan aplikasi dapat start tanpa error source-code.

Periksa:

- application startup
- module loading
- database initialization behavior
- route registration
- configuration validation
- graceful startup failure

Jangan menjalankan destructive database migration.

Jika aplikasi membutuhkan database atau secret yang tidak tersedia di environment saat ini:

jangan membuat fake value.

Laporkan dependency yang hilang.

==================================================
7. HEALTH CHECK
==================================================

Jika health endpoint tersedia:

jalankan health check.

Contoh pola:

curl -i http://127.0.0.1:<PORT>/health

atau command health check resmi repository.

Jika health endpoint berbeda, gunakan route aktual repository.

Pastikan:

- HTTP status sesuai
- response tidak membocorkan secret
- application process aktif

Jika endpoint tidak tersedia:

jangan membuat endpoint baru.

Laporkan:

Health endpoint:
NOT AVAILABLE

==================================================
8. API SMOKE TEST
==================================================

Jika API dapat dijalankan di environment ini, lakukan smoke test minimal.

Test hanya endpoint yang memang tersedia.

Minimal:

PUBLIC:
- public endpoint jika ada

AUTH:
- unauthenticated protected endpoint harus ditolak

WORKSPACE:
- authenticated workspace access

BOT:
- authenticated bot/resource access

SECURITY:
- cross-workspace request ditolak

Jangan membuat test data production.

Gunakan test/dev database jika repository menyediakannya.

Jangan menggunakan credential production.

==================================================
9. SECRET LEAKAGE FINAL CHECK
==================================================

Lakukan final audit untuk kemungkinan secret masuk ke:

- source code
- logs
- error messages
- test output
- API response
- git diff
- git history baru

Cari pola secret secara aman.

Jangan mencetak nilai secret ke terminal report.

Jika menemukan secret nyata:

JANGAN menampilkan nilainya.

Laporkan hanya lokasi file/jenis masalah.

==================================================
10. GIT FINAL AUDIT
==================================================

Setelah seluruh verification:

jalankan:

git status
git diff --stat
git diff
git log --oneline -5

Pastikan:

Working tree:
CLEAN

Jika clean, jangan membuat empty commit.

Jangan membuat commit hanya untuk dokumentasi status.

==================================================
11. PUSH FINAL
==================================================

Jika tidak ada perubahan source code dan checkpoint terakhir sudah berhasil dipush:

JANGAN membuat commit kosong.

JANGAN push ulang tanpa perubahan.

Jika memang ada perubahan nyata yang diperbaiki pada tahap ini:

- jalankan verification ulang
- buat SATU commit
- push branch backend-dev-recovery

Jika push gagal:

jangan mengubah source code.

Laporkan error Git sebenarnya.

==================================================
12. PRODUCTION READINESS DECISION
==================================================

Buat keputusan berdasarkan hasil nyata.

Gunakan kategori:

READY FOR PRODUCTION

jika:
- source code verification PASS
- tests PASS
- build PASS
- working tree CLEAN
- Git checkpoint aman
- tidak ada source-code blocker

Environment blocker seperti Docker migration harus dipisahkan sebagai:

ENVIRONMENT BLOCKER

Jangan menyebut source code FAILED jika hanya environment yang tidak tersedia.

==================================================
13. FINAL REPORT
==================================================

Tampilkan laporan akhir dengan format:

FINAL PRODUCTION VERIFICATION

Repository:
- /root/botspace

Branch:
- ...

Commit:
- hash: ...
- message: ...

Source Code:
- Domain: PASS/FAIL
- API: PASS/FAIL
- Auth/Session: PASS/FAIL
- Workspace: PASS/FAIL
- Membership: PASS/FAIL
- Bot/Resource: PASS/FAIL
- Lifecycle: PASS/FAIL
- Typecheck: PASS/FAIL
- Format: PASS/FAIL
- Import boundary: PASS/FAIL
- Build: PASS/FAIL

Runtime:
- Startup: PASS/FAIL/BLOCKED
- Health: PASS/FAIL/N/A
- API smoke test: PASS/FAIL/BLOCKED

Database:
- Migration source audit: PASS/FAIL
- Migration execution: PASS/BLOCKED
- Blocker: Docker unavailable jika memang masih terjadi

Security:
- Secret leakage: PASS/FAIL
- Cross-workspace isolation: PASS/FAIL
- Authentication: PASS/FAIL
- Authorization: PASS/FAIL

Git:
- Working tree: CLEAN/DIRTY
- Push: SUCCESS/NOT NEEDED/FAILED

FINAL DECISION:

READY FOR PRODUCTION

atau:

NOT READY

Jika NOT READY, jelaskan hanya blocker nyata.

==================================================
14. STOP CONDITION
==================================================

Jika hasil akhirnya:

- source code PASS
- tests PASS
- build PASS
- working tree CLEAN
- Git checkpoint aman
- hanya Docker migration yang BLOCKED karena environment

maka:

JANGAN melakukan coding tambahan.

JANGAN membuat commit kosong.

JANGAN membuat fitur baru.

JANGAN mengubah security code.

JANGAN mengulang audit yang sudah PASS.

Nyatakan:

SOURCE CODE FINAL
PRODUCTION READY
DATABASE MIGRATION MENUNGGU ENVIRONMENT DOCKER

Kemudian STOP.

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
