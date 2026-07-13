# Perbandingan Naive Bayes dan SVM Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia

**Judul:** Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

**Target publikasi:** TIIJ (Technology and Informatics Insight Journal), Universitas Putra Bangsa Kebumen — Sinta 5

## Ringkasan

Penelitian ini membandingkan performa Multinomial Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF untuk klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store. Eksperimen dilakukan pada dataset 6.000 ulasan dengan pipeline klasifikasi modular lima komponen, diuji 10 run dengan random seed berbeda, dan perbedaan performa diverifikasi menggunakan Wilcoxon signed-rank test dan effect size Cohen's d. Hasil menunjukkan SVM unggul secara signifikan (F1-Score 0,5627 vs 0,5532, p=0,0039, Cohen's d=1,9428) dan direkomendasikan sebagai algoritma klasifikasi sentimen untuk domain ini.

Detail lengkap topik & roadmap: [09-docs/rencana-penelitian.md](09-docs/rencana-penelitian.md)

## Struktur Direktori

| Folder | Isi |
|---|---|
| [00-admin/](00-admin/) | Administrasi penelitian (jadwal, korespondensi) |
| [01-proposal/](01-proposal/) | Proposal penelitian |
| [02-literatur/](02-literatur/) | Matriks literatur 8 paper SLR + BibTeX 11 entri |
| [03-teori/](03-teori/) | Arsitektur pipeline & skema eksperimen (Tahap 1) |
| [04-data/](04-data/) | Dataset ulasan mentah & bersih + hasil eksperimen (CSV) |
| [05-kode/](05-kode/) | Notebook Google Colab: `NB_vs_SVM_Sentiment_MobileBanking.ipynb` |
| [06-output/](06-output/) | Tabel & grafik hasil eksperimen (Tahap 4) |
| [07-manuskrip/](07-manuskrip/) | Naskah jurnal lengkap — .md & .docx (Tahap 5) |
| [08-laporan/](08-laporan/) | Laporan penelitian komprehensif |
| [09-docs/](09-docs/) | Dokumen perencanaan & roadmap tahap-tahap penelitian |

## Status Tahapan

- [x] **Tahap 1** — Perencanaan dan Studi Literatur — *Selesai* ([detail](09-docs/tahap-1-arsitektur-dan-skema-database.md))
- [x] **Tahap 2** — Perancangan Sistem dan Desain Eksperimen — *Selesai* ([detail](09-docs/tahap-2-implementasi-pipeline-klasifikasi-(phyton).md))
- [x] **Tahap 3** — Pengumpulan Data dan Preprocessing — *Selesai* ([detail](09-docs/tahap-3-pengumpulan-data-preprocessing.md))
- [x] **Tahap 4** — Eksperimen dan Analisis — *Selesai* ([detail](09-docs/tahap-4-analisis-data.md))
- [x] **Tahap 5** — Penulisan Naskah Jurnal — *Selesai* ([detail](09-docs/tahap-5-draf-paper.md))

## Laporan Penelitian

Laporan penelitian komprehensif (ringkasan eksekutif, metodologi per tahap, hasil, kendala, kesimpulan): [08-laporan/laporan-penelitian.md](08-laporan/laporan-penelitian.md)

## Author

Radika Rismawati Tri Prasaja — 240202905