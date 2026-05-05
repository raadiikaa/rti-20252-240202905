# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Radika Rismawati Tri Prasaja
Tanggal          : Minggu, 12 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: 95% akurat diukur pada dataset seperti apa? Apakah dataset tersebut seimbang antar kelas sentimennya?
   - Data yang dibutuhkan untuk verifikasi: Ukuran dan komposisi dataset uji, distribusi kelas (positif/negatif/netral), metode validasi yang digunakan, dan apakah metrik lain seperti F1-Score juga dilaporkan.


2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [✅] Design Science  [ ] Mixed
   - Alasan: Penelitian ini membangun pipeline klasifikasi sentimen sebagai artefak yang digunakan untuk menguji hipotesis — apakah SVM lebih unggul dari Naive Bayes pada teks ulasan mobile banking berbahasa Indonesia.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Rating bintang pengguna secara akurat merepresentasikan sentimen teks ulasan yang ditulis
   - Sumber bias potensial: Ulasan dengan rating tinggi belum tentu berteks positif; peneliti mungkin memilih metrik yang menguntungkan algoritmanya
   - Langkah mitigasi: Lakukan validasi subsampel manual, laporkan semua metrik (F1, Precision, Recall), dan gunakan dataset yang sama untuk kedua algoritma

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Hasil klasifikasi mentah dari kedua algoritma — tidak akan dipilih selektif hanya yang menguntungkan SVM
   - Batasan yang diakui sejak awal: Hasil hanya berlaku untuk ulasan mobile banking Indonesia di Google Play; generalisasi ke platform atau domain lain membutuhkan replikasi tambahan
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Sentiment Analysis of Mobile Banking Reviews Using Machine Learning Models
> Penulis (Tahun): Santoso et al. (2025)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengumpulkan 6.000 ulasan aplikasi BRI dan BSI dari Google Play Store periode Januari–Juli 2024 | Hanya mencakup 2 aplikasi dari periode 6 bulan — tidak merepresentasikan keseluruhan pengguna mobile banking Indonesia yang lebih beragam |
| Data → Processing | Preprocessing teks: case folding, tokenisasi, stopword removal, stemming, lalu labeling sentimen berdasarkan rating bintang |Rating bintang digunakan sebagai proxy label sentimen tanpa validasi manual — ulasan bintang 1 bisa berisi pujian dan sebaliknya |
| Processing → Analysis | Membandingkan KNN, SVM, Random Forest, dan Naive Bayes menggunakan metrik akurasi, precision, recall, F1-score | Tidak dilaporkan apakah data seimbang antar kelas — jika kelas positif dominan, akurasi tinggi bisa menyesatkan |
| Analysis → Inference | Menyimpulkan Random Forest dan Naive Bayes memiliki kinerja terbaik dengan akurasi tertinggi 81% (BRI) dan 78% (BSI) | Kesimpulan "terbaik" hanya berdasarkan akurasi — F1-Score per kelas tidak dijadikan primary metric padahal data kemungkinan tidak seimbang |
| Inference → Knowledge | Mengklaim Naive Bayes dan Random Forest cocok untuk analisis sentimen ulasan mobile banking Indonesia | Klaim terlalu luas: hasil hanya dari 2 bank dalam 6 bulan, belum diuji pada bank lain atau periode berbeda |

**Distorsi paling besar di tahap:** Processing → Analysis

**Dua distorsi spesifik yang teridentifikasi:**
1. Proxy labeling tanpa validasi — Label sentimen ditentukan langsung dari rating bintang tanpa pengecekan manual. Ini asumsi yang rawan salah karena pengguna sering memberi rating rendah karena masalah teknis sementara teksnya netral, atau sebaliknya.
2. Pelaporan metrik tidak lengkap — Kesimpulan "kinerja terbaik" didasarkan pada akurasi saja tanpa menjadikan F1-Score sebagai primary metric, padahal distribusi kelas ulasan hampir pasti tidak seimbang (ulasan positif cenderung lebih sedikit dari negatif pada aplikasi banking).

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti wajib melaporkan kedua versi hasil — dengan outlier dan tanpa outlier. Menghapus outlier hanya karena hasilnya jadi bagus tanpa alasan metodologis yang jelas = manipulasi data |
| Transparansi | Jika outlier memang dihapus, harus dijelaskan alasan teknisnya secara terbuka di paper (misalnya: error alat ukur, kondisi tidak normal yang terdokumentasi). Menyembunyikan proses ini melanggar prinsip open science |
| Peer review | Reviewer berhak meminta justifikasi penghapusan outlier. Jika tidak dijelaskan dengan baik, paper bisa ditolak atau diretract setelah publikasi karena dianggap tidak jujur |

**Keputusan akhir dan justifikasi:**
> Outlier tidak boleh dihapus hanya demi mendapatkan hasil yang signifikan. Keputusan yang etis adalah melaporkan hasil apa adanya: "Dengan data lengkap, hasil tidak signifikan (p > 0.05). Analisis sensitivitas menunjukkan penghapusan 3 outlier mengubah hasil menjadi signifikan, namun keputusan ini harus disertai justifikasi metodologis yang kuat." Ini adalah bentuk penelitian yang jujur dan dapat dipertanggungjawabkan. Menghapus outlier tanpa alasan jelas termasuk pelanggaran etika riset yang disebut data manipulation.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Perbandingan algoritma Naive Bayes dan SVM untuk klasifikasi sentimen ulasan aplikasi mobile banking Indonesia di Google Play Store

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 4 | 2 | 5 |
| Jenis data yang dikumpulkan | Data terukur: akurasi, F1-Score, Precision, Recall dari dua algoritma pada dataset yang sama | Wawancara mendalam tentang pengalaman pengguna memberi ulasan di Google Play | Membangun pipeline klasifikasi sentimen sebagai artefak, lalu menguji performa NB vs SVM |
| Limitasi paradigma | Tidak menangkap nuansa bahasa informal Indonesia yang membuat teks sulit diklasifikasikan secara objektif | Sulit direplikasi dan tidak menghasilkan perbandingan algoritma yang terukur | Sedikit lebih kompleks karena melibatkan pembangunan artefak, tapi justru sesuai karena pipeline adalah instrumen uji |

**Paradigma yang dipilih:** Design Science
**Alasan:** Penelitian ini secara eksplisit membangun pipeline klasifikasi sentimen sebagai artefak — bukan hanya mengamati fenomena, melainkan merancang sistem yang dapat diuji. Artefak ini (pipeline NB vs SVM) berfungsi sebagai instrumen pengujian hipotesis: apakah SVM menghasilkan F1-Score lebih tinggi dari NB pada dataset ulasan mobile banking Indonesia. Ini sesuai dengan definisi Design Science Research di mana artefak dibuat untuk membuktikan klaim, bukan sebagai tujuan akhir.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, klaim "akurasi 91%" pada paper analisis sentimen langsung diterima sebagai bukti bahwa metode tersebut bagus. Angka besar terasa cukup meyakinkan.
> Setelah memahami rantai distorsi dari Reality hingga Knowledge, pertanyaan yang sekarang akan diajukan saat membaca paper analisis sentimen adalah: Bagaimana label sentimen ditentukan — otomatis dari rating atau manual oleh anotator? Apakah dataset seimbang antar kelas positif, negatif, dan netral? Apakah F1-Score per kelas dilaporkan atau hanya akurasi keseluruhan? Dan apakah kedua algoritma yang dibandingkan diuji pada partisi data yang benar-benar identik?
