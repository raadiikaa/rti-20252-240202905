# Tahap 2 — Implementasi Pipline Klasifikasi (Phyton)

**Status:** Selesai
**Acuan arsitektur:** [tahap-1-arsitektur-dan-skema-database.md](tahap-1-arsitektur-dan-skema-database.md)
**Lokasi kode:** [../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb](../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb)

---

## Tujuan

Mengimplementasikan pipeline klasifikasi sentimen lengkap dalam satu notebook Google Colab yang mendukung dua kondisi eksperimen:

- **Kondisi A** — baseline: MultinomialNB (alpha=1,0) + TF-IDF
- **Kondisi B** — treatment: SVC kernel linear (C=1,0) + TF-IDF

## Deliverable

- [x] Cell 1: Instalasi google-play-scraper
- [x] Cell 2: Import semua library (pandas, numpy, sklearn, PySastrawi, scipy, matplotlib)
- [x] Cell 3: Scraping BCA Mobile (com.bca) → 2.000 ulasan
- [x] Cell 4: Scraping Mandiri Online (com.bankmandiri.mandirionline) → 2.000 ulasan
- [x] Cell 5: Scraping BRImo (id.co.bri.brimo) → 2.000 ulasan
- [x] Cell 6: Gabung + labeling sentimen + simpan `dataset_ulasan_banking.csv`
- [x] Cell 7: Download `dataset_ulasan_banking.csv`
- [x] Cell 8: Instalasi PySastrawi + definisi fungsi preprocessing
- [x] Cell 9: Load CSV + jalankan preprocessing (lowercase → cleansing → stopword → stemming)
- [x] Cell 10: Simpan `dataset_bersih.csv`
- [x] Cell 11: TF-IDF vectorizer + split 80:20 stratified (split **sebelum** fit TF-IDF)
- [x] Cell 12: Training + evaluasi MultinomialNB
- [x] Cell 13: Training + evaluasi SVC linear
- [x] Cell 14: Tabel perbandingan + simpan `hasil_perbandingan.csv`
- [x] Cell 15: Visualisasi bar chart + simpan `grafik_perbandingan.png`
- [x] Cell 16: 10 run eksperimen NB vs SVM (random_state=0–9)
- [x] Cell 17: Wilcoxon test + Cohen's d + simpan `hasil_statistik.csv` + download semua output

## Desain yang Diimplementasikan

### Struktur Notebook (`05-kode/`)
05-kode/

└── NB_vs_SVM_Sentiment_MobileBanking.ipynb
├── Cell 1–2   : Setup (install + import)
├── Cell 3–7   : Pengumpulan data (scraping + labeling + simpan)
├── Cell 8–10  : Preprocessing (PySastrawi + simpan bersih)
├── Cell 11    : Vektorisasi + split (TF-IDF fit pada train saja)
├── Cell 12–15 : Eksperimen run tunggal (NB + SVM + perbandingan + grafik)
└── Cell 16–17 : 10 run + analisis statistik + download output

### Konfigurasi Parameter

```python
# TF-IDF
max_features = 5000

# Split (dilakukan SEBELUM fit TF-IDF)
test_size    = 0.2
stratify     = y
random_state = 42  # run tunggal

# Naive Bayes (Kondisi A)
alpha        = 1.0

# SVM (Kondisi B)
kernel       = 'linear'
C            = 1.0
random_state = 42

# 10 run eksperimen
random_state = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### Pencegahan Data Leakage

sklearn Pipeline digunakan untuk memastikan TF-IDF hanya di-fit pada training set:

```python
Pipeline([
    ('tfidf', TfidfVectorizer(max_features=5000)),
    ('clf', MultinomialNB(alpha=1.0))
])
# fit() hanya pada X_train → transform otomatis pada X_test secara terpisah
```

## Hasil Verifikasi End-to-End

Diverifikasi manual via eksekusi notebook di Google Colab (2026-05-12):

- **Scraping:** BCA Mobile ✅ 2.000 ulasan, Mandiri Online ✅ 2.000 ulasan, BRImo ✅ 2.000 ulasan
- **Preprocessing:** 6.000 → 5.758 ulasan valid (242 dihapus karena kosong setelah preprocessing)
- **Distribusi:** positif 4.184 (69,7%), negatif 1.540 (25,7%), netral 276 (4,6%)
- **Run tunggal NB:** F1=0,5466, Akurasi=0,8385 ✅
- **Run tunggal SVM:** F1=0,5553, Akurasi=0,8455 ✅
- **10 run NB rata-rata:** F1=0,5532 ✅
- **10 run SVM rata-rata:** F1=0,5627 ✅
- **Wilcoxon p-value:** 0,0039 (H₀ ditolak) ✅
- **Cohen's d:** 1,9428 (large effect) ✅
- **Output file:** semua 5 file berhasil didownload ✅

## Catatan Lingkungan

- Seluruh eksperimen dijalankan di Google Colab (Python 3.12) via browser di laptop HP 14s-dq5156TU, Windows 11
- Library yang diinstall manual: `google-play-scraper==1.2.7`, `PySastrawi==1.0.1` — sisanya sudah tersedia di Colab default
- Import NLTK di awal notebook tidak digunakan — preprocessing menggunakan PySastrawi. Sebaiknya dihapus untuk menghindari kebingungan peneliti lain
- Kernel di-restart sebelum setiap repeatability test agar tidak ada state tersimpan dari sesi sebelumnya
- requirements.txt belum dibuat — versi library terdokumentasi di [../09-docs/tahap-1-arsitektur-dan-skema-database.md](tahap-1-arsitektur-dan-skema-database.md) dan [../07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md)