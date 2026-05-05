# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
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
| Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia, media sosial | SVM akurasi 84% | Bukan Google Play; teks campuran media sosial, bukan ulasan terstruktur |
| Santoso et al. | 2025 | KNN, SVM, RF, NB | 6.000 ulasan BRI & BSI, Google Play 2024 | NB & RF terbaik, akurasi 81% (BRI) | Hanya 2 bank; F1 per kelas tidak jadi primary metric; 6 bulan saja |
| Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF, LR + IndoBERT | 7.000+ ulasan SimobiPlus | SVM 91% akurasi (hyperparameter tuning) | Hanya 1 bank; tidak ada uji statistik signifikansi |
| Universitas Indonesia (Wisnu et al.) | 2021 | Naive Bayes + LDA | 6.194 ulasan mobile banking, Google Play | NB akurasi 86.76%, recall 93.47% | Hanya NB, tidak ada pembanding; hanya 2 kelas (positif/negatif) |
| Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile, Google Play | Akurasi baik, split 80:20 | Hanya NB, tidak ada pembanding SVM; hanya 2 bank syariah |
| Wattimena et al. (JUSTIN) | 2025 | SVM vs NB + TF-IDF | NLP data Indonesia 2020–2023 (bukan banking) | SVM lebih baik: Jawa 76%, Sunda 80% vs NB Jawa 73%, Sunda 77% | Bukan domain banking; bukan Google Play; bukan Bahasa Indonesia standar |
| IJSRA (anonim) | 2025 | NB vs SVM + TF-IDF | E-commerce Indonesia (marketplace) | SVM 89.5% vs NB 84.2% | Domain e-commerce, bukan banking; tidak ada uji statistik |
| Rahman & Irwiensyah | 2024 | NB | 2.000 ulasan BCA Mobile, Google Play Jan 2024 | Akurasi 86.83%, precision 52.78%, recall 46.91% | Hanya NB; tidak ada pembanding; precision rendah tidak dianalisis |

Pola yang ditemukan:
  Metode dominan     : NB dan SVM paling sering digunakan; SVM cenderung lebih unggul pada teks Indonesia (dari studi non-banking)
  Dataset umum       : Google Play Store ulasan mobile banking Indonesia, umumnya 1–7 ribu ulasan per studi; mayoritas menggunakan 1–2 aplikasi saja
  Limitasi berulang  : (1) Studi hanya menggunakan satu algoritma tanpa pembanding; (2) Tidak ada uji statistik signifikansi antar algoritma(3) Evaluasi tidak lengkap — banyak yang hanya laporkan 

GAP IDENTIFICATION

Gap 1: [Jenis: Method Gap + Context Gap ]
  Deskripsi    : Belum ada studi yang secara eksplisit membandingkan NB vs SVM dengan kondisi eksperimen identik (TF-IDF, split, preprocessing sama) pada ulasan mobile banking berbahasa Indonesia di Google Play
  Bukti        : Santoso et al. (2025) membandingkan 4 algoritma tapi tidak fokus NB vs SVM; Edwina & Mauritsius (2024) hanya 1 bank; studi yang fokus NB vs SVM (Wattimena, IJSRA) bukan domain banking
  Signifikansi : Tanpa perbandingan terkontrol, pengembang tidak bisa memilih algoritma dengan keyakinan empiris untuk konteks banking Indonesia

Gap 2: [Jenis: Method Gap ]
  Deskripsi    : Tidak ada studi yang menggunakan uji statistik (Wilcoxon/t-test) untuk membuktikan perbedaan performa NB vs SVM signifikan secara statistik — semua hanya membandingkan angka akurasi secara deskriptif
  Bukti        : Dari 8 paper final, nol yang menyebut p-value atau effect size dalam perbandingan algoritma
  Signifikansi : Perbedaan akurasi 5% bisa jadi noise statistik biasa, bukan perbedaan nyata — tanpa uji statistik, klaim "algoritma X lebih baik" tidak dapat dipertahankan secara ilmiah

Gap 3: [ Data Gap ]
  Deskripsi    : Studi yang ada menggunakan 1–2 aplikasi saja — belum ada yang membandingkan NB vs SVM pada dataset multi-bank (3+ aplikasi besar) agar hasil lebih representatif untuk industri perbankan Indonesia
  Bukti        :  Santoso et al. (2025) hanya BRI & BSI; Edwina (2024) hanya SimobiPlus; Rahman (2024) hanya BCA; tidak ada yang gabungkan 3 bank besar konvensional sekaligus
  Signifikansi : Dataset dari 1–2 bank rentan bias terhadap karakteristik spesifik aplikasi tersebut; multi-bank dataset menghasilkan temuan yang lebih 
  generalizable untuk industri

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Naive Bayes (MultinomialNB + TF-IDF) | Task identik: klasifikasi sentimen teks ulasan banking Indonesia; paling sering digunakan sebagai metode utama | Muncul di 5 dari 8 paper final sebagai metode utama atau pembanding | Santoso et al. (2025); Samudera et al. (2024); Rahman & Irwiensyah (2024) |
| SVM dengan TF-IDF (Edwina & Mauritsius, 2024) | Satu-satunya studi yang menunjukkan SVM 91% pada ulasan mobile banking Indonesia dengan hyperparameter tuning | State-of-local-practice: studi terbaru (2024) pada domain mobile banking Indonesia | Edwina & Mauritsius (2024) |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Perbandingan NB dan SVM untuk Analisis Sentimen Ulasan Mobile Banking Indonesia
**Query pencarian:** ("sentiment analysis") AND ("Naive Bayes" OR "SVM") AND ("mobile banking" OR "banking app") AND ("Google Play" OR "Indonesia")
**Database:** Google Scholar, IEEE Xplore, Scopus, Semantic Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Santoso et al. | 2025 | KNN, SVM, RF, NB | 6.000 ulasan BRI & BSI (Google Play) | NB & RF terbaik; akurasi 81% (BRI) & 78% (BSI) | Hanya 2 bank; F1 bukan metrik utama; periode terbatas |
| 2 | Edwina & Mauritsius | 2024 | SVM, NB, KNN, RF + IndoBERT | 7.000+ ulasan SimobiPlus | SVM akurasi 91% setelah tuning | Hanya 1 bank; tidak ada uji statistik signifikansi |
| 3 | Rahman & Irwiensyah | 2024 | Multinomial NB | 2.000 ulasan BCA Mobile | Akurasi 86.83%; precision 52.78% | Hanya NB; tidak ada pembanding; precision rendah tidak dianalisis |
| 4 | Samudera et al. | 2024 | Multinomial NB | Ulasan BSI Mobile & Action Mobile | Akurasi baik; split data 80:20 | Hanya NB; tidak ada pembanding SVM |
| 5 | Wisnu et al. (UI) | 2021 | NB + LDA | 6.194 ulasan mobile banking (Google Play) | Akurasi 86.76%; recall 93.47% | Hanya NB; hanya 2 kelas sentimen; tidak ada pembanding |
| 6 | Andrian et al. | 2022 | NB, SVM, Decision Tree | Digital banking Indonesia (Media Sosial) | SVM akurasi 84% | Bukan Google Play; data tidak terstruktur |
| 7 | Wattimena et al. | 2025 | SVM vs NB + TF-IDF | NLP Indonesia (Bahasa Jawa & Sunda) | SVM lebih unggul dari NB di kedua bahasa | Bukan perbankan; bukan Bahasa Indonesia standar |
| 8 | IJSRA | 2025 | NB vs SVM + TF-IDF | E-commerce Indonesia | SVM 89.5% vs NB 84.2% | Domain e-commerce; tidak ada uji statistik |


**Pola yang terlihat — Metode dominan:** NB paling sering dipakai sendiri; SVM muncul dalam studi komparatif dan cenderung lebih unggul; tidak ada yang melakukan uji statistik signifikansi
**Limitasi yang berulang:** (1) Hanya 1–2 bank per studi; (2) NB dipakai tanpa pembanding; (3) Tidak ada uji statistik untuk membuktikan perbedaan signifikan
---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [ ✅ ] Ya / [ ] Tidak | Precision NB rendah (52.78%) pada ulasan BCA Mobile (Rahman 2024) namun tidak ada studi yang menguji apakah SVM dapat memperbaiki kelemahan ini secara signifikan pada konteks yang sama |
| Method Gap | [ ✅ ] Ya / [ ] Tidak | Belum ada studi yang menggunakan uji statistik (Wilcoxon/paired t-test) untuk membuktikan perbedaan F1-Score NB vs SVM signifikan — semua perbandingan hanya deskriptif |
| Data Gap | [ ✅ ] Ya / [ ] Tidak | Semua studi menggunakan 1–2 aplikasi banking — belum ada yang menggabungkan 3 bank konvensional besar (BCA, Mandiri, BRI) dalam satu dataset untuk hasil yang lebih representatif |
| Context Gap | [ ✅ ] Ya / [ ] Tidak | Studi NB vs SVM yang ada menggunakan domain e-commerce atau media sosial, bukan ulasan mobile banking terstruktur dari Google Play yang memiliki karakteristik linguistik berbeda |

**Gap utama yang dipilih:** Method Gap + Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Gap ini penting karena dua alasan yang saling memperkuat. Pertama, secara metodologis: perbandingan algoritma tanpa uji statistik tidak dapat dipercaya — perbedaan F1 sebesar 5% antara NB dan SVM bisa jadi hanya noise dari partisi data yang berbeda, bukan bukti keunggulan nyata. Tanpa p-value dan effect size, klaim "SVM lebih baik" hanyalah anekdot, bukan temuan ilmiah. Kedua, secara kontekstual: ulasan mobile banking Indonesia memiliki karakteristik unik — bahasa informal, campur kode, keluhan teknis spesifik perbankan — yang berbeda dari e-commerce atau media sosial, sehingga temuan dari domain lain tidak bisa langsung ditransfer. Kombinasi kedua gap ini berarti pengembang aplikasi banking tidak memiliki panduan berbasis bukti yang rigorous dan kontekstual untuk memilih algoritma klasifikasi sentimen.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Multinomial Naive Bayes + TF-IDF | Task identik: klasifikasi sentimen teks ulasan mobile banking Indonesia berbahasa Indonesia menggunakan TF-IDF | Digunakan di 5 dari 8 paper final — metode paling umum di domain ini, menjadi common practice yang harus dilampaui | Ya, dalam konteks lokal: studi terbaru (2024–2025) masih menggunakannya sebagai metode utama | Santoso et al. (2025); Samudera et al. (2024); Rahman & Irwiensyah (2024) |
| 2 | SVM + TF-IDF dengan hyperparameter tuning (Edwina & Mauritsius, 2024) | Studi terbaru yang menunjukkan performa SVM tertinggi (91%) pada ulasan mobile banking Indonesia — task, domain, dan konteks lokal paling mendekati penelitian ini | State-of-local-practice: satu-satunya studi 2024 yang melaporkan SVM pada mobile banking Indonesia dengan hasil yang signifikan | Ya: studi terbaru (2024) dengan akurasi tertinggi yang dilaporkan untuk domain ini | Edwina & Mauritsius (2024) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ✅ ] Tidak
> Kedua baseline dipilih karena relevansi dan kekuatannya, bukan karena lemah. NB dipilih karena merupakan common practice yang diakui — mengunggulinya membuktikan nilai SVM. SVM Edwina (2024) dipilih karena merupakan hasil terbaik yang ada di domain ini — penelitian ini harus membuktikan apakah keunggulan SVM konsisten di dataset yang lebih luas (3 bank, bukan 1).

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim "belum ada yang meneliti" tanpa bukti adalah pernyataan yang tidak bisa diverifikasi dan mudah dipatahkan oleh satu paper yang terlewat. Research gap yang valid sebaliknya adalah ketidakhadiran yang terdokumentasi: peneliti sudah mencari secara sistematis, menemukan apa yang ada, menganalisis batas-batasnya, dan barulah menyatakan bahwa kombinasi tertentu belum diteliti dengan bukti konkret.

> Dalam penelitian ini, gap bukan sekadar "belum ada yang bandingkan NB vs SVM pada mobile banking Indonesia", melainkan lebih spesifik: belum ada yang melakukan perbandingan dengan kondisi eksperimen yang benar-benar terkontrol (preprocessing, TF-IDF, dan split identik), pada dataset multi-bank (3 aplikasi besar), dan disertai uji statistik signifikansi. Ketiga elemen ini — kontrol eksperimen, cakupan data, dan rigor statistik — yang menjadikan gap ini nyata dan berdampak, bukan sekadar retorika.
