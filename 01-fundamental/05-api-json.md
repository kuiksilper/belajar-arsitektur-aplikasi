# 05 — API dan JSON

Tanggal: 2026-07-06

Topik: Memahami API, endpoint, JSON, key-value, serta contoh alur Telegram Bot dan Google Sheets.

---

## 1. Gambaran sederhana

API adalah jalur komunikasi resmi antar aplikasi.

Bahasa sederhananya:

```text
API = pintu/loket resmi agar aplikasi bisa saling berbicara
```

Contoh pada Telegram Bot:

```text
Script Bot -> Telegram API -> Telegram -> User
```

Script bot tidak langsung masuk ke sistem Telegram. Script bot berkomunikasi dengan Telegram melalui API.

Contoh pada Google Sheets:

```text
Backend -> Google Sheets API -> Google Sheets
```

Backend tidak langsung membongkar Google Sheets. Backend memakai Google Sheets API untuk membaca atau menulis data.

---

## 2. API vs Database

API dan database punya peran berbeda.

```text
API      = jalur komunikasi
Database = tempat menyimpan data
```

API bukan tempat menyimpan data. API hanya menyediakan jalan resmi agar aplikasi bisa meminta, mengirim, membaca, atau mengubah data yang ada di sistem lain.

Contoh:

```text
Backend -> Google Sheets API -> Google Sheets
```

Pada alur itu:

- Google Sheets API adalah jalur komunikasi.
- Google Sheets adalah tempat data disimpan.

---

## 3. Endpoint

Endpoint adalah alamat tertentu di dalam API untuk menjalankan urusan tertentu.

Bahasa sederhananya:

```text
Endpoint = alamat loket untuk layanan tertentu
```

Contoh endpoint:

```text
/login
/reports
/materials
/users
```

Contoh penggunaan:

```text
POST /login
```

Artinya aplikasi mengirim data login ke endpoint `/login`.

```text
GET /reports
```

Artinya aplikasi meminta daftar laporan dari endpoint `/reports`.

Catatan koreksi:

API key bukan endpoint. API key adalah kunci/identitas akses. Endpoint adalah alamat tujuannya, misalnya `/login` atau `/reports`.

---

## 4. JSON

JSON adalah format data yang sering dipakai untuk request dan response lewat API.

Bahasa sederhananya:

```text
JSON = format penulisan data yang mudah dibaca manusia dan mudah diproses mesin
```

Contoh data biasa:

```text
Nama: Andre
Pekerjaan: Tarik kabel
Lokasi: Sanur
```

Dalam JSON:

```json
{
  "nama": "Andre",
  "pekerjaan": "Tarik kabel",
  "lokasi": "Sanur"
}
```

---

## 5. Key dan Value dalam JSON

Dalam JSON, data ditulis sebagai pasangan key dan value.

```json
{
  "nama": "Andre"
}
```

Penjelasan:

```text
"nama"   = key
"Andre" = value
```

Key adalah nama field.
Value adalah isi datanya.

Contoh lain:

```json
{
  "pekerjaan": "Tarik kabel",
  "volume": 100,
  "lokasi": "Sanur"
}
```

Key:

- pekerjaan
- volume
- lokasi

Value:

- Tarik kabel
- 100
- Sanur

Catatan koreksi:

Penulisan JSON harus rapi. Contoh yang benar:

```json
{
  "nama": "Andre"
}
```

Bukan:

```text
{ "Nama :" "Andre" }
```

Karena dalam JSON, setelah key harus ada tanda titik dua `:` di luar tanda kutip key.

---

## 6. Kenapa aplikasi sering memakai JSON?

Aplikasi sering memakai JSON karena:

1. Mudah dibaca manusia.
2. Mudah diproses mesin.
3. Ringkas.
4. Cocok untuk request dan response API.
5. Bisa dipakai di banyak bahasa pemrograman.
6. Bisa menyimpan data sederhana maupun daftar data.

Contoh JSON daftar material:

```json
{
  "materials": [
    {
      "nama": "Kabel",
      "jumlah": 10
    },
    {
      "nama": "Tiang",
      "jumlah": 2
    }
  ]
}
```

---

## 7. Telegram API

Dalam Telegram Bot, Telegram API berperan sebagai jalur komunikasi antara script bot dan Telegram.

Alur sederhananya:

```text
Script Bot -> Telegram API -> Telegram
Telegram -> Telegram API -> Script Bot
```

Contoh:

User mengirim pesan ke bot. Telegram mengirim update ke backend bot melalui API.

Contoh bentuk data mirip JSON:

```json
{
  "message": {
    "chat": {
      "id": -100123456
    },
    "from": {
      "id": 12345,
      "first_name": "Andre"
    },
    "text": "Tarik kabel 100 meter lokasi Sanur"
  }
}
```

Backend bot membaca isi pesan, memvalidasi, lalu membuat response.

---

## 8. Google Sheets API

Google Sheets API adalah jalur komunikasi yang memungkinkan backend mengakses dan mengubah isi Google Sheets sesuai data yang sudah diproses.

Contoh:

```text
Backend -> Google Sheets API -> Google Sheets
```

Jika backend ingin menambahkan laporan kerja ke Google Sheets, backend mengirim data seperti ini:

```json
{
  "values": [
    [
      "2026-07-06",
      "Andre",
      "Tarik kabel",
      "100 meter",
      "Sanur"
    ]
  ]
}
```

Google Sheets lalu menambahkan data itu sebagai baris baru.

---

## 9. Contoh JSON laporan kerja harian

Contoh JSON sederhana untuk laporan kerja harian:

```json
{
  "nama": "Andre",
  "tanggal": "2026-07-06",
  "pekerjaan": "Tarik kabel",
  "volume": 100,
  "satuan": "meter",
  "lokasi": "Sanur"
}
```

Data ini bisa dikirim dari frontend atau Telegram Bot ke backend, lalu backend memproses dan menyimpan ke Google Sheets/database.

---

## 10. Diagram alur Telegram Bot ke Google Sheets

Diagram yang dibuat:

```text
User -> Frontend Telegram -> Telegram API -> Backend -> Google Sheets API -> Google Sheets -> Google Sheets API -> Backend -> Telegram API -> Frontend Telegram -> User
```

Versi yang dirapikan:

```text
User
-> Frontend Telegram
-> Telegram API
-> Backend Bot
-> Google Sheets API
-> Google Sheets
-> Backend Bot
-> Telegram API
-> Frontend Telegram
-> User
```

Penjelasan:

1. User mengirim laporan melalui Telegram.
2. Telegram menjadi frontend yang menerima input user.
3. Telegram API meneruskan update ke backend bot.
4. Backend bot membaca, memvalidasi, dan memproses pesan.
5. Backend bot mengirim data ke Google Sheets API.
6. Google Sheets menyimpan data.
7. Backend bot membuat response.
8. Telegram API mengirim response ke Telegram.
9. User melihat balasan di Telegram.

---

## 11. Jawaban latihan Sesi 4 yang sudah dirapikan

## 1. API

API adalah jalur komunikasi antar aplikasi. Contohnya script bot Telegram berkomunikasi dengan Telegram melalui Telegram API.

## 2. API vs Database

API merupakan jalur komunikasi, sedangkan database adalah tempat menyimpan data. API tidak dipakai sebagai tempat penyimpanan data, tetapi sebagai jalan agar aplikasi bisa berkomunikasi dengan sistem lain.

## 3. Endpoint

Endpoint adalah alamat tertentu di API untuk fungsi tertentu, misalnya `/login`, `/reports`, atau `/materials`.

Catatan: API key bukan endpoint. API key adalah kunci akses, sedangkan endpoint adalah alamat tujuan API.

## 4. JSON

JSON adalah format data yang mudah dibaca manusia dan mudah diproses mesin. Data yang dikirim melalui API sering memakai format JSON agar bisa diproses lebih lanjut oleh backend.

## 5. Key dan Value

Dalam JSON, key adalah nama field, sedangkan value adalah isi datanya.

Contoh:

```json
{
  "nama": "Andre"
}
```

`nama` adalah key, sedangkan `Andre` adalah value.

## 6. Kenapa JSON

JSON sering dipakai karena formatnya mudah dibaca manusia dan mudah ditangani oleh mesin/aplikasi.

## 7. Telegram API

Telegram API berperan sebagai penghubung antara script bot dan Telegram.

## 8. Google Sheets API

Google Sheets API merupakan jalur komunikasi yang memungkinkan backend mengakses dan mengubah Google Sheets sesuai data yang telah diproses.

## 9. Contoh JSON

```json
{
  "nama": "Andre",
  "tanggal": "2026-07-06",
  "pekerjaan": "Tarik kabel",
  "volume": 100,
  "satuan": "meter",
  "lokasi": "Sanur"
}
```

Catatan tambahan untuk contoh daftar personel:

```json
{
  "personel": ["Andre", "Helman", "Bernad", "Darto"]
}
```

Jika setiap personel punya detail sendiri, bentuknya bisa seperti ini:

```json
{
  "personel": [
    {
      "nama": "Andre",
      "role": "leader"
    },
    {
      "nama": "Helman",
      "role": "anggota"
    }
  ]
}
```

## 10. Diagram

```text
User -> Frontend Telegram -> Telegram API -> Backend -> Google Sheets API -> Google Sheets -> Backend -> Telegram API -> Frontend Telegram -> User
```

---

## 12. Koreksi dan penguatan penting

Jawaban sudah benar secara konsep. Ada beberapa koreksi kecil:

1. Endpoint bukan API key. Endpoint adalah alamat seperti `/login`, `/reports`, atau `/materials`. API key adalah kunci akses.
2. JSON perlu format yang benar. Contoh yang benar adalah `{ "nama": "Andre" }`.
3. Google Sheets API bukan database. Google Sheets API adalah jalur komunikasi, sedangkan Google Sheets adalah tempat data tersimpan.
4. Diagram yang dibuat sudah benar. Hanya perlu dirapikan penulisannya agar lebih mudah dibaca.

---

## 13. Kesimpulan sesi

API adalah jalur komunikasi resmi antar aplikasi.

JSON adalah format data yang sering dipakai saat aplikasi mengirim request atau menerima response melalui API.

Endpoint adalah alamat tujuan di dalam API.

API berbeda dengan database:

```text
API      = jalur komunikasi
Database = tempat menyimpan data
```

Dalam aplikasi Telegram Bot dan Google Sheets, alurnya bisa dipahami seperti ini:

```text
User -> Telegram API -> Backend Bot -> Google Sheets API -> Google Sheets -> Backend Bot -> Telegram API -> User
```

Pemahaman API dan JSON penting sebelum masuk ke materi berikutnya: struktur folder project dan pemisahan tanggung jawab kode.

---

## 14. Next step

Sesi berikutnya:

```text
Sesi 5 — Struktur Folder Project dan Pemisahan Tanggung Jawab
```

Target sesi berikutnya:

- Memahami kenapa project perlu struktur folder.
- Memahami perbedaan file utama, folder routes, services, repositories, models, dan utils.
- Melihat contoh struktur backend sederhana.
- Mulai memahami kenapa kode tidak boleh ditaruh semua dalam satu file besar.
