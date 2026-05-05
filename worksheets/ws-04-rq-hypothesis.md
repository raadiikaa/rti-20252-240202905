# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Mayoritas studi analisis sentimen ulasan aplikasi mobile banking Indonesia hanya menggunakan satu algoritma tanpa pembanding yang terkontrol, atau melakukan perbandingan pada domain lain seperti e-commerce dan media sosial. Belum terdapat studi yang secara sistematis membandingkan Naive Bayes dan SVM menggunakan TF-IDF dengan kondisi eksperimen identik pada dataset multi-bank (BCA Mobile, Mandiri Online, BRImo) dari Google Play Store, sekaligus membuktikan signifikansi perbedaannya secara statistik.

Research Question:
  Tipe         : [✅] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?
  Variabel IV  : Jenis algoritma klasifikasi (Naive Bayes vs SVM)
  Variabel DV  : F1-Score macro-average (primary), Akurasi, Precision, Recall (secondary)
  Metrik       : F1-Score macro-average skala 0–1
  Dataset      : Ulasan pengguna BCA Mobile, Mandiri Online, BRImo dari Google Play Store (±2.000 ulasan per aplikasi, total ±6.000 ulasan, bahasa Indonesia, periode 2022–2024)
  Baseline     : Multinomial Naive Bayes

Quality Check RQ:
  [✅] Variabel spesifik — Naive Bayes vs SVM disebutkan eksplisit
  [✅] Metrik jelas — F1-Score macro-average skala 0–1
  [✅] Baseline ada — Multinomial Naive Bayes sebagai pembanding
  [✅] Konteks disebutkan — mobile banking Indonesia, Google Play Store
  [✅] Memerlukan eksperimen (bukan hanya survei literatur) — tidak bisa dijawab hanya dari survei literatur

Contribution Statement:
  Apa yang baru diketahui : Algoritma mana (Naive Bayes atau SVM) yang lebih efektif untuk klasifikasi sentimen teks ulasan berbahasa Indonesia pada domain mobile banking menggunakan TF-IDF, sehingga pengembang aplikasi perbankan Indonesia dapat memilih algoritma berbasis bukti empiris yang kontekstual
  Jenis kontribusi        : [ ] Improvement  [✅] Comparison  [ ] Novel approach
  Gap yang diisi          : Ketiadaan studi komparatif NB vs SVM dengan kondisi eksperimen terkontrol dan uji statistik pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan F1-Score antara algoritma SVM dan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi TF-IDF
  H₁ : Algoritma SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi TF-IDF
  Threshold              : α = 0.05
  Justifikasi threshold  : Threshold α = 0.05 merupakan standar yang paling umum digunakan dalam penelitian komputasi dan ilmu data, memberikan keseimbangan antara risiko false positive (kesalahan tipe I) dan kekuatan statistik yang memadai untuk menarik kesimpulan yang dapat dipertanggungjawabkan secara ilmiah
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Belum terdapat studi yang secara sistematis membandingkan Naive Bayes dan SVM dengan kondisi eksperimen identik (preprocessing, TF-IDF, dan split data yang sama) pada dataset multi-bank ulasan mobile banking berbahasa Indonesia di Google Play Store, sekaligus disertai uji statistik untuk membuktikan signifikansi perbedaannya (Method Gap + Context Gap, dibuktikan 8 paper)

**RQ versi pertama (tulis bebas):** 
> "Bagaimana perbandingan performa Naive Bayes dan SVM untuk analisis sentimen ulasan mobile banking Indonesia?"

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Ya | Naive Bayes vs SVM — keduanya disebutkan eksplisit |
| Metrik terukur | Belum | Perlu ditambahkan F1-Score macro-average sebagai primary metric |
| Baseline | Ya| Naive Bayes sebagai pembanding |
| Dataset/konteks | Belum Spesifik | Perlu menyebut nama aplikasi, platform, dan bahasa secara eksplisit |

**Tipe RQ:** [✅] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> "Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?"

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak terdapat perbedaan signifikan F1-Score antara algoritma SVM dan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi TF-IDF |
| H₁ | Algoritma SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi TF-IDF |
| Metrik | F1-Score macro-average (skala 0–1), dihitung via sklearn.metrics.f1_score(average='macro') |
| Threshold | α = 0.05 |
| Justifikasi threshold | α = 0.05 adalah standar internasional yang paling umum digunakan dalam penelitian komputasi — memberikan keseimbangan antara risiko kesalahan tipe I (false positive) dan kekuatan uji statistik yang memadai |

**Apakah hipotesis ini falsifiable?** [✅] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? H₀ akan ditolak jika uji Wilcoxon signed-rank test pada hasil 10 run eksperimen menunjukkan p-value < 0.05. H₀ gagal ditolak jika p-value ≥ 0.05, artinya tidak ada bukti statistik yang cukup untuk menyatakan SVM lebih baik dari Naive Bayes pada dataset ini. Kondisi kegagalan ini didefinisikan secara eksplisit sebelum eksperimen dimulai — bukan setelah melihat data.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah SVM menghasilkan F1-Score lebih tinggi dari Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan TF-IDF? |
| Variable (IV) | Jenis algoritma klasifikasi: Multinomial Naive Bayes vs SVM (SVC kernel linear) — dimanipulasi dengan mengganti konfigurasi model per eksperimen |
| Variable (DV) | Performa klasifikasi: F1-Score macro-average sebagai primary metric; Akurasi, Precision, Recall sebagai secondary metric |
| Metric | F1-Score macro-average (0–1) dihitung via sklearn.metrics; Akurasi, Precision, Recall via sklearn.metrics.classification_report |
| Data source | Ulasan Google Play Store: BCA Mobile (com.bca), Mandiri Online (com.bankmandiri.mandirionline), BRImo (com.bri.britama) — discraping via google-play-scraper Python, filter bahasa Indonesia, periode 2022–2024, ±2.000 ulasan per aplikasi |
| Analysis method | Wilcoxon signed-rank test pada hasil 10 run eksperimen dengan random_state berbeda (0–9); effect size Cohen's d untuk mengukur besaran perbedaan praktis |

**Apakah rantai lengkap?** [✅] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? Semua tahap dari RQ hingga metode analisis terdokumentasi tanpa lompatan logis. Setiap tahap terhubung ke tahap berikutnya secara eksplisit: RQ menentukan variabel, variabel menentukan metrik, metrik menentukan sumber data, sumber data menentukan metode analisis yang tepat.

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Sentiment Analysis of Mobile Banking Reviews Using Machine Learning Models (Santoso et al., 2025)
**RQ yang diekstrak:** "Algoritma machine learning mana yang menghasilkan akurasi terbaik untuk klasifikasi sentimen ulasan aplikasi mobile banking Indonesia?"
**Komponen yang hilang:** Tiga komponen tidak terpenuhi secara eksplisit di RQ paper tersebut. Pertama, metrik tidak spesifik — "akurasi terbaik" tidak menyebut apakah menggunakan akurasi biasa atau F1-Score, padahal keduanya bisa menghasilkan kesimpulan berbeda pada data tidak seimbang. Kedua, baseline tidak didefinisikan — tidak jelas algoritma mana yang dijadikan pembanding acuan. Ketiga, dataset tidak disebutkan di RQ — nama aplikasi dan sumber data baru muncul di bagian metodologi, bukan di rumusan pertanyaan riset. Akibatnya RQ terkesan umum dan tidak mengandung cetak biru eksperimen yang lengkap.
