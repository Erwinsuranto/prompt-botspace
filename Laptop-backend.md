




#
```



```
#
```



```
#
```



```
#
```



```
#
```



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
