# KosCheck - Platform Asisten Survei & Verifikasi Fisik Kos On-Demand

> Platform independen inspeksi dan audit kelayakan fisik kamar kos berbasis gig-economy mahasiswa lokal untuk melindungi calon mahasiswa rantau dari manipulasi foto listing, fasilitas fiktif, dan penipuan uang muka (DP).

---

## 1. Ikhtisar Projek

**KosCheck** adalah solusi PropTech berbasis *asset-light* yang menjembatani kesenjangan informasi (*information asymmetry*) antara pemilik kos dan calon penyewa di kota rantau. Portal properti komersial yang ada saat ini dibiayai oleh pemilik kos, sehingga kekurangan fasilitas sering disembunyikan. KosCheck beroperasi dari sudut pandang penyewa: dibayar oleh mahasiswa untuk melakukan audit fisik empiris apa adanya secara objektif sebelum transaksi sewa dilakukan.

Projek ini dikembangkan sebagai inisiatif mata kuliah **Digital Entrepreneurship (Semester 5)**, Program Studi Teknik Informatika, Universitas Pamulang (UNPAM).

---

## 2. Masalah Riil & Solusi KosCheck

| Masalah Lapangan | Realitas di Portal Iklan | Solusi KosCheck (Empiris) |
| :--- | :--- | :--- |
| **Manipulasi Visual** | Foto listing menggunakan lensa *ultra-wide* dan pencahayaan studio sehingga kamar 2x3 meter tampak luas. | Perekaman video kontinu 60fps sudut pandang normal (*one-take without cut*) dari gerbang luar, lorong, hingga kamar mandi. |
| **Kualitas Sanitasi Air** | Iklan mengklaim "air bersih lancar", namun aslinya berbau karat besi, keruh, atau debit pompa mati. | Uji tampung air keran selama 10 menit untuk mendeteksi endapan partikel dan stabilitas tekanan pompa. |
| **Blind Spot Sinyal HP** | Deskripsi mencantumkan "WiFi & Sinyal Kuat", tetapi di dalam kamar tertutup sinyal internet hilang total. | Pengujian speedtest 4G (Telkomsel, Indosat, XL, Smartfren) langsung di meja belajar dengan pintu kamar tertutup rapat. |
| **Penipuan Uang Muka (DP)** | Makelar palsu menduplikasi foto kos dan meminta transfer DP ke rekening bodong. | Surveyor bertemu tatap muka dengan pengelola asli dan memverifikasi kesesuaian KTP dengan rekening bank tujuan. |

---

## 3. Metodologi Standar: SOP 4 Pilar Audit

Setiap penugasan survei KosCheck mengacu pada checklist 28 parameter baku:

1. **Pilar 1: Sanitasi & Kualitas Air**
   - Kejernihan visual air keran.
   - Deteksi bau pipa / karat besi / belerang.
   - Uji debit dan kestabilan pompa air selama 10 menit.
   - Kebersihan saluran pembuangan kamar mandi (bebas genangan).

2. **Pilar 2: Konektivitas & Jaringan Seluler**
   - Speedtest 4 operator seluler utama di dalam kamar tertutup.
   - Pengujian latensi (ping) dan packet loss untuk kebutuhan kuliah daring.
   - Pengecekan stabilitas WiFi kos (jika disediakan).

3. **Pilar 3: Dimensi Riil & Rekaman Visual 60fps**
   - Pengukuran dimensi kamar menggunakan meteran fisik.
   - Video *one-take walk-through* 60fps tanpa manipulasi sudut lebar.
   - Dokumentasi sirkulasi udara, ventilasi, dan tingkat kebisingan lingkungan (dB meter).

4. **Pilar 4: Verifikasi Identitas & Pencegahan Scam**
   - Wawancara langsung dengan pemilik / pengelola sah kos.
   - Pencocokan KTP pengelola dengan nomor rekening bank penerima sewa.
   - Pemeriksaan tata tertib kos, jam malam, dan biaya tambahan (listrik, sampah, parkir).

---

## 4. Arsitektur Antarmuka & Modul

Aplikasi web dirancang dengan pendekatan *Japanese Functional Minimalism* terinspirasi dari standar desain UNIQLO dan Apple, mengutamakan kanvas putih bersih (`#ffffff`), kontras tipografi tinggi, dan nol *gimmick* visual.

### Modul Utama:

1. **Landing Page (`index.html`)**
   - **Full-Bleed Fullscreen Hero**: Visual kamar studio arsitektural resolusi tinggi membentang 100vw edge-to-edge dengan tipografi editorial modern (font Inter).
   - **Streamlined Navigation Bar**: Header lapang dengan navigasi kategori esensial (*Peta Kos, Layanan, SOP 4 Pilar, Bantuan*) dan kotak pencarian kampus responsif.
   - **Dynamic Mobile Drawer**: Menu navigasi *slide-out drawer* halus untuk viewport smartphone (`< 768px`) dengan backdrop blur.
   - **Kalkulator Finansial ROI Mahasiswa**: Simulator interaktif yang menghitung efisiensi biaya survei mandiri (tiket perjalanan + hotel Rp 1.5jt - Rp 2jt) vs tarif KosCheck (Rp 35.000).
   - **Tabel Komparasi Objektif**: Matriks perbandingan fitur KosCheck vs Mamikos vs Jastip Biasa.
   - **Modal Sampel Laporan Digital**: Dokumen interaktif simulasi hasil audit fisik lapangan lengkap dengan skor kelayakan.
   - **Smooth Scroll-Reveal**: Transisi animasi kemunculan elemen berbasis IntersectionObserver tanpa dependensi pihak ketiga.

2. **Peta Interaktif & Pencarian Kos (`cari.html`)**
   - **Split-Screen Layout**: Tampilan dua panel sejajar (katalog daftar kos di sisi kiri + peta interaktif di sisi kanan) ala Mamikos dan Airbnb.
   - **Mesin Autocomplete Predictive dengan Debounce**: Pencarian live dengan jeda 200ms untuk performa instan tanpa lag, mengelompokkan hasil berdasarkan kampus acuan (UNPAM Viktor, UNPAM Pusat, UI Depok, ITB Bandung) dan nama properti.
   - **Peta Interaktif (Leaflet.js + CartoDB Positron)**: Peta berlatar monokrom terang minimalis tanpa batasan kuota API komersial.
   - **Sinkronisasi Dua Arah (Bi-Directional Sync)**: Pin harga di peta (`custom-price-pin`) terhubung langsung dengan kartu kos di panel kiri (klik pin otomatis menyorot kartu, dan klik kartu otomatis menerbangkan kamera peta ke titik koordinat kos).
   - **Filter Cepat**: Penyaringan instan berdasarkan kampus, tipe kos (Putri, Putra, Campur), dan status kelolosan audit 4 pilar.
   - **Mobile View Toggle**: Tombol floating interaktif *"Lihat di Peta"* / *"Lihat Daftar"* untuk navigasi optimal di perangkat ponsel.

---

## 5. Model Bisnis & Struktur Layanan

- **Check My Kos (Rp 35.000 / lokasi)**: Layanan paling populer untuk calon penyewa yang sudah mengantongi 1 link iklan kos tertentu dan membutuhkan audit fisik mendalam.
- **Find My Kos (Rp 75.000 / paket)**: Rekomendasi dan kurasi 3 unit kos terbaik sesuai bujet dan kriteria jarak jalan kaki ke kampus.
- **B2B Verified Badge (Rp 50.000 / tahun)**: Sertifikasi resmi bagi pemilik properti kos jujur yang bersedia diaudit untuk mendapatkan prioritas rekomendasi dan stiker QR Code fisik di gerbang kos.

---

## 6. Struktur Direktori

```text
koscek/
├── index.html            # Landing page utama (Uniqlo/Apple aesthetic)
├── cari.html             # Halaman pencarian & peta interaktif (Leaflet.js)
├── hero-room.jpg         # Aset visual interior kamar resolusi tinggi
├── koscheck-logo.png     # Aset logo resmi kamera detektif KosCheck
└── README.md             # Dokumentasi teknis & arsitektur projek
```

---

## 7. Cara Menjalankan Projek

Projek ini dibangun menggunakan standar web modern native (HTML5, Tailwind CSS via CDN, Leaflet.js, Lucide Icons) tanpa membutuhkan proses *compilation* atau dependensi runtime Node.js yang kompleks.

### Menjalankan Langsung:
1. Unduh atau clone repositori ini:
   ```bash
   git clone https://github.com/daerobi-devs/koscek.git
   cd koscek
   ```
2. Buka file `index.html` langsung di browser apapun (Chrome, Edge, Safari, Firefox):
   - Klik ganda pada file `index.html`, atau
   - Buka via ekstensi **Live Server** di Visual Studio Code untuk pengalaman live reload.

---

## 8. Rencana Pengembangan (Roadmap)

- **Fase 1 (Selesai)**: Landing page arsitektur minimalis, SOP 4 Pilar, modul kalkulator ROI, dan peta interaktif dengan predictive search.
- **Fase 2**: Integrasi Progressive Web App (PWA) khusus surveyor lapangan dengan fitur *watermark timestamp GPS & accelerometer* pada rekaman video.
- **Fase 3**: Sistem escrow pembayaran uang muka terintegrasi QRIS otomatis yang hanya mencairkan dana ke pemilik kos setelah verifikasi KTP tatap muka selesai dan disetujui pemesan.

---

## 9. Lisensi & Hak Cipta

Hak Cipta (c) 2026 **KosCheck Indonesia**. Dikembangkan oleh **daerobi-devs** untuk Program Digital Entrepreneurship, Universitas Pamulang. Seluruh hak dilindungi undang-undang.
