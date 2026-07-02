# 01 — Bagaimana Aplikasi Bekerja

## Ringkasan

Aplikasi adalah sistem yang menerima input, memproses input tersebut, lalu menghasilkan output. Jika datanya perlu dipakai lagi nanti, aplikasi akan menyimpannya ke file atau database.

Pola paling sederhana:

```text
Input -> Proses -> Output
```

Jika memakai penyimpanan:

```text
Input -> Proses -> Simpan Data -> Output
```

Jika aplikasi web:

```text
User/Browser -> Request -> Backend -> Database -> Backend -> Response -> Browser
```

---

## Contoh sederhana

Misalnya aplikasi menghitung total material.

Input:

```text
Jenis material: Kabel
Jumlah: 10
Harga satuan: 5000
```

Proses:

```text
Total = jumlah x harga satuan
Total = 10 x 5000
Total = 50000
```

Output:

```text
Total harga Kabel adalah 50000
```

---

## Bagian utama aplikasi

## 1. Frontend

Frontend adalah bagian yang dilihat dan dipakai user.

Contoh:
- Halaman web.
- Tombol.
- Form input.
- Dashboard.

Tugas frontend:
- Menampilkan data.
- Menerima input user.
- Mengirim input ke backend.

## 2. Backend

Backend adalah bagian yang memproses logika aplikasi.

Contoh tugas backend:
- Menerima data dari form.
- Mengecek apakah data valid.
- Menghitung total.
- Menyimpan ke database.
- Mengirim hasil kembali ke frontend.

## 3. Database

Database adalah tempat menyimpan data dengan struktur yang rapi.

Contoh data:
- Data user.
- Data transaksi.
- Data pekerjaan.
- Data material.

## 4. API

API adalah pintu komunikasi antar bagian aplikasi atau antar aplikasi.

Contoh:
- Frontend meminta data ke backend.
- Bot Telegram mengirim laporan ke server.
- Server mengirim data ke Google Sheets.

---

## Analogi sederhana

Bayangkan aplikasi seperti warung makan.

```text
Pembeli = User
Pelayan = Frontend
Dapur = Backend
Buku stok/kasir = Database
Pesanan = Request
Makanan yang dikirim = Response
```

Alurnya:

1. Pembeli pesan makanan ke pelayan.
2. Pelayan meneruskan pesanan ke dapur.
3. Dapur memproses pesanan.
4. Jika perlu, dapur cek stok bahan.
5. Makanan dikirim balik ke pembeli.

Itulah cara kerja aplikasi secara sederhana.

---

## Contoh arsitektur aplikasi sederhana

```text
[User]
  |
  v
[Frontend / Form]
  |
  v
[Backend / Logic]
  |
  v
[Database / File]
  |
  v
[Output / Laporan]
```

---

## Pertanyaan untuk memastikan paham

1. Apa bedanya input dan output?
2. Kenapa aplikasi perlu backend?
3. Kapan data perlu disimpan ke database?
4. Apa fungsi API?
5. Dalam aplikasi Telegram bot, bagian mana yang menjadi input?

---

## Latihan kecil

Buat catatan desain untuk aplikasi pencatat material sederhana.

Jawab:

1. Input apa saja yang dibutuhkan?
2. Proses apa yang dilakukan aplikasi?
3. Output apa yang dihasilkan?
4. Data apa yang harus disimpan?
5. Apakah aplikasi ini butuh frontend, backend, dan database?

Contoh jawaban awal:

```text
Input:
- Nama material
- Jumlah
- Jenis transaksi: masuk/keluar

Proses:
- Validasi jumlah tidak boleh kosong
- Hitung stok akhir

Output:
- Pesan sukses
- Laporan stok

Data disimpan:
- Tanggal
- Nama material
- Jumlah
- Jenis transaksi
```
