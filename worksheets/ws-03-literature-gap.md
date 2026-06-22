# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Perbandingan Naive Bayes dan SVM untuk Analisis Sentimen Ulasan Aplikasi Mobile Banking Indonesia di Google Play Store
Database   : IEEE Xplore, Scopus, ACM Digital Library, Google Scholar
Query      : ("sentiment analysis" OR "opinion mining") AND ("Naive Bayes" OR "Support Vector Machine" OR "SVM") AND ("mobile banking" OR "banking application" OR "fintech") AND ("Google Play" OR "app review") AND ("Indonesia" OR "Indonesian text" OR "Bahasa Indonesia")
Tahun      : 2020–2025
Hasil awal : 89 paper → Screening judul+abstrak → 27 paper → Full-text → 8 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Dataset | Result | Limitation |
|-------|-------|--------|---------|--------|------------|
| Java et al. | 2024 | Multinomial NB vs SVM | Ulasan Threads Google Play Indonesia | NB dan SVM dibandingkan | Bukan banking; bukan multi-bank |
| Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF | 7.000+ ulasan SimobiPlus | SVM 91% akurasi setelah tuning | Hanya 1 bank; tidak ada uji statistik |
| Al Hakim & Irwiensyah | 2024 | Multinomial NB | 2.000 ulasan BCA Mobile | Akurasi 86,83%, precision 52,78% | Hanya NB; tidak ada pembanding |
| Munandar et al. | 2024 | KNN | Ulasan mobile banking Indonesia | Akurasi baik | Hanya KNN; tidak ada NB vs SVM |
| Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile | Akurasi baik, split 80:20 | Hanya NB; tidak ada pembanding SVM |
| Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia, Twitter | SVM F1-Score 73,34% | Bukan Google Play; bukan ulasan terstruktur |
| Ningsih et al. | 2024 | SVM vs NB + TF-IDF | Twitter mobil listrik Indonesia | SVM > NB di semua metrik | Bukan banking; bukan Google Play |
| Khaira et al. | 2023 | NB vs SVM + TF-IDF | Twitter kebijakan Kemdikbudristek | SVM lebih baik dari NB | Domain kebijakan; bukan banking; tidak ada uji statistik |

Pola yang ditemukan:
  Metode dominan     : NB paling sering dipakai sendiri; SVM muncul dalam studi komparatif dan cenderung lebih unggul; tidak ada yang melakukan uji statistik signifikansi
  Dataset umum       : Google Play Store ulasan banking Indonesia umumnya 1–2 aplikasi saja
  Limitasi berulang  : (1) Hanya 1–2 bank per studi; (2) NB dipakai tanpa pembanding; (3) Tidak ada uji statistik untuk membuktikan perbedaan signifikan

GAP IDENTIFICATION

Gap 1: [Jenis: Method Gap + Context Gap ]
  Deskripsi    : Belum ada studi yang secara eksplisit membandingkan NB vs SVM dengan kondisi eksperimen identik (TF-IDF, split, preprocessing sama) pada ulasan mobile banking berbahasa Indonesia di Google Play
  Bukti        : Java et al. (2024) membandingkan NB vs SVM tapi bukan domain banking; Edwina & Mauritsius (2024) hanya 1 bank; studi yang fokus NB vs SVM (Ningsih et al., 2024; Khaira et al., 2023) bukan domain banking
  Signifikansi : Tanpa perbandingan terkontrol, pengembang tidak bisa memilih algoritma dengan keyakinan empiris untuk konteks banking Indonesia

Gap 2: [Jenis: Method Gap ]
  Deskripsi    : Tidak ada studi yang menggunakan uji statistik (Wilcoxon/t-test) untuk membuktikan perbedaan performa NB vs SVM signifikan secara statistik — semua hanya membandingkan angka akurasi secara deskriptif
  Bukti        : Dari 8 paper final, nol yang menyebut p-value atau effect size dalam perbandingan algoritma
  Signifikansi : Perbedaan akurasi 5% bisa jadi noise statistik biasa, bukan perbedaan nyata — tanpa uji statistik, klaim "algoritma X lebih baik" tidak dapat dipertahankan secara ilmiah

Gap 3: [ Data Gap ]
  Deskripsi    : Studi yang ada menggunakan 1–2 aplikasi saja — belum ada yang membandingkan NB vs SVM pada dataset multi-bank (3+ aplikasi besar) agar hasil lebih representatif untuk industri perbankan Indonesia
  Bukti        :  Edwina (2024) hanya SimobiPlus; Al Hakim (2024) hanya BCA; Samudera (2024) hanya BSI — tidak ada yang gabungkan 3 bank besar konvensional sekaligus
  Signifikansi : Dataset dari 1–2 bank rentan bias terhadap karakteristik spesifik aplikasi tersebut; multi-bank dataset menghasilkan temuan yang lebih generalizable untuk industri

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Naive Bayes (MultinomialNB + TF-IDF) | Task identik: klasifikasi sentimen teks ulasan banking Indonesia; paling sering digunakan sebagai metode utama | Muncul di 4 dari 8 paper final sebagai metode utama atau pembanding | Samudera et al. (2024); Al Hakim & Irwiensyah (2024) |
| SVM dengan TF-IDF (Edwina & Mauritsius, 2024) | Studi terbaru SVM pada ulasan mobile banking Indonesia dengan hasil tertinggi (91%) | State-of-local-practice: studi terbaru (2024) pada domain mobile banking Indonesia | Edwina & Mauritsius (2024) |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Perbandingan NB dan SVM untuk Analisis Sentimen Ulasan Mobile Banking Indonesia
**Query pencarian:** ("sentiment analysis") AND ("Naive Bayes" OR "SVM") AND ("mobile banking" OR "banking app") AND ("Google Play" OR "Indonesia")
**Database:** Google Scholar, IEEE Xplore, Scopus, Semantic Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Java et al. | 2024 | Multinomial NB vs SVM | Ulasan Threads Google Play Indonesia | NB dan SVM dibandingkan, akurasi baik | Bukan domain banking; bukan multi-bank |
| 2 | Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF | 7.000+ ulasan SimobiPlus | SVM akurasi 91% setelah tuning | Hanya 1 bank; tidak ada uji statistik signifikansi |
| 3 | Al Hakim & Irwiensyah | 2024 | Multinomial NB | 2.000 ulasan BCA Mobile | Akurasi 86.83%; precision 52.78% | Hanya NB; tidak ada pembanding; precision rendah tidak dianalisis |
| 4 | Munandar et al. | 2024 | KNN | Ulasan mobile banking Indonesia | Akurasi baik | Hanya KNN; tidak ada perbandingan NB vs SVM |
| 5 | Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile | Akurasi baik, split 80:20 | Hanya NB; tidak ada pembanding SVM |
| 6 | Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia, Twitter | SVM F1-Score 73,34% | Bukan Google Play; bukan ulasan terstruktur |
| 7 | Ningsih et al. | 2024 | SVM vs NB + TF-IDF | Twitter mobil listrik Indonesia | SVM > NB di semua metrik | Bukan banking; bukan Google Play |
| 8 | Khaira et al. | 2023 | NB vs SVM + TF-IDF | Twitter kebijakan Kemdikbudristek | SVM lebih baik dari NB | Domain kebijakan; tidak ada uji statistik | 


**Pola yang terlihat — Metode dominan:** NB paling sering dipakai sendiri tanpa pembanding; SVM muncul dalam studi komparatif dan cenderung lebih unggul; tidak ada yang melakukan uji statistik signifikansi
**Limitasi yang berulang:** (1) Hanya 1–2 bank per studi; (2) NB dipakai tanpa pembanding; (3) Tidak ada uji statistik untuk membuktikan perbedaan signifikan
---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [ ✅ ] Ya / [ ] Tidak | Precision NB rendah (52.78%) pada ulasan BCA Mobile (Rahman 2024) namun tidak ada studi yang menguji apakah SVM dapat memperbaiki kelemahan ini secara signifikan pada konteks yang sama |
| Method Gap | [ ✅ ] Ya / [ ] Tidak | Belum ada studi yang menggunakan uji statistik (Wilcoxon/paired t-test) untuk membuktikan perbedaan F1-Score NB vs SVM signifikan — semua perbandingan hanya deskriptif |
| Data Gap | [ ✅ ] Ya / [ ] Tidak | Semua studi menggunakan 1–2 aplikasi banking — belum ada yang menggabungkan 3 bank konvensional besar (BCA, Mandiri, BRI) dalam satu dataset untuk hasil yang lebih representatif |
| Context Gap | [ ✅ ] Ya / [ ] Tidak | Studi NB vs SVM yang ada menggunakan domain non-banking (Twitter, e-commerce), bukan ulasan mobile banking terstruktur dari Google Play Store |

**Gap utama yang dipilih:** Method Gap + Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Gap ini penting karena dua alasan yang saling memperkuat. Pertama, secara metodologis: perbandingan algoritma tanpa uji statistik tidak dapat dipercaya — perbedaan F1 sebesar 5% antara NB dan SVM bisa jadi hanya noise dari partisi data yang berbeda, bukan bukti keunggulan nyata. Tanpa p-value dan effect size, klaim "SVM lebih baik" hanyalah anekdot, bukan temuan ilmiah. Kedua, secara kontekstual: ulasan mobile banking Indonesia memiliki karakteristik unik — bahasa informal, campur kode, keluhan teknis spesifik perbankan — yang berbeda dari e-commerce atau media sosial, sehingga temuan dari domain lain tidak bisa langsung ditransfer. Kombinasi kedua gap ini berarti pengembang aplikasi banking tidak memiliki panduan berbasis bukti yang rigorous dan kontekstual untuk memilih algoritma klasifikasi sentimen.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Multinomial Naive Bayes + TF-IDF | Task identik: klasifikasi sentimen teks ulasan mobile banking Indonesia berbahasa Indonesia menggunakan TF-IDF | Digunakan di 4 dari 8 paper final — metode paling umum di domain ini | Ya, dalam konteks lokal: studi terbaru 2024 masih menggunakannya sebagai metode utama | Samudera et al. (2024); Al Hakim & Irwiensyah (2024) |
| 2 | SVM + TF-IDF (Edwina & Mauritsius, 2024) | Studi terbaru yang menunjukkan performa SVM tertinggi (91%) pada ulasan mobile banking Indonesia | State-of-local-practice: studi 2024 paling relevan di domain ini | Ya: studi terbaru dengan akurasi tertinggi untuk domain ini | Edwina & Mauritsius (2024) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ✅ ] Tidak
> Kedua baseline dipilih karena relevansi dan kekuatannya, bukan karena lemah. NB dipilih karena merupakan common practice yang diakui — mengunggulinya membuktikan nilai SVM. SVM Edwina (2024) dipilih karena merupakan hasil terbaik yang ada di domain ini — penelitian ini harus membuktikan apakah keunggulan SVM konsisten di dataset yang lebih luas (3 bank, bukan 1).

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim "belum ada yang meneliti" tanpa bukti adalah pernyataan yang tidak bisa diverifikasi dan mudah dipatahkan oleh satu paper yang terlewat. Research gap yang valid sebaliknya adalah ketidakhadiran yang terdokumentasi: peneliti sudah mencari secara sistematis, menemukan apa yang ada, menganalisis batas-batasnya, dan barulah menyatakan bahwa kombinasi tertentu belum diteliti dengan bukti konkret.

> Dalam penelitian ini, gap bukan sekadar "belum ada yang bandingkan NB vs SVM pada mobile banking Indonesia", melainkan lebih spesifik: belum ada yang melakukan perbandingan dengan kondisi eksperimen yang benar-benar terkontrol (preprocessing, TF-IDF, dan split identik), pada dataset multi-bank (3 aplikasi besar), dan disertai uji statistik signifikansi. Ketiga elemen ini — kontrol eksperimen, cakupan data, dan rigor statistik — yang menjadikan gap ini nyata dan berdampak, bukan sekadar retorika.
