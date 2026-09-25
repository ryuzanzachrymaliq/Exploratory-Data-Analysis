# Praktikum Pertemuan 2 — pandas di Google Colab[cite: 2]

**Mata Kuliah:** Exploratory Data Analysis (KMTI21133) — Pertemuan 2[cite: 2]  
**Sub-CPMK2:** Mahasiswa mampu menggunakan Python (`pandas`) di Google Colab/Jupyter dan Git/GitHub untuk memuat, menelusuri, dan menyimpan data serta kode analisis[cite: 2].

---

## 📌 Deskripsi
Repositori ini berisi notebook praktikum dan dataset yang digunakan pada Pertemuan 2 mata kuliah *Exploratory Data Analysis*[cite: 2]. Praktikum ini berfokus pada pengenalan dasar manipulasi dan eksplorasi data menggunakan pustaka `pandas` dan `numpy` di lingkungan Google Colab[cite: 2].

---

## 📂 Struktur File
* `Praktikum_Pertemuan_2.ipynb`: Notebook utama berisi materi demonstrasi (`# DEMO`) dan tugas latihan mandiri/berpasangan (`# TODO`)[cite: 2].
* `penjualan_umkm_2024.csv`: Dataset transaksi penjualan UMKM tahun 2024 yang dianalisis[cite: 2].
* `README.md`: Dokumentasi dan panduan pelaksanaan praktikum.

---

## 📊 Informasi Dataset (`penjualan_umkm_2024.csv`)
Dataset memuat 1.212 baris data transaksi dengan kolom-kolom berikut[cite: 2]:
* `id_transaksi`: ID unik transaksi penjualan[cite: 2].
* `tanggal`: Tanggal transaksi[cite: 2].
* `kota`: Kota lokasi transaksi[cite: 2].
* `kategori`: Kategori produk (Makanan, Minuman, Fashion, Kerajinan)[cite: 2].
* `produk`: Nama produk yang dijual[cite: 2].
* `jumlah`: Kuantitas produk yang dibeli[cite: 2].
* `harga_satuan`: Harga per unit produk[cite: 2].
* `diskon_persen`: Persentase diskon yang diterapkan[cite: 2].
* `metode_bayar`: Metode pembayaran (Transfer, Tunai, E-Wallet, QRIS)[cite: 2].
* `rating_pelanggan`: Nilai rating dari pelanggan[cite: 2].
* `total_bayar`: Total nilai pembayaran transaksi[cite: 2].

---

## 🔄 Cara Kerja & Ketentuan Praktikum
1. **Bagian `# DEMO`**: Diisi dan dipelajari bersama dosen saat sesi perkuliahan[cite: 2].
2. **Bagian `# TODO`**: Dikerjakan secara mandiri atau berpasangan oleh mahasiswa[cite: 2].
3. **Pemeriksaan Mandiri**: Setiap bagian `# TODO` memiliki *expected output* untuk memverifikasi kebenaran hasil[cite: 2].
4. **Pengumpulan**: Simpan dan *commit* notebook yang telah diselesaikan ke repositori Tim Git/GitHub di akhir sesi[cite: 2].

---

## 🎯 Ringkasan Ringkasan Bagian Praktikum

### **Bagian 0 — Persiapan**[cite: 2]
* Memeriksa versi pustaka `pandas` dan `numpy`[cite: 2].
* Mengunggah file dataset `penjualan_umkm_2024.csv` ke dalam sesi Google Colab[cite: 2].

### **Bagian A — Memuat dan Memeriksa Data (Latihan 1)**[cite: 2]
* **DEMO A1 - A3**: Memuat file CSV (`pd.read_csv`), memeriksa jumlah baris/kolom dan tipe data (`df.shape`, `df.info()`), serta ringkasan statistik deskriptif (`df.describe()`)[cite: 2].
* **TODO A4**: Menampilkan 5 baris terakhir (`df.tail(5)`) serta daftar tipe data (`df.dtypes`)[cite: 2].
* **TODO A5**: Memeriksa kebersihan data, meliput:
  * Jumlah nilai kosong (*missing values*) per kolom (`df.isna().sum()`)[cite: 2].
  * Jumlah baris duplikat (`df.duplicated().sum()`)[cite: 2].
  * Jumlah dan daftar nilai unik pada kolom `kota` (`df['kota'].nunique()`, `df['kota'].unique()`)[cite: 2].

### **Bagian B — Seleksi dan Filter (Latihan 2)**[cite: 2]
* Melakukan seleksi kolom dan penyaringan data (*filtering*) sesuai skenario analisis[cite: 2].

---

## 🚀 Panduan Menjalankan Notebook
1. Buka [Google Colab](https://colab.research.google.com/).
2. Unggah file `Praktikum_Pertemuan_2.ipynb`[cite: 2].
3. Jalankan sel **Bagian 0** dan unggah `penjualan_umkm_2024.csv` jika diminta[cite: 2].
4. Eksekusi sel kode secara berurutan[cite: 2].
