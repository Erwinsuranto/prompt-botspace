




# 
```



```
# 
```



```

# 
```



```
# 
```



```

# 
```



```
# 
```



```
# 
```



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
