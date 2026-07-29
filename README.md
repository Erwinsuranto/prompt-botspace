# prompt-botspace

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
