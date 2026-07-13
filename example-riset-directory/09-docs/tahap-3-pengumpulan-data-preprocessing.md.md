# Tahap 3 — Pengumpulan Data & Preprocessing

**Status:** Selesai 
**Bergantung pada:** [tahap-2-implementasi-pipeline-klasifikasi-(phyton).md](tahap-2-implementasi-pipeline-klasifikasi-(python).md)
**Lokasi kode:** [../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb](../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb) Cell 1–10

---

## Tujuan

Mengumpulkan dataset ulasan mobile banking Indonesia dari Google Play Store dan menjalankan pipeline preprocessing untuk menghasilkan dataset bersih yang siap digunakan sebagai input eksperimen.

## Deliverable

- [x] Scraping 6.000 ulasan dari 3 aplikasi mobile banking (Cell 3–6)
- [x] Labeling otomatis berdasarkan rating bintang (Cell 6)
- [x] Simpan dataset mentah: `dataset_ulasan_banking.csv` (Cell 6–7)
- [x] Instalasi PySastrawi + definisi fungsi preprocessing (Cell 8)
- [x] Load CSV + jalankan preprocessing pada 6.000 ulasan (Cell 9)
- [x] Simpan dataset bersih: `dataset_bersih.csv` (Cell 10)

## Desain yang Diimplementasikan

### Struktur Scraping

| Parameter | Nilai |
|-----------|-------|
| Library | google-play-scraper 1.2.7 |
| lang | id |
| country | id |
| sort | Sort.NEWEST |
| count per app | 2.000 |
| Periode | 2022–2024 |

| Aplikasi | Package ID | Jumlah |
|----------|-----------|--------|
| BCA Mobile | com.bca | 2.000 |
| Mandiri Online | com.bankmandiri.mandirionline | 2.000 |
| BRImo | id.co.bri.brimo | 2.000 |
| **Total** | | **6.000** |

### Labeling Sentimen

Labeling dilakukan otomatis berdasarkan rating bintang — tidak ada labeling manual:

| Sentimen | Rating | Jumlah | Persentase |
|----------|--------|--------|------------|
| Positif | 4–5★ | 4.184 | 69,7% |
| Negatif | 1–2★ | 1.540 | 25,7% |
| Netral | 3★ | 276 | 4,6% |
| **Total** | | **6.000** | **100%** |

### Pipeline Preprocessing (PySastrawi)

Dijalankan **identik** untuk kedua kondisi eksperimen:

1. **Lowercase** — normalisasi kapitalisasi seluruh teks
2. **Cleansing** — hapus simbol, angka, emoji, dan karakter tidak informatif
3. **Stopword removal** — StopWordRemoverFactory dari PySastrawi
4. **Stemming** — StemmerFactory dari PySastrawi, mereduksi kata ke bentuk dasar Bahasa Indonesia

**Hasil:** 5.758 ulasan valid dari 6.000 total (242 dihapus karena teks kosong setelah preprocessing)

### Output

| File | Lokasi | Isi |
|------|--------|-----|
| `dataset_ulasan_banking.csv` | [../04-data/](../04-data/) | 6.000 ulasan mentah — kolom: nama_user, ulasan, rating, tanggal, aplikasi, sentimen |
| `dataset_bersih.csv` | [../04-data/](../04-data/) | 5.758 ulasan bersih — tambahan kolom: ulasan_bersih |

## Catatan Lingkungan

- **Error scraping BRImo** — package ID awal (com.bri.britama) menghasilkan 0 ulasan karena salah. Diperbaiki dengan package ID yang benar (id.co.bri.brimo) pada cell berikutnya — total tetap 6.000 ulasan
- Waktu total scraping + preprocessing: ~15 menit (15:30–15:45 WIB)
- Seluruh proses dijalankan dalam satu sesi Google Colab tanpa interrupt
- Dataset disimpan dalam format CSV dengan kolom: nama_user, ulasan, rating, tanggal, aplikasi, sentimen