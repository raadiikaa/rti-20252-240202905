# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [✅] Semua skenario tercakup — Comparison Study NB vs SVM selesai
  [✅] Jumlah run sesuai rencana — 10 run dari 10 yang direncanakan
  [✅] Tidak ada file output hilang — hasil_statistik.csv hasil_perbandingan.csv, grafik_perbandingan.png tersedia
  Missing: 0 dari 10 data points

Format Consistency:
  [✅] Semua file format sama — CSV untuk semua output tabular
  [✅] Header konsisten — [Run, F1_NaiveBayes, F1_SVM] di hasil_statistik.csv
  [✅] Tipe data konsisten — F1-Score bertipe float di semua run

Range & Logic:
  [✅] Nilai dalam range masuk akal — F1-Score NB dan SVM berada di rentang 0–1
  [✅] Tidak ada nilai negatif
  [✅] Metrik tidak di luar range 0–1
  Anomali ditemukan: Tidak ada anomali terdeteksi

Cross-Validation:
  [✅] Run identik → hasil mendekati — rata-rata F1 NB 0,5532 dan SVM 0,5627 konsisten antar run
  [✅] Trend konsisten dengan ekspektasi teori — SVM konsisten lebih tinggi dari NB di 9 dari 10 run

Keputusan:
  [✅] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| NB vs SVM — Comparison Study (seed 0–9) | 10 | 10 | 0 | - |


**Total expected:** 10| **Total actual:** 10 | **Missing:** 0

**Keputusan untuk data missing:**
> Tidak ada data missing. Seluruh 10 run berhasil dieksekusi secara berurutan dalam satu sesi Google Colab tanpa crash atau interupsi. Hasil setiap run tersimpan otomatis ke hasil_statistik.csv melalui pandas to_csv.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset hasil 10 run eksperimen (F1-Score NB dan SVM):**

| Run | F1-Score NB | F1-Score SVM |
|-----|-------------|--------------|
| 1 | 0,5542 | 0,5601 |
| 2 | 0,5578 | 0,5691 |
| 3 | 0,5460 | 0,5541 |
| 4 | 0,5599 | 0,5595 |
| 5 | 0,5496 | 0,5617 |
| 6 | 0,5558 | 0,5648 |
| 7 | 0,5544 | 0,5666 |
| 8 | 0,5589 | 0,5671 |
| 9 | 0,5456 | 0,5643 |
| 10| 0,5495 | 0,5594 |

**Deteksi outlier (F1-Score NB) menggunakan IQR:**

- Nilai terurut: 0,5456 / 0,5460 / 0,5495 / 0,5496 / 0,5542 / 0,5544 / 0,5558 / 0,5578 / 0,5589 / 0,5599
- Q1 = 0,5496 | Q3 = 0,5568 | IQR = 0,0072
- Batas bawah (Q1 - 1,5×IQR) = 0,5388
- Batas atas (Q3 + 1,5×IQR) = 0,5676
- Outlier terdeteksi: Tidak ada — semua nilai dalam rentang 0,5388–0,5676

**Deteksi outlier (F1-Score SVM) menggunakan IQR:**

- Nilai terurut: 0,5541 / 0,5594 / 0,5595 / 0,5601 / 0,5617 / 0,5643 / 0,5648 / 0,5666 / 0,5671 / 0,5691
- Q1 = 0,5598 | Q3 = 0,5657 | IQR = 0,0059
- Batas bawah (Q1 - 1,5×IQR) = 0,5509
- Batas atas (Q3 + 1,5×IQR) = 0,5746
- Outlier terdeteksi: Tidak ada — semua nilai dalam rentang 0,5509–0,5746

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| -       |  -    | Tidak ada outlier terdeteksi pada 10 run eksperimen | Data valid, siap analisis |

**Run 4:**
Pada Run 4 (seed=3), F1-Score NB (0,5599) lebih tinggi dari SVM (0,5595) — satu-satunya run di mana NB mengungguli SVM. Ini bukan anomali statistik karena nilainya masih dalam batas IQR, melainkan variasi natural dari pembagian data pada seed tertentu. Justru ini memperkuat pentingnya 10 run: jika eksperimen berhenti di seed=3 saja, kesimpulannya bisa terbalik.

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100 % data terkumpul — 10 dari 10 run tercatat di hasil_statistik.csv
**2. Format:** [✅] Konsisten — semua output dalam format CSV dengan header [Run, F1_NaiveBayes, F1_SVM] dan tipe data float yang seragam di semua run 
**3. Range check (anomali):** Tidak ada anomali — seluruh nilai F1-Score NB (0,5456–0,5599) dan SVM (0,5541–0,5691) berada dalam rentang valid 0–1 dan tidak ada outlier berdasarkan deteksi IQR
**4. Logic check:** [✅] Parameter sesuai plan — NB alpha=1.0, SVM kernel=linear C=1.0, TF-IDF max_features=5000, split test_size=0.2 stratify=y, random_state=0–9 untuk split dan random_state=42 untuk SVC semuanya konsisten dengan yang didokumentasikan di WS-09 dan WS-10 

**Kesimpulan:** [✅] Data siap analisis — tidak ada missing data, tidak ada anomali, format konsisten, parameter sesuai rencana eksperimen. SVM mengungguli NB di 9 dari 10 run dengan rata-rata F1 SVM 0,5627 vs NB 0,5532. Dataset hasil_statistik.csv siap digunakan untuk uji statistik Wilcoxon signed-rank test (p=0,0039) dan effect size Cohen's d (1,9428) di tahap analisis berikutnya. 

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> "Data yang benar" berarti nilai yang tercatat secara teknis akurat — tidak ada error komputasi, tidak ada nilai di luar range, dan format sesuai. Sementara "data yang dipercaya" memiliki standar yang lebih tinggi: data tidak hanya benar secara teknis, tetapi juga terbukti konsisten, lengkap, bebas anomali, dan sesuai dengan desain eksperimen yang direncanakan sejak awal.

> Dalam penelitian ini, hasil_statistik.csv dihasilkan secara otomatis oleh pandas to_csv di Cell 16 — artinya tidak ada risiko human error dalam pencatatan. Namun logging otomatis tidak menjamin data benar: bug di dalam loop seperti TF-IDF yang di-fit ulang pada seluruh dataset alih-alih hanya training set bisa menghasilkan angka yang tampak normal tetapi sebenarnya tidak valid karena terjadi data leakage. Proses validasi formal seperti range check, completeness check, dan logic check diperlukan justru untuk mendeteksi kasus-kasus seperti ini — memastikan bahwa angka yang tersimpan benar-benar mencerminkan kondisi eksperimen yang dirancang, bukan artefak dari bug yang tidak terdeteksi.