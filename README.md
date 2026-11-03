# DAZX Account Generator API

REST API berbasis Vercel Functions untuk membuat data akun **demo/fiktif** dalam format JSON.

> Generator ini membuat UID dan kredensial acak untuk pengujian aplikasi. Hasilnya bukan akun Free Fire atau akun layanan pihak ketiga yang terdaftar, dan tidak dapat dipakai untuk login.

## Endpoint

Setelah deployment:

- `GET https://YOUR-PROJECT.vercel.app/v3/generate`
- `GET https://YOUR-PROJECT.vercel.app/v3/generate?count=3`
- `POST https://YOUR-PROJECT.vercel.app/v3/generate`

### Contoh POST

```bash
curl -X POST "https://YOUR-PROJECT.vercel.app/v3/generate" \
  -H "Content-Type: application/json" \
  -d '{"count":3}'
```

`count` opsional, bilangan bulat 1–10. Jika tidak dikirim, nilai default adalah 1.

## Contoh respons

```json
{
  "success": true,
  "api": "DAZX Account Generator",
  "version": "3.0.0",
  "request_id": "generated-request-id",
  "count": 1,
  "note": "Data akun demo/fiktif. Tidak terdaftar dan tidak dapat digunakan untuk login ke layanan pihak ketiga.",
  "results": [
    {
      "uid": "1234567890",
      "username": "NovaFox1234",
      "password": "randomGenerated",
      "created_at": "2026-11-03T00:00:00.000Z",
      "account_type": "demo"
    }
  ]
}
```

Nilai di atas merupakan ilustrasi struktur; respons aktual dibuat secara acak saat endpoint dipanggil.

## Deploy dari Android

1. Ekstrak ZIP ini.
2. Buat repository baru di GitHub.
3. Unggah seluruh isi folder project ke repository (bukan folder ZIP-nya).
4. Buka https://vercel.com/new dan login.
5. Import repository GitHub tersebut.
6. Tekan **Deploy**.
7. Setelah selesai, akses `/v3/generate` pada domain Vercel kamu.

## Menjalankan lokal

Perlu Node.js 18+ dan Vercel CLI.

```bash
npm install
npm install -g vercel
vercel dev
```

Buka `http://localhost:3000/v3/generate`.

## Struktur project

```text
dazx-account-generator-api/
├── api/
│   └── v3/
│       └── generate.js
├── package.json
├── vercel.json
└── README.md
```

## Kode status

- `200`: berhasil membuat data demo.
- `400`: nilai `count` tidak valid.
- `405`: method selain GET atau POST.
