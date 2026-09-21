# Employee Attrition Prediction

Model prediksi kemungkinan seorang karyawan akan resign, dibungkus sebagai web app Flask dan disiapkan untuk deployment di Heroku.

Dibuat pada program **Celerates Acceleration Program - Data Analyst (MSIB Batch 4)**, 2022.

## Cara kerja

Pengguna mengisi lima variabel lewat form, lalu model mengembalikan prediksi **"Akan Resign"** atau **"Tidak Resign"** beserta tingkat kepercayaannya dalam persen.

| Input | Keterangan |
|---|---|
| `tingkat_kepuasan` | skor kepuasan kerja 0-100, dinormalisasi ke 0-1 |
| `lama_bekerja` | masa kerja dalam tahun |
| `is_pernah_kecelakaan_kerja` | 0 = tidak pernah, 1 = pernah |
| `kategori_gaji` | kategori tingkat gaji |
| `jam_kerja_perbulan` | rata-rata jam kerja per bulan |

Nilai kepercayaan diambil dari `predict_proba()`, lalu dibulatkan ke persen.

## Teknologi

Python - Flask - scikit-learn - Gunicorn

Model dan scaler disimpan sebagai pickle (`model/model_ds.pkl` dan `model/scaler_ds.pkl`) dan dimuat sekali saat aplikasi start. Input di-scaling dengan scaler yang sama seperti saat pelatihan sebelum masuk ke model.

## Menjalankan secara lokal

```bash
cd "27 SEPTEMBER"
pip install -r requirements.txt
python app.py
```

Lalu buka http://127.0.0.1:5000

## Deployment

`Procfile` dan `runtime.txt` sudah disiapkan untuk Heroku: `web: gunicorn app:app` pada `python-3.10.7`.

## Struktur

```
27 SEPTEMBER/
|- app.py            server Flask, route / dan /predict
|- model.py          load model dan fungsi prediksi
|- model/            model_ds.pkl, scaler_ds.pkl
|- templates/        index.html (form input dan hasil)
|- static/
|- requirements.txt
|- Procfile          konfigurasi Heroku
|- runtime.txt
```

Laporan lengkap proyek ada di `Prediksi Karyawan Resign.pdf`.
