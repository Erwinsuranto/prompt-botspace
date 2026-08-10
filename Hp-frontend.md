






#
```



```

#
```



```
#
```



```
#
```



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
