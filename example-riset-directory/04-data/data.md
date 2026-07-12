# 04-data

Data mentah hasil eksperimen — output dari Tahap 2 (scraping + preprocessing) dan Tahap 3 (eksperimen), input untuk Tahap 4 (analisis).

## Catatan

Data di folder ini bersifat mentah (raw) dan belum diolah lebih lanjut. Hasil olahan (statistik, grafik) disimpan di [../06-output/](../06-output/).

## Berkas

| File | Ukuran | Deskripsi |
|------|--------|-----------|
| [dataset_ulasan_banking.csv](dataset_ulasan_banking.csv) | 6.000 baris | Data mentah hasil scraping Google Play Store — kolom: nama_user, ulasan, rating, tanggal, aplikasi, sentimen |
| [dataset_bersih.csv](dataset_bersih.csv) | 5.758 baris | Data setelah preprocessing PySastrawi — tambahan kolom: ulasan_bersih |
| [hasil_perbandingan.csv](hasil_perbandingan.csv) | 2 baris | Hasil run tunggal (random_state=42) — F1-Score dan Akurasi NB vs SVM |
| [hasil_statistik.csv](hasil_statistik.csv) | 10 baris | Hasil 10 run eksperimen (random_state=0–9) — F1-Score NB dan SVM per run |

## Struktur Kolom

### dataset_ulasan_banking.csv
| Kolom | Tipe | Deskripsi |
|-------|------|-----------|
| nama_user | string | Nama pengguna Google Play Store |
| ulasan | string | Teks ulasan berbahasa Indonesia |
| rating | integer | Rating bintang (1–5) |
| tanggal | datetime | Tanggal ulasan ditulis |
| aplikasi | string | BCA Mobile / Mandiri Online / BRImo |
| sentimen | string | positif / netral / negatif (dari rating bintang) |

### dataset_bersih.csv
Sama dengan dataset_ulasan_banking.csv + kolom tambahan:
| Kolom | Tipe | Deskripsi |
|-------|------|-----------|
| ulasan_bersih | string | Teks ulasan setelah preprocessing (lowercase, stopword removal, stemming) |

### hasil_perbandingan.csv
| Kolom | Tipe | Deskripsi |
|-------|------|-----------|
| Algoritma | string | Naive Bayes / SVM |
| F1_Score | float | F1-Score macro-average |
| Akurasi | float | Akurasi klasifikasi |

### hasil_statistik.csv
| Kolom | Tipe | Deskripsi |
|-------|------|-----------|
| Run | integer | ID run (1–10) |
| F1_NaiveBayes | float | F1-Score NB pada run tersebut |
| F1_SVM | float | F1-Score SVM pada run tersebut |

## Distribusi Dataset

### dataset_ulasan_banking.csv (6.000 ulasan)
| Aplikasi | Jumlah |
|----------|--------|
| BCA Mobile | 2.000 |
| Mandiri Online | 2.000 |
| BRImo | 2.000 |

| Sentimen | Jumlah | Persentase |
|----------|--------|------------|
| Positif (4–5★) | 4.184 | 69,7% |
| Negatif (1–2★) | 1.540 | 25,7% |
| Netral (3★) | 276 | 4,6% |

### dataset_bersih.csv (5.758 ulasan)
242 ulasan dihapus karena kosong setelah preprocessing.