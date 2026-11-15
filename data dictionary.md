# Kamus Data (*Data Dictionary*)

| Atribut | Keterangan |
| :--- | :--- |
| **Sumber Data** | [Tourism Dataset — Kaggle (`umeradnaan`)](https://www.kaggle.com/datasets/umeradnaan/tourism-dataset) |
| **Lisensi** | CC0: Public Domain |
| **Berkas** | `data/raw/tourism_dataset.csv` |
| **Dimensi Dataset** | 5.989 baris × 7 kolom |
| **Tanggal Diunduh** | 27 September 2026 |

---

## Daftar Variabel

| Nama Kolom | Tipe | Satuan | Deskripsi | Nilai yang Mungkin | Data Pribadi? | Sumber |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `Location` | String / Teks (*Identifier*) | — | Kode atau pengenal unik untuk setiap destinasi wisata | 5.989 nilai teks unik | tidak | `tourism_dataset.csv` |
| `Country` | Kategorikal | — | Negara tempat lokasi destinasi wisata berada | `India`, `USA`, `Brazil`, `France`, `Egypt`, `China`, `Australia` (7 negara unik) | tidak | `tourism_dataset.csv` |
| `Category` | Kategorikal | — | Jenis atau kategori wisata dari destinasi tersebut | `Nature`, `Historical`, `Cultural`, `Beach`, `Adventure`, `Urban` (6 kategori) | tidak | `tourism_dataset.csv` |
| `Visitors` | Numerik (*Integer*) | Orang / Pengunjung | Jumlah total pengunjung yang datang ke destinasi wisata | Bilangan bulat dalam rentang `1.108` – `999.982` (Median: `500.831`) | tidak | `tourism_dataset.csv` |
| `Rating` | Numerik (*Float*) | Skor / Bintang | Penilaian atau ulasan rata-rata destinasi wisata | Bilangan desimal dalam rentang `1,00` – `5,00` (Median: `3,00`) | tidak | `tourism_dataset.csv` |
| `Revenue` | Numerik (*Float*) | Mata uang (umumnya USD) | Total pendapatan yang dihasilkan dari destinasi wisata | Bilangan desimal dalam rentang `1.025,81` – `999.999,49` (Median: `494.169,35`) | tidak | `tourism_dataset.csv` |
| `Accommodation_Available` | Kategorikal / Boolean | — | Ketersediaan fasilitas akomodasi atau penginapan di sekitar lokasi | `Yes`, `No` | tidak | `tourism_dataset.csv` |

> **Keterangan Klasifikasi:**
> * **Tipe:** Diisi berdasarkan tipe data semantik yang *seharusnya*, bukan sekadar tipe bawaan pembacaan `pandas` (misalnya `Country`, `Category`, dan `Accommodation_Available` dikonversi menjadi `category` untuk efisiensi memori).
> * **Data Pribadi:** Diklasifikasikan menjadi **`langsung`** (mengidentifikasi individu secara langsung, seperti NIK/email), **`tidak langsung`** (dapat mengidentifikasi bila digabungkan, seperti tanggal lahir/kode pos), dan **`tidak`** (data agregat/non-personal).

---

## Tindakan Penanganan Data Pribadi

Dataset ini **tidak memuat data pribadi sama sekali** (baik kategori *langsung* maupun *tidak langsung*). Seluruh baris dan kolom merepresentasikan data agregat tingkat destinasi wisata (jumlah pengunjung, rata-rata *rating*, total pendapatan, kategori, negara, dan ketersediaan akomodasi) tanpa mencantumkan identitas individu wisatawan maupun pengelola, sehingga tidak diperlukan tindakan penghapusan, penyamaran (*masking*), maupun *hashing* kolom.

---

## Catatan Tambahan

* **Kelengkapan & Kebersihan Data:** Berdasarkan hasil inspeksi pada tahap pra-pemrosesan (*data cleaning*), dataset memiliki tingkat kelengkapan **100%** dengan **0 nilai hilang (*missing values*)** dan **0 baris duplikat** di seluruh 5.989 observasi.
* **Distribusi & *Outlier*:** Pemeriksaan menggunakan metode IQR (*Interquartile Range*) menunjukkan **0 *outlier*** pada seluruh variabel numerik (`Visitors`, `Rating`, dan `Revenue`). Distribusi nilai `Visitors` dan `Revenue` tersebar merata secara seragam mendekati batas atas 1.000.000.
* **Karakteristik Kolom Khusus:**
  * `Location` berfungsi murni sebagai ID unik destinasi (bukan nama kota atau tempat geografis riil) dan dipertahankan bertipe `object` agar tidak ikut terhitung dalam ringkasan statistik numerik.
  * `Revenue` tidak mencantumkan simbol mata uang secara eksplisit di dalam berkas mentah.
  * `Accommodation_Available` tercatat dalam bentuk teks `Yes`/`No` (telah distandardisasi dengan `.str.strip()` dan dapat dipetakan menjadi boolean `True`/`False` pada tahap pemodelan jika diperlukan).
