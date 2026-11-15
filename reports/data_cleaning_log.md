🧹 Log Pembersihan & Pra-pemrosesan Data (Data Cleaning & Preprocessing Log)Dokumen ini mencatat seluruh tahapan inspeksi, identifikasi masalah data, keputusan pembersihan, serta transformasi data yang dilakukan pada tourism_dataset.csv sebelum memasuki tahap Analisis Data Eksplorasi (EDA).📌 Ringkasan Data AwalNama File Dataset: tourism_dataset.csvJumlah Baris (Awal): 5,989 barisJumlah Kolom (Awal): 7 kolomTipe Data: Kombinasi Numerik (int64, float64) dan Kategorikal (object/string).🔍 Tahapan Inspeksi & Pembersihan Data1. Pengecekan & Penanganan Nilai Hilang (Missing Values)Inspeksi: Menjalankan df.isnull().sum() untuk mengidentifikasi keberadaan nilai kosong di setiap kolom.Temuan:Tidak ditemukan nilai kosong (0 missing values) pada seluruh kolom dalam dataset.Tindakan:Tidak diperlukan proses imputasi atau penghapusan baris karena seluruh data telah lengkap. (Catatan: Script imputasi menggunakan nilai Median untuk variabel numerik dan Modus untuk variabel kategorikal tetap disertakan pada pipeline sebagai langkah pencegahan).2. Pengecekan & Penanganan Data Duplikat (Duplicate Records)Inspeksi: Menjalankan df.duplicated().sum() untuk mengecek baris yang terduplikasi secara keseluruhan maupun berdasarkan ID unik.Temuan: Terdeteksi 0 baris duplikat secara keseluruhan.Tindakan: Menjalankan df.drop_duplicates(inplace=True) untuk memastikan integritas dan keunikan setiap baris data tetap terjaga.3. Penyesuaian Tipe Data (Data Types Conversion)Inspeksi: Menjalankan df.dtypes dan df.info() untuk memverifikasi kesesuaian tipe data pada tiap kolom.Tindakan:Memastikan kolom identifier (Location) tetap bertipe object agar tidak ikut terhitung dalam kalkulasi statistik numerik.Mengonversi kolom kategorikal (Country, Category, Accommodation_Available) menjadi tipe category untuk efisiensi penggunaan memori saat proses analisis.4. Penanganan Format & Konsistensi Teks (Text Standardization)Inspeksi: Pengecekan nilai unik pada kolom kategorikal menggunakan df[col].unique() untuk mendeteksi typo, spasi berlebih, atau perbedaan kapitalisasi.Tindakan:Menghilangkan spasi berlebih di awal maupun akhir teks menggunakan .str.strip().Menyeragamkan format penulisan huruf menggunakan .str.title() agar seluruh kategori dan nama negara konsisten.5. Deteksi & Penanganan Outlier (Outlier Detection)Inspeksi: Menggunakan visualisasi Boxplot dan metode IQR (Interquartile Range) pada variabel numerik (Visitors, Rating, dan Revenue).Temuan: Outlier teridentifikasi pada variabel Revenue dan Visitors, namun tetap dipertahankan tanpa penghapusan maupun capping karena merepresentasikan variasi alami dari destinasi wisata populer dengan tingkat kunjungan tinggi.📊 Ringkasan Data Akhir (Post-Cleaning)Nama KolomTipe Data AwalTipe Data Akhir% Missing Values Pasca CleaningKeteranganLocationobjectobject0%ID/Nama unik lokasi (teks distandarisasi)Countryobjectcategory0%Nama negara (teks distandarisasi)Categoryobjectcategory0%Kategori wisata (teks distandarisasi)Visitorsint64int640%Jumlah pengunjung (variasi alami dipertahankan)Ratingfloat64float640%Skor penilaian destinasiRevenuefloat64float640%Pendapatan wisata (variasi alami dipertahankan)Accommodation_Availableobjectcategory0%Ketersediaan akomodasi (Yes/No)🛠️ Potongan Kode Utama yang Dijalankanimport pandas as pd

# Memuat dataset
df = pd.read_csv('tourism_dataset.csv')

# 1. Pengecekan dimensi, nilai kosong, dan duplikat
print(f"Dimensi Awal: {df.shape}")
print("Missing values:\n", df.isnull().sum())
print("Duplicates:", df.duplicated().sum())

# 2. Hapus duplikat
df = df.drop_duplicates()

# 3. Imputasi nilai kosong pada variabel numerik dengan median (jika ada)
kolom_num = df.select_dtypes(include=['number']).columns
for col in kolom_num:
    if df[col].isnull().sum() > 0:
        df[col] = df[col].fillna(df[col].median())

# 4. Standarisasi Teks & Konversi Tipe Data Kategorikal
kolom_obj = df.select_dtypes(include=['object']).columns
for col in kolom_obj:
    if df[col].isnull().sum() > 0:
        df[col] = df[col].fillna(df[col].mode()[0])
    df[col] = df[col].astype(str).str.strip()

kolom_kat = ['Country', 'Category', 'Accommodation_Available']
for col in kolom_kat:
    if col in df.columns:
        df[col] = df[col].astype('category')

print("\nPembersihan data selesai. Dimensi Akhir:", df.shape)
