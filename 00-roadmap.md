# Roadmap Belajar Arsitektur Aplikasi

Roadmap ini dibuat bertahap: dari aplikasi sederhana, lalu naik ke aplikasi yang lebih realistis dan kompleks.

---

## Level 1 — Dasar Cara Aplikasi Bekerja

Target: paham aplikasi itu sebenarnya menerima input, memproses data, lalu menghasilkan output.

Topik:

1. Apa itu aplikasi?
2. Input, proses, output.
3. File, folder, dan struktur project.
4. Frontend, backend, database secara sederhana.
5. Request dan response.
6. API secara sederhana.

Latihan kecil:

- Buat program input nama lalu tampilkan hasil.
- Buat program hitung total belanja.
- Simpan data sederhana ke file `.txt` atau `.json`.

---

## Level 2 — Aplikasi Lokal Sederhana

Target: paham aplikasi yang berjalan di komputer sendiri.

Topik:

1. Script vs aplikasi.
2. Konfigurasi aplikasi.
3. Membaca dan menulis file.
4. Validasi input.
5. Error handling dasar.
6. Logging sederhana.

Latihan kecil:

- Program pencatat transaksi material.
- Program baca Excel lalu tampilkan summary.
- Program export hasil ke PDF/CSV.

---

## Level 3 — Aplikasi Web Dasar

Target: paham bagaimana browser bicara dengan server.

Topik:

1. HTTP: GET, POST, status code.
2. Route / endpoint.
3. HTML sebagai tampilan.
4. Form input.
5. Backend sederhana dengan Flask/FastAPI.
6. Template dan static files.

Latihan kecil:

- Dashboard sederhana dari data Excel.
- Form input data pekerjaan.
- Halaman filter data.

---

## Level 4 — Database

Target: paham penyimpanan data yang lebih rapi dari file biasa.

Topik:

1. Apa itu database?
2. Tabel, baris, kolom.
3. Primary key.
4. Relasi antar tabel.
5. Query dasar: SELECT, INSERT, UPDATE, DELETE.
6. SQLite untuk latihan lokal.

Latihan kecil:

- Simpan data material ke SQLite.
- Buat pencarian berdasarkan kode tiang.
- Buat laporan transaksi per tanggal.

---

## Level 5 — Arsitektur Backend yang Rapi

Target: paham pemisahan tanggung jawab dalam kode.

Topik:

1. Controller / route.
2. Service layer.
3. Repository / data access.
4. Model / schema.
5. Validasi data.
6. Struktur folder backend.

Contoh struktur:

```text
app/
├── main.py
├── routes/
├── services/
├── repositories/
├── models/
└── utils/
```

Latihan kecil:

- Refactor aplikasi input data menjadi route + service + repository.

---

## Level 6 — API dan Integrasi

Target: paham aplikasi yang terhubung dengan sistem lain.

Topik:

1. REST API.
2. JSON.
3. Authentication token.
4. Webhook.
5. Integrasi Telegram Bot.
6. Integrasi Google Sheets.

Latihan kecil:

- Bot Telegram menerima laporan.
- Data masuk ke Google Sheets.
- Backend membaca data dari API.

---

## Level 7 — Aplikasi Produksi Sederhana

Target: paham aplikasi yang siap dipakai lebih serius.

Topik:

1. Environment variable.
2. Config dev/prod.
3. Logging yang benar.
4. Backup data.
5. Error monitoring sederhana.
6. Deployment dasar.

Latihan kecil:

- Jalankan aplikasi sebagai service lokal.
- Buat backup otomatis database/file.
- Buat halaman health check.

---

## Level 8 — Arsitektur Kompleks

Target: mengenal pola aplikasi skala lebih besar.

Topik:

1. Monolith vs microservices.
2. Event-driven architecture.
3. Queue / background job.
4. Cache.
5. Load balancer.
6. Observability: logs, metrics, tracing.
7. Security dasar.

Latihan konsep:

- Gambar arsitektur sistem laporan kerja dari Telegram -> Backend -> Database -> Dashboard -> PDF.
- Tentukan bagian mana yang sinkron dan asynchronous.

---

## Cara Belajar Setiap Topik

Untuk setiap topik, jawab 5 hal ini:

1. Masalah apa yang diselesaikan?
2. Cara kerjanya bagaimana?
3. Contoh sederhananya apa?
4. Kapan dipakai?
5. Kesalahan umum apa yang harus dihindari?
