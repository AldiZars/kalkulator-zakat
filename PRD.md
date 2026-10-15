# PRODUCT REQUIREMENTS DOCUMENT (PRD)

## Kalkulator Zakat Penghasilan Sederhana — Cek Kewajiban Zakat dari Gaji Bulanan

**STATUS: DRAFT SEMENTARA**

| | |
| --- | --- |
| **Nama Produk** | Kalkulator Zakat Penghasilan Sederhana — Cek Kewajiban Zakat dari Gaji Bulanan |
| **Versi Dokumen** | v0.1 (Draft Sementara) |
| **Disusun oleh** | Pengembang (TBD — lihat Bab 12) |
| **Untuk** | Klien / Pemilik Produk (TBD — lihat Bab 12) |
| **Tanggal** | 12 Oktober 2026 |
| **Dokumen Terkait** | Wireframe `kalkulator-zakat.html` (1 gambar mockup browser) dan Kartu Spesifikasi Teknis HTML/CSS/JS (1 gambar) — terlampir sebagai input desain |

---

# 1. Ringkasan Produk (Overview)

Banyak muslim masih menghitung zakat penghasilan secara manual dan ragu apakah gajinya sudah mencapai batas wajib (nisab). Tanpa acuan yang jelas dan alat hitung yang cepat, pengguna harus mengingat kadar 2,5%, menyetarakan nisab emas 85 gram, dan menghitung sendiri dengan kalkulator umum yang tidak memberi kepastian status wajib/tidak wajib.

Solusi yang akan dibangun adalah website satu halaman statis `kalkulator-zakat.html` berbasis HTML dan CSS dengan interaktivitas JavaScript dasar. Sistem terdiri dari dua modul utama: (1) Tabel Syarat Nisab sebagai acuan, dan (2) Form Hitung Zakat dengan kotak Hasil Hitung yang mencolok. Cakupan siklus yang ditangani adalah lihat acuan → input gaji bulanan → validasi nisab → tampilkan nominal zakat atau dialog belum wajib, seluruhnya tanpa refresh halaman. Tujuannya adalah memberi cek kewajiban zakat dari gaji bulanan yang sederhana, instan, dan tepat mengikuti wireframe.

# 2. Tujuan & Sasaran (Goals)

- Memudahkan pengguna mengecek status kewajiban zakat penghasilan dari gaji bulanan dalam satu langkah hitung.
- Mengurangi kesalahan hitung manual dengan menerapkan formula tunggal yang konsisten (2,5% × gaji).
- Menyediakan acuan nisab yang transparan (Emas 85 gram, Perak 595 gram, Penghasilan setara 85 g emas) di halaman yang sama.
- Memberikan kepastian status secara instan (wajib dengan nominal, atau belum wajib) tanpa navigasi tambahan.
- Menyediakan hasil yang langsung terlihat melalui penekanan visual yang mencolok.

# 3. Pengguna & Peran (Users & Roles)

- **Pengunjung / Pengguna Umum :** satu-satunya peran. Dapat melihat tabel syarat nisab, mengisi gaji bulanan pada form, menekan tombol Hitung, melihat hasil di kotak hasil atau dialog peringatan. Tidak ada login, tidak ada hak khusus.

# 4. Ruang Lingkup (Scope)

## 4.1 Termasuk (MVP)

- Tabel Syarat Nisab dengan kolom Jenis Harta dan Nisab.
- Form Hitung Zakat dengan input Gaji Bulanan (Rp) dan tombol Hitung.
- Validasi ambang nisab Rp 7.000.000/bulan dengan dua skenario (≥ Rp 7 juta dan < Rp 7 juta).
- Perhitungan zakat 2,5% × gaji dan penampilan hasil di elemen `div id="hasil"` dengan gaya mencolok.
- Interaksi tanpa refresh (`event.preventDefault()`) dan dialog `alert()` untuk status belum wajib.

## 4.2 Di Luar Lingkup Awal / Fase Lanjutan

Belum ada fitur yang ditunda pada tahap ini. Tidak ada fitur Fase Lanjutan yang disepakati dari wireframe dan spek (lihat Bab 11).

# 5. Asumsi & Batasan (Assumptions & Constraints)

- Teknologi murni HTML dan CSS untuk struktur dan tampilan, ditambah JavaScript vanilla untuk logika (asumsi pengembang, sesuai kartu spek HTML/CSS/JS).
- Satu file halaman `kalkulator-zakat.html`, tanpa backend, tanpa database, tanpa penyimpanan permanen (asumsi pengembang).
- Ambang nisab disederhanakan menjadi tetap Rp 7.000.000/bulan sebagai setara 85 g emas — bukan kurs emas dinamis (sesuai wireframe Skenario A/B).
- Kadar zakat tetap 2,5% per bulan; formula: Zakat = 0,025 × Gaji Bulanan (sesuai wireframe dan TIPS).
- Dialog status belum wajib menggunakan `alert()` bawaan browser dengan teks persis `Anda belum wajib zakat` (sesuai spek JS dan wireframe).
- Kotak hasil memakai `border: 4px solid`, `background-color` kontras/terang, dan `font-weight: bold` (sesuai spek CSS).
- Form harus memakai `<form>` + `<table>` + `<div id="hasil">` sesuai spek HTML; submit form dicegah reload via `event.preventDefault()` (sesuai anotasi wireframe).
- Contoh acuan: input Rp 10.000.000 menghasilkan Rp 250.000 (sesuai wireframe).
- Tidak ada ketergantungan layanan pihak ketiga dan tidak ada biaya tambahan yang teridentifikasi pada tahap ini.

# 6. Kebutuhan Fungsional (Functional Requirements)

## 6.1 Pengguna — Tabel Syarat Nisab

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **TBN-1** | Sistem menampilkan tabel Syarat Nisab pada halaman. | **Wajib** |
| **TBN-2** | Sistem menampilkan tabel dengan kolom Jenis Harta dan Nisab (batas minimal). | **Wajib** |
| **TBN-3** | Sistem menampilkan baris Emas = 85 gram, Perak = 595 gram, Penghasilan = Setara 85 g emas. | **Wajib** |

## 6.2 Pengguna — Form Hitung Zakat

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **FRM-1** | Pengguna dapat memasukkan Gaji Bulanan (Rp) pada `<form>`. | **Wajib** |
| **FRM-2** | Pengguna dapat menekan tombol Hitung untuk memproses perhitungan. | **Wajib** |
| **FRM-3** | Sistem mencegah reload halaman saat form disubmit menggunakan `event.preventDefault()`. | **Wajib** |

## 6.3 Pengguna — Validasi, Perhitungan, dan Hasil

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **HSL-1** | Sistem menampilkan dialog `alert("Anda belum wajib zakat")` dengan tombol OK jika Gaji < Rp 7.000.000. | **Wajib** |
| **HSL-2** | Sistem menghitung nominal zakat dengan formula 2,5% × gaji jika Gaji ≥ Rp 7.000.000. | **Wajib** |
| **HSL-3** | Sistem menampilkan hasil perhitungan di dalam elemen `<div id="hasil">`. | **Wajib** |
| **HSL-4** | Sistem menampilkan kotak Hasil Hitung dengan `border: 4px solid`, `background-color` mencolok/kontras, dan `font-weight: bold`, berisi nominal (contoh Rp 250.000) dan subteks Zakat 2,5% per bulan. | **Wajib** |

# 7. Alur Pengguna Utama (Key User Flows)

## 7.1 Skenario A — Gaji ≥ Rp 7.000.000 (Happy Path, Wajib Zakat)

1. Pengguna membuka `kalkulator-zakat.html` dan melihat Tabel Syarat Nisab serta Form Hitung Zakat.
2. Pengguna memasukkan Gaji Bulanan, contoh 10.000.000.
3. Pengguna menekan tombol Hitung.
4. Sistem menahan reload halaman (`event.preventDefault()`).
5. Sistem menilai gaji ≥ Rp 7.000.000, menghitung 0,025 × gaji (contoh 10.000.000 × 0,025 = 250.000).
6. Sistem menampilkan kotak HASIL HITUNG berisi Rp 250.000 dan subteks Zakat 2,5% per bulan.

## 7.2 Skenario B — Gaji < Rp 7.000.000 (Pengecualian, Belum Wajib)

1. Pengguna memasukkan Gaji Bulanan di bawah Rp 7.000.000.
2. Pengguna menekan tombol Hitung.
3. Sistem menahan reload halaman (`event.preventDefault()`).
4. Sistem menilai gaji < Rp 7.000.000 dan menampilkan dialog browser berisi teks kecil Halaman ini menyatakan dan teks utama Anda belum wajib zakat.
5. Pengguna menekan OK untuk menutup dialog; tidak ada nominal yang dihitung.

## 7.3 Melihat Acuan Nisab

1. Pengguna menggulir ke bagian Syarat Nisab.
2. Pengguna membaca baris Emas, Perak, dan Penghasilan untuk memahami batas minimal sebelum mengisi form.

# 8. Model Data (High-Level)

| **Entitas** | **Field Utama** | **Keterangan** |
| --- | --- | --- |
| **Kalkulasi** | gaji_bulanan, ambang_nisab, kadar_zakat, nominal_zakat | Data transien di memori browser saja; tidak disimpan. `ambang_nisab` = 7000000, `kadar_zakat` = 0,025. |

**Catatan:** field dalam [tanda kurung siku] merupakan bagian dari fitur usulan/Fase Lanjutan (Bab 11). Tidak ada field Fase Lanjutan pada versi ini.

# 9. Kebutuhan Non-Fungsional (Non-Functional Requirements)

- **Ketepatan visual :** implementasi harus mengikuti wireframe 100% sebagai tulang awal — posisi tabel kiri-atas, form kanan-atas, dua kotak skenario di bawah, legenda Anotasi CSS dan Dialog JS.
- **Penekanan hasil :** kotak `#hasil` harus langsung terlihat melalui border tebal, latar kontras, dan teks bold.
- **Responsivitas instan :** perhitungan terjadi tanpa refresh; tidak ada jeda navigasi.
- **Kompatibilitas :** berjalan di browser modern dengan HTML/CSS/JS vanilla tanpa pustaka tambahan; dialog memakai `alert()` bawaan.
- **Kesederhanaan :** satu halaman, satu alur, tanpa login dan tanpa penyimpanan data pribadi.

# 10. Integrasi Pihak Ketiga

Sistem berdiri sendiri dan tidak memiliki integrasi pihak ketiga.

# 11. Fitur Usulan / Fase Lanjutan

Belum ada usulan fase lanjutan.

# 12. Pertanyaan Terbuka / TBD

- Siapa nama pengembang dan klien/pemilik produk resmi untuk kolom identitas dokumen?
- Apakah ambang Rp 7.000.000 bersifat tetap atau harus mengikuti harga emas harian dinamis?
- Bagaimana validasi input kosong, non-angka, nol, atau negatif — pesan apa yang tampil?
- Bagaimana perilaku tepat pada nilai batas Rp 7.000.000 (dikonfirmasi ikut Skenario A ≥)?
- Bagaimana format tampilan angka (pemisah ribuan, prefix Rp, desimal)?
- Apakah hasil untuk Skenario B harus tetap mengosongkan/menyembunyikan kotak `#hasil`?
- Di mana website akan di-hosting dan apakah ada nama domain khusus?
- Apakah ada kebutuhan bahasa tambahan selain Bahasa Indonesia?

# 13. Glosarium

- **Nisab :** batas minimal harta yang mewajibkan zakat (di dokumen ini: Emas 85 gram, Perak 595 gram).
- **Zakat Penghasilan :** zakat dari gaji/penghasilan rutin dengan kadar 2,5% apabila mencapai nisab setara 85 g emas.
- **event.preventDefault() :** perintah JavaScript untuk mencegah perilaku bawaan form (reload halaman) saat disubmit.
- **alert() :** dialog peringatan bawaan browser dengan tombol OK.
- **div id="hasil" :** elemen penampung keluaran nominal zakat di halaman.

---

*Dokumen ini merupakan draft sementara dan dapat berubah seiring pembahasan lebih lanjut dengan klien.*
