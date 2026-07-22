













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
