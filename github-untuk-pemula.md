# GitHub untuk Pemula

Dokumen ini untuk membantu memahami cara dokumentasi belajar ini disimpan di GitHub.

## Istilah penting

## 1. Repository / repo

Repo adalah folder project yang disimpan di GitHub.

Untuk dokumentasi ini, repo akan berisi file markdown seperti:

```text
README.md
00-roadmap.md
log-belajar.md
template-catatan-belajar.md
01-fundamental/
```

## 2. Git

Git adalah alat untuk mencatat perubahan file dari waktu ke waktu.

Contoh perubahan:
- Menambah catatan belajar baru.
- Mengubah roadmap.
- Menambah folder materi baru.

## 3. Commit

Commit adalah titik simpan perubahan.

Analogi:

```text
Commit = save point
```

Contoh pesan commit:

```text
docs: tambah roadmap belajar arsitektur aplikasi
```

## 4. Push

Push artinya mengirim commit dari komputer lokal ke GitHub.

```text
Komputer lokal -> GitHub
```

## 5. Pull

Pull artinya mengambil update dari GitHub ke komputer lokal.

```text
GitHub -> Komputer lokal
```

## Alur kerja sederhana

```text
Edit file -> git add -> git commit -> git push
```

Penjelasan:

1. Edit file dokumentasi.
2. `git add` memilih file yang mau disimpan.
3. `git commit` membuat save point.
4. `git push` mengirim ke GitHub.

## Command dasar

Cek status file:

```bash
git status
```

Tambah semua perubahan:

```bash
git add .
```

Buat commit:

```bash
git commit -m "docs: update catatan belajar"
```

Kirim ke GitHub:

```bash
git push
```

## Aturan sederhana untuk dokumentasi belajar

- Setiap selesai satu sesi belajar, update `log-belajar.md`.
- Setiap topik baru, buat file markdown baru.
- Commit dengan pesan pendek dan jelas.
- Jangan masukkan token/password/API key ke repo.
