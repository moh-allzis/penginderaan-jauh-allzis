# Sentinel-1 SAR Flood Mapping & Change Detection

Repositori ini berisi skrip **Google Earth Engine (GEE)** untuk mendeteksi dan memetakan genangan banjir secara spasial menggunakan citra radar **Sentinel-1 Ground Range Detected (GRD)** dengan metode *Change Detection Analysis* (CDAT).

## 🛠️ Tahapan Metodologi Pengolahan
1. **Data Acquisition:** Filtrasi citra Sentinel-1 (polarisasi VV & VH, Mode Interferometric Wide / IW) berdasarkan rentang tanggal kejadian sebelum (*before*) dan sesudah (*after*) bencana.
2. **Speckle Filtering:** Mereduksi *noise* karakteristik citra radar menggunakan filter spasial *Boxcar* (Mono-temporal dengan *Kernel Size* = 8).
3. **Index Calculation:** Penggabungan nilai polarisasi (`VV + VH`) untuk memaksimalkan sensitivitas terhadap air permukaan.
4. **Change Detection (CDAT):** Analisis perubahan piksel antara citra pasca-kejadian dan pra-kejadian.
5. **Thresholding:** Penentuan ambang batas (*threshold*) otomatis berbasis statistik *Mean* dan *Standard Deviation* ($Mean - 1.5 \times StdDev$).
6. **Refinement & Masking:** 
   * **Masking Topografi:** Memfilter area menggunakan data DEM HydroSHEDS (hanya mengambil wilayah dengan kemiringan lereng / *slope* < 5%).
   * **Connected Pixel Filter:** Menyaring piksel terisolasi dengan kriteria minimum kelompok piksel terhubung ($\ge 8$ piksel).
7. **Statistik & Ekspor:** Perhitungan total luas genangan dalam satuan hektar dan fungsi otomatisasi ekspor raster ke Google Drive dalam format GeoTIFF (sistem proyeksi UTM Zone 47S).

## 🚀 Cara Menjalankan Skrip
1. Buka [Google Earth Engine Code Editor](https://code.earthengine.google.com/).
2. Buat skrip baru dan salin isi kode dari file `src/flood_mapping_sentinel1.js`.
3. Definisikan variabel `geometry` pada panel peta (*Drawing Tools*) sesuai area studi target Anda.
4. Sesuaikan parameter tanggal (`before_start`, `before_end`, `after_start`, `after_end`) serta zona UTM jika diperlukan.
5. Klik tombol **Run**.

## 📊 Output & Visualisasi
* Layer visualisasi interaktif di GEE Map (Perbandingan *Raw* vs *Final Filtered*).
* Ekspor raster spasial banjir ke Google Drive pada folder `GEE_Padang_Banjir`.
* Rekapitulasi luas total genangan (VV, VH, dan Combined) langsung tercetak di GEE Console.

## 📄 Lisensi
Distribusi kode ini bersifat terbuka untuk keperluan penelitian dan pembelajaran.
