# Tahap 4 — Ekstraksi Data & Visualisasi

**Status:** Selesai (2026-05-12, ~15:53–16:00 WIB)
**Bergantung pada:** [tahap-3-pengumpulan-data-preprocessing.md](tahap-3-pengumpulan-data-preprocessing.md)
**Lokasi kode:** [../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb](../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb) Cell 11–17
**Lokasi output:** [../06-output/](../06-output/)

---

## Tujuan

Menjalankan eksperimen perbandingan NB vs SVM pada kondisi identik, menganalisis hasil secara statistik, dan menghasilkan tabel serta visualisasi untuk naskah jurnal.

## Deliverable

- [x] TF-IDF vectorizer + split 80:20 stratified — split **sebelum** fit TF-IDF (Cell 11)
- [x] Training + evaluasi MultinomialNB — F1=0,5466, Akurasi=0,8385 (Cell 12)
- [x] Training + evaluasi SVC linear — F1=0,5553, Akurasi=0,8455 (Cell 13)
- [x] Tabel perbandingan + simpan `hasil_perbandingan.csv` (Cell 14)
- [x] Visualisasi bar chart + simpan `grafik_perbandingan.png` dpi=300 (Cell 15)
- [x] 10 run eksperimen NB vs SVM (random_state=0–9) (Cell 16)
- [x] Wilcoxon signed-rank test + Cohen's d + simpan `hasil_statistik.csv` + download semua output (Cell 17)
- [x] Output tabel: [../06-output/tables/](../06-output/tables/)
- [x] Output figure: [../06-output/figures/](../06-output/figures/)

## Desain yang Diimplementasikan

### Modul Analisis

| Cell | Fungsi | Output |
|------|--------|--------|
| Cell 11 | TF-IDF fit pada train + split 80:20 stratified | X_train, X_test, y_train, y_test |
| Cell 12 | Training + evaluasi MultinomialNB (run tunggal) | F1=0,5466, Akurasi=0,8385 |
| Cell 13 | Training + evaluasi SVC linear (run tunggal) | F1=0,5553, Akurasi=0,8455 |
| Cell 14 | Tabel perbandingan run tunggal | `hasil_perbandingan.csv` |
| Cell 15 | Bar chart perbandingan | `grafik_perbandingan.png` |
| Cell 16 | 10 run loop (random_state=0–9) | List F1 NB dan SVM per run |
| Cell 17 | Wilcoxon + Cohen's d + download | `hasil_statistik.csv` + semua file output |

### Definisi Metrik

**F1-Score macro-average** dipilih sebagai metrik primer karena distribusi kelas tidak seimbang — positif 69,7% vs netral 4,6%. Akurasi menyesatkan pada kondisi imbalance ini.

**Wilcoxon signed-rank test** dipilih karena non-parametrik dan cocok untuk n=10 run berpasangan (distribusi F1 tidak dapat diasumsikan normal).

**Cohen's d** mengukur besaran perbedaan praktis di luar signifikansi statistik: d > 0,8 = large effect.

## Hasil

### Hasil Run Tunggal (random_state=42)

| Algoritma | F1-Score | Akurasi |
|-----------|----------|---------|
| Naive Bayes | 0,5466 | 0,8385 |
| SVM | 0,5553 | 0,8455 |
| Selisih | +0,0087 | +0,0070 |

### Hasil 10 Run Eksperimen

| Run | F1 Naive Bayes | F1 SVM |
|-----|----------------|--------|
| 1 | 0,5542 | 0,5601 |
| 2 | 0,5578 | 0,5691 |
| 3 | 0,5460 | 0,5541 |
| 4 | 0,5599 | 0,5595 |
| 5 | 0,5496 | 0,5617 |
| 6 | 0,5558 | 0,5648 |
| 7 | 0,5544 | 0,5666 |
| 8 | 0,5589 | 0,5671 |
| 9 | 0,5456 | 0,5643 |
| 10 | 0,5495 | 0,5594 |
| **Rata-rata** | **0,5532** | **0,5627** |
| **Std. Deviasi** | **0,0052** | **0,0045** |

SVM menghasilkan F1-Score lebih tinggi pada 9 dari 10 run (pengecualian: Run 4, selisih 0,0004).

### Analisis Statistik

| Parameter | Nilai | Interpretasi |
|-----------|-------|-------------|
| p-value (Wilcoxon) | 0,0039 | p < α = 0,05 → H₀ ditolak |
| Cohen's d | 1,9428 | Large effect (d > 0,8) |

### Catatan untuk Tahap 5

- F1-Score moderat mencerminkan tantangan class imbalance (positif 69,7% vs netral 4,6%) — bukan kelemahan algoritma → relevan untuk bagian "Pembahasan" dan "Limitasi" naskah
- Akurasi tinggi vs F1-Score moderat memvalidasi pemilihan F1-Score macro-average sebagai metrik primer
- Semua angka di atas adalah klaim kunci yang harus konsisten di seluruh naskah — lihat [../07-manuskrip/00-outline.md](../07-manuskrip/00-outline.md)

## Catatan Lingkungan

- Waktu total eksperimen + analisis statistik: ~7 menit (15:53–16:00 WIB)
- Sklearn Pipeline memastikan TF-IDF hanya di-fit pada training set — tidak ada data leakage
- Import NLTK tidak digunakan di notebook — sebaiknya dihapus untuk clarity