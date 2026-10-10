[README.md](https://github.com/user-attachments/files/33273279/README.md)
# Kemiskinan Antar Provinsi di Indonesia: Regresi Berganda dan Clustering dengan R

Analisis statistik hubungan antara indikator sosial-ekonomi dan persentase penduduk miskin di tingkat provinsi, menggunakan regresi linear berganda (dengan uji asumsi dan koreksi heteroskedastisitas) dan segmentasi provinsi dengan k-means clustering.

**Laporan lengkap (HTML):** https://salsarn17.github.io/kemiskinan-provinsi-r/Analisis-Kemiskinan-Antarprovinsi-di-Indonesia.html

## Pertanyaan penelitian

Faktor sosial-ekonomi apa yang paling berkaitan dengan tingkat kemiskinan antar provinsi di Indonesia, dan bagaimana provinsi dapat dikelompokkan berdasarkan profil pembangunannya?

## Temuan utama

<!-- TODO: cocokkan angka di bawah dengan hasil di laporanmu sebelum dipublikasikan -->

- Akses sanitasi layak adalah indikator yang paling konsisten berkaitan dengan kemiskinan antar provinsi (koefisien sekitar -0,39; p = 0,006 dengan galat baku robust HC3). Hubungan ini bertahan saat dua provinsi pencilan di Papua dikeluarkan.
- Model menjelaskan sekitar 63% variasi kemiskinan (R² terkoreksi 0,63). Pengangguran terbuka, rata-rata lama sekolah, dan PDRB per kapita tidak signifikan setelah koreksi heteroskedastisitas.
- Provinsi terbagi menjadi 4 klaster berdasarkan profil pembangunan (rata-rata silhouette 0,39, struktur lemah). Satu klaster berisi dua provinsi Papua dengan kondisi paling tertinggal.

## Dashboard Tableau

[![Dashboard kemiskinan antar provinsi](dashboard-tableau.png)](https://public.tableau.com/app/profile/salsa.rifqah.nuraini/viz/KemiskinanAntarProvinsidiIndonesia/KemiskinanAntarProvinsidiIndonesia2025)

Dashboard interaktif yang menampilkan persentase penduduk miskin per provinsi (bar chart, peta, dan scatter akses sanitasi vs kemiskinan). Data: BPS, 2025.

**Buka dashboard interaktif:** [Tableau Public](https://public.tableau.com/app/profile/salsa.rifqah.nuraini/viz/KemiskinanAntarProvinsidiIndonesia/KemiskinanAntarProvinsidiIndonesia2025)

## Metode

- Eksplorasi data dan visualisasi (`ggplot2`)
- Regresi linear berganda dengan uji asumsi: VIF, Shapiro-Wilk, Breusch-Pagan, Cook's distance
- Galat baku robust (HC3) karena asumsi ragam konstan tidak terpenuhi, dan uji ketahanan tanpa dua provinsi berpengaruh
- K-means clustering dengan pemilihan jumlah klaster lewat silhouette, dan uji Kruskal-Wallis antar klaster

## Data

Sumber: Badan Pusat Statistik (BPS), 38 provinsi, tahun 2025. File data: `data_provinsi.xlsx`.

| Kolom | Isi |
|---|---|
| `Provinsi` | Nama provinsi |
| `p0` | Persentase penduduk miskin (P0), semester: <!-- TODO: Maret atau September 2025 --> |
| `tpt` | Tingkat pengangguran terbuka (%), Agustus 2025 |
| `rls` | Rata-rata lama sekolah (tahun) |
| `pdrb` | PDRB per kapita atas dasar harga berlaku (ribu rupiah), diubah ke logaritma saat analisis |
| `sanitasi` | Persentase rumah tangga dengan akses sanitasi layak |

## Cara menjalankan ulang

1. Clone atau unduh repo ini.
2. Pasang package di R:
   ```r
   install.packages(c("tidyverse", "readxl", "janitor", "here", "car",
                      "lmtest", "sandwich", "broom", "factoextra",
                      "cluster", "rmarkdown"))
   ```
3. Buka file `Analisis Kemiskinan Antarprovinsi di Indonesia.Rmd` di RStudio. Pastikan `data_provinsi.xlsx` berada di folder yang sama.
4. Klik **Knit** untuk menghasilkan laporan HTML.

## Isi repo

```
kemiskinan-provinsi-r/
├── README.md
├── Analisis Kemiskinan Antarprovinsi di Indonesia.Rmd   # kode dan narasi analisis
├── Analisis-Kemiskinan-Antarprovinsi-di-Indonesia.html  # hasil render
└── data_provinsi.xlsx                                   # data dari BPS
```

## Keterbatasan

- Sampel hanya 38 provinsi sehingga kuasa uji rendah; variabel yang tidak signifikan belum tentu tidak berhubungan.
- Dua provinsi di Papua (Papua Tengah dan Papua Pegunungan) sangat berpengaruh terhadap model; ragam residual tidak konstan sehingga dipakai galat baku robust.
- Koefisien rata-rata lama sekolah bertanda positif, kemungkinan akibat korelasinya yang tinggi dengan sanitasi (r = 0,76), sehingga tidak ditafsirkan.
- Struktur klaster lemah (silhouette 0,39) dan tingkat kemiskinan tidak berbeda nyata antar tiga klaster di luar kelompok Papua.
- Data agregat provinsi pada satu titik waktu: temuan menunjukkan asosiasi, bukan sebab-akibat.

## Kontak

Salsa Rifqah Nuraini, S.Stat | 
