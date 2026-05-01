# 📊 HR Analytics: Employee Promotion Prediction

**Author:** Aldi Smart Nur Irfansyah  
**Role Target:** Machine Learning Engineer / Data Scientist  

## 📖 Ringkasan Proyek
Proyek ini bertujuan untuk membangun model *Machine Learning* yang dapat memprediksi kelayakan seorang karyawan untuk dipromosikan. Mengelola dan menganalisis data *Human Resources* (HR) adalah proses yang krusial untuk memastikan keputusan manajemen diambil secara objektif dan meritokratis. 

Dengan latar belakang keilmuan Teknik Informatika dan pengalaman mengolah data untuk kebutuhan operasional HR, proyek ini mendemonstrasikan end-to-end pipeline mulai dari *data cleaning*, analisis data eksploratif (EDA), hingga pemodelan algoritmik menggunakan pendekatan berorientasi bisnis.

## 🛠️ Teknologi & Library yang Digunakan
* **Bahasa Pemrograman:** Python
* **Data Manipulation:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn (Random Forest Classifier)

## 🗂️ Dataset
Dataset terdiri dari rekam jejak karyawan yang mencakup berbagai metrik seperti:
* Departemen dan wilayah kerja
* Tingkat pendidikan dan metrik demografis
* Skor rata-rata pelatihan (`avg_training_score`)
* Pemenuhan target KPI > 80% (`KPIs_met >80%`)
* Penilaian kinerja tahun sebelumnya (`previous_year_rating`)

*Dataset terbagi menjadi file latih (`train_LZdllcl.csv`) dan uji (`test_2umaH9m.csv`).*

## 🔍 Alur Kerja Proyek (Pipeline)

### 1. Data Cleaning & Preprocessing
Dataset mentah memiliki beberapa nilai yang hilang yang ditangani secara logis:
* `previous_year_rating`: Karyawan dengan masa kerja 1 tahun diisi dengan `0` (karena belum memiliki riwayat evaluasi tahunan).
* `education`: Diimputasi menggunakan nilai Modus ("Bachelor's").
* **Encoding**: Melakukan transformasi data kategorikal menjadi bentuk numerik menggunakan fitur kategorikal dari Pandas untuk konsistensi antara data *train* dan *test*.

### 2. Exploratory Data Analysis (EDA)
Analisis menunjukkan adanya ketidakseimbangan kelas (*imbalanced data*) yang ekstrem, di mana jumlah karyawan yang tidak dipromosikan jauh lebih besar dibandingkan yang dipromosikan.

> `<img width="656" height="432" alt="image" src="https://github.com/user-attachments/assets/9bda39f4-29e5-4e2b-984c-d586cde1d78c" />

`

Selain itu, karyawan yang dipromosikan secara konsisten memiliki skor pelatihan rata-rata yang jauh lebih tinggi.

> `<img width="632" height="430" alt="image" src="https://github.com/user-attachments/assets/652bb09e-97ef-4e1e-97fa-d96352d61394" />

`

### 3. Pemodelan Machine Learning
Model yang dipilih adalah **Random Forest Classifier**. Mengingat data target sangat tidak seimbang, parameter `class_weight='balanced'` diterapkan. 

Tujuan utama dari model ini bukanlah sekadar mengejar tingkat Akurasi secara buta, melainkan **memaksimalkan nilai Recall** pada kelas minoritas (karyawan yang dipromosikan). 

> `<img width="480" height="361" alt="image" src="https://github.com/user-attachments/assets/48209a5f-a63c-420d-a0ee-a86d1aec5bc1" />

`

**Hasil Evaluasi:**
Model secara agresif mengidentifikasi kandidat yang layak promosi, menghasilkan nilai **Recall 84%**. Dalam konteks bisnis HR, lebih baik meninjau sedikit lebih banyak kandidat (mengorbankan *Precision*) daripada secara tidak sengaja melewatkan talenta unggul di dalam perusahaan (*False Negatives* rendah).

### 4. Feature Importance (Faktor Penentu Promosi)
Model mengekstraksi faktor-faktor yang paling krusial bagi manajemen dalam mengambil keputusan promosi.

> `<img width="894" height="502" alt="image" src="https://github.com/user-attachments/assets/4b90b9f2-4200-4e6a-9d89-e1de21d5f061" />

`

**Insight Bisnis:**
1. **KPI > 80%**: Memenuhi target kinerja harian/bulanan adalah syarat mutlak peringkat pertama.
2. **Skor Pelatihan**: Kesiapan teknis memegang peranan krusial untuk mengisi jabatan di tingkat selanjutnya.
3. **Rating Tahun Sebelumnya**: Konsistensi kinerja dari tahun ke tahun sangat dihargai.
Hal ini membuktikan bahwa lingkungan kerja pada dataset ini berjalan secara meritokratis, mengesampingkan faktor demografis seperti gender atau jalur rekrutmen.

## 🚀 Kesimpulan
Model berhasil memetakan pola promosi karyawan dengan sangat baik berdasarkan kinerja nyata. Proyek ini siap digunakan sebagai basis otomasi atau sistem pendukung keputusan (DSS) bagi departemen HRD untuk menyeleksi kandidat promosi dengan lebih cepat, adil, dan berbasis data (*data-driven*).
