# Kamus Data

Sumber data : [https://www.kaggle.com/datasets/umeradnaan/tourism-dataset](https://www.kaggle.com/datasets/umeradnaan/tourism-dataset)
Lisensi     : CC0: Public Domain
Berkas      : `data/raw/tourism_dataset.csv`
Jumlah baris: 5989   ·   Jumlah kolom: 7
Diunduh     : 27 September 2026

## Daftar variabel

| Nama kolom | Tipe | Satuan | Deskripsi | Nilai yang mungkin | Data pribadi? | Sumber |
| --- | --- | --- | --- | --- | --- | --- |
| `Location`

 | String / Teks (Identifier) | - | Kode atau pengenal unik untuk setiap destinasi wisata

 | 5.989 nilai teks unik

 | tidak | `tourism_dataset.csv`

 |
| `Country`

 | Kategorikal | - | Negara tempat lokasi destinasi wisata berada | `India`, `USA`, `Brazil`, `France`, `Egypt`, `China`, `Australia` (7 negara unik)

 | tidak | `tourism_dataset.csv`

 |
| `Category`

 | Kategorikal | - | Jenis atau kategori wisata dari destinasi tersebut

 | `Nature`, `Historical`, `Cultural`, `Beach`, `Adventure`, `Urban` (6 kategori)

 | tidak | `tourism_dataset.csv`

 |
| `Visitors`

 | Numerik (Integer) | Orang / Pengunjung | Jumlah total pengunjung yang datang ke destinasi wisata | Bilangan bulat dalam rentang `1.108` hingga `999.982` (Median: `500.831`)

 | tidak | `tourism_dataset.csv`

 |
| `Rating`

 | Numerik (Float / Desimal) | Skor / Bintang | Penilaian atau ulasan rata-rata destinasi wisata | Bilangan desimal dalam rentang `1,00` hingga `5,00` (Median: `3,00`)

 | tidak | `tourism_dataset.csv`

 |
| `Revenue`

 | Numerik (Float / Desimal) | Mata uang (tidak disebutkan secara spesifik di dataset, umumnya USD) | Total pendapatan yang dihasilkan dari destinasi wisata | Bilangan desimal dalam rentang `1.025,81` hingga `999.999,49` (Median: `494.169,35`)

 | tidak | `tourism_dataset.csv`

 |
| `Accommodation_Available`

 | Kategorikal / Boolean | - | Ketersediaan fasilitas akomodasi/penginapan di sekitar lokasi | `Yes`, `No`

 | tidak | `tourism_dataset.csv`

 |

**Kolom "Tipe"** — isi dengan tipe yang *seharusnya*, bukan tipe yang terbaca pandas.
Contoh: `tanggal_masuk` seharusnya bertipe tanggal meskipun terbaca sebagai `object`.

**Kolom "Data pribadi"** — tiga kategori:

| Kategori | Artinya | Contoh |
| --- | --- | --- |
| langsung | mengidentifikasi orang secara langsung | nama, NIK, nomor HP, email |
| tidak langsung | tidak mengidentifikasi sendiri, tetapi bisa bila digabung | tanggal lahir, kode pos, jabatan |
| tidak | tidak berkaitan dengan orang perorangan | jumlah transaksi, kategori produk |

## Tindakan penanganan data pribadi

Dataset ini **tidak memuat data pribadi sama sekali** (baik kategori *langsung* maupun *tidak langsung*). Seluruh baris dan kolom merepresentasikan data agregat tingkat destinasi/lokasi wisata (jumlah pengunjung, rata-rata rating, total pendapatan, kategori, negara, dan ketersediaan akomodasi) tanpa menyertakan identitas individu wisatawan maupun pengelola, sehingga tidak diperlukan tindakan anonimisasi, penghapusan, ataupun *hashing* kolom.

## Catatan tambahan

* **Kualitas & Kelengkapan Data:** Berdasarkan proses inspeksi awal, dataset memiliki tingkat kelengkapan 100% dengan **0 nilai hilang (*missing values*)** dan **0 baris duplikat** di seluruh 5.989 observasi.


* **Distribusi & Outlier:** Tidak ditemukan nilai ekstrem (*outlier*) menggunakan metode IQR pada variabel numerik (`Visitors`, `Rating`, dan `Revenue`). Nilai `Visitors` dan `Revenue` tersebar merata secara sintetis/seragam mendekati batas atas 1.000.000.


* **Keterangan Satuan & Format:** Kolom `Location` berperan murni sebagai ID unik (bukan nama kota/tempat riil) dan dipertahankan sebagai tipe `object` agar tidak ikut terkalkulasi dalam ringkasan statistik. Sementara itu, kolom `Revenue` tidak mencantumkan simbol mata uang eksplisit pada data mentah, dan `Accommodation_Available` direpresentasikan dalam teks `Yes`/`No` (dapat dipetakan menjadi boolean `True`/`False` jika diperlukan untuk pemodelan).
