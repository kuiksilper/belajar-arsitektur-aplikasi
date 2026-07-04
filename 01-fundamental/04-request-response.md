# 04 — Request dan Response

Tanggal: 2026-07-04

Topik: Memahami cara frontend berbicara dengan backend melalui request dan response.

---

## 1. Gambaran sederhana

Request dan response adalah pola komunikasi dasar dalam aplikasi.

Bahasa sederhananya:

```text
Request = permintaan
Response = jawaban
```

Contoh sehari-hari:

```text
Pembeli: Saya pesan nasi goreng satu.  -> request
Pelayan: Baik, tunggu sebentar.        -> response
```

Dalam aplikasi:

```text
Frontend -> Request -> Backend
Frontend <- Response <- Backend
```

Atau alur lengkapnya:

```text
User -> Frontend -> Request -> Backend -> Database -> Backend -> Response -> Frontend -> User
```

---

## 2. Request

Request adalah input atau permintaan yang dikirim dari user/frontend ke backend.

Request bisa bertujuan untuk:

- Mengambil data
- Menambah data
- Mengubah data
- Menghapus data
- Meminta aplikasi menjalankan proses tertentu

Contoh request pada aplikasi pencatat material:

```text
Simpan material masuk Kabel jumlah 10
```

Contoh request pada aplikasi laporan kerja Telegram:

```text
Laporan: Tarik kabel 100 meter lokasi Sanur
```

---

## 3. Response

Response adalah jawaban dari backend setelah menerima dan memproses request.

Response bisa berupa:

- Pesan sukses
- Pesan gagal/error
- Data hasil pencarian
- Hasil perhitungan
- Instruksi lanjutan
- Informasi bahwa user tidak punya izin

Contoh response sukses:

```text
Laporan berhasil disimpan.
Pekerjaan: Tarik kabel
Volume: 100 meter
Lokasi: Sanur
```

Contoh response gagal:

```text
Format laporan belum benar. Mohon isi jenis pekerjaan, volume, dan lokasi.
```

---

## 4. Isi request

Request biasanya membawa data yang diperlukan backend.

Pada aplikasi Telegram Bot, isi request bisa berupa:

- Teks pesan
- User ID
- Nama user
- Chat ID atau grup asal
- Waktu pesan
- Foto atau dokumen jika ada
- Lokasi jika user mengirim koordinat
- Perintah tertentu, misalnya `/start` atau `/laporan`

Contoh:

```text
User ID: 12345
Nama user: Andre
Chat ID: -100xxxx
Waktu: 2026-07-04 09:00
Pesan: Laporan tarik kabel 100 meter lokasi Sanur
```

---

## 5. Proses backend sebelum response

Sebelum backend mengirim response, backend biasanya melakukan beberapa proses:

1. Menerima request.
2. Membaca isi request.
3. Mengecek siapa pengirimnya.
4. Mengecek format data.
5. Melakukan validasi.
6. Menghitung atau mengubah data jika perlu.
7. Menyimpan data ke database jika valid.
8. Membuat response sesuai hasil proses.
9. Mengirim response kembali ke frontend/user.

Contoh:

Jika user mengirim:

```text
Laporan tarik kabel 100 meter lokasi Sanur
```

Backend bisa memproses:

```text
Jenis pekerjaan = tarik kabel
Volume = 100 meter
Lokasi = Sanur
Status validasi = valid
Aksi = simpan ke database
```

Lalu backend mengirim response:

```text
Laporan berhasil dicatat.
```

---

## 6. GET dan POST

Dalam aplikasi web, request biasanya memakai method.

Untuk awal, cukup pahami dua method ini:

## GET

GET digunakan untuk mengambil data.

Contoh:

```text
GET /laporan
```

Artinya:

```text
Tolong ambil daftar laporan.
```

## POST

POST digunakan untuk mengirim data baru ke backend agar diproses. Sering dipakai untuk menyimpan data baru.

Contoh:

```text
POST /laporan
```

Dengan data:

```json
{
  "jenis_pekerjaan": "Tarik kabel",
  "volume": 100,
  "lokasi": "Sanur"
}
```

Artinya:

```text
Tolong proses dan simpan laporan baru ini.
```

Ringkasan:

```text
GET  = mengambil data
POST = mengirim data baru untuk diproses/disimpan
```

---

## 7. Status sukses dan gagal

Response tidak selalu sukses. Backend bisa menjawab sukses atau gagal.

Contoh sukses:

```text
200 OK
Data berhasil diambil.
```

```text
201 Created
Laporan baru berhasil dibuat.
```

Contoh gagal:

```text
400 Bad Request
Format laporan salah.
```

```text
401 Unauthorized
User belum login atau token salah.
```

```text
403 Forbidden
User tidak punya izin.
```

```text
404 Not Found
Data tidak ditemukan.
```

```text
500 Internal Server Error
Backend mengalami error.
```

---

## 8. Kenapa frontend tidak langsung ke database?

Frontend sebaiknya tidak langsung menulis ke database karena:

1. Lebih berisiko dari sisi keamanan.
2. Aturan aplikasi bisa dilewati.
3. Validasi bisa tidak konsisten.
4. User bisa mengirim data sembarangan.
5. Izin akses lebih sulit dikontrol.
6. Struktur database bisa terekspos.
7. Lebih sulit menjaga data tetap rapi.

Pola yang lebih aman:

```text
Frontend -> Backend -> Database
```

Bukan:

```text
Frontend -> Database
```

Prinsip penting:

```text
Frontend adalah pintu masuk.
Backend adalah penjaga aturan.
Database adalah tempat penyimpanan.
```

---

## 9. Contoh Telegram Bot laporan kerja

Alur request-response:

```text
User
-> Frontend Telegram
-> Request berupa pesan laporan
-> Backend / script bot
-> Database / Google Sheets
-> Backend / script bot
-> Response berupa pesan sukses/gagal
-> Frontend Telegram
-> User
```

Versi dengan keterangan:

```text
User mengirim laporan kerja
-> Telegram menerima pesan
-> Telegram mengirim update ke script bot
-> Script bot membaca pesan
-> Script bot validasi format laporan
-> Script bot menyimpan data ke Google Sheets/database
-> Script bot membuat pesan balasan
-> Telegram menampilkan balasan ke user
```

---

## 10. Jawaban latihan Sesi 3

## 1. Request

Request adalah input atau permintaan yang dikirim user melalui frontend, baik untuk mengambil data maupun menambahkan data.

## 2. Response

Response adalah jawaban dari backend sesuai request/input dari user.

## 3. Request di Telegram

Pesan user di Telegram merupakan request. Request tersebut biasanya diproses berdasarkan aturan yang dibuat dalam script bot. Pesan bisa berupa permintaan data atau input data baru.

## 4. Isi request

Isi request adalah data yang diatur dan dibutuhkan oleh script bot, misalnya:

- Waktu pesan
- Siapa pengirimnya
- Apa isi laporannya
- Berapa jumlah/volume pekerjaannya
- Bagaimana format laporannya
- Chat ID/grup asal
- Foto/dokumen jika ada

## 5. Proses backend

Backend menangani proses di belakang layar, seperti validasi, perhitungan, manipulasi data input, penyimpanan ke database, dan membuat response atas request yang dikirim.

## 6. Response sukses

Response sukses terjadi ketika input user valid sesuai aturan backend. Data akan diproses, lalu aplikasi bisa menampilkan pesan sukses atau menampilkan data yang berhasil diproses, tergantung desain aplikasi.

Contoh:

```text
Laporan berhasil disimpan.
```

## 7. Response gagal

Response gagal terjadi ketika user memasukkan data yang tidak sesuai format atau aturan backend. Data tidak diproses atau tidak disimpan, lalu aplikasi menampilkan pesan gagal/error sesuai desain aplikasi.

Contoh:

```text
Format laporan salah. Mohon isi jenis pekerjaan, volume, dan lokasi.
```

## 8. GET vs POST

GET digunakan untuk mengambil data yang sudah ada.

POST digunakan untuk mengirim data baru ke backend agar diproses, dan sering dipakai untuk menyimpan data ke database.

## 9. Frontend tidak langsung ke database

Frontend sebaiknya tidak langsung ke database karena alasan keamanan. Selain itu, jika frontend langsung menulis ke database, aturan backend bisa dilewati dan data lebih mudah menjadi tidak rapi.

## 10. Diagram

```text
User
-> Frontend Telegram
-> Request
-> Backend / script bot
-> Database
-> Backend / script bot
-> Response
-> Frontend Telegram
-> User
```

---

## Koreksi dan pemahaman penting

Jawaban sudah benar secara konsep.

Poin yang perlu diingat:

1. Request bukan hanya input data baru, tapi juga bisa permintaan mengambil data.
2. Response bukan selalu sukses; response bisa sukses atau gagal.
3. Pesan Telegram bisa dianggap request karena user mengirim permintaan melalui frontend Telegram.
4. Backend perlu memvalidasi request sebelum menyimpan data.
5. GET untuk mengambil data.
6. POST untuk mengirim data baru agar diproses/disimpan.
7. Frontend tidak langsung ke database bukan hanya karena keamanan, tapi juga agar aturan aplikasi tetap terpusat di backend.

---

## Kesimpulan sesi

Request dan response adalah cara frontend dan backend berkomunikasi.

```text
Request = permintaan dari frontend/user ke backend
Response = jawaban dari backend ke frontend/user
```

Alur utama:

```text
User -> Frontend -> Request -> Backend -> Database -> Backend -> Response -> Frontend -> User
```

Pemahaman ini penting sebelum masuk ke materi API dan JSON, karena API pada dasarnya adalah jalur resmi untuk request dan response antar sistem.
