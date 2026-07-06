# 07 — Dari Struktur Folder ke Contoh Kode Sederhana

Tanggal: 2026-07-06

Topik: Memahami contoh alur kode sederhana dari `main.py` ke `routes`, `services`, `utils`, `models`, dan `repositories`.

---

## 1. Gambaran sederhana

Pada sesi sebelumnya, kita belajar bahwa aplikasi sebaiknya dipisah berdasarkan tanggung jawab.

Struktur dasarnya:

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

Pada sesi ini, kita melihat bagaimana struktur itu bekerja jika dibuat menjadi contoh kode sederhana.

Contoh input:

```text
Tarik kabel 100 meter lokasi Sanur
```

Target output:

```text
Laporan berhasil disimpan:
Pekerjaan: Tarik kabel
Volume: 100 meter
Lokasi: Sanur
```

---

## 2. Alur besar kode

Alur kode dari awal sampai data disimpan:

```text
User input
-> main.py
-> routes.handle_telegram_message()
-> services.process_report()
-> utils.parse_report_text()
-> models.create_report()
-> repositories.save_report()
-> services membuat response
-> routes mengembalikan response
-> main.py menampilkan output
```

Setiap bagian punya tugas sendiri.

---

## 3. `main.py`

Tugas `main.py` hanya menjalankan aplikasi.

Dalam contoh sederhana, `main.py`:

1. punya pesan/input,
2. meneruskan pesan ke `routes`,
3. menerima response,
4. menampilkan hasil.

Contoh kode:

```python
from routes.telegram_routes import handle_telegram_message

message = "Tarik kabel 100 meter lokasi Sanur"

response = handle_telegram_message(message)

print(response)
```

Catatan penting:

`main.py` tidak memproses laporan langsung.

Tujuannya agar kode lebih rapi, mudah dikembangkan, mudah di-maintenance, dan lebih scalable.

---

## 4. Kenapa `main.py` tidak langsung memproses laporan?

Karena aplikasi ini dibuat berdasarkan pembagian tugas.

Kalau `main.py` ikut memproses laporan, maka `main.py` akan menjadi terlalu besar dan berantakan.

Masalah yang bisa muncul:

- rentan bug,
- susah maintenance,
- susah dikembangkan,
- susah dites,
- tidak scalable.

Prinsipnya:

```text
main.py cukup menjalankan aplikasi.
Proses utama diserahkan ke services.
```

---

## 5. `routes/telegram_routes.py`

Tugas `routes` adalah menerima laporan atau pesan dari luar.

Dalam contoh Telegram Bot:

```text
routes menerima laporan pekerjaan dari Telegram
```

Lalu routes meneruskan data ke `services`.

Contoh kode:

```python
from services.report_service import process_report

def handle_telegram_message(message):
    response = process_report(message)
    return response
```

Penjelasan:

`routes` tidak perlu tahu detail parsing, validasi, atau penyimpanan data.

Tugasnya hanya:

```text
terima pesan -> teruskan ke services -> kembalikan response
```

---

## 6. `services/report_service.py`

`services` adalah otak utama aplikasi.

Tugasnya memproses data yang diterima dari `routes`.

Dalam contoh ini, `services`:

1. menerima pesan dari `routes`,
2. memanggil `utils` untuk membantu parsing data,
3. memanggil `models` untuk membentuk struktur data,
4. memanggil `repositories` untuk menyimpan data,
5. membuat response untuk dikirim balik.

Contoh kode:

```python
from utils.text_parser import parse_report_text
from models.report_model import create_report
from repositories.sheets_repository import save_report

def process_report(message):
    parsed_data = parse_report_text(message)

    report = create_report(parsed_data)

    save_report(report)

    return (
        "Laporan berhasil disimpan:\n"
        f"Pekerjaan: {report['pekerjaan']}\n"
        f"Volume: {report['volume']} {report['satuan']}\n"
        f"Lokasi: {report['lokasi']}"
    )
```

Alur di service:

```text
message
-> parse_report_text()
-> create_report()
-> save_report()
-> response
```

---

## 7. `utils/text_parser.py`

`utils` berisi fungsi kecil yang membantu `services`.

Dalam contoh ini, `text_parser` membantu mengambil kata-kata tertentu dari pesan agar bisa menjadi struktur data.

Contoh kode sederhana:

```python
def parse_report_text(message):
    return {
        "pekerjaan": "Tarik kabel",
        "volume": 100,
        "satuan": "meter",
        "lokasi": "Sanur"
    }
```

Untuk sekarang parsing dibuat sederhana dulu.

Nanti, parsing bisa dibuat lebih pintar, misalnya:

- mengambil angka otomatis,
- membaca lokasi otomatis,
- membedakan pekerjaan tanam/tarik,
- membaca koordinat,
- mengenali format laporan dari Telegram.

---

## 8. `models/report_model.py`

`models` menentukan struktur data yang diinginkan dari awal.

Tujuannya agar data tidak berantakan.

Contoh struktur laporan:

```text
tanggal
nama
pekerjaan
volume
satuan
lokasi
status
```

Contoh kode:

```python
def create_report(parsed_data):
    return {
        "nama": "Andre",
        "tanggal": "2026-07-06",
        "pekerjaan": parsed_data["pekerjaan"],
        "volume": parsed_data["volume"],
        "satuan": parsed_data["satuan"],
        "lokasi": parsed_data["lokasi"],
        "status": "baru"
    }
```

Model membuat data punya bentuk standar sebelum disimpan.

---

## 9. `repositories/sheets_repository.py`

`repositories` bertugas menyimpan data yang sudah diproses oleh `services`.

Dalam contoh ini, repository menyimpan data ke Google Sheets.

Contoh kode simulasi:

```python
def save_report(report):
    print("Menyimpan laporan ke Google Sheets...")
    print(report)
```

Untuk sekarang belum benar-benar menulis ke Google Sheets.

Yang penting dipahami:

```text
Kode penyimpanan diletakkan di repositories.
```

Kalau nanti penyimpanan diganti dari Google Sheets ke SQLite/database, bagian yang paling banyak berubah adalah `repositories`.

---

## 10. Jika penyimpanan berubah

Kalau penyimpanan berubah dari Google Sheets ke SQLite/database, bagian yang paling banyak berubah adalah:

```text
repositories
```

Contoh:

Sebelumnya:

```text
repositories/sheets_repository.py
```

Nanti bisa berubah menjadi:

```text
repositories/sqlite_repository.py
```

Bagian lain seperti `routes`, `services`, `models`, dan `utils` kemungkinan tidak banyak berubah.

Inilah keuntungan memisahkan kode berdasarkan tanggung jawab.

---

## 11. Jika format pesan berubah

Jika format pesan Telegram berubah, bagian yang kemungkinan berubah adalah:

```text
utils/text_parser.py
services/report_service.py
```

Catatan koreksi:

Pada jawaban latihan, bagian yang disebut berubah adalah `models`.

Konsepnya mendekati, tetapi lebih tepat:

- Jika bentuk data akhir berubah, maka `models` berubah.
- Jika format kalimat/pesan Telegram berubah, maka `utils/text_parser.py` yang paling mungkin berubah.
- Jika aturan prosesnya berubah, maka `services` ikut berubah.

Contoh:

Format lama:

```text
Tarik kabel 100 meter lokasi Sanur
```

Format baru:

```text
Pekerjaan: Tarik kabel
Volume: 100 meter
Lokasi: Sanur
```

Yang perlu menyesuaikan cara membaca teks adalah `utils/text_parser.py`.

---

## 12. Jawaban latihan Sesi 6 yang sudah dirapikan

## 1. `main.py`

Tugas `main.py` hanya menjalankan aplikasi. `main.py` punya pesan untuk diteruskan ke `routes`, lalu menampilkan hasil response.

## 2. Kenapa `main.py` tidak memproses laporan?

Karena aplikasi dibuat berdasarkan pembagian tugas agar lebih mudah ditata, dikembangkan, dan di-maintenance. Jika `main.py` ikut melakukan proses, aplikasi akan lebih rentan bug dan tidak scalable.

## 3. `routes`

Tugas `routes` adalah menerima laporan pekerjaan dari Telegram untuk diteruskan ke bagian `services`.

## 4. `services`

Tugas `services` adalah melakukan proses data yang diterima dari `routes`. Dalam proses ini, `services` bisa memanggil `utils` untuk membantu processing data tersebut.

## 5. `utils`

`text_parser` di `utils` membantu mengambil kata-kata tertentu agar menjadi struktur data yang diinginkan dan dapat diproses oleh `services`.

## 6. `models`

Tugas `models` adalah menentukan dari awal struktur data yang diinginkan.

## 7. `repositories`

Tugas `repositories` adalah menyimpan data yang diberikan oleh `services` setelah proses selesai.

## 8. Jika penyimpanan berubah

Jika penyimpanan berubah, maka bagian `repositories` yang paling banyak berubah, sedangkan bagian lain kemungkinan tidak berubah banyak.

## 9. Jika format pesan berubah

Jika format pesan berubah, maka bagian yang paling mungkin berubah adalah `utils/text_parser.py`, dan kadang `services` jika aturan prosesnya ikut berubah.

Jika bentuk data akhir yang berubah, barulah `models` ikut berubah.

## 10. Diagram

```text
User input
-> main.py
-> routes.handle_telegram_message()
-> services.process_report()
-> utils.parse_report_text()
-> models.create_report()
-> repositories.save_report()
-> services membuat response
-> routes mengembalikan response
-> main.py menampilkan output
```

---

## 13. Koreksi dan penguatan penting

Jawaban sudah sangat baik dan alurnya sudah tepat.

Koreksi utamanya hanya pada nomor 9:

Jika format pesan Telegram berubah, yang paling mungkin berubah adalah:

```text
utils/text_parser.py
```

Bukan pertama-tama `models`.

`models` berubah jika struktur data akhir berubah.

Contoh:

Jika hanya format kalimat berubah:

```text
Tarik kabel 100 meter lokasi Sanur
```

menjadi:

```text
Pekerjaan: Tarik kabel, Volume: 100 meter, Lokasi: Sanur
```

maka yang berubah adalah parser.

Namun jika data laporan perlu field baru, misalnya:

```text
koordinat
foto
nama tim
```

maka `models` juga perlu berubah.

---

## 14. Kesimpulan sesi

Konsep struktur folder bukan hanya teori. Struktur itu bisa diterjemahkan menjadi alur kode nyata:

```text
main.py -> routes -> services -> utils/models -> repositories
```

Setiap bagian punya tanggung jawab:

```text
main.py      = menjalankan aplikasi
routes       = menerima input/request
services     = mengatur proses utama
utils        = membantu parsing/format
models       = membentuk struktur data
repositories = menyimpan data
```

Jika aplikasi dibuat seperti ini, perubahan lebih mudah dikendalikan.

Contoh:

- penyimpanan berubah -> ubah `repositories`,
- format pesan berubah -> ubah `utils/text_parser.py`,
- struktur data berubah -> ubah `models`,
- aturan proses berubah -> ubah `services`,
- sumber input berubah -> ubah `routes`.

---

## 15. Next step

Sesi berikutnya:

```text
Sesi 7 — Praktik Mini: Membuat Struktur Folder dan Menjalankan Contoh Kode
```

Target sesi berikutnya:

- Membuat folder contoh kecil.
- Menulis file `main.py`, `routes`, `services`, `models`, `utils`, dan `repositories`.
- Menjalankan contoh kode dengan Python.
- Melihat output nyata dari alur `main.py -> routes -> services -> repositories`.
