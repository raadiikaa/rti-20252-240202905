# Matriks Literatur

**Topik:** Perbandingan Naive Bayes dan SVM untuk Analisis Sentimen Ulasan Aplikasi Mobile Banking Indonesia di Google Play Store

**Database:** IEEE Xplore, Scopus, ACM Digital Library, Google Scholar

**Query:** ("sentiment analysis" OR "opinion mining") AND ("Naive Bayes" OR "Support Vector Machine" OR "SVM") AND ("mobile banking" OR "banking application" OR "fintech") AND ("Google Play" OR "app review") AND ("Indonesia" OR "Indonesian text" OR "Bahasa Indonesia")

**Tahun:** 2020–2025

**Hasil pencarian:** 89 paper → Screening judul + abstrak → 27 paper → Full-text → **8 paper final**

---

## Status Verifikasi Referensi

| # | Study | Status | Catatan |
|---|-------|--------|---------|
| 1 | Java et al. (2024) | ✅ Terverifikasi | Jurnal TICOM Vol.12 No.2 |
| 2 | Edwina & Mauritsius (2024) | ✅ Terverifikasi | IJETT Vol.72 No.6 |
| 3 | Al Hakim & Irwiensyah (2024) | ✅ Terverifikasi | JOSH Vol.5 No.4 |
| 4 | Munandar et al. (2024) | ✅ Terverifikasi | JTSI Vol.7 No.3 |
| 5 | Samudera et al. (2024) | ✅ Terverifikasi | IJESTY Vol.4 No.4 |
| 6 | Andrian et al. (2022) | ✅ Terverifikasi | IJACSA Vol.13 No.3 |
| 7 | Ningsih et al. (2024) | ✅ Terverifikasi | MALCOM Vol.4 No.2 |
| 8 | Khaira et al. (2023) | ✅ Terverifikasi | Processor Vol.18 No.2 |

---

## Matriks Literatur (Concept-Centric)

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Java et al. | 2024 | Multinomial NB vs SVM | Ulasan Threads Google Play Indonesia | NB dan SVM dibandingkan, akurasi baik | Bukan domain banking; bukan multi-bank |
| 2 | Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF | 7.000+ ulasan SimobiPlus | SVM akurasi 91% setelah tuning | Hanya 1 bank; tidak ada uji statistik signifikansi |
| 3 | Al Hakim & Irwiensyah | 2024 | Multinomial NB | 2.000 ulasan BCA Mobile | Akurasi 86,83%; precision 52,78% | Hanya NB; tidak ada pembanding; precision rendah tidak dianalisis |
| 4 | Munandar et al. | 2024 | KNN | Ulasan mobile banking Indonesia | Akurasi baik | Hanya KNN; tidak ada perbandingan NB vs SVM |
| 5 | Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile | Akurasi baik, split 80:20 | Hanya NB; tidak ada pembanding SVM |
| 6 | Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia, Twitter | SVM F1-Score 73,34% | Bukan Google Play; bukan ulasan terstruktur |
| 7 | Ningsih et al. | 2024 | SVM vs NB + TF-IDF | Twitter mobil listrik Indonesia | SVM > NB di semua metrik | Bukan banking; bukan Google Play |
| 8 | Khaira et al. | 2023 | NB vs SVM + TF-IDF | Twitter kebijakan Kemdikbudristek | SVM lebih baik dari NB | Domain kebijakan; tidak ada uji statistik |

---

## Pola yang Ditemukan

**Metode dominan:** NB paling sering dipakai sendiri tanpa pembanding; SVM muncul dalam studi komparatif dan cenderung lebih unggul; tidak ada yang melakukan uji statistik signifikansi.

**Dataset umum:** Google Play Store ulasan banking Indonesia umumnya 1–2 aplikasi saja.

**Limitasi berulang:**
1. Hanya 1–2 bank per studi — temuan sulit digeneralisasi ke industri perbankan Indonesia
2. NB dipakai tanpa pembanding terkontrol
3. Tidak ada uji statistik untuk membuktikan perbedaan signifikan

---

## Gap Identification

| Jenis Gap | Gap Statement |
|-----------|---------------|
| **Method Gap** | Belum ada studi yang menggunakan uji statistik (Wilcoxon/paired t-test) untuk membuktikan perbedaan F1-Score NB vs SVM signifikan — semua perbandingan hanya deskriptif |
| **Context Gap** | Studi NB vs SVM yang ada menggunakan domain non-banking (Twitter, e-commerce), bukan ulasan mobile banking terstruktur dari Google Play Store |
| **Data Gap** | Semua studi menggunakan 1–2 aplikasi banking — belum ada yang menggabungkan 3 bank konvensional besar (BCA, Mandiri, BRI) dalam satu dataset |
| **Performance Gap** | Precision NB rendah (52,78%) pada ulasan BCA Mobile (Al Hakim & Irwiensyah, 2024) namun tidak ada studi yang menguji apakah SVM dapat memperbaiki kelemahan ini secara signifikan |

**Gap utama:** Method Gap + Context Gap

**Mengapa gap ini penting:**
> Gap ini penting karena dua alasan yang saling memperkuat. Pertama, secara metodologis: perbandingan algoritma tanpa uji statistik tidak dapat dipercaya — perbedaan F1 sebesar 5% antara NB dan SVM bisa jadi hanya noise dari partisi data yang berbeda, bukan bukti keunggulan nyata. Tanpa p-value dan effect size, klaim "SVM lebih baik" hanyalah anekdot, bukan temuan ilmiah. Kedua, secara kontekstual: ulasan mobile banking Indonesia memiliki karakteristik unik — bahasa informal, campur kode, keluhan teknis spesifik perbankan — yang berbeda dari e-commerce atau media sosial, sehingga temuan dari domain lain tidak bisa langsung ditransfer.

---

## Baseline Selection

| # | Baseline | Relevansi | Representatif | SOTA? | Sumber |
|---|----------|-----------|---------------|-------|--------|
| 1 | Multinomial Naive Bayes + TF-IDF | Task identik: klasifikasi sentimen teks ulasan mobile banking Indonesia berbahasa Indonesia menggunakan TF-IDF | Digunakan di 4 dari 8 paper final — metode paling umum di domain ini | Ya, studi terbaru 2024 masih menggunakannya sebagai metode utama | Samudera et al. (2024); Al Hakim & Irwiensyah (2024) |
| 2 | SVM + TF-IDF | Studi terbaru yang menunjukkan performa SVM tertinggi (91%) pada ulasan mobile banking Indonesia | State-of-local-practice: studi 2024 paling relevan di domain ini | Ya: studi terbaru dengan akurasi tertinggi untuk domain ini | Edwina & Mauritsius (2024) |

**Apakah straw man comparison?** Tidak — kedua baseline dipilih karena relevansi dan kekuatannya. NB dipilih karena merupakan common practice yang diakui; SVM Edwina (2024) dipilih karena merupakan hasil terbaik yang ada di domain ini.

---

## Posisi Penelitian

Penelitian ini mengisi gap dengan menjadi studi pertama yang:
- **(a)** Membandingkan NB vs SVM dengan kondisi eksperimen identik (preprocessing, TF-IDF, split identik)
- **(b)** Pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store (BCA Mobile, Mandiri Online, BRImo — 6.000 ulasan)
- **(c)** Disertai uji statistik Wilcoxon signed-rank test (α = 0,05) dan effect size Cohen's d