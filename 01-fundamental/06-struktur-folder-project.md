# 06 — Struktur Folder Project dan Pemisahan Tanggung Jawab

Tanggal: 2026-07-06

Topik: Memahami struktur folder project backend dan pembagian tugas antara `main.py`, `routes`, `services`, `repositories`, `models`, dan `utils`.

---

## 1. Gambaran sederhana

Saat aplikasi masih kecil, semua kode bisa saja ditaruh dalam satu file.

Contoh:

```text
bot.py
```

Isi file itu bisa mencakup:

- menerima pesan Telegram,
- membaca isi pesan,
- memvalidasi format laporan,
- mengambil nama/lokasi/volume,
- menyimpan data ke Google Sheets,
- mengirim balasan ke Telegram,
- menangani error,
- mencatat log.

Untuk latihan kecil, satu file masih bisa dipakai.

Namun, ketika aplikasi mulai berkembang, satu file besar akan sulit dirawat.

---

## 2. Kenapa satu file besar tidak bagus untuk dikembangkan?

Satu file besar bagus untuk awal belajar, tetapi tidak bagus untuk aplikasi yang ingin dikembangkan.

Masalahnya:

1. Terlalu banyak isi dalam satu tempat.
2. Rentan bug karena banyak bagian saling bercampur.
3. Sulit maintenance.
4. Sulit mencari bagian tertentu.
5. Sulit dites bagian per bagian.
6. Sulit menambah fitur baru tanpa merusak fitur lama.

Contoh:

Kalau semua kode ada di `bot.py`, lalu ada bug saat parsing laporan, kita harus mencari di file besar itu. Risiko salah mengubah bagian lain juga lebih tinggi.

---

## 3. Pemisahan tanggung jawab

Pemisahan tanggung jawab artinya setiap bagian kode punya tugas masing-masing.

Bahasa sederhananya:

```text
Jangan semua pekerjaan ditaruh di satu tempat.
Pisahkan sesuai tugasnya.
```

Contoh pembagian:

```text
main.py       = menjalankan aplikasi
routes        = menerima request/data dari luar
services      = memproses aturan utama aplikasi
repositories  = menyimpan/mengambil data
models        = bentuk/struktur data
utils         = fungsi bantuan kecil
```

---

## 4. Contoh struktur folder backend sederhana

Contoh struktur folder:

```text
app/
├── main.py
├── routes/
│   └── telegram_routes.py
├── services/
│   └── report_service.py
├── repositories/
│   └── sheets_repository.py
├── models/
│   └── report_model.py
└── utils/
    └── text_parser.py
```

Struktur ini membuat kode lebih mudah dibaca, diperbaiki, dan dikembangkan.

---

## 5. `main.py`

`main.py` adalah file utama untuk menjalankan aplikasi.

Fungsinya:

- menjadi pintu masuk aplikasi,
- menjalankan aplikasi,
- mengatur konfigurasi awal,
- mendaftarkan route/handler,
- mengatur parameter tertentu yang diperlukan saat aplikasi start.

Bahasa sederhana:

```text
main.py = saklar utama aplikasi
```

Catatan:

`main.py` sebaiknya tidak berisi semua logika aplikasi. Ia cukup menyiapkan dan menjalankan aplikasi.

---

## 6. `routes`

`routes` adalah bagian yang menerima request atau data dari luar.

Pada aplikasi web:

```text
routes menerima request dari browser/API
```

Pada Telegram Bot:

```text
routes menerima update/pesan dari Telegram
```

Tugas `routes`:

- menerima request/data,
- membaca data awal,
- meneruskan data ke `services`,
- mengirim response/balasan.

Bahasa sederhana:

```text
routes = resepsionis/loket depan
```

Routes tidak seharusnya memproses semua aturan utama aplikasi. Tugas utamanya hanya menerima dan meneruskan.

---

## 7. `services`

`services` adalah otak utama aplikasi.

Di bagian ini data yang diterima diproses sesuai aturan aplikasi.

Tugas `services`:

- menjalankan logika utama aplikasi,
- memvalidasi data,
- memanggil `models` untuk memastikan bentuk data rapi,
- memakai `utils` untuk bantuan kecil,
- memanggil `repositories` untuk menyimpan atau mengambil data,
- membuat hasil akhir/response.

Contoh pada Telegram Bot laporan kerja:

```text
report_service
-> cek format laporan
-> ambil pekerjaan, volume, lokasi
-> susun data laporan
-> minta repository menyimpan ke Google Sheets
-> buat pesan balasan
```

Bahasa sederhana:

```text
services = otak/proses utama aplikasi
```

---

## 8. `repositories`

`repositories` adalah bagian yang bertanggung jawab pada penyimpanan data.

Tugas `repositories`:

- menyimpan data,
- mengambil data,
- mengubah data,
- menghapus data,
- berkomunikasi dengan database, Google Sheets, Excel, atau tempat penyimpanan lain.

Contoh:

```text
repositories/sheets_repository.py
```

Fungsinya:

- konek ke Google Sheets,
- menambah baris baru,
- membaca isi sheet,
- update data di sheet.

Bahasa sederhana:

```text
repositories = petugas arsip/gudang data
```

Service cukup meminta:

```text
Tolong simpan laporan ini.
```

Repository yang mengurus cara menyimpannya.

---

## 9. `models`

`models` adalah tempat struktur atau bentuk data.

Tugas `models`:

- menentukan field apa saja yang dimiliki data,
- menjaga bentuk data tetap rapi,
- membantu validasi struktur data.

Contoh model laporan kerja:

```text
Report:
- tanggal
- nama
- pekerjaan
- volume
- satuan
- lokasi
- status
```

Bahasa sederhana:

```text
models = formulir standar data
```

Tanpa model, data yang diterima bisa berantakan karena tidak punya bentuk standar.

---

## 10. `utils`

`utils` adalah tempat fungsi bantuan kecil.

Tugas `utils`:

- membantu service,
- berisi fungsi kecil yang bisa dipakai ulang,
- tidak menyimpan logika utama aplikasi.

Contoh fungsi di `utils`:

- format tanggal,
- format angka/akuntansi,
- membersihkan teks,
- mengambil angka dari kalimat,
- mengubah huruf besar/kecil,
- parsing teks sederhana.

Bahasa sederhana:

```text
utils = alat bantu kecil
```

Contoh:

```text
utils/date_formatter.py
utils/text_parser.py
utils/currency_formatter.py
```

---

## 11. Alur backend Telegram Bot

Jika user mengirim laporan:

```text
Tarik kabel 100 meter lokasi Sanur
```

Alur backend yang rapi:

```text
Telegram API
-> routes/telegram_routes.py
-> services/report_service.py
-> utils/text_parser.py
-> models/report_model.py
-> repositories/sheets_repository.py
-> Google Sheets
```

Versi lebih sederhana:

```text
routes -> services -> repositories
```

Dengan bantuan:

```text
services -> models
services -> utils
```

---

## 12. Diagram lengkap

Diagram yang dirapikan:

```text
User
-> Frontend Telegram
-> Telegram API
-> routes
-> services
-> models/utils
-> repositories
-> Google Sheets
-> repositories
-> services
-> routes
-> Telegram API
-> Frontend Telegram
-> User
```

Versi inti:

```text
User -> Telegram API -> routes -> services -> repositories -> Google Sheets
```

---

## 13. Contoh pada dashboard WO

Konsep yang sama bisa dipakai pada dashboard WO.

Contoh struktur:

```text
app/
├── main.py
├── routes/
│   └── dashboard_routes.py
├── services/
│   └── wo_service.py
├── repositories/
│   └── excel_repository.py
├── models/
│   └── wo_model.py
└── utils/
    └── date_formatter.py
```

Pembagian tugas:

```text
routes/dashboard_routes.py
= menerima request dari browser dan filter user

services/wo_service.py
= memproses filter WO dan menghitung summary

repositories/excel_repository.py
= membaca data dari file Excel

models/wo_model.py
= menentukan bentuk data WO

utils/date_formatter.py
= membantu format tanggal
```

---

## 14. Jawaban latihan Sesi 5 yang sudah dirapikan

## 1. Satu file besar

Satu file besar bagus untuk belajar saja, tetapi tidak bagus untuk dikembangkan karena isinya terlalu banyak, rentan bug, dan susah maintenance.

## 2. `main.py`

`main.py` seperti konfigurasi utama atau pintu masuk aplikasi. Tugasnya menjalankan aplikasi dengan parameter tertentu dan menyiapkan bagian awal aplikasi.

## 3. `routes`

`routes` adalah bagian yang menerima request jika di aplikasi web, atau menerima data/pesan jika di aplikasi seperti Telegram Bot. Setelah menerima data, routes meneruskannya ke bagian `services`.

## 4. `services`

`services` adalah otak utama aplikasi. Di sini data yang diterima akan diproses, divalidasi, dibentuk melalui `models`, dan dibantu oleh fungsi kecil dari `utils`.

## 5. `repositories`

`repositories` adalah bagian yang bertanggung jawab untuk menyimpan, mengambil, mengubah, atau menghapus data dari tempat penyimpanan seperti Google Sheets, database, Excel, atau file lain.

## 6. `models`

`models` adalah tempat struktur data agar data yang diterima tidak berantakan.

## 7. `utils`

`utils` adalah tempat fungsi-fungsi kecil yang membantu `services`, seperti format tanggal, format akuntansi, membersihkan teks, atau mengambil angka dari kalimat.

## 8. Penerima pesan Telegram

Bagian `routes` menerima pesan Telegram untuk diteruskan ke bagian `services`.

## 9. Penyimpan ke Google Sheets

Bagian `repositories` akan menyimpan data ke Google Sheets.

## 10. Diagram

Diagram inti:

```text
routes -> services -> repositories
```

Diagram lengkap:

```text
User -> Telegram API -> routes -> services -> repositories -> Google Sheets
```

Dengan bantuan:

```text
services -> models
services -> utils
```

---

## 15. Koreksi dan penguatan penting

Jawaban sudah benar secara konsep.

Ada beberapa penguatan:

1. Nomor 5 sempat terlewat, yaitu `repositories`. Perannya adalah akses data/penyimpanan.
2. `services` boleh memakai `models` dan `utils`, tetapi `models` bukan selalu tempat validasi utama. `models` lebih tepat dipahami sebagai bentuk/struktur data. Validasi aturan biasanya ada di `services`, sedangkan validasi bentuk data bisa dibantu oleh `models`.
3. Diagram `routes > service a model b utils > repositories` konsepnya benar, tetapi lebih rapi jika ditulis:

```text
routes -> services -> repositories
services -> models
services -> utils
```

Karena `models` dan `utils` biasanya membantu `services`, bukan selalu menjadi jalur utama menuju `repositories`.

---

## 16. Kesimpulan sesi

Struktur folder membantu aplikasi tetap rapi saat berkembang.

Prinsip utama:

```text
main.py       = menjalankan aplikasi
routes        = menerima request/data
services      = logika utama aplikasi
repositories  = akses penyimpanan data
models        = struktur data
utils         = fungsi bantuan kecil
```

Alur inti backend:

```text
Request -> routes -> services -> repositories -> database/sheets
```

Dengan bantuan:

```text
services -> models
services -> utils
```

Pemahaman ini penting sebelum mulai belajar coding backend yang lebih nyata, karena struktur project menentukan apakah aplikasi mudah dikembangkan atau cepat berantakan.

---

## 17. Next step

Sesi berikutnya:

```text
Sesi 6 — Dari Struktur Folder ke Contoh Kode Sederhana
```

Target sesi berikutnya:

- Melihat contoh kode kecil berdasarkan struktur folder.
- Memahami alur data dari `routes` ke `services` lalu ke `repositories`.
- Membuat contoh sederhana tanpa framework besar.
- Mulai melihat bagaimana konsep arsitektur berubah menjadi kode.
