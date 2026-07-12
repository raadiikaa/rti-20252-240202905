# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Perbandingan Naive Bayes dan Support Vector Machine Berbasis TF-IDF untuk Klasifikasi Sentimen Ulasan Mobile Banking Indonesia di Google Play Store
Target  : [✅] Jurnal - (Target: TIIJ — Technology and Informatics Insight Journal, Sinta 5) [ ] Konferensi  [ ] Laporan

Section Check:
  [✅] Abstract — masalah (belum ada panduan algoritma), metode (NB vs SVM,
       TF-IDF, 10 run), hasil utama (F1 SVM 0,5627 vs NB 0,5532, p=0,0039,
       d=1,9428), kontribusi (rekomendasi SVM) — ±150 kata
  [✅] Introduction — konteks (pertumbuhan mobile banking) → gap (SLR 8 paper,
       3 keterbatasan) → RQ (SVM vs NB F1-Score) → kontribusi tersirat
  [✅] Related Work — concept-centric (NB tanpa pembanding vs SVM lebih
       unggul vs TF-IDF tanpa uji statistik), gap positioning jelas
  [✅] Method — reproducible: desain (kuantitatif eksperimental), variabel
       (IV/DV/CV), metrik (F1 macro-average), setup (pipeline 5 komponen),
       prosedur (10 run, Wilcoxon, Cohen's d)
  [✅] Results — Tabel 1 (run tunggal), Tabel 2 (10 run), Tabel 3 (statistik),
       grafik — dilaporkan objektif tanpa interpretasi berlebihan
  [✅] Discussion — interpretasi keunggulan SVM, perbandingan literatur,
       class imbalance, effect size — menyatu dengan Results di naskah asli
  [✅] Conclusion — jawaban RQ, kontribusi (studi pertama dgn 3 elemen
       lengkap), future work (IndoBERT, aspect-based sentiment analysis)

Consistency Matrix:
  [~] RQ di Introduction = RQ di Method = RQ di Conclusion
       (RQ konsisten disebut, tapi H₀/H₁ formal baru muncul di Method,
       belum di-preview di Introduction — lihat Latihan 2)
  [✅] Variabel di Method = variabel di Results
       (IV: algoritma; DV: F1-Score macro-average, akurasi, precision, recall)
  [✅] Klaim di Discussion didukung data di Results
       (semua klaim p=0,0039, d=1,9428 merujuk balik ke Tabel 2 dan 3)
  [~] Limitasi di Discussion di-address di Conclusion/Future Work
       (limitasi class imbalance & proxy label sudah di-address; limitasi
       dedup BELUM disebut di naskah — lihat Latihan 2)

Writing Quality:
  [✅] Clarity — mudah dipahami tanpa re-read
  [✅] Precision — istilah statistik disertai angka eksak (p, d, CI)
  [✅] Conciseness — tidak ada kalimat filler berlebihan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|----------------------------|-------------|
| Abstract | Belum ada panduan berbasis bukti untuk memilih algoritma klasifikasi sentimen ulasan mobile banking Indonesia. Studi ini membandingkan NB vs SVM dengan TF-IDF pada 6.000 ulasan, 10 run, diverifikasi Wilcoxon dan Cohen's d. Hasil: SVM unggul signifikan (F1=0,5627 vs 0,5532, p=0,0039, d=1,9428) dan direkomendasikan. | 200-250 |
| Introduction | Konteks: jutaan ulasan mobile banking Indonesia belum dianalisis sistematis. Gap: dari 8 paper SLR, tidak ada yang membandingkan NB vs SVM kondisi identik + uji statistik pada domain banking. RQ: apakah SVM menghasilkan F1-Score lebih tinggi dari NB? | 500-700 |
| Related Work | Studi NB tanpa pembanding (Al Hakim & Irwiensyah, Samudera, Soliha) menghasilkan akurasi tinggi tapi precision rendah. Studi yang menyertakan SVM (Edwina & Mauritsius, Andrian et al.) menunjukkan hasil lebih menjanjikan tapi tanpa uji statistik. Konsep dasar NB dan SVM dijelaskan, dengan Cortes & Vapnik (1995) sebagai rujukan teori hyperplane. | 700-1000 |
| Method | Desain kuantitatif eksperimental komparatif dengan paradigma Design Science Research; H₀/H₁ dirumuskan eksplisit. Variabel IV (algoritma), DV (F1-Score macro-average primer), CV (TF-IDF, split, preprocessing) dioperasionalkan. Pipeline 5 komponen modular dijalankan 10 run, dianalisis Wilcoxon + Cohen's d. | 800-1200 |
| Results | Tabel 1 (run tunggal): F1 NB=0,5466, SVM=0,5553. Tabel 2 (10 run): F1 NB=0,5532±0,0052, SVM=0,5627±0,0045, SVM unggul 9/10 run. Tabel 3: p=0,0039, Cohen's d=1,9428 (large effect). | 500-800 |
| Discussion | Keunggulan SVM dijelaskan lewat kemampuan hyperplane optimal di ruang TF-IDF berdimensi tinggi. F1-Score moderat mencerminkan class imbalance (positif 69,7% vs netral 4,6%); akurasi tinggi vs F1 moderat memvalidasi pemilihan metrik. Effect size besar membuktikan perbedaan bermakna praktis, bukan noise. | 600-900 |
| Conclusion | SVM terbukti signifikan lebih baik dari NB (p=0,0039, d=1,9428) dan direkomendasikan untuk klasifikasi sentimen ulasan mobile banking Indonesia. Kontribusi: studi pertama dengan kondisi eksperimen identik + dataset multi-bank + verifikasi statistik. Future work: IndoBERT, perluasan ke bank syariah/digital, aspect-based sentiment analysis. | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

| | Intro | Method | Result | Discussion | Conclusion |
|---|---|---|---|---|---|
| RQ1 (SVM vs NB F1-Score) | ✓ | ✓ | ✓ | ✓ | ✓ |
| RQ2 | (tidak ada — studi ini hanya memiliki 1 RQ tunggal, comparison study) | | | | |
| Metrik utama (F1-Score macro-average) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel IV (jenis algoritma) | ✗ | ✓ | ✓ (implisit di Tabel 2) | ✓ | ✓ |
| Variabel DV (F1, akurasi, precision, recall) | ✗ | ✓ | ✓ | ~ (hanya F1 dan akurasi dibahas, precision/recall tidak disinggung di Discussion) | ✗ |
| Klaim/kontribusi (studi pertama 3 elemen lengkap) | ✗ ← | ✗ | ✗ | ✗ | ✓ |
| Limitasi dedup (dari WS-13) | ✗ | ✗ ← | ✗ | ✗ | ✗ ← |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing — wajar di section itu), ✗ ← (missing yang seharusnya ada), ~ (ada tapi tidak lengkap)

**Inkonsistensi yang ditemukan:**
> 1. Klaim kontribusi "studi pertama dengan 3 elemen lengkap" hanya muncul di Conclusion, tidak di-preview sama sekali di Introduction — padahal ini klaim kontribusi utama yang seharusnya sudah disinggung di akhir Introduction sebagai janji ke pembaca.
2. Limitasi dedup (ketiadaan langkah cek duplikat, dari WS-13) sama sekali tidak muncul di Method, Discussion, maupun Conclusion — ini gap paling signifikan karena sudah teridentifikasi sejak WS-13 tapi belum pernah masuk ke naskah jurnal.
3. Precision dan Recall (DV sekunder) disebut di Method tapi tidak dibahas lagi di Discussion — hanya F1-Score dan akurasi yang dibahas, sehingga variabel yang "dijanjikan" di Method sebagian tidak "ditepati" di Discussion.

**Tindakan perbaikan:**
> 1. Tambahkan 1 kalimat di akhir Introduction: "Penelitian ini menjadi studi pertama yang memenuhi kondisi eksperimen identik, dataset multi-bank, dan verifikasi statistik secara bersamaan pada domain ini."
2. Tambahkan 1 kalimat di akhir bagian Method (setelah paragraf Preprocessing): "Pipeline preprocessing pada penelitian ini belum menyertakan langkah deteksi duplikat ulasan; keterbatasan ini dibahas lebih lanjut pada bagian Simpulan." — lalu tambahkan poin sejajar di Simpulan.
3. Tambahkan 1-2 kalimat di Discussion yang menyinggung precision/recall secara singkat, atau jika memang tidak krusial untuk argumen utama, cukup jelaskan alasannya di Method kenapa precision/recall hanya dilaporkan sebagai data pendukung di tabel tanpa dibahas mendalam.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:** (dari bagian Pembahasan naskah-jurnal.md)
> Nilai F1-Score yang moderat mencerminkan tantangan distribusi kelas yang tidak seimbang — positif 69,7% berbanding netral 4,6%. Nilai akurasi yang relatif tinggi dibandingkan F1-Score mengkonfirmasi bias akibat class imbalance, memvalidasi pemilihan F1-Score macro-average sebagai metrik primer.

| Kriteria | Evaluasi | Perbaikan |
|----------|----------|-----------|
| Clarity | "Nilai F1-Score yang moderat" tidak menyebut angka konkret — pembaca harus scroll balik ke Tabel 2 untuk tahu nilainya | Sisipkan angka langsung: "F1-Score moderat (0,5532 untuk NB, 0,5627 untuk SVM)..." |
| Precision | "Bias akibat class imbalance" agak generik — tidak dikaitkan ke temuan spesifik (F1 kelas netral = 0,00) yang justru bukti paling kuat dari bias tersebut | Tambahkan detail: "...ditunjukkan secara ekstrem oleh F1-Score kelas netral yang mendekati 0 pada kedua algoritma, akibat representasi kelas hanya 4,6% dari data" |
| Conciseness | Sudah cukup ringkas — tidak ada kalimat filler atau kata berulang yang bisa dihapus | Tidak ada perubahan diperlukan pada aspek ini |

**Paragraf setelah perbaikan:**
> Nilai F1-Score yang moderat (0,5532 untuk Naive Bayes dan 0,5627 untuk SVM) mencerminkan tantangan distribusi kelas yang sangat tidak seimbang — positif 69,7% berbanding netral hanya 4,6%. Bias ini ditunjukkan secara ekstrem oleh F1-Score kelas netral yang mendekati nol pada kedua algoritma, akibat representasi kelas yang sangat kecil pada data training maupun testing. Nilai akurasi yang relatif lebih tinggi dibandingkan F1-Score mengkonfirmasi bias akibat class imbalance ini, sekaligus memvalidasi pemilihan F1-Score macro-average sebagai metrik primer alih-alih akurasi.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis "tentang" riset berarti menyusun laporan kronologis — apa yang dilakukan lebih dulu, apa yang dilakukan berikutnya, seperti buku harian proses kerja. Menulis sebagai "argumen" berarti setiap kalimat punya fungsi meyakinkan pembaca terhadap satu klaim utama: SVM lebih unggul dari NB, dan klaim itu bisa dipercaya secara statistik maupun praktis. Perbedaan ini terasa jelas saat menyusun naskah-jurnal.md — draft kronologis akan terasa seperti "pertama saya scraping, lalu preprocessing, lalu training..." Padahal urutan yang lebih meyakinkan adalah: masalah (belum ada panduan algoritma) → gap (belum ada perbandingan terkontrol) → bukti (p=0,0039, d=1,9428) → implikasi (SVM direkomendasikan, dengan catatan boundary condition di kelas netral dari WS-14).

> Urutan penulisan Method → Discussion → Introduction (bukan Introduction dulu) juga terasa manfaatnya secara langsung: karena Method dan Results ditulis berdasarkan apa yang benar-benar dikerjakan di notebook (bukan rencana ideal di proposal), Introduction yang ditulis belakangan bisa langsung di-frame sesuai temuan aktual — termasuk klaim kontribusi "studi pertama dengan 3 elemen lengkap" yang baru bisa dituliskan dengan percaya diri setelah tahu hasil analisisnya benar-benar signifikan, bukan sekadar janji di awal yang belum tentu terbukti.