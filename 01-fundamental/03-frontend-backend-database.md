# 03 — Frontend, Backend, dan Database

Tanggal: 2026-07-02

Topik: Memahami perbedaan frontend, backend, dan database pada aplikasi laporan pekerjaan harian.

---

## 1. Gambaran sederhana

Aplikasi modern biasanya punya tiga bagian utama:

```text
Frontend -> Backend -> Database
```

Kalau dilihat dari sisi user, alurnya menjadi:

```text
User -> Frontend -> Backend -> Database -> Backend -> Frontend -> User
```

Tiga bagian ini punya tugas berbeda.

- Frontend: tempat user berinteraksi.
- Backend: tempat aturan/logika aplikasi berjalan.
- Database: tempat data disimpan.

---

## 2. Frontend

Frontend adalah wajah aplikasi, yaitu bagian yang langsung digunakan user.

Contoh frontend:

- Website
- Dashboard
- Form input
- Aplikasi Android
- Bot Telegram
- File Excel yang diisi user

Pada aplikasi laporan pekerjaan harian lewat Telegram, frontend-nya adalah Telegram atau chat bot Telegram, karena user memasukkan laporan lewat chat.

Tugas frontend:

1. Menerima input dari user.
2. Menampilkan informasi ke user.
3. Membuat input lebih mudah dan rapi.
4. Memberi batasan awal pada input jika memungkinkan.
5. Mengirim data ke backend.

Contoh input dari frontend Telegram:

```text
Laporan kerja: Tarik kabel 100 meter di lokasi A
```

---

## 3. Backend

Backend adalah otak aplikasi. Backend bekerja di belakang layar.

Tugas backend:

1. Menerima data dari frontend.
2. Membaca isi laporan.
3. Melakukan validasi.
4. Menjalankan aturan aplikasi.
5. Menghitung data jika diperlukan.
6. Mengubah format data agar rapi.
7. Menyimpan data ke database.
8. Mengirim hasil kembali ke frontend.

Contoh tugas backend pada laporan pekerjaan harian:

- Mengecek apakah format laporan benar.
- Mengecek apakah nama pekerja/lokasi/tanggal ada.
- Memisahkan data menjadi kolom-kolom.
- Menentukan jenis pekerjaan.
- Menyimpan data ke database.
- Mengirim balasan sukses atau error.

Backend bukan tempat menyimpan data utama. Backend memproses data, lalu meminta database menyimpan data tersebut.

---

## 4. Database

Database adalah tempat menyimpan data aplikasi.

Bahasa sederhananya:
Database adalah rumah/gudang data.

Tugas database:

1. Menyimpan data.
2. Mengambil data saat dibutuhkan.
3. Mengubah data.
4. Menghapus data.
5. Menjaga data tetap rapi dalam struktur tertentu.

Pada aplikasi laporan pekerjaan harian, database dapat menyimpan:

- Tanggal laporan
- Nama user
- Nama tim
- Jenis pekerjaan
- Lokasi
- Volume pekerjaan
- Keterangan
- Status validasi
- Waktu data masuk

Database bisa berupa:

- Google Sheets
- Excel
- SQLite
- PostgreSQL
- MySQL
- Supabase
- Firebase

Untuk tahap belajar dan aplikasi kecil, Google Sheets bisa dipakai sebagai database sederhana.

---

## 5. Kenapa validasi tidak cukup di frontend?

Validasi sebaiknya tetap dilakukan di backend, meskipun frontend juga boleh melakukan validasi awal.

Alasannya:

1. Frontend lebih mudah dilewati atau dimanipulasi.
2. Backend adalah pusat aturan aplikasi.
3. Data dari banyak sumber harus mengikuti aturan yang sama.
4. Backend lebih cocok untuk proses penting seperti keamanan, validasi final, dan penyimpanan data.
5. Jika ada proses sensitif seperti token, password, atau enkripsi, itu lebih aman dilakukan di backend.

Contoh:

Frontend bisa mengecek jumlah tidak boleh kosong.

Backend tetap harus mengecek ulang:

- Apakah jumlah benar-benar angka?
- Apakah user boleh mengirim laporan?
- Apakah format laporan sesuai?
- Apakah data boleh disimpan?

Prinsip penting:

```text
Frontend boleh membantu validasi.
Backend wajib melakukan validasi final.
```

---

## 6. Backend vs Database

Backend dan database sering terlihat dekat, tapi tugasnya berbeda.

Backend:

- Otak aplikasi.
- Mengatur alur kerja.
- Memproses data.
- Menjalankan aturan.
- Mengambil dan menyimpan data melalui database.

Database:

- Rumah/gudang data.
- Menyimpan data.
- Mengambil data saat diminta.
- Menjaga data dalam struktur tabel/koleksi/file.

Analogi:

```text
Backend = pegawai yang mengatur dan memproses dokumen
Database = lemari arsip tempat dokumen disimpan
```

---

## 7. Contoh diagram laporan kerja harian Telegram

Diagram dasar:

```text
User
-> Frontend Telegram
-> Backend / script bot
-> Database
-> Backend / script bot
-> Frontend Telegram
-> User
```

Versi dengan keterangan:

```text
User mengirim laporan
-> Bot Telegram menerima pesan
-> Script backend membaca dan memvalidasi laporan
-> Data disimpan ke Google Sheets/database
-> Script backend membuat balasan
-> Bot Telegram mengirim output
-> User menerima notifikasi
```

---

## 8. Jawaban latihan Sesi 2

## 1. Frontend

Frontend adalah Telegram itu sendiri. Chat ke bot merupakan frontend karena user memasukkan data lewat chat tersebut.

## 2. Backend

Backend memproses data dari frontend. Backend bisa menghitung, memvalidasi, membaca format laporan, menjalankan aturan, dan menentukan data boleh disimpan atau tidak.

## 3. Database

Database menyimpan data hasil proses backend. Data yang disimpan bisa berupa data yang sudah divalidasi, dihitung, disortir, atau dirapikan oleh backend.

## 4. Output

Output yang diterima user bisa bervariasi, tergantung desain aplikasi.

Contoh output:

- Menampilkan data yang berhasil disimpan.
- Menampilkan notifikasi bahwa data berhasil disimpan.
- Menampilkan pesan error jika data tidak valid.

## 5. Validasi

Validasi tidak cukup hanya di frontend karena backend adalah pusat aturan aplikasi. Backend lebih cocok melakukan validasi final, terutama untuk data penting dan keamanan.

Jika ada proses seperti token, password, atau enkripsi, proses tersebut lebih baik dilakukan di backend.

## 6. Backend vs Database

Backend adalah otak aplikasi. Backend mengatur alur, memproses data, dan menjalankan aturan.

Database adalah rumah/gudang data. Database menyimpan data yang sudah divalidasi atau diproses oleh backend.

## 7. Diagram

```text
User
-> Frontend Telegram
-> Backend / script bot
-> Database
-> Backend / script bot
-> Frontend Telegram
-> User
```

---

## Koreksi dan pemahaman penting

Jawaban sudah benar dan sudah lebih matang dari sesi pertama.

Poin penting yang perlu diingat:

1. Telegram bisa menjadi frontend jika user berinteraksi lewat Telegram.
2. Backend bukan hanya menerima data, tapi juga menjalankan aturan aplikasi.
3. Database menyimpan data, bukan menentukan semua aturan aplikasi.
4. Output tergantung desain aplikasi.
5. Validasi final harus di backend.
6. Backend dan database punya tanggung jawab yang berbeda.
7. Diagram aplikasi harus menunjukkan perjalanan data dari user sampai balik lagi ke user.

---

## Kesimpulan sesi

Frontend, backend, dan database adalah tiga bagian dasar aplikasi modern.

```text
Frontend = pintu masuk dan tampilan
Backend = otak/logika aplikasi
Database = rumah data
```

Alur lengkap:

```text
User -> Frontend -> Backend -> Database -> Backend -> Frontend -> User
```

Dengan memahami ini, kita bisa mulai membedah aplikasi apa pun menjadi bagian-bagian yang lebih jelas.
