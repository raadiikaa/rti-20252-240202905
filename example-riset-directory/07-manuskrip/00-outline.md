# 00-outline.md — Outline & Peta Sumber Naskah

**Judul:** Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

**Target jurnal:** TIIJ (Technology and Informatics Insight Journal), Universitas Putra Bangsa — Sinta 5 (https://jurnal.universitasputrabangsa.ac.id/index.php/tiij)

---

## Struktur Naskah

| Bagian | File | Status |
|--------|------|--------|
| Abstrak (ID & EN) | [01-abstrak.md](01-abstrak.md) | 🔲 Draft |
| 1 Pendahuluan | [02-pendahuluan.md](02-pendahuluan.md) | 🔲 Draft |
| 2 Tinjauan Pustaka | [03-tinjauan-pustaka.md](03-tinjauan-pustaka.md) | 🔲 Draft |
| 3 Metodologi | [04-metodologi.md](04-metodologi.md) | 🔲 Draft |
| 4 Hasil & Analisis | [05-hasil-analisis.md](05-hasil-analisis.md) | 🔲 Draft |
| 5 Kesimpulan | [06-kesimpulan.md](06-kesimpulan.md) | 🔲 Draft |
| Daftar Pustaka | [07-daftar-pustaka.md](07-daftar-pustaka.md) | 🔲 Draft |

---

## Peta Sumber per Bagian

| Bagian | Sumber Utama |
|--------|-------------|
| 1 Pendahuluan | proposal-penelitian.md §D.1, WS-02, WS-03 |
| 2 Tinjauan Pustaka | WS-03, matriks-literatur.md, daftar-pustaka.bib |
| 3 Metodologi | proposal-penelitian.md §E, WS-05, WS-06, WS-07, WS-09 |
| 4 Hasil & Analisis | hasil_perbandingan.csv, hasil_statistik.csv, grafik_perbandingan.png |
| 5 Kesimpulan | hasil_statistik.csv, proposal-penelitian.md §F |
| Daftar Pustaka | daftar-pustaka.bib (11 entri) |

---

## Klaim Kunci yang Harus Konsisten

| Klaim | Nilai | Sumber |
|-------|-------|--------|
| Total dataset | 6.000 ulasan | dataset_ulasan_banking.csv |
| Ulasan per aplikasi | 2.000 | dataset_ulasan_banking.csv |
| Data valid setelah preprocessing | 5.758 | dataset_bersih.csv |
| Distribusi positif | 4.184 (69,7%) | dataset_ulasan_banking.csv |
| Distribusi negatif | 1.540 (25,7%) | dataset_ulasan_banking.csv |
| Distribusi netral | 276 (4,6%) | dataset_ulasan_banking.csv |
| TF-IDF max_features | 5.000 | notebook Cell 11 |
| Split | 80:20 stratified | notebook Cell 11 |
| Data training | 4.606 | notebook Cell 11 |
| Data testing | 1.152 | notebook Cell 11 |
| F1-Score NB (run tunggal) | 0,5466 | hasil_perbandingan.csv |
| F1-Score SVM (run tunggal) | 0,5553 | hasil_perbandingan.csv |
| Akurasi NB (run tunggal) | 0,8385 | hasil_perbandingan.csv |
| Akurasi SVM (run tunggal) | 0,8455 | hasil_perbandingan.csv |
| Rata-rata F1 NB (10 run) | 0,5532 | hasil_statistik.csv |
| Rata-rata F1 SVM (10 run) | 0,5627 | hasil_statistik.csv |
| p-value Wilcoxon | 0,0039 | notebook Cell 19 |
| Cohen's d | 1,9428 | notebook Cell 19 |
| Jumlah paper SLR | 8 paper final dari 89 | WS-03, matriks-literatur.md |
| α signifikansi | 0,05 | WS-04, proposal |

---

## Catatan Konsistensi

- Semua angka di atas harus identik di setiap bagian naskah
- Nama algoritma: **Naive Bayes** (bukan NaiveBayes/naive bayes) dan **Support Vector Machine** / **SVM**
- Nama aplikasi: **BCA Mobile**, **Mandiri Online**, **BRImo** (kapital konsisten)
- Metrik utama selalu disebut **F1-Score macro-average**
- Uji statistik selalu disebut **Wilcoxon signed-rank test**