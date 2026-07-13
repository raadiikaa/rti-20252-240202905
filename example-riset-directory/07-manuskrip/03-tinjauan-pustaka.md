# 03-tinjauan-pustaka.md — Tinjauan Pustaka

## TINJAUAN PUSTAKA

### Analisis Sentimen pada Ulasan Mobile Banking Indonesia

Penelitian analisis sentimen pada ulasan mobile banking Indonesia didominasi penggunaan Naive Bayes sebagai metode tunggal tanpa pembanding terkontrol. Al Hakim dan Irwiensyah (2024) menerapkan Multinomial Naive Bayes pada 2.000 ulasan BCA Mobile dan menghasilkan akurasi 86,83% namun precision hanya 52,78%. Samudera et al. (2024) menggunakan Multinomial Naive Bayes pada ulasan BSI Mobile dan Action Mobile tanpa pembanding algoritmik. Soliha et al. (2023) juga menerapkan Naive Bayes pada ulasan digital banking tanpa pembanding dan tanpa uji statistik. Studi yang menyertakan SVM menunjukkan hasil lebih menjanjikan — Edwina dan Mauritsius (2024) menemukan SVM mencapai akurasi 91% pada SimobiPlus, dan Andrian et al. (2022) menemukan SVM menghasilkan F1-Score tertinggi sebesar 73,34% pada data digital banking Indonesia dari Twitter. Studi komparatif pada domain non-banking juga menunjukkan konsistensi keunggulan SVM sebagaimana ditunjukkan Ningsih et al. (2024) dan Khaira et al. (2023), keduanya menggunakan TF-IDF namun tanpa uji statistik signifikansi.

### Naive Bayes dan Support Vector Machine

Multinomial Naive Bayes adalah algoritma probabilistik berbasis Teorema Bayes yang mengasumsikan independensi antar fitur dan dirancang untuk data diskrit seperti TF-IDF dengan parameter alpha untuk Laplace smoothing. Support Vector Machine bekerja dengan mencari hyperplane optimal yang memaksimalkan margin antara kelas dalam ruang fitur berdimensi tinggi (Cortes & Vapnik, 1995). Kernel linear dipilih karena data teks berbasis TF-IDF umumnya linearly separable di ruang dimensi tinggi dan lebih efisien secara komputasi. Perbedaan performa tanpa verifikasi statistik tidak dapat dipercaya sebagai bukti keunggulan algoritmik karena bisa jadi merupakan noise dari partisi data yang berbeda (Andrian et al., 2022).