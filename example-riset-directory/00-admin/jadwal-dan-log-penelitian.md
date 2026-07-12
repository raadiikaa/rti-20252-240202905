# Jadwal & Log Pelaksanaan Penelitian

Catatan kronologis pelaksanaan tiap tahap (sumber: riwayat commit git & notebook `NB_vs_SVM_Sentiment_MobileBanking.ipynb`). Tanggal mengikuti `git log`.

## Log Pelaksanaan

| Tanggal | Tahap | Aktivitas | Referensi |
|---|---|---|---|
| 2026-05-12 ~15:30 s.d. ~16:00 | Tahap 1 & 2 | Setup environment Google Colab: instalasi google-play-scraper; import library (pandas, numpy, sklearn, nltk); scraping ulasan Google Play Store — BCA Mobile (com.bca) 2.000 ulasan, Mandiri Online (com.bankmandiri.mandirionline) 2.000 ulasan, BRImo (id.co.bri.brimo) 2.000 ulasan; gabung + labeling sentimen (positif 4.184, netral 276, negatif 1.540); simpan dataset_ulasan_banking.csv | Cell 1–7, NB_vs_SVM_Sentiment_MobileBanking.ipynb |
| 2026-05-12 ~16:00 | Tahap 3 | Instalasi PySastrawi; implementasi fungsi preprocessing (lowercase, remove noise, stopword removal, stemming Bahasa Indonesia); dijalankan pada 6.000 ulasan → 5.758 data valid setelah cleaning; simpan dataset_bersih.csv | Cell 8–10, NB_vs_SVM_Sentiment_MobileBanking.ipynb |
| 2026-05-12 ~16:05 | Tahap 4 | TF-IDF vectorizer max_features=5.000; split 80:20 stratified random_state=42 (train=4.606, test=1.152); training + evaluasi MultinomialNB (F1=0,5466, Akurasi=0,8385) dan SVC linear C=1.0 (F1=0,5553, Akurasi=0,8455); tabel perbandingan disimpan ke hasil_perbandingan.csv; bar chart disimpan ke grafik_perbandingan.png | Cell 11–15, NB_vs_SVM_Sentiment_MobileBanking.ipynb |
| 2026-05-12 ~16:10 | Tahap 5 | 10 run eksperimen dengan random_state=0–9; Wilcoxon signed-rank test (p=0,0039 → H₀ ditolak); effect size Cohen's d=2,0479 (large effect); rata-rata F1 NB=0,5532 vs SVM=0,5627; hasil disimpan ke hasil_statistik.csv; download semua file output | Cell 16–17, NB_vs_SVM_Sentiment_MobileBanking.ipynb |

## Status Ringkas

- **Tahap 1–5**: Selesai (2026-05-12, ~40 menit di Google Colab).
- **Dokumentasi WS**: Selesai WS-01 s.d. WS-12 (2026-04-12 s.d. 2026-06-23).
- **Naskah/laporan**: Belum dimulai — menunggu penyelesaian seluruh WS.

## Item Tindak Lanjut (Checklist Sebelum Submission)

- [✅] Scraping 6.000 ulasan dari 3 aplikasi mobile banking (BCA Mobile, Mandiri Online, BRImo)
- [✅] Preprocessing dengan PySastrawi (stopword removal + stemming Bahasa Indonesia)
- [✅] Training + evaluasi NB dan SVM dengan TF-IDF max_features=5.000
- [✅] 10 run eksperimen dengan random_state=0–9
- [✅] Uji statistik Wilcoxon (p=0,0039) + Cohen's d (2,0479)
- [✅] Seluruh WS (01–12) selesai didokumentasikan
- [ ] Penulisan naskah/laporan penelitian
- [ ] Review akhir konsistensi angka antar dokumen
- [ ] Submission ke jurnal (jika diperlukan)

## Korespondensi

*(belum ada — tambahkan catatan bimbingan dengan dosen RTI di sini saat tersedia)*