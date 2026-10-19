# Cleaning Log

> **Template M2 — Exploratory Data Analysis (KMTI21133).**
> Berkas ini diletakkan di **akar repositori** dengan nama persis `cleaning_log.md`.

**Tim:** Tim Koperasi M2  
**Dataset:** `transaksi_koperasi_2025.csv`  
**Baris mentah:** 1.543 baris → **Baris bersih:** 1.437 baris  
**Terakhir diperbarui:** 19 Oktober 2026  

---

## Urutan langkah

| # | Langkah | Kolom | Baris terdampak | Keputusan | Alasan |
|---|---|---|---|---|---|
| 1 | Perbaiki tipe data | `total_bayar` | 1.543 baris | Menghilangkan string 'Rp', titik ribuan, dan mengonversi ke tipe data numerik | Teks 'Rp' dan titik ribuan membuat kolom dibaca sebagai tipe object/string sehingga tidak dapat dihitung secara matematis. |
| 2 | Buang spasi pada kolom teks | `kategori`, `metode_bayar` | ~300 baris | Mengaplikasikan `.str.strip()` dan format *Title Case* | Spasi berlebih di awal/akhir string (misal: `" Makanan"`) menyebabkan pengelompokan (*groupby*) membaca nilai tersebut sebagai kategori terpisah. |
| 3 | Placeholder menjadi kosong | `metode_bayar` | 22 baris | Mengubah nilai `"-"`, `"Nan"`, dan `"Tidak Diketahui"` menjadi `NaN` | Menjaga kejujuran data; nilai placeholder fiktif menyamarkan fakta bahwa metode pembayaran sebenarnya tidak tercatat. |
| 4 | Seragamkan kategori | `kategori` | 85 baris | Mengubah `"Alat Tulis"` menjadi `"ATK"` dan `"Minumam"` menjadi `"Minuman"` | Menggabungkan variasi istilah dan mengoreksi salah ketik (*typo*) agar agregasi data penjualan per kategori akurat. |
| 5 | Tangani duplikat | Semua kolom | 24 baris | Menghapus baris duplikat persis (`drop_duplicates()`) | Duplikasi baris terjadi akibat *double submit* pada sistem POS, yang dapat membengkakkan nilai total transaksi secara palsu. |
| 6 | Tangani nilai mustahil | `jumlah`, `diskon_persen`, `rating_layanan` | 74 baris | Menghapus baris dengan `jumlah <= 0` (18 baris), `diskon_persen` di luar 0–100% (9 baris), dan `rating_layanan == -999` (47 baris) | Nilai negatif atau diskon >100% melanggar logika bisnis transaksi, sedangkan `-999` adalah kode *error* sistem untuk rating yang tidak diisi. |
| 7 | Tangani nilai kosong | `berat_kg`, `saldo_simpanan` | 510 baris | Dibiarkan kosong (`NaN`) tanpa diisi/diimputasi | Kekosongan pada `berat_kg` terjadi karena produk jasa/pulsa tidak memiliki berat fisik (MAR), sehingga memasukkan rata-rata/median justru menciptakan data palsu. |
| 8 | Buat kolom turunan | `total_harga_hitung` | 1.437 baris | Membuat kolom baru `jumlah` * `harga_satuan` * (1 - `diskon_persen`/100) | Diperlukan sebagai kontrol kualitas (*cross-check*) terhadap konsistensi nilai pada kolom `total_bayar`. |

---

## Peta keputusan manual

| Nilai asal | Diubah menjadi | Dasar keputusan |
|---|---|---|
| `Alat Tulis` | `ATK` | Penggabungan istilah sinonim berdasarkan katalog barang resmi koperasi. |
| `Minumam` | `Minuman` | Koreksi kesalahan ketik (*typo*) pada input manual kasir. |
| `Qris`, `qris` | `QRIS` | Penyeragaman akronim standar pembayaran digital. |
| `-`, `tidak diketahui` | *Kosong (`NaN`)* | Menjadikan status data hilang transparan alih-alih menggunakan teks penyamar. |

---

## Yang sengaja TIDAK diubah

| Masalah | Mengapa dibiarkan | Akibat bagi analisis |
|---|---|---|
| `berat_kg` kosong pada 351 baris (22.7%) | Transaksi produk digital/jasa (seperti Pulsa dan Jasa Fotokopi) memang tidak memiliki besaran berat fisik. | Analisis total berat pengiriman atau logistik hanya dapat dilakukan pada produk fisik. |
| `saldo_simpanan` kosong pada 159 baris (10.3%) | Transaksi dilakukan oleh pembeli non-anggota/umum yang tidak memiliki akun simpanan di koperasi. | Analisis hubungan saldo simpanan terhadap nilai belanja dibatasi khusus untuk anggota resmi. |
| `catatan_kasir` kosong pada 1.044 baris (67.7%) | Kolom catatan bersifat opsional saat proses kasir melayani pembeli. | Kolom ini tidak dapat digunakan sebagai variabel utama dalam pemodelan kuantitatif. |

---

## Pertanyaan yang belum terjawab

- [ ] Apakah transaksi dengan `jumlah` negatif merupakan retur barang resmi yang seharusnya dicatat di tabel terpisah?
- [ ] Apakah `saldo_simpanan` kosong untuk non-anggota bisa diisi angka `0` atau tetap dibiarkan `NaN` agar tidak mengganggu perhitungan rata-rata saldo anggota?

---

## Dampak keseluruhan

| Ukuran | Sebelum | Sesudah | Catatan |
|---|---|---|---|
| Jumlah baris | 1.543 | 1.437 | Berkurang 106 baris karena pembersihan duplikat (24) dan nilai mustahil/error (82). |
| Jumlah kolom | 16 | 17 | Bertambah 1 kolom turunan (`total_harga_hitung`). |
| Total sel kosong | 1.564 | 1.631 | **Bertambah 67 sel kosong**, karena *placeholder* teks seperti `"-"` diubah menjadi `NaN` jujur. |
| Baris duplikat | 24 | 0 | Berhasil dibersihkan sepenuhnya. |
| Kategori pada kolom kunci | 18 variasi | 5 kategori | Terpusat menjadi: `Makanan`, `Minuman`, `ATK`, `Jasa`, dan `Pulsa`. |

---

## Reproduktibilitas

- [x] Notebook berjalan dari awal sampai akhir setelah *Restart and run all*
- [x] Pembersihan dibungkus dalam satu fungsi, bukan tersebar di banyak sel
- [x] `data/raw/` tidak berubah dan tidak ikut diunggah
- [x] Hasil tersimpan di `data/processed/`
- [x] `python cek_m2.py` berjalan tanpa status GAGAL