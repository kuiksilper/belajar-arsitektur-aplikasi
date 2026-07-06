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

---

## Tanggal: 2026-07-04 — Sesi 3

Topik:
Request dan Response pada aplikasi laporan kerja Telegram.

Yang dipelajari:
- Request adalah permintaan dari frontend/user ke backend.
- Response adalah jawaban dari backend ke frontend/user.
- Request bisa dipakai untuk mengambil data atau mengirim data baru.
- Response bisa sukses atau gagal/error.
- Pesan user di Telegram bisa dianggap sebagai request.
- Backend memvalidasi request sebelum menyimpan data atau mengirim response.
- GET digunakan untuk mengambil data.
- POST digunakan untuk mengirim data baru agar diproses/disimpan.

Contoh/praktik:
- Menganalisis request-response pada aplikasi laporan pekerjaan harian via Telegram.
- Membuat diagram: `User -> Frontend Telegram -> Request -> Backend/script bot -> Database -> Backend -> Response -> Frontend Telegram -> User`.

Hal yang mulai dipahami:
- Frontend dan backend berkomunikasi melalui request dan response.
- Backend tidak boleh langsung percaya pada request; backend harus validasi dulu.
- Frontend sebaiknya tidak langsung menulis ke database karena alasan keamanan, aturan aplikasi, dan kerapian data.
- Response aplikasi tergantung desain: bisa pesan sukses, data hasil proses, atau pesan error.

Hal yang masih bingung:
- Belum ada catatan khusus. Nanti akan diperdalam saat belajar API dan JSON.

Next step:
- Pelajari API dan JSON sebagai bentuk request-response yang lebih resmi dan terstruktur.
- Materi berikutnya: `01-fundamental/05-api-json.md`.

---

## Tanggal: 2026-07-06 — Sesi 4

Topik:
API dan JSON pada Telegram Bot dan Google Sheets.

Yang dipelajari:
- API adalah jalur komunikasi antar aplikasi.
- API berbeda dengan database.
- Database adalah tempat menyimpan data, sedangkan API adalah jalur komunikasi untuk mengakses atau mengubah data melalui sistem lain.
- Endpoint adalah alamat tertentu di dalam API, misalnya `/login`, `/reports`, atau `/materials`.
- API key bukan endpoint; API key adalah kunci akses.
- JSON adalah format data yang mudah dibaca manusia dan mudah diproses mesin.
- Dalam JSON, key adalah nama field dan value adalah isi datanya.
- Telegram API menghubungkan script bot dengan Telegram.
- Google Sheets API menghubungkan backend dengan Google Sheets.

Contoh/praktik:
- Membuat contoh JSON sederhana untuk laporan kerja harian.
- Membuat diagram alur Telegram Bot yang menyimpan laporan ke Google Sheets.
- Merapikan diagram: `User -> Frontend Telegram -> Telegram API -> Backend -> Google Sheets API -> Google Sheets -> Backend -> Telegram API -> Frontend Telegram -> User`.

Hal yang mulai dipahami:
- API bukan tempat penyimpanan data.
- API adalah jalan resmi agar aplikasi dapat berkomunikasi dengan aplikasi lain.
- JSON dipakai agar data yang dikirim lewat API punya struktur yang jelas.
- Telegram Bot dan Google Sheets tidak diakses sembarangan, tetapi melalui API masing-masing.

Hal yang masih bingung:
- Belum ada catatan khusus. Nanti akan diperdalam saat mulai membahas struktur project dan pemisahan bagian kode.

Next step:
- Pelajari struktur folder project dan pemisahan tanggung jawab kode.
- Materi berikutnya: `01-fundamental/06-struktur-folder-project.md`.

---

## Tanggal: 2026-07-06 — Sesi 5

Topik:
Struktur folder project dan pemisahan tanggung jawab kode.

Yang dipelajari:
- Satu file besar cocok untuk belajar awal, tetapi tidak ideal untuk aplikasi yang akan dikembangkan.
- `main.py` adalah pintu masuk untuk menjalankan aplikasi dan menyiapkan konfigurasi awal.
- `routes` menerima request/data dari luar dan meneruskannya ke `services`.
- `services` adalah otak utama aplikasi yang memproses aturan, validasi, dan alur kerja.
- `repositories` bertanggung jawab pada penyimpanan dan pengambilan data dari Google Sheets, database, Excel, atau file lain.
- `models` menjaga bentuk/struktur data agar rapi.
- `utils` berisi fungsi bantuan kecil seperti format tanggal, format angka, atau parsing teks.

Contoh/praktik:
- Menganalisis struktur backend Telegram Bot laporan kerja.
- Membuat diagram inti: `routes -> services -> repositories`.
- Menambahkan bantuan: `services -> models` dan `services -> utils`.

Hal yang mulai dipahami:
- Kode perlu dipisah berdasarkan tugas agar tidak berantakan.
- `routes` bukan tempat logika utama; `routes` hanya menerima dan meneruskan request.
- `services` mengatur proses utama dan boleh memakai bantuan dari `models` dan `utils`.
- `repositories` adalah bagian yang menyimpan data ke Google Sheets/database.

Hal yang masih bingung:
- Belum ada catatan khusus. Nanti akan diperdalam saat melihat contoh kode sederhana.

Next step:
- Pelajari contoh kode sederhana berdasarkan struktur folder.
- Materi berikutnya: `01-fundamental/07-contoh-kode-struktur-folder.md`.
