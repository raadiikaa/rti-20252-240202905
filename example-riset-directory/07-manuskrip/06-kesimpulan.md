# 06-kesimpulan.md — Simpulan

## SIMPULAN

Penelitian ini membandingkan Multinomial Naive Bayes dan SVM menggunakan TF-IDF untuk klasifikasi sentimen 6.000 ulasan mobile banking Indonesia dari BCA Mobile, Mandiri Online, dan BRImo. Hasil 10 run eksperimen menunjukkan SVM menghasilkan rata-rata F1-Score 0,5627 dibandingkan Naive Bayes 0,5532. Wilcoxon signed-rank test menghasilkan p = 0,0039 < α = 0,05 sehingga H₀ ditolak, dan Cohen's d = 1,9428 mengindikasikan large effect. SVM dengan kernel linear direkomendasikan sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

Penelitian ini memiliki beberapa limitasi yang perlu diperhatikan. Labeling otomatis dari rating bintang dapat mengandung inkonsistensi pada ulasan yang teksnya tidak sesuai dengan ratingnya. Hasil berlaku untuk tiga bank konvensional terbesar dan tidak otomatis berlaku untuk bank syariah, bank digital, atau platform ulasan lain. Representasi TF-IDF berbasis bag-of-words juga tidak menangkap konteks semantik secara mendalam.

Untuk penelitian lanjutan, disarankan eksplorasi model transformer seperti IndoBERT, perluasan dataset ke bank digital dan syariah, serta penerapan aspect-based sentiment analysis.