# prompt-botspace






# 
```
API key StepFun sudah saya test langsung menggunakan curl ke endpoint resmi dan berhasil.

Tetapi jika request melewati nvidia-api, StepFun mengembalikan:

401
Incorrect API key provided

Artinya masalah ada di implementasi provider StepFun.

Audit seluruh provider StepFun dan periksa:

1. Cara membaca STEPFUN_API_KEY dari .env.
2. Pastikan process.env.STEPFUN_API_KEY terbaca.
3. Pastikan header Authorization dikirim persis seperti:

Authorization: Bearer <STEPFUN_API_KEY>

tanpa spasi tambahan, tanpa newline, tanpa trim yang salah.

4. Pastikan tidak menggunakan NVIDIA_API_KEY atau OPENROUTER_API_KEY secara tidak sengaja.

5. Tampilkan URL yang dipanggil.

Harus:

https://api.stepfun.ai/step_plan/v1/chat/completions

6. Tampilkan header request (masking API key).

Contoh:

Authorization: Bearer sk-xxxx...abcd

7. Audit apakah provider menggunakan axios/fetch yang benar.

8. Bandingkan request yang dikirim provider dengan request curl yang berhasil.

9. Jika ada perbedaan payload, header, atau endpoint, perbaiki.

10. Setelah selesai tampilkan:
- file yang diubah
- before → after
- hasil test menggunakan step-3.7-flash
```
# 
```
Audit seluruh project nvidia-api.

Saya ingin server API dapat diakses dari luar VPS.

1. Audit terlebih dahulu apakah server saat ini bind ke:
   - 127.0.0.1
   - localhost
   - 0.0.0.0

2. Jika masih menggunakan 127.0.0.1 atau localhost sebagai bind address, ubah menjadi:

0.0.0.0

3. Jangan mengubah host yang digunakan untuk outbound request ke provider (NVIDIA, Cloudflare, OpenRouter, StepFun). Yang diubah hanya host server Express/Fastify yang menerima request.

4. Cari seluruh hardcode berikut:
- 127.0.0.1
- localhost

Ubah hanya jika digunakan sebagai listening address server.

5. Tambahkan environment variable:

HOST=0.0.0.0
PORT=3000

Server harus membaca dari env:

host = process.env.HOST ?? "0.0.0.0"
port = process.env.PORT ?? 3000

6. Jangan merusak endpoint OpenAI-compatible.

7. Setelah selesai tampilkan:
- file yang diubah
- before → after
- hasil build
- hasil lint
- hasil test

Jika server ternyata sudah bind ke 0.0.0.0, jangan ubah apa pun dan jelaskan alasannya.
```
# 
```
Audit seluruh project nvidia-api.

Saat ini provider yang sudah ada:

- NVIDIA
- Cloudflare
- OpenRouter

Saya ingin menambahkan StepFun dan sekaligus mengganti identitas provider agar setiap provider tampil sebagai provider yang berbeda di OpenCode.

Target provider:

- nvidia
- nvidia-cloudflare
- nvidia-openrouter
- nvidia-stepfun

Jangan jadikan semuanya satu provider.

Masing-masing provider harus:

- memiliki providerId sendiri
- memiliki providerName sendiri
- muncul sebagai provider yang berbeda pada endpoint /v1/models
- bisa dipilih secara terpisah oleh client/OpenCode
- mempunyai konfigurasi .env masing-masing
- mempunyai file provider sendiri
- mempunyai routing sendiri
- mempunyai logging sendiri

Contoh:

Provider:
nvidia

Provider:
nvidia-cloudflare

Provider:
nvidia-openrouter

Provider:
nvidia-stepfun

Jangan mengubah format OpenAI-compatible API.

Pertahankan seluruh endpoint yang sudah ada.

Pisahkan seluruh konfigurasi agar provider benar-benar independen.

Contoh struktur:

src/providers/
    nvidia-provider.ts
    cloudflare-provider.ts
    openrouter-provider.ts
    stepfun-provider.ts

ProviderService hanya bertugas memilih provider berdasarkan model.

Endpoint /v1/models harus menampilkan provider masing-masing, misalnya:

{
  "id":"step-3.7-flash",
  "provider":"nvidia-stepfun"
}

{
  "id":"poolside/laguna-s-2.1:free",
  "provider":"nvidia-openrouter"
}

{
  "id":"llama-3.3-nemotron-super-49b-v1",
  "provider":"nvidia"
}

{
  "id":"deepseek-r1",
  "provider":"nvidia-cloudflare"
}

Pastikan seluruh provider tetap modular, tidak saling bergantung, tidak ada duplikasi kode, dan seluruh build, lint, serta typecheck berhasil.
```
