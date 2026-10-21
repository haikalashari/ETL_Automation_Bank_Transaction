# ETL Automation Bank Transaction

Proyek ini adalah pipeline ETL sederhana untuk memproses data bank dari file CSV, membersihkan data, dan mengunggahnya ke database Supabase.

Tujuan utama proyek ini adalah mengotomatisasi proses ekstraksi, transformasi, dan loading data rekening, kartu, nasabah, pinjaman, distrik, serta transaksi bank agar siap digunakan untuk analisis atau dashboard.

## Fitur

- Membaca dataset bank dari folder `data/`
- Membersihkan kolom dan format data seperti tanggal, angka, dan teks
- Menghapus data duplikat dan menangani nilai kosong
- Mengirim data ke Supabase PostgreSQL
- Memproses file transaksi otomatis dari folder `data/transactions/incoming/`
- Mengarsipkan file transaksi yang sudah berhasil diproses

## Struktur Proyek

- `etl_pipeline.py` : Pipeline utama untuk memproses dataset master bank
- `etl_transactions_pipeline.py` : Pipeline khusus untuk file transaksi harian
- `data/` : folder berisi dataset CSV mentah dan folder transaksi masuk/arsip
- `requirements.txt` : daftar dependency Python yang dibutuhkan
- `.env` : file konfigurasi environment (tidak ikut di-commit jika disesuaikan)

## Dataset

Dataset yang diproses meliputi:

- account.csv
- card.csv
- client.csv
- disp.csv
- district.csv
- loan.csv
- order.csv
- trnx_16.csv
- transaksi yang masuk melalui `data/transactions/incoming/`

## Persiapan

1. Buat environment virtual Python
   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   ```

2. Install dependency
   ```bash
   pip install -r requirements.txt
   ```

3. Siapkan file `.env` dan isi variabel berikut:
   ```env
   SUPABASE_URI=postgresql://... 
   SUPABASE_URL=https://... 
   SUPABASE_KEY=...
   ```

## Cara Menjalankan

Jalankan pipeline utama untuk dataset master:

```bash
python etl_pipeline.py
```

Jalankan pipeline transaksi:

```bash
python etl_transactions_pipeline.py
```

## Alur Proses ETL

1. Ekstraksi: membaca file CSV dari folder `data/`
2. Transformasi: membersihkan nama kolom, format tanggal, deduplikasi, dan imputasi nilai kosong
3. Loading: menyimpan hasil ke tabel Supabase
4. Arsip: file transaksi yang berhasil diproses dipindahkan ke folder `data/transactions/archive/`

# Retail Banking Transaction Monitoring Dashboard
 
Dashboard Power BI untuk memantau aktivitas transaksi nasabah ritel bank dalam satu tampilan. Data di-refresh otomatis setiap hari pukul 01:00 UTC melalui Github Action.
 
## Tujuan
- Memantau aktivitas transaksi nasabah secara ringkas dan berkala.
- Melihat tren transaksi dari waktu ke waktu dan komposisinya berdasarkan berbagai sudut pandang.
- Mendukung pengambilan keputusan operasional, pengelolaan risiko, dan strategi bisnis.
## KPI
| KPI | Tujuan |
|---|---|
| Total Volume | Mengukur total nilai uang yang ditransaksikan |
| Total Transaction Frequency | Mengukur seberapa sering transaksi terjadi |
| Average Transaction Value | Mengetahui rata-rata nilai per transaksi |
| Average Balance | Mengetahui kondisi rata-rata saldo nasabah |
| Active Account | Mengetahui jumlah akun yang aktif bertransaksi |
 
## Dimensi
- **Waktu (Tahun, Bulan)**: melihat tren dan pola musiman.
- **Tipe Akun**: membandingkan perilaku transaksi antar segmen nasabah.
- **Tipe Transaksi (Credit/Withdrawal)**: melihat arus uang masuk dan keluar.
- **Tujuan Transaksi (Purpose)**: memahami alasan di balik transaksi.
- **Wilayah (Region dan District)**: mengidentifikasi area dengan aktivitas tertinggi.
- **Operasi (Operation)**: melihat kanal atau jenis transaksi yang paling sering dipakai.
- **Bank**: melihat bank mitra atau tujuan transaksi.
## Filter dan Parameter
- **Tahun, Bulan**
  - Seluruh analisis bergantung pada periode, sehingga filter ini menjadi acuan utama.
  - Memudahkan perbandingan antar periode dan fokus pada bulan tertentu.
- **Parameter (Total Transaction Frequency / Total Volume)**
  - Memberi dua sudut pandang: *seberapa sering* transaksi terjadi dan *seberapa besar* nilainya.
  - Mengganti ukuran seluruh visual dengan satu dashboard, tanpa perlu laporan baru.
  - Frekuensi tinggi belum tentu volume tinggi (dan sebaliknya), sehingga keduanya perlu dibandingkan.
## Manfaat
- **Pemantauan operasional**: mendeteksi kenaikan atau penurunan transaksi dengan cepat.
- **Deteksi anomali**: mengenali pola tidak wajar, termasuk transaksi dengan tujuan tidak jelas (Unknown) yang dapat menandakan masalah kualitas data atau risiko.
- **Segmentasi nasabah**: membantu menyusun strategi produk berdasarkan tipe akun dan wilayah.
- **Perencanaan kanal dan cabang**: membantu alokasi ATM, cabang, dan layanan sesuai kanal serta wilayah dengan aktivitas tertinggi.
- **Pendukung keputusan manajemen**: ringkasan cepat untuk evaluasi kinerja dan perencanaan likuiditas.

## Catatan

- Proyek ini dibuat untuk kebutuhan portofolio
Haikal
