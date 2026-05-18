# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality
  
Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

Hypothesis        : H₀: Tidak terdapat perbedaan signifikan F1-Score   antara SVM dan Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF (α = 0,05)
H₁: SVM menghasilkan F1-Score yang secara signifikan lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan mobile banking Indonesia menggunakan TF-IDF (α = 0,05)

Tipe Eksperimen   : [✅] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi   | Deskripsi                        | IV Value       | CV Settings                                              |
|-----------|----------------------------------|----------------|----------------------------------------------------------|
| Control   | Multinomial Naive Bayes + TF-IDF | MultinomialNB  | Dataset 6.000 ulasan CSV, TF-IDF max_features=5.000,     |
|           | sebagai baseline                 | alpha=1.0      | split 80:20 stratified, random_state=0–9, preprocessing  |
|           |                                  |                | identik (lowercase, stopword, stemming PySastrawi)       |
| Treatment | SVM kernel linear + TF-IDF       | SVC            | Dataset 6.000 ulasan CSV, TF-IDF max_features=5.000,     |
|           | sebagai intervensi               | kernel=linear  | split 80:20 stratified, random_state=0–9, preprocessing  |
|           |                                  | C=1.0          | identik (lowercase, stopword, stemming PySastrawi)       |


Fairness Checklist:
  [✅] Dataset identik — file CSV yang sama untuk kedua kondisi
  [✅] Preprocessing setara — fungsi preprocessing identik dijalankan sebelum vectorizer untuk NB dan SVM
  [✅] Tuning effort setara — keduanya menggunakan parameter default yang lazim: NB alpha=1.0 (Laplace smoothing), SVM C=1.0 kernel=linear; tidak ada Bayesian optimization atau grid search yang hanya diterapkan ke salah satu
  [✅] Environment identik — keduanya dijalankan di Google Colab Python 3.12 dengan library scikit-learn 1.4 yang sama
  [✅] Metrik evaluasi sama — F1-Score macro-average, Akurasi, Precision, Recall dihitung identik via sklearn.metrics untuk kedua kondisi

Threat Analysis:
| Threat Type | Ancaman Spesifik                        | Mitigasi                                              |
|-------------|----------------------------------------|-------------------------------------------------------|
| Internal    | Data leakage: TF-IDF di-fit pada       | sklearn Pipeline memastikan TF-IDF hanya di-fit pada  |
|             | seluruh dataset sebelum split          | training set; transform terpisah pada test set        |
| Internal    | Variable contamination: komponen       | Config-driven execution — hanya parameter model_type  |
|             | selain Classifier ikut berubah         | yang diubah; semua CV dikunci di config.yaml          |
| External    | Dataset hanya dari Google Play Store;  | Tiga bank terbesar dipilih untuk representasi lebih   |
|             | silent majority tidak terwakili        | luas; limitasi dinyatakan eksplisit di proposal       |
| Construct   | Proxy labeling: rating bintang tidak   | Spot-check manual pada subsampel; inkonsistensi label |
|             | selalu merepresentasikan sentimen teks | diakui sebagai limitasi penelitian                    |
| Conclusion  | Sample size 10 run mungkin tidak       | Wilcoxon signed-rank test non-parametrik dipilih      |
|             | terdistribusi normal                   | karena tidak mengasumsikan normalitas distribusi      |

Statistical Plan:
  Uji statistik    : Wilcoxon signed-rank test (non-parametrik, paired)
  Justifikasi      : Distribusi F1-Score dari 10 run tidak dapat diasumsikan normal karena sample size kecil (n=10); Wilcoxon tepat untuk membandingkan dua kondisi berpasangan tanpa asumsi distribusi
  Alpha            : α = 0,05
  Effect size min  : Cohen's d > 0,8 (large effect) sebagai ambang batas perbedaan yang bermakna secara praktis, bukan hanya signifikan secara statistik
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?
**Tipe eksperimen:** [✅] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
| :--- | :--- | :--- | :--- |
| **Control** | Multinomial Naive Bayes dengan TF-IDF sebagai baseline — algoritma paling umum digunakan pada studi analisis sentimen ulasan mobile banking Indonesia (Java et al., 2024; Samudera et al., 2024; Al Hakim & Irwiensyah, 2024) | MultinomialNB, alpha=1.0 | Dataset: 6.000 ulasan CSV (BCA Mobile + Mandiri Online + BRImo); TF-IDF max_features=5.000; split 80:20 stratified; random_state=0–9 (10 run); preprocessing: lowercase + hapus simbol + stopword removal + stemming PySastrawi |
| **Treatment** | SVM kernel linear dengan TF-IDF sebagai intervensi — dipilih karena konsisten mengungguli NB pada studi sentimen teks Indonesia (Ningsih et al., 2024; Khaira et al., 2023) namun belum diverifikasi statistik pada domain mobile banking multi-bank | SVC, kernel=linear, C=1.0 | Identik dengan Control — dataset, TF-IDF, split, random_state, dan preprocessing sama persis; hanya parameter model_type yang berbeda di config.yaml |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
| :--- | :---: | :--- |
| **Dataset identik** | ✅ | Kedua kondisi menggunakan file CSV yang sama berisi 6.000 ulasan dari BCA Mobile, Mandiri Online, dan BRImo — tidak ada perbedaan sumber, jumlah, atau periode data |
| **Preprocessing setara** | ✅ | Fungsi preprocessing yang identik dijalankan untuk kedua kondisi sebelum masuk ke Vectorizer: lowercase → hapus simbol dan angka → stopword removal (PySastrawi) → stemming (PySastrawi). Tidak ada langkah preprocessing tambahan yang hanya diterapkan ke salah satu kondisi |
| **Tuning effort setara** | ✅ | Keduanya menggunakan parameter default yang lazim tanpa tuning tambahan: NB alpha=1.0 (Laplace smoothing default) dan SVM C=1.0 kernel=linear (parameter default scikit-learn). Tidak ada grid search, Bayesian optimization, atau cross-validation tuning yang hanya dilakukan untuk satu algoritma |
| **Environment identik** | ✅ | Kedua kondisi dijalankan dalam satu notebook Google Colab dengan Python 3.12, scikit-learn 1.4, dan library yang sama. Eksekusi dilakukan secara berurutan dalam sesi yang sama sehingga tidak ada perbedaan environment runtime |
| **Metrik evaluasi sama** | ✅ | F1-Score macro-average (primary), Akurasi, Precision macro, dan Recall macro dihitung menggunakan fungsi sklearn.metrics yang identik untuk kedua kondisi; output disimpan ke format results.csv yang sama |

**Ada yang tidak fair?** [ ] Ya / [✅] Tidak
>Seluruh kriteria fairness terpenuhi. Satu-satunya yang berbeda antara kondisi Control dan Treatment adalah komponen Classifier — NB vs SVM — yang diubah via config.yaml. Semua komponen lain identik, sehingga perbedaan F1-Score yang terukur dapat dikaitkan secara langsung ke perbedaan algoritma.
---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
| :--- | :--- | :--- |
| **Internal** | Data leakage: TF-IDF yang di-fit pada seluruh dataset sebelum split akan memasukkan informasi test set ke model sehingga evaluasi menjadi terlalu optimis | sklearn Pipeline digunakan — TF-IDF di-fit hanya pada training set dan transform diterapkan terpisah pada test set; ini mencegah kebocoran informasi apapun dari test ke training |
| **Internal** | Variable contamination: perubahan yang tidak disengaja pada komponen selain Classifier (Preprocessor, Vectorizer) bisa mencemari hasil | Config-driven execution — semua parameter CV dikunci di config.yaml; hanya model_type yang diubah antar kondisi; kode tidak dimodifikasi secara manual antar run |
| **External** | Sample bias: ulasan Google Play hanya mewakili pengguna yang aktif memberikan ulasan, bukan seluruh pengguna mobile banking Indonesia | Tiga bank konvensional terbesar dipilih (BCA, Mandiri, BRI) untuk memperluas representasi; limitasi ini diakui eksplisit di proposal dan harus dinyatakan di bagian Discussion |
| **External** | Domain spesifik: hasil hanya berlaku untuk ulasan Google Play berbahasa Indonesia dari bank konvensional; tidak otomatis berlaku untuk bank syariah, bank digital, atau platform lain | Scope penelitian dinyatakan eksplisit sejak awal; generalisasi ke luar scope memerlukan replikasi tambahan |
| **Construct** | Proxy labeling: rating bintang tidak selalu merepresentasikan sentimen teks — ulasan bintang 1 bisa berisi keluhan teknis sementara yang bersifat netral, atau sebaliknya | Spot-check manual pada subsampel ulasan untuk memverifikasi konsistensi label; inkonsistensi diakui sebagai limitasi dan dilaporkan di Discussion |
| **Conclusion** | Sample size kecil (n=10 run): distribusi F1 dari 10 run tidak dapat diasumsikan normal sehingga uji parametrik (t-test) tidak valid | Wilcoxon signed-rank test dipilih karena non-parametrik dan tidak mengasumsikan normalitas distribusi; Cohen's d dihitung sebagai ukuran besaran perbedaan praktis |

**Ancaman mana yang paling sulit dimitigasi?** External validity — sample bias

**Mengapa?**
> Ancaman external validity berupa sample bias paling sulit dimitigasi karena bersifat struktural — Google Play Store secara inheren hanya menampung ulasan dari pengguna yang bersedia meluangkan waktu untuk memberikan ulasan, yang cenderung adalah pengguna dengan pengalaman sangat positif atau sangat negatif. Pengguna dengan pengalaman biasa (silent majority) tidak terwakili, sehingga distribusi sentimen dalam dataset mungkin tidak merepresentasikan distribusi sentimen pengguna mobile banking Indonesia secara keseluruhan. Mitigasi yang bisa dilakukan hanya bersifat parsial: memilih tiga bank terbesar untuk memperluas cakupan, dan menyatakan limitasi ini secara eksplisit. Namun tidak ada cara untuk sepenuhnya menghilangkan bias ini tanpa menggunakan data dari survei langsung atau log internal bank yang tidak tersedia untuk publik.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah perbandingannya fair? — Apakah semua baseline diuji pada dataset yang sama, preprocessing yang sama, tuning effort yang sebanding, dan metrik yang identik? Atau apakah metode baru mendapat keuntungan dari fitur tambahan, hyperparameter tuning yang lebih intensif, atau dataset yang dipilih secara selektif sementara baseline menggunakan parameter default? Perbandingan yang tidak fair adalah bentuk straw man comparison yang menghasilkan klaim menyesatkan.
2. Apakah perbedaannya signifikan secara statistik dan bermakna secara praktis? — Apakah ada uji statistik (t-test, Wilcoxon, dll.) yang membuktikan perbedaan bukan sekadar noise dari variasi random seed? Berapa effect size-nya — apakah peningkatan 0,5% F1-Score yang "signifikan" secara statistik juga bermakna dalam konteks aplikasi nyata? Tanpa uji statistik dan effect size, klaim keunggulan tidak dapat dipertanggungjawabkan secara ilmiah.
3. Seberapa representatif dataset yang digunakan? — Apakah baseline yang dipilih benar-benar merepresentasikan state of the art, atau sengaja dipilih yang lemah agar metode baru terlihat lebih unggul? Apakah eksperimen dijalankan pada lebih dari satu dataset untuk membuktikan generalisabilitas, atau hanya pada satu dataset yang mungkin kebetulan menguntungkan metode baru? Dataset tunggal yang tidak representatif membuat klaim "mengalahkan semua baseline" tidak dapat digeneralisasi ke kondisi nyata.