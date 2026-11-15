# 🧹 Log Pembersihan & Pra-pemrosesan Data (Data Cleaning & Preprocessing Log)

Dokumen ini mencatat seluruh tahapan inspeksi, identifikasi masalah data, keputusan pembersihan, serta transformasi data yang dilakukan pada `tourism_dataset.csv` sebelum tahap analisis eksplorasi (EDA).

---

## 📌 Ringkasan Data Awal

* **Nama File Dataset:** `tourism_dataset.csv`
* **Jumlah Baris (Awal):** 5.989 baris
* **Jumlah Kolom (Awal):** 7 kolom (`Location`, `Country`, `Category`, `Visitors`, `Rating`, `Revenue`, `Accommodation_Available`)
* **Tipe Data:** Kombinasi Numerik (`int64`, `float64`) dan Kategorikal (`object`).

---

## 🔍 Tahapan Inspeksi & Pembersihan Data

### 1. Pengecekan & Penanganan Nilai Hilang (*Missing Values*)
* **Inspeksi:** Menjalankan `df.isnull().sum()` untuk mengidentifikasi keberadaan nilai kosong di setiap kolom.
* **Temuan:**
  * Seluruh kolom (`Location`, `Country`, `Category`, `Visitors`, `Rating`, `Revenue`, dan `Accommodation_Available`) memiliki **0 nilai kosong (0%)**.
* **Tindakan:**
  * Tidak diperlukan proses imputasi karena data sudah lengkap 100%.

### 2. Pengecekan & Penanganan Data Duplikat (*Duplicate Records*)
* **Inspeksi:** Menjalankan `df.duplicated().sum()` untuk mengecek baris ganda secara keseluruhan, serta memverifikasi keunikan kolom identifier `Location`.
* **Temuan:**
  * Terdeteksi **0 baris duplikat** secara keseluruhan, dan seluruh 5.989 nilai pada kolom `Location` bersifat unik.
* **Tindakan:**
  * Tidak ada baris yang dihapus (`df.drop_duplicates()` tidak mengurangi jumlah baris).

### 3. Penyesuaian Tipe Data (*Data Types Conversion*)
* **Inspeksi:** Menjalankan `df.dtypes` dan `df.info()`.
* **Temuan:**
  * `Location`, `Country`, `Category`, `Accommodation_Available` bertipe `object`.
  * `Visitors` bertipe `int64`.
  * `Rating` dan `Revenue` bertipe `float64`.
* **Tindakan:**
  * Mempertahankan kolom identifier `Location` sebagai tipe `object` agar tidak ikut terhitung dalam kalkulasi statistik numerik.
  * Mengonversi kolom kategorikal dengan kardinalitas rendah (`Country`, `Category`, `Accommodation_Available`) ke tipe `category` untuk efisiensi memori.

### 4. Penanganan Format & Konsistensi Teks (*Text Standardization*)
* **Inspeksi:** Pengecekan nilai unik dan potensi *leading/trailing whitespace* pada kolom teks menggunakan `df[col].unique()`.
* **Temuan:**
  * Tidak ditemukan spasi berlebih (*whitespace*) maupun inkonsistensi penulisan kapitalisasi pada seluruh kolom teks:
    * `Country` (7 nilai unik): `India`, `USA`, `Brazil`, `France`, `Egypt`, `China`, `Australia`.
    * `Category` (6 nilai unik): `Nature`, `Historical`, `Cultural`, `Beach`, `Adventure`, `Urban`.
    * `Accommodation_Available` (2 nilai unik): `Yes`, `No`.
* **Tindakan:**
  * Tetap menjalankan `.str.strip()` sebagai langkah preventif untuk memastikan kebersihan string.

### 5. Deteksi & Penanganan Outlier (*Outlier Detection*)
* **Inspeksi:** Menggunakan visualisasi Boxplot dan metode IQR (*Interquartile Range*: $Q_1 - 1.5 \times \text{IQR}$ hingga $Q_3 + 1.5 \times \text{IQR}$) pada seluruh variabel numerik.
* **Temuan:**
  * `Visitors`: **0 outlier** (Rentang nilai: `1.108` – `999.982`, Median: `500.831`).
  * `Rating`: **0 outlier** (Rentang nilai: `1,00` – `5,00`, Median: `3,00`).
  * `Revenue`: **0 outlier** (Rentang nilai: `1.025,81` – `999.999,49`, Median: `494.169,35`).
* **Tindakan:**
  * Seluruh observasi dipertahankan karena berada dalam batas distribusi yang wajar dan valid.

---

## 📊 Ringkasan Data Akhir (*Post-Cleaning*)

| Nama Kolom | Tipe Data Awal | Tipe Data Akhir | % Missing Values Pasca Cleaning | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| `Location` | `object` | `object` | 0% | ID unik lokasi (5.989 nilai unik) |
| `Country` | `object` | `category` | 0% | 7 negara unik, teks terstandarisasi |
| `Category` | `object` | `category` | 0% | 6 kategori wisata, teks terstandarisasi |
| `Visitors` | `int64` | `int64` | 0% | Lengkap, tidak ada outlier |
| `Rating` | `float64` | `float64` | 0% | Lengkap (skala 1.00–5.00), tidak ada outlier |
| `Revenue` | `float64` | `float64` | 0% | Lengkap, tidak ada outlier |
| `Accommodation_Available` | `object` | `category` | 0% | 2 nilai unik (`Yes`/`No`), teks terstandarisasi |

---

## 🛠️ Potongan Kode Utama yang Dijalankan

```python
import pandas as pd

# Memuat dataset
df = pd.read_csv('tourism_dataset.csv')

# 1. Pengecekan nilai kosong dan duplikat
print("Missing values:\n", df.isnull().sum())
print("Duplicates:", df.duplicated().sum())

# 2. Hapus duplikat (jika ada)
df = df.drop_duplicates()

# 3. Standarisasi Teks & Konversi Tipe Data Kategorikal
kolom_obj = df.select_dtypes(include=['object']).columns
for col in kolom_obj:
    df[col] = df[col].astype(str).str.strip()

kolom_kat = ['Country', 'Category', 'Accommodation_Available']
for col in kolom_kat:
    df[col] = df[col].astype('category')

# 4. Verifikasi akhir
print("\nInfo Dataset Pasca-Cleaning:")
print(df.info())
