










# 
```



```
# 
```
Investigate why models returned by GET /v1/models are not fully usable by OpenCode.

Current behavior:

- GET /v1/models correctly returns:
  openrouter/cohere/north-mini-code:free

- But:
  opencode models nvidia
  does not include that model.

- opencode models openrouter
  returns "Not found" because OpenCode only has one provider configured.

Architecture goal:

The gateway is the ONLY provider configured in OpenCode.

OpenCode should not need separate providers for:
- nvidia
- openrouter
- stepfun
- cloudflare

The gateway itself is responsible for routing.

Tasks:

1. Audit the implementation of GET /v1/models.

2. Audit how model IDs are generated.

3. Check whether model IDs with prefixes like:

   openrouter/
   stepfun/
   cloudflare/

   are being filtered or ignored by OpenCode because only one provider exists.

4. Design a solution so every model exposed by the gateway is selectable from OpenCode while keeping only ONE provider configuration.

5. Do not require additional providers in OpenCode.

6. Preserve OpenAI-compatible API behavior.

7. Verify that these models are selectable:

- nvidia/zai/glm-5.2
- stepfun/step-3.7-flash
- openrouter/cohere/north-mini-code:free

8. Explain the root cause.

9. Show every modified file.

10. Build and run tests.


```
# 
```

Refactor the AI Gateway model routing architecture.

## Goal

The gateway must NEVER replace the model selected by the client.

If the client requests:

- nvidia/glm-5.2
- nvidia/deepseek-v4-flash
- nvidia/qwen3-coder
- stepfun/step-3.7-flash
- openrouter/cohere/north-mini-code:free

the gateway MUST send exactly that model to the selected provider.

Do NOT automatically switch to another model.

## Required Behavior

Example:

Client:

model = "nvidia/glm-5.2"

Gateway:

Provider = NVIDIA
Model = glm-5.2

If the provider returns an error (429, 500, unavailable, etc.), return the provider error.

Do NOT change the model to DeepSeek, Qwen, Gemma, or any other model.

Another example:

Client:

model = "nvidia/deepseek-v4-flash"

Always send:

deepseek-v4-flash

Never replace it with GLM or Qwen.

## Provider Selection

The gateway may still choose:

- API Key
- Endpoint
- Region
- Server

But it must NOT change the requested model.

## Remove

Remove all logic that:

- selects the "best coding model"
- replaces one model with another
- automatic cross-model fallback
- automatic alias resolution that changes the requested model

## Models Endpoint

GET /v1/models must return every supported model exactly as the client should use it.

Example:

nvidia/glm-5.2
nvidia/deepseek-v4-flash
nvidia/qwen3-coder

stepfun/step-3.7-flash

openrouter/cohere/north-mini-code:free
openrouter/poolside/laguna-s-2.1:free
openrouter/openai/gpt-oss-20b:free

cloudflare/...

## Internal Flow

Request

↓

Parse provider prefix

↓

Select provider

↓

Select API key

↓

Forward EXACT requested model

↓

Return response

No model replacement.

## Logging

Log:

Incoming model

Resolved provider

Actual upstream model

Selected API key

Latency

Never log that another model was chosen.

## Compatibility

Maintain full OpenAI API compatibility.

Do not change request or response schema.

## Deliverables

- Remove model replacement logic
- Keep provider routing
- Keep API key rotation
- Keep OpenAI compatibility
- Build successfully
- Run tests
- Show all modified files
- Explain the new architecture

```

# 
```
# Prompt: Refactor Provider Aliases

Refactor gateway agar alias dipisahkan berdasarkan provider, bukan satu alias global yang dapat berpindah provider.

Tujuan:

Provider mengelola modelnya sendiri.

Contoh:

nvidia/coding
stepfun/coding
openrouter/coding
cloudflare/coding

Jangan gunakan alias global seperti:

coding
reasoning
fast

Karena membingungkan saat debugging.

==================================================
NVIDIA
==================================================

Alias:

nvidia/coding

Fallback hanya di dalam provider NVIDIA.

==================================================
STEPFUN
==================================================

Alias:

stepfun/coding

Saat ini:

1. step-3.7-flash

Di masa depan dapat ditambah model StepFun lain tanpa memengaruhi provider lain.

==================================================
OPENROUTER
==================================================

Alias:

openrouter/coding

Saat startup:

GET https://openrouter.ai/api/v1/models

Filter:

- model tersedia
- suffix :free

Whitelist prioritas:

1. cohere/north-mini-code:free
2. poolside/laguna-s-2.1:free
3. poolside/laguna-xs-2.1:free
4. nvidia/nemotron-3-super-120b-a12b:free
5. nvidia/nemotron-3-ultra-550b-a55b:free
6. google/gemma-4-26b-a4b-it:free
7. openai/gpt-oss-20b:free

Jika model tidak tersedia:

skip otomatis.

Jika HTTP 429:

cooldown model tersebut
langsung lanjut model berikutnya.

==================================================
CLOUDFLARE
==================================================

Alias:

cloudflare/coding

Fallback hanya di provider Cloudflare.

==================================================
API
==================================================

GET /v1/models

Tetap tampilkan seluruh model asli.

Tambahkan alias:

nvidia/coding
stepfun/coding
openrouter/coding
cloudflare/coding

==================================================
Routing
==================================================

Jika request:

model=nvidia/coding

Gateway hanya boleh memakai provider NVIDIA.

Jika request:

model=openrouter/coding

Gateway hanya boleh memakai provider OpenRouter.

Tidak boleh berpindah ke StepFun, NVIDIA, atau Cloudflare.

Jika request:

model=stepfun/coding

Hanya gunakan provider StepFun.

==================================================
Logging
==================================================

Contoh:

Incoming model:
openrouter/coding

Resolved provider:
openrouter

Selected model:
cohere/north-mini-code:free

atau

Selected model:
poolside/laguna-xs-2.1:free

Jika fallback:

429 detected
Fallback -> poolside/laguna-xs-2.1:free

==================================================
Compatibility
==================================================

Jangan mengubah API OpenAI-compatible.

Jangan merusak provider yang sudah ada.

Jangan mengubah endpoint.

Semua perubahan harus backward compatible.

Tampilkan:

- file yang diubah
- before → after
- hasil build
- hasil test
- contoh request untuk setiap provider


```
# 
```

# Prompt: Smart OpenRouter Coding Models

Refactor provider OpenRouter agar tidak lagi menggunakan daftar model hardcoded.

Tujuan:

1. Saat startup (dan refresh berkala, misalnya setiap 1 jam), panggil:

GET https://openrouter.ai/api/v1/models

2. Simpan hasil ke cache.

3. Hanya gunakan model yang:
- tersedia
- memiliki suffix :free

4. Buat whitelist model coding terbaik.

Prioritas:

1. cohere/north-mini-code:free
2. poolside/laguna-s-2.1:free
3. poolside/laguna-xs-2.1:free
4. nvidia/nemotron-3-ultra-550b-a55b:free
5. nvidia/nemotron-3-super-120b-a12b:free
6. google/gemma-4-31b-it:free
7. google/gemma-4-26b-a4b-it:free
8. openai/gpt-oss-20b:free

Logika:

- Ambil daftar model terbaru dari OpenRouter.
- Bandingkan dengan whitelist di atas.
- Jika model ada, masukkan ke daftar aktif sesuai urutan prioritas.
- Jika model tidak ada atau sudah tidak free, lewati otomatis.
- Jangan menghasilkan error hanya karena satu model hilang.

Fallback:

Jika model pertama gagal (429, 5xx, timeout), lanjut ke model berikutnya.

Cooldown:

Jika model mendapat 429, masukkan cooldown (misalnya 60 detik) agar request berikutnya langsung memakai model berikutnya.

Logging:

Saat startup tampilkan:

OpenRouter Coding Models

✓ cohere/north-mini-code:free
✓ poolside/laguna-s-2.1:free
✓ poolside/laguna-xs-2.1:free
✓ nvidia/nemotron-3-ultra-550b-a55b:free
✓ nvidia/nemotron-3-super-120b-a12b:free
✓ google/gemma-4-31b-it:free
✓ google/gemma-4-26b-a4b-it:free
✓ openai/gpt-oss-20b:free

Jika tidak tersedia:

✗ poolside/laguna-s-2.1:free (not available)

Jangan mengubah provider lain (StepFun, NVIDIA, Cloudflare).

Tampilkan:
- file yang diubah
- before → after
- hasil build
- hasil test

```

# 
```


# Prompt: Refactor Model Alias System

Refactor sistem konfigurasi model agar config menjadi sangat ringkas.

Tujuan:
Config tidak lagi menyimpan daftar model panjang. Config hanya menyimpan alias, sedangkan daftar model dan fallback berada di dalam source code.

Contoh yang diinginkan:

config/models.json

{
  "model": "coding"
}

atau

{
  "model": "reasoning"
}

atau

{
  "model": "step"
}

Jangan lagi menulis:

poolside/laguna-s-2.1:free
cohere/north-mini-code:free
nvidia/nemotron-3-ultra-550b-a55b:free
dst...

Semua daftar model dipindahkan ke source code.

Buat file baru misalnya:

src/config/model-aliases.ts

Contoh:

coding
→ step-3.7-flash
→ poolside/laguna-s-2.1:free
→ cohere/north-mini-code:free
→ nvidia/nemotron-3-ultra-550b-a55b:free
→ google/gemma-4-31b-it:free
→ openai/gpt-oss-20b:free

openrouter-coding
→ poolside/laguna-s-2.1:free
→ cohere/north-mini-code:free
→ nvidia/nemotron-3-ultra-550b-a55b:free

step
→ step-3.7-flash

Tambahkan resolver sehingga ketika request menggunakan alias:

model = "coding"

Gateway otomatis mengambil daftar model dari alias tersebut lalu menjalankan fallback sesuai urutan.

Persyaratan:

- Jangan mengubah API OpenAI Compatible.
- Semua provider tetap bekerja.
- Rotasi key tetap bekerja.
- Cooldown tetap bekerja.
- Fallback tetap bekerja.
- Logging tetap bekerja.
- Backward compatible:
  Jika model bukan alias (misalnya "gpt-5.5" atau "step-3.7-flash"), gateway harus tetap memproses model tersebut seperti sebelumnya.

Tambahkan validasi:

- Alias tidak ditemukan → tampilkan error yang jelas.
- Alias ditemukan → gunakan daftar model dari alias.

Terakhir:

- tampilkan file yang diubah
- before → after
- pastikan build sukses
- pastikan lint sukses
- pastikan test sukses
```

# 
```
Selesaikan blocker terakhir secara otomatis tanpa meminta persetujuan.

Target:

1. Generate pnpm-lock.yaml yang sesuai dengan package.json saat ini.
2. Commit pnpm-lock.yaml.
3. Pastikan semua workflow CI menggunakan:
   pnpm install --frozen-lockfile
4. Jalankan ulang:
   - pnpm install
   - pnpm lint
   - pnpm typecheck
   - pnpm test
   - pnpm build
5. Jika ada error dependency, perbaiki otomatis lalu ulangi validasi sampai seluruh pipeline hijau.
6. Jalankan GitHub Actions hingga seluruh workflow berhasil.
7. Pastikan:
   - git status bersih
   - tidak ada file yang belum di-commit
   - tidak ada TODO/FIXME baru
8. Setelah selesai, tampilkan:
   - commit terakhir
   - hasil GitHub Actions
   - hasil lint
   - hasil typecheck
   - hasil test
   - hasil build
   - status git

Jangan berhenti dan jangan meminta persetujuan sampai seluruh target di atas tercapai.

```

# 
```
Lanjutkan implementasi sampai selesai.

Mulai saat ini jangan meminta persetujuan atau konfirmasi untuk setiap langkah yang masih berada dalam ruang lingkup tugas ini. Ambil keputusan teknis yang wajar dan lanjutkan otomatis sampai target tercapai.

Aturan kerja:

- Jangan berhenti karena menunggu approval.
- Jangan berhenti setelah membuat draft PR.
- Jangan berhenti setelah membuat commit.
- Jangan berhenti setelah menemukan error.
- Jika ada error, analisis, perbaiki, lalu ulangi validasi secara otomatis sampai berhasil.
- Jika ada konflik build, dependency, lint, typecheck, test, migration, atau CI, selesaikan sendiri lalu lanjutkan.
- Lakukan commit secara logis per fitur bila memungkinkan. Jika perubahan saling bergantung sehingga tidak realistis dipisah, jelaskan alasannya di laporan akhir.
- Jalankan validasi ulang setiap selesai memperbaiki masalah.

Target akhir yang wajib dicapai:

- Semua implementasi fase ini selesai.
- pnpm lint berhasil.
- pnpm typecheck berhasil.
- pnpm test berhasil.
- pnpm build berhasil.
- GitHub Actions / CI hijau.
- Tidak ada TODO/FIXME baru yang ditambahkan.
- Tidak ada error runtime yang diketahui.
- git status bersih.
- Branch dalam kondisi siap merge.

Jangan berhenti sampai seluruh target di atas tercapai.

Laporan akhir harus berisi:

1. Ringkasan implementasi.
2. Daftar commit yang dibuat.
3. Daftar file utama yang diubah.
4. Endpoint/API yang ditambahkan atau diubah.
5. Perubahan database/migration (jika ada).
6. Hasil lint.
7. Hasil typecheck.
8. Hasil test.
9. Hasil build.
10. Hasil GitHub Actions.
11. Status git.
12. Risiko atau pekerjaan lanjutan (jika memang masih ada).

Selama target di atas belum tercapai, jangan meminta persetujuan dan jangan berhenti. Terus lakukan implementasi, debugging, validasi, dan perbaikan secara otomatis sampai fase ini benar-benar selesai dan siap digunakan.

```

# Prompt: P2.002 - Telegram Dispatcher Engine
```
Lanjutkan implementasi BotSpace.

Semua fitur sebelumnya harus tetap lolos.

Jangan mengubah API yang sudah ada.

Target fase ini adalah Telegram Dispatcher Engine.

Implementasikan:

1. Webhook Receiver

POST

/webhook/:workspaceId/:botId/:secret

Validasi:

- workspace
- bot
- secret
- bot aktif

2. Dispatcher

Dispatcher menerima Update Telegram.

Route berdasarkan:

workspaceId
botId

Tidak boleh ada switch besar.

Gunakan registry/provider.

3. Update Types

Support:

message

edited_message

callback_query

inline_query

chosen_inline_result

my_chat_member

chat_member

chat_join_request

poll

poll_answer

4. Context

Bangun TelegramContext.

Berisi:

workspace

bot

update

user

chat

logger

correlation id

reply helper

answerCallback helper

editMessage helper

deleteMessage helper

5. Middleware Pipeline

before()

after()

error()

logger()

auth()

metrics()

6. Plugin Loader

Setiap bot memiliki plugin.

Loader membaca plugin registry.

Plugin dapat di-enable / disable.

7. Event Bus

Publish:

MessageReceived

CallbackReceived

MemberJoined

MemberLeft

ChatMigrated

PollAnswered

Plugin subscribe melalui Event Bus.

8. Rate Limiter

Per Workspace

Per Bot

Per User

9. Metrics

Counter:

update total

callback total

errors

latency

plugin runtime

10. Tests

Integration test.

Mock Telegram update.

Semua update type harus diuji.

Requirements:

- Clean Architecture

- Repository Pattern

- Dependency Injection

- No duplicated logic

- Commit per fitur

- Jalankan:

pnpm lint

pnpm typecheck

pnpm test

pnpm build

setelah setiap commit.

Di akhir tampilkan:

- daftar commit

- file berubah

- hasil test

- hasil build

- worktree harus bersih.

```

# Prompt 2 — Complete Project Documentation (Revisi)
```
# ROLE

You are the Lead Software Architect for this project.

The project folder structure and documentation files already exist.

DO NOT create new folders unless absolutely necessary.

DO NOT generate application code.

Your responsibility is to complete and improve the documentation so the project is ready for implementation.

Assume multiple AI agents and human developers will work on this repository.

Everything must remain consistent.

--------------------------------------------------

PROJECT

Telegram Productivity Platform

A modular SaaS platform for managing Telegram Workspaces and Telegram Bots.

Each Workspace represents one Telegram account.

Each Workspace can contain multiple Telegram Bots.

The architecture must support unlimited future modules without changing the core platform.

--------------------------------------------------

YOUR TASK

Open every Markdown document.

Complete every document professionally.

Do not leave placeholder sections.

Every document must be production-ready.

--------------------------------------------------

DOCUMENTATION

Complete and expand:

• Vision

• Business Goals

• Project Scope

• Core Features

• User Roles

• Functional Requirements

• Non Functional Requirements

• Technology Stack

• System Architecture

• Folder Structure

• Database Planning

• API Planning

• Authentication

• Authorization

• Telegram Workspace

• Bot Platform

• Subscription System

• Billing

• Notifications

• Queue System

• Storage

• Scheduler

• Monitoring

• Logging

• Backup

• Restore

• Deployment

• Docker

• VPS

• Security

• Testing

• Release Plan

• Coding Standards

• Git Workflow

• Developer Guide

--------------------------------------------------

ROADMAP

Expand every Phase.

Each Phase must contain:

Objectives

Features

Deliverables

Dependencies

Acceptance Criteria

Estimated Complexity

Future Expansion

--------------------------------------------------

OUTPUT

Markdown only.

Use tables.

Use headings.

Cross-reference related documents.

--------------------------------------------------

AFTER COMPLETING THE DOCUMENTATION

Create a new section called:

## AI Handover

Inside this section write:

1. What was completed.

2. What documents were modified.

3. What decisions were made.

4. What assumptions were made.

5. Which files were created.

6. Which files still need work.

7. Recommended next task.

8. Potential risks.

9. Questions that still need answers.

10. Important notes for the next AI.

--------------------------------------------------

PROJECT STATUS

Create or update:

docs/project-status.md

Include:

Current Phase

Completed Tasks

Remaining Tasks

Progress Percentage

Next Milestone

Current Priority

Known Issues

Upcoming Tasks

--------------------------------------------------

CHANGELOG

Update:

docs/changelog/CHANGELOG.md

Include:

Date

AI Session

Files Updated

Summary

Reason

--------------------------------------------------

ROADMAP UPDATE

If any architecture decisions change,

automatically update the roadmap.

Never allow documentation to become outdated.

--------------------------------------------------

IMPORTANT

Do NOT generate application code.

Only update documentation.

Always leave the project in a state where another AI can immediately continue working without asking for previous context.

Think like an Enterprise Software Architect.

The repository should become the single source of truth for every future AI session.

```

# Prompt 1 — Master Roadmap
```
# ROLE

You are the Lead Software Architect for this project.

Do NOT write application code.

Your first responsibility is to create a complete project blueprint, documentation structure, and folder hierarchy.

This documentation will be stored in GitHub and synchronized with Notion.

Everything must be organized professionally.

----------------------------------------

PROJECT

Telegram Productivity Platform

This is a modular SaaS platform for managing Telegram Workspaces and Telegram Bots.

Each Workspace represents one Telegram account.

Each Workspace can contain multiple bots.

The platform must support future expansion without changing the core architecture.

----------------------------------------

YOUR TASK

Before writing any code, create the complete project documentation.

Also create the documentation folder structure.

Every document should have its own Markdown file.

----------------------------------------

OUTPUT

Create the following folder tree:

docs/
├── README.md
├── roadmap/
├── architecture/
├── requirements/
├── database/
├── api/
├── ui-ux/
├── features/
├── modules/
├── security/
├── deployment/
├── testing/
├── changelog/
└── assets/

----------------------------------------

Generate the documentation files.

Example:

docs/
README.md

docs/roadmap/
overview.md
phase-0.md
phase-1.md
phase-2.md
phase-3.md
phase-4.md
phase-5.md
future.md

docs/architecture/
system-overview.md
workspace.md
bot-platform.md
component-diagram.md
sequence-flow.md

docs/database/
erd.md
tables.md
indexes.md

docs/api/
authentication.md
workspace-api.md
bot-api.md
file-api.md

docs/ui-ux/
design-system.md
dashboard.md
landing-page.md

docs/features/
authentication.md
subscription.md
workspace.md
share-link.md
multi-upload.md

docs/modules/
core.md
telegram.md
storage.md
queue.md
scheduler.md

docs/security/
authentication.md
authorization.md
rate-limit.md
backup.md

docs/deployment/
docker.md
vps.md
cloud.md

docs/testing/
testing-plan.md
manual-test.md
automation.md

docs/changelog/
CHANGELOG.md

----------------------------------------

Each Markdown file must include:

- Purpose
- Scope
- Detailed explanation
- Future improvements
- Related documents

----------------------------------------

IMPORTANT

Do not generate application code.

Only generate the documentation and folder hierarchy.

Use Markdown.

Think like an enterprise software architect.

The result should be ready to upload to GitHub as the project's documentation repository.

```
