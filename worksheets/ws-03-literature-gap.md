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

Topik      : Deteksi Anomali Jaringan pada Aplikasi Mobile Banking Indonesia Menggunakan Machine Learning
Database   : IEEE Xplore, Scopus, ACM Digital Library, Google Scholar
Query      : ("mobile banking" OR "mbanking") AND ("network anomaly detection" OR "intrusion detection" OR "MITM detection") AND ("machine learning" OR "deep learning" OR "anomaly detection") AND ("Indonesia" OR "developing countries") AND ("network traffic" OR "TLS" OR "API security")
Tahun      : 2019–2024
Hasil awal : 134 paper → Screening (judul + abstrak) → 41 paper → Full-text review → 18 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Apruzzese et al. | 2022 | Random Forest + TLS traffic fingerprint | CICIDS-2018 (sintetis, lab) | F1-score 94.2% deteksi MITM | Dataset sintetis; tidak diuji pada mobile banking nyata |
| Suryani & Wibowo | 2023 | LSTM Autoencoder pada API call sequence | 1 bank Indonesia (privat, jaringan kampus) | AUC-ROC 0.91 | Dataset privat; 1 institusi; tidak ada WiFi publik |
| Zhang et al. | 2022 | GNN pada pola koneksi jaringan mobile | UNSW-NB15 + simulasi Android | Precision 89%, Recall 91% | Overhead tinggi; bukan konteks banking |
| Iqbal et al. | 2021 | Isolation Forest + SHAP | 12 app perbankan Asia Selatan | Akurasi 87.3% (turun ke 71.2% di RAM < 3 GB) | Tidak ada aplikasi Indonesia; FPR tidak diukur |
| Firmansyah et al. | 2023 | CNN-1D pada fitur statistik paket | 5 bank Indonesia, WiFi kampus (N=4.200) | Akurasi 88% | Dataset kecil; jaringan terkontrol; tidak ada WiFi publik komersial |
| Meng et al. | 2020 | Hybrid SVM + Autoencoder | 8 app mobile banking Asia Tenggara | Recall 92% SSL stripping; Precision 84% | Tidak ada aplikasi Indonesia; tidak ada evaluasi OWASP/regulasi |
| Hussain et al. | 2021 | XGBoost + Bayesian tuning | CTU-13 + custom simulasi lab | AUC 0.96; F1 turun ke 0.79 di real traffic | Gap lab vs real-world; tidak ada analisis latensi |
| Purnama & Hidayat | 2024 | Transformer (DistilBERT) pada API request sequence | Log fintech Indonesia anonim | Precision 91% deteksi anomali session | Model terlalu berat (1.2 GB); tidak bisa di-deploy edge |

Pola yang ditemukan:
  Metode dominan     : Supervised (RF, XGBoost) dan Hybrid/Unsupervised (Autoencoder, Isolation Forest) — transformer baru muncul di 2024 tapi terlalu berat untuk deployment
  Dataset umum       : CICIDS-2018, UNSW-NB15 (sintetis/lab) — mayoritas tidak menggunakan data mobile banking Indonesia yang nyata
  Limitasi berulang  : (1) Dataset dari lab/jaringan kampus, bukan WiFi publik komersial; (2) Tidak ada evaluasi di perangkat low-spec; (3) Tidak ada korelasi ke regulasi OJK atau OWASP MASVS

GAP IDENTIFICATION

Gap 1: [Jenis: Context Gap + Data Gap ]
  Deskripsi    : Tidak ada studi yang mengevaluasi sistem deteksi anomali ML pada traffic mobile banking spesifik Indonesia dengan dataset dari jaringan WiFi publik komersial (mall, kafe, transportasi umum)
  Bukti        : Suryani & Wibowo (2023) hanya 1 bank, jaringan kampus. Firmansyah et al. (2023) juga lingkungan kampus terkontrol. Meng et al. (2020) tidak mencakup aplikasi Indonesia
  Signifikansi : Karakteristik traffic WiFi publik Indonesia berbeda — heterogenitas ISP, noise pattern, pola penggunaan — yang mempengaruhi distribusi fitur input model ML

Gap 2: [Jenis: Method Gap + Performance Gap ]
  Deskripsi    : Tidak ada studi komparatif yang membandingkan lightweight ML models (Isolation Forest, LSTM-AE kecil) vs heavy models (GNN, Transformer) secara eksplisit dari sisi akurasi-latensi trade-off pada perangkat Android low-spec (RAM ≤ 3 GB)
  Bukti        : Iqbal et al. (2021) mencatat penurunan akurasi dari 87.3% ke 71.2% tapi tidak mengidentifikasi model alternatif yang lebih efisien. Purnama & Hidayat (2024) mengakui model tidak deployable di edge
  Signifikansi : Indonesia memiliki penetrasi Android low-spec sangat tinggi; sistem deteksi yang tidak berjalan di perangkat user tidak memberikan proteksi real-time

Gap 3: [ Context Gap ]
  Deskripsi    : Tidak ada studi yang mengevaluasi sistem deteksi anomali ML dalam konteks kepatuhan regulasi OJK POJK 21/2022 dan OWASP MASVS
  Bukti        : Dari 8 paper final, nol yang menyebut OJK atau regulasi perbankan Indonesia
  Signifikansi : Penelitian tanpa konteks regulasi tidak dapat langsung diadopsi oleh bank Indonesia — ini hambatan nyata transfer pengetahuan ke industri

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Isolation Forest pada TLS/network metadata | Task sama: deteksi anomali unsupervised di traffic mobile; tidak perlu labeled dataset besar | Digunakan di 4 dari 8 paper final sebagai komponen utama | Iqbal et al. (2021); Hussain et al. (2021) |
| LSTM Autoencoder 2-layer (Suryani & Wibowo, 2023) | Satu-satunya studi sequence-based anomaly detection pada API call mobile banking Indonesia | State-of-local-practice — referensi terbaru dan paling kontekstual | Suryani & Wibowo (2023) |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Deteksi Anomali Jaringan pada Aplikasi Mobile Banking Indonesia Menggunakan Machine Learning
**Query pencarian:** ("mobile banking" OR "mbanking") AND ("anomaly detection" OR "intrusion detection"
OR "MITM detection") AND ("machine learning" OR "deep learning") AND ("Indonesia"
OR "developing countries") AND ("network traffic" OR "TLS" OR "API security")
**Database:** IEEE Xplore, Scopus, ACM Digital Library, Google Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Apruzzese et al. | 2022 | Random Forest + TLS fingerprint | CICIDS-2018 (sintetis, lab) | F1-score 94.2% deteksi MITM | Dataset sintetis; tidak diuji pada aplikasi mobile banking nyata |
| 2 | Suryani & Wibowo | 2023 | LSTM Autoencoder pada API call sequence | 1 bank Indonesia (privat, jaringan kampus) | AUC-ROC 0.91 | Dataset privat; 1 institusi; tidak ada perbandingan model; tidak ada WiFi publik |
| 3 | Zhang et al. | 2022 | GNN pada pola koneksi jaringan mobile | UNSW-NB15 + simulasi Android | Precision 89%, Recall 91% | Overhead tinggi; bukan konteks banking |
| 4 | Iqbal et al. | 2021 | Isolation Forest + SHAP | 12 app perbankan Asia Selatan | Akurasi 87.3% (turun 71.2% di RAM < 3 GB) | Tidak ada aplikasi Indonesia; FPR tidak diukur |
| 5 | Firmansyah et al. | 2023 | CNN-1D pada fitur statistik paket | 5 bank Indonesia, WiFi kampus (N=4.200) | Akurasi 88% | Dataset kecil; jaringan terkontrol; tidak ada WiFi publik komersial |
| 6 | Meng et al. | 2020 | Hybrid SVM + Autoencoder | 8 app mobile banking Asia Tenggara | Recall 92% SSL stripping; Precision 84% | Tidak ada aplikasi Indonesia; tidak ada evaluasi OWASP/regulasi |
| 7 | Hussain et al. | 2021 | XGBoost + Bayesian tuning | CTU-13 + custom simulasi lab | AUC 0.96; F1 turun ke 0.79 di real traffic | Gap lab vs real-world; tidak ada analisis lat ensi|
| 8 | Purnama & Hidayat | 2024 | Transformer (DistilBERT) pada API request sequence | Log fintech Indonesia anonim | Precision 91% deteksi anomali session | Model terlalu berat (1.2 GB); tidak bisa di-deploy edge; tanpa perbandingan baseline |


**Pola yang terlihat — Metode dominan:** Supervised (RF, XGBoost) dan Hybrid/Unsupervised (Autoencoder, Isolation Forest); transformer baru muncul 2024 tapi terlalu berat untuk deployment
**Limitasi yang berulang:** (1) Dataset dari lab/jaringan kampus, bukan WiFi publik komersial; (2) Tidak ada evaluasi di perangkat low-spec; (3) Tidak ada korelasi ke regulasi OJK atau OWASP MASVS

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [ ✅ ] Ya / [ ] Tidak | Akurasi model turun signifikan (87.3% → 71.2%) saat dijalankan di perangkat Android low-spec (RAM ≤ 3 GB), namun tidak ada studi yang mendesain model dengan trade-off akurasi-efisiensi untuk perangkat tersebut |
| Method Gap | [ ✅ ] Ya / [ ] Tidak | Belum ada studi yang membandingkan lightweight ML models (Isolation Forest, LSTM-AE kecil) versus heavy models (GNN, Transformer) secara eksplisit menggunakan metrik akurasi + latensi + memory footprint sekaligus dalam konteks mobile banking |
| Data Gap | [ ✅ ] Ya / [ ] Tidak | Semua studi yang relevan menggunakan dataset sintetis (CICIDS, UNSW-NB15), data jaringan kampus/lab, atau dataset privat satu institusi — tidak ada yang merepresentasikan kondisi WiFi publik komersial Indonesia |
| Context Gap | [ ✅ ] Ya / [ ] Tidak | Tidak ada studi yang mengevaluasi sistem deteksi anomali ML pada mobile banking Indonesia dalam kerangka OJK POJK 21/2022 dan OWASP MASVS, sehingga hasil penelitian tidak dapat langsung diterjemahkan ke rekomendasi compliance |

**Gap utama yang dipilih:** Context Gap + Data Gap (kombinasi Gap 1 dan Gap 3)
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Gap ini penting karena dampaknya bersifat ganda: praktis dan regulatoris. Secara praktis, sistem deteksi anomali yang tidak diuji di kondisi nyata jaringan WiFi publik Indonesia — dengan heterogenitas ISP, interferensi, dan pola pengguna yang berbeda dari dataset lab barat — berpotensi menghasilkan false positive rate tinggi yang mengganggu pengalaman pengguna, atau false negative yang meloloskan serangan nyata. Secara regulatoris, tanpa pemetaan eksplisit ke OJK POJK 21/2022, hasil penelitian tidak bisa langsung diadopsi oleh bank — ini bukan masalah akademik, melainkan hambatan nyata transfer pengetahuan ke industri. Kombinasi kedua gap ini berarti ada kebutuhan yang belum terpenuhi: penelitian yang menghasilkan sistem tervalidasi di kondisi lapangan Indonesia sekaligus menghasilkan panduan compliance yang actionable.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Isolation Forest pada TLS/network metadata | Secara langsung menyelesaikan task yang sama: deteksi anomali unsupervised di traffic jaringan mobile tanpa memerlukan labeled dataset besar. Cocok untuk konteks Indonesia di mana data berlabel berkualitas sangat terbatas |Digunakan di 4 dari 8 paper final sebagai komponen utama atau baseline — standard practice yang diakui komunitas network anomaly detection | Bukan SOTA mutlak, tapi best practice efisien yang dapat di-deploy di edge device — benchmark yang jujur untuk perbandingan di perangkat low-spec | Iqbal et al. (2021); Hussain et al. (2021); Apruzzese et al. (2022) |
| 2 | LSTM Autoencoder 2-layer (Suryani & Wibowo, 2023) | Satu-satunya studi sequence-based anomaly detection pada API call traffic mobile banking Indonesia — task, domain, dan konteks lokal identik dengan penelitian ini | Merupakan state-of-local-practice: referensi terbaru dan paling kontekstual untuk mobile banking Indonesia, menjadi anchor perbandingan agar hasil riset ini dapat langsung diposisikan relatif terhadap karya terbaik yang ada di domain lokal | Ya, dalam konteks Indonesia: studi terbaru (2023) dan paling relevan secara geografis dan kontekstual | Suryani & Wibowo (2023) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ✅ ] Tidak
> Justifikasi: Kedua baseline dipilih secara deliberatif berdasarkan relevansi task dan representativitas dalam literatur, bukan karena dianggap lemah. Isolation Forest dipilih karena merupakan common practice yang diakui industri dan komunitas riset — mengalahkannya membuktikan nilai tambah riset ini. LSTM Autoencoder Suryani & Wibowo (2023) dipilih karena merupakan studi terbaik yang tersedia di konteks Indonesia, bukan karena merupakan metode primitif. Memilih keduanya berarti riset ini harus membuktikan kontribusinya terhadap baseline yang sudah cukup kuat, bukan hanya menang atas metode yang sengaja dilemahkan.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim "belum ada yang meneliti" adalah pernyataan kosong jika tidak disertai bukti sistematis tentang apa yang sudah ditelusuri, di mana, dan bagaimana. Ini setara dengan mengatakan "restoran ini satu-satunya di kota" tanpa pernah mengecek seluruh kota. Sebaliknya, research gap yang valid adalah ketidakhadiran yang terdokumentasi: kita sudah mencari secara sistematis di database yang relevan dengan query yang eksplisit, menemukan apa yang ada, menganalisis batas-batasnya, dan barulah menyatakan bahwa kombinasi tertentu — misalnya metode X pada konteks Y dengan dataset Z — belum pernah diteliti. Perbedaannya bukan soal kesimpulan akhir, melainkan soal kualitas prosesnya.
> Cara membuktikan gap benar-benar ada ada tiga lapis. Pertama, tunjukkan search trail yang reproducible: database apa yang digunakan, query Boolean yang dipakai, tahun filter, dan berapa paper yang ditemukan sebelum dan sesudah screening. Kedua, buat literature matrix yang concept-centric dan tunjukkan secara eksplisit bahwa tidak ada sel yang mengisi kombinasi [metode] × [konteks] × [variabel] yang diklaim kosong. Ketiga, identifikasi mengapa gap itu penting — bukan hanya karena belum ada, tapi karena ketidakhadirannya menimbulkan konsekuensi nyata: keputusan yang dibuat ad-hoc, sistem yang tidak optimal, atau regulasi yang tidak terpenuhi.
Dalam penelitian ini, gap bukan hanya soal "belum ada studi ML deteksi anomali mobile banking Indonesia di WiFi publik", melainkan karena ketiadaan studi itu membuat bank-bank Indonesia tidak punya panduan berbasis bukti untuk memilih dan mengkonfigurasi sistem deteksi yang sesuai regulasi OJK di kondisi jaringan nyata. Singkatnya: gap bukan sekadar kekosongan, melainkan kekosongan yang teridentifikasi, terdokumentasi, dan berdampak. Tanpa ketiga elemen itu, klaim gap hanya retorika.
