# Proposal Penelitian

**Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store**

Dosen Pengampu: Helmi Bahar Alim, S.Kom., M.Kom
Disusun Oleh: Radika Rismawati Tri Prasaja — 240202905
Program Studi Ilmu Komputer, Fakultas Sains dan Teknologi
Universitas Putra Bangsa Kebumen — 2025/2026

---

## A. Judul

Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

---

## B. Ringkasan

Aplikasi mobile banking di Indonesia menghasilkan jutaan ulasan pengguna di Google Play Store yang berpotensi menjadi sumber insight strategis bagi pengembang, namun belum dianalisis secara sistematis berbasis bukti empiris. Tim pengembang aplikasi mobile banking Indonesia tidak memiliki panduan berbasis bukti untuk memilih algoritma klasifikasi sentimen yang paling efektif bagi teks ulasan berbahasa Indonesia pada domain perbankan, sehingga pemilihan algoritma dilakukan secara ad-hoc tanpa landasan empiris yang kontekstual.

Penelitian ini bertujuan membandingkan performa Multinomial Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store secara empiris, terkontrol, dan disertai uji statistik signifikansi. Data dikumpulkan melalui scraping ulasan pengguna aplikasi BCA Mobile, Mandiri Online, dan BRImo dengan total 6.000 ulasan berbahasa Indonesia periode 2022–2024 menggunakan library google-play-scraper.

Pipeline klasifikasi dibangun sebagai artefak eksperimental dengan lima komponen modular: Data Loader, Preprocessor, Vectorizer TF-IDF, Classifier, dan Evaluator. Kedua algoritma diuji pada kondisi eksperimen yang identik menggunakan 10 run dengan random seed berbeda, dan perbedaan performa diverifikasi menggunakan uji statistik Wilcoxon signed-rank test pada α = 0,05 serta effect size Cohen's d. Luaran penelitian ini adalah rekomendasi algoritma berbasis bukti empiris yang dapat langsung diadopsi tim pengembang aplikasi perbankan Indonesia, serta dataset dan notebook Python yang dapat direplikasi peneliti lain.

---

## C. Kata Kunci

Analisis Sentimen; Naive Bayes; Support Vector Machine; TF-IDF; Mobile Banking Indonesia

---

## D. Pendahuluan

### D.1 Latar Belakang dan Rumusan Masalah

Aplikasi mobile banking di Indonesia mengalami pertumbuhan yang signifikan dalam beberapa tahun terakhir. Jutaan nasabah dari BCA, Bank Mandiri, dan BRI secara aktif menggunakan aplikasi mobile banking untuk bertransaksi setiap harinya, dan sebagian besar dari mereka memberikan ulasan di Google Play Store yang memuat keluhan, pujian, dan saran terhadap fitur serta layanan aplikasi. Ulasan-ulasan ini merupakan aset data yang sangat berharga bagi tim pengembang untuk memahami persepsi pengguna secara real-time dan mendukung keputusan peningkatan produk yang tepat sasaran (Prasetyo & Agastya, 2024).

Tim pengembang aplikasi mobile banking Indonesia menghadapi gejala nyata berupa inkonsistensi pemilihan algoritma klasifikasi sentimen antar studi tanpa kondisi perbandingan yang terkontrol. Munandar et al. (2024) menggunakan KNN pada ulasan mobile banking Indonesia, sementara Edwina dan Mauritsius (2024) menunjukkan SVM unggul dengan akurasi 91% pada SimobiPlus, dan Samudera et al. (2024) serta Al Hakim dan Irwiensyah (2024) hanya menggunakan Naive Bayes tanpa pembanding. Studi-studi tersebut menggunakan dataset, preprocessing, dan metrik evaluasi yang berbeda-beda sehingga hasilnya tidak dapat dibandingkan secara langsung.

Akar masalahnya adalah tidak adanya studi yang secara sistematis membandingkan Naive Bayes dan SVM dengan kondisi eksperimen yang identik pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store, sekaligus memverifikasi perbedaannya secara statistik. Dampaknya, tim pengembang aplikasi mobile banking memilih algoritma secara ad-hoc tanpa panduan berbasis bukti yang kontekstual (Al Hakim & Irwiensyah, 2024), berpotensi menghasilkan sistem analisis sentimen yang tidak optimal dan keputusan produk yang tidak didukung data yang valid.

Berdasarkan uraian di atas, rumusan masalah penelitian ini adalah: **"Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?"**

### D.2 Pendekatan Pemecahan Masalah

Penelitian ini bertujuan menghasilkan perbandingan empiris yang rigorous antara Naive Bayes dan SVM untuk klasifikasi sentimen ulasan mobile banking berbahasa Indonesia, dengan kondisi eksperimen yang sepenuhnya terkontrol dan disertai uji statistik signifikansi, sehingga hasilnya dapat dijadikan panduan berbasis bukti bagi tim pengembang.

**Research Question:** Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

**Hipotesis:**
- H₀: Tidak terdapat perbedaan signifikan F1-Score antara SVM dan Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF (α = 0,05)
- H₁: SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF (α = 0,05)

**Intervensi yang diusulkan:** Penggantian algoritma baseline Naive Bayes dengan SVM kernel linear dalam pipeline klasifikasi sentimen yang identik, dengan semua komponen lain dikunci konstan untuk memastikan variable isolation.

**Alasan pemilihan intervensi:** SVM dipilih karena secara konsisten menunjukkan performa lebih tinggi dari Naive Bayes pada studi analisis sentimen teks Indonesia (Ningsih et al., 2024; Khaira et al., 2023; Java et al., 2024), namun belum pernah diverifikasi secara statistik pada domain mobile banking Indonesia dengan dataset multi-bank.

**Baseline:** Multinomial Naive Bayes dengan representasi TF-IDF, yang merupakan algoritma paling umum digunakan dalam studi analisis sentimen ulasan mobile banking Indonesia (Java et al., 2024; Samudera et al., 2024; Al Hakim & Irwiensyah, 2024; Soliha et al., 2023).

### D.3 State of the Art dan Kebaruan

Systematic literature review dilakukan pada database IEEE Xplore, Scopus, ACM Digital Library, dan Google Scholar dengan query `("sentiment analysis") AND ("Naive Bayes" OR "SVM") AND ("mobile banking" OR "banking app") AND ("Google Play" OR "Indonesia")` periode 2020–2025. Dari 89 paper awal diperoleh 8 paper final setelah screening judul, abstrak, dan full-text.

| No | Studi | Tahun | Method | Dataset | Result | Limitasi |
|----|-------|-------|--------|---------|--------|----------|
| 1 | Java et al. | 2024 | Multinomial NB vs SVM | Ulasan Threads Google Play Indonesia | NB dan SVM dibandingkan | Bukan domain banking; bukan multi-bank |
| 2 | Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF | 7.000+ ulasan SimobiPlus | SVM 91% akurasi setelah tuning | Hanya 1 bank; tidak ada uji statistik |
| 3 | Al Hakim & Irwiensyah | 2024 | Multinomial NB | 2.000 ulasan BCA Mobile | Akurasi 86,83%, precision 52,78% | Hanya NB; tidak ada pembanding |
| 4 | Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile | Akurasi baik, split 80:20 | Hanya NB; tidak ada pembanding SVM |
| 5 | Soliha et al. | 2023 | Naive Bayes | Ulasan digital banking Google Play | Akurasi baik | Hanya NB; tidak ada pembanding |
| 6 | Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia, Twitter | SVM F1-Score 73,34% | Bukan Google Play; bukan ulasan terstruktur |
| 7 | Ningsih et al. | 2024 | SVM vs NB + TF-IDF | Twitter mobil listrik Indonesia | SVM > NB di semua metrik | Bukan banking; bukan Google Play |
| 8 | Khaira et al. | 2023 | NB vs SVM + TF-IDF | Twitter kebijakan Kemdikbudristek | SVM lebih baik dari NB | Domain kebijakan; bukan banking; tidak ada uji statistik |

Kondisi kajian saat ini menunjukkan dua pola utama: pertama, mayoritas studi pada domain mobile banking Indonesia hanya menggunakan satu algoritma tanpa pembanding terkontrol; kedua, studi yang membandingkan NB vs SVM tidak menggunakan domain mobile banking dan tidak disertai uji statistik signifikansi.

**Gap:** Tidak ada satupun dari 8 paper yang memenuhi ketiga elemen berikut secara bersamaan: (1) perbandingan NB vs SVM dengan kondisi eksperimen identik, (2) pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store, (3) disertai uji statistik yang membuktikan signifikansi perbedaannya.

**Posisi penelitian ini:** Mengisi gap tersebut dengan menjadi studi pertama yang (a) membandingkan NB vs SVM dengan kondisi eksperimen identik, (b) pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store, dan (c) disertai uji statistik Wilcoxon signed-rank test dan effect size Cohen's d.

### D.4 Peta Jalan Penelitian

| Tahap | Status | Luaran |
|-------|--------|--------|
| Identifikasi masalah dan studi literatur | ✅ Selesai | Gap terdokumentasi dari 8 paper, rumusan masalah presisi |
| Formulasi RQ dan desain metode | ✅ Selesai | Hipotesis falsifiable, variabel operasional, desain pipeline modular |
| Implementasi pipeline dan pengumpulan data | ✅ Selesai | 6.000 ulasan terkumpul, preprocessing selesai, pipeline terverifikasi |
| 10 run eksperimen + analisis statistik | ✅ Selesai | F1 NB=0,5532, F1 SVM=0,5627, p=0,0039, Cohen's d=2,0479 |
| Penulisan laporan dan interpretasi hasil | 🔲 Direncanakan | Naskah laporan penelitian |
| Revisi dan finalisasi | 🔲 Direncanakan | Laporan final siap presentasi |

---

## E. Metode

### E.1 Desain Penelitian dan Unit Analisis

Penelitian ini menggunakan desain kuantitatif eksperimental komparatif dengan paradigma Design Science Research — pipeline klasifikasi sentimen dibangun sebagai artefak eksperimental untuk menguji hipotesis, bukan sebagai produk akhir.

**Masalah inti:** Tim pengembang aplikasi mobile banking Indonesia tidak memiliki panduan berbasis bukti untuk memilih algoritma klasifikasi sentimen yang paling efektif bagi teks ulasan berbahasa Indonesia, karena belum ada studi yang membandingkan Naive Bayes dan SVM dengan kondisi eksperimen identik pada domain ini.

**Research Question final:** Apakah SVM menghasilkan F1-Score lebih tinggi dari Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia di Google Play Store menggunakan TF-IDF?

**Hipotesis:**
- H₀: Tidak ada perbedaan signifikan F1-Score antara SVM dan Naive Bayes (α = 0,05)
- H₁: SVM menghasilkan F1-Score lebih tinggi secara signifikan dari Naive Bayes (α = 0,05)

**Variabel Independen (IV):** Jenis algoritma klasifikasi sentimen — Multinomial Naive Bayes vs Support Vector Machine kernel linear — dimanipulasi dengan mengganti satu parameter di config file tanpa mengubah komponen pipeline lainnya.

**Variabel Dependen (DV):** F1-Score macro-average (primary, skala ratio 0–1) sebagai metrik utama yang mengukur performa klasifikasi per kelas secara terpisah; serta Akurasi, Precision macro, dan Recall macro (secondary, skala ratio 0–1) sebagai metrik pendukung.

**Populasi penelitian:** Seluruh ulasan pengguna berbahasa Indonesia pada aplikasi mobile banking yang tersedia di Google Play Store.

**Sampel:** 6.000 ulasan diambil menggunakan teknik purposive sampling dengan kriteria inklusi: (1) ulasan berbahasa Indonesia, (2) berasal dari tiga aplikasi mobile banking terbesar Indonesia berdasarkan pangsa pasar nasabah konvensional — BCA Mobile (com.bca), Mandiri Online (com.bankmandiri.mandirionline), dan BRImo (id.co.bri.brimo), (3) periode 2022–2024, dengan jumlah ±2.000 ulasan per aplikasi menggunakan Sort.NEWEST via library google-play-scraper.

**Unit analisis:** Setiap ulasan pengguna aplikasi mobile banking berbahasa Indonesia di Google Play Store, direpresentasikan sebagai vektor TF-IDF dan diklasifikasikan ke kelas sentimen positif (4–5★), netral (3★), atau negatif (1–2★).

**Gambaran kondisi:**
- Kondisi A (Baseline): Multinomial Naive Bayes + TF-IDF
- Kondisi B (Intervensi): SVM kernel linear + TF-IDF — semua komponen lain identik dengan kondisi A

### E.2 Variabel, Metrik, Instrumen, dan Data

**Variabel Independen (IV):** Jenis algoritma klasifikasi — Multinomial Naive Bayes vs SVM kernel linear — dimanipulasi dengan mengganti satu parameter di config file tanpa mengubah komponen pipeline lainnya.

**Variabel Dependen (DV):**
- Primary: F1-Score macro-average (skala ratio 0–1)
- Secondary: Akurasi, Precision macro, Recall macro (skala ratio 0–1)

**Variabel Kontrol (CV):**

| Variabel Kontrol | Nilai | Alasan Dikunci |
|-----------------|-------|----------------|
| Representasi fitur | TF-IDF max_features=5.000 | Perbedaan hasil murni karena algoritma |
| Split data | 80:20, stratified, random_state per run | Distribusi kelas seimbang dan reproducible |
| Preprocessing | Identik untuk kedua kondisi | Variable isolation terjaga |
| Dataset | File CSV yang sama untuk semua run | Fairness perbandingan |
| Bahasa ulasan | Bahasa Indonesia saja | Menghindari noise bahasa lain |

**Justifikasi metrik:** F1-Score macro-average dipilih karena distribusi kelas sentimen tidak seimbang — positif 4.184 (69,7%), negatif 1.540 (25,7%), netral 276 (4,6%). Pada kondisi imbalance ini, akurasi akan memberikan gambaran yang menyesatkan karena didominasi kelas mayoritas, sedangkan F1-Score macro-average menghitung performa per kelas secara terpisah lalu dirata-rata sehingga kelas minoritas tetap terwakili (Andrian et al., 2022).

**Instrumen:** Pipeline Python berbasis scikit-learn yang dijalankan di Google Colab. Semua parameter dikunci di config file untuk memastikan reproducibility dan transparansi eksperimen.

**Sumber data:** Scraping langsung dari Google Play Store menggunakan library google-play-scraper (Python), filter bahasa Indonesia, periode 2022–2024, ±2.000 ulasan per aplikasi, total 6.000 ulasan.

**Labeling:** Otomatis berdasarkan rating bintang — positif (4–5★), netral (3★), negatif (1–2★).

### E.3 Skenario dan Prosedur Pengujian

Kondisi A (Naive Bayes) dan kondisi B (SVM) dibandingkan pada dataset, preprocessing, representasi fitur, dan split data yang sepenuhnya identik — satu-satunya yang berbeda adalah komponen Classifier.

**Langkah pengujian:**
1. Scraping ±2.000 ulasan per aplikasi (BCA Mobile, Mandiri Online, BRImo) dari Google Play Store via google-play-scraper, total 6.000 ulasan, filter bahasa Indonesia, labeling otomatis dari rating bintang
2. Preprocessing identik untuk kedua kondisi: lowercase → hapus simbol, angka, emoji → stopword removal (PySastrawi) → stemming (PySastrawi)
3. TF-IDF max_features=5.000 di-fit hanya pada data training untuk mencegah data leakage, transform diterapkan terpisah pada data testing
4. Split 80% training, 20% testing, stratified, random_state dikunci per run
5. Kondisi A: training MultinomialNB (alpha=1.0) → prediksi → evaluasi → simpan ke results.csv
6. Kondisi B: training SVC (kernel=linear, C=1.0) → prediksi → evaluasi → simpan ke results.csv
7. Langkah 4–6 diulang 10 kali dengan random_state berbeda (0–9)

### E.4 Artifact, Setup, dan Kesiapan Implementasi

Pipeline klasifikasi sentimen modular berbasis Python terdiri dari lima komponen:

| Komponen | Fungsi | Peran Variabel |
|----------|--------|----------------|
| Data Loader | Memuat CSV 6.000 ulasan 3 aplikasi | CV — tidak berubah antar kondisi |
| Preprocessor | Lowercase, hapus simbol, stopword removal, stemming | CV — tidak berubah antar kondisi |
| Vectorizer TF-IDF | Mengubah teks ke vektor numerik max_features=5.000 | CV — tidak berubah antar kondisi |
| Classifier | MultinomialNB atau SVC, di-swap via config | IV — satu-satunya yang berubah |
| Evaluator | Menghitung F1, Akurasi, Precision, Recall, menyimpan ke CSV | DV — output pengukuran |

**Arsitektur pipeline**

![Pipeline Klasifikasi Sentimen](pipeline-klasifikasi.png)

**Environment:** Google Colab (Python 3.12), library: google-play-scraper, PySastrawi, scikit-learn 1.4.2, scipy, pandas, matplotlib.

**Status kesiapan:** Eksperimen telah selesai dijalankan. Dataset 6.000 ulasan telah berhasil dikumpulkan, preprocessing selesai, 10 run eksperimen telah dijalankan, dan analisis statistik telah selesai dilakukan.

### E.5 Teknik Analisis, Asumsi, dan Validitas

**Teknik analisis:**
1. Deskriptif: Tabel perbandingan rata-rata F1-Score, Akurasi, Precision, Recall dari 10 run untuk kondisi A (NB) dan kondisi B (SVM)
2. Inferensial: Wilcoxon signed-rank test (non-parametrik) pada α = 0,05
3. Effect size: Cohen's d untuk mengukur besaran perbedaan praktis
4. Visualisasi: Bar chart perbandingan F1-Score dan Akurasi antar kondisi

**Cara membaca hasil kondisi A vs B:**
- Jika p < 0,05 → H₀ ditolak, SVM terbukti menghasilkan F1-Score lebih tinggi dari NB secara statistik
- Jika p ≥ 0,05 → H₀ gagal ditolak, tidak cukup bukti statistik bahwa SVM lebih baik dari NB
- Cohen's d > 0,8 → effect size besar, perbedaan bermakna secara praktis

**Ancaman validitas:**

| Jenis Ancaman | Ancaman | Mitigasi |
|---------------|---------|----------|
| Internal | Data leakage | sklearn Pipeline — TF-IDF fit hanya pada training set |
| Internal | Variable contamination | Config-driven execution — hanya Classifier yang berubah |
| External | Sample bias | Tiga bank terbesar dipilih untuk representasi lebih luas |
| Construct | Metrik tidak tepat | F1-Score macro dipilih karena robust terhadap class imbalance |

---

## F. Hasil yang Diharapkan

Penelitian ini ditargetkan menghasilkan tiga luaran:

**Luaran 1 — Temuan empiris terukur:** Perbandingan rata-rata F1-Score, Akurasi, Precision, dan Recall antara Naive Bayes dan SVM dari 10 run eksperimen, disertai nilai p-value Wilcoxon signed-rank test dan effect size Cohen's d.

> Hasil aktual: F1 NB=0,5532, F1 SVM=0,5627, p-value=0,0039 (H₀ ditolak), Cohen's d=2,0479 (large effect) → SVM terbukti lebih baik dari Naive Bayes secara statistik.

**Luaran 2 — Rekomendasi algoritmik berbasis bukti:** Rekomendasi algoritma untuk tim pengembang aplikasi mobile banking Indonesia yang ingin mengimplementasikan sistem analisis sentimen ulasan pengguna, beserta justifikasi statistiknya.

**Luaran 3 — Artefak reproducible:** Dataset 6.000 ulasan terstruktur dari tiga aplikasi mobile banking terbesar Indonesia beserta notebook Python lengkap (`NB_vs_SVM_Sentiment_MobileBanking.ipynb`) yang dapat direplikasi oleh peneliti lain.

---

## G. Jadwal Penelitian

| No | Nama Kegiatan | Minggu 1 | Minggu 2 | Minggu 3 | Minggu 4 | Minggu 5 | Minggu 6 | Minggu 7 | Minggu 8 |
|----|---------------|----------|----------|----------|----------|----------|----------|----------|----------|
| 1 | Identifikasi masalah dan topik | ✓ | | | | | | | |
| 2 | Literatur dan gap | ✓ | ✓ | | | | | | |
| 3 | RQ dan desain metode | | ✓ | ✓ | | | | | |
| 4 | Implementasi dan pengumpulan data | | | ✓ | ✓ | | | | |
| 5 | Pengujian dan eksperimen | | | | ✓ | ✓ | | | |
| 6 | Analisis dan penulisan | | | | | ✓ | ✓ | | |
| 7 | Revisi final | | | | | | ✓ | ✓ | ✓ |

---

## H. Daftar Pustaka

Al Hakim, M. G., & Irwiensyah, F. (2024). Analisis sentimen terhadap ulasan pengguna pada aplikasi BCA Mobile menggunakan metode Naïve Bayes. *Journal of Information System Research (JOSH)*, *5*(4), 911–921. http://ejurnal.seminarid.com/index.php/josh/article/view/5343

Andrian, B., Simanungkalit, T., Budi, I., & Wicaksono, A. F. (2022). Sentiment analysis on customer satisfaction of digital banking in Indonesia. *International Journal of Advanced Computer Science and Applications*, *13*(3), 466–473. https://thesai.org/Downloads/Volume13No3/Paper_56-Sentiment_Analysis_on_Customer_Satisfaction_of_Digital_Banking.pdf

Cortes, C., & Vapnik, V. (1995). Support-vector networks. *Machine Learning*, *20*(3), 273–297. https://link.springer.com/article/10.1007/BF00994018

Edwina, & Mauritsius, T. (2024). Data-driven insights for mobile banking app improvement: A sentiment analysis and topic modelling approach for SimobiPlus user reviews. *International Journal of Engineering Trends and Technology*, *72*(6), 347–360. https://ijettjournal.org/Volume-72/Issue-6/IJETT-V72I6P132.pdf

Java, M. A., Syafrullah, M., Windarto, & Painem. (2024). Analisis sentimen ulasan pengguna aplikasi Threads pada Google Play Store menggunakan Multinomial Naive Bayes dan Support Vector Machine. *Jurnal TICOM: Technology of Information and Communication*, *12*(2), 75–80. https://jurnalticom.jakarta.aptikom.org/index.php/Ticom/article/view/112

Khaira, U., Aryani, R., & Hardian, R. W. (2023). Perbandingan algoritma Naïve Bayes dan Support Vector Machine (SVM) dalam analisis sentimen kebijakan Kemdikbudristek tentang kuota internet selama pandemi Covid-19. *Processor: Jurnal Ilmiah Sistem Informasi, Teknologi Informasi dan Sistem Komputer*, *18*(2). https://ejournal.unama.ac.id/index.php/processor/article/download/897/1158

Munandar, D., Afdal, M., Zarnelly, & Novita, R. (2024). Analisis sentimen ulasan pengguna aplikasi mobile banking menggunakan algoritma K-Nearest Neighbor. *Jurnal Teknologi Sistem Informasi dan Aplikasi*, *7*(3), 1309–1318. https://doi.org/10.32493/jtsi.v7i3.41409

Ningsih, W., Alfianda, B., Rahmaddeni, & Wulandari, D. (2024). Perbandingan algoritma SVM dan Naïve Bayes dalam analisis sentimen Twitter pada penggunaan mobil listrik di Indonesia. *MALCOM: Indonesian Journal of Machine Learning and Computer Science*, *4*(2), 556–562. https://doi.org/10.57152/malcom.v4i2.1253

Prasetyo, M. J., & Agastya, I. M. A. (2024). Analisis sentimen ulasan aplikasi perbankan di Google Play Store menggunakan algoritma Support Vector Machine. *Sistemasi: Jurnal Sistem Informasi*, *13*(6), 2386–2400. https://sistemasi.ftik.unisi.ac.id/index.php/stmsi/article/view/4536

Samudera, B. D., Nurdin, & Aidilof, H. A. K. (2024). Sentiment analysis of user reviews on BSI Mobile and Action Mobile applications on the Google Play Store using Multinomial Naive Bayes algorithm. *International Journal of Engineering, Science and Information Technology (IJESTY)*, *4*(4), 101–112. https://doi.org/10.52088/ijesty.v4i4.581

Soliha, A. N., Munandar, T. A., & Yasir, M. (2023). Sentiment analysis of the use of digital banking service applications in Google Play Store reviews using Naïve Bayes method. *International Journal of Information Technology and Computer Science Applications (IJITCSA)*, *1*(3), 129–137. https://www.researchgate.net/publication/373914432