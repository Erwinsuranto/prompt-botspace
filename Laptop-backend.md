



# 
```



```

# 
```



```
# 
```



```
# 
```



```

#
```



```
#
```



```
#
```



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
