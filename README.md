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

## Catatan

- Proyek ini dibuat untuk kebutuhan portofolio
Haikal