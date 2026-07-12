# 06-output

Hasil olahan data dan visualisasi — output dari eksperimen NB vs SVM (2026-05-12).

Dihasilkan dari notebook [`05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb`](../05-kode/NB_vs_SVM_Sentiment_MobileBanking.ipynb) dari data mentah di [`04-data/`](../04-data/).

## tables/

| File | Isi |
|------|-----|
| [`hasil_perbandingan.csv`](tables/hasil_perbandingan.csv) | F1-Score dan Akurasi NB vs SVM run tunggal (random_state=42) |
| [`hasil_statistik.csv`](tables/hasil_statistik.csv) | F1-Score NB dan SVM dari 10 run eksperimen (random_state=0–9), rata-rata, dan std. deviasi |

## figures/

| File | Isi |
|------|-----|
| [`grafik_perbandingan.png`](figures/grafik_perbandingan.png) | Bar chart perbandingan F1-Score dan Akurasi NB vs SVM (dpi=300) |

## Acuan

[../07-manuskrip/05-hasil-analisis.md](../07-manuskrip/05-hasil-analisis.md)