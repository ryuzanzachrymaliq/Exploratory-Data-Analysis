# 🌴 Tourism Dataset Analysis

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

Proyek ini berfokus pada analisis kualitatif dan kuantitatif terhadap data pariwisata global untuk mengevaluasi kinerja destinasi wisata serta efisiensi operasionalnya.

---

## 👥 Anggota Tim

| Nama | NIM |
| :--- | :--- |
| **Firza Fadillah** | `0110225070` |
| **Muhammad Fawwaz Abqory** | `0110225148` |
| **Adli Abdurrahman Syah** | `0110225008` |
| **Ryuzan Zachry Maliq** | `0110225082` |

---

## 🎯 Tujuan Proyek

Memahami tren kinerja destinasi wisata dunia berdasarkan preferensi pengunjung, tingkat kepuasan, pendapatan, serta ketersediaan akomodasi guna mendukung pengambilan keputusan strategis dalam pengembangan sektor pariwisata.

---

## 📑 Ringkasan Profil & Eksplorasi Data

### 1. Dimensi & Satuan Data
Dataset pariwisata ini secara keseluruhan memiliki dimensi data yang terdiri dari **5.989 baris** dan **7 kolom**. Dalam dataset ini, setiap baris mewakili entitas **satu lokasi atau destinasi wisata spesifik** yang dicatat kinerja bisnisnya. Setiap baris menyimpan atribut unik lokasi tersebut mulai dari identitas wilayah, tingkat kepuasan wisatawan, volume pengunjung, pendapatan yang diraih, hingga ketersediaan fasilitas penginapan.

---

### 2. Pengelompokan Jenis Kolom
Dataset ini memuat kombinasi tipe data numerik dan kategorikal, namun tidak memiliki atribut berbasis tanggal atau waktu.

* **Variabel Numerik:**
  * `Visitors` *(Integer)*: Mengukur kuantitas atau jumlah wisatawan.
  * `Rating` *(Float)*: Mencatat tingkat kepuasan wisatawan pada skala 1,00 hingga 5,00.
  * `Revenue` *(Float)*: Jumlah pendapatan finansial yang diperoleh destinasi.

* **Variabel Kategorikal:**
  * `Location` *(String)*: Kode unik lokasi destinasi.
  * `Country` *(String)*: Memuat 7 negara asal destinasi wisata.
  * `Category` *(String)*: Jenis objek wisata (*Nature*, *Historical*, *Cultural*, *Beach*, *Adventure*, dan *City*).
  * `Accommodation_Available` *(String)*: Status ketersediaan fasilitas penginapan (`Yes` / `No`).

---

### 3. Analisis Kualitas Data (*Data Issues*)
Dari aspek kualitas dan kebersihan data, dataset ini secara umum berada dalam kondisi yang sangat baik karena **tidak ditemukan adanya nilai kosong (*missing values*) maupun baris duplikat** di seluruh kolom. Tipe data dasar yang digunakan oleh Pandas juga sudah tepat sesuai dengan sifat masing-masing variabel, dan variasi entitas pada variabel kategorikal seperti nama negara serta kategori wisata tercatat secara konsisten.

> ℹ️ **Catatan Teknis:**  
> Kolom `Location` menggunakan pengodean string acak (*hash*) alih-alih nama asli tempat wisata, sehingga kurang ramah untuk dibaca secara langsung oleh manusia (*not human-readable*).

---

### 4. Kelayakan Data untuk Pertanyaan Analisis Tim
Dataset ini tergolong belum cukup lengkap apabila tim analisis ingin melakukan evaluasi tren kinerja bisnis berbasis rentang waktu, meskipun sudah memadai untuk analisis agregat deskriptif dasar.

⚠️ **Keterbatasan Utama Dataset:**
1. **Ketiadaan Atribut Waktu:** Absennya kolom tanggal atau *timestamp* menyebabkan tim tidak dapat mengukur pertumbuhan tahunan (*YoY growth*), analisis pola musiman (*seasonality*), maupun tren pengunjung bulanan.
2. **Pseudonimitas Geografis:** Penggunaan kode lokasi acak menyulitkan pemetaan spasial atau analisis geografis secara nyata.
3. **Detail Finansial Terbatas:** Ketiadaan variabel biaya operasional (*Cost*) atau harga tiket menyebabkan pengukuran profitabilitas bersih (*Net Profit*) serta evaluasi strategi penentuan harga belum dapat dilakukan secara komprehensif.
