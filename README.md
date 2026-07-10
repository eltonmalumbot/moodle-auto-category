# moodle-auto-category
Python automation script using Moodle Web Services API to create bulk course categories for multiple schools dynamically.

# Moodle Bulk Category Creator (Secure Version)

Script Python otomatisasi berbasis **Moodle Web Services API** yang digunakan untuk membuat struktur kategori (folder) baru secara massal untuk berbagai sekolah dalam sekali jalan. 

Versi ini telah **disensor dan diamankan** menggunakan *Environment Variables*, sehingga aman untuk di-publish ke GitHub tanpa risiko kebocoran data sensitif seperti Token API atau URL server sekolah.

## 🚀 Fitur Utama
* **Keamanan Data:** URL Moodle dan Token Web Services tidak ditulis keras (*hardcoded*) di dalam script.
* **Pembuatan Massal:** Otomatis mendistribusikan folder Tahun Ajaran Baru ke multi-sekolah berdasarkan ID induknya masing-masing.
* **Struktur Standar SMP:** Menghasilkan sub-kategori otomatis di dalam rumpun Tahun Ajaran baru secara rapi:
    * Tingkat Kelas: **Kelas 7, Kelas 8, dan Kelas 9**.
    * Paket Evaluasi: **PTS 1, PTS 2, PAS, PAT, dan Ujian Sekolah (US)**.

---

## 🛠️ Prasyarat (Prerequisites)

1.  **Python 3.x** terinstal di komputer.
2.  Library `requests` terinstal. Jika belum, jalankan perintah ini di terminal:
    ```bash
    pip install requests
    ```
3.  Akun Token Moodle yang memiliki hak akses (*permission*) untuk fungsi pengesahan kategori (`core_course_create_categories`).

---

## ⚙️ Cara Mengonfigurasi & Menjalankan Script

Script ini membaca data kredensial Moodle dari lingkungan sistem (*Environment Variables*). Anda bisa menjalankannya di terminal lokal Anda (VS Code / Git Bash) dengan cara berikut:

### 1. Jalankan via Terminal (Linux / macOS / Git Bash Windows)
Buka terminal Anda, deklarasikan variabel rahasia Anda, lalu eksekusi script-nya secara bersamaan:

```bash
export MOODLE_SERVER_URL="[https://link-moodle-sekolah-anda.sch.id](https://link-moodle-sekolah-anda.sch.id)"
export MOODLE_API_TOKEN="masukkan_token_api_moodle_disini"

python buat_kategori_massal.py
