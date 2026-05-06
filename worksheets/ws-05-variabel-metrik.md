# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?


| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
| Jenis algoritma klasifikasi | IV | Pendekatan matematis untuk mengklasifikasikan teks ulasan ke kelas sentimen | Kategorikal: MultinomialNB vs SVC (kernel linear) | Nominal | — | Diatur di config file, diubah per eksperimen tanpa menyentuh komponen lain | IV harus bisa di-swap tanpa mengubah komponen lain agar isolasi variabel terjaga |
| F1-Score | DV (primary) | Keseimbangan antara precision dan recall — ukuran performa klasifikasi yang robust terhadap data tidak seimbang | F1 macro-average = rata-rata F1 per kelas tanpa mempertimbangkan proporsi kelas | Ratio | 0–1 | sklearn.metrics.f1_score(average='macro') otomatis setiap run | F1-Score lebih tepat dari akurasi untuk data multi-kelas tidak seimbang; standar evaluasi NLP |
| Akurasi | DV (secondary) | Proporsi prediksi benar dari seluruh data uji | (TP+TN)/(TP+TN+FP+FN) | Ratio | 0–1 (%) | sklearn.metrics.accuracy_score | Dilaporkan sebagai secondary untuk transparansi dan perbandingan dengan studi lain |
| Precision | DV (secondary) | Proporsi prediksi positif yang benar per kelas | TP/(TP+FP), macro-average | Ratio | 0–1 | sklearn.metrics.precision_score(average='macro') | Melengkapi F1-Score untuk memahami trade-off false positive |
| Recall | DV (secondary) | Proporsi data positif yang berhasil terdeteksi per kelas | TP/(TP+FN), macro-average | Ratio | 0–1 | sklearn.metrics.recall_score(average='macro') | Melengkapi F1-Score untuk memahami trade-off false negative |
| Representasi fitur TF-IDF | CV | Metode konversi teks ke vektor numerik berbobot frekuensi-invers dokumen | TF-IDF dengan max_features=5.000, dikunci konstan | Ratio | — | TfidfVectorizer(max_features=5000) sklearn | Dikunci agar perbedaan hasil murni karena algoritma, bukan representasi fitur |
| Proporsi split data | CV | Pembagian data training dan testing | 80% training, 20% testing, random_state=42 | Ratio | — | train_test_split(test_size=0.2, random_state=42) | Dikunci agar eksperimen reproducible dan perbandingan fair |
| Bahasa ulasan | CV | Bahasa teks input yang dianalisis | Bahasa Indonesia saja | Nominal | — | Filter saat preprocessing berdasarkan deteksi bahasa | Menghindari noise dari ulasan bahasa Inggris atau campuran |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [✅] Setiap langkah terdokumentasi
  [✅] Tidak ada "lompatan logis"
  [✅] Metrik mengukur apa yang dimaksud (construct validity) - (F1-Score = construct validity performa klasifikasi multi-kelas tidak seimbang)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jenis algoritma klasifikasi | IV | Pendekatan matematis yang digunakan untuk mengklasifikasikan sentimen teks ulasan | Kategorikal: MultinomialNB vs SVC kernel linear | Nominal | — |
| F1-Score | DV (primary) | Performa keseluruhan klasifikasi yang seimbang antara precision dan recall untuk semua kelas | F1 macro-average dihitung via `sklearn.metrics` | Ratio | 0–1 |
| Akurasi | DV (secondary) | Proporsi prediksi benar dari total data uji | Accuracy score via `sklearn.metrics` | Ratio | 0–1 |
| Precision | DV (secondary) | Proporsi prediksi positif yang benar per kelas sentimen | Precision macro via `sklearn.metrics` | Ratio | 0–1 |
| Recall | DV (secondary) | Proporsi data positif yang berhasil terdeteksi per kelas | Recall macro via `sklearn.metrics` | Ratio | 0–1 |
| TF-IDF max_features=5.000 | CV | Representasi numerik teks yang dikunci konstan | TfidfVectorizer parameter dikunci di config | Ratio | — |
| Split 80:20, random_state=42 | CV | Proporsi pembagian data train-test yang dikunci | Parameter dikunci di `config.yaml` | Ratio | — |
| Bahasa ulasan | CV | Bahasa teks yang dianalisis | Bahasa Indonesia saja, difilter saat preprocessing | Nominal | — |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✅] Tidak
> Jika ya, di mana? Setiap variabel terhubung langsung ke RQ — IV adalah algoritma yang diuji, DV adalah metrik yang menjawab RQ, CV adalah semua faktor yang dikunci agar perbandingan fair. Tidak ada konsep yang mengambang tanpa operasionalisasi yang jelas.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 | F1-Score macro-average mewakili performa klasifikasi multi-kelas secara seimbang — tidak bias ke kelas mayoritas seperti akurasi biasa. Sangat tepat untuk data ulasan yang distribusi kelasnya tidak merata karena ulasan positif cenderung lebih banyak dari negatif pada aplikasi banking |
| Sensitive | 4 | F1-Score cukup sensitif menangkap perbedaan performa antar algoritma di level per kelas — mampu mendeteksi kelemahan di kelas tertentu yang akurasi tidak bisa tangkap. Skor 4 bukan 5 karena pada dataset sangat besar perbedaan kecil mungkin tidak bermakna praktis meski signifikan statistik |
| Feasible | 5 | F1-Score dihitung otomatis oleh sklearn.metrics dalam satu baris kode, tidak memerlukan anotasi tambahan atau alat khusus — sangat feasible dalam eksperimen berbasis Python di Google Colab |

**Apakah perlu secondary metric?** [✅] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Akurasi, Precision, dan Recall dilaporkan sebagai secondary metric dengan dua alasan. Pertama, untuk transparansi penuh agar hasil bisa dibandingkan dengan studi lain yang mungkin hanya melaporkan akurasi. Kedua, Precision dan Recall melengkapi F1-Score untuk memahami trade-off antara false positive dan false negative per kelas sentimen — informasi yang berguna bagi pengembang aplikasi dalam memahami jenis kesalahan yang lebih sering dibuat masing-masing algoritma.

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika dataset didominasi kelas "positif" misalnya 80% ulasan bintang 4–5, algoritma yang selalu memprediksi "positif" bisa mencapai akurasi 80% tanpa belajar apapun — inilah ceiling effect pada akurasi. F1-Score macro-average terhindar dari masalah ini karena menghitung F1 per kelas secara terpisah lalu dirata-rata, sehingga kelas minoritas (negatif atau netral) tetap terhitung dengan bobot yang sama dan tidak tersembunyi oleh dominasi kelas mayoritas.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? | Tidak semua ulasan bisa di-scraping — Google Play membatasi jumlah ulasan yang bisa diambil via API, dan beberapa ulasan mungkin terhapus oleh pengguna atau Google | Gunakan google-play-scraper dengan parameter count=2.000 per aplikasi; dokumentasikan jumlah aktual yang berhasil dikumpulkan; jika kurang dari 1.500 per aplikasi, tambah periode scraping |
| Consistency | Apakah ada kontradiksi internal? | Beberapa ulasan memiliki rating tinggi tapi teks negatif atau sebaliknya — inkonsistensi antara label otomatis dari rating dan sentimen teks sebenarnya | Lakukan spot-check manual pada 100 sampel acak untuk memverifikasi konsistensi label; ulasan dengan rating 3 bintang dikategorikan "netral" secara konsisten di seluruh dataset |
| Validity | Apakah benar-benar mengukur yang dimaksud? | Rating bintang sebagai proxy label sentimen cukup valid tapi tidak sempurna — ulasan 1 bintang bisa berisi keluhan teknis sementara (misalnya server down) yang bersifat temporer, bukan sentimen negatif permanen terhadap aplikasi | Akui limitasi ini secara eksplisit di bagian Discussion; lakukan validasi subsampel 200 ulasan secara manual untuk mengukur tingkat inkonsistensi label |
| Representativeness | Apakah sampel mewakili populasi target? | Ulasan Google Play hanya mewakili pengguna yang aktif memberikan ulasan — tidak mewakili seluruh pengguna mobile banking Indonesia yang mayoritas silent user | Nyatakan batasan ini sebagai limitasi penelitian; pilih 3 bank terbesar (BCA, Mandiri, BRI) untuk merepresentasikan segmen pengguna mobile banking konvensional Indonesia yang paling luas |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data adalah p-hacking karena peneliti secara tidak sadar atau sengaja memilih metrik yang menghasilkan hasil paling menguntungkan dari data yang sudah ada — ini sama dengan menyesuaikan pertanyaan agar cocok dengan jawaban yang diinginkan, bukan sebaliknya. Misalnya, jika setelah melihat data ternyata SVM unggul di akurasi tapi tidak di F1-Score, lalu peneliti memutuskan untuk menjadikan akurasi sebagai primary metric, maka kesimpulan "SVM lebih baik" menjadi bias — hasilnya tampak valid secara statistik tetapi sebenarnya dipilih karena menguntungkan, bukan karena paling tepat secara metodologis.

> Eksplorasi data yang sah berbeda karena tujuannya adalah memahami karakteristik data sebelum eksperimen dimulai, bukan memilih metrik berdasarkan hasil. Eksplorasi yang sah dilaporkan secara transparan sebagai analisis eksploratori dan tidak digunakan untuk menerima atau menolak hipotesis utama. Dalam penelitian ini, F1-Score macro-average ditetapkan sebagai primary metric sebelum data dikumpulkan — keputusan ini didasarkan pada karakteristik yang sudah diketahui dari literatur bahwa data ulasan cenderung tidak seimbang, bukan karena melihat hasilnya terlebih dahulu. Jika kemudian ditemukan pola menarik lain saat eksplorasi data, itu dilaporkan sebagai temuan eksploratori terpisah yang tidak mempengaruhi kesimpulan hipotesis utama.
