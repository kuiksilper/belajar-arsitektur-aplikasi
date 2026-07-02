# Log Belajar

Gunakan file ini untuk mencatat proses belajar harian/mingguan.

Format:

```markdown
## Tanggal: YYYY-MM-DD

Topik:

Yang dipelajari:

Contoh/praktik:

Hal yang mulai dipahami:

Hal yang masih bingung:

Next step:
```

---

## Tanggal: 2026-07-02 — Sesi 1

Topik:
Input -> Proses -> Output pada aplikasi pencatat material.

Yang dipelajari:
- Aplikasi menerima input, memproses data sesuai aturan, lalu menghasilkan output.
- Jika data perlu dipakai lagi, aplikasi menyimpannya ke database.
- Input punya properti, misalnya jumlah, jenis, harga, tanggal, dan keterangan.
- Frontend adalah tempat user memasukkan data dan melihat hasil.
- Backend adalah bagian yang menjalankan logika/aturan aplikasi.
- Google Sheets bisa digunakan sebagai database sederhana untuk aplikasi kecil atau tahap belajar.

Contoh/praktik:
- Menganalisis aplikasi pencatat material.
- Membuat diagram alur: `User -> Frontend -> Backend -> Database -> Backend -> Output`.

Hal yang mulai dipahami:
- Aplikasi tidak langsung “pintar”; aplikasi bekerja mengikuti aturan yang kita buat.
- Database adalah tempat tinggal data agar catatan tidak hilang.
- Frontend perlu membatasi input supaya data yang masuk lebih rapi.

Hal yang masih bingung:
- Belum ada catatan khusus. Akan dilihat saat masuk ke materi frontend, backend, database, dan API.

Next step:
- Pelajari perbedaan Frontend, Backend, dan Database.
- Baca materi berikutnya setelah dibuat: `01-fundamental/03-frontend-backend-database.md`.

---

## Tanggal: 2026-07-02 — Sesi 2

Topik:
Frontend, Backend, dan Database pada aplikasi laporan pekerjaan harian.

Yang dipelajari:
- Frontend adalah bagian aplikasi yang langsung digunakan user.
- Backend adalah otak aplikasi yang menjalankan aturan, validasi, dan proses data.
- Database adalah rumah/gudang data.
- Telegram bisa berperan sebagai frontend jika user mengirim laporan melalui chat bot.
- Google Sheets/database menyimpan data yang sudah diproses oleh backend.
- Validasi final sebaiknya tetap dilakukan di backend, bukan hanya di frontend.

Contoh/praktik:
- Menganalisis aplikasi laporan pekerjaan harian berbasis Telegram Bot.
- Membuat diagram: `User -> Frontend Telegram -> Backend/script bot -> Database -> Backend -> Frontend -> User`.

Hal yang mulai dipahami:
- Frontend, backend, dan database punya tugas yang berbeda.
- Backend bukan tempat menyimpan data, tetapi bagian yang memproses dan mengatur alur.
- Database bukan otak aplikasi, tetapi tempat menyimpan data.
- Output aplikasi tergantung desain alur kerja yang dibuat.

Hal yang masih bingung:
- Belum ada catatan khusus. Nanti akan diperdalam saat belajar request, response, API, dan database.

Next step:
- Pelajari Request dan Response: bagaimana frontend berbicara dengan backend.
- Materi berikutnya: `01-fundamental/04-request-response.md`.
