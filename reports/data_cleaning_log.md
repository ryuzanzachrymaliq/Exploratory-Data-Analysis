# 🧹 Log Pembersihan & Pra-pemrosesan Data (Data Cleaning & Preprocessing Log)

Dokumen ini mencatat seluruh tahapan inspeksi, identifikasi masalah data, keputusan pembersihan, serta transformasi data yang dilakukan pada `tourism_dataset.csv` sebelum tahap analisis eksplorasi (EDA).

---

## 📌 Ringkasan Data Awal

- **Nama File Dataset:** `tourism_dataset.csv`
- **Jumlah Baris (Awal):** *[Isi dengan jumlah baris awal, contoh: 1,000]*
- **Jumlah Kolom (Awal):** *[Isi dengan jumlah kolom awal, contoh: 8]*
- **Tipe Data:** Kombinasi Numerik (Integer/Float) dan Kategorikal (Object/String).

---

## 🔍 Tahapan Inspeksi & Pembersihan Data

### 1. Pengecekan & Penanganan Nilai Hilang (*Missing Values*)
* **Inspeksi:** Menjalankan `df.isnull().sum()` untuk mengidentifikasi keberadaan nilai kosong di setiap kolom.
* **Temuan:** 
  * *[Contoh: Kolom 'Rating' memiliki 5 nilai kosong]*
  * *[Contoh: Kolom 'Kategori' tidak memiliki nilai kosong]*
* **Tindakan:**
  * Untuk variabel numerik: Imputasi menggunakan nilai **Median** (apabila terdapat skewed distribution/outlier) atau **Mean**.
  * Untuk variabel kategorikal: Imputasi menggunakan **Modus** (nilai paling sering muncul) atau dilabeli sebagai `'Unknown'`.

### 2. Pengecekan & Penanganan Data Duplikat (*Duplicate Records*)
* **Inspeksi:** Menjalankan `df.duplicated().sum()` untuk mengecek baris ganda.
* **Temuan:** Terdeteksi *[0 / X]* baris duplikat secara keseluruhan.
* **Tindakan:** `df.drop_duplicates(inplace=True)` dijalankan untuk menghapus data yang terduplikasi (jika ada).

### 3. Penyesuaian Tipe Data (*Data Types Conversion*)
* **Inspeksi:** Menjalankan `df.dtypes` dan `df.info()`.
* **Tindakan:**
  * Memastikan kolom identifier (seperti `Location_ID`) diubah menjadi tipe `object` atau disisihkan agar tidak mengganggu kalkulasi statistik numerik.
  * Mengonversi kolom teks/kategori ke tipe `category` untuk efisiensi memori (opsional).

### 4. Penanganan Format & Konsistensi Teks (*Text Standardization*)
* **Inspeksi:** Pengecekan nilai unik pada kolom kategorikal menggunakan `df[col].unique()`.
* **Tindakan:**
  * Menghilangkan spasi berlebih di awal/akhir string menggunakan `.str.strip()`.
  * Mengubah huruf menjadi *lowercase* / *titlecase* agar format entri data seragam.

### 5. Deteksi & Penanganan Outlier (*Outlier Detection*)
* **Inspeksi:** Menggunakan visualisasi **Boxplot** dan metode IQR (*Interquartile Range*) pada variabel numerik.
* **Temuan:** Outlier diidentifikasi pada variabel *[Sebutkan kolom numerik jika ada]* tetapi tetap dipertahankan / di-cap (*capping*) karena merupakan variasi data yang valid.

---

## 📊 Ringkasan Data Akhir (Post-Cleaning)

| Nama Kolom | Tipe Data Awal | Tipe Data Akhir | % Missing Values Pasca Cleaning | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| `Location_ID` | int64 / object | object | 0% | ID unik lokasi |
| `[Nama_Kolom_2]` | float64 | float64 | 0% | Imputasi median |
| `[Nama_Kolom_3]` | object | category | 0% | Teks distandarisasi |

---

## 🛠️ Potongan Kode Utama yang Dijalankan

```python
# 1. Pengecekan nilai kosong dan duplikat
print("Missing values:\n", df.isnull().sum())
print("Duplicates:", df.duplicated().sum())

# 2. Hapus duplikat
df = df.drop_duplicates()

# 3. Imputasi nilai kosong pada variabel numerik dengan median
kolom_num = df.select_dtypes(include=['number']).columns
for col in kolom_num:
  if df[col].isnull().sum() > 0:
    df[col].fillna(df[col].median(), inplace=True)

# 4. Standarisasi Teks
kolom_obj = df.select_dtypes(include=['object']).columns
for col in kolom_obj:
  df[col] = df[col].astype(str).str.strip()
```

---
*Log ini diperbarui secara otomatis sesuai dengan alur pra-pemrosesan notebook EDA.*