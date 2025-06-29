# 📚 Course Segmentation Project (Clustering & Classification)
oleh **Rizqi Maulidi**

## 🧩 Deskripsi Proyek
Proyek ini bertujuan untuk melakukan segmentasi terhadap kursus-kursus dalam kategori *Development* dari situs Udemy menggunakan dua pendekatan utama:
1. **Clustering (Unsupervised Learning)** – Mengelompokkan kursus berdasarkan karakteristik tanpa label awal.
2. **Klasifikasi (Supervised Learning)** – Melatih model untuk mengenali pola dari hasil cluster, sehingga bisa mengklasifikasikan kursus baru ke dalam segmen yang sesuai.

Dataset ini berisi **13.608** kursus dari platform Udemy dan tersedia di Kaggle:
🔗 https://www.kaggle.com/datasets/jilkothari/finance-accounting-courses-udemy-13k-course

---

## 📂 Struktur File
- `[Clustering]_Submission_Akhir_BMLP_Rizqi Maulidi_(Updated).ipynb`  
  Notebook untuk proses segmentasi kursus dengan clustering.
- `[Klasifikasi]_Submission_Akhir_BMLP_Rizqi Maulidi.ipynb`  
  Notebook untuk membangun model klasifikasi dari hasil clustering.
- `Dataset_clustering.csv`  
  Data tidak berlabel untuk clustering.
- `udemy_output_All_Finance__Accounting_p1_p626.csv`  
  Data hasil clustering yang sudah memiliki label dan siap digunakan untuk metode klasifikasi.

---

## 🔍 Tahapan Proyek

### 🔹 1. Clustering

#### a. Persiapan Data
- Menghapus kolom tidak relevan seperti `course_url`, `instructor_name`, dll.
- Mengisi atau membuang nilai kosong.
- Encoding fitur kategorikal seperti `is_paid` (0: Gratis, 1: Berbayar).
- Scaling fitur numerik menggunakan `MinMaxScaler`.

#### b. Fitur yang Digunakan
- `is_paid`, `num_subscribers`, `avg_rating`, `num_reviews`, `num_published_lectures`, `num_published_practice_tests`, `discount_price__amount`

#### c. Pemodelan Clustering
- Algoritma: **KMeans**
- Eksperimen jumlah cluster menggunakan metode **Elbow** dan evaluasi dengan **Silhouette Score**.
- **Silhouette Score terbaik: 0.7824** (untuk 3 cluster)
- Jumlah data per cluster:
  - Cluster 0: 12.367 data
  - Cluster 1: 496 data
  - Cluster 2: 745 data

#### d. Karakteristik Tiap Cluster
- **Cluster 0 – Kursus Premium Populer**  
  Kursus berbayar, rating tinggi, banyak subscriber dan ulasan, harga premium.

- **Cluster 1 – Kursus Gratis Populer**  
  Kursus gratis yang banyak diikuti, rating cukup tinggi, namun materi terbatas.

- **Cluster 2 – Kursus Tidak Populer**  
  Kursus berbayar dengan rating & subscriber rendah. Potensi perbaikan konten/harga.

#### e. Output
- Hasil clustering disimpan ke CSV untuk digunakan dalam proses klasifikasi.

---

### 🔹 2. Klasifikasi

#### a. Persiapan Data
- Membaca dataset hasil clustering.
- Split data ke dalam train dan test set.
- Scaling menggunakan `MinMaxScaler`.

#### b. Model yang Digunakan
- **K-Nearest Neighbors (KNN)**
- **Support Vector Machine (SVM)**
- **Naive Bayes (NB)**

#### c. Evaluasi Awal dan Setelah Tuning

| Model                        | Accuracy Sebelum | Accuracy Sesudah | CV Mean Sebelum | CV Mean Sesudah |
|-----------------------------|------------------|------------------|------------------|------------------|
| KNN                         | 0.9989           | 1.0000           | 0.9979           | 0.9989           |
| SVM                         | 0.9978           | 1.0000           | 0.9969           | 0.9974           |
| Naive Bayes                 | 0.9963           | 0.9982           | 0.9904           | 0.9933           |

#### d. Analisis
- **KNN dan SVM** menunjukkan akurasi sempurna (100%) setelah tuning → indikasi kemungkinan **overfitting**.
- **Naive Bayes** lebih stabil, performa baik tanpa overfitting mencolok.

#### e. Rekomendasi
- Uji model pada data baru untuk memvalidasi generalisasi.
- Tinjau **Confusion Matrix** untuk analisis kesalahan per kelas.
- Eksplorasi metode lain seperti **Random Forest**, **XGBoost**, atau **Ensemble Learning**.
- Tambah volume data untuk meningkatkan ketahanan model.

---

## 🛠️ Tools & Library yang Digunakan
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `sklearn`: preprocessing, clustering, model selection, classification, metrics
- `scipy`, `plotly`, `PCA` untuk visualisasi

---

## 🚀 Cara Menjalankan Proyek
1. Jalankan notebook **Clustering** → simpan hasilnya ke CSV.
2. Jalankan notebook **Klasifikasi** → gunakan file CSV dari tahap sebelumnya.
3. Evaluasi performa dan lakukan tuning jika perlu.

---

## 📌 Kesimpulan
Proyek berhasil mengelompokkan kursus ke dalam segmen bermakna yang dapat dimanfaatkan untuk:
- Rekomendasi personal
- Strategi promosi dan monetisasi
- Peningkatan kualitas konten

Model klasifikasi menunjukkan performa tinggi, namun **pengujian lebih lanjut** diperlukan untuk memastikan tidak terjadi overfitting.
