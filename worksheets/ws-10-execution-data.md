# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     | NB vs SVM       | 0    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 2     | NB vs SVM       | 1    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 3     | NB vs SVM       | 2    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 4     | NB vs SVM       | 3    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 5     | NB vs SVM       | 4    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 6     | NB vs SVM       | 5    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 7     | NB vs SVM       | 6    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 8     | NB vs SVM       | 7    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 9     | NB vs SVM       | 8    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |
| 10    | NB vs SVM       | 9    | NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF 5000   | Completed | —     | hasil_statistik.csv   |

Jumlah runs per skenario : 2 (Naive Bayes dan SVM dijalankan berpasangan dalam setiap run)
Run per skenario         : 10
Total runs keseluruhan   : 20 eksekusi model (10 run × 2 algoritma)

DATA LOG (per run — contoh Run #1):
  Run ID    : run-001
  Timestamp : Dijalankan secara berurutan di Google Colab dalam satu sesi
  Skenario  : NB vs SVM — Comparison Study, random_state=0
  Input     : dataset_bersih.csv (±6.000 ulasan BCA Mobile, Mandiri Online, BRImo)
  Output    : F1-Score NB dan SVM pada run ke-1 disimpan ke hasil_statistik.csv
  Anomali   : Tidak ada
  Catatan   : SVC random_state=42 dikunci tetap di semua run; yang berubah hanya random_state train_test_split (0–9)
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | NB vs SVM — Comparison Study | 0 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 2 | NB vs SVM — Comparison Study | 1 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 3 | NB vs SVM — Comparison Study | 2 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 4 | NB vs SVM — Comparison Study | 3 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 5 | NB vs SVM — Comparison Study | 4 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 6 | NB vs SVM — Comparison Study | 5 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 7 | NB vs SVM — Comparison Study | 6 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 8 | NB vs SVM — Comparison Study | 7 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 9 | NB vs SVM — Comparison Study | 8 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |
| 10 | NB vs SVM — Comparison Study | 9 | NB: alpha=1.0 / SVM: kernel=linear, C=1.0, random_state=42 / TF-IDF: max_features=5000 / Split: test_size=0.2, stratify=y | Completed |

**Total skenario:**  1 (Comparison Study NB vs SVM)
**Run per skenario:** 10
**Total run keseluruhan:** 10 run × 2 algoritma = 20 eksekusi model

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 s.d. run-010 |
| Timestamp | Dijalankan berurutan dalam satu sesi Google Colab |
| Skenario | NB vs SVM Comparison Study |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed (train_test_split) | random_state = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 |
| Seed (SVC) | random_state = 42 (dikunci tetap di semua run) |
| Code version | Notebook NB_vs_SVM_Sentiment_MobileBanking.ipynb — Cell 15 (10 run loop) |
| Dataset | dataset_bersih.csv — ±6.000 ulasan (BCA Mobile, Mandiri Online, BRImo) |
| TF-IDF | max_features = 5.000 |
| Split | test_size = 0.2, stratify = y |
| NB | alpha = 1.0 (MultinomialNB) |
| SVM | kernel = linear, C = 1.0 (SVC) |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|-----------|-------------|
| F1-Score NB (macro-average) | float | 0.0 – 1.0 |
| F1-Score SVM (macro-average) | float | 0.0 – 1.0 |
| Rata-rata F1 NB (10 run) | float | 0.0 – 1.0 |
| Rata-rata F1 SVM (10 run) | float | 0.0 – 1.0 |
| Wilcoxon p-value | float | 0.0 – 1.0 |
| Cohen's d | float | Tidak terbatas (> 0.8 = large effect) |

**Format output:** [✅] CSV — hasil_statistik.csv berisi kolom [Run, F1_NaiveBayes, F1_SVM]; hasil_perbandingan.csv untuk run tunggal; grafik_perbandingan.png untuk visualisasi bar chart / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Scraping Google Play gagal karena koneksi terputus atau rate limit | Dokumentasi error, tunggu beberapa menit, re-run cell scraping; jika terus gagal, gunakan dataset CSV yang sudah tersimpan sebelumnya agar tidak perlu scraping ulang |
| Hasil ekstrem | F1-Score salah satu run sangat rendah (<0.3) atau sangat tinggi (>0.9) dibanding run lain | Cek apakah stratify=y aktif dan distribusi kelas pada split tersebut wajar; dokumentasi nilai anomali, jangan dihapus — laporkan di Discussion sebagai variabilitas eksperimen |
| Waktu eksekusi anomali | SVM pada run tertentu jauh lebih lama dari biasanya | Cek apakah ada proses lain berjalan di Colab; dokumentasi waktu eksekusi; jika konsisten lambat, catat sebagai catatan efisiensi komputasi di Discussion |
| Inkonsistensi dengan run lain | F1-Score run ke-5 berbeda jauh dari run lain meski seed sudah dikunci | Cek urutan eksekusi cell — pastikan kernel di-restart sebelum run ulang; jika masih anomali setelah restart, dokumentasi dan laporkan sebagai temuan, bukan dihapus |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Sebelum mengerjakan penelitian ini, belum pernah secara sadar mempertimbangkan jumlah run sebagai bagian dari validitas hasil. Eksperimen dianggap selesai ketika kode berjalan dan menghasilkan output yang masuk akal, tanpa mempertanyakan apakah hasil tersebut akan berbeda jika data dibagi dengan cara yang berbeda.

**Yang akan dilakukan berbeda:**
> Setelah memahami pentingnya multiple run, eksperimen selanjutnya akan selalu menggunakan minimal 10 run dengan seed yang berbeda-beda dan pre-determined sebelum eksekusi dimulai. Single run berisiko menghasilkan angka yang kebetulan menguntungkan atau merugikan karena pembagian data yang spesifik — tanpa distribusi hasil dari banyak run, tidak ada cara untuk mengetahui apakah angka tersebut stabil atau hanya noise. Multiple run menghasilkan mean dan standar deviasi yang memungkinkan uji statistik seperti Wilcoxon dan perhitungan effect size Cohen's d, sehingga klaim "SVM lebih baik dari NB" bisa dibuktikan secara ilmiah, bukan sekadar membandingkan dua angka dari satu percobaan.