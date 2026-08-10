








# 
```



```

# 
```



```

# 
```



```

# 
```



```

# 
```



```
# 
```



```

# F-011 audit
```

PROMPT: BOTSPACE F-011 — UI PRIMITIVES BASELINE AUDIT

Kamu adalah Kimi utama untuk BotSpace FRONTEND.

WORKTREE:
/root/botspace-frontend

BRANCH:
frontend-dev

==================================================
CURRENT STATUS
==================================================

F-002:
COMPLETE

F-010:
COMPLETE

Existing frontend design commit:
07ff3f1

F-010 tidak menghasilkan commit baru karena deliverable F-010
sudah tercakup oleh commit 07ff3f1.

Validation:
- Lint PASS
- Typecheck PASS
- Test PASS
- Build PASS
- Mobile 390px PASS
- Desktop 1440px PASS
- No horizontal overflow

Backend files changed:
NONE

Shared files changed:
NONE

Push:
NO

==================================================
TASK
==================================================

Audit F-011 — UI primitives baseline.

Baca:
- ROADMAP_V2.md
- AI_TASKS.md
- AI_RULES.md
- docs/architecture/ADR-009-frontend-framework.md
- struktur frontend aktual

JANGAN LANGSUNG CODING.

Pertama tentukan apakah F-011:
1. belum dikerjakan,
2. sebagian dikerjakan,
3. atau SUDAH TERPENUHI oleh commit 07ff3f1.

==================================================
AUDIT EXISTING UI
==================================================

Cari dan audit komponen/primitive yang sudah tersedia.

Minimal periksa apakah sudah ada:

- Button
- Card
- Badge
- Input
- Select
- Textarea
- Table
- Modal/Dialog
- Dropdown
- Tabs
- Toast
- Tooltip
- Empty State
- Loading State
- Error State

Jangan mengasumsikan semua komponen wajib dibuat.
Ikuti acceptance criteria F-011 yang sebenarnya.

Cari juga penggunaan komponen tersebut di:

apps/web
packages/ui
dan folder frontend lain yang relevan.

==================================================
DUPLICATION RULE
==================================================

SANGAT PENTING:

Jangan membuat komponen baru jika komponen yang setara sudah ada.

Jangan membuat design system kedua.

Jika 07ff3f1 sudah memenuhi F-011:
JANGAN mengubah source code.
JANGAN membuat commit baru.

Cukup dokumentasikan evidence bahwa F-011 sudah terpenuhi.

Jika F-011 hanya sebagian terpenuhi:
implementasikan HANYA bagian yang benar-benar masih kurang.

Jika F-011 membutuhkan dependency baru:
STOP dan laporkan terlebih dahulu.
Jangan install dependency tanpa alasan yang jelas.

==================================================
DESIGN REQUIREMENTS
==================================================

UI harus:

- cepat
- ringan
- jelas
- readable
- responsive
- mobile-first
- konsisten dengan design BotSpace
- tidak menggunakan animasi berat
- tidak menggunakan library besar tanpa kebutuhan

Pastikan komponen dapat digunakan kembali oleh halaman BotSpace berikutnya.

Jangan membuat komponen khusus untuk satu halaman jika sebenarnya dapat dibuat reusable.

==================================================
WORKTREE SAFETY
==================================================

Hanya bekerja di:

/root/botspace-frontend

Jangan menyentuh:

/root/botspace
/root/botspace-backend

Jangan mengubah:

- ROADMAP.md
- ROADMAP_V2.md
- pnpm-lock.yaml
- root package.json
- pnpm-workspace.yaml
- turbo.json
- packages/contracts/

kecuali F-011 secara eksplisit membutuhkan perubahan tersebut.

Jika ada kebutuhan shared-file change:
STOP dan laporkan.

==================================================
VALIDATION
==================================================

Jika tidak ada perubahan:
cukup lakukan audit dan validation ringan untuk membuktikan existing implementation.

Jika ada perubahan:
jalankan:

- lint
- typecheck
- test
- build

Verifikasi:

390px mobile
768px tablet
1440px desktop

Pastikan tidak ada horizontal overflow.

==================================================
GIT
==================================================

Jika F-011 SUDAH TERPENUHI:

- jangan ubah file
- jangan commit
- jangan push

Jika F-011 membutuhkan implementasi baru:

- hanya commit perubahan F-011
- gunakan pesan:

feat: complete F-011 ui primitives baseline

JANGAN PUSH.

==================================================
FINAL REPORT
==================================================

BOTSPACE F-011 RESULT

Task:
F-011

Title:
...

Status:
ALREADY COMPLETE / PARTIAL / IMPLEMENTED / BLOCKED

Evidence:
...

Existing Components:
...

Missing Components:
...

Files Changed:
- ...

Validation:
- Lint:
- Typecheck:
- Test:
- Build:
- Mobile:
- Desktop:

Backend Files Changed:
NONE

Shared Files Changed:
NONE

ROADMAP.md:
NOT MODIFIED

ROADMAP_V2.md:
NOT MODIFIED

Commit:
...

Working Tree:
...

Push:
NO

Next Recommended Task:
...

IMPORTANT:
Jika F-011 sudah terpenuhi oleh 07ff3f1, jangan membuat pekerjaan
duplikat. Laporkan bahwa F-011 COMPLETE berdasarkan existing deliverable.

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.

```
# 
```
PROMPT: BOTSPACE F-010 — EXECUTE FRONTEND ROADMAP TASK

Kamu adalah Kimi utama untuk BotSpace FRONTEND.

WORKTREE:
 /root/botspace-frontend

BRANCH:
 frontend-dev

==================================================
CURRENT STATUS
==================================================

Frontend design foundation:
COMPLETE

Commit design:
07ff3f1

Frontend Framework ADR F-002:
COMPLETE

Commit F-002:
167d9a2

Validation sebelumnya:
- Lint PASS
- Typecheck PASS
- Test PASS
- Build PASS
- Mobile 390px PASS
- Desktop 1440px PASS
- No horizontal overflow
- Backend files changed: NONE
- Shared files changed: NONE
- ROADMAP.md NOT MODIFIED

Backend B-001:
COMPLETE

Backend B-004 sedang dikerjakan di worktree terpisah.

==================================================
TASK
==================================================

Sekarang kerjakan:

F-010

Baca ROADMAP_V2.md dan AI_TASKS.md terlebih dahulu.

PENTING:
Jangan menebak isi F-010.
Gunakan definisi task F-010 yang tertulis di ROADMAP_V2.md sebagai source of truth.

Sebelum coding, tampilkan secara singkat:

- F-010 title
- objective
- dependencies
- expected files
- acceptance criteria
- apakah F-010 benar-benar READY

Jika F-010 ternyata masih BLOCKED oleh dependency yang belum selesai:
JANGAN CODING.
Laporkan dependency yang belum selesai dan tunggu instruksi.

Jika F-010 READY:
lanjutkan implementasi.

==================================================
WORKTREE SAFETY
==================================================

Hanya bekerja di:

/root/botspace-frontend

Branch harus:

frontend-dev

Jangan menyentuh:

/root/botspace
/root/botspace-backend

Jangan mengubah:

- ROADMAP.md
- ROADMAP_V2.md
- pnpm-lock.yaml
- root package.json
- pnpm-workspace.yaml
- turbo.json
- packages/contracts/

kecuali F-010 secara eksplisit menyatakan salah satu file tersebut sebagai bagian task.

Jika task membutuhkan shared-file change yang tidak disebutkan F-010:
STOP dan laporkan.

==================================================
FRONTEND QUALITY
==================================================

Pertahankan design foundation yang sudah dibuat.

UI harus:

- cepat
- ringan
- jelas
- responsive
- mobile-friendly
- desktop-friendly
- mudah dibaca
- konsisten dengan BotSpace
- tidak terlalu padat

Jangan membuat UI kecil atau sulit dibaca.

Hindari:

- animasi berat
- library besar yang tidak diperlukan
- dependency baru tanpa alasan
- glassmorphism berlebihan
- background animation
- efek visual berat
- client-side JavaScript yang tidak diperlukan

Gunakan komponen reusable yang sudah tersedia.

Jangan membuat design system kedua.

==================================================
CODE QUALITY
==================================================

Ikuti architecture frontend yang sudah ada.

Sebelum membuat component baru:

periksa apakah component reusable yang diperlukan sudah tersedia.

Hindari:

- duplicate component
- duplicate logic
- any tanpa alasan
- unused imports
- dead code
- file halaman yang terlalu besar
- state global jika local state cukup

Jika F-010 membutuhkan API tetapi backend endpoint belum tersedia:

gunakan abstraction/mock yang sesuai dengan architecture repository.

Jangan membuat backend endpoint baru.

Jangan memasukkan API key, token, password, atau secret.

==================================================
RESPONSIVE
==================================================

Pastikan F-010 bekerja minimal pada:

390px mobile

768px tablet

1440px desktop

Tidak boleh ada horizontal overflow.

Button harus mudah disentuh di mobile.

Text harus readable.

Table/list harus memiliki strategi responsive yang benar.

==================================================
VALIDATION
==================================================

Setelah implementasi:

1. git status
2. git diff --stat
3. git diff

Kemudian jalankan validation frontend yang tersedia:

- lint
- typecheck
- test
- build

Jika ada command khusus frontend di repository, gunakan command tersebut.

Jangan memperbaiki unrelated error.

Jika validation gagal karena masalah yang sudah ada sebelum F-010:
identifikasi dan laporkan.

==================================================
GIT
==================================================

Setelah semua valid:

Pastikan hanya perubahan F-010 yang ada.

Commit:

git add <F-010 frontend files>

git commit -m "feat: implement F-010 frontend"

JANGAN PUSH.

==================================================
FINAL OUTPUT
==================================================

BOTSPACE F-010 RESULT

Task:
F-010

Title:
...

Status:
COMPLETE / BLOCKED

Branch:
frontend-dev

Implementation:
- ...

Files Changed:
- ...

Dependencies:
- ...

Validation:
- Lint:
- Typecheck:
- Test:
- Build:
- Mobile 390px:
- Desktop 1440px:

Backend Files Changed:
NONE

Shared Files Changed:
NONE

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

Next Recommended Task:
...

DO NOT PUSH.
WAIT FOR NEXT INSTRUCTION.


```
# HP — Kimi utama — F-002
```

PROMPT: BOTSPACE F-002 — FRONTEND FRAMEWORK ADR

Kamu adalah Kimi utama untuk BotSpace FRONTEND.

WORKTREE:
 /root/botspace-frontend

BRANCH:
 frontend-dev

TASK:
F-002 — Dokumentasikan keputusan frontend framework.

FILE:
docs/architecture/ADR-009-frontend-framework.md

==================================================
KONDISI SAAT INI
==================================================

Frontend design implementation sudah selesai dan sudah di-commit:

commit:
07ff3f1

Validation sebelumnya:

- Lint PASS
- Typecheck PASS
- Test PASS
- Build PASS
- Mobile 390px PASS
- Desktop 1440px PASS
- No unused imports
- Backend files changed: NONE
- Shared files changed: NONE

Jangan merusak hasil tersebut.

==================================================
ATURAN
==================================================

- Hanya bekerja di /root/botspace-frontend.
- Branch harus frontend-dev.
- Jangan menyentuh /root/botspace-backend.
- Jangan menyentuh /root/botspace/main.
- Jangan mengubah source code frontend kecuali diperlukan untuk ADR — seharusnya tidak perlu.
- Jangan mengubah package.json.
- Jangan mengubah pnpm-workspace.yaml.
- Jangan mengubah pnpm-lock.yaml.
- Jangan mengubah turbo.json.
- Jangan mengubah packages/contracts.
- Jangan mengubah ROADMAP.md.
- Jangan melakukan dependency installation.
- Jangan menambahkan dependency.
- Jangan push.

==================================================
TUJUAN
==================================================

Buat ADR yang mendokumentasikan framework frontend yang BENAR-BENAR digunakan oleh repository.

Sebelum menulis:

- periksa apps/web
- package.json yang relevan
- tsconfig
- vite config jika ada
- router
- existing frontend source
- existing test setup
- existing UI structure

Jangan menebak framework.

==================================================
ADR CONTENT
==================================================

Buat:

docs/architecture/ADR-009-frontend-framework.md

Isi minimal:

# ADR-009: Frontend Framework

## Status
Accepted

## Date
gunakan tanggal aktual

## Context

Jelaskan kebutuhan frontend BotSpace sebagai web application untuk:

- Workspace
- Telegram Accounts
- Bots
- Modules
- Automation
- AI
- Storage
- Settings

## Decision

Dokumentasikan framework yang benar-benar digunakan.

## Why

Jelaskan alasan berdasarkan repository dan kebutuhan BotSpace.

## Alternatives Considered

Bahas alternatif yang relevan tanpa mengubah project.

## Consequences

Positive:
- ...

Negative:
- ...

## Performance Considerations

Jelaskan bagaimana framework digunakan agar:

- cepat
- ringan
- responsive
- tidak terlalu banyak client-side JavaScript
- mobile friendly

## Testing

Dokumentasikan setup testing aktual.

## Build

Dokumentasikan build tooling aktual.

## Backend Integration

Jelaskan secara konseptual bagaimana frontend akan berkomunikasi dengan backend.

Jangan membuat API baru.

## Future Considerations

Catat hal yang perlu dievaluasi nanti.

==================================================
IMPORTANT
==================================================

ADR harus berdasarkan kondisi repository AKTUAL.

Jangan mengatakan React/Vite/atau framework tertentu digunakan kalau repository tidak membuktikannya.

Jangan mengklaim API atau feature sudah production-ready jika belum ada.

==================================================
VALIDATION
==================================================

Setelah membuat ADR:

git status
git diff --stat
git diff -- docs/architecture/ADR-009-frontend-framework.md

Pastikan hanya file ADR yang berubah.

Tidak boleh ada perubahan:

- backend
- package.json
- pnpm-lock.yaml
- workspace config
- contracts
- ROADMAP.md

==================================================
COMMIT
==================================================

Jika valid:

git add docs/architecture/ADR-009-frontend-framework.md

git commit -m "docs: add frontend framework ADR"

JANGAN PUSH.

==================================================
FINAL OUTPUT
==================================================

BOTSPACE F-002 RESULT

Branch:
frontend-dev

Framework:
- ...

ADR:
docs/architecture/ADR-009-frontend-framework.md

Validation:
- ...

Changed Files:
- ...

Commit:
- ...

Backend Files Changed:
NONE

Shared Files Changed:
NONE

ROADMAP.md:
NOT MODIFIED

Push:
NO

FINAL STATUS:
F-002 COMPLETE
WAIT FOR NEXT INSTRUCTION

```
#
```

PROMPT: BOTSPACE FRONTEND — IMPLEMENT DESIGN FOUNDATION

Kamu adalah Kimi utama untuk BotSpace FRONTEND.

WORKTREE:
 /root/botspace-frontend

BRANCH:
 frontend-dev

TASK:
Implementasikan desain UI/UX BotSpace berdasarkan design direction yang sudah disetujui.

FOKUS:
FRONTEND DESIGN + UI IMPLEMENTATION.

Jangan mengerjakan backend.

==================================================
TUJUAN UTAMA
==================================================

Bangun frontend BotSpace yang:

- modern
- profesional
- clean
- cepat
- ringan
- responsive
- mudah dibaca
- nyaman di desktop
- nyaman di mobile
- tidak terlalu padat
- tidak menggunakan efek berat yang memperlambat rendering

BotSpace adalah website untuk membuat dan mengelola Telegram Bot.

UI harus membuat fungsi utama langsung terlihat:

1. Workspace
2. Telegram Account
3. My Bots
4. Create Bot
5. Modules
6. Automation
7. AI
8. Storage
9. Logs
10. Settings

==================================================
DESIGN REFERENCE
==================================================

Gunakan arah desain mockup BotSpace yang telah disetujui:

- sidebar desktop
- topbar
- dashboard
- workspace selector
- bot overview
- recent activity
- quick actions
- My Bots
- Create Bot
- Bot Detail
- Modules
- Bot Settings
- mobile responsive navigation

Jangan menyalin mockup secara buta.

Sesuaikan dengan struktur repository dan framework yang benar-benar digunakan.

==================================================
ATURAN CODE — SANGAT PENTING
==================================================

Prioritas:

PERFORMANCE > DECORATION

Gunakan implementasi yang sederhana dan efisien.

HINDARI:

- animasi berat
- background animation
- particle effects
- video background
- blur berlebihan
- backdrop-filter berlebihan
- efek glassmorphism berat
- library UI besar jika tidak diperlukan
- library animation besar jika tidak diperlukan
- chart library berat jika belum diperlukan
- icon library besar jika repository sudah memiliki icon system
- komponen yang melakukan render berulang tanpa alasan
- nested component yang tidak diperlukan
- CSS yang terlalu kompleks
- JavaScript hanya untuk styling
- polling API yang belum diperlukan

Jangan menambahkan dependency baru hanya untuk membuat UI terlihat bagus.

Gunakan dependency yang sudah tersedia.

Jika sebuah fitur bisa dibuat menggunakan CSS/native browser API, prioritaskan cara tersebut daripada dependency baru.

==================================================
READABILITY
==================================================

UI harus JELAS DI LAYAR.

Jangan membuat:

- font terlalu kecil
- sidebar terlalu lebar
- card terlalu sempit
- button terlalu kecil
- text terlalu panjang dalam satu baris
- tabel yang memaksa horizontal scroll di mobile
- terlalu banyak card dalam satu viewport
- dashboard yang terlalu penuh

Gunakan visual hierarchy yang kuat.

Target:

Desktop:
- sidebar jelas
- content memiliki ruang cukup
- heading mudah terlihat
- card tidak terlalu kecil

Mobile:
- font tetap readable
- button mudah disentuh
- card tidak berdesakan
- navigation mudah digunakan
- tidak ada horizontal overflow

Minimum body text:
gunakan ukuran yang nyaman dibaca, sekitar 14–16px sesuai konteks.

Jangan menggunakan 10–12px sebagai body text utama.

==================================================
COLOR
==================================================

Gunakan visual identity BotSpace:

Primary:
blue

Secondary:
purple/indigo secukupnya

Success:
green

Warning:
orange/yellow

Danger:
red

Background:
light neutral

Surface:
white

Text:
dark neutral

Secondary text:
muted neutral

Jangan menggunakan terlalu banyak warna.

Status harus mudah dibedakan.

==================================================
LAYOUT
==================================================

Desktop:

Sidebar
+
Topbar
+
Main Content

Sidebar:

BotSpace logo

Workspace selector

MAIN
- Dashboard
- Workspaces
- Telegram Accounts
- My Bots

FEATURES
- Modules
- Automation
- AI Configuration
- File Storage

TOOLS
- Logs
- Analytics

SETTINGS
- Team
- Workspace Settings
- Billing

Sesuaikan menu dengan route yang benar-benar tersedia.

Jangan membuat route backend baru.

==================================================
DASHBOARD
==================================================

Dashboard harus fokus pada bot management.

Header:

Welcome back

Subtitle:
Manage your Telegram bots, modules, and automation in one place.

Primary CTA:

Create Bot

Secondary:
Connect Telegram Account

Statistics:

Workspaces
Telegram Accounts
Bots
Modules
Active Bots

Bot Overview:

Total Bots
Active
Inactive
Stopped
Error

Recent Activity:

- Bot created
- Bot started
- Bot stopped
- Module installed
- Account connected

Quick Actions:

Create New Bot
Connect Telegram Account
Install Module
Create Automation

Workspace Info:

Workspace name
Members
Bots
Modules
Usage

==================================================
CREATE BOT
==================================================

Buat UI wizard yang jelas:

Step 1
Select Workspace

Step 2
Bot Information

Step 3
Configuration

Step 4
Review

Jangan membuat wizard terlalu rumit.

CTA harus jelas:

Back
Next
Create Bot

Gunakan progress indicator yang sederhana.

==================================================
MY BOTS
==================================================

Buat halaman daftar bot.

Desktop:
gunakan table/list yang readable.

Mobile:
ubah menjadi card/list.

Informasi:

Bot Name
Username
Workspace
Status
Created
Actions

Actions:

View
Settings
Start
Stop
Restart

Jangan membuat terlalu banyak tombol terlihat sekaligus.

Gunakan action menu jika diperlukan.

==================================================
BOT DETAIL
==================================================

Header:

Bot avatar/icon
Bot name
@username
Workspace
Status

Primary actions:

Start
Stop
Restart

Tabs:

Overview
Settings
Modules
Automation
AI
Logs
Analytics

Overview:

Status
Uptime
Last Restart
Version
Usage
Messages
Users
API Requests
Errors

==================================================
MODULES
==================================================

Buat halaman module management yang jelas.

Setiap module:

Name
Description
Status
Version
Action

Status:

Installed
Available
Disabled

Action:

Install
Enable
Disable
Settings

Gunakan toggle hanya jika memang sesuai UX.

==================================================
BOT SETTINGS
==================================================

Sections:

General
Bot Information
Privacy
Commands
Permissions
Language
Danger Zone

Form harus jelas.

Gunakan label yang mudah dibaca.

Jangan membuat form terlalu padat.

==================================================
RESPONSIVE
==================================================

Mobile-first considerations.

Desktop:
sidebar fixed/standard layout.

Tablet:
sidebar dapat collapse.

Mobile:
sidebar menjadi drawer.

Topbar:
compact.

Bottom navigation boleh digunakan jika memang cocok dengan existing architecture.

Prioritaskan:

Dashboard
Bots
Accounts
Modules
More

Jangan membuat mobile menjadi versi desktop yang dipaksa mengecil.

==================================================
COMPONENT ARCHITECTURE
==================================================

Gunakan reusable components.

Contoh:

Button
Card
Badge
Input
Select
Modal
Dropdown
Tabs
Table
EmptyState
LoadingState
ErrorState
PageHeader
StatCard
StatusBadge
BotCard
BotTable
WorkspaceSelector
Sidebar
Topbar

Jangan membuat duplicate component untuk fungsi yang sama.

Jika repository sudah memiliki component system:
GUNAKAN component system tersebut.

Jangan membuat design system kedua.

==================================================
MOCK DATA
==================================================

Backend belum menjadi dependency untuk design implementation.

Jika API belum tersedia:

gunakan mock/local data untuk preview UI.

Pisahkan mock data dari UI components.

Jangan membuat mock API yang terlihat seperti production implementation.

Jangan memasukkan:

- API key
- bot token
- password
- secret
- credential

==================================================
PERFORMANCE
==================================================

Optimalkan untuk perangkat mobile/VPS environment.

Gunakan:

- CSS sederhana
- reusable components
- lazy loading jika memang diperlukan
- dynamic import hanya untuk component berat
- memoization hanya jika benar-benar diperlukan
- minimal client-side JavaScript
- minimal dependencies

Jangan melakukan premature optimization.

Jangan menggunakan React.memo/useMemo/useCallback di semua tempat tanpa alasan.

Jangan menggunakan state global jika local state cukup.

Jangan melakukan fetch/polling API karena backend belum menjadi task ini.

==================================================
ACCESSIBILITY
==================================================

Pastikan:

- button memiliki label
- input memiliki label
- icon-only button memiliki aria-label
- keyboard navigation tidak rusak
- contrast cukup
- focus state terlihat
- semantic HTML digunakan bila memungkinkan

==================================================
CODE QUALITY
==================================================

Ikuti coding standard repository.

Jangan membuat file sangat besar.

Pisahkan component berdasarkan tanggung jawab.

Hindari:

any yang tidak perlu
duplicate logic
hardcoded secret
dead code
unused import
unused component
unused dependency

==================================================
IMPORTANT — SHARED FILES
==================================================

JANGAN UBAH:

pnpm-lock.yaml

JANGAN UBAH:

root package.json

JANGAN UBAH:

pnpm-workspace.yaml

JANGAN UBAH:

turbo.json

JANGAN UBAH:

backend files

JANGAN UBAH:

packages/contracts/

JANGAN UBAH:

ROADMAP.md

Jangan mengubah shared files hanya demi styling.

Jika benar-benar membutuhkan perubahan shared file:

STOP.

Laporkan file tersebut dan alasannya.

Jangan mengambil keputusan sendiri.

==================================================
IMPLEMENTATION ORDER
==================================================

Kerjakan secara bertahap:

1. Audit existing frontend architecture
2. Existing design system/components
3. App shell
4. Sidebar
5. Topbar
6. Workspace selector
7. Dashboard
8. Create Bot UI
9. My Bots
10. Bot Detail
11. Modules
12. Bot Settings
13. Responsive mobile
14. Loading/empty/error states
15. Accessibility
16. Performance cleanup

Jangan mengerjakan backend.

==================================================
VALIDATION
==================================================

Setelah implementation:

1. git status
2. git diff --stat
3. inspect changed files
4. run frontend lint jika tersedia
5. run frontend typecheck jika tersedia
6. run frontend build jika aman
7. pastikan tidak ada horizontal overflow
8. pastikan mobile layout readable
9. pastikan desktop layout readable
10. pastikan tidak ada unused import
11. pastikan tidak ada source backend berubah

Jika ada existing unrelated error:

JANGAN memperbaikinya di luar scope.

Laporkan error tersebut.

==================================================
GIT
==================================================

Setelah validation berhasil:

git status

Jika hanya frontend changes:

git add <frontend files>

git commit -m "feat: build BotSpace frontend design"

JANGAN PUSH.

==================================================
FINAL OUTPUT
==================================================

BOTSPACE FRONTEND DESIGN IMPLEMENTATION

Branch:
frontend-dev

Framework:

Implemented:
- App Shell
- Sidebar
- Topbar
- Dashboard
- Workspace Selector
- Create Bot
- My Bots
- Bot Detail
- Modules
- Bot Settings
- Responsive Mobile
- States
- Accessibility

Performance:
- ...

Dependencies Added:
- NONE / list only if absolutely required

Changed Files:
- ...

Validation:
- Lint:
- Typecheck:
- Build:
- Mobile:
- Desktop:

Backend Files Changed:
- NONE

Shared Files Changed:
- NONE

ROADMAP.md:
- NOT MODIFIED

Commit:
- ...

Push:
- NO

FINAL STATUS:
FRONTEND DESIGN IMPLEMENTED
WAIT FOR NEXT INSTRUCTION

```
