# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment)
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [✅] Problem → Gap: masalah terdokumentasi di literatur
       Ketiadaan panduan berbasis bukti untuk memilih algoritma 
       klasifikasi sentimen ulasan mobile banking Indonesia 
       terdokumentasi dari 8 paper systematic review (WS-03)
  [✅] Gap → RQ: pertanyaan menjawab gap spesifik
       RQ langsung menanyakan apakah SVM lebih unggul dari NB 
       dalam kondisi eksperimen terkontrol — menjawab gap 
       ketiadaan perbandingan sistematis dengan uji statistik
  [✅] RQ → Hypothesis: hipotesis memprediksi jawaban
       H₁ memprediksi SVM menghasilkan F1-Score lebih tinggi 
       secara signifikan dari NB pada α = 0,05
  [✅] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
       F1-Score macro-average mengukur performa klasifikasi yang 
       ada di H₁; Wilcoxon test memverifikasi signifikansinya; 
       Cohen's d mengukur besaran perbedaan praktis
  [✅] Metric → System: komponen sistem menghasilkan/mengukur metrik
       Modul Evaluator menghasilkan F1-Score, Akurasi, Precision, 
       Recall otomatis setiap run dan menyimpan ke results.csv
  [✅] System → Experiment: desain eksperimen menggunakan sistem
       Pipeline lima komponen (Data Loader → Preprocessor → 
       Vectorizer → Classifier → Evaluator) digunakan sebagai 
       instrumen eksperimen comparison study NB vs SVM dengan 
       10 run dan Wilcoxon test

Koneksi Horizontal (Konsistensi):
  [✅] Istilah sama di semua bagian
       "Naive Bayes", "SVM", "F1-Score macro-average", "TF-IDF", 
       "mobile banking Indonesia" konsisten dari WS-02 sampai WS-07
  [✅] Variabel di RQ = variabel di hipotesis = metrik di desain
       IV: jenis algoritma (NB vs SVM) — konsisten di WS-04, 05, 06, 07
       DV: F1-Score macro-average — konsisten di WS-04, 05, 06, 07
       CV: TF-IDF, split 80:20, preprocessing — konsisten di semua WS
  [✅] Scope tidak berubah dari masalah ke eksperimen
       Scope selalu: ulasan mobile banking Indonesia (BCA Mobile, 
       Mandiri Online, BRImo) di Google Play Store — tidak ada 
       perluasan atau penyempitan scope antar WS

Rubrik Self-Assessment:
| Kriteria | 1 (Lemah) | 2 (Cukup) | 3 (Baik) | Skor |
|----------|-----------|-----------|----------|------|
| Koherensi |          |           |    ✅    |   3  |
| Specificity |        |           |    ✅    |   3  |
| Feasibility |        |     ✅    |          |   2  |
| Rigor     |          |           |    ✅    |   3  |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Tim pengembang aplikasi mobile banking Indonesia tidak memiliki panduan berbasis bukti untuk memilih algoritma klasifikasi sentimen yang paling efektif bagi teks ulasan berbahasa Indonesia pada domain perbankan. Akibatnya, pemilihan algoritma dilakukan secara ad-hoc tanpa landasan empiris yang kontekstual (Al Hakim & Irwiensyah, 2024) |
| Gap | WS-03 | Dari 8 paper systematic review, tidak ada satupun yang membandingkan NB vs SVM dengan kondisi eksperimen identik pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store sekaligus disertai uji statistik signifikansi — Method Gap + Context Gap yang dibuktikan 8 paper |
| RQ | WS-04 | Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF? |
| Hipotesis | WS-04 | H₀: Tidak terdapat perbedaan signifikan F1-Score antara SVM dan Naive Bayes (α = 0,05); H₁: SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF (α = 0,05) |
| Variabel & Metrik | WS-05 | IV: jenis algoritma klasifikasi (MultinomialNB vs SVC kernel linear) — Nominal; DV primary: F1-Score macro-average (Ratio, 0–1) diukur via sklearn.metrics; DV secondary: Akurasi, Precision, Recall (Ratio, 0–1); CV: TF-IDF max_features=5.000, split 80:20 stratified, preprocessing identik, dataset identik |
| Sistem | WS-06 | Pipeline lima komponen modular: Data Loader (CV) → Preprocessor (CV) → Vectorizer TF-IDF (CV) → Classifier (IV — satu-satunya yang di-swap NB↔SVM via config.yaml) → Evaluator (DV — menghasilkan F1, Akurasi, Precision, Recall ke results.csv otomatis setiap run) |
| Desain Eksperimen | WS-07 | Comparison study: kondisi A (MultinomialNB + TF-IDF) vs kondisi B (SVC linear + TF-IDF) pada 6.000 ulasan Google Play Store yang identik; 10 run dengan random_state berbeda (0–9); fairness dijaga dengan config-driven execution; dianalisis dengan Wilcoxon signed-rank test (α = 0,05) dan effect size Cohen's d |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅ | Gap muncul dari analisis 8 paper systematic review (WS-03) yang membuktikan tidak ada studi yang membandingkan NB vs SVM secara terkontrol pada domain mobile banking Indonesia — bukan opini, melainkan ketiadaan yang terdokumentasi dengan bukti pencarian |
| Gap → RQ | ✅ | RQ di WS-04 langsung menanyakan perbandingan NB vs SVM dengan kondisi terkontrol pada dataset multi-bank ulasan mobile banking Indonesia di Google Play Store — menjawab tepat ketiga elemen gap (perbandingan terkontrol + multi-bank + uji statistik) |
| RQ → Hypothesis | ✅ | H₁ di WS-04 memprediksi jawaban RQ secara falsifiable: "SVM menghasilkan F1-Score yang secara signifikan lebih tinggi" — bisa terbukti salah jika p ≥ 0,05; H₀ dirumuskan sebagai kondisi default yang harus dibuktikan salah |
| Hypothesis → Metric | ✅ | F1-Score macro-average (WS-05) mengukur langsung variabel dalam H₁ — "F1-Score lebih tinggi" memerlukan pengukuran F1 per run; Wilcoxon test mengukur signifikansi perbedaan yang diklaim; Cohen's d mengukur besaran perbedaan praktis; semua metrik dipilih sebelum eksperimen (pre-registration) |
| Metric → System | ✅ | Modul Evaluator di pipeline (WS-06) menghasilkan F1-Score, Akurasi, Precision, Recall otomatis setiap run via sklearn.metrics dan menyimpan ke results.csv — ada jalur nyata dari metrik ke komponen sistem tanpa pengukuran manual |
| System → Experiment | ✅ | Desain eksperimen di WS-07 menggunakan pipeline sebagai instrumen comparison study: kondisi A menggunakan Classifier=MultinomialNB, kondisi B menggunakan Classifier=SVC, semua komponen lain identik; 10 run dijalankan via pipeline yang sama dengan config yang berbeda |

**Koneksi mana yang paling lemah?** Hypothesis → Metric
**Bagaimana cara memperkuatnya?**
> Koneksi Hypothesis → Metric perlu diperkuat dengan menambahkan justifikasi eksplisit mengapa F1-Score macro-average lebih tepat dari akurasi untuk mengukur klaim dalam H₁. Justifikasi ini sudah ada di WS-05 (distribusi kelas tidak seimbang: positif 69,7%, negatif 25,7%, netral 4,6%) dan sudah disertai sitasi Andrian et al. (2022). Namun untuk memperkuat lebih lanjut, perlu ditambahkan penjelasan bahwa Wilcoxon test dipilih bukan hanya karena n=10 kecil, tetapi karena secara eksplisit cocok untuk membandingkan dua kondisi berpasangan (paired comparison) pada distribusi yang tidak dapat diasumsikan normal.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [✅] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi? Terminologi "Naive Bayes", "SVM", "F1-Score macro-average", "TF-IDF", "mobile banking Indonesia", "BCA Mobile, Mandiri Online, BRImo", dan "Google Play Store" konsisten dari WS-02 sampai WS-07 tanpa ada perubahan nama atau scope. IV selalu disebut "jenis algoritma klasifikasi", DV selalu disebut "F1-Score macro-average sebagai primary metric", dan CV selalu merujuk ke TF-IDF max_features=5.000 dan split 80:20 di semua WS.

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Semua 6 koneksi kritis terpenuhi tanpa putus — Problem → Gap → RQ → Hypothesis → Metric → System → Experiment mengalir logis dan konsisten. Terminologi identik di semua WS. Scope tidak berubah dari WS-02 sampai WS-07 |
| Specificity | 3 | Semua variabel terdefinisi numerik dengan satuan eksplisit: IV nominal (NB vs SVM), DV ratio 0–1 (F1-Score macro-average via sklearn), CV nilai spesifik (max_features=5.000, split 80:20, random_state 0–9). Dataset disebutkan secara eksplisit: 6.000 ulasan dari 3 aplikasi spesifik |
| Feasibility | 2 | Secara teknis sangat feasible — Python di Google Colab gratis, dataset bisa discraping, library open source tersedia. Skor 2 bukan 3 karena ada satu risiko: scraping Google Play Store bisa terbatas oleh kebijakan Google yang bisa berubah sewaktu-waktu, sehingga perlu backup plan berupa dataset Kaggle. Waktu 8 minggu realistis untuk cakupan penelitian ini |
| Rigor | 3 | Eksperimen menggunakan 10 run dengan random_state berbeda untuk stabilitas hasil; Wilcoxon signed-rank test dipilih dengan justifikasi yang tepat (non-parametrik, paired); effect size Cohen's d ditambahkan untuk memisahkan signifikansi statistik dari makna praktis; ancaman validitas diidentifikasi sebelum eksperimen dengan mitigasi spesifik |

**Skor total:** 11 / 12

**Apakah proposal siap untuk fase eksekusi?** [✅] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki? Proposal sudah siap untuk fase eksekusi karena semua 6 koneksi kritis terpenuhi, variabel teroperasionalisasi dengan jelas, sistem pipeline sudah dirancang modular dan traceable, desain eksperimen sudah fair dan rigorous. Satu hal yang perlu disiapkan sebelum eksekusi adalah backup plan dataset (Kaggle) jika scraping Google Play terkendala, dan spot-check manual 100–200 ulasan untuk memverifikasi konsistensi proxy labeling dari rating bintang.
---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** WS-01 (Identifikasi Distorsi)
                     WS-01 terasa paling mudah karena tugasnya bersifat analitis terhadap paper yang sudah ada — membaca paper orang lain dan mengidentifikasi distorsi di setiap tahap Research Trust Model. Tidak ada tekanan untuk menciptakan sesuatu yang baru, cukup membaca dengan kritis dan mengisi tabel yang sudah tersedia. Keterampilan ini lebih natural karena mirip dengan cara membaca biasa, hanya dengan kerangka yang lebih terstruktur.

**Bagian tersulit:** WS-03 (Literature Mapping & Gap Identification)
                     WS-03 adalah bagian yang paling menantang karena menuntut dua hal sekaligus: membaca banyak paper secara concept-centric bukan per penulis, dan membuktikan bahwa gap benar-benar ada bukan sekadar klaim. Kesulitan utamanya adalah membedakan antara "belum ada yang meneliti" sebagai klaim kosong dengan gap yang terdokumentasi dari bukti pencarian yang sistematis. Selain itu, memilih baseline yang relevan dan representatif tanpa terjebak straw man comparison memerlukan pertimbangan yang lebih dalam dari yang terlihat di permukaan.

**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, hal pertama yang akan dilakukan berbeda adalah menentukan topik penelitian dan metode sejak WS-01 — bukan berubah-ubah sampai WS-04. Perubahan topik di tengah jalan menyebabkan WS-01 sampai WS-03 harus direvisi ulang agar selaras dengan topik yang akhirnya dipilih di WS-04, yang menghabiskan banyak waktu dan energi. Selain itu, akan lebih awal melakukan verifikasi nama penulis jurnal langsung dari dokumen aslinya — bukan mengandalkan hasil pencarian — untuk menghindari inkonsistensi nama yang baru ditemukan di akhir proses. Terakhir, akan lebih awal membuat keputusan tentang tools analisis (Python di Google Colab) agar desain sistem dari WS-06 sudah langsung bisa diimplementasikan tanpa perlu penyesuaian di kemudian hari.
