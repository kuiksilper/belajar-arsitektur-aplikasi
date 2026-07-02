# 02 — Latihan Input, Proses, Output

Tanggal: 2026-07-02

Topik: Menganalisis aplikasi pencatat material dengan pola Input -> Proses -> Output.

---

## Jawaban latihan

## 1. Input

Input adalah sesuatu yang ingin dicatat atau data yang dimasukkan ke aplikasi.

Contoh pada aplikasi pencatat material:

- Nama material
- Jumlah
- Jenis material
- Harga
- Tanggal transaksi
- Jenis transaksi, misalnya masuk atau keluar

Catatan penting:
Input biasanya punya properti. Misalnya material tidak hanya punya nama, tapi juga jumlah, harga, jenis, lokasi, dan keterangan.

---

## 2. Proses

Proses adalah bagian ketika aplikasi mengenali input, lalu menjalankan aturan yang sudah ditentukan.

Contoh:

Jika user memasukkan:

```text
Barang: Kabel
Jumlah: 10
Harga satuan: 1000
```

Maka aplikasi bisa memproses:

```text
Total = jumlah x harga satuan
Total = 10 x 1000
Total = 10000
```

Selain menghitung, proses juga bisa berupa:

- Memeriksa data kosong atau tidak
- Memastikan jumlah berupa angka
- Mengubah format data
- Menentukan transaksi masuk atau keluar
- Menyimpan data ke tempat penyimpanan

---

## 3. Output

Output adalah hasil yang diberikan aplikasi setelah proses selesai.

Contoh output:

- Menampilkan total perhitungan
- Menampilkan pesan sukses
- Menampilkan laporan stok
- Menampilkan data yang sudah dicatat

Contoh:

```text
Data berhasil dicatat.
Material: Kabel
Jumlah: 10
Total: 10000
```

---

## 4. Data disimpan

Aplikasi membutuhkan tempat penyimpanan karena aplikasi sendiri bukan rumah permanen untuk data.

Data yang sudah diolah bisa disimpan di database.

Bentuk database bisa bermacam-macam:

- File lokal, misalnya `.txt`, `.csv`, `.json`, atau Excel
- SQLite di komputer lokal
- Google Sheets
- Database cloud seperti PostgreSQL, MySQL, Supabase, Firebase, dan lain-lain

Intinya, database adalah tempat agar data bisa dibuka lagi nanti.

---

## 5. Frontend

Frontend adalah wajah utama aplikasi, yaitu tempat user memasukkan data dan melihat hasil.

Pada aplikasi pencatat material, frontend bisa berupa:

- Form di website
- Dashboard
- Bot Telegram
- Aplikasi Android
- File Excel yang diisi manual

Frontend juga sebaiknya memberi batasan input.

Contoh batasan:

- Jumlah harus angka
- Nama material tidak boleh kosong
- Tanggal harus format tanggal
- Jenis transaksi hanya boleh `masuk` atau `keluar`

Batasan ini penting agar data yang masuk lebih rapi dan tidak merusak proses di backend.

---

## 6. Google Sheets sebagai database

Google Sheets bisa dianggap sebagai salah satu bentuk database sederhana.

Fungsinya:

- Menyimpan data yang sudah diproses aplikasi
- Menampilkan data dalam bentuk tabel
- Memudahkan user membaca dan mengedit data
- Bisa menjadi sumber data untuk laporan

Namun Google Sheets bukan database khusus aplikasi skala besar. Untuk belajar dan aplikasi sederhana, Google Sheets sangat cocok karena mudah dilihat dan dipahami.

---

## 7. Diagram alur

Diagram dasar:

```text
User -> Frontend -> Backend -> Database -> Backend -> Output
```

Jika menggunakan Telegram Bot dan Google Sheets:

```text
User Telegram
-> Bot Telegram sebagai frontend
-> Backend / script bot
-> Google Sheets sebagai database
-> Backend / script bot
-> Bot Telegram mengirim output
-> User menerima balasan
```

---

## Koreksi dan pemahaman penting

Jawaban sudah benar secara konsep.

Poin yang paling penting:

1. Input bukan hanya data mentah, tetapi data yang punya properti.
2. Proses adalah aturan/logika aplikasi.
3. Output adalah hasil yang memang dirancang dari awal.
4. Database adalah tempat tinggal data agar tidak hilang.
5. Frontend bukan hanya tampilan, tapi juga pintu masuk data.
6. Google Sheets bisa dipakai sebagai database sederhana.
7. Diagram aplikasi harus menunjukkan arah gerak data.

---

## Kesimpulan sesi

Aplikasi bekerja dengan pola sederhana:

```text
Input -> Proses -> Output
```

Untuk aplikasi yang menyimpan data:

```text
Input -> Proses -> Database -> Output
```

Untuk aplikasi web atau bot:

```text
User -> Frontend -> Backend -> Database -> Backend -> Frontend -> User
```

Pemahaman ini adalah dasar sebelum masuk ke frontend, backend, database, API, dan arsitektur aplikasi yang lebih kompleks.
