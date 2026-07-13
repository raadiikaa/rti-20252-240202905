# Tahap 1 — Perancangan Arsitektur & Skema Database

**Status:** Selesai

---

## 1. Komponen Sistem

1. **Pipeline Klasifikasi Sentimen (Python, Google Colab)** — menerima dataset ulasan, menjalankan preprocessing, membentuk representasi TF-IDF, melatih dan mengevaluasi algoritma klasifikasi NB dan SVM secara terkontrol.
2. **Modul Preprocessor (PySastrawi)** — menjalankan pipeline preprocessing teks Bahasa Indonesia: lowercase → cleansing (hapus simbol/angka/emoji) → stopword removal → stemming. Dikunci konstan sebagai variabel kontrol.
3. **Modul Data Splitter (scikit-learn)** — membagi dataset 80:20 stratified per run dengan random_state dikunci. Split dilakukan **sebelum** TF-IDF untuk mencegah data leakage.
4. **Modul Vectorizer TF-IDF (scikit-learn)** — mengubah teks menjadi representasi vektor numerik dengan max_features=5.000. Di-**fit hanya pada training set**, lalu di-transform ke test set secara terpisah via sklearn Pipeline. Dikunci konstan sebagai variabel kontrol.
5. **Modul Classifier (scikit-learn)** — satu-satunya komponen yang berbeda antar kondisi eksperimen (variabel independen): kondisi A = MultinomialNB (alpha=1,0), kondisi B = SVC (kernel=linear, C=1,0).
6. **Modul Evaluator (scikit-learn metrics)** — menghasilkan F1-Score macro-average, Akurasi, Precision macro, Recall macro secara otomatis setiap run dan menyimpan ke CSV (variabel dependen).

## 2. Alur Resolusi Pipeline (Eksperimen)
        [ Dataset: 6.000 Ulasan Google Play Store (3 Aplikasi) ]
                                  │
                                  ▼
                [ Preprocessor (Control Variable) ]
       ┌───────────────────────────────────────────────────┐
       │ 1. Case Folding (Lowercase)                       │
       │ 2. Cleansing (Hapus simbol, angka, & emoji)       │
       │ 3. Stopword Removal                               │
       │ 4. Stemming (PySastrawi)                          │
       └───────────────────────────────────────────────────┘
                                  │
                                  ▼
             [ Data Splitter: 80:20 Stratified Split ]
             ┌───────────────────────────────────────┐
             │  • Train Set : 4.606 Ulasan (80%)     │
             │  • Test Set  : 1.152 Ulasan (20%)     │
             └───────────────────────────────────────┘
                                  │
                                  ▼
        [ Eksperimen Berulang: 10 Run (random_state 0-9) ]
                                  │
            ┌─────────────────────┴─────────────────────┐
            ▼                                           ▼
   [ Jalur Eksperimen A ]                      [ Jalur Eksperimen B ]
 ┌───────────────────────────┐               ┌───────────────────────────┐
 │ sklearn.pipeline          │               │ sklearn.pipeline          │
 ├───────────────────────────┤               ├───────────────────────────┤
 │ 1. TF-IDF Vectorizer      │               │ 1. TF-IDF Vectorizer      │
 │    (max_features=5.000)   │               │    (max_features=5.000)   │
 │    • .fit_transform(Train)│               │    • .fit_transform(Train)│
 │    • .transform(Test)     │               │    • .transform(Test)     │
 ├───────────────────────────┤               ├───────────────────────────┤
 │ 2. Klasifikator: MNB      │               │ 2. Klasifikator: SVC      │
 │    (MultinomialNB)        │               │    (Support Vector)       │
 │    • alpha = 1.0          │               │    • kernel = 'linear'    │
 │                           │               │    • C = 1.0              │
 └───────────────────────────┘               └───────────────────────────┘
            │                                           │
            └─────────────────────┬─────────────────────┘
                                  │
                                  ▼
                [ Evaluator (Dependent Variable) ]
       ┌───────────────────────────────────────────────────┐
       │  Metrik Evaluasi per Run:                         │
       │  • F1-Score   • Akurasi   • Precision   • Recall  │
       └───────────────────────────────────────────────────┘
                                  │
                                  ▼
                   [ Pengujian Hipotesis Akhir ]
       ┌───────────────────────────────────────────────────┐
       │  • Wilcoxon Signed-Rank Test (Signifikansi p-val) │
       │  • Cohen's d (Ukuran Efek / Effect Size)          │
       └───────────────────────────────────────────────────┘
                                  │
                                  ▼
                        [ Output & Artefak ]
       ┌───────────────────────────────────────────────────┐
       │  • results.csv (Data mentah 10 run)               │
       │  • grafik_perbandingan.png                        │
       └───────────────────────────────────────────────────┘
Catatan: pada mode baseline (NB), satu-satunya yang berbeda dari mode treatment (SVM) adalah komponen Classifier — semua komponen lain identik, memastikan variable isolation yang ketat.

## 3. Skema Dataset
dataset_ulasan_banking.csv (6.000 baris):

    nama_user    : string   — nama pengguna Google Play Store
    ulasan       : string   — teks ulasan berbahasa Indonesia
    rating       : integer  — rating bintang (1–5)
    tanggal      : datetime — tanggal ulasan ditulis
    aplikasi     : string   — BCA Mobile / Mandiri Online / BRImo
    sentimen     : string   — positif / netral / negatif (label dari rating bintang)

dataset_bersih.csv (5.758 baris setelah preprocessing):

    [semua kolom di atas]
    ulasan_bersih : string  — teks setelah preprocessing PySastrawi

## 4. Skema Output Eksperimen

| File | Lokasi | Isi |
|------|--------|-----|
| `hasil_perbandingan.csv` | `06-output/tables/` | F1-Score dan Akurasi NB vs SVM run tunggal (random_state=42) |
| `hasil_statistik.csv` | `06-output/tables/` | F1-Score NB dan SVM dari 10 run (random_state=0–9) + rata-rata + std. deviasi |
| `grafik_perbandingan.png` | `06-output/figures/` | Bar chart perbandingan F1-Score dan Akurasi (dpi=300) |
| `pipeline-klasifikasi.svg` | `01-proposal/`, `03-teori/` | Diagram arsitektur pipeline klasifikasi sentimen |

## 5. Keputusan Teknis (Final)

1. **Platform eksperimen:** Google Colab (Python 3.12) — gratis, cloud-based, reproducible tanpa setup lokal
2. **Mode eksperimen:** dua kondisi dalam satu notebook — kondisi A (NB) dan kondisi B (SVM) dijalankan pada konfigurasi identik, hanya Classifier yang berbeda
3. **Algoritma Baseline:** MultinomialNB (alpha=1,0) — paling umum di domain analisis sentimen mobile banking Indonesia (muncul di 4 dari 8 paper SLR)
4. **Algoritma Treatment:** SVC (kernel=linear, C=1,0) — kernel linear optimal untuk data teks TF-IDF berdimensi tinggi
5. **Preprocessing:** PySastrawi — library NLP khusus Bahasa Indonesia dengan stemmer dan stopword yang komprehensif
6. **Data Splitting:** dilakukan **sebelum** TF-IDF untuk mencegah data leakage — TF-IDF di-fit hanya pada training set via sklearn Pipeline
7. **Metrik primer:** F1-Score macro-average — robust terhadap class imbalance (positif 69,7% vs netral 4,6%)
8. **Replikasi:** 10 run dengan random_state=0–9 — memastikan stabilitas hasil
9. **Uji statistik:** Wilcoxon signed-rank test (non-parametrik) pada α = 0,05
10. **Effect size:** Cohen's d — mengukur besaran perbedaan praktis