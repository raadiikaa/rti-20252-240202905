# 05-kode

Source code implementasi eksperimen — notebook Google Colab untuk scraping, preprocessing, training, evaluasi, dan analisis statistik.

## Struktur
05-kode/

└── NB_vs_SVM_Sentiment_MobileBanking.ipynb  # notebook utama eksperimen

## Berkas

- [NB_vs_SVM_Sentiment_MobileBanking.ipynb](NB_vs_SVM_Sentiment_MobileBanking.ipynb) — notebook Google Colab lengkap (17 cell): scraping Google Play Store → preprocessing PySastrawi → TF-IDF → training NB & SVM → evaluasi → 10 run → Wilcoxon + Cohen's d → download output

## Cara Menjalankan

1. Buka [Google Colab](https://colab.research.google.com)
2. Upload file `NB_vs_SVM_Sentiment_MobileBanking.ipynb`
3. Jalankan instalasi dependency terlebih dahulu:
!pip install google-play-scraper

!pip install PySastrawi
4. Jalankan semua cell secara berurutan dari Cell 1 sampai Cell 17
5. **PENTING:** Restart kernel sebelum menjalankan ulang agar tidak ada state tersimpan

## Dependency

| Library | Version | Instalasi |
|---------|---------|-----------|
| google-play-scraper | 1.2.7 | `!pip install google-play-scraper` |
| PySastrawi | 1.0.1 | `!pip install PySastrawi` |
| scikit-learn | 1.4.2 | sudah tersedia di Colab |
| pandas | 2.2.1 | sudah tersedia di Colab |
| numpy | 1.26.4 | sudah tersedia di Colab |
| scipy | 1.13.0 | sudah tersedia di Colab |
| matplotlib | 3.8.4 | sudah tersedia di Colab |

## Struktur Cell

| Cell | Tahap | Fungsi |
|------|-------|--------|
| 1 | Setup | Install google-play-scraper |
| 2 | Setup | Import semua library |
| 3 | Scraping | Scraping BCA Mobile (com.bca) → 2.000 ulasan |
| 4 | Scraping | Scraping Mandiri Online (com.bankmandiri.mandirionline) → 2.000 ulasan |
| 5 | Scraping | Scraping BRImo (id.co.bri.brimo) → 2.000 ulasan |
| 6 | Scraping | Gabung + labeling sentimen + simpan dataset_ulasan_banking.csv |
| 7 | Scraping | Download dataset_ulasan_banking.csv |
| 8 | Preprocessing | Install PySastrawi + definisi fungsi preprocessing |
| 9 | Preprocessing | Load CSV + jalankan preprocessing |
| 10 | Preprocessing | Simpan dataset_bersih.csv |
| 11 | Eksperimen | TF-IDF vectorizer + split 80:20 stratified |
| 12 | Eksperimen | Training + evaluasi Naive Bayes |
| 13 | Eksperimen | Training + evaluasi SVM |
| 14 | Eksperimen | Tabel perbandingan + simpan hasil_perbandingan.csv |
| 15 | Eksperimen | Visualisasi bar chart + simpan grafik_perbandingan.png |
| 16 | Analisis | 10 run eksperimen NB vs SVM |
| 17 | Analisis | Wilcoxon test + Cohen's d + simpan hasil_statistik.csv + download semua output |

## Output yang Dihasilkan

| File | Deskripsi |
|------|-----------|
| dataset_ulasan_banking.csv | Data mentah ±6.000 ulasan |
| dataset_bersih.csv | Data setelah preprocessing |
| hasil_perbandingan.csv | F1-Score dan Akurasi NB vs SVM (run tunggal) |
| hasil_statistik.csv | F1-Score NB dan SVM dari 10 run |
| grafik_perbandingan.png | Bar chart perbandingan (dpi=300) |