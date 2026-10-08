# 🎓 Aplikasi Laporan Penilaian Sumatif Tengah Semester (PSTS)
> **SMP PGRI 1 Kuwarasan** — System e-Rapot Online Berbasis Google Apps Script & GitHub Pages.

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Google Apps Script](https://img.shields.io/badge/Backend-Google%20Apps%20Script-green.svg)
![TailwindCSS](https://img.shields.io/badge/Frontend-TailwindCSS%203.0-06B6D4.svg)
![Status](https://img.shields.io/badge/Status-Production-brightgreen.svg)

Aplikasi web modern, ringan, dan responsif untuk menampilkan **Laporan Hasil Belajar Penilaian Sumatif Tengah Semester (PSTS)** siswa secara instan melalui Nomor Induk Siswa (NIS). Sistem ini terintegrasi langsung dengan database Google Sheets dan dilengkapi dengan analisis kinerja belajar siswa secara otomatis.

---

## 🌟 Fitur Utama

- 🔍 **Pencarian Cepat Berbasis NIS**: Siswa/Orang tua cukup memasukkan NIS untuk melihat hasil belajar.
- 📜 **Format PDF Resmi 1:1**: Tampilan KOP sekolah, data siswa, dan tabel nilai disesuaikan dengan format cetak fisik A4 resmi sekolah.
- 🔤 **Dukungan Terbilang Otomatis**: Membaca nilai angka sekaligus teks terbilang (huruf) dari spreadsheet atau menggenerasinya secara otomatis.
- 📊 **Catatan Evaluasi & Deskripsi Otomatis**:
  - Mengidentifikasi mata pelajaran unggulan (Kelebihan).
  - Mendeteksi mata pelajaran di bawah **KKTP (70)** secara presisi.
  - Memberikan rekomendasi tindakan siswa serta saran sinergi orang tua & guru secara dinamis.
- 🖨️ **Siap Cetak / Export PDF**: Aturan `@media print` khusus memastikan rapot muat rapi dalam **1 halaman A4**.

---

## 🏗️ Arsitektur Sistem


```

[ Google Sheets (Database) ]
│
▼
[ Google Apps Script (REST API / doGet) ]
│ (JSON)
▼
[ Web Frontend (HTML5 + Tailwind CSS) ] ──► GitHub Pages

```

---

## 📑 Format Struktur Google Sheets

Agar skrip dapat membaca data nilai dengan akurat, susun header kolom pada Google Sheets Anda seperti berikut:

| NIS | Nama | Kelas | Pai | Terbilang Pai | Pp | Terbilang Pp | B. Indo | Terbilang Bindo | Mat | Terbilang Mat | ... | Walas |
| :--- | :--- | :---: | :---: | :--- | :---: | :--- | :---: | :--- | :---: | :--- | :---: | :--- |
| 1234 | ADITYA PUTRA | 9A | 82 | Delapan Puluh Dua | 75 | Tujuh Puluh Lima | 83 | Delapan Puluh Tiga | 70 | Tujuh Puluh | ... | Catur P, S.Pd. |

* **Aturan Penting**:
  1. Pastikan kolom `NIS` dan `Nama` selalu ada.
  2. Kolom terbilang diberi nama dengan awalan `Terbilang` (contoh: `Terbilang Pai`, `Terbilang Mat`). Skrip akan otomatis memasangkannya dengan kolom mapel di sebelah kirinya.
  3. Setiap *sheet* (tab) dapat dinamai sesuai nama kelas (contoh: `7A`, `8B`, `9A`).

---

## 🚀 Tutorial Memasang & Menjalankan Proyek

Berikut adalah langkah demi langkah untuk menerapkan aplikasi ini dari awal:

### Langkah 1: Pengaturan Google Apps Script (Backend)

1. Buka [Google Sheets](https://sheets.google.com) yang berisi data nilai siswa.
2. Klik menu **Ekstensi (Extensions)** $\rightarrow$ **Apps Script**.
3. Hapus seluruh kode bawaan, lalu salin dan tempel kode `Code.gs` dari repositori ini.
4. Sesuaikan objek `WALI_KELAS` atau pastikan kolom `Walas` di spreadsheet terisi.
5. Simpan proyek dengan menekan tombol `Ctrl + S`.
6. Klik **Terapkan (Deploy)** $\rightarrow$ **Penenerapan baru (New deployment)**.
7. Pilih jenis: **Aplikasi Web (Web App)**.
   - **Deskripsi**: `PSTS API v1`
   - **Jalankan sebagai (Execute as)**: `Saya (Me / Email Anda)`
   - **Yang memiliki akses (Who has access)**: `Siapa saja (Anyone)`
8. Klik **Terapkan (Deploy)** dan berikan izin akses (*Grant Access*).
9. **Salin URL Aplikasi Web** yang dihasilkan (URL ini berakhiran `/exec`).

### Langkah 2: Pengaturan Frontend (`index.html`)

1. Unduh atau *clone* repositori ini ke komputer Anda:
   ```bash
   git clone [https://github.com/username-anda/nama-repo.git](https://github.com/username-anda/nama-repo.git)

```

2. Buka berkas `index.html` menggunakan teks editor (VS Code, Notepad++, dll).
3. Cari baris variabel berikut di bagian bawah script:
```javascript
const APPS_SCRIPT_URL = "GANTI_DENGAN_URL_DEPLOYMENT_APPS_SCRIPT_ANDA";

```


4. Ganti teks petik dengan **URL Aplikasi Web** yang Anda dapatkan pada Langkah 1.
5. Simpan berkas `index.html`.

### Langkah 3: Publikasi ke GitHub Pages (Hosting Gratis)

1. *Push* perubahan berkas `index.html` ke repositori GitHub Anda.
2. Buka repositori Anda di GitHub.
3. Masuk ke menu **Settings** $\rightarrow$ **Pages**.
4. Pada bagian **Build and deployment**:
* **Source**: Pilih `Deploy from a branch`.
* **Branch**: Pilih `main` (atau `master`) dan folder `/ (root)`.


5. Klik **Save**.
6. Tunggu 1–2 menit, web rapot Anda akan aktif di URL: `https://username-anda.github.io/nama-repo/`.

---

## 🛠️ Teknologi yang Digunakan

* **Frontend**: HTML5, JavaScript (ES6 Async/Fetch), [Tailwind CSS CDN](https://tailwindcss.com/), FontAwesome Icons.
* **Backend**: Google Apps Script (V8 Engine).
* **Database**: Google Sheets.
* **Hosting**: GitHub Pages.

---

## 📄 Lisensi

Proyek ini didistribusikan di bawah lisensi **MIT License**. Bebas digunakan, dimodifikasi, dan dikembangkan kembali untuk keperluan edukasi dan sekolah.

---

---

### Cara Mengunggah Berkas ke GitHub

1. Buka halaman utama repositori Anda di **GitHub**.
2. Jika berkas `README.md` belum ada, klik tombol **Add file** $\rightarrow$ **Create new file**.
3. Beri nama berkas: `README.md`.
4. Tempelkan seluruh teks Markdown di atas ke dalam editor.
5. Klik tombol **Commit changes...** di pojok kanan atas.
---

## 📜 Lisensi & Atribusi Khusus Guru Indonesia

Proyek ini dirilis di bawah lisensi **MIT License** dan dipersembahkan secara **GRATIS** untuk **seluruh Guru dan Tenaga Kependidikan di seluruh Indonesia**. 

Anda bebas menggunakan, menggandakan, memodifikasi, dan menerapkan sistem e-Rapot ini di sekolah Anda masing-masing tanpa dipungut biaya.

### Atribusi Pengembang
Aplikasi ini dikembangkan dan didesain oleh **Catur Pamungkas (Kang Toer)**. Jika Anda menggunakan atau mengembangkan ulang proyek ini, sangat dihargai untuk tetap mencantumkan kredit pengembang asli.

---

## 🌐 Kunjungi Situs Web & Media Sosial

Yuk, terhubung dan dukung terus pengembangan karya-karya teknologi pendidikan lainnya! Kunjungi situs web resmi dan ikuti media sosial saya melalui tautan di bawah ini:

### 🏠 Situs Web Resmi
👉 **[toer.my.id](https://toer.my.id)**

### 📱 Ikuti Media Sosial
Silakan klik ikon atau tautan di bawah ini untuk terhubung secara langsung:

| Media Sosial | Tautan Resmi |
| :--- | :--- |
| <img src="https://cdn.simpleicons.org/facebook/1877F2" width="20" height="20" alt="Facebook"> **Facebook** | [pamungkas.toer](https://facebook.com/pamungkas.toer) |
| <img src="https://cdn.simpleicons.org/x/000000" width="20" height="20" alt="X"> **X (Twitter)** | [@kangtoer](https://x.com/@kangtoer) |
| <img src="https://cdn.simpleicons.org/instagram/E4405F" width="20" height="20" alt="Instagram"> **Instagram** | [@kangtoer](https://instagram.com/kangtoer) |
| <img src="https://cdn.simpleicons.org/youtube/FF0000" width="20" height="20" alt="YouTube"> **YouTube** | [@KangToer](https://www.youtube.com/@KangToer) |
| <img src="https://cdn.simpleicons.org/threads/000000" width="20" height="20" alt="Threads"> **Threads** | [@kangtoer](https://threads.net/@kangtoer) |
| <img src="https://cdn.simpleicons.org/whatsapp/25D366" width="20" height="20" alt="WhatsApp"> **Saluran WhatsApp** | [Join Channel WhatsApp](https://whatsapp.com/channel/0029Vb6R2Ny2v1J1dll5Mq27) |

---
<p align="center">
  Didedikasikan untuk kemajuan Digitalisasi Pendidikan Indonesia 🇮🇩<br>
  <b>Dibuat oleh <a href="https://toer.my.id">Kang Toer</a> untuk Guru Indonesia</b>
</p>
