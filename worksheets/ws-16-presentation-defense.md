# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides   : 9 (7 konten + title + closing)
  Time per slide : ~1,5-2 min
  Total time     : 15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Title + konteks riset | Title slide + logo UPB | 1 min |
| 2 | Problem: ulasan mobile banking belum dianalisis sistematis | Screenshot ulasan Google Play | 2 min |
| 3 | Gap + RQ: 8 paper SLR, belum ada perbandingan NB vs SVM terkontrol | Tabel ringkas gap literatur | 1,5 min |
| 4 | Method: pipeline 5 komponen, 10 run, Wilcoxon + Cohen's d | Diagram pipeline-klasifikasi.png | 2 min |
| 5 | Key result — tabel: F1 SVM 0,5627±0,0045 vs NB 0,5532±0,0052 | Tabel 2 dari naskah-jurnal.md | 2 min |
| 6 | Key result — grafik: SVM konsisten lebih tinggi & stabil | grafik_perbandingan.png | 2 min |
| 7 | Interpretasi: p=0,0039, d=1,9428 (large effect), tapi F1 netral=0,00 | Cuplikan classification_report | 2 min |
| 8 | Limitasi + future work | Bullet list 4 poin | 1,5 min |
| 9 | Kesimpulan + kontribusi | Closing slide | 1 min |

Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|---------------------|---------------|
| Problem  | Kenapa fokus 3 bank ini saja? | [C] Representasi mobile banking konvensional terbesar [E] BCA, Mandiri, BRI = bank dengan nasabah aktif terbanyak (Latar Belakang) [R] Generalisasi ke bank syariah/digital jadi future work eksplisit |
| Gap      | Bukankah Andrian et al. (2022) sudah bandingkan NB vs SVM? | [C] Andrian membandingkan pada domain Twitter, bukan Google Play mobile banking [E] Tabel Related Work menunjukkan domain dan platform berbeda [R] Karakteristik linguistik ulasan app-store berbeda dari tweet, sehingga replikasi terkontrol pada domain ini tetap perlu |
| Method   | Kenapa TF-IDF bukan embedding (Word2Vec/BERT)? | [C] TF-IDF cukup untuk membedakan NB vs SVM secara adil [E] TF-IDF representasi standar di 6 dari 8 paper SLR [R] Riset ini fokus perbandingan algoritma, bukan representasi fitur — perbandingan embedding jadi future work |
| Results  | Kenapa F1-Score kelas netral 0,00? | [C] Bukan bug, tapi konsekuensi class imbalance ekstrem [E] Kelas netral hanya 276/5.758 (4,8%), testing set ±55 sampel [R] Model cenderung prediksi kelas mayoritas tanpa teknik balancing — dilaporkan terbuka sebagai limitasi |
| Generalization | Apakah SVM selalu lebih baik dari NB di semua kasus sentimen teks Indonesia? | [C] Tidak bisa digeneralisasi sejauh itu [E] Hasil spesifik untuk domain mobile banking dengan TF-IDF dan kondisi eksperimen ini [R] Klaim dibatasi sesuai scope penelitian (WS-02) — generalisasi ke domain lain perlu replikasi terpisah |

Latihan:
  Latihan 1: [tanggal diisi saat latihan riil] — [timing: cek apakah 9 slide muat 15 menit; feedback: perjelas transisi slide 6→7]
  Latihan 2: [tanggal diisi saat latihan riil] — [timing & feedback dicatat setelah simulasi ke teman]
  Latihan 3: [tanggal diisi saat latihan riil] — [dicatat setelah sesi tanya-jawab riil]
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|-----------------------|-------|
| 1 | Judul + konteks — perbandingan NB vs SVM klasifikasi sentimen mobile banking Indonesia | Title slide, nama peneliti, logo UPB | 1 min |
| 2 | Problem — jutaan ulasan tidak dianalisis sistematis, algoritma dipilih ad-hoc | Screenshot contoh ulasan Google Play + statistik jumlah ulasan | 2 min |
| 3 | Gap + RQ — 8 paper SLR, belum ada perbandingan NB vs SVM kondisi identik + uji statistik pada domain banking | Tabel ringkas 3 gap (deskriptif, dataset tunggal, domain beda) | 1,5 min |
| 4 | Method — pipeline 5 komponen modular, 10 run, Wilcoxon + Cohen's d | Diagram pipeline-klasifikasi.png | 2 min |
| 5 | Key result (tabel) — F1 SVM 0,5627±0,0045 vs NB 0,5532±0,0052, n=10 | Tabel 2 dari naskah-jurnal.md | 2 min |
| 6 | Key result (grafik) — SVM konsisten lebih tinggi 9/10 run, variabilitas lebih rendah | grafik_perbandingan.png / box plot 10 run | 2 min |
| 7 | Interpretasi — p=0,0039 signifikan, d=1,9428 large effect, tapi F1 kelas netral=0,00 | Cuplikan classification_report highlight kelas netral | 2 min |
| 8 | Limitasi — proxy label rating, tidak ada dedup, class imbalance ekstrem, scope 3 bank konvensional | Bullet list 4 poin | 1,5 min |
| 9 | Kesimpulan — SVM direkomendasikan dengan catatan boundary condition; future work IndoBERT + aspect-based | Closing slide + kontribusi utama | 1 min |

**Total waktu estimasi:** 15 menit
---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|------------|-------|----------|-----------|
| 1 | Problem | Mengapa fokus mobile banking, bukan e-commerce yang lebih ramai ulasannya? | Mobile banking punya karakteristik linguistik dan risiko bisnis berbeda | Ulasan banking sering soal keluhan transaksi/keamanan, bukan produk fisik (disebut di Latar Belakang) | Studi domain non-banking (Ningsih, Khaira) tidak bisa langsung ditransfer ke konteks perbankan — scope dipersempit agar hasil valid untuk konteks spesifik |
| 2 | Method | Mengapa hanya 10 run, bukan 30? | 10 run adalah standar minimum yang cukup untuk uji statistik robust | Wilcoxon p=0,0039 sudah jauh di bawah α=0,05 dengan n=10 | Penambahan run tidak akan mengubah kesimpulan yang sudah signifikan kuat; trade-off waktu komputasi dipertimbangkan (WS-10) |
| 3 | Results | Kenapa selisih F1 cuma 0,0095, apa itu penting? | Selisih absolut kecil tapi konsisten dan reliable | Cohen's d=1,9428 (large effect), SVM unggul di 9/10 run dengan std lebih rendah | Bukan besar selisihnya yang penting, tapi konsistensi keunggulan SVM di seluruh run yang membuatnya bermakna praktis |
| 4 | Method | Kenapa tidak ada langkah cek duplikat ulasan? | Ini keterbatasan nyata pipeline, sudah diakui eksplisit | Tidak ada drop_duplicates() di notebook — diverifikasi di WS-13 | Prioritas riset saat itu di preprocessing teks dan uji statistik; direkomendasikan sebagai perbaikan pipeline ke depan |
| 5 | Generalization | Apakah hasil ini berlaku untuk ulasan bahasa Indonesia di platform lain? | Tidak otomatis — spesifik untuk domain dan platform ini | Karakteristik ulasan Google Play berbeda dari Twitter/App Store (disebutkan di Related Work) | Generalisasi memerlukan replikasi terpisah; scope sengaja dibatasi agar bisa dibuktikan secara rigorous (WS-02) |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|------------|--------------|----------|
| 1 | "Kenapa Cohen's d di beberapa worksheet awal beda dengan laporan akhir?" | "Itu human error waktu mengisi latihan manual di WS-09 sampai WS-12 — saya cek ulang perhitungannya dan koreksi semua worksheet agar konsisten dengan angka final di manuskrip (1,9428), yang saya verifikasi ulang dari data 10-run yang sama." | [✓] Direct [✓] Data-based [✓] Honest |
| 2 | "Apakah preprocessing kamu sudah menangani semua masalah data?" | "Belum sepenuhnya — pipeline saya belum punya langkah deteksi duplikat ulasan. Ini saya akui sebagai limitasi metodologis, bukan sesuatu yang saya sembunyikan." | [✓] Direct [✓] Data-based [✓] Honest |
| 3 | "Kenapa gak pakai deep learning saja, kan lebih canggih?" | "Karena RQ penelitian ini secara spesifik membandingkan NB vs SVM dengan TF-IDF, bukan mencari model terbaik secara umum. Deep learning seperti IndoBERT saya masukkan sebagai future work karena scope dan waktu penelitian ini dibatasi untuk perbandingan dua algoritma klasik." | [✓] Direct [✓] Data-based [✓] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Pertanyaan soal inkonsistensi Cohen's d antar worksheet — karena ini menyangkut kredibilitas proses kerja, bukan cuma hasil akhir. Untungnya proses koreksinya terdokumentasi jelas lewat riwayat commit git ("ws-09 selesai", "ws-11 selesai", "ws-12 selesai"), jadi bisa ditunjukkan sebagai bukti transparansi.

**Apa yang perlu disiapkan lebih baik:**
> Menyiapkan slide cadangan (di luar 9 slide utama) berisi classification_report lengkap per kelas, kalau-kalau penguji menanyakan detail precision/recall kelas netral yang tidak muat di slide utama.
---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Proses verifikasi ulang angka statistik (Cohen's d dan std deviasi) yang ternyata salah di beberapa worksheet mengubah cara pandang bahwa "sudah dihitung sekali" tidak sama dengan "sudah benar" — perlu cross-check sistematis antar dokumen sebelum dianggap final, persis seperti distorsi tak disengaja yang dibahas sejak WS-01.

**Yang akan selalu diterapkan:**
> Selalu melakukan cross-check numerik antar dokumen (worksheet, laporan, manuskrip) sebelum menganggap penelitian selesai, dan tidak berasumsi angka yang sudah tertulis otomatis konsisten di semua tempat.