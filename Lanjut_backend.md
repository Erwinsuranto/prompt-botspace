

# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



```
# 
```



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
