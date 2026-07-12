# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : dataset_ulasan_banking.csv (BCA Mobile, Mandiri Online, BRImo — Google Play Store)
Jumlah data awal  : 6.000 ulasan (2.000 per aplikasi)

Cleaning:
| Masalah  | Jumlah Kasus | Penanganan | Justifikasi |
|----------|-------------|------------|-------------|
| Ulasan kosong setelah preprocessing | 242 dari 6.000 (4,03%) | Listwise deletion — dropna(subset=['ulasan_bersih']) + filter string kosong (Cell 12) | Ulasan yang hanya berisi emoji/angka/simbol menjadi string kosong setelah regex cleaning — tidak bisa diberi bobot TF-IDF |
| Duplikat | Tidak ditangani | Tidak ada langkah drop_duplicates() di pipeline | Limitasi nyata implementasi — diakui secara eksplisit sebagai keterbatasan, bukan diklaim sudah tertangani |
| Error format (angka/simbol/emoji) | Seluruh 6.000 baris | Regex re.sub(r'[^a-zA-Z\s]', '', teks) | Membersihkan noise karakter yang tidak bermakna sentimen |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|--------------|----------|--------|--------|
| Case folding | ulasan | teks.lower() | Menyamakan "Bagus" dan "bagus" jadi satu token |
| Hapus non-alfabet | ulasan | Regex hapus angka, simbol, emoji | Vocabulary tidak dipenuhi karakter non-bermakna |
| Normalisasi spasi | ulasan | re.sub(r'\s+', ' ', teks).strip() | Merapikan hasil regex sebelumnya |
| Stopword removal | ulasan | Sastrawi StopWordRemoverFactory | Hapus kata umum non-diskriminatif |
| Stemming | ulasan | Sastrawi StemmerFactory | Menyatukan variasi morfologis |
| Labeling | rating → sentimen | rating≥4=positif, =3=netral, <3=negatif | Proxy label (limitasi diakui di WS-05) |

Normalization:
  Metode    : TF-IDF (TfidfVectorizer, max_features=5.000) — L2-norm default sklearn
  Alasan    : Data teks, bukan numerik berskala berbeda; min-max/z-score/robust scaling tidak relevan. TF-IDF sudah ternormalisasi (L2-norm=1) — normalisasi tambahan melanggar prinsip Minimal Distortion
  Parameter : dihitung dari: [✅] training set saja — tfidf.fit_transform(X_train), lalu tfidf.transform(X_test)

Leakage Check:
  [✅] Parameter TF-IDF (vocabulary + idf) dari training set saja
  [✅] Split (train_test_split, stratify=y, random_state=42) dilakukan sebelum TF-IDF di-fit
  [✅] 10-run eksperimen (Cell 17) split ulang sebelum fit TF-IDF setiap run — tidak ada kebocoran antar run

Jumlah data akhir : 5.758 ulasan (6.000 − 242) → Training : 4.606 (80%) | Testing : 1.152 (20%)
Script tersedia   : [✅] Ya → NB_vs_SVM_Sentiment_MobileBanking.ipynb (Cell 9–12)
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|--------------|------------|-------------|
| Ulasan kosong setelah preprocessing | 242 dari 6.000 (4,03%) | Listwise deletion (dropna + filter string kosong) | Ulasan tanpa huruf sama sekali tidak bisa diproses TF-IDF |
| Duplikat teks | Tidak diperiksa | — | Limitasi pipeline — belum ada langkah df.duplicated() |
| Karakter noise | Seluruh 6.000 baris | Regex cleaning di fungsi preprocessing() | Bukan penghapusan baris, tapi pembersihan token |

**Jumlah data sebelum cleaning:** 6.000
**Jumlah data setelah cleaning:** 5.758
**Persentase data yang hilang/berubah:** 4,03% (242 dari 6.000)

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|------------|------------|----------|--------------------|--------|
| Teks ulasan mentah | Panjang bervariasi | Right-skewed (mayoritas pendek) | Ya (beberapa panjang) | Tidak diskalakan langsung — direpresentasikan via TF-IDF | Teks tidak punya skala numerik |
| Vektor TF-IDF | 0–1 per fitur, max_features=5.000 | Sparse | Tidak relevan sebagai outlier numerik | L2-norm (built-in) | Sudah ternormalisasi otomatis saat fit |
| Rating bintang (1–5) | 1–5 | Skewed ke 4–5 (69,7% positif) | Class imbalance, bukan outlier | Tidak perlu — basis label nominal | Bukan variabel yang di-scale |

**Apakah normalisasi diperlukan?** [✅] Ya (TF-IDF L2-norm) — normalisasi numerik tambahan Tidak diperlukan
**Justifikasi:**
> TF-IDF sudah menghasilkan representasi ternormalisasi secara built-in. Menambahkan min-max/z-score di atasnya melanggar prinsip Minimal Distortion — berisiko mendistorsi bobot kata langka, terutama untuk kelas netral yang hanya 4,6% dari data.

**Leakage check:**
- [✅] Parameter (vocabulary_, idf_) dihitung dari X_train saja
- [✅] TF-IDF diterapkan setelah train_test_split
---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: dataset_ulasan_banking.csv → dataset_bersih.csv
2. Data awal: 6.000 records, 5 kolom
3. Cleaning:
   - Missing/kosong: 242 kasus, metode: dropna + filter string kosong
   - Duplikat: TIDAK diperiksa — limitasi pipeline
   - Error format: seluruh data melalui regex cleaning
4. Transformation: lowercase → hapus non-alfabet → normalisasi spasi
   → stopword removal (Sastrawi) → stemming (Sastrawi) → labeling sentimen
5. Normalisasi: TF-IDF (max_features=5.000, L2-norm), parameter dari training set saja
6. Data akhir: 5.758 records → training 4.606 (80%) / testing 1.152 (20%)
7. Leakage check: [✅] Lulus
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Preprocessing dalam penelitian ini secara sadar tidak menambahkan normalisasi numerik di atas TF-IDF — karena TF-IDF sendiri sudah ternormalisasi via L2-norm, penambahan scaling ekstra hanya akan mendistorsi bobot IDF tanpa manfaat tambahan (prinsip Minimal Distortion). Namun di sisi lain, ditemukan under-preprocessing yang tidak disadari: tidak ada langkah pengecekan duplikat sama sekali di pipeline. Ini bukan keputusan sadar melainkan langkah yang terlewat karena template preprocessing umum fokus ke noise karakter dan missing value, sementara duplikat dianggap otomatis tertangani — padahal tidak. Risiko over-preprocessing dan under-preprocessing sama-sama nyata: keduanya muncul dari mengikuti kebiasaan tanpa verifikasi eksplisit terhadap setiap elemen cleaning triad (missing, duplikat, error format).
