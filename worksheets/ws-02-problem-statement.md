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
  Domain   : Keamanan Siber & Rekayasa Perangkat Lunak Mobile
  Konteks  : Aplikasi mobile banking yang digunakan nasabah ritel di Indonesia, berjalan pada perangkat Android/iOS yang mengakses layanan perbankan melalui jaringan publik maupun privat

System Context
  Input       : Kredensial pengguna (PIN/password/biometrik), data transaksi (nominal, rekening tujuan), request HTTPS dari aplikasi mobile ke server bank
  Process     : TLS handshake dan validasi sertifikat, autentikasi token JWT, enkripsi payload AES-256, pemrosesan logika bisnis transaksi di backend/core banking
  Output      : Konfirmasi transaksi, data saldo terkini, riwayat mutasi — dikembalikan ke aplikasi dalam format JSON terenkripsi
  Outcome     : Nasabah dapat bertransaksi dengan aman; bank menjaga kepercayaan pengguna dan kepatuhan regulasi OJK POJK 21/2022
  Constraints : Perangkat end-user beragam (Android 10–14, iOS 15–17, RAM 2–8 GB); jaringan tidak terpercaya (WiFi publik); certificate pinning rentan gagal saat rotasi sertifikat; mTLS memerlukan manajemen sertifikat klien yang kompleks
  Stakeholders: Nasabah, tim keamanan dan DevSecOps bank, regulator (OJK, Bank Indonesia), pengembang aplikasi, vendor cloud/CDN

Fenomena → Problem
  Fenomena yang diamati             : Jutaan nasabah Indonesia bertransaksi lewat mobile banking setiap hari, banyak melalui WiFi publik di kafe, mall, dan transportasi umum
  Gejala (symptom) yang terukur     : Studi kasus 2023 mengkonfirmasi bahwa serangan MITM masih berhasil dilakukan pada beberapa aplikasi mobile banking Indonesia meski sudah menggunakan TLS
  Masalah yang didiagnosis          : Implementasi validasi sertifikat tidak konsisten antar-aplikasi — sebagian pakai certificate pinning statis, sebagian hanya TLS default sistem operasi — keduanya masih bisa di-bypass
  Masalah riset (researchable)      : Belum ada studi komparatif yang mengukur efektivitas certificate pinning vs mutual TLS (mTLS) dalam mencegah serangan MITM pada aplikasi mobile banking di Indonesia
  Variabel yang terukur             : Tingkat keberhasilan serangan MITM (%), overhead latensi API (ms), skor kepatuhan OWASP MASVS (0–100)

Problem Quality Check
  [✅] Clarity — Apakah satu orang membaca akan paham?
  [✅] Measurability — Apakah ada metrik kuantitatif?
  [✅] Relevance — Apakah penting untuk domain?
  [✅] Testability — Apakah bisa gagal?
  [✅] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Aplikasi mobile banking di Indonesia menghadapi ancaman serangan man-in-the-middle (MITM) yang signifikan, terutama pada pengguna yang mengakses layanan melalui jaringan WiFi publik yang tidak terenkripsi. Meskipun mekanisme pengamanan komunikasi seperti certificate pinning dan mutual TLS (mTLS) telah tersedia, penelitian terhadap aplikasi banking Android di Indonesia menunjukkan bahwa sebagian besar masih memiliki kelemahan pada lapisan transport karena implementasi yang tidak konsisten. Belum terdapat studi komparatif yang secara empiris mengukur efektivitas relatif certificate pinning versus mTLS dalam konteks aplikasi mobile banking Indonesia, sehingga pengembang memilih mekanisme keamanan secara ad-hoc tanpa panduan berbasis bukti. Penelitian ini bertujuan membandingkan tingkat keberhasilan serangan MITM (%), overhead latensi API response (ms), dan skor kepatuhan OWASP MASVS antara kedua mekanisme pada lingkungan simulasi terstandarisasi menggunakan perangkat Android 12+ dan iOS 16+, guna menghasilkan rekomendasi implementasi yang dapat diadopsi industri perbankan nasional.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Keamanan komunikasi pada aplikasi mobile banking di Indonesia

| Tahap | Hasil |
|-------|-------|
| Reality | Jutaan nasabah bank di Indonesia menggunakan aplikasi mobile banking setiap hari untuk transfer, cek saldo, dan pembayaran tagihan, banyak di antaranya melalui jaringan WiFi publik di kafe, mall, dan transportasi umum |
| Observed Issue (Symptom) | Studi kasus 2023 dari Universitas Medan Area mengkonfirmasi bahwa serangan MITM masih berhasil dilakukan pada beberapa aplikasi mobile banking Indonesia meski sudah menggunakan protokol TLS, karena implementasi sertifikat SSL yang tidak memadai |
| Diagnosed Problem (Root Cause) | Implementasi validasi sertifikat tidak standar antar-aplikasi: sebagian menggunakan certificate pinning statis, sebagian hanya mengandalkan TLS default sistem operasi. Keduanya masih memiliki celah — certificate pinning dapat di-bypass melalui tools seperti Frida, sedangkan TLS default rentan terhadap serangan melalui sertifikat CA yang dikompromikan |
| Researchable Problem | Belum terdapat studi komparatif yang secara empiris mengukur dan membandingkan efektivitas certificate pinning versus mutual TLS (mTLS) dalam mencegah serangan MITM pada aplikasi mobile banking Indonesia, serta dampaknya terhadap performa dan kepatuhan standar OWASP MASVS |
| Measurable Variable | Variabel independen: mekanisme keamanan (certificate pinning vs mTLS). Variabel dependen: (1) tingkat keberhasilan serangan MITM dalam simulasi testbed (%), (2) overhead latensi API response dibandingkan baseline (ms), (3) skor kepatuhan OWASP MASVS-NETWORK (0–100) |

**Apakah terjebak solution-first thinking?** [ ] Ya / [✅] Tidak
> Jika ya, kembali ke tahap mana? Penelitian dimulai dari gap pengetahuan — "belum ada studi komparatif" — bukan dari asumsi bahwa salah satu solusi lebih baik. Pilihan antara certificate pinning atau mTLS adalah pertanyaan riset, bukan premis awal.
---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Request HTTPS dari aplikasi mobile (Android/iOS) berisi token autentikasi JWT, data transaksi (nominal, rekening tujuan), metadata perangkat (device fingerprint, OS version, app version). Juga mencakup sertifikat klien pada implementasi mTLS |
| Process | Negosiasi TLS handshake termasuk validasi sertifikat server dan opsional sertifikat klien pada mTLS, pengecekan certificate pinning di sisi aplikasi, enkripsi/dekripsi payload AES-256-GCM, verifikasi token JWT di API Gateway, pemrosesan logika transaksi di core banking system |
| Output | Response API dalam format JSON terenkripsi berisi status transaksi (berhasil/gagal/pending), saldo terkini, referensi nomor transaksi unik, timestamp server — dikembalikan ke aplikasi dalam koneksi TLS yang sama |
| Outcome | Nasabah mendapat konfirmasi transaksi yang aman dan akurat. Bank mempertahankan kepercayaan pengguna, memenuhi kepatuhan regulasi OJK POJK 21/2022, dan mengurangi risiko kerugian akibat fraud digital |
| Constraints | (1) Heterogenitas perangkat: Android 10–14, iOS 15–17, RAM 2–8 GB; (2) jaringan tidak terpercaya: WiFi publik tanpa enkripsi end-to-end; (3) certificate pinning berisiko gagal saat rotasi sertifikat jika aplikasi tidak diperbarui; (4) mTLS memerlukan distribusi dan manajemen sertifikat klien yang kompleks; (5) batasan regulasi OJK terkait enkripsi data nasabah |
| Stakeholders | Nasabah (pengguna akhir), tim keamanan dan DevSecOps bank, regulator (OJK, Bank Indonesia), pengembang aplikasi mobile, vendor cloud/CDN yang menangani terminasi TLS, penyedia Certificate Authority (CA) |

**Komponen mana yang paling relevan dengan masalah riset?** Process dan Constraints. Komponen Process adalah inti karena gap penelitian berpusat pada perbedaan mekanisme yang terjadi selama TLS handshake dan validasi sertifikat — di sinilah certificate pinning dan mTLS beroperasi dan dapat dibandingkan. Komponen Constraints juga sangat relevan karena heterogenitas perangkat dan kondisi jaringan publik adalah variabel lingkungan yang langsung mempengaruhi hasil eksperimen.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 4 | Masalah cukup jelas dan spesifik: menyebut dua mekanisme yang dibandingkan, konteks Indonesia, dan platform target. Bisa lebih kuat jika menyebut nama tools uji (mitmproxy/Burp Suite) secara eksplisit di rumusan masalah |
| Measurability | 5 | Tiga variabel dependen dengan satuan yang jelas dan dapat diukur: success rate MITM (%), latensi (ms), skor MASVS-NETWORK (0–100). Semua bisa diukur dalam environment simulasi yang terstandarisasi |
| Relevance | 5 | Langsung relevan dengan kondisi nyata pengguna mobile banking Indonesia; dilandasi regulasi OJK POJK 21/2022 yang aktif; studi lokal masih sangat terbatas sehingga gap penelitian nyata dan signifikan |
| Testability | 5 | Hipotesis bersifat falsifiable — "mTLS lebih efektif dari certificate pinning" bisa terbukti salah jika data menunjukkan tidak ada perbedaan signifikan. Eksperimen dapat direplikasi oleh peneliti lain menggunakan tools dan testbed yang sama |
| Impact | 4 | Mengisi gap literatur keamanan mobile banking di Indonesia; menghasilkan panduan implementasi berbasis bukti bagi pengembang dan bank. Bisa lebih kuat jika dikaitkan ke standar internasional seperti NIST SP 800-163 |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Aplikasi mobile banking di Indonesia rentan terhadap serangan man-in-the-middle (MITM), terutama saat nasabah mengakses layanan melalui jaringan WiFi publik. Hasil studi kasus 2023 mengkonfirmasi bahwa serangan MITM masih berhasil dilakukan pada aplikasi mobile banking Indonesia meski sudah menggunakan TLS, akibat implementasi validasi sertifikat yang tidak konsisten. Meskipun mekanisme certificate pinning dan mutual TLS (mTLS) telah direkomendasikan oleh standar OWASP MASVS, belum terdapat studi komparatif yang mengukur efektivitas keduanya secara empiris dalam konteks spesifik aplikasi mobile banking Indonesia. Ketiadaan panduan implementasi berbasis bukti menyebabkan pengembang memilih mekanisme keamanan secara ad-hoc, berpotensi meninggalkan celah yang dapat dieksploitasi. Penelitian ini bertujuan membandingkan tiga metrik utama — tingkat keberhasilan serangan MITM (%), overhead latensi API response (ms), dan skor kepatuhan OWASP MASVS-NETWORK — antara implementasi certificate pinning dan mTLS menggunakan testbed terstandarisasi pada perangkat Android 12+ dan iOS 16+ di lingkungan jaringan WiFi publik yang disimulasikan, guna menghasilkan panduan implementasi berbasis bukti yang dapat langsung diadopsi oleh industri perbankan nasional.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah dalam coding bersifat konkret dan tunggal — ada pesan error yang spesifik, ada baris kode yang salah, ada perilaku sistem yang menyimpang dari ekspektasi. Cara pendekatannya pun langsung: debug, perbaiki kode, jalankan lagi sampai sistem berfungsi. Masalah dianggap selesai ketika sistem berjalan benar, dan tidak perlu bisa direplikasi atau dibuktikan kepada orang lain.

Masalah riset sebaliknya berangkat dari gap dalam pengetahuan — sesuatu yang belum diketahui, belum terbukti, atau belum dibandingkan secara sistematis. Tidak cukup hanya mengatakan "sistem sudah aman", karena riset menuntut jawaban atas pertanyaan "mekanisme mana yang lebih efektif, mengapa, dan seberapa besar perbedaannya secara terukur?". Solusinya harus bersifat falsifiable (bisa terbukti salah), dapat direplikasi oleh peneliti lain dengan kondisi yang sama, dan menghasilkan kontribusi pengetahuan — bukan sekadar artefak yang berjalan.

Perbedaan paling mendasar terletak pada orientasi tujuan dan standar keberhasilan. Engineering selesai ketika sistem berjalan — standarnya adalah fungsionalitas. Riset selesai ketika klaim dapat dibuktikan atau dibantah secara sistematis — standarnya adalah validitas ilmiah. Itulah mengapa mendefinisikan masalah riset jauh lebih ketat: harus ada batas lingkup yang jelas, variabel yang teroperasionalisasi, dan kriteria kegagalan yang eksplisit sejak awal.
