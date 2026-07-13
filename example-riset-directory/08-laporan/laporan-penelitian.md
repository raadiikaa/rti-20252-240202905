# Laporan Penelitian

**Judul:** Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

**Peneliti:** Radika Rismawati Tri Prasaja — 240202905
**Target Publikasi:** TIIJ (Technology and Informatics Insight Journal), Universitas Putra Bangsa — Sinta 5 (https://jurnal.universitasputrabangsa.ac.id/index.php/tiij)
**Status Penelitian:** Tahap 1–7 selesai ([../07-manuskrip/](../07-manuskrip/))

---

## 1. Ringkasan Eksekutif

Penelitian ini membandingkan performa Multinomial Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF untuk klasifikasi sentimen ulasan aplikasi mobile banking Indonesia di Google Play Store. Eksperimen dilakukan secara terkontrol menggunakan pipeline klasifikasi modular dengan lima komponen, diuji pada dataset 6.000 ulasan dari tiga aplikasi mobile banking terbesar Indonesia (BCA Mobile, Mandiri Online, BRImo) dengan 10 run menggunakan random seed berbeda, dan perbedaan performa diverifikasi menggunakan Wilcoxon signed-rank test dan effect size Cohen's d.

**Temuan utama:**

- SVM menghasilkan rata-rata F1-Score macro-average **0,5627** dibandingkan Naive Bayes **0,5532** dari 10 run eksperimen.
- Perbedaan terbukti **signifikan secara statistik** dengan Wilcoxon signed-rank test (p = 0,0039 < α = 0,05).
- Effect size Cohen's d = **1,9428** mengindikasikan large effect — perbedaan bermakna secara praktis.
- H₀ ditolak — **SVM direkomendasikan** sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

Seluruh kode, dataset, dan hasil analisis tersedia di repository ini (lihat §7 Lampiran untuk peta artefak).

---

## 2. Latar Belakang dan Rumusan Masalah

### 2.1 Latar Belakang

Aplikasi mobile banking di Indonesia mengalami pertumbuhan signifikan, dengan jutaan nasabah BCA, Bank Mandiri, dan BRI aktif memberikan ulasan di Google Play Store. Ulasan-ulasan ini mengandung keluhan, pujian, dan saran yang berpotensi menjadi sumber insight strategis bagi tim pengembang untuk memahami persepsi pengguna secara real-time (Prasetyo & Agastya, 2024). Namun, inkonsistensi pemilihan algoritma klasifikasi sentimen antar studi — tanpa kondisi perbandingan yang terkontrol dan tanpa verifikasi statistik — menyebabkan tim pengembang memilih algoritma secara ad-hoc tanpa panduan berbasis bukti yang kontekstual (Al Hakim & Irwiensyah, 2024).

Systematic literature review pada database IEEE Xplore, Scopus, ACM Digital Library, dan Google Scholar periode 2020–2025 menghasilkan 8 paper final dari 89 paper awal. Analisis terhadap 8 paper tersebut mengidentifikasi gap utama: tidak ada satupun studi yang membandingkan Naive Bayes dan SVM dengan kondisi eksperimen identik pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store, sekaligus disertai uji statistik signifikansi.

### 2.2 Rumusan Masalah

Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

### 2.3 Tujuan Penelitian

Menghasilkan perbandingan empiris yang rigorous antara Naive Bayes dan SVM untuk klasifikasi sentimen ulasan mobile banking berbahasa Indonesia, dengan kondisi eksperimen sepenuhnya terkontrol dan disertai uji statistik signifikansi, sehingga hasilnya dapat dijadikan panduan berbasis bukti bagi tim pengembang.

Detail proposal penelitian: [../01-proposal/proposal-penelitian.md](../01-proposal/proposal-penelitian.md)

---

## 3. Metodologi dan Pelaksanaan

Penelitian dilaksanakan dalam 5 tahap. Bagian ini merangkum pelaksanaan tiap tahap; detail teknis lengkap ada pada dokumen worksheet (WS-01 hingga WS-12) yang dirujuk.

### 3.1 Tahap 1 — Perencanaan dan Studi Literatur

**Status: Selesai.**

Tahap ini mencakup identifikasi masalah, penyusunan problem statement, dan systematic literature review pada 8 paper final. Gap penelitian diidentifikasi sebagai kombinasi Method Gap dan Context Gap — belum ada studi yang membandingkan NB vs SVM dengan kondisi eksperimen identik pada dataset multi-bank mobile banking Indonesia disertai uji statistik. Rumusan masalah, hipotesis, dan variabel penelitian ditetapkan pada tahap ini.

**Hipotesis:**
- H₀: Tidak terdapat perbedaan signifikan F1-Score antara SVM dan Naive Bayes (α = 0,05)
- H₁: SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes (α = 0,05)

Detail: [../02-literatur/matriks-literatur.md](../02-literatur/matriks-literatur.md)

### 3.2 Tahap 2 — Perancangan Sistem dan Desain Eksperimen

**Status: Selesai.**

Pipeline klasifikasi sentimen dirancang sebagai artefak eksperimental dengan lima komponen modular: Data Loader (CV), Preprocessor (CV), Vectorizer TF-IDF (CV), Classifier (IV — swap NB↔SVM via config), dan Evaluator (DV). Prinsip variable isolation diterapkan ketat — hanya komponen Classifier yang berbeda antar kondisi eksperimen. Desain eksperimen comparison study dengan 10 run menggunakan random_state=0–9 ditetapkan, disertai rencana analisis statistik Wilcoxon signed-rank test dan Cohen's d.

Detail: [../03-teori/arsitektur-dan-skema.md](../03-teori/arsitektur-dan-skema.md)

### 3.3 Tahap 3 — Pengumpulan Data dan Preprocessing

**Status: Selesai (2026-05-12, ~15:30–15:45 WIB).**

Data dikumpulkan melalui scraping Google Play Store menggunakan library google-play-scraper (Python) dengan parameter lang='id', country='id', Sort.NEWEST, count=2.000 per aplikasi. Terjadi satu kali error pada scraping BRImo menggunakan package ID yang salah (com.bri.britama) — diperbaiki dengan package ID yang benar (id.co.bri.brimo). Total 6.000 ulasan berhasil dikumpulkan. Labeling sentimen dilakukan otomatis berdasarkan rating bintang: positif (4–5★), netral (3★), negatif (1–2★).

Pipeline preprocessing dijalankan menggunakan PySastrawi: lowercase → hapus simbol/angka/emoji → stopword removal → stemming. Hasil: 5.758 ulasan valid dari 6.000 total (242 dihapus karena kosong setelah preprocessing).

**Distribusi dataset final:**

| Aplikasi | Jumlah Ulasan |
|----------|--------------|
| BCA Mobile | 2.000 |
| Mandiri Online | 2.000 |
| BRImo | 2.000 |
| **Total** | **6.000** |

| Sentimen | Jumlah | Persentase |
|----------|--------|------------|
| Positif (4–5★) | 4.184 | 69,7% |
| Negatif (1–2★) | 1.540 | 25,7% |
| Netral (3★) | 276 | 4,6% |

Detail dan output: [../04-data/](../04-data/)

### 3.4 Tahap 4 — Eksperimen dan Analisis

**Status: Selesai (2026-05-12, ~15:53–16:00 WIB).**

Eksperimen dijalankan dalam satu sesi Google Colab menggunakan notebook `NB_vs_SVM_Sentiment_MobileBanking.ipynb`. TF-IDF max_features=5.000 di-fit hanya pada training set untuk mencegah data leakage via sklearn Pipeline. Split 80:20 stratified menghasilkan 4.606 data training dan 1.152 data testing. Kedua kondisi (MultinomialNB alpha=1,0 dan SVC kernel=linear C=1,0) dijalankan pada konfigurasi identik sebanyak 10 run dengan random_state=0–9. Analisis statistik menggunakan Wilcoxon signed-rank test dan Cohen's d dijalankan setelah 10 run selesai.

Detail kode: [../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb](../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb)

### 3.5 Tahap 5 — Penulisan Naskah

**Status: Selesai.**

Draf naskah jurnal lengkap telah disusun di [../07-manuskrip/](../07-manuskrip/) mencakup abstrak (ID & EN), pendahuluan, tinjauan pustaka, metode, hasil dan pembahasan, simpulan, dan referensi. Naskah telah dikonversi ke format `.docx` sesuai template jurnal UPB TIIJ (Calibri 10pt, 2 kolom, APA style).

Detail: [../07-manuskrip/naskah-jurnal.md](../07-manuskrip/naskah-jurnal.md)

---

## 4. Hasil Penelitian

Ringkasan hasil lengkap: [../07-manuskrip/05-hasil-analisis.md](../07-manuskrip/05-hasil-analisis.md)

### 4.1 Hasil Run Tunggal (random_state=42)

| Algoritma | F1-Score | Akurasi |
|-----------|----------|---------|
| Naive Bayes | 0,5466 | 0,8385 |
| SVM | 0,5553 | 0,8455 |
| Selisih | +0,0087 | +0,0070 |

### 4.2 Hasil 10 Run Eksperimen

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

SVM menghasilkan F1-Score lebih tinggi pada 9 dari 10 run.

### 4.3 Analisis Statistik

| Parameter | Nilai | Interpretasi |
|-----------|-------|-------------|
| p-value (Wilcoxon) | 0,0039 | p < α = 0,05 → H₀ ditolak |
| Cohen's d | 1,9428 | Large effect (d > 0,8) |

### 4.4 Interpretasi Singkat

1. SVM terbukti menghasilkan F1-Score lebih tinggi dari Naive Bayes secara statistik (p = 0,0039 < 0,05).
2. Effect size besar (Cohen's d = 1,9428) membuktikan perbedaan bermakna secara praktis, bukan sekadar noise.
3. Nilai F1-Score moderat pada kedua algoritma mencerminkan tantangan distribusi kelas yang tidak seimbang (positif 69,7% vs netral 4,6%).
4. SVM direkomendasikan sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

---

## 5. Kendala dan Catatan

- **Error scraping BRImo** — package ID awal (com.bri.britama) menghasilkan 0 ulasan. Diperbaiki dengan package ID yang benar (id.co.bri.brimo).
- **Import NLTK tidak digunakan** — terdapat import NLTK di awal notebook yang tidak digunakan karena preprocessing menggunakan PySastrawi. Sebaiknya dihapus untuk menghindari kebingungan peneliti lain.
- **requirements.txt belum dibuat** — peneliti lain perlu menginstall library satu per satu sesuai versi di README. Disarankan membuat file requirements.txt dengan versi yang di-lock untuk reproducibility yang lebih baik.
- **Waktu eksperimen singkat** — seluruh pipeline dari scraping hingga analisis statistik selesai dalam ~30 menit di Google Colab karena dataset berukuran moderat (6.000 ulasan) dan algoritma yang digunakan (NB dan SVM linear) tidak memerlukan komputasi berat.

---

## 6. Kesimpulan dan Saran

Ringkasan kesimpulan & saran: [../07-manuskrip/06-kesimpulan.md](../07-manuskrip/06-kesimpulan.md)

Inti kesimpulan: SVM dengan kernel linear terbukti secara statistik menghasilkan F1-Score yang lebih tinggi dibandingkan Multinomial Naive Bayes untuk klasifikasi sentimen ulasan mobile banking berbahasa Indonesia di Google Play Store menggunakan representasi TF-IDF (p = 0,0039, Cohen's d = 1,9428). Penelitian ini berkontribusi sebagai studi pertama yang memenuhi ketiga elemen: kondisi eksperimen identik, dataset multi-bank, dan verifikasi statistik — menghasilkan panduan algoritmik berbasis bukti empiris bagi tim pengembang aplikasi mobile banking Indonesia.

---

## 7. Lampiran — Peta Artefak Penelitian

| Folder | Isi | Status |
|--------|-----|--------|
| [00-admin/](../00-admin/) | Jadwal dan log pelaksanaan penelitian | Selesai |
| [01-proposal/](../01-proposal/) | Proposal penelitian lengkap | Selesai |
| [02-literatur/](../02-literatur/) | Matriks literatur 8 paper + BibTeX 11 entri | Selesai |
| [03-teori/](../03-teori/) | Arsitektur pipeline dan skema eksperimen | Selesai |
| [04-data/](../04-data/) | Dataset 6.000 ulasan + hasil eksperimen (4 file CSV) | Selesai |
| [05-kode/](../05-kode/) | Notebook Google Colab (17 cell) | Selesai |
| [06-output/](../06-output/) | Grafik perbandingan F1-Score dan Akurasi (PNG) | Selesai |
| [07-manuskrip/](../07-manuskrip/) | Naskah jurnal lengkap (.md + .docx) | Selesai |
| [08-laporan/](../08-laporan/) | Laporan penelitian (dokumen ini) | Selesai |

**Cara reproduksi:**

```bash
# 1. Buka Google Colab
# 2. Upload notebook: 05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb
# 3. Install dependency:
!pip install google-play-scraper
!pip install PySastrawi
# 4. Jalankan semua cell secara berurutan dari Cell 1 sampai Cell 17
# PENTING: Restart kernel sebelum menjalankan ulang
```