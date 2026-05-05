# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Natural Language Processing & Sistem Informasi Perbankan Digital
  Konteks  : Ulasan pengguna aplikasi mobile banking Indonesia yang dipublikasikan di Google Play Store, ditulis dalam Bahasa Indonesia informal dengan karakteristik linguistik khas (singkatan, campur kode, emoji)

System Context
  Input       : Teks ulasan pengguna aplikasi BCA Mobile, Mandiri Online, dan BRImo dari Google Play Store beserta rating bintang (1–5)
  Process     : Preprocessing teks (case folding, tokenisasi, stopword removal, stemming) → representasi fitur TF-IDF → klasifikasi sentimen menggunakan Naive Bayes dan SVM → evaluasi performa
  Output      : Label sentimen per ulasan (positif/negatif/netral) beserta metrik performa: F1-Score, Akurasi, Precision, Recall untuk masing-masing algoritma
  Outcome     : Pengembang aplikasi mobile banking memiliki panduan berbasis bukti empiris dalam memilih algoritma klasifikasi sentimen yang paling efektif untuk teks ulasan berbahasa Indonesia
  Constraints : Teks ulasan bahasa Indonesia bersifat informal dan tidak baku; tidak semua rating bintang mencerminkan sentimen teks secara akurat; data ulasan yang bisa di-scraping terbatas oleh kebijakan Google Play
  Stakeholders: Pengembang aplikasi mobile banking, tim product & UX bank, peneliti NLP bahasa Indonesia, pengguna aplikasi mobile banking

Fenomena → Problem
  Fenomena yang diamati             : utaan ulasan pengguna aplikasi mobile banking Indonesia tersedia di Google Play Store, namun sebagian besar tidak dianalisis secara sistematis
  Gejala (symptom) yang terukur     : Pengembang memilih algoritma analisis sentimen secara ad-hoc tanpa panduan berbasis bukti untuk konteks teks Bahasa Indonesia pada domain perbankan
  Masalah yang didiagnosis          : Mayoritas studi analisis sentimen menggunakan dataset berbahasa Inggris; studi pada bahasa Indonesia tidak secara konsisten membandingkan NB dan SVM dengan metrik yang lengkap (F1, Precision, Recall)
  Masalah riset (researchable)      : Belum ada studi komparatif yang secara empiris membandingkan Naive Bayes dan SVM menggunakan TF-IDF pada ulasan mobile banking berbahasa Indonesia di Google Play Store dengan metrik evaluasi lengkap
  Variabel yang terukur             : Jenis algoritma (NB vs SVM) sebagai IV; F1-Score macro-average, Akurasi, Precision, Recall sebagai DV

Problem Quality Check
  [✅] Clarity — Satu orang membaca akan paham
  [✅] Measurability — Ada metrik kuantitatif (F1-Score 0–1)
  [✅] Relevance — Penting untuk domain NLP bahasa Indonesia & perbankan digital
  [✅] Testability — Bisa gagal: H₀ gagal ditolak jika tidak ada perbedaan signifikan
  [✅] Impact — Menghasilkan panduan pemilihan algoritma berbasis bukti

Problem Statement (1 paragraf):
Aplikasi mobile banking di Indonesia menghasilkan jutaan ulasan pengguna di Google Play Store yang berpotensi menjadi sumber insight berharga bagi pengembang, namun analisis sentimen terhadap ulasan tersebut belum dilakukan secara sistematis dan berbasis bukti. Studi yang ada umumnya menggunakan dataset berbahasa Inggris atau hanya menerapkan satu algoritma tanpa perbandingan yang rigorous — sehingga tidak diketahui algoritma mana yang paling efektif untuk karakteristik linguistik Bahasa Indonesia yang informal dan kaya campur kode. Belum terdapat studi komparatif yang secara empiris membandingkan Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF pada ulasan mobile banking berbahasa Indonesia di Google Play Store dengan pelaporan metrik yang lengkap (F1-Score, Akurasi, Precision, Recall). Ketiadaan panduan ini menyebabkan pengembang memilih algoritma secara ad-hoc tanpa landasan empiris yang kontekstual. Penelitian ini bertujuan mengisi gap tersebut dengan membandingkan performa Naive Bayes dan SVM secara sistematis pada ulasan aplikasi BCA Mobile, Mandiri Online, dan BRImo dari Google Play Store, guna menghasilkan rekomendasi algoritma berbasis bukti yang dapat langsung diadopsi oleh tim pengembang aplikasi perbankan Indonesia.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Analisis sentimen ulasan aplikasi mobile banking Indonesia di Google Play Store

| Tahap | Hasil |
|-------|-------|
| Reality | Jutaan pengguna aplikasi mobile banking Indonesia (BCA Mobile, Mandiri Online, BRImo) secara aktif memberikan ulasan di Google Play Store yang berisi keluhan, pujian, dan saran terhadap fitur dan layanan aplikasi |
| Observed Issue (Symptom) | Studi Andrian et al. (2022) menunjukkan bahwa analisis sentimen pada ulasan digital banking Indonesia masih menghasilkan akurasi yang bervariasi antar metode, namun tidak semua studi melaporkan F1-Score sebagai metrik utama — menyulitkan perbandingan yang adil |
| Diagnosed Problem (Root Cause) | Tidak ada konsensus tentang algoritma klasifikasi sentimen terbaik untuk teks ulasan berbahasa Indonesia pada domain mobile banking — setiap studi menggunakan dataset, metrik, dan preprocessing yang berbeda sehingga hasil tidak bisa langsung dibandingkan |
| Researchable Problem | Belum terdapat studi yang secara sistematis dan dengan kondisi eksperimen yang identik membandingkan Naive Bayes dan SVM menggunakan TF-IDF pada ulasan mobile banking berbahasa Indonesia di Google Play Store |
| Measurable Variable | IV: jenis algoritma (NB vs SVM). DV: F1-Score macro-average (primary), Akurasi, Precision, Recall (secondary). CV: representasi TF-IDF, split 80:20, preprocessing identik |

**Apakah terjebak solution-first thinking?** [ ] Ya / [✅] Tidak
> Penelitian dimulai dari gap pengetahuan — "belum ada perbandingan sistematis NB vs SVM pada konteks ini" — bukan dari asumsi bahwa SVM pasti lebih baik. Pertanyaan risetnya terbuka: hasilnya bisa mendukung NB, SVM, atau menunjukkan tidak ada perbedaan signifikan.
---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Teks ulasan pengguna aplikasi BCA Mobile, Mandiri Online, BRImo dari Google Play Store (±2.000 ulasan per aplikasi, bahasa Indonesia, periode 2022–2024) beserta rating bintang 1–5 sebagai proxy label sentimen |
| Process | Scraping data via google-play-scraper → preprocessing (lowercase, hapus simbol/angka/emoji, stopword removal Bahasa Indonesia, stemming Sastrawi) → labeling otomatis berdasarkan rating (1–2★=negatif, 3★=netral, 4–5★=positif) → ekstraksi fitur TF-IDF (max_features=5.000) → split 80:20 → training dan evaluasi NB dan SVM secara terpisah |
| Output | Label sentimen per ulasan (positif/negatif/netral), classification report per algoritma (F1-Score, Akurasi, Precision, Recall), tabel perbandingan hasil kedua algoritma dalam format CSV |
| Outcome | Rekomendasi algoritma berbasis bukti empiris untuk tim pengembang mobile banking Indonesia dalam mengimplementasikan sistem analisis sentimen ulasan pengguna |
| Constraints | (1) Teks bahasa Indonesia informal mengandung singkatan tidak baku dan campur kode yang mempersulit preprocessing; (2) Rating bintang sebagai proxy label tidak selalu akurat merepresentasikan sentimen teks; (3) Google Play membatasi jumlah ulasan yang bisa di-scraping via API; (4) Distribusi kelas sentimen cenderung tidak seimbang |
| Stakeholders | Pengembang aplikasi mobile banking, tim product & UX bank, peneliti NLP bahasa Indonesia, pengguna aplikasi mobile banking Indonesia |

**Komponen mana yang paling relevan dengan masalah riset?** Process dan Constraints. Process adalah inti karena di sinilah perbedaan antara NB dan SVM beroperasi — semua tahap sebelum classifier harus identik agar perbandingan fair. Constraints juga kritis karena karakteristik teks bahasa Indonesia informal dan proxy labeling dari rating bintang adalah sumber utama noise yang harus diakui sebagai limitasi.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Masalah sangat spesifik: dua algoritma yang dibandingkan, representasi fitur, domain, platform, dan bahasa disebutkan eksplisit |
| Measurability | 5 | F1-Score macro-average sebagai primary metric dengan skala 0–1; semua metrik dihitung otomatis oleh sklearn — tidak ada ambiguitas pengukuran |
| Relevance | 4 | Relevan untuk domain NLP bahasa Indonesia dan pengembangan produk perbankan digital; bisa lebih kuat jika dikaitkan ke standar evaluasi NLP internasional seperti SemEval |
| Testability | 5 | H₀ falsifiable — "tidak ada perbedaan signifikan F1-Score antara NB dan SVM" dapat ditolak atau gagal ditolak berdasarkan uji Wilcoxon p < 0.05 |
| Impact | 4 | Menghasilkan panduan pemilihan algoritma berbasis bukti; bisa lebih kuat jika hasilnya dikaitkan ke estimasi biaya komputasi deployment |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Aplikasi mobile banking di Indonesia menghasilkan jutaan ulasan pengguna di Google Play Store yang berpotensi menjadi sumber insight berharga bagi pengembang, namun hingga saat ini belum terdapat panduan berbasis bukti empiris mengenai algoritma klasifikasi sentimen yang paling efektif untuk teks ulasan berbahasa Indonesia pada domain perbankan. Studi-studi yang ada umumnya hanya menerapkan satu algoritma tanpa pembanding yang terkontrol, atau melakukan perbandingan pada domain lain seperti e-commerce dan media sosial yang memiliki karakteristik linguistik berbeda dari ulasan banking — sehingga hasilnya tidak dapat langsung ditransfer. Belum terdapat studi yang secara sistematis membandingkan Naive Bayes dan Support Vector Machine (SVM) menggunakan representasi TF-IDF dengan kondisi eksperimen identik pada dataset multi-bank (BCA Mobile, Mandiri Online, BRImo) dari Google Play Store, sekaligus membuktikan signifikansi perbedaannya secara statistik. Ketiadaan panduan ini menyebabkan pengembang memilih algoritma secara ad-hoc tanpa landasan empiris yang kontekstual, berpotensi menghasilkan sistem analisis sentimen yang tidak optimal. Penelitian ini bertujuan mengisi gap tersebut dengan membandingkan F1-Score, Akurasi, Precision, dan Recall antara Naive Bayes dan SVM menggunakan TF-IDF pada ±6.000 ulasan berbahasa Indonesia dari tiga aplikasi mobile banking terbesar di Indonesia, guna menghasilkan rekomendasi algoritma berbasis bukti yang dapat langsung diadopsi oleh tim pengembang aplikasi perbankan Indonesia.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah dalam coding bersifat konkret dan langsung — ada error, ada baris yang salah, ada output yang tidak sesuai ekspektasi. Pendekatannya pun langsung: debug, perbaiki, jalankan ulang. Tidak perlu dibuktikan ke orang lain dan tidak perlu bisa direplikasi.

Masalah riset sebaliknya berangkat dari ketidaktahuan yang sistematis — sesuatu yang belum terbukti secara empiris dalam konteks tertentu. Dalam penelitian ini, masalahnya bukan "bagaimana membuat kode klasifikasi sentimen jalan", melainkan "algoritma mana yang terbukti lebih efektif untuk konteks spesifik ini, dan seberapa besar perbedaannya secara statistik?" Jawabannya harus falsifiable, reproducible, dan menghasilkan kontribusi pengetahuan yang bisa dikritisi dan diverifikasi oleh peneliti lain.
