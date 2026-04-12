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
   - Pertanyaan pertama saya: 95% akurat diukur pada dataset seperti apa? Siapa yang mengumpulkan datanya, dan apakah kondisi pengujiannya mewakili kondisi nyata?
   - Data yang dibutuhkan untuk verifikasi: Ukuran dan komposisi dataset uji, metode validasi (cross-validation / hold-out / independent test set), baseline pembanding, dan apakah ada konflik kepentingan dari peneliti.

2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [✅] Design Science  [ ] Mixed
   - Alasan: Riset TI seringkali menghasilkan sistem/artefak. Design Science memungkinkan kita membangun sekaligus menguji hipotesis — apakah artefak yang dibuat memang menjawab masalah yang diklaim.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Dataset yang digunakan bersih, representatif, dan bebas dari bias seleksi
   - Sumber bias potensial: Peneliti memilih metrik evaluasi yang paling menguntungkan metodenya; dataset terlalu homogen sehingga tidak bisa digeneralisasi
   - Langkah mitigasi: Gunakan dataset independen dari pihak ketiga, laporkan semua metrik (bukan hanya yang bagus), dan lakukan peer review sebelum publikasi

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Data hasil eksperimen mentah — tidak akan dihapus outlier tanpa justifikasi metodologis yang jelas dan transparan
   - Batasan yang diakui sejak awal: Penelitian ini hanya berlaku pada konteks/domain tertentu; generalisasi ke luar konteks membutuhkan replikasi tambahan
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul:  Optimasi Algoritma Random Forest menggunakan Principal Component Analysis untuk Deteksi Malware
> Penulis (Tahun): Fauzi Adi Rafrastara, Ricardus Anggi Pramunendar, Dwi Puji Prabowo, Etika Kartikadarma, Usman Sudibyoe (2023)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengunduh dataset malware dari UCI Machine Learning Repository (VxHeaven & VirusTotal), terdiri dari 595 file goodware dan 5.653 file malware |  Dataset dibuat tahun 2019, sementara penelitian dilakukan 2023 — malware sudah banyak berkembang, sehingga dataset tidak merepresentasikan ancaman malware terkini |
| Data → Processing | Menghapus 2 fitur bernilai 0 di seluruh data, menghapus fitur 'filename', lalu menyeimbangkan data menggunakan Random Under Sampling dari 5.653 menjadi 595 data malware | Random Under Sampling membuang 5.058 data malware — banyak pola malware yang hilang dan tidak ikut dianalisis |
| Processing → Analysis | Membandingkan 5 algoritma (Random Forest, Adaboost, Neural Network, SVM, kNN) menggunakan 5-Fold Cross Validation, kemudian menerapkan PCA |Hanya menggunakan 2 metrik (akurasi & recall) — metrik lain seperti precision, F1-score, dan AUC tidak dilaporkan sama sekali |
| Analysis → Inference | Menyimpulkan Random Forest terbaik dengan akurasi 98.3%, dan dengan PCA meningkat menjadi 98.7% | Peningkatan hanya 0.4% (dari 98.3% ke 98.7%) namun diklaim signifikan — ini bisa jadi dalam batas noise statistik biasa, bukan peningkatan nyata |
| Inference → Knowledge | Mengklaim "PCA berhasil meningkatkan performa Random Forest untuk deteksi malware" | Klaim terlalu luas: eksperimen hanya dilakukan di satu dataset statis dari satu sumber, belum diuji di lingkungan nyata atau dataset malware lain yang lebih baru |

**Distorsi paling besar di tahap:** Data → Processing

**Dua distorsi spesifik yang teridentifikasi:**
1. Random Under Sampling yang agresif — Dari 5.653 data malware, hanya 595 yang dipertahankan (membuang 89% data malware). Ini sangat berisiko karena banyak pola serangan malware yang ikut terbuang, sehingga model tidak belajar dari variasi malware yang sesungguhnya.
2. Dataset usang — Dataset berasal dari tahun 2019, sementara penelitian dipublikasikan 2023. Para penulis sendiri mengakui ini di bagian kesimpulan. Artinya, performa 98.7% hanya berlaku untuk malware lama, bukan malware yang berkembang saat ini.

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

**Topik riset:**  Pengaruh penggunaan WhatsApp terhadap produktivitas belajar mahasiswa

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 | 3 | 2 |
| Jenis data yang dikumpulkan | Data terukur: frekuensi penggunaan WhatsApp per hari, nilai IPK, jam belajar efektif mahasiswa | Wawancara mendalam tentang perasaan dan pengalaman mahasiswa saat belajar sambil buka WhatsApp | Membuat fitur/sistem baru di WhatsApp untuk membantu produktivitas belajar lalu diuji efektivitasnya |
| Limitasi paradigma | Tidak menangkap alasan mendalam kenapa WhatsApp bisa mengganggu atau membantu belajar | Sulit direplikasi karena jawaban setiap mahasiswa berbeda-beda dan subjektif | Kurang cocok karena topik ini bukan tentang membangun sistem baru |

**Paradigma yang dipilih:** Positivis
**Alasan:** Topik ini bisa diukur secara objektif. Variabel independennya jelas yaitu intensitas penggunaan WhatsApp, dan variabel dependennya terukur yaitu produktivitas belajar mahasiswa yang bisa dilihat dari IPK atau jam belajar efektif. Hasilnya bisa diuji ulang oleh peneliti lain dengan kondisi yang sama, sesuai prinsip positivisme.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, klaim "95% akurat" langsung dipercaya begitu saja tanpa mempertanyakan apapun. Angka yang besar terasa sudah cukup sebagai bukti bahwa metode tersebut memang bagus.
> Setelah memahami rantai distorsi dari Reality hingga Knowledge, pertanyaan yang sekarang akan diajukan saat membaca paper adalah: Dataset apa yang digunakan dan seberapa representatif datanya? Apakah semua metrik dilaporkan atau hanya yang terlihat bagus saja? Apakah ada variabel lain yang ikut mempengaruhi hasil tanpa disadari? Dan apakah peneliti memiliki kepentingan pribadi terhadap metode yang diteliti?
