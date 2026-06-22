# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah algoritma SVM menghasilkan F1-Score lebih tinggi 
                    dibandingkan Naive Bayes dalam klasifikasi sentimen ulasan 
                    aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, 
                    BRImo) di Google Play Store menggunakan representasi fitur TF-IDF?
Metrik Utama      : F1-Score macro-average (primary), Akurasi (secondary)

Tabel Hasil:
| Algoritma   | F1-Score macro (mean ± std) | Akurasi* | n  |
|-------------|-----------------------------|----------|----|
| SVM         | 0,5627 ± 0,0039             | 0,8455   | 10 |
| Naive Bayes | 0,5532 ± 0,0057             | 0,8385   | 10 |

*Akurasi dari run tunggal random_state=42 — tidak dicatat per 10 run

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar chart grouped | Perbandingan F1-Score dan Akurasi NB vs SVM run tunggal | F1-Score & Akurasi run tunggal |
| 2 | Box plot | Distribusi F1-Score NB vs SVM dari 10 run | F1-Score 10 run |

Bias Check:
  [✅] Y-axis mulai dari 0 (atau dijustifikasi)
  [✅] Error bar/CI ditampilkan - std dari 10 run
  [✅] Semua data disertakan (tidak cherry-picked)
  [✅] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Perhitungan std F1-Score dari 10 run:

NB: 0,5542 / 0,5578 / 0,5460 / 0,5599 / 0,5496 / 0,5558 / 0,5544 / 0,5589 / 0,5456 / 0,5495
Mean = 0,5532 | Std = 0,0057

SVM: 0,5601 / 0,5691 / 0,5541 / 0,5595 / 0,5617 / 0,5648 / 0,5666 / 0,5671 / 0,5643 / 0,5594
Mean = 0,5627 | Std = 0,0039

**Tabel Perbandingan Hasil Eksperimen NB vs SVM (10 Run):**

| Algoritma | F1-Score macro (mean ± std) | Akurasi | n |
|-----------|-----------------------------|---------|---|
| SVM | 0,5627 ± 0,0039 | 0,8455 | 10 |
| Naive Bayes | 0,5532 ± 0,0057 | 0,8385 | 10 |

*Akurasi dari run tunggal random_state=42 — tidak dicatat per 10 run. Diurutkan berdasarkan F1-Score (metrik utama) dari tertinggi ke terendah N=10 run per algoritma dengan random_state=0–9 pada train_test_split

**Checklist tabel:**
- [✅] Self-contained — judul jelas, satuan ada, N tercantum
- [✅] Mean ± std — bukan single number (untuk F1-Score)
- [✅] Diurutkan berdasarkan metrik utama (F1-Score tertinggi ke terendah)
- [✅] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|--------------|-------|---------------------|
| 1 | Bar chart grouped (sudah dibuat di Cell 14 → grafik_perbandingan.png) | SVM unggul dari NB baik di F1-Score maupun Akurasi pada run tunggal | F1-Score NB=0,5466, SVM=0,5553; Akurasi NB=0,8385, SVM=0,8455 |
| 2 | Box plot | Distribusi F1-Score NB vs SVM dari 10 run menunjukkan SVM konsisten lebih tinggi dengan variabilitas lebih rendah | F1-Score 10 run NB (mean=0,5532, std=0,0057) dan SVM (mean=0,5627, std=0,0039) |

**Justifikasi pemilihan grafik:**

- Bar chart → tepat untuk perbandingan dua algoritma pada dua metrik secara langsung; sudah diimplementasikan di Cell 14 dengan dpi=300
- Box plot → melengkapi bar chart dengan menampilkan distribusi dan variabilitas F1-Score dari 10 run; memperlihatkan bahwa SVM tidak hanya lebih tinggi rata-ratanya tapi juga lebih stabil (std lebih kecil)

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91,2%, Metode B = 90,8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|------------|---------|
| Apakah Y-axis menyesatkan? | Ya — dengan Y-axis mulai dari 90%, Metode A terlihat jauh lebih unggul padahal perbedaannya hanya 0,4%. Secara visual perbedaan tampak dramatis padahal sangat kecil |
| Apakah error bar ditampilkan? | Tidak — tanpa error bar tidak bisa diketahui apakah perbedaan 0,4% ini signifikan atau hanya variasi acak |
| Apakah semua kondisi ditampilkan? | Tidak jelas — jika hanya run terbaik yang ditampilkan, ini termasuk cherry-picking |
| Apa solusinya? | Mulai Y-axis dari 0, tambahkan error bar (± std), tampilkan semua run, dan sertakan uji statistik untuk membuktikan perbedaan signifikan |

**Evaluasi grafik penelitian ini (Cell 14 — grafik_perbandingan.png):**

- [✅] Y-axis mulai dari 0 — ax.set_ylim(0, 1.1) dikunci di kode
 Error bar belum ditampilkan — Cell 14 hanya bar chart tanpa error bar karena menggunakan run tunggal; untuk box plot 10 run variabilitas akan terlihat
- [✅] Semua data disertakan — kedua algoritma dan kedua metrik ditampilkan
- [✅] Tidak menggunakan 3D — grafik 2D sederhana

**Yang perlu diperbaiki:**
Bar chart di Cell 14 belum menyertakan error bar karena hanya menggunakan nilai run tunggal. Untuk melengkapi, box plot dari 10 run (Latihan 2 grafik ke-2) akan menampilkan variabilitas secara eksplisit sehingga pembaca bisa menilai stabilitas hasil kedua algoritma.

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik melayani fungsi yang berbeda dan saling melengkapi. Tabel memberikan presisi numerik yang self-contained — pembaca bisa membaca angka F1-Score NB 0,5532 ± 0,0057 dan SVM 0,5627 ± 0,0039 secara eksak, membandingkan, dan memverifikasi sendiri. Grafik sebaliknya memberikan pola visual yang tidak bisa ditangkap dari angka saja — box plot dari 10 run langsung memperlihatkan bahwa distribusi SVM lebih tinggi dan lebih sempit dari NB tanpa perlu menghitung. Jika hanya ada tabel, pembaca harus membayangkan distribusinya. Jika hanya ada grafik, pembaca tidak bisa mengutip angka presisi untuk perbandingan atau replikasi. Keduanya wajib ada karena menjawab pertanyaan yang berbeda: tabel menjawab "berapa tepatnya?" dan grafik menjawab "bagaimana polanya?".

> Dalam penelitian ini, bar chart di Cell 14 dibuat tanpa error bar karena hanya menggunakan nilai run tunggal. Tanpa error bar, pembaca tidak bisa menilai apakah perbedaan F1-Score antara NB dan SVM stabil atau hanya kebetulan dari satu pembagian data. Ini adalah contoh grafik yang secara tidak sengaja menyesatkan — secara teknis benar (angkanya akurat) tapi menyembunyikan ketidakpastian yang penting. Box plot dari 10 run melengkapi kekurangan ini dengan menampilkan variabilitas secara eksplisit.