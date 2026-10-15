# Kalkulator Zakat Penghasilan Sederhana

> Cek kewajiban zakat dari gaji bulanan secara cepat, tepat, dan transparan sesuai acuan fiqih nisab emas 85 gram.

Live Demo: [https://kalkulator-zakat-amber.vercel.app](https://kalkulator-zakat-amber.vercel.app)

---

## 📌 Deskripsi

Website satu halaman statis untuk menghitung zakat profesi/penghasilan bulanan (2,5%) dengan validasi ambang batas nisab tetap (Rp 7.000.000/bulan) berbasis vanilla HTML, CSS, dan JavaScript tanpa dependensi eksternal.

## ✨ Fitur Utama

- **Tabel Syarat Nisab (`<table>`):** Menampilkan acuan batas nisab Emas (85g), Perak (595g), dan Penghasilan (setara 85g emas).
- **Form Hitung Zakat (`<form>`):** Input gaji bulanan dengan pencegahan reload (`event.preventDefault()`).
- **Validasi Dua Skenario:**
  - **Skenario A (Gaji ≥ Rp 7.000.000):** Wajib zakat. Hasil dihitung instan $2,5\% \times \text{Gaji}$ dan ditampilkan pada kotak `#hasil` dengan gaya mencolok (`border: 4px solid`, background kontras, teks bold).
  - **Skenario B (Gaji < Rp 7.000.000):** Belum wajib zakat. Menampilkan dialog notifikasi browser `alert("Anda belum wajib zakat")`.

## 📁 Struktur Berkas

```text
├── kalkulator-zakat.html   # Halaman utama kalkulator zakat
├── index.html              # Salinan entry point web server
├── style.css               # Styling eksternal
├── PRD.md                  # Product Requirements Document v0.1
└── README.md               # Dokumentasi proyek
```

## 🚀 Cara Menjalankan Secara Lokal

Cukup buka berkas `kalkulator-zakat.html` atau `index.html` langsung di browser favorit Anda, atau jalankan local server:

```bash
# Menggunakan Python
python3 -m http.server 8080

# Menggunakan Node.js npx serve
npx serve .
```

Buka peramban di `http://localhost:8080`.
