# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware (Laptop HP 14s-dq5156TU):
  CPU     : Intel Core i5-1235U (12th Gen, up to 4.4 GHz, 10 Core — 2P + 8E)
  RAM     : 16 GB DDR4-3200 MHz
  GPU     : Intel Iris Xe Graphics (tidak digunakan — eksperimen CPU-only)
  Storage : 512 GB PCIe NVMe M.2 SSD

Software:
  OS        : Windows 11 Home
  Browser   : Google Chrome (untuk mengakses Google Colab)
  Platform  : Google Colab (cloud-based Python notebook)
  Runtime   : Python 3.12 (Google Colab default)
  Framework : scikit-learn 1.4.2 (pipeline, klasifikasi, vektorisasi, evaluasi metrik)

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| scikit-learn         | 1.4.2   | PyPI   | MultinomialNB, SVC, TfidfVectorizer, metrik evaluasi|
| google-play-scraper  | 1.2.7   | PyPI   | Scraping ulasan BCA Mobile, Mandiri, BRImo          |
| PySastrawi           | 1.0.1   | PyPI   | Stopword removal & stemming Bahasa Indonesia        |
| pandas               | 2.2.1   | PyPI   | Manipulasi dan penyimpanan dataset CSV              |
| numpy                | 1.26.4  | PyPI   | Operasi numerik dan kalkulasi statistik             |
| scipy                | 1.13.0  | PyPI   | Wilcoxon signed-rank test & Cohen's d               |
| matplotlib           | 3.8.4   | PyPI   | Visualisasi bar chart perbandingan NB vs SVM        |

Konfigurasi:
  Config file     : Parameter dikunci langsung di notebook
  Random seed     : random_state=42 (run tunggal NB & SVM)
                    random_state=0–9 (10 run eksperimen)
                    SVC random_state=42 (fixed di semua run)
  Hyperparameters : NB    → alpha = 1.0 (Laplace smoothing default)
                    SVM   → kernel = linear, C = 1.0
                    TF-IDF→ max_features = 5.000
                    Split → test_size = 0.2, stratify = y

Reproducibility Check:
  [✅] Dependency terdokumentasi (versi library tercatat di README)
  [✅] Dependency terdokumentasi (versi library tercatat di README)
  [✅] Parameter dikunci di notebook dan terdokumentasi di README
  [✅] README instruksi reproduksi lengkap (Latihan 3)
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel Core i5-1235U (12th Gen, up to 4.4 GHz, 10 Core — 2 Performance + 8 Efficient) |
| RAM | 16 GB DDR4-3200 MHz |
| GPU | Intel Iris Xe Graphics (tidak digunakan — MultinomialNB dan SVC berjalan optimal di CPU) |
| OS | Windows 11 Home |
| Runtime | Python 3.12 via Google Colab (diakses melalui browser di laptop HP 14s-dq5156TU) |
| Framework | scikit-learn 1.4.2 — pipeline, klasifikasi, vektorisasi, dan evaluasi metrik |
| Random Seed | Run tunggal: random_state=42 / 10 run eksperimen: random_state=0,1,2,3,4,5,6,7,8,9 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| scikit-learn | 1.4.2 | Pipeline modular, MultinomialNB, SVC, TfidfVectorizer, classification_report, f1_score, accuracy_score |
| google-play-scraper | 1.2.7 | Scraping ulasan BCA Mobile (com.bca), Mandiri Online (com.bankmandiri.mandirionline), BRImo (id.co.bri.brimo) |
| PySastrawi | 1.0.1 | Stopword removal dan stemming Bahasa Indonesia menggunakan StopWordRemoverFactory dan StemmerFactory |
| pandas | 2.2.1 | Manipulasi dan penyimpanan dataset dalam format CSV (read_csv, to_csv, concat, dropna) |
| numpy | 1.26.4 | Operasi numerik dan kalkulasi statistik (np.mean, np.std) untuk analisis 10 run |
| scipy | 1.13.0 | Wilcoxon signed-rank test (scipy.stats.wilcoxon) dan kalkulasi effect size Cohen's d |
| matplotlib | 3.8.4 | Visualisasi bar chart perbandingan F1-Score dan Akurasi, disimpan sebagai grafik_perbandingan.png |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | random_state=42 | F1-Score macro NB dan SVM | — (run pertama sebagai acuan) |
| 2 | random_state=42 | F1-Score macro NB dan SVM | [✅] Ya— hasil identik dengan Run 1 / [ ] Tidak |
| 3 | random_state=42 | F1-Score macro NB dan SVM | [✅] Ya— hasil identik dengan Run 1 dan 2 / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> Hasil bisa berbeda jika urutan eksekusi cell di Colab tidak berurutan dari atas ke bawah sehingga state internal library berubah. Penyebab lain adalah cell yang dieksekusi ulang tanpa restart kernel sehingga ada cache/state tersimpan dari sesi sebelumnya. Untuk mencegah ini, kernel di-restart sebelum setiap repeatability test dan semua cell dijalankan berurutan dari Cell 1.

**Checklist kontrol yang sudah diterapkan:**
- [✅] Random seed dikunci via random_state di setiap fungsi sklearn (train_test_split dan SVC)
- [✅] Tidak ada background process yang mengganggu — Colab dijalankan dalam sesi baru
- [✅] Cache dibersihkan antar-run — kernel di-restart sebelum setiap repeatability test
- [✅] Config file yang sama untuk semua run — NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF max_features=5000 tidak diubah antar run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Perbandingan Naive Bayes dan SVM Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store

## 1. Environment
> Hardware : HP 14s-dq5156TU
             CPU     : Intel Core i5-1235U (12th Gen, 4.4 GHz, 10 Core)
             RAM     : 16 GB DDR4-3200 MHz
             Storage : 512 GB PCIe NVMe M.2 SSD
             OS       : Windows 11 Home
             Platform : Google Colab (Python 3.12)
             Library  :
                        - scikit-learn        == 1.4.2
                        - google-play-scraper == 1.2.7
                        - PySastrawi          == 1.0.1
                        - pandas              == 2.2.1
                        - numpy               == 1.26.4
                        - scipy               == 1.13.0
                        - matplotlib          == 3.8.4

## 2. Installation
> Jalankan cell berikut di Google Colab sebelum eksperimen:
    !pip install google-play-scraper
    !pip install PySastrawi
  (scikit-learn, pandas, numpy, scipy, matplotlib sudah tersedia di Colab secara default)

## 3. Data
> Sumber   : Google Play Store via google-play-scraper
  Aplikasi : BCA Mobile        (com.bca)
             Mandiri Online    (com.bankmandiri.mandirionline)
             BRImo             (id.co.bri.brimo)
  Jumlah   : ±2.000 ulasan per aplikasi, total ±6.000 ulasan
  Bahasa   : Indonesia (lang='id', country='id')
  Sort     : Sort.NEWEST, count=2000
  Format   : CSV → [nama_user, ulasan, rating, tanggal, aplikasi sentimen]
  Label    : positif (4–5★), netral (3★), negatif (1–2★)
  File     : dataset_ulasan_banking.csv  (data mentah)
             dataset_bersih.csv          (setelah preprocessing)

## 4. Execution
> Jalankan notebook NB_vs_SVM_Sentiment_MobileBanking.ipynb
  secara berurutan dari cell pertama sampai terakhir:
    Cell 1  : Install google-play-scraper
    Cell 2  : Import semua library
    Cell 3  : Scraping BCA Mobile
    Cell 4  : Scraping Mandiri Online
    Cell 5  : Scraping BRImo (ID: id.co.bri.brimo)
    Cell 6  : Gabungkan + labeling sentimen + simpan CSV
    Cell 7  : Install PySastrawi + fungsi preprocessing
    Cell 8  : Load CSV + jalankan preprocessing
    Cell 9  : Simpan dataset_bersih.csv
    Cell 10 : TF-IDF vectorizer + split 80:20 stratified
    Cell 11 : Training + evaluasi Naive Bayes
    Cell 12 : Training + evaluasi SVM
    Cell 13 : Tabel perbandingan + simpan hasil_perbandingan.csv
    Cell 14 : Visualisasi bar chart + simpan grafik_perbandingan.png
    Cell 15 : 10 run eksperimen NB vs SVM
    Cell 16 : Wilcoxon test + Cohen's d + simpan hasil_statistik.csv
    Cell 17 : Download semua file output
  PENTING: Restart kernel sebelum menjalankan ulang agar tidak ada state tersimpan dari sesi sebelumnya

## 5. Configuration
> Parameter utama yang dikunci:
    TF-IDF  : max_features = 5.000
    Split   : test_size = 0.2, stratify = y, random_state = 42
    NB      : alpha = 1.0
    SVM     : kernel = linear, C = 1.0, random_state = 42
    10 run  : random_state = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

## 6. Expected Output
> File output yang dihasilkan:
    dataset_ulasan_banking.csv → data mentah ±6.000 ulasan
    dataset_bersih.csv         → data setelah preprocessing PySastrawi
    hasil_perbandingan.csv     → F1-Score dan Akurasi NB vs SVM (run tunggal)
    hasil_statistik.csv        → F1-Score NB dan SVM dari 10 run
    grafik_perbandingan.png    → bar chart perbandingan (dpi=300)

  Hasil aktual eksperimen:
    F1-Score NB   : 0,5466 (run tunggal) / 0,5532 (rata-rata 10 run)
    F1-Score SVM  : 0,5553 (run tunggal) / 0,5627 (rata-rata 10 run)
    Akurasi NB    : 0,8385
    Akurasi SVM   : 0,8455
    p-value       : 0,0039 (H₀ ditolak, SVM lebih baik)
    Cohen's d     : 2,0479 (effect size besar)

```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [✅] Repeatability / [✅] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Justifikasi:

Repeatability sudah tercapai karena seed dikunci via random_state di setiap fungsi sklearn sehingga menjalankan notebook yang sama dengan kernel restart menghasilkan output identik. Reproducibility juga sudah tercapai karena semua file hasil tersedia dan README sudah lengkap dengan spesifikasi hardware laptop HP 14s-dq5156TU, langkah instalasi, deskripsi data, urutan eksekusi cell, konfigurasi parameter, dan contoh output aktual.

> Komponen yang belum terdokumentasi:

File requirements.txt dengan versi yang di-lock secara eksplisit belum dibuat, sehingga peneliti lain perlu menginstall library satu per satu sesuai versi di README. Selain itu, import NLTK di awal notebook tidak digunakan (preprocessing menggunakan PySastrawi) dan sebaiknya dihapus agar tidak membingungkan peneliti lain.
