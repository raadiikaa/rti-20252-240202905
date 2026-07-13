# 04-metodologi.md — Metodologi

## METODE

### Desain Penelitian

Penelitian ini menggunakan desain kuantitatif eksperimental komparatif dengan paradigma Design Science Research. Hipotesis yang diuji adalah H₀: tidak terdapat perbedaan signifikan F1-Score antara SVM dan Naive Bayes pada α = 0,05, dan H₁: SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes pada α = 0,05. Sampel sebanyak 6.000 ulasan diambil menggunakan teknik purposive sampling dari BCA Mobile, Mandiri Online, dan BRImo dengan kriteria inklusi ulasan berbahasa Indonesia periode 2022–2024, masing-masing ±2.000 ulasan per aplikasi.

### Variabel Penelitian

Variabel independen adalah jenis algoritma klasifikasi — Multinomial Naive Bayes vs SVM kernel linear. Variabel dependen primer adalah F1-Score macro-average, dipilih karena distribusi kelas sentimen tidak seimbang sehingga akurasi akan memberikan gambaran yang menyesatkan (Andrian et al., 2022). Variabel kontrol mencakup TF-IDF max_features=5.000, split 80:20 stratified, preprocessing identik, dan dataset yang sama untuk semua run.

### Pengumpulan Data dan Preprocessing

Data dikumpulkan melalui scraping Google Play Store menggunakan google-play-scraper dengan parameter lang='id', country='id', Sort.NEWEST, dan count=2.000 per aplikasi. Labeling sentimen dilakukan otomatis berdasarkan rating bintang: positif (4–5★), netral (3★), dan negatif (1–2★). Distribusi dataset: 4.184 ulasan positif (69,7%), 1.540 negatif (25,7%), dan 276 netral (4,6%). Pipeline preprocessing meliputi lowercase, penghapusan simbol dan angka, stopword removal dan stemming menggunakan PySastrawi, menghasilkan 5.758 ulasan valid.

### Arsitektur Pipeline dan Prosedur Eksperimen

Pipeline klasifikasi dibangun dengan lima komponen modular: Data Loader (CV), Preprocessor (CV), Vectorizer TF-IDF (CV), Classifier (IV — kondisi A: MultinomialNB alpha=1,0; kondisi B: SVC kernel linear C=1,0), dan Evaluator (DV). Sklearn Pipeline digunakan untuk memastikan TF-IDF hanya di-fit pada data training. Kedua kondisi dijalankan pada dataset dan konfigurasi yang identik, diulang 10 run dengan random_state=0–9. Analisis statistik menggunakan Wilcoxon signed-rank test (α = 0,05) dan Cohen's d. Eksperimen dijalankan di Google Colab dengan Python 3.12, scikit-learn 1.4.2, PySastrawi 1.0.1, scipy 1.13.0, dan matplotlib 3.8.4.

![Pipeline Klasifikasi Sentimen](pipeline-klasifikasi.png)
Gambar 1. Arsitektur Pipeline Klasifikasi Sentimen NB vs SVM