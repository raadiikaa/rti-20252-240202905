# 01-abstrak.md — Abstrak

## ABSTRAK

Aplikasi mobile banking di Indonesia menghasilkan jutaan ulasan pengguna di Google Play Store yang berpotensi menjadi sumber insight strategis bagi pengembang. Namun, belum tersedia panduan berbasis bukti empiris untuk pemilihan algoritma klasifikasi sentimen pada teks berbahasa Indonesia di domain perbankan. Penelitian ini membandingkan Multinomial Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF pada dataset 6.000 ulasan dari BCA Mobile, Mandiri Online, dan BRImo. Pipeline klasifikasi dibangun dengan lima komponen modular dan diuji pada kondisi eksperimen identik menggunakan 10 run dengan random seed berbeda. Perbedaan performa diverifikasi menggunakan Wilcoxon signed-rank test (α = 0,05) dan Cohen's d. Hasil menunjukkan SVM menghasilkan rata-rata F1-Score 0,5627 dibandingkan Naive Bayes 0,5532, dengan perbedaan signifikan secara statistik (p = 0,0039) dan effect size besar (Cohen's d = 1,9428). SVM direkomendasikan sebagai algoritma klasifikasi sentimen untuk ulasan mobile banking berbahasa Indonesia.

**Kata Kunci:** Analisis Sentimen; Naive Bayes; Support Vector Machine; TF-IDF; Mobile Banking

---

## ABSTRACT

Mobile banking applications in Indonesia generate millions of user reviews on Google Play Store as potential strategic insights for developers. However, no empirical evidence-based guidance exists for selecting sentiment classification algorithms for Indonesian-language text in the banking domain. This study compares Multinomial Naive Bayes and Support Vector Machine (SVM) using TF-IDF representation on a dataset of 6,000 reviews from BCA Mobile, Mandiri Online, and BRImo. A modular five-component classification pipeline was tested under identical experimental conditions using 10 runs with different random seeds. Performance differences were verified using the Wilcoxon signed-rank test (α = 0.05) and Cohen's d. Results show SVM achieved a mean F1-Score of 0.5627 compared to Naive Bayes at 0.5532, with a statistically significant difference (p = 0.0039) and large effect size (Cohen's d = 1.9428). SVM is recommended as the sentiment classification algorithm for Indonesian mobile banking reviews.

**Keywords:** Sentiment Analysis; Naive Bayes; Support Vector Machine; TF-IDF; Mobile Banking