# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Apakah algoritma Support Vector Machine (SVM) menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

Variable → Component Mapping:
| Variabel              | Tipe | Komponen Sistem       | Cara Manipulasi/Pengukuran                          |
|-----------------------|------|-----------------------|-----------------------------------------------------|
| Jenis algoritma       | IV   | Modul Classifier      | Ganti config: model_type: "nb" atau "svm"           |
| F1-Score macro-avg    | DV   | Modul Evaluator       | sklearn.metrics.f1_score(average='macro') tiap run  |
| Akurasi, Prec, Recall | DV   | Modul Evaluator       | sklearn.metrics.classification_report tiap run      |
| TF-IDF max_feat=5.000 | CV   | Modul Vectorizer      | Dikunci di config.yaml, tidak diubah antar run      |
| Split 80:20, strat    | CV   | Modul Data Splitter   | Dikunci di config.yaml, random_state per run        |
| Preprocessing teks    | CV   | Modul Preprocessor    | Fungsi identik dijalankan sebelum vectorizer        |
| Dataset ulasan 3 app  | CV   | Modul Data Loader     | File CSV yang sama untuk semua eksperimen           |

4 Prinsip Desain:
  [✅] Traceability — Setiap komponen bisa ditelusuri ke variabel: Data Loader + Preprocessor + Vectorizer + Splitter = CV Classifier = IV Evaluator = DV
  [✅] Variable Isolation — IV (Classifier) bisa diubah NB↔SVM dengan mengubah satu baris config.yaml tanpa menyentuh komponen lain
  [✅] Measurement Integration — Evaluator otomatis menghasilkan F1, Akurasi, Precision, Recall dan menyimpan ke results.csv setiap run tanpa pengukuran manual
  [✅] Reproducibility — Semua parameter dikunci di config.yaml; notebook dan dataset didokumentasikan di Google Colab sehingga siapapun bisa mereproduksi eksperimen

Experimental Setup:
  Input data     : 6.000 ulasan Google Play Store (BCA Mobile + Mandiri Online + BRImo), format CSV: [nama_user, ulasan, rating, tanggal, aplikasi, sentimen] Label: positif (4–5★), netral (3★), negatif (1–2★)
  Parameter      : TF-IDF max_features=5.000, split=80:20 stratified random_state=0–9 (10 run), NB alpha=1.0, SVM kernel=linear C=1.0
  Output format  : results.csv berisi [run_id, model, f1_macro, accuracy, precision_macro, recall_macro] + grafik bar chart perbandingan PNG

```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah algoritma SVM menghasilkan F1-Score lebih tinggi dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
| :--- | :---: | :--- | :--- |
| **Jenis algoritma klasifikasi (NB vs SVM)** | IV | Modul Classifier — swap MultinomialNB ↔ SVC | Ganti config: `model_type: "nb"` atau `"svm"` — satu baris, tidak menyentuh komponen lain |
| **F1-Score macro-average** | DV (primary) | Modul Evaluator | `sklearn.metrics.f1_score(average='macro')` — dihitung otomatis setiap run, disimpan ke results.csv |
| **Akurasi, Precision, Recall** | DV (secondary) | Modul Evaluator | `sklearn.metrics.classification_report` — dihitung otomatis bersamaan setiap run |
| **TF-IDF max_features=5.000** | CV | Modul Vectorizer | Dikunci di config.yaml — tidak diubah antar eksperimen |
| **Split 80:20, stratified, random_state per run** | CV | Modul Data Splitter | Dikunci di config.yaml — memastikan kedua algoritma diuji pada partisi data identik |
| **Preprocessing (lowercase, stopword, stemming)** | CV | Modul Preprocessor | Fungsi preprocessing identik dijalankan sebelum Vectorizer untuk kedua kondisi |
| **Dataset 6.000 ulasan 3 aplikasi** | CV | Modul Data Loader | File CSV yang sama dimuat untuk setiap run tanpa perubahan apapun |

**Apakah semua variabel bisa di-map?** [✅] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? Semua variabel berhasil dipetakan ke komponen sistem yang spesifik. IV dipetakan ke Classifier, DV ke Evaluator, dan seluruh CV dipetakan ke Vectorizer, Splitter, Preprocessor, dan Data Loader yang semuanya dikunci konstan. Tidak ada variabel yang mengambang tanpa representasi komponen.

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
| :--- | :---: | :--- |
| **Traceability** | ✅ | Setiap komponen memiliki label variabel eksplisit: Data Loader + Preprocessor + Vectorizer + Splitter = CV; Classifier = IV; Evaluator = DV. Hubungan ini terdokumentasi di komentar kode dan config.yaml sehingga peneliti lain bisa menelusuri fungsi setiap komponen tanpa membaca seluruh kode |
| **Modularity** | ✅ | Classifier diimplementasikan sebagai objek terpisah yang dipanggil via config. Mengganti NB ke SVM hanya memerlukan perubahan satu baris di config.yaml (model_type: "nb" → "svm") tanpa menyentuh modul Preprocessor, Vectorizer, Splitter, atau Evaluator sama sekali — variable isolation terjaga sempurna |
| **Controllability** | ✅ | Semua parameter CV dieksternalisasi ke config.yaml: max_features=5.000, test_size=0.2, random_state per run, alpha NB=1.0, C SVM=1.0. Tidak ada parameter yang hardcoded di dalam fungsi — siapapun bisa memverifikasi dan mereproduksi kondisi eksperimen hanya dari file config |
| **Measurability** | ✅ | Modul Evaluator memanggil classification_report dan menyimpan semua metrik (F1, Akurasi, Precision, Recall) ke results.csv secara otomatis setiap run — tidak ada pengukuran manual dan tidak ada risiko human error dalam pencatatan hasil |

**Prinsip mana yang paling sulit dipenuhi?** Modularity
**Strategi untuk mengatasinya:**
> Modularity paling menantang karena Vectorizer (TF-IDF) dan Classifier harus dikoppel dengan benar untuk mencegah data leakage. TF-IDF harus di-fit hanya pada data training, bukan seluruh dataset — jika di-fit pada seluruh data sebelum split, informasi dari test set akan bocor ke model sehingga hasil evaluasi menjadi terlalu optimis dan tidak valid. Solusinya adalah menggunakan sklearn Pipeline yang menggabungkan Vectorizer dan Classifier dalam satu objek: Pipeline([('tfidf', TfidfVectorizer()), ('clf', MultinomialNB())]). Dengan Pipeline, fit hanya terjadi pada training set dan transform otomatis diterapkan ke test set secara terpisah. Ini memastikan modularity tetap terjaga — swap NB↔SVM tetap bisa dilakukan hanya dengan mengubah parameter clf di Pipeline tanpa risiko leakage.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

| Kondisi | Preprocessing | TF-IDF Vectorizer | Classifier | Hasil yang Diharapkan |
| :--- | :--- | :--- | :--- | :--- |
| **Full NB (Baseline)** | ✅ Aktif lengkap | ✅ max_features=5.000 | ✅ MultinomialNB | Performa baseline NB — acuan perbandingan utama |
| **Full SVM (Treatment)** | ✅ Aktif lengkap | ✅ max_features=5.000 | ✅ SVC linear | Performa treatment SVM — dibandingkan dengan Full NB |
| **– Preprocessing** | ❌ Dinonaktifkan (teks mentah) | ✅ max_features=5.000 | ✅ NB & SVM | Penurunan F1 signifikan — membuktikan kontribusi preprocessing terhadap kualitas representasi fitur |
| **– TF-IDF (ganti CountVectorizer)** | ✅ Aktif | ❌ CountVectorizer tanpa bobot IDF | ✅ NB & SVM | Penurunan F1 moderat — membuktikan kontribusi pembobotan TF-IDF dibanding frekuensi mentah (BoW) |

**Komponen mana yang diprediksi paling berkontribusi?** Preprocessing
**Mengapa?**
> Ulasan Google Play berbahasa Indonesia mengandung banyak noise yang sangat beragam: singkatan tidak baku seperti "gk", "bgt", "sy", emoji, angka, tanda baca berulang, dan campur kode Indonesia-Inggris. Tanpa preprocessing, Vectorizer akan membuat vocabulary yang sangat besar dan berisik — kata "tidak", "tdk", "ga", "gak", "ngga" akan dianggap sebagai fitur yang berbeda padahal bermakna sama. Akibatnya representasi fitur TF-IDF menjadi sangat sparse dan tidak informatif, sehingga algoritma apapun — baik Naive Bayes maupun SVM — tidak bisa belajar pola sentimen yang bermakna dari data. Preprocessing adalah fondasi yang menentukan kualitas semua komponen berikutnya dalam pipeline, dan kualitas fitur input jauh lebih menentukan performa model daripada pilihan algoritma itu sendiri.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun monolitik seperti produk — semua komponen saling terhubung erat, parameter hardcoded, tidak ada pemisahan modul yang jelas — maka ketika peneliti ingin mengganti satu variabel seperti algoritma dari Naive Bayes ke SVM, ia harus menyentuh banyak bagian kode sekaligus. Ini menciptakan risiko besar: perubahan yang tidak disengaja pada komponen lain bisa mempengaruhi hasil eksperimen, dan peneliti tidak bisa memastikan bahwa perbedaan hasil murni disebabkan oleh perubahan variabel yang dimaksud. Selain itu, sistem monolitik sangat sulit direplikasi oleh peneliti lain karena tidak ada cara untuk memverifikasi bahwa kondisi eksperimen benar-benar identik. Lebih jauh, jika ada bug di tengah eksperimen, seluruh hasil sebelumnya menjadi tidak dapat dipercaya karena tidak jelas komponen mana yang bermasalah.

> Arsitektur modular penting untuk riset karena memungkinkan variable isolation yang ketat — hanya satu komponen yaitu IV yang berubah, sementara semua komponen CV tetap identik. Ini adalah syarat fundamental eksperimen yang valid secara internal. Dalam penelitian ini, hanya Modul Classifier yang di-swap antara MultinomialNB dan SVC, sementara Data Loader, Preprocessor, Vectorizer, dan Evaluator tidak berubah sama sekali — memastikan bahwa perbedaan F1-Score yang terukur benar-benar berasal dari perbedaan algoritma, bukan dari perbedaan data atau cara pengukuran. Dengan config-driven execution, setiap run eksperimen terdokumentasi sepenuhnya dalam satu file konfigurasi yang bisa dibagikan, direplikasi, dan diverifikasi oleh siapapun.