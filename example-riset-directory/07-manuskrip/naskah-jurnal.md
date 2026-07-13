# Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

Radika Rismawati Tri Prasaja
Universitas Putra Bangsa
email: radikarismawati10@gmail.com

---

## ABSTRAK

Aplikasi mobile banking di Indonesia menghasilkan jutaan ulasan pengguna di Google Play Store yang berpotensi menjadi sumber insight strategis bagi pengembang. Namun, belum tersedia panduan berbasis bukti empiris untuk pemilihan algoritma klasifikasi sentimen pada teks berbahasa Indonesia di domain perbankan. Penelitian ini membandingkan Multinomial Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF pada dataset 6.000 ulasan dari BCA Mobile, Mandiri Online, dan BRImo. Pipeline klasifikasi dibangun dengan lima komponen modular dan diuji pada kondisi eksperimen identik menggunakan 10 run dengan random seed berbeda. Perbedaan performa diverifikasi menggunakan Wilcoxon signed-rank test (α = 0,05) dan Cohen's d. Hasil menunjukkan SVM menghasilkan rata-rata F1-Score 0,5627 dibandingkan Naive Bayes 0,5532, dengan perbedaan signifikan secara statistik (p = 0,0039) dan effect size besar (Cohen's d = 1,9428). SVM direkomendasikan sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

**Kata Kunci:** Analisis Sentimen; Naive Bayes; Support Vector Machine; TF-IDF; Mobile Banking

---

## ABSTRACT

Mobile banking applications in Indonesia generate millions of user reviews on Google Play Store as potential strategic insights for developers. However, no empirical evidence-based guidance exists for selecting sentiment classification algorithms for Indonesian-language text in the banking domain. This study compares Multinomial Naive Bayes and Support Vector Machine (SVM) using TF-IDF representation on a dataset of 6,000 reviews from BCA Mobile, Mandiri Online, and BRImo. A modular five-component classification pipeline was tested under identical experimental conditions using 10 runs with different random seeds. Performance differences were verified using the Wilcoxon signed-rank test (α = 0.05) and Cohen's d. Results show SVM achieved a mean F1-Score of 0.5627 compared to Naive Bayes at 0.5532, with a statistically significant difference (p = 0.0039) and large effect size (Cohen's d = 1.9428). SVM is recommended as the sentiment classification algorithm for Indonesian mobile banking reviews.

**Keywords:** Sentiment Analysis; Naive Bayes; Support Vector Machine; TF-IDF; Mobile Banking

---

## PENDAHULUAN

Pertumbuhan layanan mobile banking di Indonesia telah mendorong jutaan nasabah BCA, Bank Mandiri, dan BRI untuk aktif memberikan ulasan di Google Play Store. Ulasan-ulasan ini mengandung keluhan, pujian, dan saran yang berpotensi menjadi sumber insight strategis bagi tim pengembang untuk memahami persepsi pengguna secara real-time (Prasetyo & Agastya, 2024). Namun, potensi tersebut belum dapat dimanfaatkan secara optimal karena tidak tersedianya panduan berbasis bukti empiris dalam pemilihan algoritma klasifikasi sentimen yang paling efektif untuk teks ulasan berbahasa Indonesia pada domain perbankan.

Inkonsistensi pemilihan algoritma antar studi menjadi permasalahan utama. Munandar et al. (2024) menggunakan K-Nearest Neighbor pada ulasan mobile banking Indonesia, sementara Edwina dan Mauritsius (2024) menunjukkan SVM unggul dengan akurasi 91% pada SimobiPlus, dan Samudera et al. (2024) serta Al Hakim dan Irwiensyah (2024) hanya menggunakan Naive Bayes tanpa pembanding. Studi-studi tersebut menggunakan dataset, preprocessing, dan metrik evaluasi yang berbeda sehingga hasilnya tidak dapat dibandingkan secara langsung, dan akibatnya tim pengembang memilih algoritma secara ad-hoc tanpa landasan empiris yang kontekstual (Al Hakim & Irwiensyah, 2024).

Systematic literature review pada database IEEE Xplore, Scopus, ACM Digital Library, dan Google Scholar periode 2020–2025 menghasilkan 8 paper final dari 89 paper awal. Analisis terhadap 8 paper tersebut mengidentifikasi tiga keterbatasan berulang: perbandingan hanya deskriptif tanpa uji statistik; dataset hanya dari satu hingga dua aplikasi; dan studi komparatif Naive Bayes vs SVM menggunakan domain non-banking yang karakteristik linguistiknya berbeda dari ulasan perbankan di Google Play Store. Tidak satu pun dari 8 paper yang memenuhi ketiga elemen berikut secara bersamaan: kondisi eksperimen identik, dataset multi-bank, dan verifikasi statistik. Penelitian ini bertujuan mengisi gap tersebut dengan membandingkan Naive Bayes dan SVM pada kondisi eksperimen identik menggunakan dataset multi-bank ulasan mobile banking berbahasa Indonesia, disertai verifikasi statistik Wilcoxon signed-rank test dan effect size Cohen's d.

Secara teoritis, Multinomial Naive Bayes merupakan algoritma probabilistik berbasis Teorema Bayes yang mengasumsikan independensi antar fitur, sehingga cocok untuk data diskrit seperti representasi TF-IDF. Sebaliknya, Support Vector Machine bekerja dengan mencari hyperplane optimal yang memaksimalkan margin antar kelas dalam ruang fitur berdimensi tinggi (Cortes & Vapnik, 1995), sehingga secara teoritis lebih robust terhadap data berdimensi tinggi seperti representasi TF-IDF pada teks. Perbedaan mendasar antara kedua pendekatan ini — probabilistik berbasis independensi fitur versus margin-maximization pada ruang berdimensi tinggi — menjadi dasar mengapa perbandingan performa keduanya perlu diverifikasi secara empiris dan statistik, bukan hanya diasumsikan dari karakteristik teoritisnya saja.

---

## TINJAUAN PUSTAKA

### Analisis Sentimen pada Ulasan Mobile Banking Indonesia

Penelitian analisis sentimen pada ulasan mobile banking Indonesia didominasi penggunaan Naive Bayes sebagai metode tunggal tanpa pembanding terkontrol. Al Hakim dan Irwiensyah (2024) menerapkan Multinomial Naive Bayes pada 2.000 ulasan BCA Mobile dan menghasilkan akurasi 86,83% namun precision hanya 52,78%. Samudera et al. (2024) menggunakan Multinomial Naive Bayes pada ulasan BSI Mobile dan Action Mobile tanpa pembanding algoritmik. Soliha et al. (2023) juga menerapkan Naive Bayes pada ulasan digital banking tanpa pembanding dan tanpa uji statistik. Studi yang menyertakan SVM menunjukkan hasil lebih menjanjikan — Edwina dan Mauritsius (2024) menemukan SVM mencapai akurasi 91% pada SimobiPlus, dan Andrian et al. (2022) menemukan SVM menghasilkan F1-Score tertinggi sebesar 73,34% pada data digital banking Indonesia dari Twitter. Studi komparatif pada domain non-banking juga menunjukkan konsistensi keunggulan SVM sebagaimana ditunjukkan Ningsih et al. (2024) dan Khaira et al. (2023), keduanya menggunakan TF-IDF namun tanpa uji statistik signifikansi.

### Naive Bayes dan Support Vector Machine

Multinomial Naive Bayes adalah algoritma probabilistik berbasis Teorema Bayes yang mengasumsikan independensi antar fitur dan dirancang untuk data diskrit seperti TF-IDF dengan parameter alpha untuk Laplace smoothing. Support Vector Machine bekerja dengan mencari hyperplane optimal yang memaksimalkan margin antara kelas dalam ruang fitur berdimensi tinggi (Cortes & Vapnik, 1995). Kernel linear dipilih karena data teks berbasis TF-IDF umumnya linearly separable di ruang dimensi tinggi dan lebih efisien secara komputasi. Perbedaan performa tanpa verifikasi statistik tidak dapat dipercaya sebagai bukti keunggulan algoritmik karena bisa jadi merupakan noise dari partisi data yang berbeda (Andrian et al., 2022).

---

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

---

## HASIL DAN PEMBAHASAN

### Hasil Eksperimen

Tabel 1 menyajikan hasil perbandingan run tunggal (random_state=42) dan Tabel 2 menyajikan hasil 10 run eksperimen.

Tabel 1. Hasil Perbandingan Run Tunggal (random_state=42)

| Algoritma | F1-Score | Akurasi |
|-----------|----------|---------|
| Naive Bayes | 0,5466 | 0,8385 |
| SVM | 0,5553 | 0,8455 |
| Selisih | +0,0087 | +0,0070 |

Tabel 2. Hasil F1-Score Macro-Average dari 10 Run Eksperimen

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

SVM menghasilkan F1-Score lebih tinggi pada 9 dari 10 run. Perbandingan visual ditunjukkan pada Gambar 2.

![Perbandingan F1-Score dan Akurasi NB vs SVM](grafik_perbandingan.png)
Gambar 2. Perbandingan F1-Score dan Akurasi Naive Bayes vs SVM

### Analisis Statistik

Tabel 3. Hasil Analisis Statistik

| Parameter | Nilai | Interpretasi |
|-----------|-------|-------------|
| p-value (Wilcoxon) | 0,0039 | p < α = 0,05 → H₀ ditolak |
| Cohen's d | 1,9428 | Large effect (d > 0,8) |

Nilai p = 0,0039 < α = 0,05 menunjukkan perbedaan F1-Score antara SVM dan Naive Bayes signifikan secara statistik sehingga H₀ ditolak dan H₁ diterima. Cohen's d = 1,9428 mengindikasikan large effect yang bermakna secara praktis.

### Pembahasan

Hasil penelitian ini konsisten dengan temuan studi sebelumnya yang menunjukkan keunggulan SVM atas Naive Bayes pada analisis sentimen teks Indonesia (Ningsih et al., 2024; Khaira et al., 2023; Andrian et al., 2022). Keunggulan SVM dapat dijelaskan oleh kemampuannya mencari hyperplane optimal di ruang dimensi tinggi representasi TF-IDF (Cortes & Vapnik, 1995), sehingga lebih robust terhadap noise pada ulasan berbahasa Indonesia yang mengandung singkatan tidak baku dan campur kode. Nilai F1-Score yang moderat mencerminkan tantangan distribusi kelas yang tidak seimbang — positif 69,7% berbanding netral 4,6%. Nilai akurasi yang relatif tinggi dibandingkan F1-Score mengkonfirmasi bias akibat class imbalance, memvalidasi pemilihan F1-Score macro-average sebagai metrik primer (Andrian et al., 2022). Effect size besar (Cohen's d = 1,9428) membuktikan perbedaan antara NB dan SVM konsisten dan bermakna secara praktis, bukan sekadar noise dari partisi data.

Penelitian ini berkontribusi mengisi gap metodologis yang teridentifikasi dari systematic literature review — ketiadaan perbandingan NB vs SVM dengan kondisi eksperimen identik pada dataset multi-bank ulasan mobile banking berbahasa Indonesia yang disertai uji statistik. Berbeda dari studi sebelumnya yang hanya membandingkan angka akurasi secara deskriptif (Edwina & Mauritsius, 2024; Samudera et al., 2024; Al Hakim & Irwiensyah, 2024), penelitian ini membuktikan bahwa perbedaan performa antara SVM dan Naive Bayes bukan sekadar noise melainkan perbedaan nyata yang dapat dipertanggungjawabkan secara ilmiah.

---

## SIMPULAN

Penelitian ini membandingkan Multinomial Naive Bayes dan SVM menggunakan TF-IDF untuk klasifikasi sentimen 6.000 ulasan mobile banking Indonesia dari BCA Mobile, Mandiri Online, dan BRImo. Hasil 10 run eksperimen menunjukkan SVM menghasilkan rata-rata F1-Score 0,5627 dibandingkan Naive Bayes 0,5532. Wilcoxon signed-rank test menghasilkan p = 0,0039 < α = 0,05 sehingga H₀ ditolak, dan Cohen's d = 1,9428 mengindikasikan large effect. SVM dengan kernel linear direkomendasikan sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

Penelitian ini memiliki beberapa limitasi yang perlu diperhatikan. Labeling otomatis dari rating bintang dapat mengandung inkonsistensi pada ulasan yang teksnya tidak sesuai dengan ratingnya. Hasil berlaku untuk tiga bank konvensional terbesar dan tidak otomatis berlaku untuk bank syariah, bank digital, atau platform ulasan lain. Representasi TF-IDF berbasis bag-of-words juga tidak menangkap konteks semantik secara mendalam.

Untuk penelitian lanjutan, disarankan eksplorasi model transformer seperti IndoBERT, perluasan dataset ke bank digital dan syariah, serta penerapan aspect-based sentiment analysis.

---

## REFERENSI

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