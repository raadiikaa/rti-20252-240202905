# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
   | Naive Bayes  | 0,5532 | 0,0052 | 0,5541 | 0,5456 | 0,5599 | 10 |
   | SVM          | 0,5627 | 0,0045 | 0,5624 | 0,5541 | 0,5691 | 10 |

2. Uji Hipotesis:
   Uji yang digunakan  : Wilcoxon signed-rank test (paired,     non-parametrik)
   Justifikasi          : Data berpasangan (NB dan SVM diuji pada   partisi data identik di tiap run) dengan n=10 kecil — Wilcoxon dipili sebelum eksperimen (pre-registration) karena tidak mengasumsikan distribusi normal, cocok untuk ukuran sampel kecil
   Hasil: p = 0,0039, effect size (Cohen's d) = 1,9428
   CI 95% selisih F1 (SVM−NB) : [0,0060 ; 0,0130]  *(dihitung post-hoc dari 10 run, paired t-based CI — bukan digunakan untuk mengubah keputusan hipotesis, hanya melengkapi interpretasi)

3. Keputusan:
   [✅] H₀ ditolak → H₁ diterima (p = 0,0039 < α = 0,05)
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : RQ bertanya apakah SVM menghasilkan F1-Score lebih tinggi dari NB — hasil membuktikan SVM unggul secara statistik dan praktis (large effect)
   Practical significance: Cohen's d = 1,9428 jauh di atas ambang large effect (>0,8) — selisih F1 rata-rata 0,0095 konsisten di 9 dari 10 run, bukan kebetulan partisi data
   Perbandingan literatur: Konsisten dengan Edwina & Mauritsius (2024) dan Andrian et al. (2022) yang juga menemukan SVM unggul dari NB pada teks berbahasa Indonesia

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | Construct validity | Rating bintang sebagai proxy label sentimen | Ulasan 1★ karena bug teknis bisa dilabel "negatif" padahal netral | Diakui eksplisit; disarankan validasi manual subsampel di penelitian lanjutan |
   | Statistical limitation | n=10 run — ukuran sampel kecil untuk uji statistik | Power test terbatas meski hasil signifikan | CI 95% dilaporkan untuk transparansi rentang ketidakpastian |
   | Internal validity | Tidak ada langkah dedup — potensi ulasan template terhitung ganda | Bisa sedikit memengaruhi distribusi kelas | Diakui sebagai limitasi pipeline (lihat WS-13) |
   | External validity | Hanya 3 bank konvensional, periode 2022–2024 | Tidak otomatis berlaku untuk bank syariah/digital | Dinyatakan eksplisit sebagai batas generalisasi di Simpulan |

6. Failure Analysis (H₀ ditolak, TIDAK berlaku — dicantumkan untuk   kelengkapan): Karena H₀ berhasil ditolak dengan p dan effect size yang solid, tidak ada "failure" pada level hipotesis utama. Namun catatan penting: F1-Score kelas netral pada classification_report kedua algoritma tercatat 0,00 — ini adalah bentuk failure parsial yang layak dianalisis di bawah.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|------------|---------|
| Berapa grup yang dibandingkan? | 2 (Naive Bayes vs SVM) |
| Apakah data berpasangan (paired)? | Ya — kedua algoritma diuji pada partisi train-test yang identik di tiap run (random_state sama untuk NB dan SVM dalam 1 run) |
| Apakah distribusi normal? | Diuji post-hoc dengan Shapiro-Wilk pada selisih (SVM−NB): W=0,943, p=0,588 → tidak signifikan menyimpang dari normal. Namun keputusan uji ditetapkan sebelum melihat data ini |
| **Uji yang dipilih:** | Wilcoxon signed-rank test |
| **Justifikasi:** | Ditetapkan sejak WS-04 (pre-registration) sebagai uji non-parametrik yang aman untuk n=10 kecil tanpa asumsi normalitas — meskipun uji normalitas post-hoc menunjukkan data cukup normal, keputusan awal tetap dipertahankan karena mengubah metode analisis setelah melihat data adalah p-hacking (WS-05) |

**Effect size yang akan dilaporkan:** [✅] Cohen's d 
---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Algoritma | F1-Score macro (mean ± std) | n |
|-----------|------------------------------|---|
| Naive Bayes | 0,5532 ± 0,0052 | 10 |
| SVM | 0,5627 ± 0,0045 | 10 |

p = 0,0039, Cohen's d = 1,9428, CI 95% = [0,0060 ; 0,0130]

| Aspek | Interpretasi |
|-------|--------------|
| Signifikansi statistik | p = 0,0039 < α = 0,05 → signifikan secara statistik, H₀ ditolak |
| Effect size | Cohen's d = 1,9428 → large effect (jauh di atas ambang 0,8), lebih dari dua kali lipat ambang "large" |
| Practical significance | Selisih rata-rata F1 hanya 0,0095 (0,95 poin persentase) — kecil dalam angka absolut, tapi konsisten di 9 dari 10 run dengan variabilitas rendah (std SVM 0,0045 < std NB 0,0052), sehingga meskipun selisih absolut kecil, keandalan/konsistensi keunggulan SVM lah yang membuatnya bermakna praktis |
| Hubungan ke RQ | Menjawab langsung RQ: SVM terbukti unggul secara statistik maupun praktis untuk klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF |
| Perbandingan literatur | Sejalan dengan Andrian et al. (2022) yang menemukan SVM unggul di data digital banking Indonesia, dan Edwina & Mauritsius (2024) yang menemukan SVM akurasi 91% pada SimobiPlus — namun penelitian ini menjadi yang pertama memverifikasi keunggulan tersebut dengan uji statistik formal pada dataset multi-bank |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Hipotesis utama penelitian ini (H₁: SVM > NB) berhasil didukung (p=0,0039, Cohen's d=1,9428). Namun saat classification_report per kelas diperiksa, ditemukan F1-Score kelas netral = 0,00 pada kedua algoritma (NB maupun SVM) — sebuah failure parsial di level sub-kelas yang tidak terlihat dari F1-Score macro-average saja.

| Pertanyaan | Jawaban |
|------------|---------|
| Apakah ini "gagal"? | Bukan gagal pada hipotesis utama (H₁ tetap didukung), tapi merupakan failure parsial pada level per-kelas yang layak dianalisis terpisah |
| Kemungkinan penyebab? | Kelas netral hanya 276 dari 5.758 data (4,8%) — setelah split 80:20, testing set hanya berisi ±55 sampel netral. Baik NB maupun SVM cenderung memprediksi kelas mayoritas (positif) ketika data sangat timpang, sehingga precision/recall kelas netral mendekati nol |
| Boundary condition? | Kedua algoritma efektif untuk klasifikasi biner-dominan (positif vs negatif) tapi gagal pada kelas minoritas ekstrem (<5% dari data) tanpa teknik penyeimbangan kelas (oversampling, class_weight) |
| Insight yang bisa diambil? | Rekomendasi berbasis F1-Score macro-average yang "SVM lebih baik" perlu diberi catatan: keunggulan itu didorong oleh performa pada kelas positif dan negatif, bukan netral. Penelitian lanjutan perlu menerapkan SMOTE atau class_weight='balanced' khusus untuk menangani kelas netral |
| Apakah layak dilaporkan? Mengapa? | Ya — ini adalah bentuk kejujuran ilmiah (WS-01) dan mencegah pembaca menyimpulkan bahwa SVM "sempurna" di ketiga kelas. Melaporkannya justru memperkuat kredibilitas penelitian dan membuka arah riset lanjutan yang jelas |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Kelas netral hanya 4,6% dari data, testing set ±55 sampel | F1 kelas netral tidak reliable, mendekati 0 pada kedua algoritma |
| Construct validity | Class imbalance tidak ditangani (tidak ada oversampling) | F1 macro-average tetap lebih baik dari akurasi, tapi belum sepenuhnya mengatasi bias kelas minoritas |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Failure dalam riset ini muncul bukan di level hipotesis utama (yang justru berhasil didukung), tapi di level yang lebih halus: performa kelas netral. Sebelum memahami failure analysis, kemungkinan besar temuan F1 kelas netral = 0,00 akan diabaikan atau disembunyikan karena "mengganggu" narasi keberhasilan SVM. Setelah memahami bahwa partial failure + analisis mendalam adalah kontribusi yang lebih kaya daripada full success tanpa analisis, temuan ini justru dilaporkan secara eksplisit sebagai bagian dari limitasi dan arah penelitian lanjutan — mengubah nilai penelitian dari sekadar "SVM menang" menjadi "SVM menang, tapi dengan boundary condition yang jelas pada kelas minoritas ekstrem."
